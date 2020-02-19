# php-learn

PHP
What are magic methods in PHP?

Immutability in PHP
. The only immutable data available in PHP is constants
. Constants are set with define() or the const keyword on a PHP class.
. Class constants cannot be changed at runtime
. With constants defined using define() method, constants cane be initialized conditionally, but once set, cannot be changed.
. PHP will raise notice if we try to modify constant.
. We can check if a constant is defined with the function defined() 
. Arrays can be defined as constants in PHP 7, but not objects
. Can we write immutables?
. We can invoke constructor method on the object to modify the state of the object. 
	$x = new A();
	$x->__construct();
. We can use a flag to make it mutable 
	example: 
	class A {
		private $a, $b;
		private $mutable = true;
		public function __construct($a, $b) {
			if(false === $this->mutable) {
				throw new \BadMethodCallException(‘Constructor called twice’);
			}
			$this->a = $a;
			$this->b = $b;
			$this->mutable = false;
		}
	}
. How about extending this class and overload the constructor?
	example: 
	class AA extends A {
		public $a, $b;
		public function __construct($a, $b) {
			$this->a = $a;
			$this->b = $b;
		}

		public function setA($a) {
			$this->a = $a
		}
	}
. PHP final keyword tell the parser that the class cannot be extended
. We can clone an object and modify the private properties of the cloned object
. When we clone an object we get a opportunity to change it’s private properties
. Can we write a function to get a clone of the object?
	public function withA(string $input) : A {
		$clonedClass = clone $this;
		$clonedClass->a = $input;
		return $clonedClass;
	}
. Here in this method, we are creating a cloned object inside a public method which can access the private members of object and hence we can modify the private members 
. In PHP it is possible to add properties to a class at runtime
. Is it possible to add properties to a final class? Yes
. To prevent modifying the class definition, the simple way to prevent this is to add an empty __set() magic method implementation
. It is also possible to remove property values by using unset() construct.
. We can prevent this using magic method __unset()
. Can we write a single function which can be used as getter methods for all the properties of a class? Yes
Example: 
	public function __get($property) {
		if(property_exists($this, $property) {
			return $this->property;
		}
	}
. With above definition, we can now invoke methods using the property names
Example: $obj = new A(); $obj->a;

Clone: 
. Object cloning is creating a copy of an object.
. Cloning an object in php is doing a shallow copy and not a deep copy.
. The contained objects within the cloned objects are not copied.
. For having a deep cloning of the object, you need to implement the __clone() method.
. When there is a need that you do not want the outer enclosing object to modify the internal state of the object then the default PHP cloning can be used.
. With shallow copy, any changes made in the cloned object will not affect original object
. Shallow copy is also known as field-by-field copy. 
. A new object is created and field values are copied from A to B
. If the field values are references to other objects, it copies the references, hence referring to the same object.

. 


REFERENCES: 
. A class in php is twice as memory efficient as an array
. Create an object which is collection of other objects
. Collection only needs to implement Iterator or Iterator Aggregator 
. A collection object can enforce that it contains only a single type of data.

. The language is interpreted, not compiled, which means that it is executed in run-time.
. Reference mismatches happen anytime a by-value variable is passed to a by-ref function argument, and the other way around.
. PHP support 10 primitive types
. 4 scalar types - 
	boolean
	integer
	float
	string
. 4 compound types 
	array
	object
	callable
	iterable
. 2 special types
	resource
	NULL

. In php, the type of the variable is decided at runtime based on the context in which the variable is used.
. You cannot define variable type in php
. What is pseudo-variable $…
. What is the function to know the type of variable? - gettype()
. What is the function to check the type of a variable? - is_int(), is_string()…
. Uneven division of integer variables will result in float by automatic conversions.

. Boolean expresses truth value, it can be either TRUE or FALSE
. Values are case-insensitive
. To explicitly convert a value to boolean, use (bool) or (boolean) casts.
. While converting to boolean, following values are considered false -
	FALSE, 0, -0, 0.0, -0.0, empty string ‘’, string zero - “0”, an array with zero elements, NULL, SimpleXML objects created from empty tags
. An empty string is FALSE and non-empty string is TRUE with one exception.
. A string containing a single zero is considered FALSE.
. NEVER use the OR operator without explicit parentheses around the expression where it is being used
. Instead one should use || instead of OR
. TRUE and FALSE are not integers in php. Beware of interpreting FALSE and TRUE as integers
. When using FALSE as array index on array, It will return the first element of the array
. Example: 
	$arr = [“A”, “B”, “C”]; 
	echo $arr[NULL]; // will print the first element of array - A
. We should be extra cautious when deleting elements from array based on indexes
. Example: 
	$array = [“A”, “B”, “C”]; 
	$index = array_search(“X”, $array); // array_search will return FALSE
	unset($array[$index]); //Will result in deleting the first element of array

ARRAYS
. Array in php is an ordered map. 
. The key can either be an integer or a string, the value can be of any type
.  What happens when you try to use other types to be used as keys?
. String containing valid decimal integers which are not preceded by + sign will be cast to integer type. Example: “8” will be converted to 8, where as “08” will not be casted, as its not valid decimal integer
. Floats are casted to integers when used as keys, which means fractional part will be truncated.
. Booleans are cast to integers too. 
. Null will be cast to the empty string
. Arrays and objects cannot be used as keys, doing so will result in warning.
. What will be output of the following program -  	<?php
	$array = array(
    		1    => "a",
    		"1"  => "b",
    		1.5  => "c",
    		true => "d",
	);
	var_dump($array);
	?> // 1 => “d”
. Php does not distinguish between indexed and associative arrays
. Key is optional in php when defining arrays
. When key is optional, how does php defines keys internally?  	It will increment the largest used integer key.
. We can define keys for only few elements and leave out others
. What is E_NOTICE level error message? 
. Element not found in an array results in an E_NOTICE. 
	Should this be allowed, as the result evaluates to NULL. 
. There are built in functions for sorting -
	sort() and rsort() for sorting indexed arrays
	asort() and arsort() for sorting associative array by value
	ksort() and krsort() for sorting associative array by key
. To remove an element from an array, call the unset($array[$index]);
. How can you delete an entire array? unset($array);
. Using unset() function, we can either remove a key from an array or delete an entire array
. What is bare string in PHP? An unquote string which does not correspond to any known symbol (deprecated as of PHP7.2).
. How can you config php to display errors?
	error_reporting(E_ALL);
	ini_set('display_errors', true);
. Array Casting: for any of the scalar types and resource, array casting results to an array with single element.
	(array) $scalar or array($scalar)
. Can an object be casted to an array? No
. Array conversion of an object results into an array of elements which are the objects properties.
. What are the keys for such array? 

Namespaces 
Namespaces are a way to encapsulate items
Namespace names are case-insensitive
Must start with a letter -  	namespace Mynamespace\1;  // Illegal
	Instead use this:
	namespace Mynamespace\v1; // OK
PSR - Php Standard Recommendations
. What is the principle of Autoload in PHP?
. Any php code can be contained within a namespace, but only following types of code are affected by namespaces
	Classes (abstract, traits), Interfaces, functions and constants
. Namespaces are declared using namespace keyword
. A file containing a namespace must declare the namespace at the top of the file before any other code (one exception is for declare keyword)
. Declare keyword is used for defining encoding of a source file
. No php code may precede a namespace declaration including EXTRA whitespace
. Namespace declaration statement has to be the very first statement or after any declare call
. Php allows splitting up of a namespace’s content across the filesystem, the same namespace can be defined in multiple files in PHP
. You should not try to create namespaces that use PHP keywords
	- namespace Project/Classes/Function; // Causes parse errors
	- namespace Project/Abstract/Factory; // Causes parse errors
. A namespace name can be defined with sub-levels
. Multiple namespaces may also be declared in the same file
. You can define multiple namespaces in a file with and without bracketed syntax
. It is discouraged to combine multiple namespaces into the same file.
. What is the use of multiple namespace in php?
  To combine multiple php scripts into the same file
. Can you define a non-namespaces code in php? Yes
	namespace {
		//
	}
. To combine global non-namespaced code with namespaced code, only bracketed syntax is supported
. We can alias a namespace name to use a shorter name for the class you are extending incase your class is in separate namespace
	namespace com\rsumilang\util;
	use com\rsumlang\common as Common;

	class String extends Common\Object
. FQCN (Full Qualified Class Name)
. __NAMESPACE__ constant is useful for dynamically constructing names
. The use keyword must be declared in the outermost scope of a file (the global scope) or inside namespace declarations
. Without any namespace definition, all class and function definitions are placed into the global space
. Prefixing a name with \ will specify that the name is required from the global space even in the context of the namespace
. 


* Namespaces and Dynamic Language Feature
* Standard interfaces
* Traits
* Constructors, deconstructors, and singletons
* Cloning objects
* Abstract classes
* Iterators
* Generators
* Password hashing and verification
* Type hints, strict type hints, and return types
* Advanced closures
* Nested exceptions and SPL exceptions
