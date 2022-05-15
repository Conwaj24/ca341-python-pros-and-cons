## What is Python used for?

By looking at the most popular frameworks, libraries, and tools of 2020[10] we can gauge what use cases Python is most popular for. Categories include frontend development, backend development, machine-learning, data analysis, game development, and IT automation. I'm also writing from my own experience with the language where it is relevant

##### Education

My relationship with Python comes largely from its use in college; it was used to guide us through the fundamentals of computer programming in our first semester and was the tool we used to complete all of our first programing assignments. Python's inclusion in the curriculum was not an arbitrary choice; all of the most notable characteristics of the language have obvious benefits for a beginner to programming.

Python is very deliberately designed to be simple to understand for non-programmers. Where many other languages use syntax constructs derived from mathematics or computer science, Python often uses plain words. Here comparing the syntax of  Python with that of a more C-based language. Note that the operators in the below example are still available in Python but don't mean the same things.

```python
x is y and 0 is not (x or z)
```

```c
x == y && 0 != (x || z)
```

While it may seem like Python is keyword-heavy, it actually has fewer reserved words than many other languages[1,2,3]. Python uses whitespace instead of parentheses to delimit code blocks, which may be more familiar to non-programmers as similar conventions are used to similar effect in document writing. Python is interpreted, which allows it to be run sooner after being written by skipping the compilation phase and even allows code to be written and interpreted simultaneously using the REPL functionality of the python interpreter, which makes the language a lot more fluid to use even with minimal tooling. Here I'm using the REPL to interactively write some code and read the inbuilt documentation.

```python
Python 2.7.18 (default, Apr 19 2020, 21:45:35)
[GCC 9.3.0] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>> help(range)

>>> range(2,12,3)
[2, 5, 8, 11]
>>> '\n'.join(['*' * i for i in range(2,12,3)])
'**\n*****\n********\n***********'

```

It uses dynamic typing, which shields the programmer from needing to know the names of different types, and makes the code faster to write because the programmer simply has to do less typing (no pun intended).

##### Science

Pandas and Tensorflow are among the most popular frameworks, both of which are Python frameworks. Pandas is a Data Science framework, and Tensorflow is a machine learning framework, which is arguably a subset of data science.

It's hard to find objective data on the subject, as download and usage statistics are not published by the popular package repositories, but just from surveying some of the top search results[25,26,27,28] the most common libraries which appear are (in no particular order) TensorFlow, Pytorch, Keras (machine learning), Theano. Matplotlib, Numpy, SciPy (Mathematics), BeautifulSoup, OpenCV, Pendulum (Data Extraction and Regularization), Requests, Flask, Bottle (Web Frameworks and Tools), PyQt, and TKinter (Application Development).

This is hardly conclusive, especially since these kinds of websites (content farms) are known to copy from one-another without adding any original value to the the internet, but it should at least give an indication of the current discourse around Python and its use. A majority of the libraries mentioned focus on technical professions aside from software development, such as data science or mathematics. 

##### Hackathons

Advent of Code is an annual online event where participants solve a new contrived programming challenge each day of advent[11]. You are deemed to have passed if you produce the correct answer, and are awarded extra points for completing the challenge sooner, but the code itself is not assessed. Infact you could work out some of the problems on paper if you were so inclined (though they are usually designed to be far too tedious for humans). It seems that in the field of tiny, single-use programs, that don't have to be well written, tackling novel use-cases, where time-to-live is the only important determinant of quality, is dominated by Python according to Github statistics[12]. These characteristics pretty much form the prototype of the ideal use case for Python, and dynamically typed languages in general

## Type Systems

It’s worth mentioning at this point, what dynamic typing actually is and how approaches to type systems differ across languages. The most basic kind of type system is one where the programmer must explicitly declare the type of each variable, this is called strict typing.

```c
static const uint myInt = 64;
```

Many strictly typed languages also support type inference, which leaves the compiler to figure out for itself what type a variable is, usually in the case that the variable is explicitly assigned and therefore it is obvious what type it is.

```rust
let i = 0;
let s = "hello"
```

Type inference is really just syntactic sugar rather than a distinct type system, the section of memory that your variable represents still has a definite type but you have saved yourself the effort of stating what that type is.

##### Dynamic typing is quite different

In a dynamically typed language it is more useful to think of a variable name, not as a label on a specific part of memory, but rather as a key to one of the values in the variables database. This does not necessarily reflect the actual implementation of the language, it’s perfectly possible to make a dynamically typed language where variables names refer to directly to memory, and a statically typed language that uses a key-value store for all its variables, it is more a remark on what a variable name means to a programmer as opposed to how it is implemented (that said, python’s variables are actually implemented as a key-value store, which can be accessed at runtime). In Python there are no variable declarations or initializations; variables in Python are created by assignment, and assignment of variables always succeeds.

```python
i = 0
i = "hello"
```

One important thing to note is that variables in Python do actually have types, the same types present in most languages, the only thing that makes dynamic typing special is that the labels that refer to the working memory of the program are divorced from any notion of what they are actually referring to, sort of like a void pointer in C. You can still get errors in Python if your variables have the incorrect type, but the type of a variable must be determined by looking at its value at runtime, and checking the type is entirely optional.

```python
def plusone(i):
    return i + 1
plusone('1')
#this Python code will throw a TypeError at runtime
```

```java
class TypeDemo {
    int plusOne (int i) {
        return i + 1;
    } public static void main(String[] args) {
       plusOne('1'); 
    }
}
//this Java program will not run because it violates the type rules
```

##### Dynamic typing is not automatically better

The mere existence of Typescript[24], a language which is identical to Javascript except that it supports static typing, should be enough to demonstrate this point. With static typing comes peace of mind, you can trust that certain conditions will always be true, you don't need to implement checks or recoveries for when you get bad data, which costs both the time of the developer and runtime of the computer.

The problems with dynamic typing tend to compound with the scale the project, as the burden of remembering the edge cases of each function grows. This is why Typescript is advertised as "Javascript at any scale"[24], and is something that needs to be considered before choosing a language like Python.

##### There are some typeless languages;

Languages that go beyond dynamic typing and have no concept of type whatsoever. Bash is an example of this. In Bash (and other shell scripting languages) all variables are strings, and all function arguments are strings. This makes perfect sense as shell languages evolved from text terminals where users type in strings which are evaluated to run programs and produce more strings to display on the screen. Bash is essentially a language for moving strings between programs, and it is the responsibility of said programs to decide what to make of these strings. Below is an example of how you might do maths using shell script.

```bash
echo 3 5 | awk '{print $1 + $2}'
```

Note that the `awk` program (which is what performs the addition) is responsible for interpreting the strings we give it through standard input as numbers, so we essentially defer to another domain-specific language when we need to think about anything except strings. Typeless programming languages like Bash are very uncommon, Bash is only able to be used for reasonably large projects because of its ability to *"shell out"* to other languages, like awk or, indeed, Python; languages which *do* have a concept of type, even if they are dynamically typed.

There is another, much more common, language which is often compared to Python, and somewhat resembles Bash in its relationship with strings:

##### Javascript

Much like how shell script was originally made for moving strings between programs, Javascript was originally intended to read and write strings on a webpage. Unlike Bash, Javascript has types, but it is far less strict with type enforcement than Python; and in how it resolves disparate types in situations where Python would simply throw a type error demonstrates its preference for strings.

```javascript
> 5 + true
6
> 5 + true + "5"
'65'
> "5" + 5 + true
'55true'
> "5" + (5 + true)
'56'
// the result of addition with a string and some other type is always a string
```

This quality of Javascript is owed in part to the language’s aforementioned relationship with strings, and in part to the Robustness Principle, which which it shares with HTML and CSS and which has been standard practice for web technologies since as far back as TCP[4]. The comparison with Javascript is quite important as Python and Javascript are the two most high-profile examples of general-purpose dynamically-typed programming languages[7,15], and so one of the most telling ways to examine the strengths and weaknesses of Python is by examining how it differs from Javascript.

## Comparing Python and Javascript

For reference, here is how Python interprets the above expressions:

```python
>>> 5 + True
6
>>> 5 + True + "5"
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unsupported operand type(s) for +: 'int' and 'str'
>>> "5" + 5 + True
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: can only concatenate str (not "int") to str
>>> "5" + (5 + True)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: can only concatenate str (not "int") to str
```

The first operation succeeds, because `True` is really just syntactic sugar for `1`, (this is the case in many languages, especially those which borrow their syntax from C) the remaining operations fail because Python doesn't allow addition between strings and integers. There are many other examples of the kinds of things Javascript allows and Python doesn't:

##### Object literals

```javascript
const literalObject = {
	foo: "hello",
    bar: "world",
	literalMethod() {
		console.log(this.foo + " " + this.bar)
	},
    getFoo() {
        return this.foo
    }
}
```

Objects can be declared in Javascript without having to be  initialized, this is useful for a few things, such as creating named scopes for an ad-hoc import hierarchy and it eliminates the need for the verbose and cumbersome singleton pattern[16] which is used in many object oriented languages to enforce that only one instance of a particular object can be in scope at a time (a problem which only exists due to the need to instantiate an object at runtime rather than just declaring it). Though really this serves best as an example of the expressiveness and directness of Javascript, things that are only possible in dynamically-typed, interpreted languages.

Python does not make it impossible to do something like this, it allows you to define arbitrarily nested dictionaries using a syntax almost identical to json:

```python
d = {
    "foo": "hello",
    "bar": "world",
    "literalMethod": lambda self: print(self.foo, self.bar),
    "getFoo": lambda self: self.foo
}
```

And since in Python, an object is mostly just a fancy interface to a dictionary, it's possible to convert an object to a dictionary relatively easily, like so:

```python
from types import MethodType

class DictionaryObject:
    def process_child(self, child):
        if isinstance(child, dict):
            return DictionaryStruct(child)
        if isinstance(child, list):
            return [self.process_child(c) for c in child]
        if isinstance(child, tuple):
            return (self.process_child(c) for c in child)
        # and so on, for every builtin collection...

        try:
            return MethodType(child, self)
        except TypeError:
            pass # child is not callable

        return child
    
    def __init__(self, d):
        self.__dict__.update( # __dict__ defines all the attributes of the object
            {k: self.process_child(v) for k, v in d.items()}
        )

o = DictionaryObject(d)
o.literalMethod()
# hello world
```

This is a fairly succinct piece of code and shows off a lot of the strengths of Python; the list, set, and dictionary comprehensions, the simple-but-powerful import system, the easy type checking which doesn't involve comparing strings, and the robust and straightforward exception handling and its use in an EAFP[16] style, which lends itself to duck-typed languages much better than type checking (a.k.a LBYL[17]). Despite all these merits, though, this code lacks the declarative quality of the Javascript example; the ability to directly write arbitrary data into existence, and it's still substantially more code than Javascript's zero lines.

In Javascript, objects aren't a fancy interfaces to dictionaries, they *are* dictionaries, and no conversion is neccesary to be able to treat them like either. 

```javascript
literalObject.literalMethod()
// hello world
literalObject["literalMethod"]()
// hello world
```

##### Runtime attribute binding

```js
function bind_controller(websocket) {
	websocket.controller = tpinput.open(config)
	websocket.controller.on('close', (code, sig) => {
		if (sig == 'SIGTERM' || sig == 'SIGKILL')
			return
		console.error(`${websocket.id}: Controller closed unexpectedly, restarting`)
		bind_controller(websocket)
	})
}
```

Here is some code that was used in my third year project. I needed to keep track of the relationship between a websocket and a process that was reading the data from it. Other languages would have many possible way of doing this:

- Making a lookup table of controllers that uses websockets as the keys, or rather some unique identifier of the websocket (should one exist), since there are often complications with using the object itself (either by value or by reference).
- Making an object called `WebsocketController` or `WebsocketAndController` or `WebsocketWithController` which contains the websocket and the associated controller and using that to refer to the websocket or its controller in the future.
- Making a subclass of the websocket which includes the additional field and either statically casting the websocket to the new class and setting the additional field, or creating a new object which has all the same attributes as the websocket (including the private ones) as well as the additional field.

Javascript just lets you attach arbitrary attributes and methods to any object, which is a far more direct way of going about it and far more eloquently expresses the relationship between the websocket and the controller.

#### In General

Python is a much safer language than Javascript, it imposes more restrictions on what can be legally evaluated and it has a much stronger emphasis in organizational and safety features like type checking, exception handling, and importing modules. Although they are both dynamic languages, they have quite different design philosophies; Javascript lends much of its design to the aforementioned Robustness Principle (a.k.a Postel's Law), while Python is designed to be as intuitive and predictable as possible.

One of the main criticisms of Javascript's interpretation of the Robustness Principle is that when the languages tries its utmost to interpret any code without crashing, it results in a lot of implicit functionality; implicit type conversion (as demonstrated previously), accessing undefined elements in arrays or objects, unintuitive results to equality testing (and the subsequent inclusion of a second equality operator, `===`, with a different meaning), and the flagrant violation of the distributive property of addition[5,6]. This implicit functionality can mean that a lot of things can go wrong in succession before the program finally crashes, meaning that the program can fail in ways that are very difficult to predict. Python does not offer the same freedom and expressiveness as Javascript because being safe is an important part of being simple, understandable, and beginner friendly.

Still, one can't help but think that Javascript is a much better example of what is possible with a dynamically-typed, interpreted language. Python doesn't make you declare the types explicitly, but it still makes you care about the types, it still still throws `TypeError`'s when you don't use them properly, and it still expects you to know them names of the types for type checking. It could be argued that Python obfuscates its types without really abstracting them away, which only makes the language more confusing. It might save you the effort of explicitly declaring your types, but not when you have to write your own type-checking and error-handling code in each function to ensure your program is safe. Python also obfuscates the distinction between values and references, which leads to this classic headscratcher:

```python
def headscratcher(a=[1,2,3]):
    b = a
    b.append(4)
    print(b)

headscratcher() #[1, 2, 3, 4]
headscratcher([4,5,6]) #[4, 5, 6, 4]
headscratcher() #[1, 2, 3, 4, 4]
```

The function produces different results when run with the same arguments because the argument `a` is actually declared as a reference to the default assignment, so the arguments you pass to the function can change the reference but not the actual value of the default assignment, which persists across iterations. The distinction between references and values is not made explicit and, like types, is something that the programmer is just expected to memorize.

To put it simply, the difference between Python and Javascript is that Python is dynamically typed because it is afraid of burdening users with being explicit about types, while Javascript is dynamically typed because it's afraid of nothing and revels in the inherent danger of dynamic languages. Personally, I have a lot more respect for Javascript's philosophy; if one wants safety, one does not choose a dynamic language.

There is another important quality of Javascript that benefits it in every conceivable application, a quality that Python lacks.

## Performance

We finally reach the elephant in the room; Python is slow, not just a bit slow, but the slowest language I could find benchmarks for[8]. Python (Specifically the CPython official implementation) sacrifices performance for other concerns at every turn: Being interpreted means that code is not machine-optimized before being run. Dynamic typing gives computer more work to do at runtime and gives the interpreter less information with which to optimize. Using whitespace to define scope requires a more complex parsing model and prevents the code from being easily minified. PyPy, another Python implementation, is able to gain significant performance improvements using just-in-time compilation[9], however this comes at the cost of startup time, which is more important to CPython than speed.

Python is often given as an example of how the increased speed of computers due to Moore's Law[20] gives us the freedom to write more expressive code in slower languages, the suggestion being that caring about performance is being made obsolete. The first problem with this sentiment is that the ease with which one can create a computer program has not  been doubling every two years, this should go without saying. Certain types of programs have been trivialized as the number of specific frameworks grows (linearly, I might add) but broadly speaking, the relative ease with which one can create a piece of software has been increasing slowly if at all, while the performance of computer programs has, if anything, been decreasing[21]. The second problem is that the belief in a causal relationship between high levels of abstraction and poor performance is a fallacy[22]. Haskell is an excellent (and all too uncommon) example of a language which is fast, not in spite of its high level of abstraction, but because of it[23].

Somewhat counterintuitively, safety features tend to make compiled languages faster but interpreted languages slower, this is because a language for which safety is ensured at compile-time, is allowed to be less safe at runtime. For example, Rust is able to outperform C in certain applications[19] because Rust ensures memory-safety at compile time, which eliminates the need to count references or use more robust but slower data structures. Rust is not faster than C per se, but it can allow you to safely write faster code. A lot of what makes Python so much slower than Javascript is its safety, which is enforced at runtime.

On the subject of C...

### The C programming language is often given as the opposite of Python. 

Whereas Python is a low-performance language with a syntax that intentionally obscures the specifics of the hardware, C is a systems programming language which was primarily designed for speed, it is very close to the hardware in a way that many of its precursors (such as Fortran or Cobol) were not.

That said, Python and C/C++ actually have a fairly close relationship; the Python Interpreter is written in C which lends the two languages to have easier interoperability and, as such, It is often advised that the performance-critical components of a python program be written in C or C++[13]. The way these two complementary languages so easily interoperate has been a tremendous boon for Python as it greatly expands the value profile of the language, more so than if a more similar language (like Ruby, or Javascript) was the natural choice for extending Python. While speeding up a Python program is a common use case for interoperability between C and Python, the inverse case is also quite common; 

##### Python is a very popular language for plugins.

Large Graphical programs like Microsoft Word and other Microsoft Office applications, Adobe CC programs, 3D rendering, and CAD programs, are almost always written in C++. This is the case partly because C++ is a very high-performing language with Object-Oriented features (which are often desirable for graphical user interfaces), and partly because many of these applications would have to be of significant age to have become so large, which would limit the choice of language to those that were available and modern at the time and were fast enough to provide a good user experience on the computers of the time. I was able to find very few exceptions: VSCode (which is an open-source and cross-platform rewrite of Visual Studio) is written in typescript, as it would be much easier to port to other platforms and the performance of the language was not of concern. Many developer tools with a focus on a specific language (such as Intellij and MonoDevelop) are written in the associated language (Java and C# respectively), provided that language can meet the performance demands, and FLStudio is written in Delphi for reasons I won’t attempt to guess. But I digress, most such programs are written in C++ and a very common user extensibility strategy for such programs is plugin support.

##### A plugin has a very different set of requirements than the application it plugs into

Plugins are small programs, they do not need to be fast as they rely on the fast functionality of the application, they do not need to be well written as few people will see the code and there is little utility for genericism in such a small and specific program, and plugins should be as easy as possible to create, because having a large third-party toolset is an important selling point for such applications. Another way of putting this is that the ideal value profile for a plugin programming language is more or less the opposite of the ideal value profile for an application programming language, given that, and the first-class interoperability that Python has with C/C++, it’s plain to see why Python would be such a popular language for plugins. Python’s dominance in the plugins space is not nearly as great as the dominance of C++ in the application space; javascript is popular and has replaced Visual Basic (the most dreaded programming language[14]) as the primary extension language for the Microsoft Office Suite, it’s especially popular for web-related or web-native applications, though it’s web-focus makes less suitable as a sandboxed scripting language in the way that Python is. Lua is also a popular language for plugins, though still fairly niche. Suffice it to say, python is an obvious choice for extending or scripting large C++ programs, and is used by Blender, Gimp, Krita, Fusion360, Sublime Text, and TensorFlow. The latter is perhaps the most interesting as it has led to the near total dominance of Python in one of the fastest growing fields in computer science; machine learning.

## In Summary

##### Python is...

- A clean, simple, and understandable language, uncompromising on convenience, with many novel features that aid in quickly working on data and solving problems
- Relatively safe and organized for a dynamic language, especially if exception handling is used to full effect
- Interoperates well with its most complementary languages, C and C++, making it perfect for plugins or scripting interfaces to larger programs

##### but

- Has the worst performance of any mainstream language
- Does not make full use of the freedoms of dynamic typing and often seems to obfuscate types, as well as the distinction between values and references, without really abstracting them away
- Is still not very safe compared to languages with compile-time type checking, despite all its efforts to be, and all the performance implications therein

## References

[1] C++ keywords - cppreference.com [Online]. Available: https://en.cppreference.com/w/cpp/keyword. [Accessed: December 20 2020].

[2] Java Language Keywords (The Java&trade; Tutorials &gt; Learning the Java Language &gt; Language Basics) [Online]. Available: https://docs.oracle.com/javase/tutorial/java/nutsandbolts/_keywords.html. [Accessed: December 20 2020].

[3] 2.3.1 Keywords [Online]. Available: https://docs.python.org/2.5/ref/keywords.html. [Accessed: December 20 2020].

[4] RFC 761 - DoD standard Transmission Control Protocol [Online]. Available: https://tools.ietf.org/html/rfc761#section-2.10. [Accessed: December 20 2020].

[5] Wat [Online]. Available: https://www.destroyallsoftware.com/talks/wat. [Accessed: December 20 2020].

[6] JavaScript Breaks Math [Online]. Available: https://rhodesmill.org/brandon/2012/js/. [Accessed: December 20 2020].

[7] Stack Overflow Developer Survey 2020 [Online]. Available: https://insights.stackoverflow.com/survey/2020#technology-programming-scripting-and-markup-languages-all-respondents. [Accessed: December 21 2020].

[8] Python 3&nbsp;vs&nbsp;Node js - Which programs are fastest? | Computer Language Benchmarks Game [Online]. Available: https://benchmarksgame-team.pages.debian.net/benchmarksgame/fastest/python.html. [Accessed: December 20 2020].

[9] Why is Python so slow? | Hacker Noon [Online]. Available: https://hackernoon.com/why-is-python-so-slow-e5074b6fe55b. [Accessed: December 20 2020].

[10] Stack Overflow Developer Survey 2020 - frameworks, libraries, and tools [Online]. Available: https://insights.stackoverflow.com/survey/2020#technology-other-frameworks-libraries-and-tools-all-respondents3. [Accessed: December 20 2020].

[11] Advent of Code 2020 [Online]. Available: https://adventofcode.com/. [Accessed: December 20 2020].

[12] Search · advent of code · GitHub [Online]. Available: https://github.com/search?q=advent+of+code. [Accessed: December 20 2020].

[13] The Python Tutorial &#8212; Python 3.9.1 documentation [Online]. Available: https://docs.python.org/3/tutorial/index.html. [Accessed: December 20 2020].

[14] Stack Overflow Developer Survey 2020 - Most dreaded languages [Online]. Available: https://insights.stackoverflow.com/survey/2020#technology-most-loved-dreaded-and-wanted-languages-dreaded. [Accessed: December 20 2020].

[15] List of dynamic programming language - Wikipedia [Online]. Available: https://en.wikipedia.org/wiki/Dynamic_programming_language#Examples. [Accessed: August 04 2021].

[16] Singleton Design Pattern | Implementation - GeeksforGeeks [Online]. Available: https://www.geeksforgeeks.org/singleton-design-pattern/. [Accessed: August 08 2021].

[17] Glossary &#8212; Python 3.5.9 documentation [Online]. Available: https://docs.python.org/3.5/glossary.html#term-eafp. [Accessed: August 08 2021].

[18] Glossary &#8212; Python 3.5.9 documentation [Online]. Available: https://docs.python.org/3.5/glossary.html#term-lbyl. [Accessed: August 08 2021].

[19] Is It Time to Rewrite the Operating System in Rust? [Online]. Available: https://www.infoq.com/presentations/os-rust/. [Accessed: August 09 2021].

[20] Moore's law - Wikipedia [Online]. Available: https://en.wikipedia.org/wiki/Moore%27s_law. [Accessed: August 09 2021].

[21] Wirth's law - Wikipedia [Online]. Available: https://en.wikipedia.org/wiki/Wirth%27s_law. [Accessed: August 09 2021].

[22] #Gamelab2018 - Jon Blow&#39;s Design decisions on creating Jai a new language for game programmers - YouTube [Online]. Available: https://www.youtube.com/watch?v=uZgbKrDEzAs. [Accessed: August 09 2021].

[23] Haskell is Faster than Rust! &#8230; Wait a Sec! &#8211; akquinet AG &#8211; Blog [Online]. Available: https://blog.akquinet.de/2021/01/03/haskell-is-faster-than-rust-wait-a-sec/. [Accessed: August 09 2021].

[24] TypeScript: Typed JavaScript at Any Scale. [Online]. Available: https://www.typescriptlang.org/. [Accessed: August 09 2021].

[25] 34 Open-Source Python Libraries You Should Know About [Online]. Available: https://www.mygreatlearning.com/blog/open-source-python-libraries/. [Accessed: August 09 2021].

[26] Top 10 Python Libraries You Must Know In 2021 | Edureka [Online]. Available: https://www.edureka.co/blog/python-libraries/. [Accessed: August 09 2021].

[27]  [Online]. Available: https://towardsdatascience.com/best-python-libraries-for-every-python-developer-77daab4fa40e?gi=99d72d726438. [Accessed: August 09 2021].

[28] Top 10 Python Packages Every Developer Should Learn | ActiveState [Online]. Available: https://www.activestate.com/blog/top-10-must-have-python-packages/. [Accessed: August 09 2021].