;; -*- mode: lisp -*-
========================================================================
========================================================================

                        ======================
                        |The Order of Symbols|
                        ======================

          "...there once existed a language which perfectly
              and unambiguously expressed the essence of
                 all possible things and concepts..."

                       -- Umberto Eco [6TSFTPL]

        "Most good programmers do programming not because they
          expect to get paid or get adulation by the public,
                  but because it is fun to program."

                          -- Linus Torvalds

            "Computers are good at following instructions,
                    but not at reading your mind."

                       -- Donald Knuth [7TAOCP]

========================================================================
========================================================================

Introduction
------------

Lisp as a computer programming language is as Latin is to English or
modern day Italian.  It is the second oldest high level computer
language still in use, invented (or found) in the 1950's by John
McCarthy and is the most powerful and expressive programming language
there is [citation needed].  Lisp comes in many shapes and forms and
Sigil, the Lisp used in Eturia, is no different.  It is a 'dialect' of
Lisp, as Lisp is more of an idea than a concrete thing, with all
dialects looking similar, but behaving, sometimes, very differently.
And like any dialect of a language, it is malleable and modifiable,
something which I will show you though this document we build our
language from base principals (axioms, here known as builtins).

The following is meant to be both an introduction and reference to
Sigil.  You will find an explanation of syntax, followed by a brief
explanation of Eturia, the Listener and Window Manager, followed by
the list of builtins, and then a set of examples that can be followed
along and typed into the Eturia Listener, which can be found at:

http://home.busfactor1.ca/bin/eturia/client/dev.html

This paper is intended to follow the ideas of Guy Steele in his
talk/paper 'Growing a language':

https://www.cs.virginia.edu/~evans/cs655/readings/steele.pdf
https://www.youtube.com/watch?v=_ahvzDzKdB0

All terms in the following text are (hopefully) defined before use.

This material is the result of many years of study and research, of
both myself and others.  It's opinions are all mine, built upon
those I have admired in the past, knowingly or unknowingly. I hope
you find the material as useful and entertaining as I have writing it
down and preparing it.

Burton Samograd <burton.samograd@gmail.com>
Homepage: http://home.busfactor1.ca
Facebook: https://www.facebook.com/burton.samograd
Twitter:  https://twitter.com/kruhft (@kruhft)

Intended Audience
-----------------

This work is intended for both beginners and professionals alike.  For
beginners, if they work through the exercises, should gain an
understanding for all of the code and exercises given, with a little
thought.  Professionals may benefit in the same way, finding the
material refreshing over the typical code chaos one might see at work,
while learning something new and, hopefully, interesting: programming
language design and implementation.

The main desire of the reader should be to learn to program.  This is
not a traditional programming course in any way and will teach you
little on how to get a job as a programmer.  But knowing what this
course will teach you will benefit you for as long as you act as a
programmer during your life [citation needed].

This course assumes a basic understanding of arithmetic and algebra,
along with the idea that a computer is something that simply follows
the instructions that they are told, nothing more.  As Picasso
noted, "Computers...they can only give you answers."


Eturia
------

Eturia is a (simulated) computer for Computer Science Education.  It
is designed to be simple and limited, perfect for teaching and
learning with few distractions.  Although probably unfamiliar at
first, it's spartan interface can be quickly learned by any newcomer
with its few and simple commands. Finally, it runs in a Web browser,
so it is accessable from any location with an internet connection.

The current version of Eturia can always be found at:

    http://home.busfactor1.ca/bin/eturia

along with videos and other information about the project.


The Listener
------------

There is no copy/pasting in Eturia.  To enter the code, it must be
typed manually into the 'Listener'.  This way the code will go through
your fingers and your brain, giving you a better chance of learning
the concepts as you go along and build your own language in Sigil.

This 'Listener' is like VI, but a bit different[1]:

i - insert mode, allows you to overwrite text in the buffer
? - command mode, allows you to execute the following commands
    and break out of insert mode
hjkl - move the cursor left, down, up, or right (h,j,k,l)
e - evaluate lisp code
z - clear the screen
np - previous/next in history (experimental)

To type characters use 'insert' (overwrite) mode by pressing 'i'. You
can tell when you are in 'insert' mode by the GREEN border around the
console.  To 'escape' out of insert mode, press '?'.

REMEMBER TO CLICK IN THE WINDOW TITLE BEFORE TRYING TO TYPE IN THE
LISTENER.

[1] VI and Emacs are programmers text editors.  There has been a
decades long debate over the merits and benfits of using each.  Emacs
is a modern day Lisp Machine, VI is akin to a Unix machine.  I chose a
VI-like editor interface for Eturia due to the simplicity of
implementing it.

Window Manager
--------------

The window manager is responsible for drawing the outline of the
windows in the Eturia system.  There are 3 main functions:

    1. left click in title bar to focus window

    2. click and drag in title bar to move window

    3. middle click in title bar to delete the window

======
Syntax
======

The following is the syntax of Sigil.  Examples with a => are mean to
be typed into the Listener, for example:

```lisp
    (+ 1 1) => 2
```

The above example can be evaulated using the following technique in
the Listener:

    1. Click the 'Listener' title bar.

    2. Type the letter 'i' to enter insert mode.

    3. Type (+ 1 1) normally.

    4. Hit the question mark key '?' to enter command mode.

    5. Type the letter 'e' to evaulate the buffer.

After this you will find the result '2' in a green entry below the
listener console.  I urge you to go through all of the examples and
type them in in this way.  Precision and correctness are key, not
speed, which comes with time and practice.

Comments - notes to your future self
------------------------------------

Comments are important in programs as they are used to explain the
purpose of the code you are writing.  Especially difficult code is
even more difficult to understand after time. Comments are specified
using the semicolon character ';' and continue to the end of the line.

Examples:

```lisp
> ; this is an example comment

> (+ 1 1)	; add 1 and 1
2
```

Numbers - a string of digits
----------------------------

Numbers are strings of digits with an optional period '.' or
negative sign '-'.

Examples:

```lisp
> 1		; is a number
1

> 100	; is a number
100

> 3.141516	; is a number
> -3	; is a number
```

Symbol - a string of characters
-------------------------------

A symbol is a string of characters not containing '(', or ')'.
Symbols with spaces can be enclosed in the pipe '|' symbol for
enclosing the characters.

Examples:

```lisp
    > `x ; is a symbol
    x

    > `abc ; is a symbol
    abc

    > `x123 ; is a symbol
    x123

    > `123x ; is a symbol
    123x

    > `a-longer-symbol ; is a symbol
    a-longer-symbol

    > `|a symbol with spaces| ; is a symbol
    a symbol with spaces
```

You may be wondering what the backtick '`' is doing there.  Read on.

NOTE: SYMBOLS AND NUMBERS ARE ALSO KNOWN AS ATOMS.


Quoting - stops evaluation
--------------------------

Evaluation means to 'get the value of something'.  Sometimes you want
this to not happen and just get 'something'.  Quoting is used for that
and is an essential part of the following examples.

Examples:

```lisp
    > 1 			; The value of the number 1 is 1[1]
    1

    > `1			; the number symbol 1
    1

    > x  			; Error, undefined symbol

    > `x			; the symbol x
    x

    > (1 2 3)    		; Error, undefined function: 1[2]

    > `(1 2 3)			; the list (1 2 3)
    (1 2 3)
```

[1] This is known as being self-evaulating, or something that
evaluates to itself.  Numbers and Strings are of this type.

[2] The result of evuating an unquoted list is such that the first
element of the list is called as a function applied to the rest of the
arguments.  But let's not get ahead of ourselves here.

NOTE: many Lisps have 2 types of quotes, the regular using ' and
another using `.  This has been discarded in Sigil and there is only
one type of quote, the backtick.


List - build lists
------------------

Besides 'atoms' (numbers and symbols), Sigil also has 'lists'.  A list
is a collection of atoms or other lists, also known as an
'S-expression' (Symbolic Expression) for historical reasons.

Examples:

```lisp
> `()		; the empty list
()

> `(1)		; a 'proper' list containing the digit 1
(1)

> `(1 . ())	; a 'proper' list containing the digit 1
(1)

> `(1 2 3)	; is a 'proper' list of the digits 1 2 3
(1 2 3)

> `(1 2 3 . ()) ; is a 'proper' list of the digits 1 2 3
(1  2 3)

> `(1 . 2)	; is an 'improper' list of the digits 1 and 2
(1 . 2)

> `(x . y)	; is an 'improper' list of the symbols x and y
(X . Y)

> `(1 2 . (3 . (4 . ())))
(1 2 3 4)
```

A proper list has the empty list () as its last element, which is not
normally shown.  An improper list does not have () as it's last
element, and this is shown by preceeding the last element with a period.

NOTE: you will being to soon notice almost all of the code we enter
into the Listener will be lists, but for atoms. This is an important
language concept known as homocinicity, which is the ability for a
programs internal structure to be interpreted by it's program
text. The lists used as programs in Sigil are actaully lists
internally and Sigil is a language about building and generating
lists, a powerful combination, as you will see.


Comma ',' - evaluate inside of a quote
--------------------------------------

Oten you want to build a quoted a list, but also want to include the
values of other symbols inside of it.  To perform this action, you use
the comma operator inside of a quoted list.

Examples:

```lisp
> (set `x 1)	; give x a value of 1
1

> x		; check the value of x
1

> `(x 2 3)	; build a quoted list using x
(x 2 3)

> `(,x 2 3)	; build a quoted list with the *value of* x
(1 2 3)
```

Commaat ',@' - evaluate a list inside of a quote, and splice it
----------------------------------------------------------------

Other times when building code, you want to embed the contents of a
list inside of a quoted list.  This is done with the commaat (,@)
operator inside of a quoted list.

Examples:

```lisp
> (set `x `(a b c))	; give x a list value
(a b c)

> x			; check the value of x
(a b c)

> `(x 1 2 3)		; build a list using the symbol x
(x 1 2 3)

> `(,x 1 2 3)		; build a list with evaluated x at the head
((a b c) 1 2 3)

> `(,@x 1 2 3)		; build a list with spliced x at the head
(a b c 1 2 3)

> `(1 2 3 ,x)		; build a list with evaluated x at the tail
(1 2 3 (a b c))

> `(1 2 3 ,@x)		; build a list with spliced x at the tail
(1 2 3 a b c)

> `(1 2 3 . ,@x)	; error, no splicing after a dot
```

Booleans
--------

    () is false, everything else is true

As in most languages, Sigil has the idea of booleans, true and false.
In this case, the empty list, () is 'false' and everything else is
'true'.  A special symbol 't' is defined to represent truth when
needed, but is not required to be used.

Functions that are meant to return either a true or false value are
known as 'predicates'.

Builtins
========

The following are the builtin commands for Sigil.  A builtin is a
function that is available by default in the language and is always
available.

0) quote, unquote, unquote-splice - control evaluation
------------------------------------------------------

Rather than use the shorthands described above, you can also call
'quote', 'unquote' and 'unquote-splice' directly to build lists and
control evaluation within a quoted list.

Examples:

```lisp
> 1				 ; 'give me the value of' 1
1

> (quote 1)			 ; 'give me the symbol' 1
1

> x				 ; 'give me the value of' x, error, as x has no value


> (quote x)			 ; 'give me the symbol' x
x

> (quote (1 2 3))		 ; give me the list of digits 1, 2 and 3
(1 2 3) 

> ;; longhand evaluation with ',' and splicing with ',@'

> (set (quote x) 1)		 ; give x the value 1
1

> (quote ((unquote x) 2 3)	 ; evaluate inside of quoted list as with ','
(1 2 3) 

> (quote ((unquote-splice x) 2 3) ; error, cannot unquote-splice a non-list

> (set (quote x) (quote (1 2 3))) ; give x a value that is a list (1 2 3) 

> (quote ((quote x) 2 3))	 ; unquote x with as with ','
((1 2 3) 2 3)

> (quote ((unquote-splice x) 2 3)) ; splice the list as with ',@'
(1 2 3 2 3) 
```

Normally you would use the shorthands but somtimes using the symbols
will come in handy.


1) atom - a predicate to test if its argument is an atom
--------------------------------------------------------

Everything in Sigil is either an atom (symbol, number, or ()) or a
list.

Examples:

```lisp
> (atom t)		; t is an atome
t

> (atom ())		; () is an atom
t

> (atom `x)		; x is an atom
t

> (atom 1)		; 1 is an atom
t

> (atom `(1 2 3))	; (1 2 3) is not an atom
()
```

2) eq - equality
----------------

Atoms can be tested for equality using 'eq'.

Examples:

```lisp
> (eq t t)			; t is eq to t
t

> (eq () ())			; () is eq to ()
t

> (eq t ())			; t is not eq to ()
(

> (eq `x `x)			; x is eq to x
t

> (eq `x `y)			; x is not eq to y
(

> (eq 1 1)			; 1 is eq to 1
t

> (eq 1 2)			; 1 is not eq to 2
()

> (eq `(1 2 3) `(1 2 3))	; notice! not eq. see 'equal', below.
()
```

3) cons - create a new list cell
--------------------------------

A cons cell is a 2 element cell that has a head slot and an a tail
slot.  The 'cons' function allocates one of these cells and assigns
the first argument to the head slot and the second argument to the
tail slot.

Examples:

```lisp
> (cons 1 ())		; build a proper list with () at the tail
(1) 

> (cons `x ())		; build another proper list
(x) 

> (cons () ())		; again, but with () at the head
(()) 

> (cons `x `y)		; notice! an improper list
(x . y) 

> (cons 1 2)		; and again
(1 . 2) 

> (cons (1 (cons 2 ()))) ; making a proper list with () at the tail
(1 2) 

```


4) car - return the first element of a list
-------------------------------------------

Take a list and return the head slot of its first cell.

Examples:

```lisp
> (car `(1 2 3)) 
1

> (car `((1 2 3) 2 3))
(1 2 3) 

> (car ())		; the head of () is ()
()

> (car `x)		; Error, not a list

> (car 1)		; Error, not a list

```


5) cdr - return everything but the first element of a list
----------------------------------------------------------

Return the 'rest' of the list, besides the head element.

Examples:

```lisp
> (cdr `(1 2 3))
(2 3)

> (cdr `((1 2 3) 2 3))
(2 3)

> (cdr ())
()

> (cdr `x)		; Error, not a list

> (cdr 1)		; Error, not a list

```

6) set - assign a symbol a value (variables)
--------------------------------------------

Values can be stored in symbols using the set builtin, creating a
named shortcut for the value known as a variable. 'set' can be used
to create or change the values of symbols in the variable namespace.

Examples:

```lisp
> (set `x 1)		; set single values
1 

> x
1

> (set `x 2)
2

> x
2

> (set `x `(1 2 3))
(1 2 3)

> x
(1 2 3)

> (set `x 1 `y 2 `z 3)	; set multiple values at once
3 

> x
1

> y
2

> z
3

```


6) cond - conditional statement
-------------------------------

Cond is used to make decisions on what statements to execute.  It goes
through it's arguments, executing each test, until one of them returns
true (not ()), after which it then executes the statements following
the test and returns the value of the last one.  You will often set
't' as the last test in a cond, meaning to always execute that set of
statements if none of the previous tests pass.

Examples:

```lisp
> (cond (t 1))
1

> (cond (() 1))
()

> (cond ((t 1) (t 2)))
1

> (cond ((() 1) (t 2)))
2

> (cond ((() 1) (() 2) (t 3)))
3

> (cond ((() 1) (t 2) (t 3)))
2

> (set `x ())
()

> (set `y t)
t

> (cond
      (x `wont-get-here)	; x is ()
      (y `will-get-here)	; y is t, so will run this branch
      (t `wont-get-here))	; didn't get to default as there was a match above
will-get-here
```


8) lambda - create a function
-----------------------------

A function is a set of bound variables and a series of statements,
known as the body, that can be 'called', which assigns values to the
variables and executes the statements of the body sequentially, until
the value of the last evaluated expression is returned.

Examples:

```lisp
> (lambda (x) x)			; declare a function that returns its argument
(lambda (x) x)

> ((lambda (x) x) 1)			; call the function immediately, passing x = 1
1 

> (set `x 1)
1

> ((lambda (x) (+ x x)) 2)		; x is bound to 2 during the call
4 

> x					; the value of x was not changed by calling the function
1 

> ((lambda (y) (set `x y)) 2)		; set x in the function
2

> x					; the value of x is still unchanged
1 

> ((lambda (x y) (* x y)) 2 3)		; x is bound to 2, y is bound to 3
6

> (set `double (lambda (x) (+ x x)))	; give the functioan a name


> (double 2)				; call the named function
4 

```

We use the keyword 'lambda' to declare functions because of Lisp's
close ties to what is known as the "Lambda Calculus", discovered by
Alonzo Church in the 1930's.


9) alambda - create an anonymous, recursive function
----------------------------------------------------

Exactly the same as to lambda, but binds the variable named by 'self'
to the defined function in its body, allowing for anonymous recursion.
The 'a' in 'alambda' stands for 'anamorphic', a topic which is
discussed later in this book.

    "To iterate is human, to recurse divine."

        -- L. Peter Deutsch

Recursion is a fundamental concept used for looping, or doing
something more than once in Sigil.  To count the number of elements in
a list, one can break the problem into counting the first element of
the list, which is always 1, and adding that to the number of elements
in the rest of the list.  This can be done in a function by calling
itself, or recursing, with the rest of the list until the empty list
is found, meaning we are done and can return the computed length by
adding all of the 1's together.

Examples:

```lisp
> ((alambda self (l n) ; return the length of a list, recursively
   (cond
     ((cdr l)  ; if there are still elements in the list
      (self (cdr l) (+ 1 n))) ; recurse with the tail of the list,
                              ; and increment accumulator
     (t ; there are no elements left in the list
      n))) ; return accumulator
  `(a b c) 0)
3 

> ((alambda self (l) ; return the last element of the list, recursively
   (cond
     ((null (cdr l)) ; if the next element is ()
      (car l)) ; return the head of the list
     (t ; the next element is not ()
       (self (cdr l))))) ; recurse down the list
 `(1 2 3))
3
```

Recursion may be confusing at first, but don't get frustrated.  It is
highly recommended you take the time to follow through the above
examples so you can gain a solid understanding of recursion and how it
works.


10) apply - call a function with a list of arguments
----------------------------------------------------

Sometimes you want to call a function with a prepared list of
arguments, having the contents of the list bound to each of the
arguments of the function.  The reason for this will become more
apparent later as we work through the examples and projects.

Examples:

```lisp
> (apply (lambda (x) (+ x x)) `(1))
2

> (apply (lambda (x y z) (+ x y z)) `(1 2 3))
6

> (apply double `(2))		; using previously defined function in 9)
4 

```

11) values - return multiple values from a function
---------------------------------------------------


Normally functions can return a single value, but Sigil allows you to
return as many values as needed.  Notice how the multiple values are
printed after evaluating a function returning them in the listener.

Examples:

```lisp
> (values 1)
1

> (values 1 2) 
1
2

> ((lambda (x) (values x)) 1)
1

> ((lambda (x y) (values x y)) 1 2)
1
2
```

See 'bind' next, to learn what they can be used for.


12) bind - bind multiple values to symbols
------------------------------------------

When a function returns multiple value, you can 'bind' the returned
values to variables and execute the statements in the body using these
bindings.

Examples:

```lisp
> (set `multiple-values			; a function returning multiple values
       (lambda (x y) (values x y))) 
...


> (bind (a b) (multiple-values 1 2)	; bind the return values to a and b
    (cons a b))
(1 . 2)
```

13) define-macro - define a macro
---------------------------------

FIXME: TODO:

Macros are functions that return code that is executed immediately
after.  This is in contrary to regular functions that can return
anything. Using macros we can build the our language from the
primitives described in this section.

Macros are a powerful tool that give Lisp it's power and are the
reason for its form.  There are many examples that follow that use
define-macro, so study them carefully to understand it's use.


14) + - addition, sum
---------------------

Mathematical addition, or sum with more than 2 arguments.  Also used
to concatenate symbols.

Examples:

```lisp
> (+ 1 2)		; arithmetical addition of numbers
3 

> (+ 1 2 3)		; sum of multiple numbers
6 

> (+ `x `y)		; concatenation of symbols
xy 

```

15) - - subtraction, difference
-------------------------------

Mathematical subtraction, or difference with more than 2 arguments.

```lisp
> (- 1 2)		; arithmetical subtraction
-1 

> (- 1 2 3)		; difference of multiple numbers
-4 

```

16) * - multiply, product
-------------------------

Mathematical multiply, or product with more than 2 arguments.

```lisp
> (* 1 2)		; arithmetical multiplication
2 

> (* 1 2 3)		; product of multiple numbers
6 

```

17) / - divide, quotient
------------------------

Mathematical divide, or quotient with more than 2 arguments.

Examples: 

```lisp
> (/ 1 2)		; arithmetical division
.5 

> (/ 1 2 3)		; quotient of multiple numbers
0.1666... 

```

18) % - remainder, mod
----------------------

Mathematical remainder, or 'mod'.

Examples:

```lisp
> (% 5 2)		; 1 is the remainder of dividing 5 by 2
1 

```

19) env - return the current environment

Variables are defined in the 'variable namespace'.  env is used to
return this namespace for inspection and modification.  If env is
called with an argument, it will set the current 'variable namespace'
to the argument given.

Examples:

```lisp
> (env)		; return the current environment
((t . t) ...) 

> (env (env))		; set the current environment
... 

```

20) fenv - return the current function environment

Functions are defined in the 'function namespace'.  fenv is used to
return this namespace for inspection and modification.  If fenv is
called with an argument, it will set the current 'variable namespace'
to the argument given.

Examples:

```lisp
> (fenv) 
((set . builtin) (cons . builtin) ...)

> (fenv (fenv))		; set the current function environment
... 

```

21) save - save the current environments
----------------------------------------

The environment where you store your variables and macros can be saved
to local storage in your browser using the 'save' command.

```lisp
(save)		; default /core is saved


(save /backup)		; saved to /backup in local storage

```

22) load - load a core into the current environment

The environment can be loaded from local storage using the 'load' command.

THIS FEATURE IS CURRENTLY NOT IMPLEMENTED.


23) me - macro expand
---------------------

Expand macros in the code given as an argument.  Helpful for
debugging.

Examples:

```lisp
> (define-macro cadr (l) `(car (cdr ,l)) ; define the macro cadr

> (me (cadr `(1 2 3)))		; expand it
(car (cdr `(1 2 3))) 
```

24) eval - evaluate an expression
---------------------------------

Sometimes you have a code in a form that you wish to evaluate.  You
can do this by calling eval.

Examples:

```lisp
> `(+ 1 2)		; unevaluated code
(+ 1 2) 

> (eval `(+ 1 2))	; calling eval on it gives the result
3 

```

25) => - evaluate JavaScript code
---------------------------------

Used to execute JavaScript code that can be built by concatenating symbols.

Examples:

``lisp
> (=> |1 + 1|)
2

> (=> |console.log("Testing")|) ; prints Testing in the JavaScript console

```

This builtin allows for the interaction between Sigil and the
underlying web browser. It is an advanced operation that will be used
to build Eturia as a Lisp Machine from within Sigil itself.  Eturia is
written in JavaScript, but the goal of the system is to modify the
JavaScript code as little as possible from outside of it.

26) split - split an atom
-------------------------

Used to break a symbol atom into a list of symbol pieces.  Takes an
optional argument that specifies where to perform the split in the atom.

Examples:

```lisp
> (split `a-long-atom)		; default: '-'
(a long atom) 

> (split `a/long/atom `/)		; specify: '/'
(a long atom) 

```

HERE

========================================================================
========================================================================

                           ================
                           |Basic Training|
                           ================


             "...an individual's thoughts and actions are
                    determined by the language..."

                    -- The Sapir-Whorf Hypothesis
   
            "Lisp is a programmable programming language."

                           -- John Foderaro

                  "Talk is cheap. Show me the code."

                          -- Linus Torvalds


========================================================================
========================================================================


The following exercises build upon the primitive builtins defined
previously and are meant to be typed into the Eturia 'Listener'
console.  The 'Examples' can be used as test cases to ensure the
correctness of your inputs.

0) first, second, third, rest, ... - shortcuts
----------------------------------------------

These first code examples show the most basic of macro, the shortcut.

(define-macro first (x)
  `(car ,x))

(define-macro second (x)
  `(car (cdr ,x)))

(define-macro third (x)
  `(car (cdr (cdr ,x))))

(define-macro rest (x)
  `(cdr ,x))

(define-macro caar (x)
  `(car (car ,x)))

(define-macro cadr (x) ; same a second
  `(car (cdr ,x)))

(define-macro cdar (x)
  `(cdr (car ,x)))

(define-macro cddr (x)
  `(cdr (cdr ,x)))

As you can see, the above macros return non-evaluated 'code'.  This
'code' is then executed immediately after the macro is called with
arguments, as the following examples show.

Examples:

    (first `(1 2 3)) => 1 ; expands to (car `(1 2 3))
    (me (first `(1 2 3))) => (car `(1 2 3))
    (second `(1 2 3)) => 2 ; expands to (car (cdr `(1 2 3)))
    (me (second `(1 2 3))) => (car (cdr `(1 2 3)))
    (third `(1 2 3)) => 3 ; expands to (car (cdr (cdr `(1 2 3))))
    (me (third `(1 2 3))) => (car (cdr (cdr `(1 2 3))))
    (rest `(1 2 3)) => (2 3) ; expands to (cdr `(1 2 3))
    (me (rest `(1 2 3))) => (cdr `(1 2 3))
    (caar `((1 2 3) 2 3)) => 1
    (cdar `((1 2 3) 2 3)) => (2 3)
    (cadr `(1 (1 2 3) 2 3)) => (1 2 3)
    (cddr `(1 2 3)) => (3)
    
The final 4 shortcuts above show how the names 'car' and 'cdr' can be
combined into terse, longer combinations to allow for selection into
more complex list structures.

Spend some time to fully understand what is happening here when these
macros are defined and run.

Exercise: write 'fourth', and 'fifth'.

    (fourth `(1 2 3 4 5 6)) => 4
    (fifth `(1 2 3 4 5 6)) => 5


1) if - tradional conditional
-----------------------------

cond is a general purpose conditional, but sometimes it can be clearer
to use more a traditional conditional construct known as 'if'.  It
takes a test, evaluates it and if it is true, runs the second
statement, and when not, it runs the second statement.

(define-macro if (test true false)
  `(cond
     (,test ,true) ; check test, evaulate true if not ()
     (t ,false)))  ; else, evaluate false
    
Examples: 

    (if t 1 2) => 1
    (if () 1 2) => 2
    (if (eq t t) 1 2) => 1
    (if (eq t ()) 1 2) => 2


2) when - single branch conditional
-----------------------------------

Sometimes you don't need both branches of an if statement and just
want to perform and action when the test is true.  This is when you
use when.  This macro makes use of &body in the argument list, which
means to take all of the arguments following as a list and bind them
to the variable name following &body in the argument list.

(define-macro when (test &body body)
  `(cond
     (,test ,@body)))

Examples: 

    (when t 1) => 1
    (when () 1) => ()
    (when (eq t t) 1) => 1
    (when (eq t ()) 1) => ()


3) reverse - reverse a list
---------------------------

Reverse a list by building a new list in opposite order using
cons'ing.  Building a list this way is an important idiom to
understand, and thankfully this function is quite simple because the
lists built using cons'ing are in 'reverse' order, that is, items are
added to the front rather than the back of the list.

(define-macro reverse (l)
  `((alambda self (l2 a) ; an anonymous function
      (if l2 ; if l2 is not null
          (self (cdr l2) (cons (car l2) a)) ; recurse
          a)) ; else return a, the accumlator
    ,l ())) ; call the anonymous function immediately

Examples: 

    (reverse `(1 2 3)) => (3 2 1)
    (reverse `((1 2 3) a b c)) => (c b a (1 2 3))

Exercises:

    1. Will reverse work with improper lists?  Why not?


4) map - build a list by running a function over another list
-------------------------------------------------------------

'map' is what is known as a higher order function, that is, one which
takes a function as an argument.  In this case the function given is
'run over' the second argument, a list. The function is called with
every element of the list, and a new list is built using the results.

(define-macro map (f l)
  `((alambda self (l2 a) ; declare an anonymous function
      (if l2 ; if l2 is not null
          (self (cdr l2) (cons (,f (car l2)) a)) ; recurse
          (reverse a))) ; return the acummulator, reversed
    ,l ())) ; call the anonymous function, evaluating l
            ; and passing () for a

Examples:

    (map (lambda (x) (+ x x)) `(1 2 3)) => (2 4 6)
    (map car `((1 a) (2 b) (3 c))) => (1 2 3)
    (map second `((1 a) (2 b) (3 c))) => (a b c)

Exercises:

    1. Write a map statement that takes a list `(1 2 3) and
       returns `(3 6 9).

5) ls - show the current environment
------------------------------------

'env' is a useful function but it's output can be a bit verbose.  'ls'
is a macro that returns you just the variables that are defined in the
environment but not their values, making for less output to that you
have to parse mentally.

(define-macro ls ()
  `(map car (env)))

Examples:

    (ls) => (t nil)
    (set `x 1) => 1
    (ls) => (t nil x)

5) lsf - show the current function environment
----------------------------------------------

Like 'ls', but shows the names of the functions and macros that have
been defined.

(define-macro lsf ()
  `(map car (fenv)))

Examples:

    (lsf) => (atom null ...  ls lsf)
    (define-macro f (x) x) => (macro (x) x)
    (lsf) => (atom null ... lsf f)

6) let - declare local variables
--------------------------------

Often you need to use additional temporary variables when performing a
computation. 'let' can be used to create these temporaries, cleaning
them up after the body of the form is completed, returning the value
of the last executed statement.

(define-macro let (args &body body)
  ((lambda (vars values) ; notice! we are processing the arguments to let
     `((lambda ,vars ,@body) ,@args)) ; notice! this is the code that
                                      ; is returned by let
     (map car args) ; argument 1 above, vars
     (map cadr args))) ; argument 2 above, values

Examples:

    (map car `((a 1) (b 2))) => (a b) ; like vars, above
    (map cadr `((a 1) (b 2))) => (1 2) ; like values, above
    (let ((a 1) (b 2)) (+ a b)) => 3
    a => ; error, undefined symbol
    b => ; error, undefined symbol

7) aif - anamorphic if
----------------------

Since () is always false and anything else is true, sometimes we may
want to know the value that is returned by the test that is passed to
'if'.  This can be done by saving the value in the environment for the
body of the 'if', which we are going to call 'it'.  You can then
reference the value of 'it' anywhere in the body of the 'if' statement.

(define-macro aif (test true false)
  `(let ((it ,test))
     (if it ,true ,false)))

Examples:

    (aif 1 it ()) => 1
    (aif (car `(1 2 3)) it 2) => 1
    (aif (car `(() 2 3)) it 2) => 2

Note: the injection of variables that can be used in the body of a
macro makes the macro 'anamorphic'.  For a further explanation of this
concept, see "On Lisp", chapter 14.

8) awhen - anamorphic when
--------------------------

Like 'aif', but with when.

(define-macro awhen (test &body body)
  `(let ((it ,test))
     (when it ,@body)))

Examples:

    (awhen 1 it) => 1
    (awhen () it) => () ; notice! awhen by default returns ()


9) last - return the last element of a list
-------------------------------------------

Sometimes you want the last element of the list. This function shows
recursing down a list until it reaches the end, when it return the
last element.

(define-macro last (l)
  `((alambda self (l)
      (if (cdr l)
          (self (cdr l))
          (car l))))
  ,l))

Examples:

    (last `(1 2 3)) => 3


10) length - return the length of a list
----------------------------------------

Knowing the length of a list is generally very useful during
computations.  Here is a macro that recursively computes it given a
list using an accumulator.

(define-macro length (l)
  `((alambda self (l n)
      (if l
          (self (cdr l) (+ n 1))
          n))
    ,l 0))

Examples:

    (length ()) => 0
    (length `(1 2 3)) => 3
    (length `((1 2 3) a b c)) => 4


11) nth - return the nth element of a list
------------------------------------------

Although macros like 'first', 'second' and 'third' are useful, you
often want a general purpose way of getting a certain element from a
list.  'nth' is designed to perform that operation, given a list and
an integer.

(define-macro nth (n l)
  `((alambda self (n l)
      (if (eq n 0)
          (car l)
          (self (- n 1) (cdr l)))) ,n ,l))

Examples:

    (nth 0 `(1 2 3)) => 1
    (nth 1 `(1 2 3)) => 2
    (nth 2 `(1 2 3)) => 3


12) not - logical compliment
----------------------------

When using boolean values, sometimes you want the opposite of the
value you have. In this case you use 'not', which returns the
compliment of any value, logically.

(define-macro not (x)
  `((alambda self (v)
      (cond
        ((null v) t) ; check for (), if so, return t
        (t ()))) ; else return () for everything else
    ,x)) ; evaulate the argument x

Examples:

    (not ()) => t
    (not t) => ()
    (not 1) => ()


13) unless - negative single branch conditional
----------------------------------------------

Like when, but the logical opposite. It runs its body of when its test
returns ().

(define-macro unless (test &body body)
  `(cond ((not ,test) ,@body)))

Examples:

    (unless t 1) => ()
    (unless () 1) => 1
    (unless (eq t t) 1) => ()
    (unless (eq t ()) 1) => 1


14) and - logical and
---------------------

'and' is another boolean function, one that returns true when all of
its parameters are true.  Because of this property, if any of the
values that it is passed returns false, you can assume the final value
is false, so you can stop evaluating the arguments and just return
false.  This behaviour is called 'short circuiting' and will be very
useful in the future.

(define-macro and (&rest args)
  `((alambda self (args) ; an anonymous function
      (if args ; if args is not ()
          (if (eval (car args)) ; evaluate the argument
              (self (cdr args)) ; if true, continue with other args
              ()) ; evaluation returned false, so and is false
          t)) ; all evaluated args returned true, so return true
    `,args)) ; call anonymous function with args quoted,
             ; as we are evaluating them individually above

Examples:

    (and () ()) => ()
    (and () t) => ()
    (and t ()) => ()
    (and t t) => t
    (and 1 1) => t
    (and () (set `a 1)) => ()
    a => ; error, undefined variable,
         ; set was not run due to short circuiting

15) or - logicial or
--------------------

Similar to and, or returns true if any of its arguments are true.  We
can also take advantage of this and 'short circuit' on this behaviour
as well.

(define-macro or (&rest args)
  `((alambda self (args)
      (if args
          (aif (eval (car args))
               it
               (self (cdr args)))
          ())) `,args))

Examples:

    (or () ()) => ()
    (or () t) => t
    (or t ()) => t
    (or t t) => t
    (or 1 1) => 1
    (or t (set `a 1)) => t
    a => ; error, undefined variable, 
         ; set was not run due to short circuiting

16) xor - logical exclusive or
------------------------------

Similar to 'and' and 'or', 'xor' returns true if one or the other of
its arguments is true.  You will notice that we are use 'let' to hold
the value of our evaluated arguments.  You generally only want to
evaluate the arguments you are passed once. This is because the
evaluation of certain arguments may cause 'side effects', and
evaluating them more than once may cause unintended consiquences and
should be avoided.

(define-macro xor (x y)
  `(let ((xe ,x) ; evaluate x once
         (ye ,y)) ; evaluate y once
     (and
      (or xe ye)
      (not (and xe ye)))))

Examples:

    (xor () ()) => ()
    (xor t ()) => t
    (xor () t) => t
    (xor t t) => ()

17) list - create a proper list of all arguments
------------------------------------------------

Creating lists with cons can often be tedious, so lets define a macro
to make it easier.  This example shows how to use the underlying lisp
to build the list and evaluate the arguments.

(define-macro list (&rest rest)
  `((lambda (&rest rest)
     rest) ,@rest))

Examples:

    (list `a `b `c) => (a b c)
    (list 1 2 3) => (1 2 3)

18) equal - compare if two things are equal, including lists
------------------------------------------------------------

If you recall from the discussion of 'eq', it does not compare the
equality of lists, just atoms.  The following is a function that does
a 'deep' comparison between 2 items, including lists.  If you want,
you can always use 'equal' instead of 'eq', but 'equal' is slower than
using just 'eq' when you know you are dealing with only atoms.

(define-macro equal (x y)
  `((alambda self (a b) ; anonymous function
      (cond
        ; 2 atoms, test with eq
        ((and (atom a) (atom b)) (eq a b))
        ; both lists null, must be equal
        ((and (null a) (null b)) t)
        ; one list is null, cannot be equal
        ((or (null a) (null b)) ())
        ; one is an atom, the other not, so not equal
        ((or (atom a) (atom b)) ())
        ; if the heads are equal
        ((equal (car a) (car b))
         (self (cdr a) (cdr b)))))
    ; return () if none of the above are true
    ,x ,y)) ; call anonymous function with evaluated arguments

Examples:

    (equal t t) => t
    (equal () ()) => t
    (equal 1 1) => t
    (equal `(1 2 3) `(1 2 3)) => t
    (equal `((1 2 3 (x y z)) a b c) `((1 2 3 (x y z)) a b c)) => t
    (equal `(1 2 3) `(1 2)) => ()
    (define-macro pallindromep (l)
      `(let ((le ,l))
         (equal le (reverse le))))
    (pallindromep `(1 2 3 4)) => ()
    (pallindromep `(1 2 3 4 3 2 1)) => t

19) member - find if something is in a list
-------------------------------------------

Often you want to search a list to see if an item is contained in it.
'member' takes a 'thing', a 'list' and a 'test'.  The 'test', if
omitted, defaults to 'eq', can be any predicate, and normally is given
as 'equals' so that you can search for lists within lists.  The return
value is the contents of the list up to the item found, else () if the
'thing' is not found in the 'list'.

(define-macro member (thing list &rest test)
  `(let ((t (aif ,(car test) it eq)))
     ((alambda self (x l)
        (if l
            (if (t x (car l))
                l
                (self x (cdr l)))
            ()))
      ,thing ,list)))

Examples:

    (member 1 `(1 2 3)) => (1 2 3)
    (member 3 `(1 2 3)) => (3)
    (member 4 `(1 2 3)) => ()
    (member `(1 2 3) `(a b c (1 2 3))) => ()
    (member `(1 2 3) `(a b c (1 2 3)) equal) => ((1 2 3))  


21) filter - remove elements from a list
----------------------------------------

'filter' is like map, in that it is a higher order function.  It takes
a predicate and a list, building a new list by running the predicate
over the list and including the members for which the predicate
returns true.

(define-macro filter (f l)
  `((alambda self (l a)
      (if l
          (if (,f (car l))
              (self (cdr l) (cons (car l) a))
              (self (cdr l) a))
          (reverse a))) ,l ()))

Examples:

    (filter
     (lambda (x) 
       (eq x 1))
     `(1 2 3)) => (1)
    (filter
     (lambda (x)
       (or (eq x 1) (eq x 3)))
     `(1 2 3)) => (1 3)

22) rm - remove a symbol from the environment
---------------------------------------------

(define-macro rm (&rest xs)
  `(env (filter
         (lambda (e)
           (not (member (car e) `,xs))) (env))))

Examples:

    (set `x 1) => 1 ; define a symbol in the environment
    (set `y 2) => 2 
    x => 1
    y => 2
    (rm x y) => ... ; returns new environment
    x => ; Error, undefined symbol
    y => ; Error, undefined symbol

Exercise:

    1. Rewrite 'rm' so that it returns the last value(s) of the
       symbol(s) that was/were deleted. [HARD]


23) rmf - remove a macro from the function environment
------------------------------------------------------

Identical to above, but works with the function environment rather
than the variable environment.

(define-macro rmf (&rest xs)
  `(fenv (filter
          (lambda (e)
            (not (member (car e) `,xs))) (fenv))))

Examples:

    (define-macro double (x) `(+ ,x ,x)) => (macro (x) `(+ ,x ,x))
    (double 2) => 4
    (rmf double) => ...
    (double 2) => ; Error, undefined function


22) dolist - iterate over a list
--------------------------------

Often it is easier to create a shorthand for commonly done operations
to make them both easier to read and to write.  In this case one of
them will be iterating over a list. This macro is also anamorphic, as
it always injects its first variable and sometimes, it's second.

(define-macro dolist (vlr &body body)
  (let ((var (first vlr))
        (list (second vlr))
        (ret (third vlr)))
    `((alambda self (l)
        (when l
          (let ((,var (car l))
                (,(if (atom list) list `it) l))
            ,@body)
          (self (cdr l)))
        ,ret) ,list)))

Examples:

    (let ((r 0))
      (dolist (x `(1 2 3) r)
        (set `r (+ x r)))) => 6
    (set `x `(1 2 3)) => (1 2 3)
    (let ((r ()))
      (dolist (i x)
        (set `r (cons (cons i x) r)))
      r) => ((3 3)) (2 2 3) (1 1 2 3))
    

;; WARNING: THE FOLLOWING CODE IS UNTESTED AND/OR NOT WORKING
            
23) join - rebuild a split atom
-------------------------------

Used when you would like to combine a list of atoms into a single
atom, with an optional delimeter that defaults to '-'.

(define-macro join (atoms &rest delim)
  `((lambda (as d)
      (let ((retval `||))
        (dolist (s as retval)
          (set `retval (+ s (if (cdr as) d `||) retval)))))
    `,(reverse (eval atoms)) ,(or (car delim) `-)))

Examples:

    (join `(a long atom)) => a-long-atom
    (join `(a long atom) `/) => a/long/atom


15) mapn - like map, but takes n lists as arguments
---------------------------------------------------

'mapn' is like 'map', in that it runs a function to create a new list,
but it can take multiple lists, and therefore, functions of multiple
arguments.  'mapn' iterates down the lists in parallel, calling the
function f with the first elements of each of the lists, after which
it recurses with the rest of the lists.  If you only have one list,
'map' is faster to use computationally, although 'mapn' will work with
a single list if needed.

;; Note: this doesn't work yet
(define-macro mapn (f &rest lists)
  `((lambda (xs a)
      (if xs
          (let ((heads (map car xs)))
            (self (cdr xs) (cons (eval `(,f ,@heads) a)))
        (reverse a)))
    `,lists ()))

Examples:

    (mapn (lambda (x y) (+ x y)) `(1 2 3) `(1 2 3)) => (2 4 6)
    (mapn (lambda (x y) (+ x y)) `(x y z) `(a b c) `(1 2 3)) => (xa1 yb2 zc3)

16) setq

(define-macro setq (&rest rest)
  (lambda (vars values)
    `(mapn (lambda (var value)
             (set var value)) ,vars ,values)
    (map car vars)
    (map cadr vars)))

Examples:

    (setq x 1) => 1
    x => 1
    (setq x 2 y 3) => 3
    x => 2
    y => 3

;; TO BE CONTINUED

push - add an element to the head of a list
-------------------------------------------

'push' is used to insert elements onto the head of a list.

(define-macro push (x l)
  `(let ((xe ,x))
     (set xe (cons xe l))))

Examples:

    (set `x `(1 2 3)) => (1 2 3)
    (push 0 x) => (0 1 2 3)
    (push 0 `(1 2 3)) => ; error, list is not a symbol

pop - remove the head of a list
-------------------------------

'pop' is the compliment to 'push' and removes the head of the list
that was (possibly) added last by pop.  With 'push' and 'pop' one can
use a list as a 'stack', or a FIFO (first in first out) queue.

(define-macro pop (l)
  `(let ((le ,l))
     ((lambda (o)
        (set ll (cdr le))
        o) (car le))))

Examples:

    (set `x `(1 2 3)) => (1 2 3)
    (pop x) => 1
    x => (2 3)

shift - add an element to the tail of a list
--------------------------------------------

(define-macro shift (x l)
  `(let ((le ,l))
     (set le (reverse (cons ,x (reverse le))))))

Examples:

    (set `x `(1 2 3)) => (1 2 3)
    (shift 4 x) => (1 2 3 4)

unshift - remove an element from the tail of a list
----------------------------------------------------

(define-macro unshift (l)
  `(let ((le ,l))
     ((lambda (o)
        (set le (cdr (reverse le)))
        o) (car (reverse le)))))

Examples:

(set `x `(1 2 3)) => (1 2 3)
(unshift x) => 3
x => (1 2)

rotate - rotate a list
----------------------

(define-macro rotate (l n))


assoc - associative lookup
--------------------------


flatten - build a list from nested lists
----------------------------------------

sort - sort a list based on a predicate
---------------------------------------

random - generate a random number
---------------------------------

(define-macro random ()
  (=> `|Math.random()|))

;; Interesting alternate implementation but we don't really have
;; integers in Sigil yet TODO: implement integers (big-nums) in Sigil
(set `*rand-max* 32767)
(set `*random-seed* 31337)
(define-macro random (&rest random-seed)
  `(let ((seed ,(or random-seed *random-seed*)))
     (set `*random-seed* (& (/ (+ (* *random-seed* 1103515245) 12345) 65536) *rand-max*))))

replace - replace an element at an index in a list
--------------------------------------------------

(define-macro replace (l n v)
  `((alambda 
     self (l n2 a)
     (if l
         (if (= n2 0)
             (self (cdr l) (- n2 1) (cons value a))
             (self (cdr l) (- n2 1) (cons (car l) a)))
         (reverse a)))))

========================================================================
========================================================================

                              ==========
                              |THE MIDS|
                              ==========

       "Because language is the carrier of ideas, it is easy to
   believe that it should be very little else than such a carrier."

                           -- Louise Bogan

          "Lisp isn't a language, it's a building material."

                              - Alan Kay

========================================================================
========================================================================

=======================
Exercises 0 - TODO List
=======================

THis exercise we will make a helpful utility, a set of functions to
keep track of a TODO list.  It helps to think of the actions we want
to do with a todo list: add items, remove items and prioritize items.

First off, we are going to write a macro that will treat a list as a
stack.  A stack is what's known as a FIFO, or 'First In, First Out'
queue.  Meaning that you 'push' items onto a stack and they return in
the same order as you 'pop' them off.

(define-macro push (x l)
  `(setq ,l (cons ,x ,l)))

Examples:

    (setq x ()) => ()
    (push 1 x) => 1
    x => (1)
    (push 2 x) => 2
    x => (2 1)
    
(define-macro pop (l)
  `((lambda (o)
      (setq ,l (cdr ,l))
      o) ,(car l)))

Examples:

    (set x ()) => ()
    (push `a x) => a
    (push `b x) => b
    (pop x) => b
    (pop x) => a
    (pop x) => ()
    
Now let's define a place to hold our todo list:

    (setq *todo* ())

Having to remember to quote things is sometimes frustrating, so we'll
define a helper macro 'todo' that does it for us:

(define-macro todo (thing)
  (push `,thing *todo*))

Examples:

    (todo finish-this-exercise!)

For the last function 'done', it helps to write a generic helper
function called 'remove', that removes elements from a list at a
certain index:

(define-macro remove (l n)
  `((alambda 
     self (l2 n2 a)
     (if l2
         (if (eq n2 0)
             (self n2 a)
             (self (cdr l2) (- n2 1) (cons (car l2) a)))))
    `,l ,n))

Examples:

    (setq x `(a b c 1 2 3))
    (remove 4 x) => (a b c 1 3)
    x => (a b c 1 2 3) ; x was not changed

Now we can easily write 'done':

(define-macro done (n)
  (setq *todo* (remove *todo* n)))

Examples:

    (todo task-1) => task1
    (todo task-2) => task2
    *todo* => (task2 task1)
    (done 1) => task1
    *todo* => (task2)
    (done 0) => task2
    *todo* => ()

But how about if we want to proritize the items to have one show up
earlier in the list to attract our attention?

(define-macro swap (l m n)
  `(let ((m (if (< m n) m n)) ; sort m and n
         (n (if (< m n) n m)))
     (let ((va (nth l m))
           (vb (nth l n)))
       ((alambda
         self (l2 m2 n2 a)
         (if l2
             (if (= m2 0)
                 (self (cdr l2) (cons vb l2))
                 (if (= n2 0)
                     (self (cdr l2) (cons va l2))
                     (self (cdr l2) (cons l2 a))))
             (reverse a)))))))

(define-macro prioritize (m n)
  `(set *todo* (swap *todo* m n)))

=================================
Exercises 2 - S-Expression Editor
=================================

An interesting aside into building a data structure editor.

==================
Exercises 1 - Life
==================

The classic, and simple, 'game' discovered (or found) by John Conway
in 1970 [WPCGOL].  It simulates a virtual 'world' that follows very
simple mathematical rules to determine which individuals in the world
life, breed and die.  It has been a greatly studied and analyzed game,
and some of the forms that take shape in the world have names such as
'gliders' and 'puffers', showing the rich variety that studiers of the
game can see.

Life is best watched as a graphical game, where you can see the
interactions of the individuals in real time.  Eturia is capable of
that from JavaScript, but we are going to want to do this from Sigil.
This means we need to develop and 'interface' between Sigil and
Eturia.  This will be acommonplished with some inline JavaScript code
using the => builtin.

(setq *terminal* `|notebook.app().terminal().|)

(define-macro terminal-clear-screen ()
  `(=> (+ *terminal* `|clearScreen()|)))

(define-macro terminal-on-character (x y)
  `(=> (+ *terminal* `|onCharacter(| ,x `|,| ,y `|)|)))

(define-macro terminal-off-character (x y)
  `(=> (+ *terminal* `|offCharacter(| ,x `|,| ,y `|)|)))

(define-macro terminal-is-character-on (x y)
  `(=> (+ *terminal* `|isCharacterOn(| ,x `|,| ,y `|)|)))

(define-macro terminal-rows ()
  `(=> (+ *terminal* `|rows()|)))
  
(define-macro terminal-columns ()
  `(=> (+ *terminal* `|cols()|)))

The Life world is going to be held in a grid the size of the console
screen.  The next section is going to define a 'grid' type and some
utility functions for dealing with its data.

;; First, we're going to define a helper function. The data in the
;; grid is going to be represented by a list, each containing a
;; specific value. To make things interesting, we are going to
;; evaluate the value argument each time we add an element to the
;; list; this is because we might be able to do some interesting
;; effects using functions that cause side effects in the future.
(define-macro make-list (length value)
  `((alambda 
     self (n a)
     (if (and (eq n 0))
         a
         (self (- n 1) (cons (list (eval `,value)) a)))))
    ,length ()))

;; Here we make a grid type.  Its internal representation is a list
;; consisting of the empty list as items, of length w * h.
(define-macro make-grid (w h &rest data)
  `(let ((w ,w)
         (h ,h))
     (let ((data (or ,data
                     (make-list (* w h) ()))))
       (list "grid" w h data))))

;; Now, the regular predicate and data utility accessing functions.
(define-macro is-grid (g) 
  `(eq (car ,g) "grid"))

(define-macro grid-width (g)
  `(first (cdr ,g)))

(define-macro grid-height (g)
  `(second (cdr ,g)))

(define-macro grid-data (g)
  `(third (cdr ,g)))

;; Get the value at a grid x, y postiion.
(define-macro grid-get (g x y)
  `(let ((g ,g)
         (x ,x)
         (y ,y))
     (let ((w (grid-width g)))
       (nth (+ x (* w y))  (grid-data g)))))

Now we see another opporunity to factor out some code redundancy.
These macros we are defining above are actually 'functions', in that
they are not doing anything interesting with the evaulation of their
arguments. So we can create a helper macro called 'define-function'
that will take care of evaulating the arguments for us:

(define-macro define-function (name args &body body)
  (let ((argse (map (lambda (arg)
                      (list arg `(eval arg))) `,args)))
    `(define-macro ,name ,args
       (let ,argse
         ,@body))))

Next is the redefining the above two macros that were defined as
functions, using define-function, giving us some more brevity:

(define-function make-grid (w h &rest data)
  (let ((data (or ,data
                  (make-list (* w h) ()))))
    (list "grid" w h data)))

(define-function grid-get (g x y)
  (let ((w (grid-width g)))
    (nth (+ x (* w y))  (grid-data g))))

After all of this practice writing macros, you now should have a very
solid understanding of evaulation and when to evaluate your arguments.
A macro is a special case of a function, where you want control over
argument evaluation, but functions can be written more compactly since
you are letting the computer do a task for you that is a common
pattern.  From now on we will define functions using define-function
and macros with define-macro.

;; Set a grid x, y position with value, returning a new grid with the
;; modifications.
(define-function grid-set (g x y value)
  (let ((i (+ x (* y (grid-width g)))))
    (make-grid (grid-width g) (grid-height g)
               (replace (grid-data data) i value))))

;; Runs the function f, which takes 3 parameters, x, y and value, from
;; left to right, top to bottom over the data contained in the grid.
(define-function grid-map (g f))

====================================
Mathmatical Exercises 2 - Ray Tracer
====================================

A ray tracer is a type of graphic generation program that attempt to
simulate how light actually works when passing through a scene using
individual 'beams' of light, known as rays.  This allows for the
creation of high quality images at the expense of speed, due to the
accuracy of the rendering process.

First, we will define some mathematical utility functions:

(define-macro ^ (x to-the)
  `((alambda self (to-the2 a)
     (if (= to-the2 0)
         a
         (self (- to-the2 1) (* a x))))
    ,x ,to-the))

(define-macro square (x)
  `(^ x 2))

(define-macro square-root (x)
  `(=> (+ `|Math.sqrt(| ,x `|)|)))

(define-macro round (x)
  `(=> (+ `|Math.round| ,x `|)|)))

Next, a 'point structure' will be defined:

(define-macro make-point (x y z) `(list `point ,x ,y ,z))

(define-macro is-point (p) `(eq (car ,p `point)))

(define-macro point-x (p) `(first ,(cdr p)))
(define-macro point-y (p) `(second ,(cdr p)))
(define-macro point-z (p) `(third ,(cdr p)))

And some helpful point structure mathematical utility functions:

(define-macro point-magnitude (p)
  (square-root (+ (square (point-x p))
                  (square (point-y p))
                  (square (point-z p)))))

;; Compute the difference between 2 points, returning as multiple
;; values, dx, dy and dz.
(define-macro point-difference (p1 p2)
  `((lambda ()
      (values
       (- (point-x p2) (point-x p1))
       (- (point-y p2) (point-y p1))
       (- (point-z p2) (point-z p1))))))

;; Find the distance between 2 points
(define-macro point-distance (p1 p2)
  `((lambda ()
      (point-magnitude (point-difference p1 p2)))
    ,p1 ,p2))

;; Return a normalize point, which is one which all of its components
;; have been divided by its magnitude so that all of its components
;; are within the range of 0...1.
(define-macro point-normalize (p)
  `(let ((m (point-magnitude ,p)))
     (make-point (/ (point-x p) m)
                 (/ (point-y p) m)
                 (/ (point-z p) m))))

Now a function helpful with finding roots of equations:

;; A function for comparing 2 numbers to see which is less than the
;; other.
(define-macro < (x y)
  `(=> (+ `|| ,x `|<| ,y)))

;; Some helpful constants.
(define-macro *FLOAT-MAX* (=> `|Math.FLOAT_MAX|))
(define-macro *FLOAT-MIN* (=> `|Math.FLOAT_MIN|))

;; Find the minimum of the arguments.
(define-macro minimum (&rest args) 
  `((alambda
     self (l min)
     (if l
         (aif (< (eval (car l)) min)
              (self (cdr l) it)
              (self (cdr l) min))
         min))
    `,args *FLOAT-MAX*))
                            
;; Find the maximum of the arguments
(define-macro maximum (&rest args) 
  `((alambda
     self (l min)
     (if l
         (aif (> (eval (car l)) min)
              (self (cdr l) it)
              (self (cdr l) min))
         min))
    `,args *FLOAT-MIN*))

One thing you might notice above is the similarity between minimum and
maximum code wise.  When you see this, it is an opportunity to use
another macro to encapulate the similarities between the functions,
and use arguments to fill in the slots for the differences.  The
following is a redefinition of the two above functions using a macro
to factor out and hold the common code between them, after which the
original functions are redefined using the newly created higher order
function.

;; Run predicate over args using init as the initial value
(define-macro accumulate-over-args (predicate init &body args) 
  `((alambda
     self (l a)
     (if l
         (aif (,predicate (eval (car l)) a)
              (self (cdr l) it)
              (self (cdr l) a))
         a))
    `,args ,init))

;; Find the minimum of the args
(define-macro minimum (&rest args)
  `(accumulate-over-args `< *FLOAT-MAX* ,@args))

;; Find the maximum of the args
(define-macro maximum (&rest args)
  `(accumulate-over-args `> *FLOAT-MIN* ,@args))

;; Find the minimum root of the equation defined by a, b and c
(define-macro mininum-root (a b c)
  `((let ((ae ,a)
          (be ,b)
          (ce ,c))
      (if (eq 0 ae)
          (/ (- ac) ab)
          (let ((d (- (square be) (* 4 ae ce))))
            (unless (< d 0)
              (let ((d2 (square-root d)))
                (miniumum (/ (+ (- be) d2) (* 2 ae))
                          (/ (- (- be) d2) (* 2 ae))))))))))

And now for some raytracing functions:

;; Find the pixel color at x, y using the point eye as the source of
;; the rays.
(define-macro raytracer-color-at (eye x y)
  `(let ((eyee ,eye)
         (xe ,x)
         (ye ,y))
     (round (* (raytracer-send-ray eyee
                                   (- xe (point-x eyee))
                                   (- ye (point-y eyee))
                                   (- 0 (point-z eyee)))))))

;; The background color index for the image.
(set `*raytracer-background-color-index* 0)

;; Cast a ray from point through rx, ry and rz, returning a color
;; index if an object is hit, or the background color otherwise.
(define-function raytracer-send-ray (point rx ry rz)
  `(bind (s int) (raytracer-first-hit point rx ry rz)
         (if s
             (* (raytracer-lambert s int xr yr zr)
                (surface-color s))
             *raytracer-background-color-index*)))

;; Find the first object hit by the ray cast from point through xr, yr
;; and zr in the *raytracer-world*.
(define-function raytracer-first-hit (point xr yr zr)
  `(dolist (s *raytracer-world*)
     (let ((h (raytracer-intersect s point rx ry rz)))
       (when a
         (let ((d (point-distance h point)))
           (when (or (null dist) (< d dist))
             (set `surface s `hit h `dist d))))))
  (values surface hit))

(define-function raytracer-lambert (s int xr yr zr)
  (let ((n (raytracer-normal s int)))
    (maximum 0 (+ (* xr (point-x n))
                  (* yr (point-y n))
                  (* zr (point-z n))))))


Now define a sphere type that we can use to fill the world with:


(define-macro make-sphere (radius center-point color-index)
  `(list `sphere ,radius ,center-point ,color-index))

(define-macro sphere-radius (s)
  `(first ,(cdr s)))

(define-macro sphere-center-point (s)
  `(second ,(cdr s)))

(define-macro sphere-color-index (s)
  `(third ,(cdr s)))

(define-macro is-sphere (s)
  `(eq (car ,s) `sphere))

(define-macro define-sphere (r p c)
  `(push (make-sphere ,r ,p ,c) *raytracer-world*))
  

(define-function
    
==========================================
Exercises 4 - GPS (General Problem Solver)
==========================================

The GPS, or General Problem Solver was an early artificial
intelligence program from 1959 [5PAIP, WPGPS].  It is an interesting and
simple program that gave high hopes for early AI researchers, but was
soon found rather limiting in it's 'generality' of problems it could
solve.

GPS is best described by what it does: it takes a start state, a goal
state and a list of rules to change states.  So, for any start goal
state and an appropriate set of rules, one should be able to solve the
path from the start state to the end state using the transformation
rules.  This approach can solve problems like 'getting milk from the
store' to mazes, but falls over on what seem to be some very simple
problems that were found after its discovery [WPSA].

The reason we are implementing this is so we have a general 'search'
function in Eturia.  Like everything we have done before, we are going
to build on what is available in Eturia as much as possible to inprove
the functionality and richness of our future programs to help break
them out of the box.

=======================================
Exercises 5 - A (Simulated) Trading Bot
=======================================

A simulated FOREX market arbitrage trading bot.

Possible other projects:

Debt Repayment Calculator

It's always good to be able to know how long it will be before you can
pay off some of your essential debt, such as your mortgage.

Phrase Generator

Building sentences using data driven design.

Probablistic Primes

Introductory computation on the probabilistics of primality.

========================================================================
========================================================================

                            ==============
                            |THE ADVANCED|
                            ==============

                    "Language disguises thought."

                        -- Ludwig Wittgenstein

========================================================================
========================================================================

=========================================
Exercises 6 - Boolean Propagator Networks
=========================================

This exerecise will be to build a language to compute boolean
functions using what is known as a Propagator Network.  Propagators
were credited to Gerald Jay Sussman and can be read more about in
[2SICP] and [4TAOTP].

What is interesting about propagator networks is that they can compute
bi-directionally.  That is, once you define the network, they are
capable of computing any of their variables when enough information is
applied to the terminals to be able to know them.  In this way they
are simple inferrence engines and allow for an interesting way to
write and solve computational problems.

Boolean logic is a simple yet versatile calulus that was found by
George Boole in 1815 and can be the basis of all hardware
computational engines and arithmetic.

========================================
Exercises 3 - Autograph, A Lazy Language
========================================

Sometimes it's interesting to think and program without thinking of
limitations, also known as working with infinite data structures.
There are many ways of implementing 'laziness', and we are going to
take the direction of developing our own language, 'Autograph', that
is in itself 'lazy', or has 'lazy evaluation'.

Lazy evaluation is the opposite of strict evaluation.  With most
languages, when a function is called, all of the arguments are
evaluated in left to right order prior to calling the function. With
macros, arguments are evaluated only when they are needed.  A lazy
language automates this process by only evaulating values when they
need to be evaluated for further processing.

===============================================
Mathmatical Exercises 4 - Multi-Core Ray Tracer
===============================================

A raytracer is a classic 'compuationally bound' problem in that it
takes a long time not due to it's amount of input/output operations,
but on it's actual CPU usage time.  It is also an 'embarassingly
parallell' problem, in that it repeats a very simple algorithm a large
number of times on identical data.  What this means is that we can
take advantage of this nature and split the problem up on multiple CPU
cores on your computer.

Since Eturia is a computer that runs in a web browser, we will be
taking advantage of WebWorkers to gain access to the additional cores
on the machine that are not normally available to Sigil, due to its
JavaScript nature.  Luckily, all that work has been done for you
behind the scenes, and Sigil's multi-core support is realized using
the following primitive operators:

|| - the parallel operator

Example:

(|| (task) callback) ; start a task, calling callback when it has completed
(set `*results* ()) ; list to store results of completed tasks
(|| ((lambda (x) (+ x x)) 4) ; computation task
    (lambda (result) (push result *results*))) ; callback with result

TODO: implement multi-core language operations in the browser using
WebWorkers.

Take the ray tracer from before and try to melt your cpu this time.

======================================
Exercises 8 - Prolog, a Logic Language
======================================

With all the usefulness that comes fromt the GPS (General Problem
Solver) that was implemented earlier, it still has some very serious
flaws and problems, often very simple ones, that it is incapable of
solving.  Prolog is a language that allows for the solution to
problems in a similar way, and was touted by Sussman as being the
elegant solution to the problems that GPS face.

Prolog is a 'logic language' in that, you give it facts and rules and
it logically infers solutions to the question, simply and succinctly
with a 'yes' or 'no' answer.  This unique way of programming is really
a very powerful database language and system, and in this chapter we
are going to be implementing a Prolog interpreter and compiler for
further use in our Eturia system.

===============================
Exercise 9 - A 'GPU' Ray Tracer
===============================

Take the multi-core raytracer and use WebGL to use the GPU for
rendering.

========================================================================
========================================================================

                               ========
                               |DREAMS|
                               ========

                          "Mind has no end."

                         -- K. David Harrison

========================================================================
========================================================================

================================
Exercise 10 - The 'Games' Problem
================================

The following MD5 sums and time lengths represent the checksums of a
corresponding (2 channel) .WAV file:

1. 0efb11a05d937c87a6823eebd8cded12 03:48
https://kruhft.bandcamp.com/track/0efb11a05d937c87a6823eebd8cded12

2. 2f139bfb26216eb48c1eb9c0bf0f4bd3 06:19	
https://kruhft.bandcamp.com/track/2f139bfb26216eb48c1eb9c0bf0f4bd3

3. 6c920420de5748f1da5a5bd1fc476bec 03:05	
https://kruhft.bandcamp.com/track/6c920420de5748f1da5a5bd1fc476bec

4. 9fb9456b7260d001d014413d3a62281c 01:58	
https://kruhft.bandcamp.com/track/9fb9456b7260d001d014413d3a62281c

5. 420d64b6dbcc779f9631f4599f4bb5dd 02:26	
https://kruhft.bandcamp.com/track/420d64b6dbcc779f9631f4599f4bb5dd

6. 422c8336d3e435ffe80d5f9e6a895154 03:55	
https://kruhft.bandcamp.com/track/422c8336d3e435ffe80d5f9e6a895154

7. 517f4c4e232319935b02fcfe006c30ec 03:40	
https://kruhft.bandcamp.com/track/517f4c4e232319935b02fcfe006c30ec

8. 6630d10982950b490c5a0c3bad1cdd0a 14:24	
https://kruhft.bandcamp.com/track/6630d10982950b490c5a0c3bad1cdd0a

9. e2b5363aa86ecdf78eedde1dfba9da23 04:56
https://kruhft.bandcamp.com/track/e2b5363aa86ecdf78eedde1dfba9da23

10. e37cb070c2cfabb9892ba1f540fdb08e 05:34
https://kruhft.bandcamp.com/track/e37cb070c2cfabb9892ba1f540fdb08e

11. e2b5363aa86ecdf78eedde1dfba9da23 06:36
https://kruhft.bandcamp.com/track/e2b5363aa86ecdf78eedde1dfba9da23

12. f44fab15d65679c91783580a82e76b18 05:00
https://kruhft.bandcamp.com/track/f44fab15d65679c91783580a82e76b18

13. fc917df3225544db59247e30fbf235d7 04:23
https://kruhft.bandcamp.com/track/fc917df3225544db59247e30fbf235d7

Problem: Rebuild the original .WAV files using the data given above.

An MD5-Sum Propagator Network Calculator
----------------------------------------

Utilizing the Boolean Propagtor Network from Exercise 6, we are going
to build a calculator for MD5 sums using such a network.  Due to the
ability of the propagator network to compute both forwards and
backwards, we are hoping that the network might contain some 'extra'
information when we look inside of it with partial information given
on its inputs and outputs.

================================
Exercise 11 - Genetic Programming
================================

TODO: find an interesting example, maybe from TLOL

====================================
Exercise 12 - A (Simulated) RISC CPU
====================================

Always wanted to to do this.

==========================================================
Exercise 13 - A Lisp Compiler for the (Simulated) RISC CPU
==========================================================

Same.

=====================================
Exercises 14 - A (Simulated) Lisp CPU 
=====================================

Ditto.

================================================
Exercises 15 - A Multi-Core (Simulated) Lisp CPU 
================================================

Ahoy.

=================================
Appendix 1 - A DSL For Javascript
=================================

==========
References
==========

[1OL]
Title: On Lisp
Year: 1993
Author: Paul Graham
URL: http://www.paulgraham.com/onlisp.html

[2SICP]
Title: Structure and Interpretation of Computer Programs
Year: 1979
Author: Gerald Jay Sussman
Author: Hal Abelson
URL: https://mitpress.mit.edu/sicp/full-text/book/book.html

[3ACL]
Title: ASNI Common Lisp
Year: 1995
Author: Paul Graham
URL: http://paulgraham.com/acl.html

[4TAOTP]
Title: The Art of the Propagator
Year: 2009
Author: Gerald Jay Sussman
URL: https://dspace.mit.edu/handle/1721.1/44215

[5PAIP]
Title: Paradigms of Artificial Intelligence Programming
Year: 1991
Author: Peter Norvig
URL: norvig.com/paip.html

[6TSFTPL]
Title: The Search for the Perfect Language
Year: 1993
Author: Umberto Eco
URL: http://www.amazon.com/Search-Perfect-Language-Making-Europe/dp/0631205101

[7TAOCP]
Title: The Art of Computer Programming
Year: 1962
Author: Donald Knuth
URL: https://www.amazon.ca/Computer-Programming-Volumes-1-4A-Boxed/dp/0321751043/

[WPGPS]
Title: General Problem Solver
URL: https://en.wikipedia.org/wiki/General_Problem_Solver

[WPSA]
Title: Susman Anomoly
URL: https://en.wikipedia.org/wiki/Sussman_Anomaly

[WPCGOL]
Title: Conway's Game of Life
URL: https://en.wikipedia.org/wiki/Conway%27s_Game_of_Life

--
Copyright - 2016

All rights reserved.  

If you wish to reproduce this work, please ask my permission first.
Fair use provisions apply.  The computer code contained in this
document can be used for any purpose without restriction.

"Things don't have to change the world to be important."

  -- Steve Jobs
