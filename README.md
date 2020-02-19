<p><strong># php-learn </strong></p>
<p><strong>PHP </strong></p>
<p>What are magic methods in PHP?</p>
<p><strong>Immutability in PHP</strong></p>
<ul>
<li>The only immutable data available in PHP is constants</li>
<li>Constants are set with define() or the const keyword on a PHP class.</li>
<li>Class constants cannot be changed at runtime</li>
<li>With constants defined using define() method, constants cane be initialized conditionally, but once set, cannot be changed.</li>
<li>PHP will raise notice if we try to modify constant.</li>
<li>We can check if a constant is defined with the function defined()</li>
<li>Arrays can be defined as constants in PHP 7, but not objects</li>
<li>Can we write immutables?</li>
<li>We can invoke constructor method on the object to modify the state of the object. <br /> $x = new A(); <br /> $x-&gt;__construct();</li>
<li>We can use a flag to make it mutable <br /> example: <br /> class A { <br />&nbsp; &nbsp;private $a, $b; <br />&nbsp; &nbsp;private $mutable = true; <br />&nbsp; &nbsp;public function __construct($a, $b) { <br />&nbsp; &nbsp; &nbsp; if(false === $this-&gt;mutable) { <br />&nbsp; &nbsp; &nbsp; &nbsp; throw new \BadMethodCallException(&lsquo;Constructor called twice&rsquo;); <br />&nbsp; &nbsp; &nbsp; } <br />&nbsp; &nbsp; &nbsp; $this-&gt;a = $a; <br />&nbsp; &nbsp; &nbsp; $this-&gt;b = $b; <br />&nbsp; &nbsp; &nbsp; $this-&gt;mutable = false; <br />&nbsp; &nbsp;} <br />}<br /><br /></li>
<li>How about extending this class and overload the constructor? <br />example: <br />class AA extends A { <br />&nbsp; public $a, $b; <br />&nbsp; public function __construct($a, $b) { <br />&nbsp; &nbsp; $this-&gt;a = $a; <br />&nbsp; &nbsp; $this-&gt;b = $b; <br />&nbsp; } <br />&nbsp; public function setA($a) { <br />&nbsp; &nbsp; $this-&gt;a = $a <br />&nbsp; } <br />}<br /><br /></li>
<li>PHP final keyword tell the parser that the class cannot be extended</li>
<li>We can clone an object and modify the private properties of the cloned object</li>
<li>When we clone an object we get a opportunity to change it&rsquo;s private properties</li>
<li>Can we write a function to get a clone of the object? <br />public function withA(string $input) : A { <br />&nbsp; $clonedClass = clone $this; <br />&nbsp; $clonedClass-&gt;a = $input; <br />&nbsp; return $clonedClass; <br />} <br />Here in this method, we are creating a cloned object inside a public method which can access the private members of object and hence we can modify the private members<br /><br /></li>
<li>In PHP it is possible to add properties to a class at runtime</li>
<li>Is it possible to add properties to a final class? Yes</li>
<li>To prevent modifying the class definition, the simple way to prevent this is to add an empty __set() magic method implementation</li>
<li>It is also possible to remove property values by using unset() construct.</li>
<li>We can prevent this using magic method __unset()</li>
<li>Can we write a single function which can be used as getter methods for all the properties of a class? Yes <br />Example: <br />public function __get($property) { <br />&nbsp; if(property_exists($this, $property) { <br />&nbsp; &nbsp; return $this-&gt;property; <br />&nbsp; } <br />}<br /> </li>
<li>With above definition, we can now invoke methods using the property names <br />Example: <br />&nbsp; $obj = new A(); <br />&nbsp; $obj-&gt;a; Clone:<br /><br /></li>
<li>Object cloning is creating a copy of an object</li>
<li>Cloning an object in php is doing a shallow copy and not a deep copy</li>
<li>The contained objects within the cloned objects are not copied</li>
<li>For having a deep cloning of the object, you need to implement the __clone() method</li>
<li>When there is a need that you do not want the outer enclosing object to modify the internal state of the object then the default PHP cloning can be used</li>
<li>With shallow copy, any changes made in the cloned object will not affect original object</li>
<li>Shallow copy is also known as field-by-field copy</li>
<li>A new object is created and field values are copied from A to B</li>
<li>If the field values are references to other objects, it copies the references, hence referring to the same object<br /><br /><strong>REFERENCES</strong>:</li>
<li>A class in php is twice as memory efficient as an array</li>
<li>Create an object which is collection of other objects</li>
<li>Collection only needs to implement Iterator or Iterator Aggregator</li>
<li>A collection object can enforce that it contains only a single type of data</li>
<li>The language is interpreted, not compiled, which means that it is executed in run-time</li>
<li>Reference mismatches happen anytime a&nbsp;by-value&nbsp;variable is passed to a&nbsp;by-ref&nbsp;function argument, and the other way around<br /><br /></li>
<li>PHP support 10 primitive types</li>
<li>4 scalar types - boolean integer float string</li>
<li>4 compound types array object callable iterable</li>
<li>2 special types resource NULL</li>
<li>In php, the type of the variable is decided at runtime based on the context in which the variable is used</li>
<li>You cannot define variable type in php</li>
<li>What is pseudo-variable $&hellip;</li>
<li>What is the function to know the type of variable? - gettype()</li>
<li>What is the function to check the type of a variable? - is_int(), is_string()&hellip;</li>
<li>Uneven division of integer variables will result in float by automatic conversions.&nbsp;</li>
<li>Boolean expresses truth value, it can be either TRUE or FALSE</li>
<li>Values are case-insensitive</li>
<li>To explicitly convert a value to boolean, use (bool) or (boolean) casts.</li>
<li>While converting to boolean, following values are considered false - <br />FALSE, 0, -0, 0.0, -0.0, empty string &lsquo;&rsquo;, string zero - &ldquo;0&rdquo;, an array with zero elements, NULL, SimpleXML objects created from empty tags</li>
<li>An empty string is FALSE and non-empty string is TRUE with one exception</li>
<li>A string containing a single zero is considered FALSE</li>
<li>NEVER use the OR operator without explicit parentheses around the expression where it is being used</li>
<li>Instead one should use || instead of OR</li>
<li>TRUE and FALSE are not integers in php. Beware of interpreting FALSE and TRUE as integers</li>
<li>When using FALSE as array index on array, It will return the first element of the array<br />Example: <br />&nbsp; $arr = [&ldquo;A&rdquo;, &ldquo;B&rdquo;, &ldquo;C&rdquo;]; <br />&nbsp; echo $arr[NULL]; // will print the first element of array - A</li>
<li>We should be extra cautious when deleting elements from array based on indexes <br />Example: <br />&nbsp; $array = [&ldquo;A&rdquo;, &ldquo;B&rdquo;, &ldquo;C&rdquo;]; <br />&nbsp; $index = array_search(&ldquo;X&rdquo;, $array); // array_search will return FALSE <br />&nbsp; unset($array[$index]); //Will result in deleting the first element of array ARRAYS</li>
<li>Array in php is an ordered map</li>
<li>The key can either be an integer or a string, the value can be of any type</li>
<li>What happens when you try to use other types to be used as keys?</li>
<li>String containing valid decimal integers which are not preceded by + sign will be cast to integer type. <br />Example: &ldquo;8&rdquo; will be converted to 8, where as &ldquo;08&rdquo; will not be casted, as its not valid decimal integer</li>
<li>Floats are casted to integers when used as keys, which means fractional part will be truncated.</li>
<li>Booleans are cast to integers too.</li>
<li>Null will be cast to the empty string</li>
<li>Arrays and objects cannot be used as keys, doing so will result in warning.</li>
<li>What will be output of the following program -  <br />// 1 =&gt; &ldquo;d&rdquo;</li>
<li>Php does not distinguish between indexed and associative arrays</li>
<li>Key is optional in php when defining arrays</li>
<li>When key is optional, how does php defines keys internally?   <br />It will increment the largest used integer key.</li>
<li>We can define keys for only few elements and leave out others</li>
<li>What is E_NOTICE level error message?</li>
<li>Element not found in an array results in an E_NOTICE. <br />Should this be allowed, as the result evaluates to NULL.</li>
<li>There are built in functions for sorting - <br />&nbsp; sort() and rsort() for sorting indexed arrays <br />&nbsp; asort() and arsort() for sorting associative array by value <br />&nbsp; ksort() and krsort() for sorting associative array by key</li>
<li>To remove an element from an array, call the unset($array[$index]);</li>
<li>How can we delete an entire array? unset($array);</li>
<li>Using unset() function, we can either remove a key from an array or delete an entire array</li>
<li>How can you config php to display errors? <br />error_reporting(E_ALL); <br />ini_set('display_errors',&nbsp;true);<br /><br /></li>
<li>Array Casting: <br />For any of the scalar types and resource, array casting results to an array with single element. <br />(array) $scalar or array($scalar)</li>
<li>Can an object be casted to an array? No</li>
<li>Array conversion of an object results into an array of elements which are the objects properties.</li>
<li>What are the keys for such array? <br /><br /><strong>Namespaces</strong> <br /><br /></li>
<li>Namespaces are a way to encapsulate items</li>
<li>Namespace names are case-insensitive</li>
<li>Must start with a letter -   <br />&nbsp; namespace Mynamespace\1;&nbsp; // Illegal <br />Instead use this: <br />&nbsp; namespace Mynamespace\v1; // OK </li>
<li>What is the principle of Autoload in PHP?</li>
<li>Any php code can be contained within a namespace, but only following types of code are affected by namespaces:<br />Classes (abstract, traits), Interfaces, functions and constants</li>
<li>Namespaces are declared using namespace keyword</li>
<li>A file containing a namespace must declare the namespace at the top of the file before any other code (one exception is for declare keyword)</li>
<li>Declare&nbsp;keyword is used for defining encoding of a source file</li>
<li>No php code may precede a namespace declaration including EXTRA whitespace</li>
<li>Namespace declaration statement has to be the very first statement or after any declare call</li>
<li>Php allows splitting up of a namespace&rsquo;s content across the filesystem, the same namespace can be defined in multiple files in PHP</li>
<li>You should not try to create namespaces that use PHP keywords -&nbsp; &nbsp; <br />&nbsp; namespace&nbsp;Project/Classes/Function;&nbsp;// Causes parse errors - <br />&nbsp; namespace&nbsp;Project/Abstract/Factory;&nbsp;// Causes parse errors</li>
<li>A namespace name can be defined with sub-levels</li>
<li>Multiple namespaces may also be declared in the same file</li>
<li>You can define multiple namespaces in a file with and without bracketed syntax</li>
<li>It is discouraged to combine multiple namespaces into the same file</li>
<li>What is the use of multiple namespace in php? To combine multiple php scripts into the same file</li>
<li>Can you define a non-namespaces code in php? Yes namespace { // }</li>
<li>To combine global non-namespaced code with namespaced code, only bracketed syntax is supported</li>
<li>We can alias a namespace name to use a shorter name for the class you are extending incase your class is in separate namespace <br />namespace&nbsp;com\rsumilang\util; <br />use&nbsp;com\rsumlang\common&nbsp;as&nbsp;Common; <br />class&nbsp;String&nbsp;extends&nbsp;Common\Object</li>
<li>FQCN (Full Qualified Class Name)</li>
<li>__NAMESPACE__&nbsp;constant is useful for dynamically constructing names</li>
<li>The&nbsp;use&nbsp;keyword must be declared in the outermost scope of a file (the global scope) or inside namespace declarations</li>
<li>Without any namespace definition, all class and function definitions are placed into the global space</li>
<li>Prefixing a name with&nbsp;\&nbsp;will specify that the name is required from the global space even in the context of the namespace</li>
</ul>
