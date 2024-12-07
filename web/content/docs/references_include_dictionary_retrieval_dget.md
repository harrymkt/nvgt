---
title: Dictionary Retrieval (dget.nvgt)
url: docs/references_include_dictionary_retrieval_dget.html
---

<h1>Dictionary Retrieval (dget.nvgt)</h1>
<h2>Dictionary retrieval functions</h2>
<p>The way you get values out of AngelScript dictionaries by default is fairly annoying, mainly due to its usage of out values instead of returning them. Hence this include, which attempts to simplify things.</p>
<h2>functions</h2>
<h3>dgetb</h3>
<p>Get a boolean value out of a dictionary.</p>
<p><code>bool dgetn(dictionary@ the_dictionary, string key, bool def = false);</code></p>
<h4>Arguments:</h4>
<ul>
<li>dictionary@ the_dictionary: a handle to the dictionary to get the value from.</li>
<li>string key: the key of the value to look up.</li>
<li>bool def = false: the value to return if the key wasn't found.</li>
</ul>
<h4>Returns:</h4>
<p>bool: the value for the particular key in the dictionary, or the default value if not found.</p>
<h3>dgetn</h3>
<p>Get a numeric value out of a dictionary.</p>
<p><code>double dgetn(dictionary@ the_dictionary, string key, double def = 0.0);</code></p>
<h4>Arguments:</h4>
<ul>
<li>dictionary@ the_dictionary: a handle to the dictionary to get the value from.</li>
<li>string key: the key of the value to look up.</li>
<li>double def = 0.0: the value to return if the key wasn't found.</li>
</ul>
<h4>Returns:</h4>
<p>double: the value for the particular key in the dictionary, or the default value if not found.</p>
<h3>dgets</h3>
<p>Get a string value out of a dictionary.</p>
<p><code>string dgets(dictionary@ the_dictionary, string key, string def = 0.0);</code></p>
<h4>Arguments:</h4>
<ul>
<li>dictionary@ the_dictionary: a handle to the dictionary to get the value from.</li>
<li>string key: the key of the value to look up.</li>
<li>string def = &quot;&quot;: the value to return if the key wasn't found.</li>
</ul>
<h4>Returns:</h4>
<p>string: the value for the particular key in the dictionary, or the default value if not found.</p>
<h3>dgetsl</h3>
<p>Get a string array out of a dictionary.</p>
<p><code>string[] dgetsl(dictionary@ the_dictionary, string key, string[] def = []);</code></p>
<h4>Arguments:</h4>
<ul>
<li>dictionary@ the_dictionary: a handle to the dictionary to get the value from.</li>
<li>string key: the key of the value to look up.</li>
<li>string[] def = []: the value to return if the key wasn't found.</li>
</ul>
<h4>Returns:</h4>
<p>string[]: the value for the particular key in the dictionary, or the default value if not found.</p>
<h4>Remarks:</h4>
<p>The default value for this function is a completely empty (but initialized) string array.</p>
