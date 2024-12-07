---
title: Data Manipulation
url: docs/references_builtin_data_manipulation.html
---

<h1>Data Manipulation</h1>
<h2>Classes</h2>
<h3>json_array</h3>
<h4>Methods</h4>
<h5>add</h5>
<p>Add a value to the end of a JSON array.</p>
<p>void json_array::add(var@ value);</p>
<h6>Arguments:</h6>
<ul>
<li>var@ value: a handle to the value to be set.</li>
</ul>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	json_array@ arr = parse_json(&quot;[]&quot;);
	for (uint i = 0; i &lt; 5; i++)
		arr.add(random(1, 100));
	alert(&quot;Filled array&quot;, arr.stringify());
}
</code></pre>
<h5>clear</h5>
<p>Clears the JSON array completely.</p>
<p>void json_array::clear();</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	string data = &quot;[1, 2, 3, 4, 5]&quot;;
	json_array@ arr = parse_json(data);
	alert(&quot;Before being cleared&quot;, arr.stringify());
	arr.clear();
	alert(&quot;After being cleared&quot;, arr.stringify());
}
</code></pre>
<h5>is_array</h5>
<p>Determine if the value at the given index is a JSON array or not.</p>
<p>bool json_array::is_array(uint index);</p>
<h6>Arguments:</h6>
<ul>
<li>uint index: the position of the item.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the value at the specified index is a JSON array, false otherwise.</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	json_array@ arr = parse_json(&quot;[[1, 2], [3, 4]]&quot;);
	alert(&quot;Info&quot;, arr.is_array(1) ? &quot;It is an array&quot;: &quot;It is not an array&quot;);
}
</code></pre>
<h5>is_null</h5>
<p>Determine if the value at the given index is null.</p>
<p>bool json_array::is_null(uint index);</p>
<h6>Arguments:</h6>
<ul>
<li>uint index: the position of the item.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the value at the specified index is null, false otherwise.</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	json_array@ arr = parse_json(&quot;[1, 2, null, 4]&quot;);
	alert(&quot;Info&quot;, &quot;Index 1 &quot; + (arr.is_null(1) ? &quot; is null&quot;: &quot; is not null&quot;));
	alert(&quot;Info&quot;, &quot;Index 2 &quot; + (arr.is_null(2) ? &quot; is null&quot;: &quot; is not null&quot;));
}
</code></pre>
<h5>is_object</h5>
<p>Determine if the value at the given index is a JSON object.</p>
<p>bool json_array::is_object(uint index);</p>
<h6>Arguments:</h6>
<ul>
<li>uint index: the position of the item.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the value at the specified index is a JSON object, false otherwise.</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	json_array@ arr = parse_json(&quot;&quot;&quot;[{}, {}, &quot;test&quot;, {}]&quot;&quot;&quot;);
	alert(&quot;Info&quot;, &quot;Position 0 &quot; + (arr.is_object(0) ? &quot;is an object&quot; : &quot;is not an object&quot;));
	alert(&quot;Info&quot;, &quot;Position 2 &quot; + (arr.is_object(2) ? &quot;is an object&quot;: &quot;is not an object&quot;));
}
</code></pre>
<h5>remove</h5>
<p>Remove a value from the JSON array given an index.</p>
<p>void json_array::remove(uint index);</p>
<h6>Arguments:</h6>
<ul>
<li>uint index: the index of the value to remove.</li>
</ul>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	string data = &quot;&quot;&quot;[47, 4, 584, 43, 8483]&quot;&quot;&quot;;
	json_array@ arr = parse_json(data);
	alert(&quot;Initial&quot;, arr.stringify());
	arr.remove(2);
	alert(&quot;After removal&quot;, arr.stringify());
}
</code></pre>
<h5>size</h5>
<p>Return the size of the JSON array.</p>
<p>uint json_array::size();</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	string data = &quot;[&quot;;
	for (int i = 0; i &lt; random(10, 20); i++)
		data += i + &quot;, &quot;;
	// Strip off the trailing comma and space character, as they'll make the JSON throw a syntax error.
	data.erase(data.length() - 1);
	data.erase(data.length() - 1);
	data += &quot;]&quot;;
	clipboard_set_text(data);
	json_array@ arr = parse_json(data);
	alert(&quot;Info&quot;, &quot;The JSON array contains &quot; + arr.size() + &quot; items&quot;);
}
</code></pre>
<h5>stringify</h5>
<p>Return the JSON array as a string.</p>
<p>string json_array::stringify(int indent = 0, int step = -1);</p>
<h6>Arguments:</h6>
<ul>
<li><p>int indent = 0: specifies how many spaces to use to indent the JSON. If 0, no indentation or formatting is performed.</p>
</li>
<li><p>int step = -1: the outwards indentation step, for example setting it to two would cause your outdents to only be two spaces. -1 (the default) keeps it how it is, normally you don't need to use this parameter.</p>
</li>
</ul>
<h6>Returns:</h6>
<p>string: the JSON array as a string.</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	string data = &quot;&quot;&quot;[&quot;Apple&quot;, &quot;Banana&quot;, &quot;Orange&quot;, &quot;Lemon&quot;]&quot;&quot;&quot;;
	json_array@ arr = parse_json(data);
	alert(&quot;JSON array&quot;, arr.stringify(4));
}
</code></pre>
<h4>Operators</h4>
<h5>get_opIndex</h5>
<p>Get a value out of the JSON array with literal syntax, for example <code>arr[2]</code>.</p>
<p>var@ json_array::get_opIndex(uint index) property;</p>
<h6>Arguments:</h6>
<ul>
<li>uint index: the index of the value to get.</li>
</ul>
<h6>Returns:</h6>
<p>var@: a handle to the object, or null if not found.</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	json_array@ cats = parse_json(&quot;&quot;&quot;[&quot;Athena&quot;, &quot;Willow&quot;, &quot;Punk&quot;, &quot;Franky&quot;, &quot;Yoda&quot;, &quot;Waffles&quot;]&quot;&quot;&quot;);
	alert(&quot;The third cat is&quot;, cats[2]);
	for (uint i = 0; i &lt; cats.size(); i++)
		alert(&quot;Awww&quot;, &quot;Hi &quot; + cats[i]);
}
</code></pre>
<h5>opCall</h5>
<p>Get a value out of a JSON array using a query.</p>
<p>var@ json_array::opCall(string query);</p>
<h6>Arguments:</h6>
<ul>
<li>string query: the JSON query (see the remarks section for details).</li>
</ul>
<h6>Returns:</h6>
<p>var@: a handle to the object, or null if it couldn't be found.</p>
<h6>Remarks:</h6>
<p>Queries are formatted like so, using key names and indexes separated with &quot;.&quot;:</p>
<blockquote>
<p>world.player.0</p>
</blockquote>
<p>It can be as nested as you like.</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	string data = &quot;&quot;&quot;[[[&quot;Colorado&quot;, &quot;Kansas&quot;, &quot;Minnesota&quot;]]]&quot;&quot;&quot;;
	json_array@ arr = parse_json(data);
	string location = arr(&quot;0.0.0&quot;);
	alert(&quot;My favorite state is&quot;, location);
}
</code></pre>
<h5>set_opIndex</h5>
<p>Set a value in the JSON array at a particular position.</p>
<p>void json_array::set_opIndex(uint index, var@ value) property;</p>
<h6>Arguments:</h6>
<ul>
<li><p>uint index: the index to insert the item at.</p>
</li>
<li><p>var@ value: the value to set.</p>
</li>
</ul>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	json_array@ arr = parse_json(&quot;[]&quot;);
	arr[0] = &quot;meow&quot;;
	alert(&quot;Info&quot;, &quot;Cats say &quot; + arr[0]);
}
</code></pre>
<h4>Properties</h4>
<h5>empty</h5>
<p>Determine if the JSON array is empty.</p>
<p>const bool json_array::empty;</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	json_array@ arr = parse_json(&quot;[]&quot;);
	json_array@ arr2 = parse_json(&quot;[1, 2, 3]&quot;);
	alert(&quot;First is empty&quot;, arr.empty ? &quot;true&quot; : &quot;false&quot;);
	alert(&quot;Second is empty&quot;, arr2.empty ? &quot;true&quot; : &quot;false&quot;);
}
</code></pre>
<h5>escape_unicode</h5>
<p>Determines the amount of escaping that occurs in JSON parsing.</p>
<p><code>bool json_array::escape_unicode;</code></p>
<h6>Remarks:</h6>
<p>If this property is true, escaping will behave like normal. If it's false, only the characters absolutely vital to JSON parsing are escaped.</p>
<h3>json_object</h3>
<h4>Methods</h4>
<h5>clear</h5>
<p>Clears the JSON object completely.</p>
<p>void json_object::clear();</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	string data = &quot;&quot;&quot;{&quot;numbers&quot;: [1, 2, 3, 4, 5]}&quot;&quot;&quot;;
	json_object@ o = parse_json(data);
	alert(&quot;Before being cleared&quot;, o.stringify());
	o.clear();
	alert(&quot;After being cleared&quot;, o.stringify());
}
</code></pre>
<h5>exists</h5>
<p>Determine if a key exists in the JSON object.</p>
<p>bool json_object::exists(const string?&amp;in key);</p>
<h6>Arguments:</h6>
<ul>
<li>const string&amp;in key: the key to search for.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the key exists, false if not.</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	string data = &quot;&quot;&quot;{&quot;engine&quot;: &quot;NVGT&quot;}&quot;&quot;&quot;;
	json_object@ o = parse_json(data);
	alert(&quot;Info&quot;, (o.exists(&quot;engine&quot;) ? &quot;The key exists&quot; : &quot;The key does not exist&quot;));
}
</code></pre>
<h5>get_keys</h5>
<p>Get a list of all the keys in the JSON object.</p>
<p>string[]@ json_object::get_keys();</p>
<h6>Returns:</h6>
<p>string[]@: a handle to an array of strings containing all the keys of the JSON object.</p>
<h6>Remarks:</h6>
<p>Note that this function isn't recursive, you only get the keys for the object you're running this function on, not any child objects.</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	string data = &quot;&quot;&quot;{&quot;thing&quot;: 1, &quot;other_thing&quot;: &quot;test&quot;, &quot;another&quot;: true}&quot;&quot;&quot;;
	json_object@ o = parse_json(data);
	string[]@ keys = o.get_keys();
	alert(&quot;The keys are&quot;, join(keys, &quot;, &quot;));
}
</code></pre>
<h5>is_array</h5>
<p>Determine if the value with the given key is a JSON array or not.</p>
<p>bool json_object::is_array(string key);</p>
<h6>Arguments:</h6>
<ul>
<li>string key: the key to query.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the value with the specified key is a JSON array, false otherwise.</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	string data = &quot;&quot;&quot;{&quot;classes&quot;: [&quot;json_object&quot;, &quot;json_array&quot;]}&quot;&quot;&quot;;
	json_object@ o = parse_json(data);
	alert(&quot;Info&quot;, o.is_array(&quot;classes&quot;) ? &quot;array&quot;: &quot;nonarray&quot;);
}
</code></pre>
<h5>is_null</h5>
<p>Determine if the value with the given key is null.</p>
<p>bool json_object::is_null(string key);</p>
<h6>Arguments:</h6>
<ul>
<li>string key: the key to query.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the value with the specified key is null.</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	string data = &quot;&quot;&quot;{&quot;brain&quot;: null}&quot;&quot;&quot;;
	json_object@ o = parse_json(data);
	alert(&quot;Info&quot;, o.is_null(&quot;brain&quot;) ? &quot;null&quot; : &quot;not null&quot;);
}
</code></pre>
<h5>is_object</h5>
<p>Determine if the value with the given key is a JSON object or not.</p>
<p>bool json_object::is_object(string key);</p>
<h6>Arguments:</h6>
<ul>
<li>string key: the key to query.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the value with the specified key is a JSON object, false otherwise.</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	string data = &quot;&quot;&quot;{&quot;json_object&quot;: {\}\}&quot;&quot;&quot;;
	json_object@ o = parse_json(data);
	alert(&quot;Info&quot;, o.is_object(&quot;json_object&quot;) ? &quot;Object&quot; : &quot;Non-object&quot;);
}
</code></pre>
<h5>remove</h5>
<p>Remove a value from the JSON object given a key.</p>
<p>void json_object::remove(const string&amp;in key);</p>
<h6>Arguments:</h6>
<ul>
<li>const string&amp;in key: the key of the value to remove.</li>
</ul>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	string data = &quot;&quot;&quot;{&quot;name&quot;: &quot;Quin&quot;}&quot;&quot;&quot;;
	json_object@ o = parse_json(data);
	alert(&quot;Initial&quot;, o.stringify());
	o.remove(&quot;name&quot;);
	alert(&quot;After removal&quot;, o.stringify());
}
</code></pre>
<h5>set</h5>
<p>Set a value in a JSON object.</p>
<p>void json_object::set(const string&amp;in key, var@ value);</p>
<h6>Arguments:</h6>
<ul>
<li><p>const string&amp;in key: the key to give the value.</p>
</li>
<li><p>var@ value: a handle to the value to be set.</p>
</li>
</ul>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	json_object@ o = parse_json(&quot;{}&quot;);;
	o.set(&quot;nvgt_user&quot;, true);
	alert(&quot;Info&quot;, (bool(o[&quot;nvgt_user&quot;]) ? &quot;You are an NVGT user&quot; : &quot;You are not a regular NVGT user&quot;));
}
</code></pre>
<h5>size</h5>
<p>Return the size of the JSON object.</p>
<p>uint json_object::size();</p>
<h6>Remarks:</h6>
<p>Note that this function returns the number of top-level keys; it's not recursive.</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	string data = &quot;&quot;&quot;{&quot;numbers&quot;: [1, 2, 3, 4, 5]}&quot;&quot;&quot;;
	json_object@ o = parse_json(data);
	alert(&quot;Info&quot;, &quot;The json object's size is &quot; + o.size());
}
</code></pre>
<h5>stringify</h5>
<p>Return the JSON object as a string.</p>
<p>string json_object::stringify(int indent = 0, int step = -1);</p>
<h6>Arguments:</h6>
<ul>
<li><p>int indent = 0: specifies how many spaces to use to indent the JSON. If 0, no indentation or formatting is performed.</p>
</li>
<li><p>int step = -1: the outwards indentation step, for example setting it to two would cause your outdents to only be two spaces. -1 (the default) keeps it how it is, normally you don't need to use this parameter.</p>
</li>
</ul>
<h6>Returns:</h6>
<p>string: the JSON object as a string.</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	string data = &quot;&quot;&quot;{&quot;name&quot;: &quot;Quin&quot;, &quot;age&quot;: 18}&quot;&quot;&quot;;
	json_object@ o = parse_json(data);
	alert(&quot;JSON object&quot;, o.stringify(4));
}
</code></pre>
<h4>Operators</h4>
<h5>get_opIndex</h5>
<p>Get a value out of the JSON object with literal syntax, for example <code>json[&quot;key&quot;]</code>.</p>
<p>var@ json_object::get_opIndex(const string&amp;in key) property;</p>
<h6>Arguments:</h6>
<ul>
<li>const string&amp;in key: the key of the object to get.</li>
</ul>
<h6>Returns:</h6>
<p>var@: a handle to the object, or null if not found.</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	string data = &quot;&quot;&quot;{&quot;name&quot;: &quot;Quin&quot;, &quot;age&quot;: 18}&quot;&quot;&quot;;
	json_object@ o = parse_json(data);
	alert(&quot;Info&quot;, o[&quot;name&quot;] + &quot; is &quot; + o[&quot;age&quot;]);
}
</code></pre>
<h5>opCall</h5>
<p>Get a value out of a JSON object using a query.</p>
<p>var@ json_object::opCall(const string&amp;in query);</p>
<h6>Arguments:</h6>
<ul>
<li>const string&amp;in query: the JSON query (see the remarks section for details).</li>
</ul>
<h6>Returns:</h6>
<p>var@: a handle to the object, null if not found.</p>
<h6>Remarks:</h6>
<p>Queries are formatted like so:</p>
<blockquote>
<p>first_field.subfield.subfield</p>
</blockquote>
<p>It can be as nested as you like.</p>
<p>This method also works on json_array's, and you access array indexes just with their raw numbers, like so:</p>
<blockquote>
<p>world.players.0</p>
</blockquote>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	string data = &quot;&quot;&quot;{&quot;countries&quot;:{&quot;us&quot;:[&quot;Colorado&quot;, &quot;Kansas&quot;, &quot;Minnesota&quot;]\}\}&quot;&quot;&quot;;
	json_object@ o = parse_json(data);
	string locations = o(&quot;countries.us&quot;);
	alert(&quot;My favorite states are&quot;, locations);
}
</code></pre>
<h5>set_opIndex</h5>
<p>Set a value in the JSON object with a particular key.</p>
<p>void json_object::set_opIndex(const string&amp;in key, var@ value) property;</p>
<h6>Arguments:</h6>
<ul>
<li><p>const string&amp;in key: the key of the object.</p>
</li>
<li><p>var@ value: the value to set.</p>
</li>
</ul>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	json_object@ o = parse_json(&quot;{}&quot;);
	o[&quot;name&quot;] = &quot;Quin&quot;;
	alert(&quot;Hi&quot;, &quot;I am &quot; + o[&quot;name&quot;]);
}
</code></pre>
<h4>Properties</h4>
<h5>escape_unicode</h5>
<p>Determines the amount of escaping that occurs in JSON parsing.</p>
<p><code>bool json_object::escape_unicode;</code></p>
<h6>Remarks:</h6>
<p>If this property is true, escaping will behave like normal. If it's false, only the characters absolutely vital to JSON parsing are escaped.</p>
<h3>pack</h3>
<h4>methods</h4>
<h5>add_file</h5>
<p>Add a file on disk to a pack.</p>
<p><code>bool pack::add_file(const string&amp;in disk_filename, const string&amp;in pack_filename, bool allow_replace = false);</code></p>
<h6>Arguments:</h6>
<ul>
<li>const string&amp;in disk_filename: the filename of the file to add to the pack.</li>
<li>const string&amp;in pack_filename: the name the file should have in your pack.</li>
<li>bool allow_replace = false: if a file already exists in the pack with that name, should it be overwritten?</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the file was successfully added, false otherwise.</p>
<h5>add_memory</h5>
<p>Add content stored in memory to a pack.</p>
<p><code>bool pack::add_memory(const string&amp;in pack_filename, const string&amp;in data, bool replace = false);</code></p>
<h6>Arguments:</h6>
<ul>
<li>const string&amp;in pack_filename: the name the file should have in your pack.</li>
<li>const string&amp;in data: a string containing the data to be added.</li>
<li>bool allow_replace = false: if a file already exists in the pack with that name, should it be overwritten?</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the data was successfully added, false otherwise.</p>
<h5>close</h5>
<p>Closes a pack, freeing all its resources.</p>
<p><code>bool pack::close();</code></p>
<h6>Returns:</h6>
<p>bool: true if the pack was successfully closed, false otherwise.</p>
<h5>delete_file</h5>
<p>Attempt to remove a file from a pack.</p>
<p><code>bool pack::delete_file(const string&amp;in filename);</code></p>
<h6>Arguments:</h6>
<ul>
<li>const string&amp;in filename: the name of the file to be deleted.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the file was successfully deleted, false otherwise.</p>
<h5>file_exists</h5>
<p>Query whether or not a file exists in your pack.</p>
<p><code>bool pack::file_exists(const string&amp;in filename);</code></p>
<h6>Arguments:</h6>
<ul>
<li>const string&amp;in filename: the name of the file to query.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the file exists in the pack, false if not.</p>
<h5>get_file_name</h5>
<p>Get the name of a file with a particular index.</p>
<p><code>string pack::get_file_name(int index);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int index: the index of the file to retrieve (see remarks).</li>
</ul>
<h6>Returns:</h6>
<p>string: the name of the file if found, or an empty string if not.</p>
<h6>Remarks:</h6>
<p>The index you pass to this function is the same index you'd use to access an element in the return value from <code>pack::list_files()</code>.</p>
<h5>get_file_offset</h5>
<p>Get the offset of a file in your pack.</p>
<p><code>uint pack::get_file_offset(const string&amp;in filename);</code></p>
<h6>Arguments:</h6>
<ul>
<li>const string&amp;in filename: the name of the file to get the offset of.</li>
</ul>
<h6>Returns:</h6>
<p>uint: the offset of the file (in bytes).</p>
<h6>Remarks:</h6>
<p>Do not confuse this with the offset parameter in the pack::read_file method. This function is provided encase you wish to re-open the pack file with your own file object and seek to a file's data within that external object. The offset_in_file parameter in the read_file method is relative to the file being read.</p>
<h5>get_file_size</h5>
<p>Returns the size of a particula file in the pack.</p>
<p><code>uint pack::get_file_size(const string&amp;in filename);</code></p>
<h6>Arguments:</h6>
<ul>
<li>const string&amp;in filename: the name of the file to query the size of.</li>
</ul>
<h6>Returns:</h6>
<p>uint: the size of the file (in bytes), or 0 if no file with that name was found.</p>
<h5>list_files</h5>
<p>Get a list of all the files in the pack.</p>
<p><code>string[]@ pack::list_files();</code></p>
<h6>Returns:</h6>
<p>string[]@: a handle to an array of strings containing the names of every file in the pack.</p>
<h5>open</h5>
<p>Open a pack to perform operations on it.</p>
<p><code>bool pack::open(const string&amp;in filename, uint mode, bool memload = false);</code></p>
<h6>Arguments:</h6>
<ul>
<li>const string&amp;in filename: the name of the pack file to open.</li>
<li>uint mode: the mode to open the pack in (see <code>pack_open_modes</code> for more information).</li>
<li>bool memload = false: whether or not the pack should be loaded from memory as opposed to on disk.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the pack was successfully opened with the given mode, false otherwise.</p>
<h5>read_file</h5>
<p>Get the contents of a file contained in a pack.</p>
<p><code>string pack::read_file(const string&amp;in pack_filename, uint offset_in_file, uint size);</code></p>
<h6>Arguments:</h6>
<ul>
<li>const string&amp;in pack_filename: the name of the file to be read.</li>
<li>uint offset_in_file: the offset within the file to begin reading data from (do not confuse this with pack::get_file_offset)</li>
<li>uint size: the number of bytes to read (see <code>pack::get_file_size</code> to read the entire file).</li>
</ul>
<h6>Returns:</h6>
<p>string: the contents of the file.</p>
<h6>Remarks:</h6>
<p>This function allows you to read chunks of data from a file, as well as an entire file in one call. To facilitate this, the offset and size parameters are provided. offset is relative to the file being read E. 0 for the beginning of it. So to read a file in one chunk, you could execute:</p>
<pre><code>string file_contents = my_pack.read_file(&quot;filename&quot;, 0, my_pack.get_file_size(&quot;filename&quot;));
</code></pre>
<h5>set_pack_identifier</h5>
<p>Set the identifier of this pack object (e.g. the first 8-bytes that determine if you have a valid pack or not).</p>
<p><code>bool pack::set_pack_identifier(const string&amp;in ident);</code></p>
<h6>Arguments:</h6>
<ul>
<li>const string&amp;in ident: the new identifier (see remarks).</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the pack's identifier was properly set, false otherwise.</p>
<h6>Remarks:</h6>
<ul>
<li>The default pack identifier is &quot;NVPK&quot; followed by 4 NULL bytes.</li>
<li>Your pack identifier should be 8 characters or less. If it's less than 8 characters, 0s will be added as padding on the end. If it's larger than 8, the first 8 characters will be used.</li>
</ul>
<h3>regexp</h3>
<p>The regexp object allows for the easy usage of regular expressions in NVGT.</p>
<p>regexp(const string&amp;in pattern, int options = RE_UTF8);</p>
<h4>Arguments:</h4>
<ul>
<li><p>const string&amp;in pattern: the regular expression's pattern (see remarks).</p>
</li>
<li><p>int options = RE_UTF8: a combination of any of the values from the <code>regexp_options</code> enum.</p>
</li>
</ul>
<h4>Remarks:</h4>
<p>Regular expressions are a language used for matching, substituting, and otherwise manipulating text. To learn about the regular expression syntax that nVGT uses (called PCRE), see this link: https://en.wikipedia.org/wiki/Perl_Compatible_Regular_Expressions</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	regexp re(&quot;^[a-z]{2,4}$&quot;); // Will match any lowercase alphabetical string between 2 and 4 characters in length.
	string compare = input_box(&quot;Text&quot;, &quot;Enter the text to check against the regular expression.&quot;);
	if (compare.empty()) {
		alert(&quot;Regular expression tester&quot;, &quot;You didn't type a string to test.&quot;);
		exit(1);
	}
	bool matches = re.match(compare);
	alert(&quot;The regular expression&quot;, matches ? &quot;matches&quot; : &quot;does not match&quot;);
}
</code></pre>
<h4>methods</h4>
<h5>match</h5>
<p>Determine if the regular expression matches against a particular string or not.</p>
<ol>
<li><code>bool regexp::match(const string&amp;in subject, uint64 offset = 0);</code></li>
<li><code>bool regexp::match(const string&amp;in subject, uint64 offset, int options);</code></li>
</ol>
<h6>Arguments (1):</h6>
<ul>
<li>const string&amp;in subject: the string to compare against.</li>
<li>uint64 offset = 0: the offset to start the comparison at.</li>
</ul>
<h6>Arguments (2):</h6>
<ul>
<li>const string&amp;in subject: the string to compare against.</li>
<li>uint64 offset: the offset to start the comparison at.</li>
<li>int options: any combination of the values found in the <code>regexp_options</code> enum.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the regular expression matches the given string, false if not.</p>
<h2>Enums</h2>
<h3>pack_open_modes</h3>
<p>This is a list of all the possible open modes to be passed to the <code>pack::open()</code> function.</p>
<ul>
<li>PACK_OPEN_MODE_NONE.</li>
<li>PACK_OPEN_MODE_APPEND: open the pack and append data to it.</li>
<li>PACK_OPEN_MODE_CREATE: create a new pack.</li>
<li>PACK_OPEN_MODE_READ: open the pack for reading.</li>
</ul>
<h3>regexp_options</h3>
<p>This enum holds various constants that can be passed to the regular expression classes in order to change their behavior.</p>
<h4>Notes:</h4>
<p>Portions of this regexp_options documentation were Copied from POCO header files.</p>
<ul>
<li>Options marked [ctor] can be passed to the constructor of regexp objects.</li>
<li>Options marked [match] can be passed to match, extract, split and subst.</li>
<li>Options marked [subst] can be passed to subst.</li>
</ul>
<p>See the PCRE documentation for more information.</p>
<h4>Constants:</h4>
<ul>
<li>RE_CASELESS: case insensitive matching (/i) [ctor]</li>
<li>RE_MULTILINE: enable multi-line mode; affects ^ and $ (/m) [ctor]</li>
<li>RE_DOTALL: dot matches all characters, including newline (/s) [ctor]</li>
<li>RE_EXTENDED: totally ignore whitespace (/x) [ctor]</li>
<li>RE_ANCHORED: treat pattern as if it starts with a ^ [ctor, match]</li>
<li>RE_DOLLAR_END_ONLY: dollar matches end-of-string only, not last newline in string [ctor]</li>
<li>RE_EXTRA: enable optional PCRE functionality [ctor]</li>
<li>RE_NOT_BOL: circumflex does not match beginning of string [match]</li>
<li>RE_NOT_EOL: $ does not match end of string [match]</li>
<li>RE_UNGREEDY: make quantifiers ungreedy [ctor]</li>
<li>RE_NOT_EMPTY: empty string never matches [match]</li>
<li>RE_UTF8: assume pattern and subject is UTF-8 encoded [ctor]</li>
<li>RE_NO_AUTO_CAPTURE: disable numbered capturing parentheses [ctor, match]</li>
<li>RE_NO_UTF8_CHECK: do not check validity of UTF-8 code sequences [match]</li>
<li>RE_FIRSTLINE: an unanchored pattern is required to match before or at the first newline in the subject string, though the matched text may continue over the newline [ctor]</li>
<li>RE_DUPNAMES: names used to identify capturing subpatterns need not be unique [ctor]</li>
<li>RE_NEWLINE_CR: assume newline is CR ('\r'), the default [ctor]</li>
<li>RE_NEWLINE_LF: assume newline is LF ('\n') [ctor]</li>
<li>RE_NEWLINE_CRLF: assume newline is CRLF (&quot;\r\n&quot;) [ctor]</li>
<li>RE_NEWLINE_ANY: assume newline is any valid Unicode newline character [ctor]</li>
<li>RE_NEWLINE_ANY_CRLF: assume newline is any of CR, LF, CRLF [ctor]</li>
<li>RE_GLOBAL: replace all occurrences (/g) [subst]</li>
<li>RE_NO_VARS: treat dollar in replacement string as ordinary character [subst]</li>
</ul>
<h2>Functions</h2>
<h3>ascii_to_character</h3>
<p>Return the character that corresponds to the given ascii value.</p>
<p>string ascii_to_character(uint8 ascii);</p>
<h4>Arguments:</h4>
<ul>
<li>uint8 ascii: the ascii value to convert.</li>
</ul>
<h4>Returns:</h4>
<p>string: the character for the given ascii value.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	uint8 ascii = parse_int(input_box(&quot;ASCII value&quot;, &quot;Enter the ascii value to convert.&quot;));
	alert(&quot;Info&quot;, ascii + &quot; has a value of &quot; + ascii_to_character(ascii));
}
</code></pre>
<h3>character_to_ascii</h3>
<p>Return the ascii value for the given character.</p>
<p>uint8 character_to_ascii(const string&amp;in character);</p>
<h4>Arguments:</h4>
<ul>
<li>const string&amp;in character: the character to convert.</li>
</ul>
<h4>Returns:</h4>
<p>uint8: the ascii value for the given character.</p>
<h4>Remarks:</h4>
<p>If a string containing more than one character is passed as input to this function, only the left-most character is checked.</p>
<p>If an empty string is passed, the function returns 0.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	string character = input_box(&quot;Character&quot;, &quot;Enter a character to convert&quot;);
	if (character.is_empty()) {
		alert(&quot;Error&quot;, &quot;You did not type anything.&quot;);
		exit();
	}
	if (character.length() != 1) { // The user typed more than one character.
		alert(&quot;Error&quot;, &quot;You must only type a single character.&quot;);
		exit();
	}
	alert(&quot;Info&quot;, character + &quot; has an ascii value of &quot; + character_to_ascii(character));
}
</code></pre>
<h3>join</h3>
<p>turn an array into a string, with each element being separated by the given delimiter.</p>
<p>string join(const string[]@ elements, const string&amp;in delimiter);</p>
<h4>Arguments:</h4>
<ul>
<li><p>const string[]@ elements: a handle to the array to join.</p>
</li>
<li><p>const string&amp;in delimiter: the delimiter used to separate each element in the array (can be empty).</p>
</li>
</ul>
<h4>Returns:</h4>
<p>string: the given array as a string.</p>
<h4>Remarks:</h4>
<p>If an empty array is passed, a blank string is returned.</p>
<p>The delimiter is not appended to the end of the last item in the returned string. For example if an array contains [1, 2, 3] and you join it with a delimiter of . (period), the result would be &quot;1.2.3&quot; without an extra delimiter appended.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	string[] names = {&quot;Sam&quot;, &quot;Quin&quot;, &quot;Patrick&quot;};
	string people = join(names, &quot;, &quot;);
	alert(&quot;Info&quot;, people);
}
</code></pre>
<h3>number_to_words</h3>
<p>Convert a number into its string equivalent, for example, one thousand four hundred and fifty six.</p>
<p>string number_to_words(int64 the_number, bool include_and = true);</p>
<h4>Arguments:</h4>
<ul>
<li><p>int64 the_number: the number to convert.</p>
</li>
<li><p>bool include_and = true: whether or not to include the word &quot;and&quot; in the output.</p>
</li>
</ul>
<h4>Returns:</h4>
<p>string: the specified number, converted to a readable string.</p>
<h4>Remarks:</h4>
<p>At this time, this function only produces English results.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	int64 num = random(1000, 100000);
	string result = number_to_words(num);
	alert(&quot;Info&quot;, num + &quot; as a string is &quot; + result);
}
</code></pre>
<h3>pack_set_global_identifier</h3>
<p>Set the global identifier of all your packs (e.g. the first 8-bytes that determine if you have a valid pack or not).</p>
<p><code>bool pack_set_global_identifier(const string&amp;in ident);</code></p>
<h4>Arguments:</h4>
<ul>
<li>const string&amp;in ident: the new identifier (see remarks).</li>
</ul>
<h4>Returns:</h4>
<p>bool: true if the identifier was properly set, false otherwise.</p>
<h4>Remarks:</h4>
<ul>
<li>The default pack identifier is &quot;NVPK&quot; followed by 4 NULL bytes.</li>
<li>Your pack identifier should be 8 characters or less. If it's less than 8 characters, 0s will be added as padding on the end. If it's larger than 8, the first 8 characters will be used.</li>
<li>NVGT will refuse to open any pack files that do not match this identifier.</li>
</ul>
<h3>regexp_match</h3>
<p>Test if the text matches the specified regular expression.</p>
<p>bool regexp_match(const string&amp;in text, const string&amp;in pattern);</p>
<h4>Arguments:</h4>
<ul>
<li><p>const string&amp;in text: the text to compare against the regular expression.</p>
</li>
<li><p>const string&amp;in pattern: the regular expression to match.</p>
</li>
</ul>
<h4>Returns:</h4>
<p>bool: true if the text matches the given regular expression, false otherwise.</p>
<h4>Remarks:</h4>
<p>If you would like a lower level interface to regular_expressions in NVGT, check out the regexp class which this function more or less wraps.</p>
<p>To learn more about regular expressions, visit: https://en.wikipedia.org/wiki/Regular_expression</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	bool match = regexp_match(&quot;Test&quot;, &quot;^[a-zA-Z]+$&quot;);
	alert(&quot;the regular expression&quot;, match ? &quot;matches&quot; : &quot;does not match&quot;);
}
</code></pre>
<h3>string_base32_decode</h3>
<p>Decodes a string from base32.</p>
<p>string string_base32_decode(const string&amp;in the_data);</p>
<h4>Arguments:</h4>
<ul>
<li>const string&amp;in the_data: The data that is to be decoded.</li>
</ul>
<h4>Returns:</h4>
<p>String: The decoded string on success or an empty string on failure.</p>
<h4>Remarks:</h4>
<p>You can learn more about the base32 format <a href="https://en.wikipedia.org/wiki/Base32">here</a>.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	string text = input_box(&quot;Text&quot;, &quot;Enter the text to decode.&quot;);
	if (text.is_empty()) {
		alert(&quot;Error&quot;, &quot;You did not type any text.&quot;);
		exit();
	}
	alert(&quot;Info&quot;, string_base32_decode(text));
}
</code></pre>
<h3>string_base32_encode</h3>
<p>Encodes a string as base32.</p>
<p>string string_base32_encode(const string&amp;in the_data);</p>
<h4>Arguments:</h4>
<ul>
<li>const string&amp;in the_data: The data that is to be encoded.</li>
</ul>
<h4>Returns:</h4>
<p>String: The encoded string on success or an empty string on failure.</p>
<h4>Remarks:</h4>
<p>You can learn more about the base32 format <a href="https://en.wikipedia.org/wiki/Base32">here</a>.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	string text = input_box(&quot;Text&quot;, &quot;Enter the text to encode.&quot;);
	if (text.is_empty()) {
		alert(&quot;Error&quot;, &quot;You did not type any text.&quot;);
		exit();
	}
	alert(&quot;Info&quot;, string_base32_encode(text));
}
</code></pre>
<h3>string_base32_normalize</h3>
<p>Normalize a string to conform to the base32 spec.</p>
<p>string string_base32_normalize(const string&amp;in the_data);</p>
<h4>Arguments:</h4>
<ul>
<li>const string&amp;in the_data: the string to normalize.</li>
</ul>
<h4>Returns:</h4>
<p>string: the normalized string.</p>
<h4>Remarks:</h4>
<p>The primary thing this function does is to skip separators, convert all letters to uppercase, and make sure the length is a multiple of 8.</p>
<p>To learn more about base32, click <a href="https://en.wikipedia.org/wiki/Base32">here</a>.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	string text = input_box(&quot;Text&quot;, &quot;Enter the text to normalize.&quot;);
	if (text.is_empty()) {
		alert(&quot;Error&quot;, &quot;You didn't type anything.&quot;);
		exit();
	}
	alert(&quot;Info&quot;, string_base32_normalize(text));
}
</code></pre>
<h3>string_base64_decode</h3>
<p>Decodes a string which has previously been encoded in base64.</p>
<p>string string_base64_decode(const string&amp;in the_data, string_base64_options options = STRING_BASE64_PADLESS);</p>
<h4>Arguments:</h4>
<ul>
<li><p>const string&amp;in the_data: The data that is to be decoded.</p>
</li>
<li><p>string_base64_options options = STRING_BASE64_PADLESS: A bitwise of options that control the behavior of the decoding (see remarks).</p>
</li>
</ul>
<h4>Returns:</h4>
<p>String: The decoded string on success or an empty string on failure.</p>
<h4>Remarks:</h4>
<p>The following options may be passed to the options argument of this function:</p>
<ul>
<li><p>STRING_BASE64_DEFAULT: The defaults passed to the string_base64_encode function.</p>
</li>
<li><p>STRING_BASE64_URL: Use base64 URL encoding as opposed to the / and = characters.</p>
</li>
<li><p>STRING_BASE64_PADLESS: Allows decoding even if the string does not end with = padding characters.</p>
</li>
</ul>
<p>You can learn more about base64 <a href="https://en.wikipedia.org/wiki/Base64">here.</a></p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	alert(&quot;example&quot;, string_base64_decode(&quot;aGVsbG8=&quot;)); // Should print &quot;hello&quot;.
}
</code></pre>
<h3>string_base64_encode</h3>
<p>Encodes a string as base64.</p>
<p>string string_base64_encode(const string&amp;in the_data, string_base64_options options = STRING_BASE64_DEFAULT);</p>
<h4>Arguments:</h4>
<ul>
<li><p>const string&amp;in the_data: The data that is to be encoded.</p>
</li>
<li><p>string_base64_options options = STRING_BASE64_DEFAULT: A bitwise of options that control the behavior of the encoding (see remarks).</p>
</li>
</ul>
<h4>Returns:</h4>
<p>String: The encoded string on success or an empty string on failure.</p>
<h4>Remarks:</h4>
<p>The following options may be passed to the options argument of this function:</p>
<ul>
<li><p>STRING_BASE64_DEFAULT: The default options (i.e. insert padding and do not use URL encoding).</p>
</li>
<li><p>STRING_BASE64_URL: Use base64 URL encoding as opposed to the / and = characters.</p>
</li>
<li><p>STRING_BASE64_PADLESS: Allows decoding even if the string does not end with = padding characters.</p>
</li>
</ul>
<p>You can learn more about base64 <a href="https://en.wikipedia.org/wiki/Base64">here.</a></p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	alert(&quot;example&quot;, string_base64_encode(&quot;Hello&quot;)); // Should print SGVsbG8=
}
</code></pre>
<h2>Global Properties</h2>
<h3>pack_global_identifier</h3>
<p>Represents the identifier currently being used for all your packs.</p>
<p><code>const string pack_global_identifier;</code></p>
