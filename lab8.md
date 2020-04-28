# Background

## Learning objectives

* Learn how to write basic assembly and machine code programs
* Learn how does recursion work

## Story

A high-level program (Java, C/C++, etc.) is first converted to an semantically-equivalent low-level program (assembly) that is converted to directly machine runnable code (machine code).
The low-level program is composed of many instructions, which are executed by the computer hardware.
Those low-level program usually doesn't even have the concept of function, array, nor string.
Yet they are 100% capable of doing whatever you can do with Java!

**Attention: We are NOT using IntelliJ IDEA nor GitHub Classroom in this lab.**

# Part 1: Left Shift

(Name your file as `lab8-left-shift.toy`)

1. Read [The TOY Machine](https://introcs.cs.princeton.edu/java/62toy/). Before you proceed, make sure you understand:
    * Where (which memory address) should I put my first line of program? (`0x10`)
    * What's special for memory address `0xFF`? (If you read from it, you actually read from stdin; if you write to it, you actually write to stdout)
1. Download [X-TOY](https://lift.cs.princeton.edu/xtoy/).
1. Launch the Visual X-TOY.  (Run `java -jar toy.jar` from the command line)
1. Click `File`/`Open Example Program`.
1. Select `Stdin`  (this is the name of the Example program from the `Open Example Program` menu item in the `File` menu.)
1. Read and understand the assembly program.
**Note:** Only the blue part (`xx: xxxx`) are actual program! Everything else is treated as comment, including `read R[A]`, `program xxx`, and `function xxx`.
1. Click `Mode`/`Sim Mode`. You should see a fake ancient computer interface.
1. To the right of your window, you can see that your program has already been loaded into the memory, starting at `0x10`.
1. Click the `Reset` button.
1. Click the `Run` button. You should see that the `INWAIT` light is on. It means that the machine is waiting for your input.
1. Flip the switches in the `DATA` section to represent the *decimal* number 115. (You need to convert it to binary) Note that the right-most switch represents 2^0 = 1 and the left-most switch represents 2^15 = 32768.
1. Click the `Enter` button. The `READY` light should be on.
1. Click the `Run` button. You should see that, in the memory panel, the second instruction (`0x11`) is being executed. At the same time, the `INWAIT` light is on, meaning that the machine is waiting for your input.
1. Flip the switches in the `DATA` section to represent the *decimal* number 126. (You need to convert it to binary)
1. Click the `Enter` button. The `READY` light should be on.
1. Click the `Run` button. The instruction at address `0x14` has been executed, which cause the machine to stop. Besides, an value it written to the big `STDOUT` display. It's hexadecimal so convert it back to decimal. What's the number? Does this result match your expectation?
1. When you are familiar with how TOY works, go back to `Mode`/`Edit Mode`.

**Now, try to modify the program that takes one input `A`, calculates `C = (2 to the power of A)` and output `C`.** (You may assume that A is no larger than 15)

Hint: There is nothing in the TOY instruction set that can perform multiplication, not to mention the power of arbitrary number. However, you only need to calculate the power of **2**. Which operator should you use? And how?

When you've finished, save your file as `lab8-left-shift.toy` and submit.

# Part 2: Dot product

(Name your file as `lab8-dot-product.toy`)

What you need to do is to compute the dot product of two 3-dimensional vectors.
Specifically, you need to read 6 values from stdin: `x1, y1, z1, x2, y2, z2` and output `x1*x2 + y1*y2 + z1*z2`.

Hint: How do you compute multiplication? See the **example** program `Fast Multiply` (`File`/`Open Example Program`). If you have trouble understanding `Fast Multiply`, you can use `Multiply` instead (at the cost of your grades).

When you've finished, save your file as `lab8-dot-product.toy` and submit.

# Part 3: Recursion

(Name your file as `lab8-recursion.toy`)

### Understand recursion and stack

Although TOY looks so tiny that you might feel it's kind of useless, it is actually much more powerful than you think.
You can even implement recursion right on top of TOY!

Think of the following simple Java program.
```java
public static void fib(int n) {
    if (n == 0)
        return 0;
    if (n == 1)
        return 1;
    int s;
    s = fib(n - 1);
    s += fib(n - 2);
    return s;
}
```
How do I translate it to something low-level, such as TOY?
Well, to make recursions possible, we need a new kind of data structure called *stack*.
You may treat a stack as a **resizable** array, but it can only resize by appending an item to the end or dropping the last item.
When used for making recursive function calls, we slice a stack into multiple *stack frames*, each corresponding to an *ongoing* function **call**. Stack frames can be of different sizes, of course.

**Note:** Making a function call creates a stack frame. `return` destroys one. Recursive functions will cause multiple stack frames of the same function to be live at the same time.

For example, if I call `fib(3)`, `fib(3)` calls `fib(2)`, `fib(2)` calls `fib(1)`, the stack looks like:
```
int[] stack = new [] {
        // the stack frame of fib(3)
        xxxx, xxxx, xxxx,
        // the stack frame of fib(2)
        xxxx, xxxx, xxxx,
        // the stack frame of fib(1)
        xxxx, xxxx, xxxx
    };
```

So what's inside a stack frame? It contains
* Things you need to **make another function call**, including
    * The arguments I want to use (`n - 1` and `n - 2`)
* Things you need to **remember after you make a function call**, including
    * The values of my local variables (my `int s`, because I don't want my `s` to be messed up with `fib(n - 1)`'s `s`)
    * Where should I return to (return address / previous PC)

### Implement stack with TOY

We put the array at the origin `0x00,0x01,0x02,...`. We use register `R[F]` to mark the *top* of the stack (i.e. the position of the last item **plus one**).

* At the very beginning, the top of the stack is `0x00`, which means that there is no elements in the stack.
* To append (push) an item, we can assign `M[R[F]]` to some value and increment `R[F]` by one.
* To remove (pop) an item, we can decrement `R[F]` by one. (*Q: Why we don't modify `M[R[F]]`?*)
* To access an item (local variables, return address, etc.) of my own, we can access `M[R[F] - k]` where different `k` corresponds to different items.
* To access an item (like parameters) that is stored by my parent (i.e. my caller), we can also do so by `M[R[F] - k]`.
(FYI: in modern computers we use stack base pointers to do so, but in this lab we don't require you to do it that way.)

### Your Job

Filling the blanks, try the program yourself, and submit the file.

**Note:** You may **NOT** add, remove, or modify any instructions. You may only fill in the blanks.

**Hint:** Read the comments. Make sure that your code is consistent with the comments.

**Hint:** You may want to print them out and figure out answers using paper and pencil.

**Hint:** To make the Visual X-TOY run faster, click `Tools`/`Options`, and click `Execution`/`Performance`.  Out of the box, X-TOY runs slows in order to allow the user to watch the program run, but for this program, the runtime might become long, so you might want to speed up the simulation.

```
program Recursion

// Register Convention
// R[0]: Fixed value 0000.
// R[1]: Fixed value 0001.
// R[2]: Fixed value 0002.
// R[3]: Fixed value 0003.
// R[4]~R[9]: DO NOT USE.
// R[A]: Good to use. Value may change after making a function call.
// R[B]: Good to use. Value may change after making a function call.
// R[C]: DO NOT USE.
// R[D]: Only use it to store function return values.
             Value may change after making a function call.
// R[E]: Only use it to temporarily store a PC.
             Value may change after making a function call.
// R[F]: Stack pointer. Used to mark the top of the stack.
             Value does NOT change after making a function call.

10: 7101   R[1] <- 0001
11: 7202   R[2] <- 0002
12: 7303   R[3] <- 0003
13: ____   R[F] <- ____
14: ____
15: EE00   goto R[E]

function fib                             public static void fib(int n) {
// M[00]:(The bottom of stack)
// ...       ...
//           My parent's parameter n
// ...           My parent's parent's PC
// M[R[F]-2]:    My parent's variable s
// M[R[F]-1]:    My parent's a, my parameter n
// M[R[F]]:          (Will be my parent's PC)
D0: BE0F   M[R[F]] <- R[E]
D1: 1FF1   R[F] <- R[F] + R[1]
D2: ____
D3: ____                                     int a = n;
D4: 9AFF   write R[A]                        System.out.println(a);
D5: ____                                     if (a != 0) {
D6: ____                                         a = a - 1;
D7: ____                                         if (a != 0) {

D8: ____                                             int s = 0; // on stack
D9: 1FF1   R[F] <- R[F] + R[1]
DA: ____                                             // copy a to the stack
DB: 1FF1   R[F] <- R[F] + R[1]
// M[00]:(The bottom of stack)
// ...       ...
//           My parent's parameter n
//               My parent's parent's PC
//               My parent's variable s
//               My parent's a, my parameter n
// ...               My parent's PC
// M[R[F]-2]:        My variable s
// M[R[F]-1]:        My variable a, my children's n
// M[R[F]]:              (Will be my child's parent's PC)
DC: FED0   R[E] <- PC; goto D0                       int d = fib(a);
DD: ____
DE: AA0B   R[A] <- M[R[B]]                           // a is recovered
DF: ____                                             a = a - 1;
E0: ____                                             // modify a on stack
E1: ____
E2: BD0B   M[R[B]] <- R[D]                           s = d; // on stack
E3: FED0   R[E] <- PC; goto D0                       d = fib(a);
E4: ____
E5: ____                                             int b = s;
E6: 1DDB   R[D] <- R[D] + R[B]                       d = d + b;
E7: ____
// M[00]:(The bottom of stack)
// ...       ...
//           My parent's parameter n
//               My parent's parent's PC
// ...           My parent's variable s
// M[R[F]-1]:    My parent's a, my parameter n
// M[R[F]]:          (Was my parent's PC)
// M[R[F]+1]:        (Was my variable s)
// ...               (Was my variable a)
E8: ____
E9: EE00   goto R[E]                                 return d;

EA: 7D01   R[D] <- 0001                          } else {
EB: ____
EC: ____
ED: EE00   goto R[E]                                 return d = 1;
                                                 }
EE: 7D00   R[D] <- 0000                      } else {
EF: ____
F0: ____
F1: EE00   goto R[E]                             return d = 0;
                                             }
                                         }

function main                            public static void main(String[] args) {
F2: ____                                     int a = scanner.nextInt();
F3: BA0F   M[R[F]] <- R[A]                   // copy a to the stack
F4: ____
F5: FED0   R[E] <- PC; goto D0               int d = fib(a)
F6: ____                                     System.out.println(d);
F7: ____                                     System.out.exit(0);
                                         }
```

### Bonus Questions

If you can answer the following questions successfully, you get bonus points.
Answer the questions directly in the `lab8-recursion.toy` file as comments.

1. (1 point) What is the maximum `n` such that this program still gives correct answer?
1. (2 points) If TOY registers and memory could handle infinite large numbers, will this program give correct answer for arbitrarily large `n`? Why or why not?
1. (5 points) Why is the program NOT contiguous? There is a big gap between `0x15` and `0xD0`.
1. (15 points) Add memoization to the program. You may use more registers if you want.
Please submit a separate file named `lab8-recursion-bonus.toy`.
*Hints:* How do you declare an array to store the results? Is the array shared across different function calls (stack frames) or each of them have its own array? Think about how stack is created out of nothing.
