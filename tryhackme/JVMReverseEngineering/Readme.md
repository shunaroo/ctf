# [Task 1] Introduction
```
getstatic java/lang/System.out:Ljava/io/PrintStream; // Retrieve the static variable "out" in the System class and store it on the stack
ldc "Hello World" // Load the string "Hello World" onto the stack
invokevirtual java/io/PrintStream.println:(Ljava/lang/String;)V // Invoke the "println" function on the System.out variable using the string at the top of the stack as an argument

https://en.wikipedia.org/wiki/Java_bytecode_instruction_listings

void main(String[] args, int i)
main([Ljava/lang/String;I)V

javap 
javap -v -p HelloWorld.class



Consider the following bytecode:
LDC 0
LDC 3
SWAP
POP
INEG
Which value is now at the top of the stack?

0
30
03
3
-3

```

# 2[Task 2] Simple Hello World
```
C:\Users\shuna\Downloads>javap -v -p Main.class
Classfile /C:/Users/shuna/Downloads/Main.class
  Last modified 2020/05/21; size 438 bytes
  MD5 checksum ac137f1b1f296b8ad0d9b1710faa7c42
  Compiled from "SecretSourceFile.java"
class Main
  minor version: 0
  major version: 52
  flags: ACC_SUPER
Constant pool:
   #1 = Methodref          #6.#15         // java/lang/Object."<init>":()V
   #2 = Fieldref           #16.#17        // java/lang/System.out:Ljava/io/PrintStream;
   #3 = String             #18            // Hello World
   #4 = Methodref          #19.#20        // java/io/PrintStream.println:(Ljava/lang/String;)V
   #5 = Class              #21            // Main
   #6 = Class              #22            // java/lang/Object
   #7 = Utf8               <init>
   #8 = Utf8               ()V
   #9 = Utf8               Code
  #10 = Utf8               LineNumberTable
  #11 = Utf8               main
  #12 = Utf8               ([Ljava/lang/String;)V
  #13 = Utf8               SourceFile
  #14 = Utf8               SecretSourceFile.java
  #15 = NameAndType        #7:#8          // "<init>":()V
  #16 = Class              #23            // java/lang/System
  #17 = NameAndType        #24:#25        // out:Ljava/io/PrintStream;
  #18 = Utf8               Hello World
  #19 = Class              #26            // java/io/PrintStream
  #20 = NameAndType        #27:#28        // println:(Ljava/lang/String;)V
  #21 = Utf8               Main
  #22 = Utf8               java/lang/Object
  #23 = Utf8               java/lang/System
  #24 = Utf8               out
  #25 = Utf8               Ljava/io/PrintStream;
  #26 = Utf8               java/io/PrintStream
  #27 = Utf8               println
  #28 = Utf8               (Ljava/lang/String;)V
{
  Main();
    descriptor: ()V
    flags:
    Code:
      stack=1, locals=1, args_size=1
         0: aload_0
         1: invokespecial #1                  // Method java/lang/Object."<init>":()V
         4: return
      LineNumberTable:
        line 3: 0

  public static void main(java.lang.String[]);
    descriptor: ([Ljava/lang/String;)V
    flags: ACC_PUBLIC, ACC_STATIC
    Code:
      stack=2, locals=2, args_size=1
         0: iconst_0
         1: istore_1
         2: getstatic     #2                  // Field java/lang/System.out:Ljava/io/PrintStream;
         5: ldc           #3                  // String Hello World
         7: invokevirtual #4                  // Method java/io/PrintStream.println:(Ljava/lang/String;)V
        10: iinc          1, 2
        13: return
      LineNumberTable:
        line 5: 0
        line 6: 2
        line 7: 10
        line 8: 13
}
SourceFile: "SecretSourceFile.java"
```


# [Task 3] Cracking a password protected application
```
C:\Users\shuna\Downloads>javap -v -p PasswordProtectedApplication.class
Classfile /C:/Users/shuna/Downloads/PasswordProtectedApplication.class
  Last modified 2020/05/21; size 735 bytes
  MD5 checksum 5ad7ff92fa2461a0ae59cfcd6c85d8d7
  Compiled from "PasswordProtectedApplication.java"
public class PasswordProtectedApplication
  minor version: 0
  major version: 52
  flags: ACC_PUBLIC, ACC_SUPER
Constant pool:
   #1 = Methodref          #10.#21        // java/lang/Object."<init>":()V
   #2 = String             #22            // yxvF2ho95ANJVCX
   #3 = Methodref          #23.#24        // java/lang/String.equals:(Ljava/lang/Object;)Z
   #4 = Fieldref           #25.#26        // java/lang/System.out:Ljava/io/PrintStream;
   #5 = String             #27            // You guessed the correct password
   #6 = Methodref          #28.#29        // java/io/PrintStream.println:(Ljava/lang/String;)V
   #7 = String             #30            // You guessed the wrong password
   #8 = String             #31            // Please supply a password
   #9 = Class              #32            // PasswordProtectedApplication
  #10 = Class              #33            // java/lang/Object
  #11 = Utf8               <init>
  #12 = Utf8               ()V
  #13 = Utf8               Code
  #14 = Utf8               LineNumberTable
  #15 = Utf8               main
  #16 = Utf8               ([Ljava/lang/String;)V
  #17 = Utf8               StackMapTable
  #18 = Class              #34            // java/lang/String
  #19 = Utf8               SourceFile
  #20 = Utf8               PasswordProtectedApplication.java
  #21 = NameAndType        #11:#12        // "<init>":()V
  #22 = Utf8               yxvF2ho95ANJVCX
  #23 = Class              #34            // java/lang/String
  #24 = NameAndType        #35:#36        // equals:(Ljava/lang/Object;)Z
  #25 = Class              #37            // java/lang/System
  #26 = NameAndType        #38:#39        // out:Ljava/io/PrintStream;
  #27 = Utf8               You guessed the correct password
  #28 = Class              #40            // java/io/PrintStream
  #29 = NameAndType        #41:#42        // println:(Ljava/lang/String;)V
  #30 = Utf8               You guessed the wrong password
  #31 = Utf8               Please supply a password
  #32 = Utf8               PasswordProtectedApplication
  #33 = Utf8               java/lang/Object
  #34 = Utf8               java/lang/String
  #35 = Utf8               equals
  #36 = Utf8               (Ljava/lang/Object;)Z
  #37 = Utf8               java/lang/System
  #38 = Utf8               out
  #39 = Utf8               Ljava/io/PrintStream;
  #40 = Utf8               java/io/PrintStream
  #41 = Utf8               println
  #42 = Utf8               (Ljava/lang/String;)V
{
  public PasswordProtectedApplication();
    descriptor: ()V
    flags: ACC_PUBLIC
    Code:
      stack=1, locals=1, args_size=1
         0: aload_0
         1: invokespecial #1                  // Method java/lang/Object."<init>":()V
         4: return
      LineNumberTable:
        line 1: 0

  public static void main(java.lang.String[]);
    descriptor: ([Ljava/lang/String;)V
    flags: ACC_PUBLIC, ACC_STATIC
    Code:
      stack=2, locals=2, args_size=1
         0: aload_0
         1: arraylength
         2: iconst_1
         3: if_icmplt     37
         6: aload_0
         7: iconst_0
         8: aaload
         9: astore_1
        10: aload_1
        11: ldc           #2                  // String yxvF2ho95ANJVCX
        13: invokevirtual #3                  // Method java/lang/String.equals:(Ljava/lang/Object;)Z
        16: ifeq          28
        19: getstatic     #4                  // Field java/lang/System.out:Ljava/io/PrintStream;
        22: ldc           #5                  // String You guessed the correct password
        24: invokevirtual #6                  // Method java/io/PrintStream.println:(Ljava/lang/String;)V
        27: return
        28: getstatic     #4                  // Field java/lang/System.out:Ljava/io/PrintStream;
        31: ldc           #7                  // String You guessed the wrong password
        33: invokevirtual #6                  // Method java/io/PrintStream.println:(Ljava/lang/String;)V
        36: return
        37: getstatic     #4                  // Field java/lang/System.out:Ljava/io/PrintStream;
        40: ldc           #8                  // String Please supply a password
        42: invokevirtual #6                  // Method java/io/PrintStream.println:(Ljava/lang/String;)V
        45: return
      LineNumberTable:
        line 3: 0
        line 4: 6
        line 6: 10
        line 7: 19
        line 8: 27
        line 10: 28
        line 11: 36
        line 14: 37
        line 15: 45
      StackMapTable: number_of_entries = 2
        frame_type = 252 /* append */
          offset_delta = 28
          locals = [ class java/lang/String ]
        frame_type = 250 /* chop */
          offset_delta = 8
}
SourceFile: "PasswordProtectedApplication.java"

C:\Users\shuna\Downloads>

```
