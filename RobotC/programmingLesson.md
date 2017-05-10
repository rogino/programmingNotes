# Bits

A computer, at its most basic level, runs on 1s and 0s. This, is called a 'bit'. Each bit can take one of two values, 0 or 1, true or false, yes or no: any two values, really.

If you have two bits, you can have 4 values. For now, think of them as the answers to two closed questions, which can be answered 'yes' or 'no'.

|       | True       | False       |
| ----- | ---------- | ----------- |
| True  | True True  | True False  |
| False | False True | False False |

As you can see, you can have 4 distinct values. You can also use bits to represent numbers. From here on, we will denote the values of a bit as 1 or 0.

# Bytes 

With three bits, you could have the first bit equal 1, the second bit equal 2, and the third bit equal 4, each value doubling: this is useful because you can represent all values up to 7 with this.

If, for example, the 3 bits equal '000', then the number it represents is 0. With '001', it is 1. '010' is 2 and so on. You can do this systematically using a table:

| 4    | 2    | 1    |
| ---- | ---- | ---- |
| 1    | 0    | 1    |

Here, '101' represents 5 as there is a '1' in the column representing 4, and '1' in the column representing '1'. Add 1 and 4 together to get 5.



Computers usually use bits in groups of 8, called a byte. With this, you can represent numbers up to 255, which is $$2^8 -1$$ (2^8 means 2x2x2x2x2x2x2x2, or two multiplied by itself 8 times):

| 128  | 64   | 32   | 16   | 8    | 4    | 2    | 1    |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| 1    | 1    | 0    | 1    | 0    | 1    | 1    | 0    |

Here, this number equals:

$$128+64+16+4+2=214$$

### Sidenote: Integer overflow

If you have done long addition, you should be familiar with carrying. What happens in binary? If you add `11` to `1101 0110`:

| 128  | 64   | 32   | 16   | 8    | 4    | 2    | 1    |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| 1    | 1    | 0    | 1    | 0    | 1    | 1    | 0    |
| 0    | 0    | 0    | 0    | 0    | 0    | 1    | 1    |
| 1    | 1    | 0    | 1    | 1    | 0    | 0    | 1    |

With the first byte, `0+1=1`. But for the second, `1+1=?`. One plus one will, in base 2, equal `10`. Thus, it will carry: 	`1+0=1`, `0+0=0`, `1+1=10`.

But what happens if you add `1` to `1111 1111`, or 255?

Lets do the same as above, but have 9 columns:

| -    | 1    | 1    | 1    | 1    | 1    | 1    | 1    | 1    |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| -    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 1    |
| 1    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    |

Evidently, the `10` from `1+1` will carry throughout the entire 8 bits, ending up as `1 0000 0000` at the end. However, the computer does not read the first `1`, so it becomes `0000 0000`: `1111 1111 + 1 = 0000 0000`. This is integer overflow.



## Signs

Currently, we have a range of `0 to 255`, but what if we want negatives, such as for making the robot go backwards? We can use *signed* numbers. Like the name suggests, these numbers have signs: + or -, instead of all of it being positive. This halves the range to `-128 to 127`, almost split down the middle, and is what the motors actually use.

# Types

Computers can count up more than 255- in fact, this is a data type called a `char`. Usually, you will be dealing with `int`, which means integer, which in math, means a whole number. This has a much greater range, and is made by using more than one byte, but 2, 3, 4 or more bytes.



## Booleans

Booleans are made of 1 bit: they can have either `true` or `false`, `1` or `0` values. These are useful for what are called *conditionals*

## Conditionals

Conditionals allow you to respond to events, such as a button being pressed on the remote. For example, you may want an arm to move up when a button is pressed. To do this, use a `if else ` statement.

```C
if (vexRT[Btn6U]) {
  motor[armMotor] = 127;
}

else {
  motor[armMotor] = 0;
}
```

The `if else` statement allows you to put a fork in your program, where it can take more than one path. 

Up the top you see `if(vexRT[Btn6U])...`. The `if` tells it that it is a if statement. Between `()` is a *boolean*. It tells it, *if some condition is true*, in this case, if button 6U is pressed, *then do something*. That something is between `{}` curly braces, and you can have multiple lines in here. This has only one line, which **sets the value** of `armMotor` (named in `Robot->Motors and Sensors setup`, referring to a motor in a specific port) to 127.

If that button is not pressed: if that condition is not met, it sets it to 0.



# Loops

Loops allow you to do things multiple times without needing to write them out multiple times. There are two main types, `while` and `for`.

## While

While loops tell you to repeat a task *while some condition is true*- a boolean is true. That might be if the battery is running at a voltage greater than 5V:

```C
while(nImmediateBatteryLevel/1000 > 5) {
  //do stuff
}
```

Here, you divide `nImmediateBatteryLevel` by 1000 to get the voltage, and see if it is *greater than* 5. The `>` is a comparison operator, which checks if the left side is bigger than the right side. Others exist, such as `==` (if the left side *equals* the right side), `<=` (If the left side is *smaller or equal to* the right side), and "!" (changes `false` to `true` and vice versa).

## For 

For loops are more complicated than this. For no reason, lets count from 1 to 100:

```C
print(1);
print(2);
print(3);
...
```

NB: `print` is not a real function. 

That takes quite a bit of time. Instead, you can use `for` loops:

```C
for (int i = 1; i <= 100; i++) {
  print(i);
}
```

The `for` is a *keyword*, telling it that this is a for loop. The stuff inside the `()` tells you several things: `int i = 0` creates a integer, `i` , setting it to equal `1`. After the `;` semicolon is a boolean: `i <= 100`. This means that the loop will continue until `i` is not *smaller than or equal to* 100: a boolean statement. Finally, after another `;`, is `i++`. This tells the computer to add `1` to `i` every time the loop loops. It is the same as saying, `i = i + 1`, which sets `i` to the current value of `i` plus 1.



 # Functions

If I tell you to make me a cup of coffee, I do not tell you to conduct a single operation. Instead, you conduct a series of, *multiple* operations under the umbrella of 'making a cup of coffee' such as getting a cup, boiling water etc.. This is essentially what a function is. 

Inside a function, you can have multiple commands. For example, you might make the robot go forwards for 5 seconds, turn right for 1 second, then go backwards for 5:

```C
void myFunction() {
  motor[l] = 127;
  motor[r] = 127;
  wait1Msec(5000);
  
  motor[l] = -127;
  motor[r] = 127;
  wait1MSec(1000);
  
  motor[l] = -127;
  motor[r] = -127;
  wait1MSec(5000);
  
  motor[l] = 0;
  motor[r] = 0;
}
```

If you type, `myFunction();`, then the robot will do everything inside that block.



Going back to the coffee analogy, let's say that I am a tea nerd, and tell you, 'Get me a cup of Earl Grey tea', and 'Get me a cup of English Breakfast tea'. Those two are essentially the same thing, with only minor differences in what teabag you use etc.. If `makeCupOfTea()` was a function, it would have what are called *arguments*, which can get user input. For a robot, one such function might be one that sets the two motors:

```C
void setMotorSpeed(int leftMotor, int rightMotor) {
  motor[l] = leftMotor;
  motor[r] = rightMotor;
}
```

Now, instead of setting the two motors one by one, you can do it more efficiently. Instead of typing:

```C
motor[l] = 127;
motor[r] = 127;
```

You can do:

```C
setMotorSpeed(127, 127);
```

This is much cleaner, easier to read, and shorter.



# Syntax

Computers are very picky about syntax. First, end statements/commands with a `;` semicolon. This includes:

```C
int variable = 10; //Declaring Variables
variable *= 10; //Modifying variables. NB: *= is the same as variable = 10 * variable
setMotorSpeed(126, 127); //After running functions

//BUT NOT
while(true) {
  if (true) {
    for(int i = 0; i < 100; i++) {
      //Except for inside the () in for loops
    }
  }
}
```

