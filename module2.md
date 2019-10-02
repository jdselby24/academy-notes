# Module 2 - PHP
`$newVariable89`
- - - -
## 11/09/19
### PHP - Personal Home Page, now PHP Hypertext Processor
- Hypertext - text on the internet  - PHP creates/modifies HTML
- Needs to be interpreted by a server/interpreter, opening a PHP file in a browser without running will just show plaintext, runs like a program based on settings, e.g. output errors
- Settings stored in php.ini - usually configured by sysadmin/server manager(s)

### Stacks
Technology stack you are working with e.g LAMP 
- Linux - operating system
- Apache - web server
- MySQL - database
- PHP - backend language

2 types of files:
	- Static - HTML, CSS, images (returned through apache alone)
	- Dynamic - PHP, JS etc. (runs and returns a result)

### Local Development Environment (Vagrant)
Replicates server behaviour on local machine for testing, before using 		a live server. Lets you use PHP locally - mirrors the live server  as closely 	as possible(IMPORTANT, prevents unforeseen bugs - same versions of 	the same software)
 	
This is done through virtual machines - install another operating system inside the host.

In this case we are using Vagrant to run virtual machines

/sites/VM/academy-php7     -   VM location
`$ vagrant up` - starts VM
`$ vagrant halt` - stops vm
`$ Vagrant reload` - restarts vm
`$ vagrant destroy`  - deletes vm and contents
`$ vagrant ssh` - CLI of VM

Industry is switching toward DOCKER

### Docker
Docker allows changing stacks within the same VM, unlike vagrant, which needs a new VM for each stack.

`$ docker-compose up`   - starts vm
`$ docker-compose up --detach`  - starts vm without taking up terminal window

/sites/academyServer/htm

### PHPStorm
Is an IDE (Integrated Development Environment) with multi language support, project management, project structure, git, increases in power with more languages. 

 Commands:

cmd+shift+v  -  paste from history
cmd+shift+a  - spotlight equivalent 
alt+shift+(arrow keys) - moves selected content
cmd+delete - deletes entire line
tab/shift+tab - can tab/un-tab code blocks

- - - -
### PHP
PSR2 - standardised way of doing things in PHP (best practice, shared rules and opinions) - formatting - created by the user group PHP Fig - here are some of the rules:

- Indents are 4 spaces
- true/false/null are lower case

Syntax vs Semantics: syntax is the grammatical rules whereas semantics is additional info and readability.

Start of a .php file: `<?php`

`phpinfo()` - built in function that lets you view your settings.

- Every line in php must finish with a semicolon e.g. `phpinfo();`
- Every command should be on its own line.
 
`echo` - used to output text, e.g. `echo ‘hello world’;` 

#### Variables
A box to store data inside - data don’t define the box, v~v.
Variables in PHP are declared using `$` e.g `$geckosBankVault`
 
- Must start with a letter or an underscore.
- Only contain a-z, A-Z, 0-9, _
 
Variables are assigned values using `=`.
e.g `$geckosBankVault = ‘a shit ton of money;`.

Variables can be used in other functions e.g. `echo $geckosBankVault;`.
Variables can be used many times in many places.

**!!! NO VARIABLE VARIABLES !!!** (`$hello = “yo”; $$hello = “waddup”;`

#### Constants
A box to store data that cannot be changed - they are immutable
 Defined using `define(name, value);` e.g `define(POSTLENGTH, 9);`

#### Data Types
Simple (scalar) data types (only contain one type of data):
- Strings - store alphanumeric characters, inside double or single quotes `$string  = “yo”;`
- Integer  - whole numbers `$integer = 9;`
- Float - decimal numbers `$float = 4.5;`
- Boolean - yes/no, true/false, 1/0 `$boolean = true;`
- Null - nothing (intentionally) `$null = null;`
 
Complex data types (can store multiple data types):
- Array  - multiple values stored inside a single value `$array = [9, true 45.1 “hey”;`
- Object - stores data and info on how to process that data
- - - -
~Strictly Typed vs Untyped/Loosely Typed~
- Typed: data type defined at creation of variable and cannot change
- Untyped: data type of variables can change

PHP is a untyped language. Untyped languages are more flexible when reusing variables but are’t so concerned with memory management 

Typed languages are more reliable
- - - -

To check the type of something in PHP `gettype($var);`.
`var_dump($var);`  - tells you about the variable (data type and value), useful for debugging, never deploy live

Variables will change data type based on what you are doing with it (type juggling) 
- - - -
~Type Casting~
Forces variables to a particular data type
`$foo = (string) 2;`  - string with value 2, not enforced, useless as data type can still be changed
- - - -
~Quotes~
The difference between single and double quotes is variable interpolation
- Single quotes outputs the exact value
- Double quotes interprets any variables inside the string as their values

**USE DOUBLE QUOTES ONLY WHERE NEEDED**
- - - -
~Special Characters~
 Particularly useful for cleansing user input or retrieving cleansed data from a DB
- & = `&amp`
- “ = `&quot`
- ‘ = `&039`
- < = `&lt`
- > = `&gt`

- To escape a character e.g ‘ or “ - `\’` or `\”`
- \ = `\\`
- `\` can be used in front of any character that should be treated literally

For quotation marks mixed quotes can also be used
- - - -
~Concatenation~
Used for joining multiple strings together - `$foo . $bar` - would join the strings stored in foo and bar together. Can be used on as many strings as required
- - - -
#### Symbols and Operators
- Mathematical operators:
- `!` - not (reverse or negation)
- `&&` - AND
- `||` - OR
- `=` - assignment 
- `==` - non strict comparison operator (compares only values)
- `===` - strict comparison (compares values and data type) - better practice where possible, prevents type juggling.
- `!=` - not equal to
- `!==` - not strict equal to
 
~Compound assignment~
Do other things at the same time as assignment 
- `*=` - multiply and assign
- `/=` - divide and assign
- `+=` - add and assign
- `-=` - subtract and assign
- `.=` - concatenate and assign 

~Increment and decrement~
- `++`  - increments variable by 1
- `--` - decrement variable by 1
- Works for integers and floats
- - - -
~Operator Precedence~
The order in which you apply operators
- Safe bet to go with BIDMAS (Brackets Indices Division Multiplication Addition Subtraction)
- Use brackets to force things to happen first 
- - - -
~Conditionals~
One of multiple things can happen that depend on a condition, where the condition must evaluate to a boolean. If the bool is a 1 it happens if its 0 it doesn’t happen.
```php

 if (condition) {
	thing;
 }
```
Else can be added, and runs if no condition is met
```php

if (condition) {
	thing;
} else {
	thing2;
}
```
Else if can add another condition
```php

if (condition) {
	thing;
} else if (condition2) {
	thing2;
} else {
	thing3;
}
```

Switch:
```php

switch (var) {
 case condition:
		thing;
		break;
 case condition2:
		thing2;
		break;

 ...

	default:
		defaultThing;
		break;
}
```

Switch statements are technically loops not a conditional but used more like a conditional. Give them a variable to compare in each case, break exits the switch statement.
**ALWAYS REMEMBER A DEFAULT**

```php

$a = 1;
$b = 2;
$c = 2;

switch (true) {
	case $a === $b:
		echo 'a and b are the same';
		break;
	case $b === $c:
		echo 'b and c are the same';
		break;
	default:
		echo 'this is the default';
}
```
- - - -
~Ternary Operators~
Shorthand `if` statements

`$var1 = ($ifVar == condition ? 'returnTrue' : 'returnFalse');`

Is the same as

```php

if ($ifVar == condition) {
	$var1 = 'returnTrue';
} else {
	$var1 = 'returnFalse';
}
```
- - - -
~Arrays~
Two types:
- Indexed - numerically indexed 
`$indexedArr = [1,2,”yes”,’hello’];`
- Associative - key value pairs.  (not objects)                                                                  
`$assocArr = [“name”=> ‘cuthbert’,”age”=> 99];`

**PHP indexed arrays are zero indexed**
Arrays are indexed with `$varName[x];` where x is the index

`=>` -  key value pair identifier

Arrays can also be defined using `$var = array(1,2,..)`
Values can be added to an array using:
`array-push(array name, value);`
This adds the value to the end of the array
Also can be added using:
`$var[] = ‘value’;`
Which adds it to the end and automatically assigns a key, you can also add your own key between the brackets. If the key already exists, it replaces the data at that key. Any value of key can be assigned.

~Multidimensional Arrays~
Arrays within arrays
Normal arrays are 1 dimensional

```php

$mdArray = [1,2,3,4,[1,2,’meat’,4,5]];

echo $first[4][2]; //is meat (5th element of first array, 3rd element of second)
```

~Array for each~
Performs a block of code for every item in the array. It is unaffected by array length and will always know how many times to run.  
```php

foreach ($arrayName as $refVal) {
	echo $refVal;
}
```

Would echo every value in the array $arrayName

To get the key also 
```php

foreach ($arrayName as $key => $value) 
```
- - - -
~Loops~
~For Loop~
```php

for ($i=0; $i<10; $i++); {
	echo ‘hello geckos! <br>’;
}
```


```php

$class = [‘Alex’, ‘Luke’, ‘josh’, ‘Charlotte’, ‘calum’, ‘marc’, ‘sean’, “thing”=>’cosmin’, ‘cuthbert’];

for ($I=0; $I<count($class); $I++){
    echo $class[$I] . ‘<br>’;
}
```
- - - -
~While Loop~
```php

$i = 0;

while ($i<0) {
	echo $i . 'is the result <br>';
	i++;
}
```
- - - -
~Do While~
Will run at least once
```php
do {
	thing;
} while (condition)
```
Use increment to stop never ending loops

e.g
```php
$x = 6;

do {
	echo 'hello';
	$x++;
} while ($x , 5);
```
- - - -
~Stopping Loops~
`continue;` -  can be used inside loops to stop the current iteration and skip to the next

`break;` - stop the whole loop

e.g.
```php
$i = 0
while ($i < 10) {
	if ($i === 5) {
		continue;
	}
	echo $i;
}
// would output 12346789
```
```php
$i = 0
while ($i < 10) {
	if ($i === 5) {
		break;
	}
	echo $i;
}
// would output 1234
```
- - - -
~Nested Loops~
```php
for ($i=0;$i<10;$i++) {
    for ($y=0;$y<10;$y++) {
        echo $i . ' and ' . $y . '<br>';
    }
}
```
- - - -
~Functions~
Reusable sets of instructions (blocks of code)
- User declared functions - 
To Declare:
```php 
function funcName () { // your code goes here }`
```
To Call:
```php
funcName();	
```

Functions can take params, which are defined and passed in the (). Functions can take as many params as you like

``` php
function whatTime($time, $amOrPm){
    echo 'its: ' . $time . $amOrPm;
}


whatTime(5, 'am');

echo '<br>';

whatTime(7, 'pm');
```

Function outputs using `return` - should be used so the output can be ‘caught’ and used elsewhere.

The ‘calum’ function:
```php
function areYouCalum($name){
  if($name === 'calum'){
    return true;
  } else {
    return false;
  }
}

$name = 'calum';
$result = areYouCalum($name);
var_dump($result);
```

Functions can have there params typed hinted as follows:
```php
function exapmpleFunc(array $array) { //must be an array
	//do a thing
}
```
Will throw a PHP error if the data type is incorrect. Stops the function before it can run, prevents unexpected results.

Returns can also be type hinted:
```php
Function exampleFunc() :string {
}
```
Would only allow a string to be returned

Functions cannot access variables outside the scope of the function.
They can however access constants from outside their scope (DON’T DO IT THOUGH).

Functions don’t change the value of variables passed in unless passed by reference

- Built In functions - variables are usually passed by reference rather than value, e.g  - `shuffle($arr);` changes the actual value of the variable `$arr`. Not all built in functions have pass by ref. 

Passing by ref can be forced using adding `&` in front of the `$` of the name of a parameter of a function.

PHP is extensible, and can be extended with additional functions.
You can check if a function exists using the `function_exists` function.

Built in function groups:
- Math Functions  - e.g `floor` and `ceil`
- String Functions - e.g `trim`  (removes white space) and `strtolower` and `explode`
- Array Functions  - e.g. `is_array` or `array_key_exists` or `array_slice`
- And many more…..

~Comments~
// - Single line
/* */  - multiline, each line marked with *

Doc Blocks:
Every function should have a doc block. above the function, explain what it does, with a line break underneath. Then under that detail each parameter using @param

E.g.
```
/*
* Description of function
*
* @param $paramName dataType Description
* 
* @param $param2 otherDataType OtherDesciption
*
* @return dataType description
*/
```

Example with a function:

```php
<?php

/** 
* Combines two words together
*
* @param string $word1 the first word
*
* @param string $word2 the second word
*
* @return string the new word created from the params
*/
function stickTwoWordsTogether (string $word1, string $word2){
	return $word1 . $word2;
}
```


### Databases
For storing data in a structured manner

CRUD:
- Create
- Read 
- Update 
- Delete
Data needs to be stored in a structured way: SQL
Structured Query Language - used to interact with databases 

Many different databases, we a using MySQL - a relational database engine
Manages and powers database
90% of PHP apps use MySQL
Documentation is awful
Runs in the background
Uses command line - nasty - use SequelPro as GUI

There is no limit to how many databases you can have other than storage space

Don’t use spaces in database names
Most apps have one database 

Databases have tables with store tabular data displayed as a grid, databases can have multiple tables. No set naming convention for tables however you need to be consistent. Names should be plural e.g users not user. No spaces in the names - camel case or underscores.

Tables contain fields which are the names of columns - edited in the structure tab. 

MySQL has functions:
- Built in superset of SQL
- mostly named the same as to PHP e.g (RTRIM - removes whitespace from right hand side) 
- Logic should be done in PHP not SQL if it can be done in PHP

SQL datatypes: (four main ones)
- Numeric
- String
- Date and Time
- Other
 
Numeric intergers:
- tinyint - 
- smallint - 
- mediumint - 
- int - 
- bigint - 
All versions of integers, use appropriate to the size based on +/-ve range required

Signed numbers can be negative, but shift the range

Numeric floats/doubles:
- Defined with FLOAT (x,y) - x is total number of digits, y is the number of decimal digits e.g. 5.2 would need a FLOAT (2,1), 43.898 would need a FLOAT (5,3)

Strings: 
- CHAR : characters, any string (specify max length) - always uses max length - reserves space for future
- VARCHAR : characters, any string (specify max length) - only uses length required. Dangerous, can break database e.g if storage is full.
- TEXT : unoptimised for searching
- TINYTEXT :  unoptimised for searching
- BLOB : unoptimised for searching, has a 2 byte prefix that details how much data the blob contains. (Advanced optimisation)
- BINARY : store binary strings 
- ENUM : pick from a predefined set of values, stored as a CSV (Comma Separated Values) 

Date and time:
- Date : YYYY-MM-DD format
- Datetime : YYYY-MM-DD HH:MM:SS format
- Timestamp : Unix time stamp - number of seconds since 00:00 on 01/01/1970
- Time : hh:mm:ss
- Year : yyyy

#### SQL Syntax - SWOGL
~DML - Data Manipulation~
```sql
SELECT `fieldName` FROM `tableName`;
``` 
- retrieve all the data from the fields ‘column’ from the table
```sql
SELECT `fieldName` AS "alias" FROM `tableName`;
``` 
- same as above but changes key of generated array
```sql
SELECT `fieldName` FROM `tableName` WHERE `fieldName` = "value";
```
- Using WHERE to filter data, can use any mathematical operator. Search can be performed on data that isn’t in a selected field.
```sql
SELECT `fieldName` FROM `tableName` GROUP BY `fieldName`;
```
- Used for group data from the same table that is similar. Groups all similar rows with the same value for that field and only show the first of those rows. 
```sql
SELECT `fieldName` FROM `tableName` ORDER BY `fieldName` ASC;
```
- Selects the output order ASC/DESC (ascending/descending)
```sql
SELECT `fieldName` FROM `tableName` LIMIT 0, 10;
```
- Specifies a limit of how many records to return 
```sql
SELECT * FROM `table1` INNER JOIN `table2` ON `table1`.`table1id` = `table2`.`table2id`;
```
```sql
SELECT * FROM `table1` LEFT JOIN `table2` ON `table1`.`table1id` = `table2`.`table2id`;
```

- Limits the number of values returned, first value is the offset, second is the number of records
`JOIN`  - selects data from multiple tables. `INNER JOIN`  - returns just the matching data
`LEFT JOIN` returns all the data from the table on the left and the matching data from the table on the right (left is the left side of the equals). `RIGHT JOIN`  - not used, just use left join and swap equals order.

```sql
INSERT INTO `table` (`field1, `field2`) 
	VALUES ('value1', 'value2')
```

```sql
UPDATE `table` SET `field`= 'value' WHERE `field2` = 'value'
```

```sql
DELETE FROM 'table' WHERE `field` = 'value'
```
- don’t use delete, set a deleted flag instead

#### Using databases with PDO (PHP Data Objects)
- Lots of ways to connect to databases, PDO is the accepted method for connecting PHP to MySQL
- PHP is extensible, PDO is a library. Will be present on industry standard VM
- PDO creates a connection between PHP and MySQL
- Only need to connect once per page, connection saved into a variable and reuse it. 
- Create a new one:
```php
$db = new PDO('mysql:host=ipa.dd.re.ss; dbname=NAMEOFDB', 'root', 'password'); /*        
* Replace ip with db on docker */
```
- Query:
```php
$query = $db->prepare("INSERT INTO `colors` (`color`) VALUES ('Silver');");
$query->execute();
```

- Getting data out in php: (fetch only returns the first item, use fetchAll to get all the data.
You must execute before you can fetch. Data comes out of fetchAll as a MD array with each record having its own array.  Fetch just returns an indexed array. Data is doubled with two of the same value with one being associative and one being indexed.
```php
    $db = new PDO('mysql:host=db; dbname=ex1', 'root', 'password');

    $query = $db->prepare("SELECT `color` FROM `colors`;");

    $query->execute();

    $result = $query->fetch(); // Retrieves data as array

    var_dump($result);
```
- To specify wether you would like associative or indexed:
```php
$db->setAttribute(PDO::ATTR_DEFAULT_FETCH_MODE, PDO::FETCH_ASSOC); // For assoc

$db->setAttribute(PDO::ATTR_DEFAULT_FETCH_MODE, PDO::FETCH_NUM); // For indexed

$query->setFetchMode(PDO:FETCH_NUM or FETCH_ASSOC); // Per query setting
```

~Fetch Types~
- PDO::FETCH_BOTH - the default, returns both associative and indexed
- PDO::FETCH_ASSOC - returns data as an indexed array of associative arrays(keys are field names)
- PDO::FETCH_OBJ - returns the data as an anonymous object with properties as field names
- PDO::FETCH_CLASS, ‘className` - returns the data as a class to base an object on, properties match field names

#### User input
- Users can perform SQL injection attacks if input is unfiltered
- To circumvent this use bindParam
```php
$db = new PDO('mysql:host=db; dbname=EX1', 'root', 'password');

$db->setAttribute(PDO::ATTR_DEFAULT_FETCH_MODE, PDO::FETCH_ASSOC);

$userInput = 'mellow yellow';

$query = $db->prepare("INSERT INTO `colors` (`color`) VALUES (:newColor)");

$query->bindParam(':newColor', $userInput); //Strips mal code

$query->execute();

```
- You can also anomalously bind params using a ‘?’ 
```php
$query = $db->prepare("INSERT INTO `adults` (`name`, `age`) VALUES (?, ?)");

$query->execute([$name, $age]);
```
- You can also pass a associative array
```php
$query = $db->prepare("INSERT INTO `adults` (`name`, `age`) VALUES (:name, :age)");

$query->execute([“name” => $name, “age” => $age]);
```

~Advanced Databases Concepts~
**Indexes** increase the speed your tables can be searched in, like a book index helps you search efficiently. Creates a lookup table in a sorted order. You can index any field and searching it will be quicker, however this should not be done as all the data is stored in the lookup table, increasing DB size and data entry time. Index frequently used/searched tables.

**Primary Keys** you should always have a primary key in a table. It is a unique indentifier for records in a table. You should aim to join on primary keys.

**Foreign Keys** data in one table that relates to the primary key in another. Not a tangible link, rather a concept. 

~Functions~
`COUNT()` - returns number of rows in select statement, should use primary key
`AVG()` - average of what you are selecting

Advanced Where:
`LIKE` - works as a contains e.g. 
```php
WHERE `name` LIKE %a%
```
Would return all values of name containing the letter ‘a’
- % -  is a wildcard, represents multiple characters
- _ - represents a single letter, e.g. _o_ would return every value of with the second letter ‘o’ that is 3 letters long
- [a -z] - character list
- [1b]o_ - would ignore results with the letter ‘b’ (negation)
- BETWEEN - returns results where the values of the specified filed are within a certain range
```php
SELECT `age` FROM `adults` WHERE `age` BETWEEN 22 AND 40;
```

~Transactions~
A set of queries that run as a group. If one fails the others won’t run. Treats as one unit of work.
ACID transactions:
- Atomicity - if one query fails they all do. 
- Consistency - DB changes in a reliable way
- Isolation - Transactions can’t affect each other
- Durability -  results are committed all at once
We aim to make our transactions as ACID compliant as possible

~Storage Engines~
Manages the accessing of data from the database
≠ to the database engine (MySQL)
- InnoDB - newest, most popular, recommended
- myIsam - much older, original, still used in places
- Others: memory, CSV, merge, archive, federated, black hole

~InnoDB~
- ACID compliant
- Can use transactions
- Row level locking - prevents access by other queries from another connection whilst a row is being queried 
- Supports foreign key constraints
- Writing data is quick, reading data is slow

~myIsam~
- Writing data is slow, reading data is quick
- Good for DBs that don’t change much
- Doesn’t support transactions
- Doesn’t support foreign key constraints
- Table level locking
- Less flexible than InnoDB

~Architecture decisions~
- Relationship types:
	- One to one - one piece of data in one table links to one piece of data in another
	- One to many - one piece of data in one table links to many in another
	- Many to many - many pieces of data link to many pieces of data
- EAV (Entity Attribute Value) table
	- Don’t store nulls
	- Optimised - store what you need
	- Easy to add new fields
	- Total number of values stored is much lower
	- May get some duplication
	- Not easy to use






