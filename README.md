MathML Acid Tests
=================

*Although the creation of the tests is now complete, I expect to modify some
of them if I get feedback or if I find errors while I write the detailed
description below. Once the tests are considered stable, I plan to submit them 
to organizations like the Math WG or the WaSP, that could publish them and 
provide an official URL. In the meantime, online versions are available on
GitHub:*

* [MathML Acid 2](http://fred-wang.github.com/AcidTestsMathML/acid2/)
  ([description](http://fred-wang.github.com/AcidTestsMathML/acid2/description.html))
* [MathML Acid 3](http://fred-wang.github.com/AcidTestsMathML/acid3/)
  ([description](http://fred-wang.github.com/AcidTestsMathML/acid3/description.html))

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
