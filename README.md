MathML Acid Tests
=================

*Although the creation of the tests is now complete, I expect to modify some
of them if I get feedback or if I find errors while I write the detailed
description below. Once the tests are considered stable, I plan to submit them 
to organizations like the Math WG or the WaSP, that could publish them and 
provide an official URL. In the meantime, online versions are available on
GitHub:*

* [MathML Acid 2](http://fred-wang.github.com/AcidTestsMathML/acid2/)
* [MathML Acid 3](http://fred-wang.github.com/AcidTestsMathML/acid3/)

This repository contains MathML versions of the famous
[Acid2](http://acid2.acidtests.org) and [Acid3](http://acid3.acidtests.org)
tests. At the time these MathML versions are published, most modern browsers
support the advanced HTML/CSS/SVG/Javascript/DOM features verified by the
classical Acid2 and Acid3 tests but very few have a decent support for even the
simplest mathematical constructions. MathML is a very old W3C standard, now
integrated into HTML5 and EPUB3 so browser vendors can not claim having a
standard-compliant rendering engine when this one lacks a native MathML
implementation.

Perhaps the most popular MathML tests are the
[Mozilla's MathML Torture Test](https://developer.mozilla.org/en-US/docs/Mozilla_MathML_Project/MathML_Torture_Test) or
[Joe Java's MathML test](https://eyeasme.com/Joe/MathML/MathML_browser_test)
where the rendering quality of a few basic constructions is compared against
TeX images and the [W3C's MathML test suite](http://www.w3.org/Math/testsuite)
where a large number of features are tested against sample references.
Unfortunately these tests are not automated and are very subjective. This makes
evaluation and comparison of native MathML implementations a difficult task.

The MathML recommendation almost never describes precisely the
rendering of elements, so exact pixel matching does not make sense in general
as opposed to SVG or CSS.
Here, we use MathML features like `mathbackground='yellow'` or `<mpadded>`
whose visual renderings are clearly defined in order to draw the smiley face
from the Acid2 test.
Most other MathML features can be verified via Javascript by testing
the relative position of boxes (e.g. the numerator is above a denominator
in an `<mfrac>` element) and thus can just be included in the Acid3 test. Hence
the combination of these MathML Acid2 and Acid3 tests should give a pretty
good coverage of MathML features, while still being automated and hopefully
quite objective. This set of tests is not claimed to be perfect, for example
the tests only work with native MathML implementations or do not capture the
subjective but important notion of "good-looking mathematical expressions".
However it has the advantage to quickly provide objective results to people
even those without advanced knowledge of the MathML language.

The goal of these MathML tests is to compare native browser implementations,
they are not supposed to be executed in other MathML layout engines. The result
given for other MathML layout engines (including polyfills) should not be
considered reliable.
The design of these tests is biased: some features like `<mglyph>` or
some `<mstyle>` attributes that are assumed to be less important in a browser
context are not tested at all while some tests require interaction between
MathML and other Web features.
However, many tests make sense out of a browser
context and could be verified by humans, in the same way as the other MathML
tests mentioned above.

The score in the MathML Acid3 test should not be overstated to say for example
that a browser supports 15% or 80% of MathML. Exact pixel matching or rendering
quality is hard to test and so a browser that renders the fraction with a very
large gap between the numerator and denumerator would pass the basic `<mfrac>`
test, while such a rendering would not be considered acceptable by most people.
On the other hand, the three first buckets should be enough to reach a decent
mathematical rendering and supporting only the first one would still provide
readable mathematical expressions.

Acid2
=====

**Perfect pixel matching is not required to pass the test. See below.**

**The MathML code is valid against the MathML RelaxNG schema if HTML `<span>`'s
  are allowed in `<mtext>` elements (e.g. the one used in Validator.nu).**

As said in the introduction, perfect pixel matching is hard to achieve with
MathML elements. As a consequence, the MathML Acid2 only relies on a few
MathML elements whose rendering is well-defined. The requirements to pass the
MathML Acid2 test are:

* All the smiley face (except maybe the nose) should match the reference
  rendering.
* The eyes should be a link pointing to the reference rendering.
* The nose should have the rendering and `hover` effect described in test ??
* The "Hello World!" should be placed as described in test 2 and have the
  aspect described in test 3.

This makes the test a bit less objective but still provides something that
looks like the good old Acid2 test.

Test 1: Invisible Elements
--------------------------

The test verifies that some invisible MathML elements do not appear. These
elements are `<mtext>` or `<semantics>` with HTML content inside as described in
chapter 6. We test the following elements:

* An empty `<mrow>` should not be visible and should have size 0.

* The `<mphantom>` should hide its content. The `<mpadded>` element is used to
  force the size to 0. The combination is equivalent to an empty `<mrow>`.

* The `<maction>` element is used with a `selection` attribute and unknown
  `actiontype`. Only the selected child should appear, not the other children.

* The `<semantics>` element is used to annotate a presentation MathML element.
  Only the annotated element should appear, not the annotations.

Note that even a browser without MathML support might be able to recognize the
HTML content and incorrectly make it visible. Depending on the browser MathML
support and its ability to hide the MathML elements above, various rectangle
of different sizes and colors as well as ERROR messages might show up. This
may recall you the failure of the classical Acid2 test in older browser
versions.

Test 2: mover
-------------

The main element is a `<mover accent="true">` with two children:

* An `<mpadded width="168px" height="84px" depth="84px">` where the the smiley
  face will be drawn.
* An `<mpadded depth="+36px">` that contains the "Hello World!" message.

The first element is a square with side of size 168px. The baseline of its
content is the horizontal symmetric axis. The "Hello World!" message should be
placed over the square and aligned center. **The MathML recommendation does not
specify the vertical gap between the two children** but the `accent="true"`
helps making the overscript closer to the base. The `depth="+36px"` increases
the bottom padding of the "Hello World!" and guarantee that the gap is at
least 36px (value from the classical Acid2). Hence the overall layout should
look like something like

<div style="width: 168px; margin-left: auto; margin-right: auto;">
  <svg width="168px" height="228px">
    <rect x="10px" y="0px" width="148px" height="24px" fill="navy"/>
    <rect x="0px" y="60px" width="168px" height="168px" fill="yellow"/>
  </svg>
</div>

Test 3: Hello World!
--------------------

This message is contained in a `<mtext mathcolor="navy" mathvariant="sans-serif"
mathsize="24px">` element and so should at least have the following properties
(values from the classical Acid2).

* font-size should be 24px. In particular, it is not influenced by the
  scriptlevel incrementation in the `<mover>` overscript.
* characters should be sans-serif.
* color should be `navy` or equivalently `#000080`.

<div style="text-align: center">
  <span style="font: 24px sans-serif; color: #000080;">Hello World!</span>
</div>

Test 4:
-------

...

Acid3
=====

**Note: test 10 contains invalid markup: this is on purpose and intended to 
check error handling!**

...

Bucket 1: Basic Presentation MathML Elements
--------------------------------------------

...

Bucket 2: More Advanced Presentation Attributes
-----------------------------------------------

...

Bucket 3: Displaystyle, Scriptlevel and Operators
-------------------------------------------------

...

Bucket 4: More Features of Operators
------------------------------------

...

Bucket 5: Directionality and Linebreaking
-----------------------------------------

...

Bucket 6: Alignment and Elementary Mathematics
----------------------------------------------

...

Special tests
-------------

...
