#language #kotlin #basics
# Kotlin basics
## Variables
var => mutable  
val => immutable = read only  

Top-level properties and class properties must be initialized.  
Local variables can be declared but not initialized
```kotlin

val data: Int // ERROR
val data: Int = 10 // OK

class MyClass() {
	val data: Int // ERROR
	val data: Int = 10 // OK
	
	fun myFun() {
		val data: Int // OK
	}
}

```

**Properties**  
Properties (class member variables) all have getter and setter. This means we can custom the accessors ourselves.  

**Lateinit and lazy**

`lateinit` allows us to initialize the property after creating an object. There are rules: 
- only var properties can use it
- only on class member and top level properties, not on constructor
- nullable cannot use it
- property should not be a primary type

`lazy` allows us to wait to initialize the property until we use it.  
We define an initial value but it is not initialized.  
Rules:
- val/var can use it
- can be used on primary constructor
- use `by lazy{}`

```kotlin
val data: String by lazy {
	println("lazy")
	"hello" // initial value
}
```


## Data types
**Any type**  
Everything is an object.  
Every Kotlin class has `Any` as superclass

**Unit type**   
Return type when there is no return statement.  

**Nothing type**  
Show explicitly there is no value  

**Type check**  
We can use `is` to check the type of variable.  
It checks and casts automatically:
```kotlin
fun isOperator(obj: Any): Int? {
	if (obj is String) {
		return obj.length // automatically casts to String
	}
	return null
}
```

**Type casting**  
No implicit conversion for numbers, should use toXXX() function:  
`toDouble()` for example  

Kotlin supports `as` operator to cast to super types  

## Array, lists and maps  
**Arrays**  
We can create arrays by constructor, or assignment.  
We can use generic types, no types, or specify the type  
```kotlin
var array = arrayOf(1, "one", true)

var array2 = arrayOf<Int>(1, 2, 3)
var array3 = IntArrayOf(1, 2, 3)
```

**Lists, sets, maps**  
Default is immutable `mapOf()` `listOf()  
We can create mutable with `mutableMapOf()` `mutableListOf()`   

## Functions
**Single expression function**  

If a function has only one expression, you can omit the {} and use = symbol.
Single expression function can omit the return type.  These are equivalent:
```kotlin
fun add(a: Int, b: Int) = a+b 

fun add(a: Int, b: Int): Int {
	return a+b
}
```

**Function overloading**  
Multiple function can have the same name but different parameters  

**Named arguments**  
If a function has multiple arguments with some default value, we can pass only the parameters we want with their name:
```kotlin
fun sayHello(name: String = "default", number: Int)

sayHello(number = 1)
```

## Conditional Expressions
**IF**  
`If` statement are expressions => They return a value.  
If we use `If` as an expression, we must use `else` too. 
```kotlin
val result = if (a > 10) "hello" else "world"
```

**WHEN**
Similar to `switch` in other languages.  
When can also be used as expressions => must use `else`  
```kotlin
when(arg) {
	1 -> println("is one")
	10, 20 -> println("is either 10 or 20")
	30 -> {
		val result = arg as Int * 10
		println("arg is 30")
	}
	is Int -> println("arg is an Int")
	else -> println("waddup")
}
```

## Loops
**For loops**  
Kotlin uses keywords
```kotlin
for (i in 1..10) // 1 to 10 included
for (i in 1 until 100) // 1 to 9
for (i in 2..10 step 2) // iterates 2 by 2
for (i in 10 downTo 1) // Decrement
```
We can use `.indices` to get the indices of a list.  
We can use `.withIndex()` to get index and values.  
```kotlin
for ((index,value) in list.withIndex()) {}
```

**Continue and Break**  
We can use break and continue like in other languages.  
We can use a label to go to a specific label with `@`  
```kotlin
myLabel@ for (i in 1..3) {
			for(j in 1..3) {
				if (j > 1) break @myLabel // if j> 1 it will go back to the label
				println("yep")
			}
		}
```

## Null safety
**Elvis operator**  
Allows to perform operation only for null values => `?:`
```kotlin
length = data?length ?: -1 // if the property is null, length will be -1
```

**Null pointer exception**  
The `!!` operator throws an exception is the property is null
```kotlin
data!!.length
```

**Null safe casting**  
Returns null if the cast is not successful => `as?`
```kotlin
strData as? Int
```