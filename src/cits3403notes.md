---
title: CITS3403 Notes
description: Uni Notes
layout: default.hbs
---

<a class="nav-link" href="notes.html">cd -</a>

>Written by Jeremy Butson 2024 based on UWA CITS3403 Lecture Notes

# Introduction
## ==================================
## Brief History:
- DoD created ARPA, now DARPA:
	  wanted communications, program sharing, remote computer access
- NSFnet - 1986:
	National Science Foundation
	Initially connected 5 supercomputer centres, spreading to other academic institutes and labs
	Became the network for all by early 90s, the internet
- The Internet:
	If computers are close together; local area network (LAN), wide area (WAN)

## How the Internet Works:
- Protocols:
	  Computers "speak" a common language
		  signal another computer
		  identify requesting computer
		  transmit messages in blocks
		  retransmit if messages fail
		  detect errors
		  signal transmission complete
		  terminate connection
- TCP/IP:
	Transmission Control Protocol/Internet Protocol

## Client-Server Architecture:
- User accesses the web via software (browser)
- Browsers locate and display info
- browser communicates user requests to the server
- Web page is delivered

# HTML
## =====================================

## Hyper Text Markup Language:
- General layout of documents
- Clear specifications on error handling
- Not breaking the web (backward compatibility)
- Aiming at easier authoring of web apps

## Basic Syntax:
```html
<!DOCTYPE html>
<html>
<head>
	<title>Page Title</title>
</head>

<body>
	<h1>Heading</h1>
	<p>Paragraph</p>
	<table border="1" cellpadding="1">...</table>
	<!-----COMMENT------>
</body>
</html>
```

## Font Styles and Sizes:
- Generally just do in [[3. CSS|CSS]] however is possible in HTML:
```html
<b> for bold </b>
<i> italics </i>
<big> larger </big>
<small> smaller </small>
<tt> monospace </tt>

&amp, &lt, &gt, &quot, &apos, &frac34, &deg, &nbsp
```

## Inserting Images:
```html
<img src="image.png" alt="image text" style="width:300px;height:200px;">
```

## Hypertext Links:
`<a href="Link">to page</a>`

## Lists:
```html
<h3>Shopping List:</h3>
	<ul>
		<li>Milk</li>
		<li>Eggs</li>
	</ul>
```

## Tables:
```html
<table style="width:100%" border="border">  
  <tr>  
    <th>Company</th>  
    <th>Contact</th>  
    <th>Country</th>  
  </tr>  
  <tr>  
    <td>Alfreds Futterkiste</td>  
    <td>Maria Anders</td>  
    <td>Germany</td>  
  </tr>  
  <tr>  
    <td>Centro comercial Moctezuma</td>  
    <td>Francisco Chang</td>  
    <td>Mexico</td>  
  </tr>  
</table>
```
![[Pasted image 20240226104914.png]]

## Layout in HTML5:
![[Pasted image 20240226105135.png]]

## Forms:
- A way to get information from the browser to a server
- HTML has tags for widgets such as checkboxes
- When "SUBMIT" is clicked, the values are sent to a server
```html
<form action="/action_page.php">
	<fieldset>
		<legend>Personal Information:</legend>
		First Name:<br>
		<input type="text" name="firstname" value="mickey">
		<br>
		Last Name:<br>
		<input type="text" name="lastname" value="mouse">
		<br><br>
		<input type="submit" value"Submit">
	</fieldset>
</form>
```
- Submit does two things:
	- encodes the data of the form
	- requests that the server execute the server-resident program specified as the value of action attribute of `<form>`
- HTML5 browsers support basic validation on email, url and tel types:
	- `<input id="phone" name="phone" pattern="\d{8}" type="tel">`

# CSS
## =====================================


**CSS** or Cascading Style Sheets is:
- a stylesheet language for the web
- used to specify the presentation (layout and style) of markup languages
- can be applied to any XML documents as well as [[2. HTML|HTML]]
```css
body {
	backgroudn-color: blue;
	color: white;
	text-align: center;
	font-family: verdana;
	font-size: 20px;
}
```

## Advantages of CSS:
- Separation of content and presentation
- Advantages for web:
	- Speed
	- Maintainability
	- Accessibility
	- Portability
	- Reduced work
	- Consistency

## Why Cascading?
- 3 types:
	- Inline - applies to a single tag only
	- Document - \<head> elements and applies to whole document
	- External - separate files, usually on server and can be applied to any number of documents in their \<head> element
- Lowest level has precedence

## Inline:
- Attribute of almost any tag
```html
<p style="color:yellow">styled text</p>
```

## Document:
```html
<style>
	p {
		color:yellow;
	}
</style>
```

## External:
- Has to be specified in head of HTML doc
```html
<link rel="stylesheet" type="text/css" href="style.css"></link>
```

## Selectors:
- Determines which elements a style applies to
```css
*{...} UNIVERSAL
p{...} ELEMENT
.important{...} CLASS
.important:hover{...} PSEUDO-CLASS
important::first-letter{...} PSEUDO-ELEMENT
s1,s2,s3{...} GROUP
```

## Property Groups:
- Main Ones:
	- text
		- font-size: ;
		- font-style: italic;
		- font-weight: bold;
		- font: list of properties;
		- text-decoration: none;
		- letter-spacing: 2;
		- text-indent: 20%;
		- text-align: left;
		- float: left; (to get text to flow around image)
	- background
	- borders
		- border-style: solid;
		- border-width: medium;
		- border-color: red;
	- the box model
		- padding-top:30px; (inside border)
		- margin-top:20px; (outside border)
		- width / height:20px; (content)
	- color
	- table
	- list
		- list-style-type: square;
	- position
		- static = go with normal
		- relative = element is offset relative to its normal flow position
		- absolute = element is offset relative to its most recently positioned ancestor. Element is removed entirely from normal flow
		- fixed = element offset relative to the fixed viewport
		- sticky = switches between relative and fixed depending on scroll position


# Bootstrap
## =================================
A [[3. CSS|CSS]] framework. To include in your page, you can download and host the code yourself, or reference a Content Delivery Network in the header of your webpage. Bootstrap consists of a CSS, JavaScript and optional theme files. 
```html
<head>
	<link rel="stylesheet" href="bootstrapfile.css">
	<script src="jquery.js"></script>
	<script src="bootstrapfile.js"></script>
</head>
```

## Grid System:
- Bootstrap uses rows of 12 columns for layout. 
`<div class="col-sm-3>...</div> 
`<div class="col-sm-3>...</div>
- fills the whole screen
- columns can be nested, so a span of eight columns can be divided into 12

## Tables:
```html
<tbody>
	<tr>
		<td>First column, first row</td>
		...
</tbody>
```

## More Info (Yay I love lecturers):
- https://www.w3schools.com/bootstrap5/


# JavaScript
## ===================================
## What is JavaScript?
- A.K.A. JS
- High-level, dynamic, untyped and interpreted language
- An alternative to server-side programming
	- servers are often overloaded
	- client processing is quicker
- Can interact with the internal model of the web page to alter the page dynamically

## Events:
- User's actions are referred to as *events*
- Such as mouse-clicking/interacting

## Executing JS:
- The browser: every modern browser can execute JS, however a HTML file must call the JS function
- NodeJS: a server-side JS environment, more like a traditional console (e.g. python)

## JS on the Browser:
- Several ways to include JS:
	- Inline in a tag attribute (``on click``)
	- Included in the document in the body of a ``<script>`` tag
	- From an external file referenced via a URL, using ``src`` attribute of the ``<script>`` tag

## JS I/O:
- The standard output for JavaScript embedded in a browser is the window displaying the page in which the JavaScript is embedded
- Writing logs or error messages to the document object is now considered bad practice. For simple debugging use ``console.log``, which outputs to console (WOW!)
- To output information to the user, you can use the ``alert`` or ``confirm`` 
- To get input from user, you can use ``prompt``

## Basics of JavaScript
## Variables:
- variable names must start with a dollar `$` symbol, an `_` or any letter and must continue with any combination of these plus numbers. They are usually written in ``camelCase``
- Variable assignment is performed using `=`
- Variables are declared using `let`, `const`, `var` or nothing at all:
```js
let z = x + y;
const x = 6;
var stopFlag = true;
zz = z;
```
- Good rule of thumb is use `let` by default

## Syntax:
`// single line comment`
```js
/*
multiple
line
comment
*/
```
- Statements *should* be terminated with a `;`, however the interpreter will insert the semicolon, but you should not rely on it as it may not put it where you want

## Primitives and Objects:
- Primitive types: Number, String, Boolean, null, undefined
- Some object types: Function, Array, Date, Math, etc.
- Object properties are accessed by `.`
	- `Math.sin()`
- Objects are automatically collected when there no longer exists any reference to them

## Numbers:
- All `Number`s are represented internally as double-precision floating-point
- All standard arithmetic operators, incrementors and compound assignment operators are available in JavaScript
- Convert a string to an integer by using ``parseInt("124")``
- Invalid operators return a special value `NaN` or "Not a Number"
	- This can be checked via `isNaN(value)`

## Strings:
- A string literal can either be double or single quotes
- `\\` to use a literal backslash
- `\n` for new line
- `\t` for tab
- Characters are single length strings
```js
charAt(number_value); //returns character at spot
indexOf("a"); //returns index of character
substring(0, 3); //returns substring from position 0 to 3
toLowerCase();
toUpperCase();
toString(1234); //returns string of the number
"con" + "cat" = "concat";
```

## Booleans:
- JavaScript is much the same as other languages, return values of `true` and `false`
- `!`, `&&` and `||` can all be used
- These are also equal to `1` and `0` respectively

## Loops:
```js
let triangle = 0;
for (let i = 1; i <= 3; i++) {
	triangle += i;
}
//triangle = 6
```

## Arrays:
- Lists of elements indexed
- Begin at zero, size can be modified
```js
var index;
var fruits = ["banana", "orange"];
for (index = 0; index < fruits.length; index++){
	text += fruits[index];
}


let a = Array(10);
//makes an array of length 10
let b = Array();
//creates an empty array
let c = Array(10, 2, "three", "four");
//create array of length 4 with the 4 elements contained
```
![[Pasted image 20240314152122.png]]

## Functions
```js
function <name> (<parameters>) {
	<statements>
}
```
- Parameters do not have a defined type
- Parameters named in function definitions are *formal parameters*
- Parameters passed in are *actual parameters*
- A property array called arguments holds all the actual parameters:
```js
function findMax(){
	let max = -infinity;
	for (let i = 0; i < arguments.length; i++){
		if (arguments[i]  > max){
			max = arguments[i];
		}
	}
	return max;
}

findMax(4,5,6);
```

## Scopes
- The scope is the range of statements over which it is visible
- 3 types:
	- Global
	- Function
	- Block
- Different variable declarations differ what scope:
	- `const` and `let` have block-level scope
	- `let` can be changed within the block
	- `var` outside of a function has global scope, within, they can only be used within that function
	- Undeclared variables can be used *anywhere*, **DON'T DO IT**

## Inner Functions:
- A function inside another function
- Allow us to use *closures*
	- A closure is the local variables for a function - kept alive after the function has been returned


## Objects
- Collections of name-value pairs:
	- names are Strings
	- values can be any JS value
- Properties can be accessed using `.`
	- `Obj.name = "Matthew Daggit"`
- Alternatively:
	- `Obj["name"] = "Matthew Daggit"`
- `Object.prototype` allows you to modify an object's prototype at run time
- Constructors are functions that create and initialize properties for new objects
```js
	function Person(first, last, age, eye) {
		this.firstName = first;
		this.lastName = last;
		this.age = age;
		this.eyeColor = eye;
	}
	
	var myFather = new Person("John", "Doe", 50, "blue");
```
- ``this`` refers to the current object, in the scope of a browser, that means the window displaying HTML

# DOM
## ===================================
>The Document Object Model

- Is a platform and language-neutral interface that will allow programs and scripts to dynamically access and update content, structure and style of documents
- It mimics the "tree structure"

## The BOM Execution Environment
- The DOM tree is just one subsection of a larger ***Browser Object Model*** tree that also includes nodes for the execution environment in a browser, which includes:
	- The type of browser
	- Cookies
	- History
	- Screen size
	- Geolocation
	- Local storage

## Accessing Elements
`x.getElementsByTagName("p")
- will return `<p>` elements inside the node represented by the element object x
- also:
``getElementById("imageOne")``

## DOM Modification
```js
insertBefore
replaceChild
removeChild
appendChild
open()
close()
write()
writeIn()
```

## BOM Functions
``window.navigator`` object contains information about browser:
```js
appCodeName //code name of browser
appName //name of browser
appVersion //version of browser
cookieEnabled //determines whether cookies are enabled
geolocation //returns a geolocation object, used to find user's positio
language 
onLine //determines whether the browser is online
platform 
product //returns engine name
userAgent
```
``window.history`` contains methods for moving backwards and forwards:
```js
back()
forward()
go()
length
```

# Client-Side JavaScript
## ===================================
## Event-Driven Programming:
- Flow of program is determined by sensor outputs or user actions
- Program loop:
	- event detection
	- event handling
- Common events:
```js
onblur
onchange
onclick
ondblclick
onfocus
onkeydown
onkeypress
onkeyup
onload
onmousedown
onmousemove
onmouseout
onmouseover
onmouseup
onreset
onselect
onsubmit
onunload
```
- Usually registered by:
```js
button = document.getElementsById("myButton");
button.addEventListener("click", myHandler, false);
#where myHandler is the code and there is a myButton in the HTML
#false means by default it "bubbles up"
```

## What is J-Query?
- Makes DOM manipulation and other client-side JavaScript much more concise and easier to write
- Imported by:
```html
<script src = "https://code.jquery.com/jquery-3.7.1.min.js"></script>
```
- Basic jQuery syntax: `$(selector).action()`
	- `$` is an abbreviation for jQuery
	- `selector` is a query to find HTML elements (syntax is a superset of CSS)
	- `action` is a jQuery function such as:
		- `text()`
		- `html()`
		- `val()`
		- `attr()`
	- Can also be used for DOM like events:
```js
$("p").click(() => {
	$(this).slideDown("slow");
})
$("p").on( {
	mouseenter:function(){
		$(this).css("background-color", "lightgray");
	},
	mouseleave:function(){
	
	},
});
```
- Commonly `$(document).ready(() => {` wraps jQuery so that it is waiting until the document is fully loaded.


# HTTP and AJAX
## ===================================
## HTTP Requests
#### Structure of HTTP Requests and Responses
- Updating when something happens on a server (a message is sent in a forum, submitting a form, etc.)
- Client-server-architecture: Client sends a HTTP request to a server, server receives request, formulates and sends a response, protocol becomes once again stateless.
- Methods include:
	- GET, POST, UPDATE, DELETE
- This is included in the request, as long with the URL and message body
- A response reports the status (200 == OK, 404 file not found), a header and message body
```js
//GET requests
xhttp.open("GET", "demo_get2.asp?fname=Henry&lname=Ford", true); //true is whether its asynchronous
xhttp.send();

//POST requests
xhttp.open("POST", "ajax_test.asp", true);
xhttp.setRequestHeader("Content-type", "application/x-www-form-urlencoded");
xhttp.send("fname=Henry&lname=Ford");

//PUT request to replace data on server

//readystate is the progress of req, onreadystatechange is a callback func
function loadDoc() {
	var xhttp = new XMLHttpRequest();
	xhttp.onreadystatechange = function() {
		if (this.readystate == 4 && this.status == 200) { //status == OK
			document.getElementById("demo").innerHRML = this.responseText;
		}
	};
	xhttp.open("GET", "ajax_info.txt", true);
	xhttp.send();
}
```
#### Asynchronous Communication
- We do not know when/if the server will respond
- JavaScript is single-threaded so must run each statement in order, but the environment that JavaScript runs in is not single-threaded, so we can write a function with a function as the parameter
#### XMLHttpRequests
- Modern browsers have this object to handle requests to and responses from a server
#### jQuery and HTTP Requests
- jQuery `get` function will send a GET request to a URL and passes the data to a callback function.
```js
$("button").click(function() {
	$.post("demo_test_post.asp", fucntion(data, status){
		alert("Data: " + data + "\nStatus: " + status);
	});
});
```
- jQuery `post` function will send a POST request, with data to a URL and passes the response to a callback function.
```js
$("button").click(function() {
	$.post("demo_test_post.asp",
	{
		name: "Donald Duck",
		city: "Duckburg"
	},
	function(data, status) {
		alert("Data: " + data + "\nStatus: " + status);
	});
});
```

## AJAX
- Asynchronous JavaScript and XML
- A protocol for what information should be sent
- For JS to communicate directly with a server, we require a format, which is usually XML and JSON
- XML:
	- All data is held within tags, much like HTML
- JSON: 
	- stores data in the syntax of JS

# Flask and Server-Side Rendering
## ===================================
>A web server is simply a program running on a computer connected to the internet that responds to requests from other computers on the network. This is also referred to as back-end development (so now full-stack development).


#### Different Stacks
- LAMP, Ruby on Rails or Django (Python)
- We will use:
	- Flask: a micro framework, that allows us to write our backend in Python
	- SQLite: a lightweight database management system
	- AJAX: provides the method for transmitting data between the browser and server
	- jQuery: to have bindings for AJAX on the client side.

## Flask
- Micro framework that can be used to create a server program that will run on any machine and has few dependencies.
- Basic "Hello World" Flask application in an `app.py` file
```python
from flask import flask
app = Flask(__name__)
@app.route("/")     #annotate with this, in this case top level
def hello():
	return "Hello World"
if __name__ == "__main__":
	app.run()
```
- Single file structure does NOT scale well
- Create a Python package that will contain all the code we need for the web app
- The `__init__.py` file creates an instance of the Flask class and `routes.py` contains request handlers
- Then we need a file at top level to support the app. 
```python
#app/__init__.py
from flask import flask
app = Flask(__name__)
from app import routes

#app/routes.py
from app import app
@app.route("/")              #this is an endpoint
@app.route("/index")         #can be multiple endoints
def index():
	return "Hello World"

#microblog.py
from app import app
```
- Endpoints can also use variables: `@app.route("/user/<username>")` where `<username>` is a variable

#### Endpoints
- By default, endpoints are only available as `GET` requests, you can add others though:
```python
@app.route("/login", methods=['GET', 'POST'])
def login():
	if request.method == 'POST':
		do_the_login()
	else:
		show_the_login_form()
```
- You can use `url_for` function to retrieve the URL for a given endpoint

#### Server-side vs Client-side Rendering
- Two main approaches:
	- Server-side rendering:
		- the server builds the HTML when it receives the request and sends it to the client
	- Client-side rendering:
		- the server sends JS and an HTML skeleton to the client and the client can then request JSON and build the HTML using AJAX and jQuery

#### Flask Server-side
- Most basic approach:
```python
from app import app
@app.route("/")              #this is an endpoint
@app.route("/index")         #can be multiple endoints
def index():
	user = ("username" : "Miguel")
	return '''
<html>
	...
</html>'''
```
- Alternatively, we can use templates, Flask uses **Jinja** for this
- We would generally have a `template` directory, with variables distinguished by `{{...}}`
```html
<!--app/templates/index.html-->
<html>
	<head>
		<title>{{title}} - Microblogs</title>
	</head>
	<body>
		<h1> Hello, {{user.username}}</h1>
	</body>
</html>
```
```python
#app/routes.py
from flask import render_template
from app import app

@app.route("/")
@app.route("/index")
def index():
	user = {'username': 'Miguel'}
	return render_template("index.html", title = "Home", user = user)
```

#### Running in VSCode
`> set FLASK_APP=main.py`
`> $env:FLASK_APP = "main.py"`
`> flask run`
``

# Flask and Client-Side Rendering
## ===================================
#### Single Page Applications (SPA)
- Services where the entire website is provided via client-side rendering:
	- Browser/client does heavy lifting
	- Server only provides data
	- The user never navigates to a new URL
- Pros of SPA:
	- Less load on server
	- A more responsive client
	- Genuine separation between content and presentation
- Cons of SPA:
	- Longer load time
	- Search engine optimisation (SEO) can be an issue
	- Navigation (forward and back buttons) can be an issue

#### Client Side Rendering w/ Web Sockets
- HTTP requests are useful for providing dynamic content but are heavy weight and expensive to setup
- Many web applications depend on real time interaction
- Web sockets provide full duplex communication
- Supported in flask via the `flask-socketIO` package
- `socketIO` is good for message passing chat or distributed games
- `WebRTC` can be used for direct video and audio
- Clients connect to a socket on a server and then the server can push messages to clients
- Sockets mirror routes of a flask project, however they listen for messages and actions and broadcast those
- The server works as a common blackboard for the session and clients listen via jQuery

# Databases
## ===================================
#### Architecture
- Design patterns describe re-usable design concepts, including:
	- Client-server
	- Pipe and filter
	- Blackboard

#### Model-view-controller Pattern (MVC)
- Model is the data
- Controller receives, updates, queries
- View is presentation and assets
- Advantages:
	- Can alter view without altering the model
	- Can swap database without altering view
	- Specialist developers can work on each bit
	- Can support multiple views
	- Easier to test parts in isolation
- The model is the python objects
- The view is the HTML
- The controller is the code in `routes.py`

#### Mock-ups of views
- Wireframes show the basic layout and functionality of a user interface
- Various tools, or by hand

#### Implementing Models
- A model is an object that is paired with an entity in a database
- There is an **Object Relational Mapping** (ORM) linking the data to the models in the application

#### Relational Databases
- Store data as a set of relations
- Each row is an entity, each column an attribute
- Each has a Primary Key
- Linkages are Foreign Keys
#### Database Management System (SQLite)
- A database management system (DBMS) is an application that controls access to a database
- SQLite as its small and simple
- SQLite commands start with a `.` 
```sql
sqlite3 app.db #creates database

CREATE TABLE contact_groups (
	contact_id integer,
	group_id integer,
	PRIMARY KEY (contact_id, group_id),
	FOREIGN KEY (contact_id) REFERENCES contacts(contact_id)
	ON DELETE CASCADE ON UPDATE NO ACTION
);

.database #shwos file path
.table #lists tables
.schema tableName #shows the schema for a table
.indexes
.exit
```
- In SQL-Alchemy:
```python
class Student(db.model):
	uwa_id = db.Column(db.String(8), primary_key = True)
	name = db.Column(db.String(120), nullable = False)
	group_id = db.Column(db.Integer, db.ForeignKey("group.group_id"),                        nullable = True)
	group = db.relationship("Group", back_populates = "students")
```
- Must use `db.session.commit` in order to commit changes
	- Useful so that error messages can be returned, while not having to unwind the database to get rid of errors
- `users = User.query.<SQL syntax>.all()`

#### Database Migration in Flask
- How can you dynamically add things in a table?
- Like version control for your database
- Each is accompanied with *upgrade* and *downgrade* scripts

# Security
## ===================================
#### Breakdown
- Security on the web depends on trust. There are several elements to this:
	1. The web server needs to be confident that someone accessing data is authorised
		- Achieved via session/token-based authentication
	2. The user needs to know that the site they are visiting is the one they intend to
		- Achieved via SSL Certificates
	3. Both the server and the client need to be confident that no one in the middle is accessing unauthorised data
		- Achieved via HTTPS (HTTP Secure)
	- Underlying all of these are public-key encryption and cryptographic hashing

#### Public Key Encryption
- Secure communication is based on Public Key Encryption. There is an encryption and decryption function
- A public-private key is a pair of keys `pub` and `priv` such that
	$x = D_{priv}E_{pub}(x)$      $x = D_{pub}E_{priv}(x)$
	you cannot work out `priv` even if you know `pub`
- "Salting" is added to each user, differently, so that the hash cannot be computed via a rainbow table

#### Hashing
- Secure data storage is based on Cryptographic Hashing
	- A cryptographic hash function is a function hash that takes a string or arbitrary length and returns a fixed length integer such that:
	- Essentially it computes a number from a stream of data, in such a way that it's very difficult to fabricate data with a certain hash
	- Related to hashing for hash tables, but the hash function must satisfy the much stronger properties above to be cryptographically secure

#### Session-based User Authentication
- HTTP is stateless, application is not!
- To track a user's session, we need to have them register so we can associate a username and password with them. The password is hashed, and the result is stored in the database
- When someone logs in, they provide the same password
- If successful, the server's response contains a cookie with the session ID and hash
- Whenever a future HTTP request is made, the server checks the session ID in the cookie and recomputes hash to check the ID hasn't been altered

## Attacks on Session Based Protocols
#### Impersonation Attack
- Sessions allow the server to authenticate the user. However, remember the network is still fundamentally insecure
- Without extra security, the easiest attack is an impersonation attack
	- The network redirected the user's request to a fake user
	- The fake server acts just like the real server
	- User submits passwords, private data etc. to the fake server

#### SSL Certificates
- An impersonation attack can be prevented by the server a certificate that it's real via the Secure Socket Layer protocol
- Certificates are provided by a trusted third party known as a Certificate Authority (CA)

#### Man-in-the-middle Attack
- Even when using certificates, the network can still perform man-in-the-middle attacks
	- All traffic is first redirected to the attacker and then forwarded to the real server
	- Because the user is interacting with the real server, the certificate check passes
	- However, the attacker still gets access to all the information sent back and forth, including the signed cookies

#### Encrypted Sessions With SSL
- We cannot prevent the network from redirecting the messages via a third party, so we must encrypt our messages
- SSL also includes a public key encryption process to enable secure HTTP requests
- After the initial certificate handshake establishing that the server has the public key, both parties use a key distribution protocol to generate a shared set of private session keys
- They then use these keys to encrypt all future traffic during that session

#### HTTPS 
- In theory SSL can be used to encrypt any data between two end points
- In practice, the most common type of traffic is simply HTTP requests. Using HTTP over SSL is known as HTTPS

#### Cross-Site Request Forgery (CRSF) Attack
- A signed cookie from their server in your browser:
	- Cookies are transferred automatically when making the request to the domain they are associated with, and therefore the signed cookie is sent to the server
	- The server checks the cookie, which passes as it is real, and therefore thinks the request is from the user and the transfer goes through

## Token-Based User Authentication
#### Downsides of Session-Based Authentication
- Session-based authentication works for web-based applications but has several drawbacks
	- It requires the application to track all user sessions which may not scale well
	- HTTP requests are sent in plain text, and passwords should never be transmitted or stored in plain text
	- The user may be accessing the application via a mobile application where there is no such thing as a cookie
	- It is inherently stateful, which may not be necessary
	- It requires users to have registered their information with the server

#### Tokens and JWT
- From a cryptographic perspective, tokens are the same as session cookies, but unlike session cookies, tokens are not usually used to authenticate a user and retrieve the state on the server
- Instead, they authorise the holder to perform a particular action
- Crucially, it is not necessary for the server to know who the requester is

#### Advantages of Tokens
- By sacrificing the ability to store state, tokens have many advantages over sessions:
	- Validating a token doesn't require querying the database
	- Tokens aren't vulnerable to CRSF attacks
	- They don't require cookies and therefore work on mobile apps
	- Tokens can store a set of privileges, rather than just one

# Testing
## ===================================
Many various ways; in order of effectiveness:
- Code reviews: peer reviews
- Testing: providing test cases
- Formal verification: building precise specifications of correctness and proving code meets these specifications

#### Types of Tests
- Unit tests: test an individual function to ensure it behaves correctly
- Integration tests: execute each scenario to make sure modules integrate correctly
- Systems tests: integrate real hardware platforms and test their behaviours
- Acceptance tests: run through complete user scenarios via UI

#### Unit Tests
The purpose of a unit test is to test an individual function, using 2 to 5 per function.
Properties include:
- Automated
- Repeatable
- Run quickly
- Pinpoint the failure
- Limited in scope
Often "test doubles" are used, such as:
- Fakes: objects with working implementations, but not the same as the production environment, for example, the full database has been replaced by a fake
- Stubs: objects that hold predefined data to respond to specific requests
- Mocks: like stubs but remember the calls they receive

#### The Python `unittest` Module
Provides several classes and functions:
- **Test Fixtures** prepare for a test case, called `setUp` and `tearDown` which run before and after
- **Test Case** is the standard class for running a test, specifying fixtures and functions to execute
- **Test Suite** allows tests to be run together and run at the same time
- **Test Runner** responsible for running the test

#### Creating a Mock DB in Flask
`SQLALCHEMY_DATABASE_URI = "sqlite:///:memory"` creates a non-persistent database in memory rather than as a file on disk.
`Config` class holds the options shared between all configurations, subclasses hold options specific to a particular configuration:
```python
class Config:
	SQL_ALCHEMY_TRACK_MODIFICATIONS = False
	SECRET_KEY = os.environ.get("FLASK_SECRET_KEY")
class DeploymentConfig(Config):
	SQLALCHEMY_DATABASE_URI = "sqlite:///" + os.path.join(basedir, 'test.db')
class TestConfig(Config):
	SQLALCHEMY_DATABASE_URI = "sqlite:///:memory"
	TESTING = True
```

#### Writing Unit Tests
The name MUST begin with `test` and use `assert` methods to define whether it passes.
```python
def test_password_hashing(self):
	s = Student.query.get("01234587")
	s.set_password("bubbles")
	self.assertTrue(s.check_password("bubbles"))
	self.assertFalse(s.check_password("rumbles"))
```
- This is then run using `python -m unittest <filename>`

#### System Tests
Integrate real hardware platforms and test their behaviour. In the web, this means testing the behaviour of how the application works in a browser. 
**Selenium** is one possible program that can be used to automate browsers to run test cases; two variations:
- Selenium IDE: a browser plugin that can record interactions and run them back to confirm the outcome stays the same
- Selenium WebDriver: a set of tools for scripting system tests

# RESTful APIs
## ===================================
>An *Application Programming Interface* (API) is a means to provide the logic and data structures of your app as a service to other developers so they can embed the functionality into different applications and customise the UI

The most common API design is based on REST APIs, client-side page rendering uses what are essentially REST APIs designed for private rather than public use

### Principles of REST
- **REpresentational State Transfer** (REST) is an architecture for the web that describe interactions with web-based resources
#### The 6 Characteristics of REST
1. Client-server model: sets out different roles of the client and server in the system, should be clearly differentiated as separate processes, the interface is through HTTP and the transport through TCP/IP
2. Layered System: there does not need to be a direct link between the client and the server, the client does not need to distinguish between the actual server and an intermediary, and the server does not need to know whether it is communicating directly with the client
3. Cache: states that it is acceptable for the client or intermediaries to cache responses to requests and serve these without going back to the server every time. This allows for efficient operations of the web. Anything encrypted cannot be cached by an intermediary, saves reloading the same static files.
4. Code on Demand (Optional): can provide executable code in responses to a client
5. Stateless: servers should not maintain any memory of prior transactions and every request from clients should include sufficient context for the server to satisfy the request
6. Uniform Interface: clients in principle do not need to be specifically designed to consume a server

### Designing a REST API
- Standard CRUD operations are CREATE, READ, UPDATE and DELETE, typical ways to interact with our data model
- In web apps, they are mapped to HTTP methods: POST, GET, PUT/PATCH and DELETE

### REST in Flask
- Can augment a Flask web app so that it provides a REST API but shares the database with the web app
- The REST API provides a web interface to the backend data model
- Flask application looks like:
```
myapp\
	app\
		__init__.py
		FORMS.py
		models.py
		controllers.py
		routes.py
		templates\
			base.html
			...
		static\
			bootstrap.css
			...
		api\
			__init__.py              //initialise the api
			auth.py                  //handle token based auth
			models_api.py            //handle api routes for each model
			token_api.py             //handles tokens
```
- **TOKENS**: access to many APIs are controlled by tokens, the token API allows a logged-in user to generate a token that allows access to the API


# Deployment
## ===================================
### Upgrading to Production-Grade Tools
- We used Flask and SQLite to allow fast development
- For security and scalability reasons, these aren't particularly suitable
- SQLite => MySQL
- Flask => Gunicorn and nginx

### Why Replace SQLite?
- MySQL is a server database rather than an embedded database, meaning it can run on entirely separate machines and act like a server for multiple web servers
- Means better in production and scales well
- Also has inbuilt authentication methods that keeps your data secure even if your VM is compromised
- Easy to replace

### Why Replace Flask Server?
- In a production system, common to decompose the web-server into two separate servers:
	- A public facing *reverse-proxy server* that serves cached static content, handles load balancing and handles SSL encryption
	- One or more private *origin servers* that contain the actual logic of the web application
- We will use **Gunicorn** as the origin server (installable as Pip)
- **Nginx** as the reverse-proxy server:
	- For dealing with external traffic and serving static content
	- Does several things:
		- Routes all traffic through HTTPS so it is encrypted
		- Caches any static data served to improve efficiency
		- Handles public-key encryption/decryption

### Deploying the Website
#### Via Linux VM
- The server runs applications listening to ports for requests and serves those requests
- As most people don't want to worry about the physical infrastructure they use hosting solutions
- These include Amazon, Azure and etc. where you register an account and request an instance, you have a user account with login details, that allows you to SSH into the VM and configure and deploy your app from the command line
- Steps should be taken to secure the server:
	- Remove passwords for login and use key files instead
	- Disable root logins
	- Use a firewall to only accept traffic on ports 22 (SSH), 80 (HTTP) and 443 (HTTPS)
	- Route all web requests through HTTPS, HTTP traffic is transmitted in plaintext and is visible to intermediate nodes

#### Via Your Own Physical Server
- Can use something such as a Raspberry Pi, and connect it to a wireless router and then access the administrator interface of the router

#### Via Cloud Containers
- There exists a lot of Platform-as-a-Service (PaaS) products, largely doing away with having to set up a server, manage storage and maintain infrastructure
- **Containers** are often used to put your web app in its own little transportable box that stays the same no matter what, they standardise the software you've written, along with all the dependencies so it runs the same from one environment to another
- Services such as **docker** and **Heroku** don't offer full Linux VMs but a container to run a single process as a service, they install code directly from Git repository, install all the dependencies and execute and initialise the app