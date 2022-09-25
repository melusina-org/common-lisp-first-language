# Evaluation of Physics Formulas and LET


## Last session recap

We used Lisp REPL to evaluate numeric expressions such as `(+ 1 2 3 4)`
or `(/ (* 2 11) 7)`. We also used the `float` function to ask the
Lisp REPL to convert exact rational expressions into
approximated floating point values as in the following example:

~~~ lisp
CL-USER> (float 22/7)
3.142857
CL-USER> (float (/ (* 2 11) 7))
3.142857
~~~

## Duration of free fall

Newton mechanics provide a model for predicting the acceleration,
speed and distance covered by a free falling body near the surface of
Earth. Such bodies are meteors, sky-divers, jumping athletes,
catapulted stones or apple falling from their tree for instance.

In this model, we can predict the time that a free falling object
needs to cover the distance to the ground: if $h$ is the starting
height that small object, the time it needs to cover the distance to
the ground is given by

$$ \sqrt{ 2h \over g }$$

where $g \simeq 9.81 \mathrm{m}/\mathrm{s}^2$ is the so called
*free-fall acceleration due to gravity*.  An important and somewhat
counter-intuitive result displayed by the model is that this duration
only depends of the starting height of the body and none of its other
characteristics such as weight or density.

In Lisp the square root function is denoted by `sqrt` and provides an
approximated result as a floating point number, for instance

~~~
CL-USER> (sqrt 2)
1.4142135
~~~

So if an apple falls from a heigth of 9.50m, the time it needs to cover
the distance to the ground is computed in Lisp by evaluating

~~~
CL-USER> (sqrt (/ (* 2 9.5) 9.81))
1.3916893
~~~

which yields an approximated duration of 1.40 seconds.

**Question 1.** Poor Newton is sleeping under the tree on the trajectory
of the apple. The top of his head is at 0.65m above the ground. How to
change the previous computation to know how long the apple needs to
reach his head? (This new duration is about 1.34 seconds.)

**Question 2.** A glass falls from a table of heigth 0.85m, how long
does it take for it reach the floor?


## The LET special operator

Expressions featuring several number and nested evaluations such as
the one we used to compute the [duration of free fall](#Duration-of-free-fall)
can be hard to read and cryptic. It is maybe hard to recognise the
expression `(sqrt (/ (* 2 9.5) 9.81))` as a special case of

$$ \sqrt{ 2h \over g }$$

but the LET special operator in Lisp allows us to rewrite the
expression
~~~ lisp
(sqrt (/ (* 2 9.5) 9.81))
~~~
as
~~~
(sqrt (/ (* 2 h) g))
~~~
provided we take time we expalin what $h$ and $g$ stand for. We can
write
~~~
CL-USER> (let ((h 9.5)
               (g 9.81))
	   (sqrt (/ (* 2 h) g)))
1.3916893
~~~
which reads, using common terminology from algebra, “let $h$ be 9.5
and let $g$ be 9.81 in the expression `(sqrt (/ (* 2 h) g))`.

Normally in Lisp, the first word of an expression is a function such
as `+` or `sqrt` but an expression starting with `let` is evaluted
following different rules than the ones used for function, this is
why `let` is called a *special operator*.

**Question 3.** How to modify the LET expression above to answer
Questions 1 and 2?

**Question 4.** Near the surface of the Moon *free-fall acceleration
due to gravity* is approximately equal to $1.63 \mathrm{m}/\mathrm{s}^2$
instead of $9.81 \mathrm{m}/\mathrm{s}^2$ near the surface of the
Earth. How long does a hammer released from a heigth of 1.60m above
the surface of the moon needs to reach the ground? A feather?


## Research problem

Select a physics formulas or a geometric formulas and evaluate with
Lisp on specific parameters. Use the LET special operator so that it
easy to read the evaluated expression and confirm it matches the
formula used in the source.

As an inspiration, here is a list of topics to look into:

 - The computation of distances, areas and surfaces;
 - The surface of triangles on a sphere; 
 - The acoustic properties of a vibrating string;
 - The oscillations of a pendulum

A supplementary source of inspiration could be found in a mathematics
of physics high-school textbook.

Common mathematical functions and constants are available in Common
Lisp:

 - The Archimedes number $\pi$ (PI): `pi`;
 - The trigonometric functions sinus and cosinus: `sin` and `cos`;
 - The natural exponential and logarithm: `exp` and `log`.
 - The square root of a positive number: `sqrt`.

Example:

~~~
CL-USER> (- (cos (/ pi 4)) (/ (sqrt 2) 2))
1.2101617152815436d-8
~~~

