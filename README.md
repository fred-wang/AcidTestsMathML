MathML Acid Tests
=================

*Although the creation of the tests is now complete, I expect to modify some
of them if I get feedback or if I find errors while I write the detailed
description below. Once the tests are considered stable, I plan to submit them 
to organizations like the Math WG or the WaSP, that could publish them and 
provide an official URL. In the meantime, online versions are available on
GitHub:*

* [MathML Acid 1](http://fred-wang.github.com/AcidTestsMathML/acid1/)
  ([description](http://fred-wang.github.com/AcidTestsMathML/acid1/description.html))
* [MathML Acid 2](http://fred-wang.github.com/AcidTestsMathML/acid2/)
  ([description](http://fred-wang.github.com/AcidTestsMathML/acid2/description.html))
* [MathML Acid 3](http://fred-wang.github.com/AcidTestsMathML/acid3/)
  ([description](http://fred-wang.github.com/AcidTestsMathML/acid3/description.html))

This repository contains MathML versions of the famous
[Acid Tests](http://www.acidtests.org/)
([Acid1](http://acid1.acidtests.org), [Acid2](http://acid2.acidtests.org) and
[Acid3](http://acid3.acidtests.org)).
At the time these MathML versions are published, most modern browsers
support the advanced HTML/CSS/SVG/Javascript/DOM features verified by the
classical Acid tests but very few have a decent support for even the
simplest mathematical constructions. MathML is a very old W3C standard, now
integrated into HTML5 and EPUB3 so browser vendors can not claim having a
standard-compliant rendering engine when this one lacks a native MathML
implementation. Incidentally, here are some references if you wish to follow the development of MathML in browsers:

* Blink (e.g. Chrome and Opera): [Chromium Dashboard](http://www.chromestatus.com/features/5240822173794304), [Enable MathML](https://code.google.com/p/chromium/issues/detail?id=152430)
* Gecko (e.g. Firefox): [Implementation Status](https://developer.mozilla.org/en-US/docs/Mozilla/MathML_Project/Status), [MathML 2](https://bugzilla.mozilla.org/show_bug.cgi?id=525772), [MathML 3](https://bugzilla.mozilla.org/show_bug.cgi?id=534959), [MathJax](https://bugzilla.mozilla.org/show_bug.cgi?id=687809)
* Trident (e.g. Internet Explorer): [status.modern.ie](http://status.modern.ie/mathml). [All the bug reports for MathML](https://connect.microsoft.com/IE/SearchResults.aspx?SearchQuery=mathml) have been resolved "by design" so far.
* WebKit (e.g. Safari): [Implementation Status](https://trac.webkit.org/wiki/MathML%20Status), [Master Bug](https://bugs.webkit.org/show_bug.cgi?id=3251), [Basic Support](https://bugs.webkit.org/show_bug.cgi?id=99623), [MathJax](https://bugs.webkit.org/show_bug.cgi?id=84019)

Of course these Acid tests are not perfect, for example they do not
capture the subjective but important notion of "good-looking mathematical
expressions". Also, they are supposed to be executed in browsers ; the result
for other MathML layout engines (including polyfills) should not be considered
reliable. However, these tests have the advantage to quickly provide objective
results to people even those without advanced knowledge of the MathML language. 
Many tests make sense out of a browser context and could be verified by
non-browser MathML implementers.

Perhaps the most popular MathML tests are the
[Mozilla's MathML Torture Test](https://developer.mozilla.org/en-US/docs/Mozilla_MathML_Project/MathML_Torture_Test) or
[Joe Java's MathML test](https://eyeasme.com/Joe/MathML/MathML_browser_test)
where the rendering quality of a few basic constructions is compared against
TeX images and the [W3C's MathML test suite](http://www.w3.org/Math/testsuite)
where a large number of features are tested against sample references.
Unfortunately these tests are not automated and are very subjective. This makes
evaluation and comparison of native MathML implementations a difficult task.
Since the MathML Acid1 test contains very elementary MathML constructions, we
keep this subjective evaluation method. Any rendering that looks more or less
like the reference and satisfies the basic requirements could be accepted.

The MathML recommendation almost never describes precisely the
rendering of elements, so exact pixel matching does not make sense in general
as opposed to SVG or CSS. For the MathML Acid2 test,
we use MathML features like `mathbackground='yellow'` or `<mpadded>`
whose visual renderings are clearly defined in order to draw the smiley face.
Most other MathML features can be verified via Javascript by testing
the relative position of boxes (e.g. the numerator is above a denominator
in an `<mfrac>` element). These features are verified in the MathML Acid3 test.
Hence the combination of these MathML Acid2 and Acid3 tests should give a pretty
good coverage of MathML features, while still being automated and hopefully
quite objective.
