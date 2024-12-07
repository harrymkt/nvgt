---
title: Math
url: docs/references_builtin_math.html
---

<h1>Math</h1>
<h2>Classes</h2>
<h3>vector</h3>
<p>A class containing x, y and z coordinates, usually used to represent a 3d point in space.</p>
<ol>
<li><p>vector();</p>
</li>
<li><p>vector(const vector&amp; in vec);</p>
</li>
<li><p>vector(float x, float y = 0.0, float z = 0.0);</p>
</li>
</ol>
<h4>Arguments (3):</h4>
<ul>
<li><p>float x: The initial x point or coordinate this vector represents.</p>
</li>
<li><p>float y = 0.0: The initial y point or coordinate this vector represents.</p>
</li>
<li><p>float z = 0.0: The initial z point or coordinate this vector represents, defaulted to 0 because it may not be needed in some 2d applications.</p>
</li>
</ul>
<h4>Remarks:</h4>
<p>An advantage with vectors is that they contain basic addition and scaling operators.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	vector v1(5, 5, 5);
	vector v2(10, 10, 0);
	vector v3 = v1 + v2;
	alert(&quot;example&quot;, &quot;the new vector is &quot;+v3.x + &quot;, &quot; + v3.y + &quot;, &quot; + v3.z); // will show that the vector is 15, 15, 5.
}
</code></pre>
<h4>Operators</h4>
<h5>opAssign</h5>
<p>Overloads the = operator, allowing you to assign a vector to another, already existing one.</p>
<p>vector&amp; opAssign(const vector &amp;in other);</p>
<h6>Arguments:</h6>
<p>const vector&amp; in other: the vector to assign to.</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	vector v1;
	vector v2(1.2, 2.3, 9.3);
	v1 = v2;
	alert(&quot;The first vector =&quot;, &quot;(&quot; + round(v1.x, 2) + &quot;, &quot; + round(v1.y, 2) + &quot;, &quot; + round(v1.z, 2) + &quot;)&quot;);
}
</code></pre>
<h4>Properties</h4>
<h5>x</h5>
<p>Represents the x coordinate of the vector.</p>
<p>float vector::x;</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	vector v(2.9);
	alert(&quot;The x value of the vector is&quot;, round(v.x, 2));
}
</code></pre>
<h5>y</h5>
<p>Represents the y coordinate of the vector.</p>
<p>float vector::y;</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	vector v(2.9, 19.2);
	alert(&quot;The y value of the vector is&quot;, round(v.y, 2));
}
</code></pre>
<h5>z</h5>
<p>Represents the z coordinate of the vector.</p>
<p>float vector::z;</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	vector v(2.9, 19.2, 4.1);
	alert(&quot;The z value of the vector is&quot;, round(v.z, 2));
}
</code></pre>
<h2>Functions</h2>
<h3>abs</h3>
<p>Returns the absolute value of a value.</p>
<p>double abs(double x);</p>
<h4>Arguments:</h4>
<ul>
<li>double x: The value whose absolute value is to be calculated.</li>
</ul>
<h4>Returns:</h4>
<p>The absolute value of the given value.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	alert(&quot;Example&quot;, &quot;The absolute value of -5 is &quot; + abs(-5));
}
</code></pre>
<h3>acos</h3>
<p>Returns the arc cosine of a value in radians.</p>
<p>double acos(double x);</p>
<h4>Arguments:</h4>
<ul>
<li>double x: The value whose arc cosine is to be calculated.</li>
</ul>
<h4>Returns:</h4>
<p>The arc cosine of the given value.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
    alert(&quot;Example&quot;, &quot;The arc cosine of 0.5 is &quot; + acos(0.5) + &quot; radians&quot;);
}
</code></pre>
<h3>asin</h3>
<p>Returns the arc sine of a value in radians.</p>
<p>double asin(double x);</p>
<h4>Arguments:</h4>
<ul>
<li>double x: The value whose arc sine is to be calculated.</li>
</ul>
<h4>Returns:</h4>
<p>The arc sine of the given value.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
    alert(&quot;Example&quot;, &quot;The arc sine of 0.5 is &quot; + asin(0.5) + &quot; radians&quot;);
}
</code></pre>
<h3>atan</h3>
<p>Returns the arc tangent of a value in radians.</p>
<p>double atan(double x);</p>
<h4>Arguments:</h4>
<ul>
<li>double x: The value whose arc tangent is to be calculated.</li>
</ul>
<h4>Returns:</h4>
<p>The arc tangent of the given value.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
    alert(&quot;Example&quot;, &quot;The arc tangent of 1 is &quot; + atan(1) + &quot; radians&quot;);
}
</code></pre>
<h3>atan2</h3>
<p>Returns the arc tangent of y/x, where y and x are the coordinates of a point.</p>
<p>double atan2(double y, double x);</p>
<h4>Arguments:</h4>
<ul>
<li><p>double y: The ordinate coordinate.</p>
</li>
<li><p>double x: The abscissa coordinate.</p>
</li>
</ul>
<h4>Returns:</h4>
<p>The arc tangent of y/x.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
    alert(&quot;Example&quot;, &quot;The arc tangent of (1, 2) is &quot; + atan2(1, 2) + &quot; radians&quot;);
}
</code></pre>
<h3>ceil</h3>
<p>Returns the smallest integer greater than or equal to a value.</p>
<p>double ceil(double x);</p>
<h4>Arguments:</h4>
<ul>
<li>double x: The value whose ceiling is to be calculated.</li>
</ul>
<h4>Returns:</h4>
<p>The smallest integer greater than or equal to x.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	alert(&quot;Example&quot;, &quot;The ceiling of 3.14 is &quot; + ceil(3.14));
}
</code></pre>
<h3>cos</h3>
<p>Returns the cosine of an angle given in radians.</p>
<p>double cos(double x);</p>
<h4>Arguments:</h4>
<ul>
<li>double x: The angle (in radians) to get the cosine of.</li>
</ul>
<h4>Returns:</h4>
<p>The cosine of the angle.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	alert(&quot;Example&quot;, &quot;The cosine of 45 is &quot; + cos(45 * 3.14159 / 180) + &quot; radians&quot;);
}
</code></pre>
<h3>cosh</h3>
<p>Returns the hyperbolic cosine of a value.</p>
<p>double cosh(double x);</p>
<h4>Arguments:</h4>
<ul>
<li>double x: The value whose hyperbolic cosine is to be calculated.</li>
</ul>
<h4>Returns:</h4>
<p>The hyperbolic cosine of the given value.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
    alert(&quot;Example&quot;, &quot;The hyperbolic cosine of 2 is &quot; + cosh(2));
}
</code></pre>
<h3>floor</h3>
<p>Returns the largest integer less than or equal to a value.</p>
<p>double floor(double x);</p>
<h4>Arguments:</h4>
<ul>
<li>double x: The value whose floor is to be calculated.</li>
</ul>
<h4>Returns:</h4>
<p>The largest integer less than or equal to x.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	alert(&quot;Example&quot;, &quot;The floor of 3.14 is &quot; + floor(3.14));
}
</code></pre>
<h3>fraction</h3>
<p>Returns the fractional part of a value.</p>
<p>double fraction(double x);</p>
<h4>Arguments:</h4>
<ul>
<li>double x: The value whose fractional part is to be extracted.</li>
</ul>
<h4>Returns:</h4>
<p>The fractional part of the given value.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	alert(&quot;Example&quot;, &quot;The fractional part of 3.75 is &quot; + fraction(3.75));
}
</code></pre>
<h3>log</h3>
<p>Returns the natural logarithm (base e) of a value.</p>
<p>double log(double x);</p>
<h4>Arguments:</h4>
<ul>
<li>double x: The value whose natural logarithm is to be calculated.</li>
</ul>
<h4>Returns:</h4>
<p>The natural logarithm of the given value.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
    alert(&quot;Example&quot;, &quot;The natural logarithm of 10 is &quot; + log(10));
}
</code></pre>
<h3>log10</h3>
<p>Returns the base 10 logarithm of a value.</p>
<p>double log10(double x);</p>
<h4>Arguments:</h4>
<ul>
<li>double x: The value whose base 10 logarithm is to be calculated.</li>
</ul>
<h4>Returns:</h4>
<p>The base 10 logarithm of the given value.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
    alert(&quot;Example&quot;, &quot;The base 10 logarithm of 100 is &quot; + log10(100));
}
</code></pre>
<h3>pow</h3>
<p>Returns x raised to the power of y.</p>
<p>double pow(double x, double y);</p>
<h4>Arguments:</h4>
<ul>
<li><p>double x: The base.</p>
</li>
<li><p>double y: The exponent.</p>
</li>
</ul>
<h4>Returns:</h4>
<p>x raised to the power of y.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
    alert(&quot;Example&quot;, &quot;2 raised to the power of 3 is &quot; + pow(2, 3));
}
</code></pre>
<h3>round</h3>
<p>Returns the value of a number rounded to the nearest integer.</p>
<p>double round(double n, int p);</p>
<h4>Arguments:</h4>
<ul>
<li><p>double n: The number to be rounded.</p>
</li>
<li><p>int p: The number of decimal places to round to.</p>
</li>
</ul>
<h4>Returns:</h4>
<p>The value of the number rounded to the nearest integer.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	alert(&quot;Example&quot;, &quot;Rounding 3.14159 to 2 decimal places gives &quot; + round(3.14159, 2));
}
</code></pre>
<h3>sin</h3>
<p>Returns the sine of an angle given in radians.</p>
<p>double sin(double x);</p>
<h4>Arguments:</h4>
<ul>
<li>double x: The angle (in radians) to get the sine of.</li>
</ul>
<h4>Returns:</h4>
<p>The sine of the angle.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	alert(&quot;Example&quot;, &quot;The sine of 45 is &quot; + sin(45 * 3.14159 / 180) + &quot; radians&quot;);
}
</code></pre>
<h3>sinh</h3>
<p>Returns the hyperbolic sine of a value.</p>
<p>double sinh(double x);</p>
<h4>Arguments:</h4>
<ul>
<li>double x: The value whose hyperbolic sine is to be calculated.</li>
</ul>
<h4>Returns:</h4>
<p>The hyperbolic sine of the given value.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
    alert(&quot;Example&quot;, &quot;The hyperbolic sine of 2 is &quot; + sinh(2));
}
</code></pre>
<h3>sqrt</h3>
<p>Returns the square root of a value.</p>
<p>double sqrt(double x);</p>
<h4>Arguments:</h4>
<ul>
<li>double x: The value whose square root is to be calculated.</li>
</ul>
<h4>Returns:</h4>
<p>The square root of the given value.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	alert(&quot;Example&quot;, &quot;The square root of 16 is &quot; + sqrt(16));
}
</code></pre>
<h3>tan</h3>
<p>Returns the tangent of an angle given in radians.</p>
<p>double tan(double x);</p>
<h4>Arguments:</h4>
<ul>
<li>double x: The angle (in radians) to get the tangent of.</li>
</ul>
<h4>Returns:</h4>
<p>The tangent of the angle.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	alert(&quot;Example&quot;, &quot;The tangent of 45 is &quot; + tan(45 * 3.14159 / 180) + &quot; radians&quot;);
}
</code></pre>
<h3>tanh</h3>
<p>Returns the hyperbolic tangent of a value.</p>
<p>double tanh(double x);</p>
<h4>Arguments:</h4>
<ul>
<li>double x: The value whose hyperbolic tangent is to be calculated.</li>
</ul>
<h4>Returns:</h4>
<p>The hyperbolic tangent of the given value.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
    alert(&quot;Example&quot;, &quot;The hyperbolic tangent of 2 is &quot; + tanh(2));
}
</code></pre>
<h3>tinyexpr</h3>
<p>Evaluate a mathematical expression using the tinyexpr library.</p>
<p>double tinyexpr(string expression);</p>
<h4>Arguments:</h4>
<ul>
<li>string expression: the expression to evaluate.</li>
</ul>
<h4>Returns:</h4>
<p>double: the result of the expression.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	string expression = input_box(&quot;Expression&quot;, &quot;Enter expression to evaluate&quot;);
	if (expression.is_empty()) exit();
	alert(&quot;Result&quot;, expression + &quot;= &quot; + tinyexpr(expression));
}
</code></pre>
