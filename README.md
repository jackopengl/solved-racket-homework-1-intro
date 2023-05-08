Download Link: https://assignmentchef.com/product/solved-racket-homework-1-intro
<br>
The first thing you will need to do is to download and install <a href="https://racket-lang.org/">Racket</a> and then the <a href="http://pl.barzilay.org/pl.plt">course plugin</a><a href="http://pl.barzilay.org/pl.plt">.</a> You might want to consult <a href="http://www.htdp.org/"><em>How to Design Programs</em></a> and the <a href="http://pl.barzilay.org/resources.html#classnotes">Class</a> <a href="http://pl.barzilay.org/resources.html#classnotes">Notes</a> before writing your code.

For this problem set, you are required to set the language level to the course’s language, by beginning you file with #lang pl.

<strong><u>The language and how to form tests:</u></strong> In this homework (and in all future homework) you should be working in the “Module” language, and use the appropriate language using a #lang line. You should also click the “Show

Details” button in the language selection dialog, and check the “Syntactic test suite coverage” option to see parts of your code that are not covered by tests: after you click “run”, parts of the code that were covered will be colored in green, parts that were not covered will be colored in red, and if you have complete coverage, then the colors will stay the same. Note that you can also set the default language that is inserted into new programs to #lang pl, to make things more convenient. There are some variants for the pl language for various purposes — in particular, #lang pl untyped will ignore all type declarations, and will essentially run your code in an untyped Racket. The language for this homework is:

#lang pl

As will also be shown in class, this language has a new special form for tests: test. It can be used to test that an expression is true, that an expression evaluates to some given value, or that an expression raises an error with some expected text message. For example, the three kinds of tests are used in this example:

(define (safe-length list)

(cond [(null? list) 0]

[(pair? list) (add1 (safe-length (cdr list)))]

[else (error ‘safe-length “bad value: ~s” list)]))

(test (zero? (safe-length null)))

(test (safe-length ‘(1 2 3)) =&gt; 3)

(test (safe-length “three”) =    error&gt; “bad value”)

In case of an <em>expected</em> error, the string specifies a pattern to match against the error message. (Most text stands for itself, “?” matches a single character and “*” matches any sequence of characters.)

Note that the =error&gt; facility checks only errors <strong>that <em>your</em> code throws</strong>, not Racket errors. For example, the following test <strong>will not</strong> succeed (because it is an error thrown by Racket):

(test (/ 4 0) =error&gt; “division by zero”)

Reminder: code quality will be graded. Write clean and tidy code. Consult the <a href="http://pl.barzilay.org/style-guide.html">Style Guide</a><a href="http://pl.barzilay.org/style-guide.html">,</a> and if something is unclear, ask questions on the course’s forum.

<h1>Questions</h1>

<ol>

 <li>Define the following functions, all of which consume five characters and return a string.

  <ul>

   <li>The function <em>append5</em> – consumes 5 characters and returns the concatenation of them. For example, (append5 #a #b #c #d</li>

  </ul></li>

</ol>

#e) would return “abcde”. Here is another example, written in a form of a test that you can use:

(test (append5 #e #d #c #b #a) =&gt; “edcba”)

<ul>

 <li>The function <em>permute3</em> – consumes 3 characters and returns a list of strings the concatenation of them in any possible ordering (you may assume all of them are distinct). <strong>Important: </strong>make sure to declare the most precise type for the returned value of your function. For example, if you know you are using a list of two naturals, then, <sub>(List Natural </sub>Natural) is more precise than (Listof Any).</li>

</ul>

Here is an example, written in a form of a test that you can use.

(test (permute3 #a #b #c) =&gt;

‘(“abc” “acb” “bac” “bca” “cab” “cba”))




<ol start="2">

 <li><u>Reminder:</u></li>

</ol>

Remember that lists are defined inductively as either:

<ul>

 <li>An empty list — null</li>

 <li>A cons pair (sometimes called a “cons cell”) of <em>any</em> head value and a list as its tail — (cons <em>x</em> <em>y</em>)</li>

</ul>

A “<sub>Listof </sub><em>T</em>” would be similar, except that it will use the type <em>T</em> (which needs to be defined by you, say, Symbol, Natural, or Number) instead of

“any”.




<ol>

 <li>With this in mind, define a <u>recursive</u> function count-3lists that consumes a list of lists (where the type of the elements in the inner lists may be any type) and returns the number of inner lists (within the wrapping list) that contain exactly 3 elements.</li>

</ol>




For example, written in a form of a test that you can use:

(test (count-3lists ‘((1 3 4) (() (1 2 3)) (“tt” “Three” 7) (2 4 6 8) (1 2 3))) =&gt; 3)

<ol>

 <li>Define a function count-3lists-tail that works the same as count-3lists, but now you need to use <u>tail-recursion</u>.</li>

</ol>




You can use the same example (only here the name of the function is count-3lists-tail):

(test (count-3lists-tail ‘((1 3 4) (() (1 2 3)) (“tt” “Three” 7) (2 4 6 8) (1 2 3))) =&gt; 3)

<ol>

 <li>Write an additional function count-3listsRec that is similar to the above count-3lists, however counts the number of lists of length 3 recursively (i.e., on all levels of nesting).</li>

</ol>




For example, written in a form of a test that you can use:

(test (count-3listsRec ‘((1 3 4) (() (1 2 3)) (“tt” “Three” 7) (2 4 6 8) (1 2 3))) =&gt; 4)




<ol start="3">

 <li>In this question we will implement a keyed-stack data structure. In this data structure you will need to define a new type called Each element in the stack will be keyed (indexed) with a symbol. In the following the operations that you are required to implement are detailed below, together with some guidance.

  <ul>

   <li>Implement the empty stack EmptyKS – this should be a variant of the data type (constructor).</li>

   <li>Implement the push operation Push – this too should be a variant of the data type. The push operation should take as input a symbol (key), a string (value), and an existing keyed-stack and return an extended keystack in the natural way – see examples below.</li>

   <li>Implement the search operation search-stack – the search operation should take as input a symbol (key) and a keyed-stack and return the first (LIFO, last in first out) value that is keyed accordingly – see examples below. If the key does not appear in the original stack, it should return a #f value (make sure the returned type of the function supports this; use the strictest type possible for the returned type).</li>

   <li>Implement the pop operation pop-stack – the pop operation should take as input a keyed-stack and return the keyed-stack without its first (keyed) value – see examples below. If the original stack was empty, it should return a #f value (make sure the returned type of the function supports this; use the strictest type possible for the returned type).</li>

  </ul></li>

</ol>

For example, written in a form of a test that you can use:

<table width="487">

 <tbody>

  <tr>

   <td width="487">(test (EmptyKS) =&gt; (EmptyKS))(test (Push ‘b “B” (Push ‘a “A” (EmptyKS))) =&gt;(Push ‘b “B” (Push ‘a “A” (EmptyKS))))(test (Push ‘a “AAA” (Push ‘b “B” (Push ‘a “A”  (EmptyKS)))) =&gt; (Push ‘a “AAA” (Push ‘b “B” (Push ‘a “A” (EmptyKS)))))(test (search-stack ‘a (Push ‘a “AAA” (Push ‘b “B” (Push ‘a “A” (EmptyKS))))) =&gt; “AAA”)(test (search-stack ‘c (Push ‘a “AAA” (Push ‘b “B” (Push ‘a“A” (EmptyKS))))) =&gt; #f)(test (pop-stack (Push ‘a “AAA” (Push ‘b “B” (Push ‘a “A” (EmptyKS))))) =&gt; (Push ‘b “B” (Push ‘a “A” (EmptyKS))))(test (pop-stack (EmptyKS)) =&gt; #f)</td>

  </tr>

 </tbody>

</table>




<ol start="4">

 <li>In this question you are given full code together with tests for the presented functions. All you are required to do is to add the appropriate comments for each of the functions. These comments should describe what the function takes as input, what it outputs, what its purpose is, and how it operates. Do not forget to also add your personal remarks on the process in which you personally came to realize the above. You should copy the following code into your .rkt file, and add the comment therein.</li>

</ol>




(: is-odd? : Natural -&gt; Boolean)

<h2>;; &lt;&lt; Add your comments here&gt;&gt; ;; &lt;&lt; Add your comments here&gt;&gt;</h2>

(define (is-odd? x)   (if (zero? x)       false

(is-even? (- x 1))))




(: is-even? : Natural -&gt; Boolean)

<h2>;; &lt;&lt; Add your comments here&gt;&gt; ;; &lt;&lt; Add your comments here&gt;&gt;</h2>

(define (is-even? x)   (if (zero? x)       true

(is-odd? (- x 1))))




;; tests — is-odd?/is-even?

(test (not (is-odd? 12)))

(test (is-even? 12))

(test (not (is-odd? 0)))

(test (is-even? 0))

(test (is-odd? 1))

(test (not (is-even? 1)))




(: every? : (All (A) (A -&gt; Boolean) (Listof A) -&gt; Boolean)) ;; See explanation about the All syntax at the end of the file…

<h2>;; &lt;&lt; Add your comments here&gt;&gt; ;; &lt;&lt; Add your comments here&gt;&gt;</h2>

(define (every? pred lst)

(or (null? lst)

(and (pred (first lst))

(every? pred (rest lst)))))







;; An example for the usefulness of this polymorphic function

(: all-even? :   (Listof Natural) -&gt; Boolean)

<h2>;; &lt;&lt; Add your comments here&gt;&gt; ;; &lt;&lt; Add your comments here&gt;&gt;</h2>

(define (all-even? lst)

(every? is-even? lst))







;; tests

(test (all-even? null))

(test (all-even? (list 0)))

(test (all-even? (list 2 4 6 8)))

(test (not (all-even? (list 1 3 5 7))))

(test (not (all-even? (list 1))))

(test (not (all-even? (list 2 4 1 6))))







(: every2? : (All (A B) (A -&gt; Boolean) (B -&gt; Boolean) (Listof A) (Listof B) -&gt; Boolean))

<h2>;; &lt;&lt; Add your comments here&gt;&gt; ;; &lt;&lt; Add your comments here&gt;&gt;</h2>

(define (every2? pred1 pred2  lst1 lst2)

(or (null? lst1) ;; both lists assumed to be of same length

(and (pred1 (first lst1))

(pred2 (first lst2))

(every2? pred1 pred2 (rest lst1) (rest lst2)))))

syntax

<table>

 <tbody>

  <tr>

   <td width="80"></td>

  </tr>

  <tr>

   <td></td>

   <td></td>

  </tr>

 </tbody>

</table>

<a href="https://docs.racket-lang.org/ts-reference/type-ref.html?q=all#%28form._%28%28lib._typed-racket%2Fbase-env%2Fbase-types-extra..rkt%29._.All%29%29">(</a><a href="https://docs.racket-lang.org/ts-reference/type-ref.html?q=all#%28form._%28%28lib._typed-racket%2Fbase-env%2Fbase-types-extra..rkt%29._.All%29%29"><strong>All</strong></a> (<em>a</em> …) <em>t</em>) <a href="https://docs.racket-lang.org/ts-reference/type-ref.html?q=all#%28form._%28%28lib._typed-racket%2Fbase-env%2Fbase-types-extra..rkt%29._.All%29%29">(</a><a href="https://docs.racket-lang.org/ts-reference/type-ref.html?q=all#%28form._%28%28lib._typed-racket%2Fbase-env%2Fbase-types-extra..rkt%29._.All%29%29"><strong>All</strong></a> (<em>a</em> … <em>a</em> <em>ooo</em>) <em>t</em>)

is a parameterization of type <em>t</em>, with type variables v <a href="https://docs.racket-lang.org/reference/stx-patterns.html#%28form._%28%28lib._racket%2Fprivate%2Fstxcase-scheme..rkt%29._......%29%29">…</a><a href="https://docs.racket-lang.org/reference/stx-patterns.html#%28form._%28%28lib._racket%2Fprivate%2Fstxcase-scheme..rkt%29._......%29%29">.</a> If <em>t</em> is a function type constructed with infix <a href="https://docs.racket-lang.org/ts-reference/type-ref.html?q=all#%28form._%28%28lib._typed-racket%2Fbase-env%2Fbase-types-extra..rkt%29._-~3e%29%29">-&gt;</a><a href="https://docs.racket-lang.org/ts-reference/type-ref.html?q=all#%28form._%28%28lib._typed-racket%2Fbase-env%2Fbase-types-extra..rkt%29._-~3e%29%29">,</a> the outer pair of parentheses around the function type may be omitted.

Examples:

&gt; <a href="https://docs.racket-lang.org/ts-reference/special-forms.html?q=all#%28form._%28%28lib._typed-racket%2Fbase-env%2Fprims..rkt%29._~3a%29%29">(</a><a href="https://docs.racket-lang.org/ts-reference/special-forms.html?q=all#%28form._%28%28lib._typed-racket%2Fbase-env%2Fprims..rkt%29._~3a%29%29">:</a> list-length <a href="https://docs.racket-lang.org/ts-reference/special-forms.html?q=all#%28form._%28%28lib._typed-racket%2Fbase-env%2Fprims..rkt%29._~3a%29%29">:</a> <a href="https://docs.racket-lang.org/ts-reference/type-ref.html?q=all#%28form._%28%28lib._typed-racket%2Fbase-env%2Fbase-types-extra..rkt%29._.All%29%29">(</a><a href="https://docs.racket-lang.org/ts-reference/type-ref.html?q=all#%28form._%28%28lib._typed-racket%2Fbase-env%2Fbase-types-extra..rkt%29._.All%29%29">All</a> (A) <a href="https://docs.racket-lang.org/ts-reference/type-ref.html?q=all#%28form._%28%28lib._typed-racket%2Fbase-env%2Fbase-types..rkt%29._.Listof%29%29">(</a><a href="https://docs.racket-lang.org/ts-reference/type-ref.html?q=all#%28form._%28%28lib._typed-racket%2Fbase-env%2Fbase-types..rkt%29._.Listof%29%29">Listof</a> A) <a href="https://docs.racket-lang.org/ts-reference/type-ref.html?q=all#%28form._%28%28lib._typed-racket%2Fbase-env%2Fbase-types-extra..rkt%29._-~3e%29%29">-&gt;</a> <a href="https://docs.racket-lang.org/ts-reference/type-ref.html?q=all#%28form._%28%28lib._typed-racket%2Fbase-env%2Fbase-types..rkt%29._.Natural%29%29">Natural</a><a href="https://docs.racket-lang.org/ts-reference/type-ref.html?q=all#%28form._%28%28lib._typed-racket%2Fbase-env%2Fbase-types..rkt%29._.Natural%29%29">)</a>)

&gt; <a href="https://docs.racket-lang.org/ts-reference/special-forms.html?q=all#%28form._%28%28lib._typed-racket%2Fbase-env%2Fprims..rkt%29._define%29%29">(</a><a href="https://docs.racket-lang.org/ts-reference/special-forms.html?q=all#%28form._%28%28lib._typed-racket%2Fbase-env%2Fprims..rkt%29._define%29%29">define</a> (list-length lst)

<a href="https://docs.racket-lang.org/reference/if.html#%28form._%28%28quote._~23~25kernel%29._if%29%29">(</a><a href="https://docs.racket-lang.org/reference/if.html#%28form._%28%28quote._~23~25kernel%29._if%29%29">if</a> <a href="https://docs.racket-lang.org/reference/pairs.html#%28def._%28%28quote._~23~25kernel%29._null~3f%29%29">(</a><a href="https://docs.racket-lang.org/reference/pairs.html#%28def._%28%28quote._~23~25kernel%29._null~3f%29%29">null?</a> lst)

0

<sub>  </sub><a href="https://docs.racket-lang.org/reference/generic-numbers.html#%28def._%28%28quote._~23~25kernel%29._add1%29%29">(</a><a href="https://docs.racket-lang.org/reference/generic-numbers.html#%28def._%28%28quote._~23~25kernel%29._add1%29%29">add1</a> (list-length <a href="https://docs.racket-lang.org/reference/pairs.html#%28def._%28%28quote._~23~25kernel%29._cdr%29%29">(</a><a href="https://docs.racket-lang.org/reference/pairs.html#%28def._%28%28quote._~23~25kernel%29._cdr%29%29">cdr</a> lst)))))

&gt; (list-length <a href="https://docs.racket-lang.org/reference/pairs.html#%28def._%28%28quote._~23~25kernel%29._list%29%29">(</a><a href="https://docs.racket-lang.org/reference/pairs.html#%28def._%28%28quote._~23~25kernel%29._list%29%29">list</a> 1 2 3))

– : Integer [more precisely: Nonnegative-Integer]

3




In the above example, all elements in the list argument must be of the same (polymorphic) type.





