# SQL

I love databases!!

I did make sure that I make copious notes on how to set up new databases:

1. Create a schema.sql file with the appropriate table info - see the schema note for an example
2. Create a database with psql - 2)  Starting database in Ubuntu in this Notebook
---Can't do the below until the above is done---
1. npm install pg
2. Require ('pg')
3. Process.env.DATABASE_URL in .env file
4. Create a client using DATABASE_URL
5. Connect to db with client
6. app.listen to PORT *after* connect 
7. client.on('error', err => { throw err; });
8. --status--add--commit--push
9. Test Heroku
10. Addon for postgres
11. Set DATABASE_URL in review apps or whatever in Heroku
12. --status--add-commit--push
13. Create a table (from schema.sql)

The most confusing part was working through Ubuntu to get everything connected:
- ymcla$ psql -U postgres -h localhost
- Password for user postgres:
- postgres=# CREATE DATABASE Workouts;    <-----this will create the database - MAKE SURE TO END LINE WITH SEMI-COLON ----  unless you are going to continue on with another line of code, then put the semi colon at the end of the last code line.
- CREATE DATABASE
- postgres=# \l      <-----this will list out all postgres user databases
- postgres=# \c workouts      <-----this will connect you to the workouts database owned by postgres
- You are now connected to database "workouts" as user "postgres".
- workouts=# \q   <-----this will quit you from postgres - you need to quit to get out and link up the schema
- ymcla$ cd Desktop/shopping-site/database;    <-----this will change the directory to where the schema file is
- database[main !?]$ ls  <-----this will list out files in this location; schema needs to be one
- database[main !?]$ psql -U postgres -h localhost  <-----this will get you to the database
- Password for user postgres:
- postgres=# \c workouts;  <-----connect to database again
- You are now connected to database "workouts" as user "postgres".
- workouts-# \i schema.sql;
- CREATE TABLE
- workouts-# \dt
		          List of relations
		 Schema |   Name   | Type  |  Owner
		--------+----------+-------+----------
		 public | workouts | table | postgres
		(1 row)
- workouts=# SELECT * FROM workouts;  <-----nothing in table yet, but shows the structure
		 id | program | avgminutes | trainer | workouttype | numberofworkouts
		----+---------+------------+---------+-------------+------------------
		(0 rows)
- workouts=# INSERT INTO workouts (program, avgminutes, trainer, workouttype, numberofworkouts)  <-----using schema titles and no semi colon since there is another line of coding that is the values for each
- workouts-# VALUES ('21 Day Fix', '30 minutes', 'Autumn Calabrese', 'Weights and Cardio', '10');
		INSERT 0 1  <-----shows that a line was inserted
- workouts=# SELECT * FROM workouts;   <-----shows the info that was added and automatically assigned the ID#
		 id |  program   | avgminutes |     trainer      |    workouttype     | numberofworkouts
		----+------------+------------+------------------+--------------------+------------------
		  1 | 21 Day Fix | 30 minutes | Autumn Calabrese | Weights and Cardio | 10
		(1 row)
