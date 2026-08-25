<h1 align="center">Kotlin Introduction (with Java equivalents ) </h1>
## Before You Start 

This only covers the programming concepts that I've frequently used in FRC programming.  Its goal is to build a strong foundation through a few hands-on activities and examples. However, it does not cover every single concept, as I plan on introducing more advanced topics when they're useful and/or as extra optional chapters if I have time.  

If you would like a more comprehensive introduction to Java, I would recommend checking out [Bro Code's YouTube video](https://www.youtube.com/watch?v=xTtL8E4LzTQ), [Code Academy's free Java course](https://www.codecademy.com/learn/learn-java), or [JetBrains' Java courses](https://lp.jetbrains.com/academy/learn-java/). 

Since my team writes primarily in Kotlin, this is primarily written for Kotlin; however, I will put the Java 25 (what WPILib currently uses) equivalent code and explanation (when needed) behind a 

> [!info]- Java Callout
> This is where any Java-specific stuff will be 

Similarly, I will be providing example code for how I would go about doing something using only the principles that were covered up to this point. If your version is different, that's fine - we each write code differently.
>[!note]- Example code
>```java
>IO.println("test")
>```

There are optional challenges you can do,  more in-depth explanations, or extra information behind the 
>[!info]- Optional Challenges
>This is where I would put the challenge

>[!info]- In-depth Explanations or extra information
>this is where I will put the in-depth Explanations 


## What are Programs

A program is a set of instructions that tells the computer what to do, like how a recipe tells us how to make something. 

```text
Gather ingredients
Mix dry ingredients 
Mix wet ingredients 
Mix dry and wet ingredients together 
Cook mixture for 30 min at 400 degrees 
Output/result cake.
```

However, unlike humans, computers will follow the instructions exactly as the program describes. So, for example, a human can understand "mix dry ingredients", but a computer won't know what it needs to mix, how long it should be mixed,  nor what should be used to mix it. Instead, we have to break it down into steps that it can understand.   So, "mix dry ingredients" becomes something like this:

```text
Grab flour  
Grab sugar  
Grab salt  
Grab bowl  
  
Measure 1 cup flour into bowl  
Measure 1 cup sugar into bowl  
Measure 1/4 tsp salt into bowl  
  
Mix bowl contents for 3 minutes
```

## Installing An IDE

Integrated Development Environments, or IDEs, are popular tools that allow programmers to write, debug, and run code within one application. You can use whichever one you want, but I've linked a guide to setting up IntelliJ for FRC since that is what I use. 

[How to Install and Set Up IntelliJ](@todo )

## Writing A Program
When you first create a Kotlin project with IntelliJ, the first thing you'll probably see is something similar to this, but with a few tips and explanations.

```kotlin
	fun main(){
		val name = "Kotlin"
		println("Hello" + name)
		for(i in 0..5){
				println("i = $i")
		}
	}
``` 

>[!info]- Java Equivalent
>```java
>void main() {  
>	IO.println(String.format("Hello and welcome!"));
>	
>	for (int i = 1; i <= 5; i++) {
>		IO.println("i = " + i); 
>	}
>}
>```


You don't need to know what everything means; I'll cover that later. For now, just replace everything with this and run the code by clicking on the green arrow at the top of the screen.


```kotlin
fun main(){
	println("Hello World")
}
``` 

>[!info]- Java Equivalent
>```java
>		void main() {
>			IO.println("Hello World");
>		}
>```

This should cause a panel to appear on the bottom third of IntelliJ. This is called the console, and it is where the code runs.  

Near the top of the console is a really long line of text. This is just IntelliJ telling your computer to run the code with the file you're writing, and you can ignore it. 

But below it you should see 
```bash
Hello World
```
>[!info]- How programs run
>Most programs run from the top of `main()` to its bottom.
>
>So something like 
>```Kotlin
>fun main(){
>	println("one")
>	println("two")
>	println("three")
>}
>```
>will print
>```
>one 
>two 
>three
>```
>This is because the program starts at the top of the code and works its way down. So it will run  `println("one")`, then `println("two")`, and finally `println("three")`
>
>You can assume that code follows this behavior unless explicitly said otherwise.


This is because the `println("Hello World")` tells the computer to print the text in the parentheses to the console.


>[!note]- Ways to Write to the Console 
>1. Kotlin
>	- You can write on the same line several times with `print()`
>	- When you use `println()`, it prints the text you give it and then moves to the next line. Anything printed afterward will appear on a new line.
>	- When you want the next printed text to be on the next line, you use `println()`
>2. Java
>	- Similar to Kotlin, to write on the same line several times, you use `System.out.print();`
>	- `IO.println()` does the same as Kotlin's `println()`
>	

Now try changing the text and adding more print statements to see what happens 

>[!info]- If you get a Java error
>In Java, when the computer is performing a task like writing to the console, you'll need a semicolon at the end.  Since without it, you'll `java: ';' expected` in the console.

## Getting Inputs from the User
So far, all this code can do is just print the same thing over and over, so how about we add some user interaction. In Kotlin, it's pretty easy to do so with 
```kotlin
readLine()
```
Since the function `readLine()`(we'll cover what functions are later) will wait for the user to type something into the console and press Enter. Once they do so, the `readLine()` is replaced by the text the user typed into the console.

>[!note]- Combining Text
>**Although Java has a different way to get user input (I'll get to that later), combining text is the same for both Kotlin and Java**
>
>Sometimes we want to include what the user typed as part of a larger message. For example, 
>```Kotlin
>println("What year is it?")
>print("It is already " + readLine() + "!?!?!")
>```
>As a result, the console will print 
>```
>What year is it?
>2026 <- User input
>It is already 2026!?!?!
>```
>The + lets us combine multiple pieces of text into a single message.
>

So something like this 
```kotlin
fun main() {
	println("Hello, what year is it?")
	println("Really, it is " + readLine())
}
```

will first print  
```
Hello, what year is it?
```

then it will pause until the user types something and presses Enter 
```
Hello, what year is it?
2026 <- User input
```

Then it will continue running the rest of the code 
```
Hello, what year is it?
2026 <- User input
Really, is it 2026
```

>[!info]- Java Equivalent 
>Before reading from the console, we must first make a Scanner. Don't worry about what it is, since I'll get to that later.
>```
>Scanner input = new Scanner(System.in);
>```
>Now you can get the input.
>```java
>import java.util.Scanner;
>
>void main(){
>	Scanner input = new Scanner(System.in);
>	IO.println("What year is it?");
>	IO.println("Really, is it " + input.nextLine());
>}
>```


## Activity 1:
For Activity 1, let's make a greeter that can:
- Ask for the user's name and greet them 
- Ask if you can take the user's coat
- Respond to their answer

```
Hello, what is your name?  
John <- User input  
  
Nice to meet you, John. May I take your coat?  
yes <- User input  
  
yes, okay, then you can follow me.
```
>[!note]- Hint
>How do you print a message and the user's input on the same line?

>[!note]- Example Code
>>[!note]- Kotlin
>>```Kotlin
>>fun main(){
>>	println("What is your name?")
>>	println("Nice to meet you " + readLine() + ". May I take your coat?")
>>	println(readLine() + ", okay, then follow me.")  
>>}
>>
>>```
>
>>[!note]- Java
>>```Java
>>import java.util.Scanner;
>>
>>public class Main{
>>	 void main() {
>>		Scanner input = new Scanner(System.in);
>>		IO.println("What is your name?");
>>		IO.println("nice meet you " + input.nextLine() + ". May I take your coat?");
>>		IO.println(input.nextLine() + ", okay, then follow me.");
>>	}
>>}
>>```

## Variables
Suppose I asked you to do Activity 1 again, but this time you had to use both the user's name and response.  It would be awkward because the code has no way to remember what the user typed. As a result, you would have to ask for the user's name, leading to something like this.
```
What is your name?
John <- User input

Nice to meet you John, may I take your coat?
no <- User input

no, okay

What is your name?
John <- User input

John, then follow me.
```

This is where variables come in, since they allow us to store information that we can use again later.

Take, for example, the two sentences: 

"I like apples"
"They are good"

Although the second sentence never explicitly says "Apples are good", we understand that `they` refers to apples. This is because `they` points back to the apples mentioned earlier. Variables work in a similar way. They store a value that we can repeatedly use without needing to ask for the same information every time. So by adding this: 

```Kotlin 
var name = readLine()
```
This creates a variable called `name`, and whatever the user typed will be stored inside of it.

You can use the user's name several times without needing to ask. This makes using both the user's name and their response really easy:  
```Kotlin
fun main(){
	println("What is your name?")
	var name = readLine()
	
	println("Nice to meet you " + name + ". May I take your coat?" )
	println(readLine() + ", okay " + name + ", then follow me")

}
```

>[!info]- Val vs Var
>In Kotlin, there are two types of variables: `val` and `var`.
>
>A `var` can be changed after it has been created.
>A `val` can't be assigned a new value after it has been created.
>
>So this works:
>```Kotlin
>var name = "John"
>name = "Bob"
>```  
>
>However, this won't work:
>```Kotlin
>val name = "John"
>name = "Bob"
>```
>>[!info]- In-depth Explanation 
>>
 >>Imagine you're baking a cake, and only have one measuring cup, so you have to use it for several different ingredients. Throughout the process, the contents of the cup change from things like flour to sugar to water.  That doesn't mean you can't check what's stored in the cup, only that it might be different. `vars` are like that. Even if what they're holding changes, you can still check and use what's inside it.
 >>
 >>Unlike its contents, the measuring cup itself doesn't change. Even if you put stuff in it, the measuring cup will still be the same measuring cup that you started with. Similarly, you can still interact with and use the `val`, but you can't change the `val` itself.

>[!info]- Java Equivalent
>Similar to Kotlin's `var`s, Java's variables can be changed after they're created, but creating them is a little bit different. In Java, you must specify what kind of data the variable will store. This allows Java to catch mistakes, like trying to do math with text, before the code runs.  For example, storing text would look something like this:
>```Java
>String name = "John";
>name = "Bob";
>```
>However, trying something like this wouldn't: 
>```Java
>String age = 13;
>```
>Instead, you can either do:
>```Java 
>String age = "13";
>int age = 13;
>```
>
>All you need to know is:
>`String` = text
>`int` = whole number 
>`double` = decimal number 

## Activity 2: 
For Activity 2, let's create a customer before they enter the restaurant.
- Ask the user what type of outerwear they're wearing 
- Ask the size of the party 
- Update the greeter's responses to match the information

It should look something similar to this: 
```
What type of outerwear are you wearing: Hoodie <- User input
What is the size of the party: 5 <- User input

___________
Hello, what is your name? 
John <- User input
Nice to meet you, John. May I take your Hoodie? 
no <- User input
no, okay John, follow me to your table for 5
```
>[!note]- Example Solution
>> [!note]- Kotlin
>> ```Kotlin
>> fun main(){
>> 	print("What type of outerwear are you wearing:")
>> 	val outerwear = readLine()
>> 	print("What is the party size:")
>> 	val partySize = readLine()
>> 	
>> 	println("___________")
>> 	println("Hello, what is your name?")
>> 	val name = readLine()
>> 	println("Nice to meet you, " + name +". May I take your " + outerwear)
>> 	val takeOuterwear = readLine()
>> 	println(takeOuterwear + ", okay " + name + ", follow me to your table for " + partySize)
>> }
>> ```
> 
>>[!note]- Java
>>```Java
>>import java.util.Scanner;
>>public class Main{
>>	void main(){
>>		Scanner input = new Scanner(System.in);
>>		System.out.print("What type of outerwear are you wearing:");
>> 		String outerwear = input.nextLine();
>> 		System.out.print("What is the party size:");
>> 		String partySize = input.nextLine();
>> 		
>> 		IO.println("___________");
>> 		IO.println("Hello, what is your name?");
>> 		String name = input.nextLine();
>> 		IO.println("Nice to meet you, " + name +". May I take your " + outerwear);
>> 		String takeOuterwear = input.nextLine();
>> 		System.out.print(takeOuterwear + ", okay " + name + ", follow me to your table for " + partySize);
>>		}
>>
>>}
>>```

>[!info]- Naming Conventions
>Imagine you're working on a project where everyone named their variables differently. So something as simple as party size could look like: 
>```Kotlin
>var partysize = 3
>var Partysize = 3
>var PartySize = 3 
>var partySize = 3
>var numberofpeople = 3
>```
>Sure, all of them work, but some of them can be harder to read since some of the words blur together: 
>```Kotlin
>var partysize = 3
>```
>On the other hand, `partySize` is much easier to read since you can clearly see both words.
>
To make code easier to read and consistent, Kotlin and Java programmers tend to use camelCase. This means the first word starts lowercase, and any additional words start with an uppercase letter.  As a result, it is far easier to tell where one word ends and the next begins. 
>
So party size becomes :
>```Kotlin
var partySize = 3
>```

## Conditional
Up until now, the program has been following the same path no matter what the user types. However, real programs often need to make decisions. For example, if the greeter asks "May I take your coat?", their response should be different depending on  whether the user answers `"yes"` or `"no"`.


```Kotlin 
println("May I take your coat?")
var response = readLine()

if(response == "yes"){
	println("I'll put up your jacket")
}
```
The part inside the parentheses is called a condition. A condition is something the computer checks to see if it's true or false. So: 
```Kotlin
(response == "yes")
```
checks if `response` is equal to `"yes"`. If it is, then the code inside the `{ }` will be run. If it is false, the code inside the `{ }` is skipped  

### Else
 What if they answered something different than "yes"? Well, that can be handled with an `else`:
```Kotlin 
println("May I take your coat?")
var response = readLine()

if(response == "yes"){
	println("I'll put up your jacket")
}else{
	println("Okay, you can keep it on you")
}
```
In this example, if `(response == "yes")` was false, then the computer will move on to the else and run its code. However, if it was true, then the `else` would be skipped.

### Else If
What if the user typed `"sure"`? 
```Kotlin 
println("May I take your coat?")
var response = readLine()

if(response == "yes"){
	println("I'll put up your coat")
}else if(response == "sure"){
	println("I'll put up your coat")
}
```
`else if` lets us check another condition if the previous one was false.  However, if any of the conditions above it are true, then the remaining `else if` statements will be skipped.

If `response` was not equal to `"yes"`, then the program checks the next `else if` conditions. There, the computer would check if the second `if` condition was true. If that is also false, then nothing will be run.  
 
>[!notes]- More comparisons
>In Kotlin, we are not just limited to checking if two values are equal. Take, for example, the following comparison operators. 
>```Kotlin
>var num1 = 3
>var num2 = 6
>
>num1 == num2 //false. Checks if num1 is equal to num2
>num1 != num2 // true. Checks if num1 is not equal to num2
>num1 > num2 // false, Checks if num1 is greater than num2
>num1 < num2 // true.  Checks if num1 is less than num2
>num1 >= num2 // false. Checks if num1 is greater than or equal to num2 
>num1 <= num2 // true. Checks if  num1 is less than or equal to num2
>``` 

>[!info]- Dealing with Uppercases when comparing text 
>In Kotlin and Java alike, uppercase letters are treated as different characters. So, even though "yes" and "Yes" are the same word, they are considered not equal. This means `"Yes" == "yes"` will always be false. Although there is a simple fix :
>
>```Kotlin
>var response = readLine()?.lowercase() 
>```
>This will change the text from `readLine()` into lowercase. You might notice the `?` before the `.lowercase()`. For now, just include it whenever you use `readLine().lowercase`, I'll cover why later.

>[!note]- Java Equivalent
>In Java, you use `.equals()` to check whether the text on the left is the same as the text inside the parentheses . For example, 
>```Java
>void main(){
>	Scanner input = new Scanner(System.in);
>	IO.println("May I take your coat?");
>	String response = input.nextLine();
>	
>	if(response.equals("yes")){
>		IO.println("I'll take your coat");
>	}
>	
>}
>```
>So if the user types in `"yes"`, then `I'll take your coat` is printed
>
In Java, you use `text.toLowerCase()` instead of `text.lowercase`. 


## Activity 3 
Up until now, the greeter dialogue has been centered around the belief the user made a reservation. However, that is not always true. Some people might prefer to make a reservation, while others may choose not to. So let's give the user the choice to make a reservation that determines how the greeter responds.
- Before the user goes to the restaurant, ask if they want to make a reservation
- If the user decide to make a reservation, ask for a name and party size
- When they arrive at the restaurant, the greeter asks if they have a reservation 
	- If they say yes, ask for the name 
- Verify that the reservation actually exists  
- Greeters dialogue reflects if they made a reservation  
Example 1- the user made a reservation 
```
Do you want to make a reservation before heading to the restaurant? 
yes <- User input
Who is the reservation for?
john <- User input
How many people will there be? 
3 <- User input 
Okay your reservation is made 

You head to the restaurant 

Hello, do you have a reservation? 
yes <- User input
Who made the reservation 
john <- User input 
.... Old greeter dialogue here ....
```
Example 2- The user didn't make a reservation 
``` 
Do you want to make a reservation before heading to the restaurant?
no <- User input 
You head to the restaurant 

Hello, do you have a reservation? 
yes <- User input
Who made the reservation 
john <- User input 

Sorry, there is no reservation under that name
```

>[!note]- Example Code
>Later, I'll cover how to combine these checks so we don't need to repeat the same code multiple times. 
>>[!note]- Kotlin
>>```Kotlin
>>fun main(){
>>	var name = ""
>>	var partySize = "0"
>>	
>>	println("Do you want to make a reservation before heading to the restaurant? ")
>>	var response = readLine()?.lowercase()
>>	
>>	if(response == "yes"){
>>		println("Who is the reservation for?")
>>		name = readLine().toString()
>>		
>>		println("How many people will there be?")
>>		partySize = readLine().toString()
>>		
>>		println("Okay your reservation is made ")
>>	}else if(response == "sure"){
>>		println("Who is the reservation for?")
>>		name = readLine().toString()
>>		
>>		println("How many people will there be?")
>>		partySize = readLine().toString()
>>		
>>		println("Okay your reservation is made ")
>>	}else if(response == "ya"){
>>		println("Who is the reservation for?")
>>		name = readLine().toString()
>>		
>>		println("How many people will there be?")
>>		partySize = readLine().toString()
>>		
>>		println("Okay your reservation is made ")
>>	}
>>	
>>	println("You head to the restaurant ")
>>	
>>	println("Hello, do you have a reservation?")
>>	response = readLine()?.lowercase()
>>	if(response == "yes"){  
>>		println("Who made the reservation ")  
>>		val nameCheck =  readLine().toString().lowercase()  
>>		
>>		if(nameCheck == name.lowercase()) {  
>>			println("Nice to meet you, " + name + ". May I take your coat")  
>>			val takeOuterwear = readLine()  
>>			println(takeOuterwear + ", okay " + name + ", follow me to your table for " + partySize)  
>>		}else{  
>>			println("There are no reservations under this name")  
>>			println("Please wait for a table to be available")  
>>		}  
>>	}else{
>>		println("Please wait for a table to be available")
>>	}
>>}
>>```
>
>>[!note]- Java 
>>```Java
>>import java.util.Scanner;
>>
>>class Main{
>>	void main(){
>>		Scanner input = new Scanner(System.in);
>>		String partySize = "";
>>		String name = "";
>>		
>>		IO.println("Do you want to make a reservation before heading to the restaurant? ");
>>		String response = input.nextLine().toLowerCase();
>>		if(response.equals("yes")){
>>			IO.println("Who is the reservation for?");
>>			name =  input.nextLine();
>>			
>>			IO.println("How many people will there be?");
>>			partySize =  input.nextLine();
>>			
>>			IO.println("Okay your reservation is made ");
>>		}else if(response.equals("sure")){
>>			IO.println("Who is the reservation for?");
>>			name =  input.nextLine();
>>			
>>			IO.println("How many people will there be?");
>>			partySize =  input.nextLine();
>>			
>>			IO.println("Okay your reservation is made ");
>>		}else if(response.equals("ya")){
>>			IO.println("Who is the reservation for?");
>>			name =  input.nextLine();
>>			
>>			IO.println("How many people will there be?");
>>			partySize =  input.nextLine();
>>			
>>			IO.println("Okay your reservation is made ");
>>		}
>>	
>>		IO.println("You head to the restaurant ");
>>	
>>		IO.println("Hello, do you have a reservation?");
>>		response =  input.nextLine().toLowerCase();
>>		if(response.equals("yes")){  
>>			IO.println("Who made the reservation ")  ;
>>			String nameCheck = input.nextLine().toLowerCase();
>>			
>>			if(nameCheck.equals(name.toLowerCase())) {  
>>				IO.println("Nice to meet you, " + name + ". May I take your coat");
>>				String takeOuterwear =  input.nextLine();  
>>				IO.println(takeOuterwear + ", okay " + name + ", follow me to your table for " + partySize);
>>			}else{  
>>				IO.println("There are no reservations under this name");
>>				IO.println("Please wait for a table to be available");
>>			}  
>>		}else{
>>			IO.println("Please wait for a table to be available");
>>		}
>>	}
>>}
>>```

## Type Conversion
If you look back at `partySize`, you'll notice we initially store it like this :
```Kotlin
var partySize = "0"
```
Even though 0 is a number, Kotlin will treat it like text since it's placed inside of quotes. This becomes an issue if we try something like this: 
```Kotlin
partySize < 3
```
 Kotlin will give an error. Why? Because, Kotlin sees `partySize` as text, while `3` is a number. Kotlin treats the text and number as different types of data, so it doesn't know how to compare them. To compare them, we first have to change the text into a number. 

>[!info]- Important - Types of Data
>
>Not all information is stored in the same way.  The way it is stored affects what we can do with it. Take someone's name, for example. You might want to convert it to lowercase or use just the first letter. You probably won't need to do math with it.  On the other hand, you will probably need to do math with numbers, but you probably won't need to add additional symbols to it.
>
>Because of this, Kotlin uses several different data types to store information.
>	- Booleans: `var takeCoat = true`. They can only hold true or false
>	- Int: `var partySize = 3`. They can only hold whole numbers
>	- Double: `var average = 3.2` .They can hold numbers with decimals 
>	- Char: `var firstInitial = 'J'`. They can only hold one letter or symbol
>	- String: `var name = "John"`. They store text

To convert a String into a number is pretty simple : 
```Kotlin
var partySize = "3".toInt() 
//or
partySize = readLine()!!.toInt()
```
Although, if the user doesn't type a whole number, then the code will **crash**. You might notice the `!!` after `readLine()`. For now, just include it whenever you use `readLine()`. I'll explain why later.

>[!info]- You can't change the type of Variables 
>Once you create a variable like 
>```Kotlin
>var name = "John"
>```
>the var `name` can only hold Strings, so this won't work
>```Kotlin
>var name = "John"
>name = 3 //Error
>```
>So if you want to store other type of data in a variables, you must create a new variable 
>```Kotlin
>var name = "John"
>var age = 3
>```

>[!info]- Ways to Convert Types
>```Kotlin
>var partySize  =  "3".toDouble() // or .toInt();
>var takeCoat = "false".toBoolean()
>
>var partySize = 3.toString()
>var takeCoat = false.toString()
>```

>[!info]- Better way to print
>Up until now you've probably been doing something like this:
>```Kotlin 
>println("The party size is " + partySize)
>```
>Sure this works, but it can get a bit messy once you start adding multiple variables and the first thing you print is a number.
>
> For example: 
>```Kotlin
>val age = 17
>val name = "John"
>val questionNum = 1
>println(questionNum + ": " + name + " what was your favorite food when you were " + age + " years old")
>``` 
>This would not work because  Kotlin does not know how to add a String to an Int. As a result, it will cause an error and it's pretty messy to read. Fortunately, both issues can be fixed with something called string interpolation. 
>
>String interpolation lets us place variables directly into strings using `$`:
>```Kotlin
>val age = 17
>val name = "John"
>val questionNum = 1
>println("$questionNum: $name what was your favorite food when you were $age years old")
>```

### Handling bad inputs
Take a look at this code:
```Kotlin
println("What year is it?")
response = readLine()!!.toInt()
```
Everything works fine as long as the user enters a number. But what do you think would happen if the user did this:

```
What year is it?
apple
```
Since `"apple"` cannot be converted into an `Int`, the program crashes. Instead of letting that happen, we can tell Kotlin what to do if the conversion fails by using a `try`-`catch` block.

```Kotlin
println("what year is it?")
var response: Int = 0
try{ 
	response = readLine()!!.toInt()	
} catch (e: NumberFormatException) {
	println("please enter a number next time")
}
```
	
The `try` block attempts to run the code inside its `{}`. If something goes wrong,  Kotlin will stop running its code and move on to the `catch` block.

The `catch` block receives information about what went wrong inside the `try` block in the variable `e` . If the error is a `NumberFormatException`, Kotlin runs the `catch` block and stores information about the error in `e`.  Then the code inside the `catch` block runs, and once it finishes, the program continues with the code below the `try`-`catch` block. However, if a different kind of error occurs, this `catch` block won't handle it, and the program will still crash.

>[!note]- Types in Java
>Java tends to be stricter about types than Kotlin. For example, using the wrong number type can cause 3/4 to be equal to 0. 
>
>>[!info]- Variables
>>Up until now you have been using code like this:
>>```Java
>>String name = "John";
>>```
>>let's break it down
>>- `String` tells the computer what type of data will be stored. In this case, name will be a string.
>>- `name` tells the computer that whatever data stored within it can be accessed through `name`.
>>- `=` stores the value on the right inside of the variable on the left
>>- `"John"` is the value being stored
>>- After this line runs, `name` will store `"John"`
>
>>[!info]- Type Conversion
>>Compared to Kotlin, converting strings into other types is a bit trickier in Java.
>>```Java
>>Scanner input = new Scanner(System.in);
>>String wholeNum = "3";
>>String decimalNum = "2.1";
>>String bool = "true";
>>
>>int num1 = Integer.parseInt(wholeNum);
>>double num2 = Double.parseDouble(decimalNum);
>>boolean trueOrFalse = Boolean.parseBoolean(bool);
>>```
>>The parse methods take whatever String is inside the parentheses and convert it into the type on the left. Although, converting numbers between doubles and ints is simpler.
>>```Java
>>int num1 = 3;
>>double num2 = (double) num1;
>>``` 
>>The `(double)` takes the value to its right and turns it into a double. You can also convert an expressions like this :
>>```Java
>>double num2 = (double) (num1 + 3);
>>``` 
>
>>[!info]-  Int and Double math 
>>What would happen if you tried this:
>>```Java
>>IO.println(3/4);
>>```
>>You would expect it to print `0.75`, but it won't. Instead you'll see `0`. 
>>This is because both numbers are `int`s.  When Java divides two ints, known as integer division, the results must also be int. Since ints can't store decimals, the decimal part is not part of the answer. 
>>But, as long as one of the numbers is a double, then Java will perform decimal division.  So these would work
>>```Java
>>double num1 = 3.0;
>>int num2 = 4;
>>IO.println(num1/num2);
>>``` 
>>```Java 
>>IO.println(3.0/4);
>>```
>>```Java
>>IO.println((double) 3/4);
>>//This works because the double converts the 3 into 3.0 before any math is done.
>>```

>[!info]- Clarifying Something
>You can do `"3" < "-1"` in Kotlin, however its not recommended nor is it good practice.  

## Activity 4: 
Currently, the restaurant can only reserve one table per party. Although this works for smaller groups, it wouldn't work for larger groups. After all, a party of 12 or more people will need more space than a party of 4. So, let's write some code that will choose the correct tables based on the party's size.
There are three seating options
	-A small table that seats up to 4 people 
	-A large table that seats up to 8 people 
	-Two large tables that seat up to 16 people.
Reserve tables using the following rules 
	-1-4 people : Small table
	-5-8: large table 
	-9-16: two large tables
	-more than 16: Tell them the restaurant cannot currently seat their party. 

```
What is the party size?
13 <- User input 
Okay, your reservation for two large tables is done.
```

>[!note]- Example code 
>>[!note]- Kotlin
>>```Kotlin
>>println("What is the party size")
>>var response = readLine()?.toInt()
>>if (response <= 4){
>>	println("Okay, your reservation for one small tables is done.")
>>}else if (response <= 8){
>>	println("Okay, your reservation for one large table is done.")
>>}else if (response <= 16){
>>	println("Okay, your reservation for two large tables is done.")
>>}else{
>>	println("We can't currently seat your party of $response")
>>}
>>```
>
>>[!note]- Java
>>```Java
>>Scanner input = new Scanner(System.in);
>>IO.println("What is the party size");
>>
>>String response = input.nextLine();
>>int partySize = Integer.parseInt(response);
>>
>>if (partySize <= 4){
>>	IO.println("Okay, your reservation for one small table is done.");
>>}else if (partySize <= 8){
>>	IO.println("Okay, your reservation for one large table is done.");
>>}else if (partySize <= 16){
>>	IO.println("Okay, your reservation for two large tables is done.");
>>}else {
>>	IO.println("We can't currently seat your party of " + partySize);
>>}
>>```

## Functions 
Take a look at the program you have been working on. You probably noticed the same code is used several times. 
```Kotlin
println("Who is the reservation for?")
name = readLine().toString()

println("How many people will there be?")
partySize = readLine().toString()	

println("Okay your reservation is made ")
```
Even though the same code appears several times,  it always does the same thing. The only thing that changes is which answer caused the code to run. Rewriting the same code over and over only makes the code longer, harder to read, and harder to fix.After all, if you made a mistake in the original code, you would have to fix every single copy.

It would be nice if we only had to write this code once and reuse it whenever we need to.

That is exactly what a function is for.

A function is a named block of code. Instead of rewriting the same code over and over, you can place it inside a function and run it whenever you need it. Take this function, for example, which takes two inputs from the user and prints out which is bigger: 
```Kotlin
fun whichIsBigger(){
	println("what is the first number")
	val num1 = readLine()!!.toInt()
	
	println("what is the second number")
	val num2 = readLine()!!.toInt()
	
	if (num1 > num2){
		println("$num1 is bigger than $num2")
	}else if (num1 < num2){
		println("$num2 is bigger than $num1")
	}else {
		println("$num1 is equal to $num2")
	}
}
```
- `fun` tells Kotlin that we want to create a function
- `whichIsBigger` is the function's name we're creating
- The code inside the `{}` runs whenever `whichIsBigger()` is called. 


To use this function, all we have to do is this:
```Kotlin
whichIsBigger()
```

### Adding Parameters 
There is one issue with the code above: The user has to type the numbers and you can't choose which numbers are compared. 

To fix that, we add parameters. They let us pass information into the function. 

Take a look at the same function from earlier but with parameters: 
```Kotlin
fun whichIsBigger(num1 : Int, num2 : Int){	
	if (num1 > num2){
		println("$num1 is bigger than $num2")
	}else if (num1 < num2){
		println("$num2 is bigger than $num1")
	}else {
		println("$num1 is equal to $num2")
	}
}
```
Now we can choose which numbers get used.
```Kotlin
whichIsBigger(3,4)
```
When the function runs, `num1` becomes `3` and `num2` becomes `4`, in that order.  This is because: 
- `num1 : Int` tells Kotlin that the first parameter must be an `Int`.
- the `,` separates the parameters and allows for multiple parameters.
- `whichIsBigger(3,4)`: The numbers in the parentheses are the values that Kotlin will store in num1 and num2.  

### Parameters are `Val`s
When you pass something into a function, Kotlin creates `val` for it. This means it can read what is stored, but it won't be able to change the parameter itself. 

So something like this won't work :
```Kotlin
fun addOne(num1 : Int) : Int{
	return num1 = num1 + 1// Creates an error
}
```

Instead you could do something like this
```Kotlin
fun addOne(num1: Int) : Int{
	var num = num1 + 1
	return num
}
```
This works because function parameters are read only. So if you want a modified version of a parameter, you'll need to create a new variable for it.  

### Returning Values 
So far, the functions I've shown were passed information. However, functions can send back information using a `return`. However, whenever you `return` something, the function stops running.

Here is an updated version of `whichIsBigger` that returns the bigger number.
```Kotlin
fun whichIsBigger(num1 : Int, num2 : Int) : Int{	
	if (num1 > num2){
		return num1 
	}else if (num1 < num2){
		return num2 
	}else {
		println("$num1 is equal to $num2")
		return -1
	}
}
```
>[!note]- A Cleaner way of doing it
>```Kotlin
>fun whichIsBigger(num1 : Int, num2 : Int) : Int{	
>	return if (num1 > num2){
>		num1 
>	}else if (num1 < num2){
>		num2 
>	}else {
>		println("$num1 is equal to $num2")
>		 -1
>	}
>}
>```
>When using this style, Kotlin returns the last value in whichever block runs. So whatever value we place after the `println()` becomes the return value. In this case, the else block returns -1 
>
- The `: Int` outside of the parentheses tell Kotlin that the function will return an `Int`
- `return` sends back a value to wherever it was called.

This allows us to do something like this: 
```Kotlin
val largerNum = whichIsBigger(3,4)
println(largerNum)
```
Since `whichIsBigger()` returns an `Int`, we can store the returned value inside a variable.

### Scope
Why doesn't this work
```Kotlin 
fun main(){
	if (true){
		val name = "John"
	}
println(name)
}
```
However, this works: 
```Kotlin
val name = "John"
if (true){
	println(name)
}
```
This happens because variables only exist inside the code block where they are created.

In the case of the first example, `name` is created inside the `if` block. This means `name` only exists between the `{}` of that `if` statement. Once the `if` is finishes running, name no longer exists. As a result, Kotlin creates an error when `println(name)` is called because name is outside its scope

In the second example, `name` is created just inside of `main`. Since, the `if` is also in `main`, it can access `name` . 

>[!info]- When to make a function
>If your code:
>- has repeating code
>- has parts with clear jobs
>- is getting to long 

>[!note]- Java Equivalent 
>**Methods**
>Java does not have standalone functions. Instead, all functions belong to classes and are called methods. 
>```Java
>public static void test(){}
>```
>
>The first three things - `public`, `static`, and `void` - describe how the method behaves:
>- `public` tells java the method can be accessed anywhere 
>- I'll get to `static` later, but for now just know that methods inside `class Main {}` are usually marked `static` so they can be called directly from `main`.
>- `void` tells Java that this method will return nothing
>
>So if you want a method to return a specific type, just replace void with the returned type. Like this:
>```Java
>public static int add(int num1, int num2){
>	return num1 + num2;
>}
>```
>Additionally, Java allows multiple methods with the same name as long as their parameters are different. This is called method overloading. Take this, for example : 
>```Java
>public static double add(double num1, double num2){
>	return num1 + num2;
>}
>public static double add(int num1, double num2){
>	return num1 + num2;
>}
>public static int add(int num1, int num2){
>	return num1+num2;
>}
>```
>
>However, this wouldn't work: 
>```Java
>public static double add(double num1, double num2){
>	return num1 + num2;
>}
>public static int add(double num1, double num2){
>	return (int) (num1 + num2);
>}
>```
>This is because Java determines which overloaded method to call based on the number and types of the parameters. However, both functions above have the exact same parameters, so Java can't tell them apart. 
>


## Activity 5
Take a look back at your greeter code, doesn't it seem a bit messy? How about we clean it up by adding in functions.
- Replace repeating code with functions 
- At least one function should return a value
- Use the returned value somewhere in the code  

>[!note]- Example code
>>[!note]- Kotlin
>>```Kotlin 
>>fun main(){
>>    var name = "no name"  
>>    var partySize = -1  
>> 
>>   println("Do you want to make a reservation before heading to the restaurant? ")  
>>    var response = readLine()?.lowercase()  
>>  
>>    if(response == "yes"){  
>>        name = getReservationName()  
>>        partySize = getReservationPartySize()  
>>  
>>        println("Okay your reservation is made ")  
>>    }else if(response == "sure"){  
>>       name = getReservationName()  
>>        partySize = getReservationPartySize()  
 >> 
>>      println("Okay your reservation is made ")  
>>    }else if(response == "ya"){  
>>        name = getReservationName()  
>>        partySize = getReservationPartySize()  
>>  
>>        println("Okay your reservation is made ")  
>>    }  
>>      
>>      println("You head to the restaurant ")  
>>      println("Hello, do you have a reservation?")  
>>      response = readLine()?.lowercase()  
>>      if(response == "yes"){  
>>      println("Who made the reservation ")  
>>      val nameCheck =  readLine()?.lowercase()  
>>      
>>      if(nameCheck == name.lowercase()) {  
>>          println("Nice to meet you, $name. May I take your coat") 
>>              val takeOuterwear = readLine()  
>>              println("$takeOuterwear, okay $name follow me to your table for $partySize")  
>>      }else{  
>> 	     println("There are no reservations under this name")  
>> 	     println("Please wait for a table to be available")  
>> 	     }  
>> 	 }else{  
>> 		 println("Please wait for a table to be available")  
>> 	}  
>>}
>>fun getReservationName() : String{  
>>  println("Who is the reservation for?")  
>>   return readLine()!!
>>}  
>>
>>fun getReservationPartySize() : Int{  
>>  println("What is the party size")  
>>    val response = readLine()!!.toInt()  
>>  
>>if (response <= 4){  
>>            println("Okay, your reservation for one small table is done.")  
>>        }else if (response <= 8){  
>>           println("Okay, your reservation for one large table is done.")  
>>        }else if (response <= 16){  
>>            println("Okay, your reservation for two large tables is done.")  
>>       }else{  
>>            println("We can't currently seat your party of $response")  
>>        }  
>>  
>>   return response  
>>}   
>>
>>```
>
>>[!note]- Java
>>```Java
>>import java.util.Scanner;
>>
>>class Main{
>>	void main(){
>>		Scanner input = new Scanner(System.in);
>>		int partySize = -1;
>>		String name = "";
>>		
>>		IO.println("Do you want to make a reservation before heading to the restaurant? ");
>>		String response = input.nextLine().toLowerCase();
>>		if(response.equals("yes")){
>>			name = getReservationName(input);
>>			partySize = getPartySize(input);
>>			
>>			IO.println("Okay your reservation is made ");
>>		}else if(response.equals("sure")){
>>			name = getReservationName(input);
>>			partySize = getPartySize(input);
>>			
>>			IO.println("Okay your reservation is made ");
>>		}else if(response.equals("ya")){
>>			name = getReservationName(input);
>>			partySize = getPartySize(input);
>>			
>>			IO.println("Okay your reservation is made ");
>>		}
>>	
>>		IO.println("You head to the restaurant ");
>>	
>>		IO.println("Hello, do you have a reservation?");
>>		response =  input.nextLine().toLowerCase();
>>		if(response.equals("yes")){  
>>			IO.println("Who made the reservation ")  ;
>>			String nameCheck = input.nextLine().toLowerCase();
>>			
>>			if(nameCheck.equals(name.toLowerCase())) {  
>>				IO.println("Nice to meet you, " + name + ". May I take your coat");
>>				String takeOuterwear =  input.nextLine();  
>>				IO.println(takeOuterwear + ", okay " + name + ", follow me to your table for " + partySize);
>>			}else{  
>>				IO.println("There are no reservations under this name");
>>				IO.println("Please wait for a table to be available");
>>			}  
>>		}else{
>>			IO.println("Please wait for a table to be available");
>>		}
>>	}
>>
>>
>>	public static String getReservationName(Scanner input){
>>		IO.println("Who is the reservation for?");
>>		return input.nextLine();
>>	}
>>
>>	public static int getPartySize(Scanner input){
>>		IO.println("How many people will there be?");
>>		int partySize = Integer.parseInt(input.nextLine());
>>	
>>		if (partySize <= 4){
>>			IO.println("Okay, your reservation for one small tables is done.");
>>		}else if (partySize <= 8){
>>			IO.println("Okay, your reservation for one large table is done.");
>>		}else if (partySize <= 16){
>>			IO.println("Okay, your reservation for two large tables is done.");
>>		}else {
>>			IO.println("We can't currently seat your party of " + partySize);
>>		}
>>		return partySize;
>>	}
>>}
>>```


>[!info]- Nulls 
>Let's imagine you're working the host stand and someone wants to reserve a table for 3. But what if they just walk away when you ask for a name. Sure you could just ignore it, but lets say in this case your manager forces you to make the reservation without a name.
>
>Well you would need some way to represent that no name was provided, so you "write no name provided".  Even though that isn't a real name, it lets you know the reservation exists but the name is missing. 
>
>Kotlin sometimes encounters similar issues.  Sometimes the information meant to be stored isn't available.  Instead of using a string like "no name provided", we can use a special value called `null`.  However we can't do something like this:
>
>```Kotlin
>var name = null
>name = "John"
>```
>When Kotlin sees `var name = null`, it assumes name can only  hold `null`s. So, when you try to store "John" in `name`, you'd get an error. Instead, you have to do this 
>
>```Kotlin
>var name : String? = null
>name = "John"
>```
>This works because:
>-`: String` tells Kotlin that this `name` will hold a String 
>-`?` tells Kotlin `name` can store null
>
>**Nulls with functions**
>```Kotlin
>var name : String? = readLine()?.lowercase()
>```
>Sometimes `readLine()` can return null, and `null` cannot be converted to lowercase. Instead we use a `?.` which tells Kotlin
>- To run the `lowercase()` function if `readLine()` returns a string
>- If `readLine()` returns null, then skip `lowercase()` and just return null
>
>**The !! Operator**
>The `?.` operator is good if you want to handle `null`s without crashing your code. However, there are times when you know a certain variable should not be `null`. In those cases,  we can use `!!` to tell Kotlin that the value should never be `null`.
>```Kotlin 
>var name = readLine()!!.lowercase()
>``` 
>The `!!` tells Kotlin that `readLine()` should never be null. If it is, then the code will crash. 
>
>>[!note]- Java Equivalent
>>Unlike Kotlin, most variables, apart from the primitive types (like int, double, and boolean), can hold  a `null` in Java without any changes. Additionally, there are no null safety operators like  `!!` or `?`. Instead, you'll have to manually check them. 
>>```Java
>>public static void printUserInput(String userInput){
>>	if(userInput != null){
>>		IO.println(userInput);
>>	}
>>	
>>}
>>```
>
>
>>[!note]- Optional Activity
>>Now you know about nulls, I think it's time to update your greeter code a little bit. 
>>- Replace placeholder, such as `""`, with null 
>>- Update your code so they it can handle nulls
>>- Update your variables to support storing null


## Multiple Conditions
Take a look at your greeter code and how it might have several `if` statements that do the same thing:
```Kotlin
if(response == "yes"){ 
	// make reservation
}else if(response == "sure"){
	// make reservation
}else if(response == "ya"){ 
	// make reservation
}
```
Even though `ya`, `sure`, and `yes` all mean the same thing, we still had to write separate checks for each response.  By repeating the same code, it becomes longer and harder to read.

###  Or

Wouldn't it be nice to check if at least one of the conditions is true in a single `if` statement.  Something like: 
```Kotlin
val hasReservation = true
val tableOpen = true

if(hasReservation or tableOpen){
	println("please follow me")
}  
// This technically works, but we generally use || instead
```
Well by replacing the `or` with `||`, we'll be able to do that :

```Kotlin 
val hasReservation = true
val tableOpen = true

if (hasReservation || tableOpen){
	println("please follow me")
} 
```

Using the `||` we can finally compact down the code into this:  

```Kotlin
if (response == "yes" || response == "ya" || response == "sure"){
	//make reservation 
}
```

### And
>[!info]- Optional Challenge
>For this challenge, I want you to check whether several conditions are all true in one `if` statement.
>>[!info]- hint1 
>> What would happen if you tried this code:
>> ```Kotlin
>> val x = 9 // you can change this 
>> println( (x+1)*-1 )
>> ```
>
>>[!info]- hint2
>>What do you think would happen if you printed this: 
>>```Kotlin
>>val x = 9 //you can change this number
>>println( (x+1) < 8)
>>```
>>What kind of value does `(x + 1) < 8` produce?
>
>>[!note]- A Solution That Technically Works
>>This solution only uses concepts I've already covered, so it technically solves the challenge. However, it is difficult to read and is **not** how we normally combine conditions. I'll cover how to combine them properly below this.
>>
>>```Kotlin 
>>val nextClass = "English" 
>>val hoursSlept = 6
>>val boringLesson = true
>>
>>if( ( (nextClass == "English") == (hoursSlept == 6) ) == boringLesson ){
>>	println("time to sleep.")
>>} 
>>```
Sometimes when you go to a restaurant with a reservation, you might have to wait a minute for the table to be cleaned. How would you go about writing code to check for this. Maybe something like this:  
```Kotlin
val hasReservation = true 
val tableReady = false

if (hasReservation){
	if(tableReady){
		println("please follow me ")
	}
} 
```

Or this way, which technically works:
```Kotlin
if (! (!hasReservation || !tableReady) ) {
	println("please follow me")
	//If you're curious about this, look up deMorgan's law.
}
```

Well with the Kotlin and operator `&&`, it is pretty easy to simplify :  
```Kotlin
if (hasReservation && tableReady){}
```

>[!note]- Java Equivalent
>The `&&` and `||` operators work the same way in Java as they do in Kotlin.

## Loops 
 Until now, our program has assumed the user always replies with an answer. However, that doesn't always happen. Take this, for example:  
 ```Kotlin
 println("Do you want to make a reservation?")
 var response = readLine()
 
 if (response == "ya" || response == "yes"){
	 //create reservation 
 }
 ```

What would happen if the user typed something random?
```
Do you want to make a reservation?
apple
```

Well, the program would assume the user doesn't want to make a reservation. It never gives the user another chance to provide a valid answer. Instead, wouldn't it be nice if we could repeat the same code until they give a valid answer? 

This is where loops come in. They allow us to repeat a section of code until a certain condition is met.  

In Kotlin there are two types of loops: 
- `while` loop that runs **while** a condition is true
- `for` loops repeat code once for each value in a sequence, such as a range of numbers or every item in a list.

### While 
A while loop looks something like this: 
```Kotlin
while(condition){
	//the code that will run.
}
```

In practice it looks something like this: 
```Kotlin
var quit = false
var response : String
//Tells Kotlin to create a variable, but we'll give it something to hold 
//later

while(!quit){ 
	// The ! means not
	//In English, this reads as "while quit is not true".

	println("do you want to quit?")
	response = readLine()!!.lowercase()
	
	if (response == "yes"){
		quit = true 
		// you could also use break to escape from the while loop
	}
}
```

### For Loop
A while loop is useful when we don't know how many times we want to repeat something. But there are times when we only want to run the same code a certain number of times, or for each item in a sequence. 

For example, imagine you wanted to calculate the average test score for a class of 31 students.  Since there are 31 students, we would need to ask for 31 test scores. Sure we could write the same code 31 times, but that's repetitive and bad practice. Instead, we can use a `for` loop: 

```Kotlin
var sum = 0

for (i in 1..31){
	println("what did student $i get on the test?")
	sum += readLine()!!.toInt()
	// the plus equal means take sum's current and add
	// readLine()!!.toInt()
} 
val average = sum/31.0
println("the average score was $average")
```
Every time a loop repeats, it completes one **iteration**. In this loop, Kotlin stores the current number (from 1 to 31) in `i`. Then it runs the code inside the loop. This repeats once for every number in the range.

>[!note]- Java Equivalent
>Java's `for` loop uses a different syntax than Kotlin. 
>It looks something like this 
>```Java
>for(int i = 0; i < 3; i++){
>	//code to repeat
>}
>```
>Unlike Kotlin, Java splits its for loop into three parts: 
>- `int i = 0` creates the starting point for the loop. As the loop runs, the value `i` is updated.
>- `i < 3` is the condition that must stay `true` for the loop to continue
>- `i++` increases the value of `i` by one after iteration 

## Activity 6
I think it is time to make sure we get a valid answer from the user. So, go back to your greeter code and update it to insure the user provides a valid response to the question "Do you want to make a reservation?". 
- Accept the same valid responses you used earlier (such as `yes`, `ya`, `sure`, and `no`).
- If the user answers anything other than a valid response, ask the question again.
 
>[!note]- Example code
>>[!note]- Kotlin
>>```Kotlin
>>var validResponse = false
>>var response : String
>>while(!validResponse){
>>	println("Do you want to make a reservation?")
>>	response = readLine()!!.lowercase()
>>
>>	if (response == "ya" || response == "yes" || response == "sure"){
>>		makeReservation()
>>		validResponse = true
>>	}else if (response == "no"){
>>		validResponse = true
>>	}
>>}
>>```
>
>>[!note]- Java
>>```Java
>>Scanner input = new Scanner(System.in);
>>String response; 
>>boolean validResponse = false;
>>
>>while(!validResponse){
>>	IO.println("Do you want to make a reservation?");
>>	response = input.nextLine().toLowerCase();
>>	
>>	if (response.equals("ya") || response.equals("yes") || response.equals("sure")){
>>		makeReservation();
>>		validResponse = true;
>>		
>>	}else if(response.equals("no")){
>>		validResponse = true;
>>	}
>>}
>>```

## Activity 7 
 Although the greeter activities have helped us learn the basics, I think it's time we move on to a new program. Next, we'll focus on making a character creator. 

For this activity you must:
- Ask the user if they want to create a character
- Allow the user to select from several heads, torsos, and legs
- Feel free to design your own or use the ones I provided
- Ask the user for the name of the character 
- Print out the complete character
- If the user enters an invalid option, ask them again.

To save on space, I've omitted pasting in the parts in this example 
```
Do you want to make a character?
yes

What should it have for the head?
1)Head 1 
2)Head 2 
3)Head 3

1  <- User input

What should it have for the torso?
1)Torso 1 
2)Torso 2 
3)Torso 3

3 <- User input

What should it have for legs?
1) Legs 1 
2) Legs 2
3) Legs 3
   
2 <- User input

What is your character's name?

John <- User input

Here is the character you made: 

John
+---+  
|o o|  
|_-_|  
+---+  
[###]  
 |#|  
 |#|  
 / \  
/___\


```


I've provided some parts below, however you can find more here
>[!info]- How to print the different parts
>>[!info]- Kotlin
>>```Kotlin 
>>println("""
>>This message
>>Will be printed on 
>>Several lines
>>""").trimIndent()
>>```
>
>>[!info]- Java
>>```Java
>>IO.println("""
>>This message 
>>Will be printed on
>>Several lines
>>""");
>>```

>[!info]- Parts
>>[!info]- Heads
>>```
>>  .-.
>>(•‿•)
>>  `-'
>>```
>>
>>```
>>+---+  
>>|o o|  
>>|_-_|  
>>+---+
>>```
>>
>>```
>>  .-.  
>>|x x|  
>>| ^ |  
>>  `-'
>>```
>
>>[!info]- Torso
>>```
>>  /|\
>>|===|
>>|___|
>>```
>>
>>```
>>[###]
 >>  |#|
>>  |#|
>>```
>>
>>```
>>  /V\  
>><###>  
>>  \#/
>>```
>
>>[!info]- Legs
>>```
>>  / \ 
>>/___\
>>```
>>
>>```
>>(O O)
>>```
>>
>>```
>>"~~~~~"
>>```


>[!info]- Example Code
>>[!info]- Kotlin
>>```Kotlin
>>   fun main(){
>>    var head = ""
>>    var torso = ""
>>    var legs = ""
>>    var name = ""
>>    var response : Int
>>
>>    if (validateYesOrNo("Do you want to make a character")){
>>        println("Here are the heads you can choose from")
>>        printHeads()
>>        response = validateNumber("Which head do you want?",1, 3)
>>
>>        if(response == 1){
>>            head = """
>>                 .-.
>>                (•‿•)
>>                 `-'
>>            """.trimIndent()
>>        }else if(response == 2){
>>            torso = """
>>                +---+  
>>                |o o|  
>>                |_-_|  
>>                +---+
>>            """.trimIndent()
>>        }else {
>>            head = """
>>                 .-.  
>>                |x x|  
>>                | ^ |  
>>                 `-'
>>            """.trimIndent()
>>        }
>>
>>        println("Here are the torsos you can choose from")
>>        printTorsos()
>>        response = validateNumber("which torso do you want?",1, 3)
>>
>>        if (response == 1){
>>            torso = """
>>                 /|\
>>                |===|
>>                |___|
>>            """.trimIndent()
>>        }else if(response == 2){
>>            torso = """
>>                [###]
>>                 |#|
>>                 |#|
>>            """.trimIndent()
>>        }else {
>>            torso = """
>>                 /V\  
>>                <###>  
>>                 \#/
>>            """.trimIndent()
>>        }
>>
>>        println("Here are the legs you can choose from")
>>        printLegs()
>>        response = validateNumber("Which legs do you want?",1, 3)
>>
>>        if(response == 1){
>>            legs = """
>>                 / \ 
>>                /___\
>>            """.trimIndent()
>>        }else if(response == 2){
>>            legs = """
>>                (O O)
>>            """.trimIndent()
>>        }else{
>>            legs = """
>>                '~~~~~
>>            """.trimIndent()
>>        }
>>
>>        println("What is your characters name?")
>>        name = readLine()!!
>>
>>        println("Here is your character $name")
>>        println(head)
>>        println(torso)
>>        println(legs)
>>
>>    }
>>
>>}
>>// These helper functions keep main() shorter and easier to read.
>>fun validateYesOrNo(question : String) : Boolean{
>>    var response : String
>>
>>    while(true){
>>        println(question)
>>        response = readLine()!!.lowercase()
>>
>>        if (response == "sure" || response == "yes" || response == "ya") {
>>            return true
>>        }else if (response == "na" 
>> 	       || response == "no" 
>> 	       ||  response == "nope"
>> 	   ){
>>            return false
>>        }
>>        println("please respond with yes or no")
>>
>>    }
>>}
>>
>>fun validateNumber(question : String, min : Int, max : Int) : Int{
>>    while(true){
>>        println(question)
>>        try{
>>            val answer = readLine()!!.toInt();
>>            if (answer <= max && answer >= min ){
>>                return answer
>>            }
>>
>>            println("Please enter a number between $min and $max.")
>>
>>        }catch (e: NumberFormatException){
>>           println("Please enter a valid number")
>>        }
>>    }
>>}
>>
>>fun printHeads(){
>>    println("""
>>        Head 1
>>            .-.
>>           (•‿•)
>>            `-'
>>       """.trimIndent()
>>    )
>>    println("""
>>        Head 2
>>            +---+  
>>            |o o|  
>>            |_-_|  
>>            +---+
>>       """.trimIndent()
>>    )
>>    println("""
>>        Head 3
>>             .-.  
>>            |x x|  
>>            | ^ |  
>>             `-'
>>       """.trimIndent()
>>    )
>>}
>>
>>fun printTorsos(){
>>    println("""
>>         /|\
>>        |===|
>>        |___|
>>    """.trimIndent()
>>    )
>>
>>    println("""
>>        [###]
>>         |#|
>>         |#|
>>    """.trimIndent()
>>    )
>>
>>    println("""
>>         /V\  
>>        <###>  
>>         \#/
>>    """.trimIndent()
>>    )
>>}
>>
>>fun printLegs(){
>>    println("""
>>         / \ 
>>        /___\
>>    """.trimIndent())
>>
>>    println("""
>>        (O O)
>>    """.trimIndent())
>>
>>    println("""
>>      "~~~~~"
>>    """.trimIndent())
>>}
>>```
>
>>[!info]- Java
>>```Java
>>import java.util.Scanner;
>>
>>class Main {
>>    void main() {
>>        Scanner input = new Scanner(System.in);
>>        String head;
>>        String torso;
>>        String legs;
>>        String name;
>>        int response;
>>
>>        if (validateYesOrNo("Do you want to make a character")){
>>            IO.println("Here are the heads you can choose from");
>>            printHeads();
>>            response = validateNumber("Which head do you want?",1, 3);
>>
>>            if (response == 1) {
>>                head = """
>>                         .-.
>>                        (•‿•)
>>                         `-'
>>                        """;
>>            }else if (response == 2) {
>>                head = """
>>                        +---+
>>                        |o o|
>>                        |_-_|
>>                        +---+
>>                        """;
>>            }else{
>>                head = """
>>                         .-.
>>                        |x x|
>>                        | ^ |
>>                         `-'
>>                        """;
>>            }
>>
>>            IO.println("Here are the torsos you can choose from");
>>            printTorsos();
>>            response = validateNumber("Which torso do you want?",1, 3);
>>
>>            if (response == 1) {
>>                torso = """
>>                         /|\\
>>                        |===|
>>                        |___|
>>                        """;
>>            }else if (response == 2) {
>>                torso = """
>>                        [###]
>>                         |#|
>>                         |#|
>>                        """;
>>            }else {
>>                torso = """
>>                        /V\\
>>                       <###>
>>                        \\#/
>>                       """;
>>            }
>>
>>            IO.println("Here are the legs you can choose from");
>>            printLegs();
>>            response = validateNumber("Which legs do you want?",1, 3);
>>
>>            if (response == 1) {
>>                legs = """
>>                         / \\
>>                        /___\\
>>                        """;
>>            }else if  (response == 2) {
>>                legs = """
>>                    (O O)
>>                """;
>>            }else {
>>                legs = "~~~~~";
>>            }
>>
>>            IO.println("What do you want to name your character?");
>>            name = input.nextLine();
>>
>>            IO.println("Here is your character " + name);
>>            System.out.print(head);
>>            System.out.print(torso);
>>            System.out.print(legs);
>>        }
>>    }
>>
>>
>>    public static boolean validateYesOrNo(String question) {
>>        Scanner input = new Scanner(System.in);
>>
>>        while (true) {
>>            IO.println(question);
>>            String response = input.nextLine().toLowerCase();
>>
>>            if (response.equals("yes")
>>                    || response.equals("y")
>>                    || response.equals("sure")
>>            ) {
>>                return true;
>>            } else if (response.equals("na")
>>                    || response.equals("nope")
>>                    || response.equals("no")) {
>>                return false;
>>            }
>>        }
>>
>>    }
>>
>>    public static int validateNumber(String question, int min, int max) {
>>        Scanner input = new Scanner(System.in);
>>
>>        while (true) {
>>            IO.println(question);
>>            try {
>>                int answer = Integer.parseInt(input.nextLine());
>>                if (answer >= min && answer <= max) {
>>                    return answer;
>>                }
>>                IO.println("Please enter a number between " + min + " and " + max);
>>
>>            } catch (NumberFormatException e) {
>>                IO.println("please enter a valid number");
>>            }
>>
>>        }
>>
>>    }
>>    public static void printHeads(){
>>        IO.println("""
>>                 .-.
>>                (•‿•)
>>                 `-'
>>                """
>>        );
>>        IO.println("""
>>                +---+ \s
>>                |o o| \s
>>                |_-_| \s
>>                +---+
>>                """
>>        );
>>
>>        IO.println("""
>>                 .-. \s
>>                |x x| \s
>>                | ^ | \s
>>                 `-'
>>                """
>>        );
>>
>>    }
>>
>>    public static void printTorsos(){
>>        IO.println("""
>>                 /|\\
>>                |===|
>>                |___|
>>                """
>>
>>        );
>>        IO.println("""
>>                [###]
>>                 |#|
>>                 |#|
>>                """);
>>        IO.println("""
>>                 /V\\ \s
>>                <###> \s
>>                \\#/
>>                """);
>>    }
>>
>>    public static void printLegs(){
>>        IO.println("""
>>                 / \\\s
>>                /___\\
>>                
>>                """);
>>
>>        IO.println("""
>>                (O O)
>>                
>>                """);
>>
>>        IO.println("""
>>                "~~~~~"
>>                """
>>
>>        );
>>    }
>>
>>}
>>```

## Classes and Objects 
Take a look at the program you just wrote. Now imagine that you wanted to create two or three more characters. This would require double or even triple the variables you started with: 

```Kotlin
var head1 : String
var head2 : String 
var head3 : String

var torso1 : String
var torso2 : String
var torso3 : String

var legs1 : String
var legs2 : String
var legs3 : String

var name1 : String
var name2 : String
var name3 : String
```

And printing each character would also require repeating the code:
```Kotlin
println("Here is your character $name1")
println(head1)
println(torso1)
println(legs1)

println("Here is your character $name2")
println(head2)
println(torso2)
println(legs2)

println("Here is your character $name3")
println(head3)
println(torso3)
println(legs3)
```

 Notice how every character has the same four pieces of information. The only thing that changes is what is being stored. Instead of having standalone variables, wouldn't it be nice to group them into one thing? 
 
 That is exactly what a class allows us to do. A class is like a blueprint that defines what information something can store and what functions it has. We can use that blueprint to create objects, which hold their own values and can use the functions defined by the blueprint. 

### Classes
In Java, it is usually best to give each class its own file.  So instead of adding a `Character` class to main, you should put it in its own file. 

In Kotlin, it's not required to give each class its own, since many people put small related classes into one file as long as it doesn't make it harder to read. However, I would recommend putting `Character` in its own file to keep things organized. 

Creating a class is a really simple thing. 
```Kotlin 
class Character{}
```
All you need to do is write `class` and then the name of the class. 

If you want to store information in the class, like `name`, all you do is create the variable inside the class. 
```Kotlin
class Character{
	var name : String = "John" 
} 
```
Now whenever you use `Character` to make a new object, that object will get its own field (a variable declared in a class, but belonging to an individual object) named `name`. 

Now our class can store a character's name. But what if we wanted to print that name?

Sure, we could print it outside of the class. However, since the `Character` class already stores the character's information, doesn't it make sense to keep the function that uses that information inside `Character`? A function inside a class is called a method.

```Kotlin
class Character{
	var name : String = "John" 
	
	fun printName(){
		println(name)
	}
} 
```
Since `printName()` was declared in the class, all instances of `Character` (what we call objects made from a class) can use it. So, whenever an object runs `printName()`, it uses that object's own fields.

Now we have a class that describes how a character stores and prints its name. But how do we actually create a character from it?

Well, like this:
```Kotlin
fun main(){
	// We create an object by writing the class name followed by `()`.
	val character1 = Character()
	var character2 = Character()
	
	character1.name = "Joe"
	
	character1.printName() // -> prints Joe
	println(character2.name) // -> prints John
}
```
Every time we call `Character()`, a new object is made.

Notice that changing `character1` did not affect `character2`. Even though both objects were created from the same class, each object stores its own values.

However, there is still one problem. Every new `Character` starts with the same values.  This means every new character is named `John`, and we have to manually change its name after creating the object. Right now it's not too bad with one field, but imagine if we had several `Character`s with more fields like head, torso, and legs. We would have to manually assign every one of those values every time we created a new character.

 Instead, we can use something called a constructor. A constructor is code that automatically runs whenever a new object is created, allowing us to initialize the object's fields. Initialize simply means giving something its starting values. 

### Primary Constructor 
The most common way to give an object its starting values is with a primary constructor: 
```Kotlin
class Character(var name : String){  
	fun printName(){  
		println(name)  
	}  
}
```
The values inside the `()` look similar to function parameters. However, by adding `var` or `val`, Kotlin automatically creates fields and stores the values passed into them.

Now, instead of creating a character and changing its fields afterward, we can provide those values immediately.

```Kotlin
fun main(){  
	val character1 = Character("Joe")  
	val character2 = Character("John")  
	
	character1.printName() // -> prints Joe  
	character2.printName() // -> prints John  
}
```


### `init` Blocks
Sure, giving the fields starting values is useful, but there are some times we want to run additional code whenever a new object is created.

For example, what if the programmer provides a negative number for `Character`'s age.  Our code would expect it, but a `Character` cannot be -1 years old. 
This is where `init` comes in:
```Kotlin
 class Character(var name : String, characterAge : Int){  
	var age : Int = -1
	//Kotlin requires fields to be initialized
	
	init{
		if ( characterAge < 0 ){
			age = 21
		}  else {
			age = characterAge
		}
		
	}
	
	fun printName(){  
		println(name)  
	}  
}
```
Since `characterAge` doesn't have a `val` or `var` attached, it is treated as a parameter. As a result, we have to create our own field called `age`. 

>[!info]- Some things not to include in an `init` 
>- Asking for user input
>- printing, unless for debugging
>- Heavy logic 
>- Creating lots of unrelated objects.

### Passing Objects as a Parameter
Remember how you have to specify the type of data being passed? Well, objects are no different. Instead, we use the class name as the data type. Like this: 
```Kotlin
fun main(){
	var character = Character("Joe", 20)
	example(character)
	
	character.printName()// -> prints John
}

fun example(character : Character){
	character.name = "John"
} 
```
Notice that after calling `example()`, the character's name changed from `"Joe"` to `"John"`. 

Although these seem to contradict the idea that all parameters are `vals`, it doesn't. The parameter is still read-only, so we can't give the parameter something new to hold. Instead, we're changing the values stored inside that object's fields. Since `main()` and `example()` are both referring to the same `Character` object, they both see the updated values.

>[!info]- Why I used `CharacterAge` instead of `Age`
>Remember how the example above I had this 
>```Kotlin
>class Character(var name : String, characterAge : Int){  
>	var age : Int = -1
>	
>	init{
>		if ( characterAge < 0 ){
>			age = 21
>		}  else {
>			age = characterAge
>		}
>		
>	}
>	
>```
>The reason I used `characterAge` instead of `age` is because both the constructor parameter >and field share the same name. As a result, Kotlin can't tell which one you mean. However, this can be fixed with the `this` keyword.
>```Kotlin
>class Character(var name : String, age : Int){  
>	var age : Int = -1
>	
>	init{
>		if ( age < 0 ){
>			this.age = 21
>		}  else {
>			this.age = age
>		}
>		
>	}
>	
>```
>Notice the `age` in `age < 0` now refers to the constructor parameter, while `this.age `refers to the field. This is because the `this` keyword refers to the object that's currently running the code.

>[!info]- Java Equivalent 
>>[!info]- Creating a class and object
>>Creating a class is almost identical to Kotlin:
>>```Java
>>class Character{}
>>```
>>One difference is how field variables are declared.
>>```Java
>>class Character{
>>	public String name = "John"; 
>>}
>>``` 
>>`public` allows a field or method to be accessed anywhere within your code. This is called an access modifier. I won't cover much about them, but if you're interested, you can read more here: [look here](https://www.geeksforgeeks.org/java/access-modifiers-java/).
>>
>>Similarly, creating an object is a little different:
>>```java
>>Character character = new Character();
>>```
>>Java requires the `new` keyword whenever you create an object. It tells Java to create a new `Character` object.
>
>>[!info]- Constructors 
>>Unlike Kotlin, Java does not have a primary constructor. Instead, constructors are written inside the class and look really close to a function
>>```Java 
>>class Character{
>>	public String name;
>>	
>>	public Character(String characterName){
>>		name = characterName;
>>	}		
>>}
>>```
>>Now whenever you try to create a new `Character`, you must pass a `String`.
>>```Java 
>>Character character = new Character("John");
>>```
>>
>>One more thing, you can overload constructors just like functions:
>>```Java
>>class Character{
>>	public String name;
>>	
>>	public Character(){
>>		name = "John";
>>	}
>>	public Character(String characterName){
>>		name = characterName;
>>	}
>>}
>>```
>>Now we can do this 
>>```Java
>>Character character1 = new Character();
>>Character character2 = new Character("Joe");
>>```
>
>>[!info]- Static
>>The `static` keyword can be placed before fields and methods 
>>
>>```Java
>>class School{
>>	public static int districtSize;
>>	public String name; 
>>	
>>	
>>	public School(String name){
>>		districtSize += 1;
>>		this.name = name;
>>	}
>>}
>>``` 
>>The static keyword makes a field value belong to the class. So all objects can access it, and any changes would change the field for all objects. So in this case, if I were to make a new school, then `districtSize` would increase by one for all School objects.
>>
>>A static method is similar
>>```Java
>>class School{
>>	public static int districtSize;
>>	public String name;
>>	
>>	public School(String name){
>>		districtSize += 1;
>>		this.name = name;
>>	}
>>	
>>	public static void printDistrictSize(){
>>		IO.println(School.districtSize);
>>	}
>>}
>>``` 
>>Making the method static results in a method belonging to the class, not an object.  Since the method is not running for a specific object, there is no  object for `this` to refer to.  So the following code will cause an error:
>>```Java
>>	public static void printDistrictSize(){
>>		IO.println(School.districtSize);
>>		IO.println(this.name); // This would cause an error 
>>	}
>>```

## Activity 8
Now you know what classes are, I think it's time to update your character creator to include classes.

For this activity, I want you to: 
- Create a `Character` class 
- Allow the user to create and store up to 3 `Character` objects
- Create a separate file for `Character`

```
Do you want to make a character?
yes <- User input

... Character Creation Dialogue (Look at activity 7) ... 


Do you want to make another? 
yes <- User input 

... Character Creation Dialogue (Look at activity 7) ... 


Do you want to make another? 
yes <- User input

... Character Creation Dialogue (Look at activity 7) ... 

Here are the characters you created:

... print out the Characters ...

```

>[!info]- Example code 
>Since most of the code is the same as Activity 7, I've replaced those sections with `// Code from Activity 7` to keep it short.
>>[!info]- Kotlin
>>```Kotlin 
>>// Character.kt
>>class Character(
>>	val name : String,
>>	val head: String, 
>>	val torso : String,
>>	val legs : String,
>>){
>>	fun printCharacter(){
>>		println("Here is your character $name")  
>>		println(head)  
>>		println(torso)  
>>		println(legs)
>>	}
>>
>>}
>>
>>// Even though it is a small class, adding it to Main would only make it longer // and distract from what main() is trying to do. 
>>```
>>```Kotlin
>>// Main.kt 
>>fun main(){
>>	var character1 : Character? = null
>>	var character2 : Character? = null
>>	var character3 : Character? = null
>>	
>>	var finishedCreatingCharacters = false
>>	
>>	if (validateYesOrNo("Do you want to make a character")){
>>		character1 = createNewCharacter()
>>	}else{
>>		finishedCreatingCharacters = true
>>	}
>>	
>>	if (validateYesOrNo("Do you want to make another character") && !finishedCreatingCharacters){
>>		character2 = createNewCharacter()
>>	}else{
>>		finishedCreatingCharacters = true
>>	}
>>	
>>	if (validateYesOrNo("Do you want to make another character") && !finishedCreatingCharacters){
>>		character3 = createNewCharacter()
>>	}
>>	
>>	println("Here are your character(s)")
>>	if (character1 != null){
>>		character1.printCharacter()
>>	}
>>	if (character2 != null){
>>		character2.printCharacter()
>>	}
>>	if (character3 != null){
>>		character3.printCharacter()
>>	}
>>}
>>
>>fun validateNumber(question : String, min : Int, max : Int) : Int{
>>	// Code from Activity 7
>>}
>>
>>fun validateYesOrNo(question : String) : Boolean{
>>	//Code from Activity 7
>>}
>>
>>fun createNewCharacter() : Character{
>>	// Code from Activity 7 
>>	return character
>>}
>>
>>```
>
>>[!info]- Java
>>```Java
>>// Character.java
>>class Character{
>>	String name;
>>	String head;
>>	String torso;
>>	String legs;
>>	
>>	public Character(
>>		String name,
>>		String head,
>>		String torso,
>>		String legs
>>	){
>>		this.name = name;
>>		this.head = head;
>>		this.torso = torso;
>>		this.legs = legs;
>>	}
>>	
>>	public void printCharacter(){
>>		IO.println("Here is your character named " + this.name);
>>		IO.println(this.head);
>>		IO.println(this.torso);
>>		IO.println(this.legs);
>>	}
>>}
>>```
>>```Java
>>// Main.java
>>import java.util.Scanner;
>>
>>class Main{
>>	static Scanner input = new Scanner(System.in); 
>>	
>>	void main(){
>>		Character character1 = null;
>>		Character character2 = null;
>>		Character character3 = null;
>>		
>>		boolean finishedCreatingCharacters = false;
>>		
>>		if (validateYesOrNo("Do you want to make a character")){
>>			character1 = createNewCharacter();
>>		}else{
>>			finishedCreatingCharacters = true;
>>		}
>>		
>>		if (validateYesOrNo("Do you want to make another character") && !finishedCreatingCharacters){
>>			character2 = createNewCharacter();
>>		}else{
>>			finishedCreatingCharacters = true;
>>		}
>>		
>>		if (validateYesOrNo("Do you want to make another character") && !finishedCreatingCharacters){
>>			character3 = createNewCharacter();
>>		}
>>		
>>		IO.println("Here are your characters:");
>>		if (character1 != null){
>>			character1.printCharacter();
>>		}
>>		if (character2 != null){
>>			character2.printCharacter();
>>		}
>>		if (character3 != null){
>>			character3.printCharacter();
>>		}
>>	}
>>	
>>	public static int validateNumber(String question, int min, int max){
>>		// Code from Activity 7
>>		return answer;
>>	}
>>	
>>	public static boolean validateYesOrNo(String question){
>>		// Code from Activity 7
>>		return answer;
>>	}
>>	
>>	public static Character createNewCharacter(){
>>		//Code from Activity 7
>>		return character;
>>	}
>>}
>>```

## List and arrays
 Even though we added classes, we still have to make a new variable for each extra character.  So how could we add more characters without needing too many extra variables?
 
```Kotlin
var character1 : Character? = null
var character2 : Character? = null
var character3 : Character? = null
var character4 : Character? = null
var character5 : Character? = null
var character6 : Character? = null
var character7 : Character? = null

```
 Well, that is where lists and arrays come in as they allow us to store multiple values (called elements) of the same type in a single object.

### Creating Lists
Lists store multiple values of the same type in one place. Unlike using separate variables, each element in the list is identified by its index, which is its position in the list.

One thing to be careful of is that indexes start at `0`. This means the first element in the list has an index of  `0`, the second element has the index `1`, and the third has `2`.

In Kotlin there are two types of lists: read-only and mutable lists. A read-only list cannot be changed once it's made. On the other hand, a mutable list can have items added, removed, or changed.

Mutable means something that can be changed.

To make a list, you do this: 
```Kotlin
//indexes                    0        1        2
var readOnlyList = listOf("apple", "pear", "orange")
var mutableList = mutableListOf<String>("apple", "pear", "orange") 

```
- `listOf()` tells Kotlin to make a read-only list containing `"apple"`, `"pear"`, and `"orange"`
- `mutableListOf()` tells Kotlin to make a mutable list containing `"apple"` , `"pear"`, and `"orange"`
- `<String>` tells Kotlin that the mutable list will only hold strings. If you're interested in how this works, look up Kotlin or Java Generics.  

The reason `listOf()` doesn't have `<String>` is because Kotlin automatically determines the type of data it will hold based on its contents. 

### Getting Data From a List 
We know how to create a list, but that isn't very useful if we can't access the values stored in the list. However, by using `[]` and the item's index, we can access specific elements in the list like this:

```Kotlin
println(readOnlyList[0]) // apple  
println(readOnlyList[1]) // pear  
println(readOnlyList[2]) // orange
```
The number inside the `[]` is what tells Kotlin which element we want to access. 

What do you think would happen if we tried to access index `7` like this: 
```Kotlin 
println(readOnlyList[7])
```
Well, you would get a `Index out of bounds` error. This is because we're trying to get information from index 7 from a list whose highest valid index is `2`. This means we're trying to get a value stored in an index that doesn't exist.

### Reassigning an item
We already know how to change the value stored in a variable by assigning it a new value. Changing an element in a list works almost the same way. Instead of writing the variable's name, we specify the item's index.

```Kotlin 
mutableList[0] = "peach"
```
Now our `mutableList` holds "peach", "pear", and "orange".

### Adding an Element 
Changing an element in the list is useful, but what about adding something to the list? Well `MutableList` allows us to add new items with `add()`

So we can either add a value to the end of the list like this: 
```Kotlin
mutableList.add("peach")

// apple, pear, orange, peach
```

Or adding it to a specific index by passing in a `Int` right before the value we want to add: 
```Kotlin
mutableList.add(1, "peach")

//apple, peach, pear, orange 
```

### Removing an Element
Sometimes we no longer need an element in a list. `MutableLists` let us remove an element either by their value or by their index.

```Kotlin
mutableList.remove("pear")
// apple, orange 

mutableList.removeAt(1)
//apple 
```

### Iterating through a list 
Right now we can print elements from a list one at a time. That works fine for small lists, but what if we had a list with several different types of fruit? We would have to print every element manually:

```Kotlin
var fruits = mutableListOf("pear","apple","orange", "peach", "grape", "cherry")

println(fruits[0])
println(fruits[1])
println(fruits[2])
println(fruits[3])
println(fruits[4])
println(fruits[5])


```

However, this won't work well with longer lists. Every time we add another fruit, we need to add another `println`. Instead we can use a `for` loop:
```Kotlin 
var fruits = mutableListOf("pear","apple","orange", "peach", "grape", "cherry")

for (index in 0..fruits.size){  
    val fruit = fruits[index]  
    print(" $fruit")  
}
//prints pear apple orange peach grape cherry, then errors
```
`fruits.size` tells us how many elements are in the list. However, indexes start at 0, not 1, but `fruits.size` counts the number of elements in the list. This means `fruits.size` will always be one greater than it's highest index. As a result, it will always check an invalid index. But this is quite easily fixable: 

```Kotlin
var fruits = mutableListOf("pear","apple","orange", "peach", "grape", "cherry")

for (index in 0..fruits.size - 1){  
    val fruit = fruits[index]  
    print(" $fruit")  
}
	//prints pear apple orange peach grape cherry and won't error

```
Now it won't error.

This is one way we can iterate through a list. By replacing `0..fruits.size - 1` with the list itself, we can iterate through each element without requiring their index: 

```Kotlin
var fruits = mutableListOf("pear","apple","orange", "peach", "grape", "cherry")

for (fruit in fruits){
	print(fruit)
}
```

This starts off with the first element in fruits and saves it to fruit, then the code inside `{}` runs. From there it goes onto the second element in the list - apple -, saves it to fruit, and runs the code. Then the pattern repeats until it has gone through every element in the list.  

>[!info]- Using `indices`
>It gets pretty annoying to add a `-1` every time, so you can do something like this instead:
>
>```Kotlin 
>var fruits = mutableListOf("pear","apple","orange", "peach", "grape", "cherry")
>
>for (index in fruits.indices){  
>   val fruit = fruits[index]  
>    print(" $fruit")  
>}
>``` 
>`fruits.indices` a range containing all of the valid indexes. In other words, it's equivalent to:
>```Kotlin
>fruits.indices == (0..fruits.size - 1)
>```

### How to Check if Something is in an Array or List
Let's imagine `fruits` is a list of available fruits at the store and the user can buy something from  the list.  How would you go about checking to see if the fruit they're buying is actually in the list? Well, you could do this:
```Kotlin
var fruits = mutableListOf("pear","apple","orange", "peach", "grape", "cherry")
var found = false

println("which fruit do you want to buy?")
for (fruit in fruits){
	print(", $fruit")
}

var response = readLine()!!.lowercase()

for (fruit in fruits){
	if (fruit == response){
		println("You bought a $response")
		found = true
	}
}
if (!found){
	println("we do not have a $response")
}

```

We just wrote a loop whose only job was to check whether a value existed. Since this is such a common task, Kotlin already provides a function that does it for us. It's `.contains()` which checks whether the list contains the value passed as a parameter.

```Kotlin
var fruits = mutableListOf("pear","apple","orange", "peach", "grape", "cherry")

println("which fruit do you want to buy?")
for (fruit in fruits){
	print(", $fruit")
}

var response = readLine()!!.lowercase()

if ( fruits.contains(response) ){ // fruits.contains(response) returns a boolean
	println("You bought a $response")
}else {
	println("We do not have a $response")
	
}
```

### Arrays 
Now that we've learned about lists, arrays should feel familiar. After all, arrays are very similar to mutable lists. The biggest difference is that an array has a fixed size. Once an array is created, you can't add or remove elements from it. They're often used when you know exactly how many elements you need to hold ahead of time.

```Kotlin
var fruits = arrayOf("pear","apple","orange", "peach", "grape", "cherry")
```

Imagine trying to create an array with 100 values. Writing dozens of values inside `arrayOf()` quickly becomes impractical. Fortunately, Kotlin lets us create an array with a fixed size instead.

```Kotlin
var fruits : Array<String?> = arrayOfNulls(100)
```
- `arrayOfNulls(100)` creates an array with 100 nulls
- `Array<String?>` tells Kotlin that this will either hold strings or nulls. It is required when creating either an empty array or an array of nulls since without other values, Kotlin can't tell what type of data it will hold.

Aside from how arrays are created and the fact that their size cannot change, you'll access and modify elements exactly the same way you would with a list.

```Kotlin
var fruits = arrayOf("pear","apple","orange", "peach", "grape", "cherry")

println(fruits[0]) //prints pear
println(fruits.size)//prints 6 

fruits[0] = "banana"

if ( fruits.contains("banana") ){
	println("There is a banana")
}

for (fruit in fruits){
	println(" $fruit")
} 
//prints banana apple orange peach grape cherry 
```



>[!info]- How to create long Lists and Arrays with a default value 
>Sometimes we already know how many elements we need, but we also want each one to start with the same value. For example, if you were writing a program that stores each person's drink at a restaurant. If nobody has ordered yet, we might want every drink to start as `water`.
>
>We can  give each element a starting value by doing this:
>```Kotlin
>fun orderDrinks(tableSize : Int){
>	var availableDrinks = arrayOf("water", "apple juice", "coffee")
>	// you can add more, but this is just for exmaple
>	var drinks = Array(tableSize) {"water"}
>	var response = ""
>	
>	for (index in 0..tableSize - 1){
>		println("What do you want to drink")
>		response = readLine()!!.lowercase()
>		
>		if (availableDrinks.contains(response))
>		{
>			drinks[index] = response
>		}
>	} 
>}
>```
>Now each element within `drinks` will start off holding `water`. 
>- `Array(tableSize)` creates an array with space for `tableSize` elements 
>- `{"water"}` tells Kotlin that each element should hold `water`.
>If you're interested in how this works, look up Kotlin or Java lambdas.

>[!info]- Java Equivalent
>>[!info]- Lists
>>Java's `ArrayList`s and Kotlin's `MutableList`s are very similar, but with different creation methods. 
>>```Java
>>List<String> drinks = new ArrayList<String>();
>>```
>>- `List<String>` tells java drink will be a list holding `Strings`
>>- `new ArrayList<String>()` creates a new `ArrayList` that holds `Strings`
>>
>>Similar to Kotlin's Mutable Lists, you can add, remove, or reassign items within a `ArrayList` 
>>```Java
>>import java.util.ArrayList;  
>>List<String> drinks = new ArrayList<String>();
>>
>>drinks.add("water");
>>drinks.add(0,"coffee"); //puts coffee into index zero and pushes everything else //back 1. So drinks == {"coffee", "water"}
>>
>>drinks.set(0, "soda");
>>
>>IO.println(drinks.get(0)); //prints soda
>>
>>drinks.remove(0);//removes the element at index 0
>>
>>IO.println(drinks.size()); //prints 1
>>```
>
>>[!info]- Arrays
>>Java's arrays are pretty similar to Kotlin's.Both allow their elements to be changed, but have a fixed size. Creating one is simple:
>>
>>```Java 
>>
>>String[] drinks = {"coffee", "soda", "water"};
>>
>>IO.println(drinks[0]); //prints coffee
>>
>>drinks[0] = "juice";
>>
>>IO.println(drinks[0]); //prints juice
>>
>>IO.println(drinks.length); //prints 3
>>```
>
>>[!info]- Iterating through List and Arrays
>>```Java
>>import java.util.ArrayList;
>>	
>>String[] drinksAvailable = {"coffee", "soda", "water"};
>>List<String> drinksRequest = new ArrayList<String>();
>>
>>for (int i = 0; i < drinksAvailable.size(); i++){
>>	IO.println("this works for drinksAvailable");
>>	IO.println(drinksAvailable.get(i));
>>}
>>
>>for (String drink : drinksRequested){
>>	IO.println("You can replace drinksAvailable with drinksRequested");
>>	IO.println(drink);
>>}
>>```
>>- `String drink` creates a new variable for each element within `drinksAvailable`
>>- `: drinksAvailable` is the array, or list that will be iterated through 


## Activity 9 
Now we're no longer limited to the number of variables, how about allowing the user to create as many characters as they want.  

- Allow the user to create as many characters as they want
- Store the characters in `MutableList`
- After the user is done, print out all the characters

```
Do you want to make a character?
yes <- User input

... Character Creation Dialogue (Look at activity 7) ... 


Do you want to make another? 
yes <- User input 

... Character Creation Dialogue (Look at activity 7) ... 


Do you want to make another? 
yes <- User input

... Character Creation Dialogue (Look at activity 7) ... 

Do you want to make another? 
yes <- User input

... Character Creation Dialogue (Look at activity 7) ... 

Do you want to make another? 
no <- User input 

Here are the characters you created:
... print out the Characters ...
```

>[!info]- Example Code
>>[!info]- Kotlin
>>```Kotlin
>>fun main(){
>>	val characters = mutableListOf<Character>()
>>	
>>	if (validateYesOrNo("Do you want to make a character")){
>>		characters.add(createNewCharacter())
>>		
>>		while(validateYesOrNo("Do you want to make another character")){
>>			characters.add(createNewCharacter())
>>		}
>>
>>		println("Here are the characters you created:")
>>		
>>		for (character in characters){
>>			character.printCharacter()
>>		}
>>	}
>>}
>>```
>
>>[!info]- Java
>>```
>>import java.util.ArrayList; 
>>import java.util.List; 
>>
>>
>>void main(){
>>	List<Character> characters = new ArrayList<Character>();
>>
>>	if(validateYesOrNo("Do you want to make a character")){
>>		characters.add(createNewCharacter());
>>		
>>		while (validateYesOrNo("Do you want to make another character")){
>>			characters.add(createNewCharacter());
>>		}
>>		
>>		IO.println("Here are the characters you created:");
>>		
>>		for (Character character : characters){
>>			character.printCharacter();
>>		}
>>	}
>>}
>>```

## Enums and Data Class 
If you created a `createNewCharacter()` function, then I want you to look back at it. If not, then you can look at the example below. 

>[!info]- Example code
>```Kotlin
>var head = ""
>    var torso = ""
>    var legs = ""
>    var name = ""
>    var response : Int
>
>    if (validateYesOrNo("Do you want to make a character")){
>        println("Here are the heads you can choose from")
>        printHeads()
>        response = validateNumber("Which head do you want?",1, 3)
>
>        if(response == 1){
>            head = """
>                 .-.
>                (•‿•)
>                 `-'
>            """.trimIndent()
>        }else if(response == 2){
>            torso = """
>                +---+  
>                |o o|  
>                |_-_|  
>                +---+
>            """.trimIndent()
>        }else {
>            head = """
>                 .-.  
>                |x x|  
>                | ^ |  
>                 `-'
>            """.trimIndent()
>        }
>
>        println("Here are the torsos you can choose from")
>        printTorsos()
>        response = validateNumber("which torso do you want?",1, 3)
>
>        if (response == 1){
>            torso = """
>                 /|\
>                |===|
>                |___|
>            """.trimIndent()
>        }else if(response == 2){
>            torso = """
>                [###]
>                 |#|
>                 |#|
>            """.trimIndent()
>        }else {
>            torso = """
>                 /V\  
>                <###>  
>                 \#/
>            """.trimIndent()
>        }
>
>        println("Here are the legs you can choose from")
>        printLegs()
>        response = validateNumber("Which legs do you want?",1, 3)
>
>        if(response == 1){
>            legs = """
>                 / \ 
>                /___\
>            """.trimIndent()
>        }else if(response == 2){
>            legs = """
>                (O O)
>            """.trimIndent()
>        }else{
>            legs = """
>                '~~~~~
>            """.trimIndent()
>        }
>
>        println("What is your characters name?")
>       name = readLine()!!
>       
>       return Character(name, head, torso, legs)
>```

Even though it's really simple code, isn't it annoying to read? Sure you could store the heads into variables, but where would you put it? In Character, which would require a character object to access. Instead we can choose to use an Enum. 

An Enum is a data type that has fixed possible values. So if we're to place one of the heads into one, we could replace all instances of it with `Head.SMILE`.  It could look like this. 
```Kotlin 
enum class Head(val asciiArt : String){
	SMILE(
		"""
		 .-.
		(•‿•)
		 `-'
		""".trimIndent()
	),
}

fun main(){
	println(Head.SMILE.asciiArt)
	//this would be printed  
	//   .-.
	//	(•‿•)
	//   `-'
}
```
There are a few things to notice in this Enum example: 
- `enum class Head` which creates the Enum 
- `(val asciiArt : String)` which tells Kotlin that each possible value of the Enum will store a `String`
- `SMILE(...)` creates one of the possible values of `Head` and stores the provided text in `asciiArt`.
- `Head.SMILE.asciiArt` is how we access the text stored in the `SMILE` object
- `SMILE` is in all caps because the Kotlin convection is that we capitalize each letter of the name of a constant. However, on our team, we capitalize only the first letter of constants in a Enum. If the constant is outside of an Enum, the we put its in name in full caps.

If you want to add another head, then just add a comma to the end of the first line and create another possible below it. Like this: 
```Kotlin
enum class Head(val asciiArt : String){
	SMILE(
		"""
		 .-.
		(•‿•)
		 `-'
		""".trimIndent()
	),
	ROBOT(
		"""
		+---+  
		|o o|  
		|_-_|  
		+---+
		""".trimIndent()
	)
	
}
```
You can add as many Enum values as you want.

### Passing Enum Values 
Since Enums are their own data type, we can easily pass their values into parameters.  
```Kotlin
fun printHead(head : Head){
	println(head.asciiArt)
}
```

You can also return Enum values. 
```Kotlin
fun getHead(headNum : Int) : Head{
	if (headNum == 1){
		return Head.SMILE
	}else{
		return Head.ROBOT
	}	
}
```

### Methods
Just like classes, Enums can also have methods. Since each head already stores its own ASCII art, it makes sense for it to know how to print itself. To add a `print()` method, we first need to add a semicolon after the final Enum value
```Kotlin 
enum class Head(val asciiArt : String){
	SMILE(
		"""
		 .-.
		(•‿•)
		 `-'
		""".trimIndent()
	),
	ROBOT(
		"""
		+---+  
		|o o|  
		|_-_|  
		+---+
		""".trimIndent()
	);
	
	fun print(){
		println(asciiArt)
	}
	
}
```


### Data Classes 
Take a look at this code:
```Kotlin
class Student(
	var firstName : String, 
	var lastName : String, 
	var school : String,
	val studentID : Int,
	val dayBorn : Int,
	val monthBorn : Int,
	val yearBorn : Int
)
```
Can you think of any way to improve it? Some of you might say put `dayBorn`, `monthBorn`, and `yearBorn` into a class, which would be correct. However, a `Date` class would only exist to store information. So we can use a data class instead. A data class is a type of class whose primary purpose is to store information. 
```Kotlin
data class Date(
	val month : Int, 
	val day : Int,
	val year : Int	
)

```
Now we can combine `dayBorn`, `monthBorn`, and `yearBorn` into a single variable.

```Kotlin
class Student(
	var firstName : String, 
	var lastName : String, 
	var school : String,
	val studentID : Int,
	val dateBorn : Date,
)

fun main(){
	val dateBorn = Date(1,1,2012)
	
	val student1 = Student("John", "Smith", "Oak School", 2600809, dateBorn)

}
```

### Data Class Methods
I know I said data classes are meant for storing information and that is true; however, imagine you have a data class named `Person` which stores a person's weight in kilograms. What if you wanted their weight in pounds? Sure you could make a function called `fromKgToLbs()` or you could just make a method inside of `Person` that did it for you.  
```Kotlin
data class Person(var weight : Double){
	val CONVERSION_FACTOR = 2.20462
	
	fun weightInLbs() : Double{
		return weight * CONVERSION_FACTOR
	}
}
```

Generally, methods inside a data class should be directly related to the information stored. Like converting kilograms to pounds, different forms of the same information (like a method that returns the name of the month rather than its number), or calculating the area of a shape.

>[!info]- Java Equivalent
>>[!info]- Enums
>>Java's Enums are a little bit different since you put the field below the Enum values you're defining - like this:
>>```Java
>>enum Head{
>>	SMILE("""
>>		 .-.
>>		(•‿•)
>>		 `-'
>>		"""
>>	),
>>
>>	ROBOT("""
>>		+---+  
>>		|o o|  
>>		|_-_|  
>>		+---+
>>		"""
>>	);
>>	
>>	private String asciiArt;
>>	
>>	private Head(String asciiArt){
>>		this.asciiArt = asciiArt;
>>	}
>>	
>>	public String getAsciiArt(){
>>		return this.asciiArt;
>>	}
>>}
>>``` 
>
>>[!info]- Data Classes
>>Java does have something similar to a data class. However, the fields in its instances (objects made from it) are private and immutable (unchangeable).  Moreover, extra fields declared in the body of the record (the stuff in-between the `{}`) must have the `static` keyword  which makes it a value shared by all instances.
>>```
>>record Person(double weight, String name){
>>	static double CONVERSION_FACTOR = 2.20462;
>>
>>	public double weightInLbs(){
>>		return this.weight * CONVERSION_FACTOR;
>>	}
>>}
>>```
>>However, Java automatically generates getters (functions that return private field variables) so it's pretty easy to access the data.
>>```
>>record Person(double weight, String name){
>>	static double CONVERSION_FACTOR = 2.20462;
>>
>>	public double weightInLbs(){
>>		return this.weight * CONVERSION_FACTOR;
>>	}
>>}
>>
>>void main(){
>>	Person person1 = new Person(65, "John");
>>	IO.println(person1.weight());
>>}
>>```

## Activity 10 
Although we have a functional character creator, we are still missing RPG professions - such as a mage. For this activity, you're going to create 5 programming classes for 5 different professions.

>[!info]- example professions and skills
>- Mage: Fireball
>- Archer: Long Shot
>- Fighter: Power Strike
>- Rogue: Sneak Attack
>- Healer: Heal

- Create a class for each of the five professions
- Each class should have a mana, hp, strength, intelligence, and agility stat 
- Each object should start out with 3 healing potions
- Each should have a skill unique to them, e.g. fireball for the mage. 
- Each class should have a function to use their special skill, to attack, to rest (restores hp and mana), to use a healing potion, and to take damage. 

```
There is no user interaction for this activity 
```

>[!info]- Rounding
>>[!info]- Kotlin
>>In Kotlin, there is a function that will round numbers we pass into it: 
>>```Kotlin
>>import kotlin.math.round
>>fun main(){
>>	val num1 : Double = 3.6
>>	val num2: Double = 3.2
>>	
>>	val rounded1 = round(num)
>>	val rounded2 = round(num2)
>>	println("num1 rounds ups to become $rounded1)
>>	println("num2 rounds down to $rounded2") 
>>}
>>```
>
>>[!info]- Java
>>In Java, there is a method that will round the doubles we pass into it
>>```Java
>>import static java.lang.Math.round;
>>void main(){
>>	double num1 = 2.6;
>>	double num2 = 2.3;
>>	
>>	int rounded1 = (int) round(num1);
>>	IO.println("num1 rounded is " + rounded1);
>>	
>>	int rounded2 = (int) round(num2);
>>	IO.println("num2 rounded is " + rounded2);
>>}
>>``` 

>[!info]- Example Code
>>[!info]- Kotlin
>>>[!info]- Mage
>>>```Kotlin
>>>class Mage(var name : String){
>>>	var hp : Int = 100
>>>	var mana : Int = 100
>>>	var strength : Int = 5
>>>	var intelligence : Int = 10
>>>	var agility : Int = 7
>>>	var healingPotionsLeft : Int = 3
>>>	
>>>	fun takeDamage(damage : Int){
>>>		hp -= damage
>>>	}
>>>	
>>>	fun attack() : Int{
>>>		return strength
>>>	}
>>>	
>>>	fun specialSkill() : Int{
>>>		println("I cast Fireball")
>>>		return round(intelligence * 1.1).toInt()
>>>	}
>>>	
>>>	fun rest(hours : Double){
>>>		val recovery = round(hours * 1.5).toInt()
>>>		hp += recovery
>>>		mana += recovery 
>>>	}
>>>	
>>>	fun useHealingPotion(){
>>>		if (healingPotionsLeft <= 0){
>>>			println("You don't have any healing potions left")
>>>		}else{
>>>			hp += 30
>>>			healingPotionsLeft -= 1
>>>			println("You have $healingPotionsLeft healing potions remaining")
>>>		}
>>>	}
>>>
>>>}
>>>```
>>
>>>[!info]- Archer
>>>// Archer file 
>>>```Kotlin
>>>class Archer(var name : String){
>>>	var hp : Int = 100
>>>	var mana : Int = 100
>>>	var strength : Int = 7
>>>	var intelligence : Int = 5
>>>	var agility : Int = 10
>>>	var healingPotionsLeft : Int = 3
>>>	
>>>	fun takeDamage(damage : Int){
>>>		hp -= damage
>>>	}
>>>	
>>>	fun attack() : Int{
>>>		return strength
>>>	}
>>>	
>>>	fun specialSkill() : Int{
>>>		println("I use Long Shot")
>>>		return round(strength * 1.1).toInt()
>>>	}
>>>	
>>>	fun rest(hours : Double){
>>>		val recovery = round(hours * 10).toInt()
>>>		hp += recovery
>>>		mana += recovery 
>>>	}
>>>	
>>>	fun useHealingPotion(){
>>>		if (healingPotionsLeft <= 0){
>>>			println("You don't have any healing potions left")
>>>		}else{
>>>			hp += 30
>>>			healingPotionsLeft -= 1
>>>			println("You have $healingPotionsLeft healing potions remaining")
>>>		}
>>>	}
>>>}
>>>```
>>
>>>[!info]- Fighter
>>>```Kotlin
>>>class Fighter(var name : String){
>>>	var hp : Int = 100
>>>	var mana : Int = 100
>>>	var strength : Int = 10
>>>	var intelligence : Int = 5
>>>	var agility : Int = 7
>>>	var healingPotionsLeft : Int = 3
>>>	
>>>	fun takeDamage(damage : Int){
>>>		hp -= damage
>>>	}
>>>	
>>>	fun attack() : Int{
>>>		return strength
>>>	}
>>>	
>>>	fun specialSkill() : Int{
>>>		println("I used Power Attack")
>>>		return round(strength * 1.1).toInt()
>>>	}
>>>	
>>>	fun rest(hours : Double){
>>>		val recovery = round(hours * 10).toInt()
>>>		hp += recovery
>>>		mana += recovery 
>>>	}
>>>	
>>>	fun useHealingPotion(){
>>>		if (healingPotionsLeft <= 0){
>>>			println("You don't have any healing potions left")
>>>		}else{
>>>			hp += 30
>>>			healingPotionsLeft -= 1
>>>			println("You have $healingPotionsLeft healing potions remaining")
>>>		}
>>>	}
>>>
>>>}
>>>```
>>
>>>[!info]- Rogue
>>>```Kotlin
>>>class Rogue(var name : String){
>>>	var hp : Int = 100
>>>	var mana : Int = 100
>>>	var strength : Int = 5
>>>	var intelligence : Int = 7
>>>	var agility : Int = 10
>>>	var healingPotionsLeft : Int= 3
>>>	
>>>	fun takeDamage(damage : Int){
>>>		hp -= damage
>>>	}
>>>	
>>>	fun attack() : Int{
>>>		return strength
>>>	}
>>>	
>>>	fun specialSkill() : Int{
>>>		println("I use Sneak Attack")
>>>		return round(agility * 1.1).toInt()
>>>	}
>>>	
>>>	fun rest(hours : Double){
>>>		val recovery = round(hours * 10).toInt()
>>>		hp += recovery
>>>		mana += recovery 
>>>	}
>>>	
>>>	fun useHealingPotion(){
>>>		if (healingPotionsLeft <= 0){
>>>			println("You don't have any healing potions left")
>>>		}else{
>>>			hp += 30
>>>			healingPotionsLeft -= 1
>>>			println("You have $healingPotionsLeft healing potions remaining")
>>>		}
>>>	}
>>>
>>>}
>>>```
>>
>>>[!info]- Healer
>>>```Kotlin
>>>class Healer(var name : String){
>>>	var hp : Int = 100
>>>	var mana : Int = 100
>>>	var strength : Int= 5
>>>	var intelligence : Int = 10
>>>	var agility : Int = 7
>>>	var healingPotionsLeft : Int = 3
>>>	
>>>	fun takeDamage(damage : Int){
>>>		hp -= damage
>>>	}
>>>	
>>>	fun attack() : Int{
>>>		return strength
>>>	}
>>>	
>>>	fun specialSkill() : Int{
>>>		println("I cast Heal")
>>>		return round(-intelligence * 1.1).toInt();
>>>	}
>>>	
>>>	fun rest(hours : Double){
>>>		val recovery = round(hours * 10.0).toInt()
>>>		hp += recovery
>>>		mana += recovery 
>>>	}
>>>	
>>>	fun useHealingPotion(){
>>>		if (healingPotionsLeft <= 0){
>>>			println("You don't have any healing potions left")
>>>		}else{
>>>			hp += 30
>>>			healingPotionsLeft -= 1
>>>			println("You have $healingPotionsLeft healing potions remaining")
>>>		}
>>>	}
>>>
>>>}
>>>```
>
>>[!info]- Java
>>>[!info]- Mage
>>>```Java 
>>>class Mage {
>>>	int hp = 100;
>>>	int mana = 100;
>>>	int strength = 5;
>>>	int intelligence  = 10;
>>>	int agility = 5;
>>>	int healingPotionsLeft = 3;
>>>	String name;
>>>	
>>>	public Mage(String name){
>>>		this.name = name;
>>>	}
>>>	
>>>	public void takeDamage(int damage){
>>>		hp -= damage;
>>>	}
>>>	
>>>	public int attack(){
>>>		return strength;
>>>	}
>>>	
>>>	public int specialSkill(){
>>>		IO.println("I cast Fireball");
>>>		return (int) round(intelligence * 1.1)
>>>	}
>>>	
>>>	public void rest(double hours){
>>>		int recovery = (int) round(hours * 10.0);
>>>		hp += recovery;
>>>		mana += recovery;
>>>	}
>>>	
>>>	public void useHealingPotion(){
>>>		if (healingPotionsLeft <= 0){
>>>			IO.println("You don't have any healing potions left");
>>>		}else {
>>>			hp += 30;
>>>			healingPotionsLeft -= 1;
>>>			IO.println("You have " + healingPotionsLeft +  "healing potions remaining");
>>>		}
>>>	}
>>>}
>>>```
>>
>>>[!info]- Archer
>>>```Java 
>>>class Archer {
>>>	int hp = 100;
>>>	int mana = 100;
>>>	int strength = 7;
>>>	int intelligence   = 5;
>>>	int agility = 10;
>>>	int healingPotionsLeft = 3;
>>>	String name;
>>>	
>>>	public Archer(String name){
>>>		this.name = name;
>>>	}
>>>	
>>>	public void takeDamage(int damage){
>>>		hp -= damage;
>>>	}
>>>	
>>>	public int attack(){
>>>		return strength;
>>>	}
>>>	
>>>	public int specialSkill(){
>>>		IO.println("I use Long Shot");
>>>		return (int) round(strength * 1.1);
>>>	}
>>>	
>>>	public void rest(double hours){
>>>		int recovery = (int) (hours * 10);
>>>		hp += recovery;
>>>		mana += recovery;
>>>	}
>>>	
>>>	public void useHealingPotion(){
>>>		if (healingPotionsLeft <= 0){
>>>			IO.println("You don't have any healing potions left");
>>>		}else {
>>>			hp += 30;
>>>			healingPotionsLeft -= 1;
>>>			IO.println("You have " + healingPotionsLeft +  "healing potions left");
>>>		}
>>>	}
>>>}
>>>```
>>
>>>[!info]- Fighter
>>>```Java 
>>>class Fighter {
>>>	int hp = 100;
>>>	int mana = 100;
>>>	int strength = 10;
>>>	int intelligence   = 5;
>>>	int agility = 7;
>>>	int healingPotionsLeft = 3;
>>>	String name;
>>>	
>>>	public Fighter(String name){
>>>		this.name = name;
>>>	}
>>>	
>>>	public void takeDamage(int damage){
>>>		hp -= damage;
>>>	}
>>>	
>>>	public int attack(){
>>>		return strength;
>>>	}
>>>	
>>>	public int specialSkill(){
>>>		IO.println("I use Power Attack");
>>>		return (int) (strength * 1.1);
>>>	}
>>>	
>>>	public void rest(int hours){
>>>		double recovery = (int) (round(hours * 10));
>>>		hp += recovery;
>>>		mana += recovery;
>>>	}
>>>	
>>>	public void useHealingPotion(){
>>>		if (healingPotionsLeft <= 0){
>>>			IO.println("You don't have any healing potions left");
>>>		}else {
>>>			hp += 30;
>>>			healingPotionsLeft -= 1;
>>>			IO.println("You have " + healingPotionsLeft +  "healing potions left");
>>>		}
>>>	}
>>>}
>>>```
>>
>>>[!info]- Rogue
>>>```Java 
>>>class Rogue {
>>>	int hp = 100;
>>>	int mana = 100;
>>>	int strength = 5;
>>>	int intelligence   = 7;
>>>	int agility = 10;
>>>	int healingPotionsLeft = 3;
>>>	String name;
>>>	
>>>	public Rogue(String name){
>>>		this.name = name;
>>>	}
>>>	
>>>	public void takeDamage(int damage){
>>>		hp -= damage;
>>>	}
>>>	
>>>	public int attack(){
>>>		return strength;
>>>	}
>>>	
>>>	public int specialSkill(){
>>>		IO.println("I use Sneak Attack");
>>>		return (int) (agility * 1.1);
>>>	}
>>>	
>>>	public void rest(double hours){
>>>		int recovery = (int) (round(hours * 10));
>>>		hp += recovery;
>>>		mana += recovery;
>>>	}
>>>	
>>>	public void useHealingPotion(){
>>>		if (healingPotionsLeft <= 0){
>>>			IO.println("You don't have any healing potions left");
>>>		}else {
>>>			hp += 30;
>>>			healingPotionsLeft -= 1;
>>>			IO.println("You have " + healingPotionsLeft +  "healing potions left");
>>>		}
>>>	}
>>>}
>>>```
>>
>>>[!info]- Healer
>>>```Java 
>>>class Healer {
>>>	int hp = 100;
>>>	int mana = 100;
>>>	int strength = 5;
>>>	int intelligence   = 10;
>>>	int agility = 7;
>>>	int healingPotionsLeft = 3;
>>>	String name;
>>>	
>>>	public Healer(String name){
>>>		this.name = name;
>>>	}
>>>	
>>>	public void takeDamage(int damage){
>>>		hp -= damage;
>>>	}
>>>	
>>>	public int attack(){
>>>		return strength;
>>>	}
>>>	
>>>	public int specialSkill(){
>>>		IO.println("I cast Heal");
>>>		return (int) round(intelligence * -1.1);
>>>	}
>>>	
>>>	public void rest(double hours){
>>>		int recovery = (int) (round(hours * 10));
>>>		hp += recovery;
>>>		mana += recovery;
>>>	}
>>>	
>>>	public void useHealingPotion(){
>>>		if (healingPotionsLeft <= 0){
>>>			IO.println("You don't have any healing potions left");
>>>		}else {
>>>			hp += 30;
>>>			healingPotionsLeft -= 1;
>>>			IO.println("You have " + healingPotionsLeft +  "healing potions left");
>>>		}
>>>	}
>>>}
>>>```

## Inheritance
Take a look at the code from the previous activity. Don't the classes seem pretty similar? They have the same fields and some of the same methods: `mana`, `hp`, `rest`, etc. If we wanted to add another profession like `Cleric`, then we would have to rewrite the same fields and methods. Moreover, if we wanted to change something like the `rest()` mechanic, then we would have to change it for all professions.

Wouldn't it be better if we only had to write one set of fields and methods instead of repeating them for every profession. This is where inheritance comes in.

Let's say we had this `Person` (the parent class) class:
```Kotlin
open class Person(
		val name : String
	){
	
	fun printInfo(){
		println(name)
	}
}
```
- By default, Kotlin classes can't be inherited, so use the `open` keyword to tell Kotlin that other classes can inherit it

And we wanted a `Student` class (the child class) to include the same fields and methods as `Person`. So we have the `Student` inherit `Person` like this:
```Kotlin
class Student(
	name : String,
	val school : String
) : Person(name){

}
```
- The `: Person` tells Kotlin that the `Student` class will inherit from `Person`. 
- Since `Person` requires the `name` constructor parameter, we add it as a parameter to `Student` so that we can pass it to `Person`.   

By letting `Student` inherit (or extend) from `Person`, we can now do this: 
```Kotlin
val student1 = Student("John", "River School")

student1.printInfo()
println(student1.name)
println(student1.school)

```
This is because when a class inherits another, it takes it as a base. From there, the child class's fields and methods will be added on top, allowing us to access the fields and methods in the child and parent classes. 

### Override
Sometimes we want a class to inherit from another, but we want its method to work a bit differently. Take the `printInfo()` method as an example, right now it will only print the name of the student, but it doesn't mention which school they attend. However, by overriding the method, we're able to create a custom version of `printInfo()` inside of `Student`.

Since `printInfo()` has code in it (there are cases when methods don't have anything in them), we first have to tell Kotlin that `printInfo()` can be overridden by adding `open`:

```Kotlin
open class Person(
		val name : String
	){
	
	open fun printInfo(){
		println(name)
	}
}
```

Now we can override `printInfo()`
```Kotlin 
class Student(
	name : String,
	val school : String
) : Person(name){

	override fun printInfo(){
		super.printInfo()
		println(school)
	}
}

```
- `override`  tells Kotlin that we want to replace the `printInfo()` function only in this child class
- Normally, calling `printInfo()` inside `Student` would call the overridden version in `Student` again. `super.printInfo()` tells Kotlin to use the parent class's version instead

### Passing Child Classes in Parameters
Let's say you were making a game, where the user can choose to interact with several different character types - employees, bosses, students, teachers etc. You could make a function of each type of interaction: 
```Kotlin
fun interactWithEmployee(employee : Employee){}

fun interactWithBoss(boss : Boss){}

fun interactWithStudent(student : Student){}

fun interactWithTeacher(teacher : Student){}
```
Or if they all inherit the same type, you could do this: 
```Kotlin
fun interactWithCharacter(character : Character){}
```
Now you can pass any object whose class inherits `Character` into the function. **However**, you'll only be able to access and use methods from the parent class **unless** Kotlin can guarantee that the passed object is a specific type. If curious how to guarantee a type, then look at [Kotlin's Type Checks](https://kotlinlang.org/docs/typecasts.html)
 
>[!info]- Java
>>[!info]- Inheritance  
>>Class inheritance in Java is really simple, you just add `extends` and then the class it's inheriting.  Like this:
>>```
>>class Person{
>>	String name;
>>	
>>	public Person(String name){
>>		this.name = name;
>>	}
>>	
>>	public void printInfo(){
>>		IO.println("Name : " + name); 
>>	}
>>}
>>
>>class Student extends Person{
>>	String school; 
>>	
>>	public Student(String name, String school){
>>		super(name);
>>		this.school = school;
>>	}
>>}
>>```
>
>>[!info]- overriding 
>>You can override a method by only redefining the method inside the child class. Although it is recommended to put a `@Override` before the function, like this:
>>```Java
>>class Student extends Person{
>>	String school; 
>>	
>>	public Student(String name, String school){
>>		super(name);
>>		this.school = school;
>>	}
>>	
>>	@Override
>>	public void printInfo(){
>>		super.printInfo();
>>		IO.println("School : " + school );
>>	}
>>}
>>```

## Activity 11
This is usually the point where I would say "lets add xyz", but this activity is a bit different. I want to introduce an open ended final project. You can make whatever you want as long as it includes:
- Classes 
- Lists
- Inheritance

If you don't know what to make, here are a few ideas 
- Finish creating a combat system for the Character Creator 
- A choose your own adventure game 


>[!info]- Complex Ideas 
>- If you want to make an android app, [here is a website to help with that.](https://developer.android.com/courses/android-basics-compose/course)
>- If you want to make a game with visuals, [I would recommend taking a look at this](https://www.geeksforgeeks.org/blogs/kotlin-for-game-development/#2-choose-the-right-game-engine)  


## others no activity
%%
Enums 
	- use 
	- when we use it 
	- how to make them 

companion objects
	 - how to make them 
	 - why we use it 

interface 
	- Why we use it 
	- example 
	- 
%%
%%

When Time permits
Useful Kotlin shortcuts
- `when`
- `repeat`
- `if` expressions (Kotlin's replacement for the ternary operator)
- `in`
- `!in`
- `until`
- `downTo`
- `step`
- `indices`
- `withIndex()`
- `Pair`
- `Triple`
- Destructuring
- Named arguments
- Default parameters
- Trailing commas
- String templates (`"${}"`)
- Raw strings (`""" """`)
- Scope functions (`let`, `run`, `also`, `apply`, `with`) — maybe just an overview
- Type inference (`val x = 5`)
- Smart casts (`is`)
// when()
// terinary opperators 
//repeat


Advanced 

lamdas
example:

- Generics
- Lambdas
- Function references (`::`)
- Higher-order functions
- Extension functions
- Delegation
- Companion objects
- Object declarations
- Anonymous objects
- Sealed classes
- Inline functions
- Reified generics (probably very advanced)
- Coroutines (only if you think they'll ever use them)

%%