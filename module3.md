# Module 3 - PHP 2
## Refresher of Scope
- Global - Available everywhere
- PHP is a functionally scoped language  - every function has its own scope
- If you need something in a function pass it as a parameter
- Params + returns move things in and out of 

## Unit Testing
Code should behave in a predictable fashion - unit testing increases confidence that the code is doing what it should be. 
Testing types:
- Acceptance testing - test of user behaviour
- Integration testing - testing how the functions work together
- Unit testing - testing each function of an program on its own (like each brick of a building)
 
A function should only do one thing - this makes it easy to test and increases usability
You should avoid creating functions that call other functions - not unit testable
Function mopping - faking the function you need and pretend its done as expected

What do we need to do unit testing?
- A testing framework/library - another program that runs your code

What should we test? - Every function should aim for at least 3 tests:
- Success test - does it work when I use it properly
- Failure test - does it do what it is supposed to do when I don’t use it properly e.g input outside expected range - shows that it can handle it even if it is used wrong, no necessarily that the function fails 
- Malformed test - if the function is given the wrong data type, how does it handle it? e.g array instead of a int - remember to type hint parameters, then all you need to do is expect an array
 
~PHPUnit~
- Inside your project directory, you need a subdirectory named tests. Inside the tests directory, you need to have a file for every php file inside your app. This should mirror the structure of the project directories. 

```php
require '../phpFileName.php'; // Links to another php file, needed when testing
use PHPUnit\Framework\TestCase;

class StackTest extends TestCase {
	// Write tests here
}
```
 
~Running~
To run the test, cd to the tests folder, and run `$ phpunit filename.php` on the file to be tested.

**Success Test**
```php

class StackTest extends TestCase {
	public function testSuccessMultiplyByTwo() { //Replace with name of func to be tested
		$expected = 6; // The expected reuslt of the function to be tested
		$input = 3; // The test input
		$case = multiplyByTwo($input); // Runing the function from the test
		$this->assertEquals($case, $expected); // Asertion, compares expected reuslt to actual result
	}
}
```


**Failure Test**
```php

class StackTest extends TestCase {
	public function testFailureMultiplyByTwo() { //Replace with name of func to be tested
		$expected = -6;
		$inout = -3;
		$this->assertEquals($case, $expected);
	}
}
```

**Malformed Test**
```php

class StackTest extends TestCase {
	public function testMalformedMultiplyByTwo() { //Replace with name of func to be tested
		$input = [3];
		$this->expectException(TypeError::class);
		$case = multiplyByTwo($input);
	}
}
```

## Web Concepts
- Resource functions - a resource is a PHP datatype that connects things - primarily used for error logs. 
- Filename functions: (need correct perms)
	- `file_get_contents()` - open a connection to a file, read the data in the file and close the connection.
	- `file_put_contents()` - open a connection to a file, write data into the file and close the connection.
	- `file_exists()` - returns a boolean based on file existence. 
	- `fileatime()` - returns the last time a file was edited.
- Directory separators:
UNIX: /
Windows: \  
PHP has a predefined constant: DIRECTORY_SEPERATOR
- Embedded HTML/PHP ;
	- Echo out static HTML within PHP 
	- Write HTML within PHP outside the <?php - use this one
	- PHP inside of html tags
Put function decelerations in a separate file (SOC) - makes functions more unit testable

``` php
function sayHi(array $names) :string {

    //create an empty string in a var to catch the output into
    $result = '';

    //loop over the names and concatenate each one as a p tag onto the existing result variable
    //we dont define result inside the loop otherwise it would be overwritten each time
    foreach ($names as $name){
        $result = '<p>Hello ' . $name . '</p>';
    }

    //return a giant string with all p tags concatenated together in it. 
    return $result;
}
```

``` php
require 'functions.php';

$names = ['cuthbert', 'dilbert', 'bob', 'seana'];

$greeting = sayHi($names);

?>

<html>
<head>

</head>
<body>
    <div class="geckos"><?php echo $greeting; ?></div>
</body>
</html>
```

## Require in PHP 
- `include ‘filename.php’;` - copy and pastes contents of the file - if the file doesn’t exist, just moves on, throws a PHP notice.
- `include_once 'filename.php';` - same as include but won’t do it more than once
- `require ‘filename.php’`; - same but if file doesn’t exist throws a serious error and stops execution
- `require_once ‘filename.php’;` - same but only happens once

## Cookies: 
File stored on the users computer - used to store additional info. They are transferred as part of the HTTP header in the HTTP response and are unseen data,. They have a max limit of approx 255 bytes.  Only the creation website can read the cookies (in theory, however they can be a security vulnerability). Not limited to a certain number. They are most commonly used for ad tracking. 

Cookies can be created in PHP:
```php
setcookie('name','data');
```
This creates a cookie on the users machine. You can also give them a time limit in seconds to exist.
This time limit is set by default to be at the end of the users session (navigating away from the page)
```php
setcookie('name','data',timeInSeconds);
```

Rules about cookies:
- Don’t trust them - they are like a lollipop you put down in a shopping centre
- They are the users files, not yours
- HTTPS makes them more trustworthy but still not to be trusted

Info about cookies:
- Optional param: path (were the cookie is accessible from) (path sep on MS is still / in browser)

## Superglobals
Superglobals transcend scope. They are all arrays. There are 9 in totals.
They follow this structure: `$_NAME` 
- `$_COOKIES` - all they cookies stored on the users machine for that site

When creating a cookie and getting the cookies superglobal, the super global will not be able to see the cookie until the next time the page is loaded. The same goes for deleting cookies.
 
To make this work:
```php
setcookie('name','data');

if(isset($_COOKIE['name'])) {
	//code
}
```

### Sessions
- Started from the first server request
- Last from the 1st HTTP response to the last HHTP response
- Each session has an ID, which is a unique identifier for each user.
- unlike a cookie, stored on the server
- Have a default expiry of 24 minutes
- browser sessions (cookies) ≠ sessions
- Stores info about the user
- useful as they persist as an identifier through HTTP requests.
- kinda like a server side cookie, trusted unlike cookies
 
In order to uses sessions:
```php
session_start();
```

`$_SESSION` is an associative array
You can freely r/w to it
Data limit is configurable in php.ini
Use `unset($_SESSION[‘name’]);` to remove data
`session_abort()` - ends session and deletes data
`session_destroy()` - deletes session data keeping session open
`session_status()` - is a session active? Can it be accessed? 

### Get + Post
These are methods of sending data via HTTP
HTTP verbs:
- get - default, used for getting data, not for passing secure data, data usually appears in URL e.g  :  ?name=Charlie&searched=GardenShed : use get when you want to retrieve some data.
- post - sending data, sent in HTTP body, hidden inside request. Still not secure, can be found through traffic sniffing (MIM attack). Has no size limit. Use when you need to send data
- put - used for editing
- delete - for deleting data
- 
Since get is in the head and post is in the body, both are possible at the same time 

`$_GET` and `$_POST` are superglobals
`$_POST[name]` to access data

Cannot set post data like an array

Using with forms: 
``` html
<!--action is where to send the data-->
<!--method is the type of http request to send-->
<form action="pokemon.php" method="post">
<!--$_POST on pokemon.php will be populated with ['favePokemon'=>'whateverYouType']-->
    <input type="password" name="favePokemon" />
<!--Submit button kicks off the new http request-->
    <input type="submit">
</form>
```

``` php
//checks if there is any data inside the POST request
//specifically relating to favePokemon
if(isset($_POST['favePokemon'])){
    //shows us whats inside post data
    var_dump($_POST);
}

?>

<!--will always be output on this page-->
<p>This is the new page</p>
```

### Security
- Any data sent by the browser to the server is considered untrusted 
	- When you build a program, you should sanitise and validate any and all data from the browser - remove malicious characters and check that it contains what it supposed to and reject if needed. 
		- If statements are useful for checking data. 
		- Use built in functions to check type. 
		- Use type hinting
		- Create reusable validation/sanitisation functions
- Password storage
	- **! Do not store plaintext !**
	- Hash passwords - cryptographic algorithm that creates a random key from the text input , check against this rather than the actual password. Means that actual password is never stored. - php uses bCrypt to hash.
	- Websites add ‘salt’ to passwords to make the same password look different
	- password_hash() - params: password, salt . Runs bCrypt on result

PHP header redirect

## OOP
There are three programming methodologies:
- Procedural
- Functional
- Object-Orientated
 
As a style of coding:
- Widely considered to be:
	- Readable 
	- Maintainable
	- Semantic
	- Updatable
	- Slower to write
	- Have larger code

OOP attempts to model the real world in code using objects. Objects have characteristics linked to them and have actions that are intrinsically linked to them. e.g a deck of cards has 52 cards and can be shuffled and dealt. Objects are complex data types, they can contain other data types as well as other objects. They can also contain functions (the object’s actions). 

Objects are created from classes. A class acts as a blueprint or specification of what a specific type of object should look like. CLASS ≠ OBJECT. Objects are instantiated (created) from classes. Many objects can be instantiated from the same class, objects are different based on what has happened to them. PHP has a default class, standard object, **don’t use it.** 

In classes and objects variables are called properties  

``` php

<?php
class Pig
{
    public $name;
    public $leg_count = 4;
    public function __construct($name)
    {
        $this->name = $name;
    }
    public function sleep()
    {
        echo 'zzzzzzzzzz';
    }
}
$andy = new Pig('Andy');
echo $andy->name;
$rupert = new Pig('Rupert');
echo $rupert->name;
```

### Extending classes:
Classes can inherit properties and methods from a parent class using `extends`
e.g. `class Sheep extends Animal`

``` php
<?php

//parent class
class Animal
{
    public $legs = 4;

    public function run()
    {
        echo 'im running';
    }

    public function shout()
    {
        echo 'im shoutin';
    }
}

//child class
class Sheep extends Animal
{
    public $wool = true;

}

//child class
class Chicken extends Animal
{
    public $beak = true;

    public function layEggs()
    {
        echo 'im laying here';
    }

    public function flap()
    {
        echo ' im flappin';
    }
}
//object instansiation
$jeanClaudeVanLamb = new Sheep();
//object instansiation
$henniferAniston = new Chicken();

//calling a method inherited from a parent class (Animal)
echo $henniferAniston->shout();
```

### Visibility:
Three levels of visibility:
- public - anything can see or change the property or access the method
- protected - can only be read/written by the object or a child object
- private - can only be read and written to by current class

Getters and Setters:
- Are a design pattern -  a way of structuring code
- when a property is set to public anyone can see or edit the data
- in some cases you want to restrict how a property can be changed e.g int 1-4
- Getters and setters are the public facing methods that restrict how the data is accessed/modified

### Encapsulation
Hiding functionality inside the object so the user only worries about about how to use it
Agreed ignorance helps code defensively

### Abstract Classes - `abstract`
- Classes that cannot be instanciated
- Give inheritance opportunities
- Suit concepts rather than things e.g animal class
- Protects that you from having objects that are too generalised
``` php
abstract class Animal
{
    //does generic animal stuff
}

class Pig extends Animal
{

}

//ok
$kevinBacon = new Pig();

//nope throws a fatal error
$darthAnimal = new Animal();
```

Abstract can also be used to establish a ‘contract’ that you are going to define a certain method in a certain way in classes extending the abstract class. This can only be done when the class the abstract method is in is an abstract class. (Forces child classes to implement method). Abstracts shouldn’t extend any class. 

### Interfaces
Interfaces provide a contract of what the implementing classes should contain. Only specify what methods to have, not the functionality. Like abstract you can implement as many interfaces as you like. Abstracts > Interfaces (usually). 
You can type hint interfaces

```php
<?php

interface eat
{
	public function eatFood();
}

interface sleep
{
	public function sleep();
{

class Pig implements eat, sleep
{
	public function eatFood() {
		
	}
	public function sleep() {

	}
}
```

# **DON’T WORRY ABOUT WRITING PERFECT CODE FIRST TIME, YOU CAN ALWYS REFACTOR LATER**
### Polymorphism
Concept around how data is used. If two classes extend the same abstract class or implement the same interface they should be able to used in the same way.

``` php
<?php

interface speak
{
    public function speak();
}

class Pig implements speak
{
    public function speak()
    {
        return 'oink';
    }
}

class Dog implements speak
{
    public function speak()
    {
        return 'woof';
    }
}

function makeAnimalSpeak(speak $animal){
    echo $animal->speak();
}

$harryTrotter = new Pig();
$lassie = new Dog();

makeAnimalSpeak($lassie);
```







