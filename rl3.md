#  MUSTACHE

Mustache is a logic-less template syntax. It can be used for HTML, config files, source code — anything. It works by expanding tags in a template using values provided in a hash or object.

It is often referred to as “logic-less” because there are no if statements, else clauses, or for loops. Instead, there are only tags. Some tags are replaced with a value, some nothing, and others a series of values.

mustache.js is an implementation of the mustache template system in JavaScript. It is often considered the base for JavaScript templating. And, since mustache supports various languages, we don’t need a separate templating system on the server side.

Remember:  {{}} is calling something to template whereas {{{}}} is inserting something

 #  FLEXBOX

There is so much information and examples of using flex box that it is hard to give just a summary.  Here are some sites that guided me and a cheatsheet:

https://css-tricks.com/snippets/css/a-guide-to-flexbox/
https://css-tricks.com/video-screencasts/42-all-about-floats-screencast/
https://css-tricks.com/all-about-floats/
https://webdesign.tutsplus.com/tutorials/how-to-build-a-responsive-navigation-bar-with-flexbox--cms-33535
https://webdesign.tutsplus.com/tutorials/building-responsive-forms-with-flexbox--cms-26767
https://learn.shayhowe.com/advanced-html-css/responsive-web-design/
https://yoksel.github.io/flex-cheatsheet/


A sample snippet that I found interesting:

- module-checkout.css
	- label {
		- display: flex;
		- padding:  10px;  <<--puts space between the address and city and state, etc.
	- }
	- label select, label input {
		- flex: 1;    <<--makes the input box as wide as the form box
		- margin-left: 20px;  <<--puts space between the label and the entry box
	- }
