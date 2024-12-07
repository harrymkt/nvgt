---
title: Character Rotation (rotation.nvgt)
url: docs/references_include_character_rotation_rotation.html
---

<h1>Character Rotation (rotation.nvgt)</h1>
<h2>character rotation</h2>
<p>This include contains functions for moving a rotating character in a 2D or 3D game.</p>
<h3>Disclaimer:</h3>
<p>Though these have been improved over the years and though I do use this myself for Survive the Wild and my other games, it should be understood that I started writing this file in BGT when I was only 12 or 13 years old and it has only been getting improved as needed. The result is that anything from the math to the coding decisions may be less than perfect, putting it kindly. You have been warned!</p>
<h2>Functions</h2>
<h3>calculate_theta</h3>
<p>Calculate the radians value for a given angle in degrees.</p>
<p>double calculate_theta(double deg);</p>
<h4>Arguments:</h4>
<ul>
<li>double deg: the angle to convert, in degrees.</li>
</ul>
<h4>Returns:</h4>
<p>double: the specified angle in radians.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">#include &quot;rotation.nvgt&quot;
void main() {
	alert(&quot;Info&quot;, &quot;45 degrees in radians is &quot; + calculate_theta(45));
}
</code></pre>
<h3>get_1d_distance</h3>
<p>Get the distance between two points on the x axis.</p>
<p>double get_1d_distance(double x1, double x2);</p>
<h4>Arguments:</h4>
<ul>
<li><p>double x1: the first point.</p>
</li>
<li><p>double x2: the second point.</p>
</li>
</ul>
<h4>Returns:</h4>
<p>double: the distance between the two points on the x axis.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">#include &quot;rotation.nvgt&quot;
void main() {
	double x1 = 2.0;
	double x2 = 6.8;
	alert(&quot;The distance between &quot; + x1 + &quot; and &quot; + x2 + &quot; is&quot;, get_1d_distance(x1, x2));
}
</code></pre>
<h3>get_2d_distance</h3>
<p>Get the distance between two x/y points.</p>
<p>double get_2d_distance(double x1, double y1, double x2, double y2);</p>
<h4>Arguments:</h4>
<ul>
<li><p>double x1: the first x point.</p>
</li>
<li><p>double y1: the first y point.</p>
</li>
<li><p>double x2: the second x point.</p>
</li>
<li><p>double y2: the second y point.</p>
</li>
</ul>
<h4>Returns:</h4>
<p>double: the distance between the two points.</p>
<h4>Remarks:</h4>
<p>This function uses the Euclidean distance formula, meaning it will return the possible closest distance between the two points.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">#include &quot;rotation.nvgt&quot;
void main() {
	double x1 = 2.0, y1 = 0.3;
	double x2 = 6.8, y2 = 9.45;
	alert(&quot;The distance between (&quot; + x1 + &quot;, &quot; + y1 + &quot;) and (&quot; + x2 + &quot;, &quot; + y2 + &quot;) is&quot;, get_2d_distance(x1, y1, x2, y2));
}
</code></pre>
<h3>get_3d_distance</h3>
<p>Get the distance between two x/y/z points.</p>
<p>double get_3d_distance(double x1, double y1, double z1, double x2, double y2, double z2);</p>
<h4>Arguments:</h4>
<ul>
<li><p>double x1: the first x point.</p>
</li>
<li><p>double y1: the first y point.</p>
</li>
<li><p>double z1: the first z point.</p>
</li>
<li><p>double x2: the second x point.</p>
</li>
<li><p>double y2: the second y point.</p>
</li>
<li><p>double z2: the second z point.</p>
</li>
</ul>
<h4>Returns:</h4>
<p>double: the distance between the two points.</p>
<h4>Remarks:</h4>
<p>This function uses the Euclidean distance formula, meaning it will return the possible closest distance between the two points.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">#include &quot;rotation.nvgt&quot;
void main() {
	double x1 = 2.0, y1 = 0.3, z1 = 0.0;
	double x2 = 6.8, y2 = 9.45, z2 = 1.942;
	alert(&quot;The distance between (&quot; + x1 + &quot;, &quot; + y1 + &quot;, &quot; + z1 + &quot;) and (&quot; + x2 + &quot;, &quot; + y2 + &quot;, &quot; + z2 + &quot;) is&quot;, get_2d_distance(x1, y1, x2, y2));
}
</code></pre>
<h2>Global Properties</h2>
<h3>direction constants</h3>
<p>This is a list of the various direction constants present in the rotation include. Each constant will be listed, as well as what it represents.</p>
<ul>
<li>int north: 0 degrees.</li>
<li>int northeast: 45 degrees.</li>
<li>int east: 90 degrees.</li>
<li>int southeast: 135 degrees.</li>
<li>int south: 180 degrees.</li>
<li>int southeast: 225 degrees.</li>
<li>int west: 270 degrees.</li>
<li>int northwest: 315 degrees.</li>
<li>int half_up: 45 degrees (upwards).</li>
<li>int straight_up: 90 degrees (upwards).</li>
<li>int half_down: 135 degrees (downwards).</li>
<li>int straight_down: 180 degrees (downwards).</li>
</ul>
<h3>pi</h3>
<p>Holds 32 digits of PI.</p>
<p>const double pi;</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">#include &quot;rotation.nvgt&quot;
void main() {
	alert(&quot;32 digits of PI is&quot;, pi);
}
</code></pre>
