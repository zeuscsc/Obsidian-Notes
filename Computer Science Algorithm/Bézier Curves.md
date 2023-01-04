A Bézier curve (/ˈbɛz.i.eɪ/ BEH-zee-ay) is a parametric curve used in computer graphics and related fields. A set of discrete "control points" defines a smooth, continuous curve by means of a formula. Usually the curve is intended to approximate a real-world shape that otherwise has no mathematical representation or whose representation is unknown or too complicated. The Bézier curve is named after French engineer Pierre Bézier (1910–1999), who used it in the 1960s for designing curves for the bodywork of Renault cars. Other uses include the design of computer fonts and animation. Bézier curves can be combined to form a Bézier spline, or generalized to higher dimensions to form Bézier surfaces. The Bézier triangle is a special case of the latter.
![[Pasted image 20221213102426.png]]
![[Pasted image 20221213102422.png]]
## What is it so good about it?
1. Can get slop and tangent of a specific point easily
2. Same goes to velocity and accretion
Which means it is good for phyisc simulation.  Maybe that's why Maya is not a good tools for production but Autocadesk Alias and SolidWork are good for product production.

You can create a Bézier Curves easily in HTML.

~~~js
bezierCurveTo(cp1x, cp1y, cp2x, cp2y, x, y)
~~~

~~~js
const canvas = document.getElementById('canvas');
const ctx = canvas.getContext('2d');

ctx.beginPath();
ctx.moveTo(30, 30);
ctx.bezierCurveTo(120,160, 180,10, 220,140);
ctx.stroke();
~~~

