---
title: Size Conversions (size.nvgt)
url: docs/references_include_size_conversions_size.html
---

<h1>Size Conversions (size.nvgt)</h1>
<h2>Size Conversions Include</h2>
<p>This include provides a simple function to convert an unsigned int to a human readable size. It also provides a few very useful size constants.</p>
<h2>Functions</h2>
<h3>size_to_string</h3>
<p>Converts an unsigned int into a human-readable size.</p>
<p>string size_to_string(uint64 size, uint8 round_place = 2);</p>
<h4>Arguments:</h4>
<ul>
<li><p>uint64 size: the size to convert.</p>
</li>
<li><p>uint8 round_place = 2: how many decimal places to round the sizes to.</p>
</li>
</ul>
<h4>Returns:</h4>
<p>The given size as a human-readable string.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">#include &quot;size.nvgt&quot;
void main() {
	uint64[] sizes = {193, 3072, 1048576, 3221225472, 1099511627776, 35184372088832};
	string results;
	for (uint i = 0; i &lt; sizes.length(); i++)
		results += sizes[i] + &quot; bytes = &quot; + size_to_string(sizes[i]) + &quot;,\n&quot;;
	// Strip off the trailing comma and new line.
	results.trim_whitespace_right_this();
	results.erase(results.length() - 1);
	alert(&quot;Results&quot;, results);
}
</code></pre>
<h2>Global Properties</h2>
<h3>GIGABYTES</h3>
<p>The number of bytes in a gigabyte.</p>
<p>const uint GIGABYTES;</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">#include &quot;size.nvgt&quot;
void main() {	
	alert(&quot;Info&quot;, &quot;A gigabyte is &quot; + GIGABYTES + &quot; bytes&quot;);
}
</code></pre>
<h3>KILOBYTES</h3>
<p>The number of bytes in a kilobyte.</p>
<p>const uint KILOBYTES;</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">#include &quot;size.nvgt&quot;
void main() {
	alert(&quot;Info&quot;, &quot;10 kilobytes is &quot; + 10 * KILOBYTES + &quot; bytes&quot;);
}
</code></pre>
<h3>MEGABYTES</h3>
<p>The number of bytes in a megabyte.</p>
<p>const uint MEGABYTES;</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">#include &quot;size.nvgt&quot;
void main() {
	alert(&quot;Info&quot;, &quot;19 megabytes is &quot; + 19 * MEGABYTES + &quot; bytes&quot;);
}
</code></pre>
<h3>SIZE_TO_STRING_UNITS</h3>
<p>String array of all the supported units for size_to_string().</p>
<p>const array<string> SIZE_TO_STRING_UNITS;</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">#include &quot;size.nvgt&quot;
void main() {
	string possible_units;
	for (uint i = 0; i &lt; SIZE_TO_STRING_UNITS.length(); i++)
		possible_units += SIZE_TO_STRING_UNITS[i] + &quot;,\n&quot;;
	// Strip off the trailing comma and new line.
	possible_units.trim_whitespace_right_this();
	possible_units.erase(possible_units.length() - 1);
	alert(&quot;Info&quot;, &quot;The possible units are: &quot; + possible_units + &quot;.&quot;);
}
</code></pre>
<h3>TERABYTES</h3>
<p>The number of bytes in a terabyte.</p>
<p>const uint TERABYTES;</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">#include &quot;size.nvgt&quot;
void main() {	
	alert(&quot;Info&quot;, &quot;A terabyte is &quot; + TERABYTES + &quot; bytes&quot;);
}
</code></pre>
