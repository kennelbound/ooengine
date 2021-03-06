ooengine
========

Intuitive pseudo object orientation for bash (Shell Script)

Project maintainance:
--------------------------------------
This was more of an experiment whether I can get some of OO greatness into bash scripts.
I'm not planning to continue any of it at the moment.
But feel free to fork it if you are interested!


Features:
--------------------------------------
1. "Classes" containing "methods".
2. Created objects saved in variables.
3. Public / private attributes.
4. Inheritance (extending classes).
5. Traits (multiple inheritance).
6. Object cloning.
7. Exceptions - throw and catch them.

As intuitive as possible (it's still bash though).

Crash course:
--------------------------------------
1. 'Classes' are functions, prefixed with 'class::'.
2. 'Methods' are functions within classes, prefixed with 'method::'.
3. 'Objects' are created by calling new [Class name], save it's return value into a variable.

Example:
--------------------------------------

```shell
#!/bin/bash
source ooengine || exit 1

# A simple base class named 'TestClass'.
class::TestClass() {

  # Public attribute, 'get' and 'set'-able.
  public attributePublic "optional default value"

  # Private attribute, only internal 'get' and 'set'-able.
  private attributePrivate "optional default value"

  # Public method, reachable with any reference.
  method::publicTestMethod() {
    echo "Do something here."
    # Call private method.
    $this internalTestMethod
  }

  # Public getter method for private attribute 'attributePrivate'.
  method::getAttributePrivate() {
    $this get attributePrivate
  }

  # Public setter method for private attribute 'attributePrivate'.
  method::setAttributePrivate() {
    $this set attributePrivate "$1"
  }

  # Private method, only internal reachable with $this reference.
  __method::internalTestMethod() {
    echo "Or do something here."
  }
}

# Create an object of the class.
testObject=$(new TestClass)

# Call a method.
$testObject publicTestMethod

# Get a public attribute.
value=$($testObject get attributePublic)
echo $value

# Set a public attribute.
$testObject set attributePublic "New value"

# Get a private attribute.
# echo $($testObject get attributePrivate) # This would fail.
value=$($testObject getAttributePrivate)
echo $value

# Set a private attribute.
# $testObject set attributePrivate # This would fail.
$testObject setAttributePrivate "New value"

# Destruct the object.
$testObject destruct
```

More?
--------------------------------------
Please have a look at the examples in ./examples directory!


Packed libraries
--------------------------------------
- Console (Incomplete) - Console/IO help functions.
- String (Incomplete) - String class.
- Array (Incomplete)
- MySQL (Incomplete)
- ...

Using libraries
--------------------------------------

Use libraries by importing them:

```shell
import String # (searches for $librarypath/String/String)
import String/StringManipulation # (searches for $librarypath/String/StringManipulation)
```

Use own library directories:

```shell
add ./mylibraries
import MyLibrary
import MyLibrary/SubClass
```
