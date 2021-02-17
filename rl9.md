# Refactoring

I really enjoyed refactoring the server.js to be more clean and then to create the modules and such so that everything had a home.

When we refactored last time, instead of having locations, weather, yelp, movies, etc. in our server.js, we created a .js page in a modules folder for each of them.  That is where those "handlers" were housed.  Then in the server.js, we just saw them being required for wehn they are called and used.

Here is an example of a server.js before refactoring:
'use strict';

require('dotenv').config();


const express = require('express');
const app = express();

const pg = require('pg');

const client = new pg.Client(process.env.DATABASE_URL);
client.on('error', err => console.error(err));

const superagent = require('superagent');

const cors = require('cors');

const PORT = process.env.PORT || 3000;

app.use(express.static('./public'));
app.use(cors());


app.get('/', (request, response) => {
  response.send('You have found the home page! ');
});


app.get('/location', locationHandler);
app.get('/weather', weatherHandler);
app.get('/parks', parksHandler);
app.get('/yelp', yelpHandler);
app.get('/movies', moviesHandler);


//weather

function weatherHandler(request, response) {
  const city = request.query.search_query;
  const url = 'https://api.weatherbit.io/v2.0/forecast/daily';

  superagent.get(url)
    .query({
      city: city,
      key: process.env.WEATHER_API_KEY,
      days: 4
    })
    .then(weatherResponse => {
      let weatherData = weatherResponse.body; //this is what comes back from API in json
      console.log(weatherData);

      let dailyResults = weatherData.data.map(dailyWeather => {
        return new Weather(dailyWeather);
      })
      response.send(dailyResults);
    })

    .catch(err => {
      console.log(err);
      errorHandler(err, request, response);
    });
}
//parks

function parksHandler(request, response) {
  // const state_code = response.query.state_code;
  const url = 'https://developer.nps.gov/api/v1/parks';


  superagent.get(url)
    .query({
      // q: 'parks?',
      stateCode: 'ID',//hard coded state code for the moment
      api_key: process.env.PARKS_API_KEY
    })

    .then(parksResponse => {
      let parksData = parksResponse.body; //this is what comes back from API in json
      console.log(parksData);

      let parksResults = parksData.data.map(eachPark => {
        return new Parks(eachPark);
      })
      response.send(parksResults);
    })

    .catch(err => {
      console.log(err);
      errorHandler(err, request, response);
    });
}

//location

function getLocationFromCache(city) { //<<--this is the function for using the database to cache
  const SQL = `  --<<--these are tic marks not single quotes
    SELECT * 
    FROM location2
    WHERE search_query = $1
    LIMIT 1  --<<--brings back only one of the rows for that city
    `;
  const parameters = [city];

  return client.query(SQL, parameters);
}

function setLocationInCache(location) { //<<--this is a function for using the database to cache
  const { search_query, formatted_query, latitude, longitude } = location
  const SQL = `  --<<--these are tic marks not single quotes
    INSERT INTO location2 (search_query, formatted_query, latitude, longitude)--<<--location2 is the name of the database
    VALUES ($1, $2, $3, $4)  --<<--will take in the results
    RETURNING *
    `;
  const parameters = [search_query, formatted_query, latitude, longitude];

  return client.query(SQL, parameters) //<<super duper common error - promisey stuff inside of a function, return a promise that says we're done
    .then(result => {
      console.log('Cache Location', result);
    })
    .catch(err => {
      console.log('Failed to cache location', err);
    })
}

function locationHandler(request, response) { //<<this handler works
  if (!process.env.GEOCODE_API_KEY) throw 'GEO_KEY not found';

  const city = request.query.city;

  getLocationFromCache(city)
    .then(result => {
      console.log('Location from cache', result.rows)
      let { rowCount, rows } = result;
      if (rowCount > 0) {
        response.send(rows[0]);
      }
      else {
        return getLocationFromAPI(city, response); //<<--have to pass the response so that it will get picked up by the getLocationFromAPI response.send(location)
      }
    })
}

function getLocationFromAPI(city, response) {
  console.log('Requesting location from API', city);
  const url = 'https://us1.locationiq.com/v1/search.php';
  superagent.get(url)
    .query({
      key: process.env.GEOCODE_API_KEY,
      q: city,
      format: 'json'
    })
    .then(locationResponse => {
      let geoData = locationResponse.body;
      // console.log(geoData);

      const location = new Location(city, geoData);

      setLocationInCache(location) //<<--if we don't already have it, then save it too, BUT wait to find out and .then set
        .then(() => {
          console.log('Location has been cached', location);
          response.send(location);
        });

    })
    .catch(err => {
      console.log(err);
      errorHandler(err, request, response);
    });
}

Here is an example of the server.js refactored:

'use strict';

require('dotenv').config();

const express = require('express');
const cors = require('cors');
const { json } = require('express');
const pg = require('pg');

const client = require('./modules/client');


const PORT = process.env.PORT;
const app = express();

app.use(cors()); //<<--need to have the inner parenthesis

app.get('/', (request, response) => {
  response.send('City Explorer Goes Here!');
});

app.get('/bad', (request, response) => {
  throw new Error('oops');
});

const locationHandler = require('./modules/locations');
const weatherHandler = require('./modules/weather');
const yelpHandler = require('./modules/yelp');

app.get('/location', locationHandler);
app.get('/weather', weatherHandler);
app.get('/yelp', yelpHandler);


//where books was originally

//Has to be after stuff loads too
app.use(notFoundHandler);

//Has to be after stuff loads
app.use(errorHandler);

//Make sure the server is listening for requests - after app.gets and app.uses and errorHandlers
client.connect()  //<<--keep in server.js
  .then(() => {
    console.log('PG connected!');

    app.listen(PORT, () => console.log(`App is listening on ${PORT}`)); //<<--these are tics not single quotes
  })
  .catch(err => {
    throw `PG error!:  ${err.message}`  //<<--these are tics not single quotes
  });



//Route handlers
function errorHandler(error, request, response, next) {
  console.error(error);
  response.status(500).json({
    error: true,
    message: error.message,
  });
}

function notFoundHandler(request, response) {
  response.status(404).json({
    notFound: true,
  });
}