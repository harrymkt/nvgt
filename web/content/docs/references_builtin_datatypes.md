---
title: Datatypes
url: docs/references_builtin_datatypes.html
---

<h1>Datatypes</h1>
<p>In this documentation, we consider a datatype to be any class or primitive that typically stores one value. While such a datatype could contain a pointer/handle to a more complex type that may store many values (in which case the handle itself is the single value the datatype contains), the types documented here do not directly contain more than one piece of data be that a string of text, a dynamically typed handle or just a simple number.</p>
<p>Beware that a few of these datatypes may get quite advanced, and you are not expected to understand what all of them do (particularly the dynamically typed ones) during the course of normal game development. Instead, we recommend learning about basic datatypes here, and then coming back and looking at any that seemed confusing at first glance when you are trying to solve a particular problem usually relating to a variable you have that needs to be able to store more than one kind of value.</p>
<h2>any</h2>
<p>A class that can hold one object of any type, most similar to a dictionary in terms of usage but with only one value and thus no keys.</p>
<ol>
<li><p>any();</p>
</li>
<li><p>any(?&amp;in value);</p>
</li>
</ol>
<h3>Arguments (2):</h3>
<ul>
<li>?&amp;in value: The default value stored in this object.</li>
</ul>
<h3>Remarks:</h3>
<p>Though NVGT uses Angelscript which is a statically typed scripting language, there are sometimes occasions when one may not know the type of value that could be stored in a variable, or may want to create a function that can accept an argument of any type. While this isn't the only way to do so, the any object provides a safe way to accomplish this task, possibly the safest / least restrictive of all available such options. There should be no type that this object can't store.</p>
<p>The biggest downside to this class is simply that storing and retrieving values from it is just as bulky as the usual way of doing so from dictionary objects. That is, when retrieving a value one must first create a variable then call the any::retrieve() method passing a reference to that variable.</p>
<p>something to note is that the constructor of this class is not marked explicit, meaning that if you create a function that takes an any object as it's argument, the user would then be able to directly pass any type to that argument of your function without any extra work.</p>
<p>Again just like with dictionaries, there is no way to determine the type of a stored value. Instead if one wants to print the value contained within one of these variables, they must carefully attempt the retrieval with different types until it succeeds where the value can then be printed.</p>
<h3>Example:</h3>
<pre><code class="language-NVGT">// Lets create a version of the join function that accepts an array of any objects and supports numbers, strings, and vectors.
string anyjoin(any@[]@ args, const string&amp;in delimiter) {
	if (@args == null) return &quot;&quot;; // Nobody should ever be passing the null keyword to this function, but if they do this line prevents an exception.
	string[] args_as_strings;
	for (uint i = 0; i &lt; args.length() &amp;&amp; args[i] != null; i++) {
		// We must attempt retrieving each type we wish to support.
		int64 arg_int;
		double arg_double;
		string arg_string;
		vector arg_vector;
		if (args[i].retrieve(arg_string)) args_as_strings.insert_last(arg_string);
		else if (args[i].retrieve(arg_vector)) args_as_strings.insert_last(&quot;(%0, %1, %2)&quot;.format(arg_vector.x, arg_vector.y, arg_vector.z));
		else if (args[i].retrieve(arg_double)) args_as_strings.insert_last(arg_double);
		else if (args[i].retrieve(arg_int)) args_as_strings.insert_last(arg_int);
		else args_as_strings.insert_last(&quot;&lt;unknown type&gt;&quot;);
	}
	return join(args_as_strings, delimiter);
}
void main() {
	string result = anyjoin({&quot;the player has&quot;, 5, &quot;lives, has&quot;, 32.97, &quot;percent health, and is at&quot;, vector(10, 15, 0)}, &quot; &quot;);
	alert(&quot;example&quot;, result);
}
</code></pre>
<h3>Methods</h3>
<h4>retrieve</h4>
<p>Fetch the value from an any object and store it in a variable.</p>
<p><code>bool retrieve(?&amp;out result);</code></p>
<h5>Arguments:</h5>
<ul>
<li>?&amp;out result: A variable that the value should be copied into.</li>
</ul>
<h5>Returns:</h5>
<p>bool: true if successful, false if the variable supplied is of the wrong type.</p>
<h5>Example:</h5>
<p>See the main any chapter where this function is used several times.</p>
<h4>store</h4>
<p>Store a new value in an any object, replacing an existing one.</p>
<p>void store(?&amp;in value);</p>
<h5>Arguments:</h5>
<ul>
<li>?&amp;in value: The value that should be stored (can be any type).</li>
</ul>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	int number;
	string text;
	any example;
	example.store(&quot;hello&quot;);
	example.retrieve(text); // Check the return value of the retrieve function for success if you are not certain of what type is stored.
	example.store(42); // The previous text value has now been deleted.
	example.retrieve(number);
	alert(text, number);
}
</code></pre>
<h2>ref</h2>
<p>A class that can hold an extra reference to a handle of any type.</p>
<ol>
<li><p>ref();</p>
</li>
<li><p>ref(const ?&amp;in handle);</p>
</li>
</ol>
<h3>Arguments (2):</h3>
<ul>
<li>const ?&amp;in handle: The handle that this ref object should store at construction.</li>
</ul>
<h3>Remarks:</h3>
<p>In Angelscript, a handle is the simplest method of pointing multiple variables at a single object, or passing an object to a function without copying it in memory. If you know any c++, it is sort of like a c++ shared pointer. You can only create a handle to a complex object, and a few built-in NVGT objects do not support them such as the random number generators because they are registered as value types. Describing handles much further is beyond the scope of this reference chapter, but you can <a href="https://www.angelcode.com/angelscript/sdk/docs/manual/doc_script_handle.html">learn more about handles from the Angelscript documentation</a> including why a few complex objects in NVGT don't support them.</p>
<p>Usually handles must be typed to the object they are pointing at, for example I could create a variable called `dictionary@ d;~ to create an empty handle to a dictionary object.</p>
<p>The type restriction on handles is almost always perfectly ok, however in a few super rare cases it can become bothersome or could make a coding task more tedious. The ref object is a workaround for that. Where ever typed handles can be used to point to an object, a ref object could point to it as well.</p>
<p>Unlike normal typed handles, one must cast a ref object back to the type it is storing in order to actually call methods or access properties of the stored type.</p>
<p>The = (assignment) operator is supported which causes the ref object to point to the value supplied, and the == (equality) operator is supported to compare whether a ref object and either another ref object or typed handle are pointing to the same actual object.</p>
<h3>Example:</h3>
<pre><code class="language-NVGT">// Lets create a function that can set the volume of either a mixer or a sound object.
void set_volume(ref@ obj, int volume) {
	mixer@ m = cast&lt;mixer@&gt;(obj);
	if (@m != null) {
		m.set_volume(volume);
		return;
	}
	sound@ s = cast&lt;sound@&gt;(obj);
	if (@s != null) s.set_volume(volume);
}
void main() {
	sound my_sound;
	my_sound.load(&quot;c:\\windows\\media\\ding.wav&quot;);
	mixer mix;
	my_sound.set_mixer(mix);
	set_volume(mix, -5);
	alert(&quot;mixer volume&quot;, mix.volume);
	set_volume(my_sound, -10);
	alert(&quot;sound volume&quot;, my_sound.volume);
	my_sound.close();
}
</code></pre>
<h2>string</h2>
<h3>Methods</h3>
<h4>empty</h4>
<p>Check to see if a string is empty.</p>
<ol>
<li><p>bool string::empty();</p>
</li>
<li><p>bool string::is_empty();</p>
</li>
</ol>
<h5>Returns:</h5>
<p>bool: True if the string is empty; false otherwise.</p>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	string test = input_box(&quot;String is Empty Tester&quot;, &quot;Enter a string.&quot;);
	if (test.empty())
		alert(&quot;String is Empty Tester&quot;, &quot;The string appears to be empty.&quot;);
	else
		alert(&quot;String is Empty Tester&quot;, &quot;The string isn't empty.&quot;);
}
</code></pre>
<h4>ends_with</h4>
<p>Determines if a string ends with another string.</p>
<p>bool string::ends_with(const string&amp;in str);</p>
<h5>Arguments:</h5>
<ul>
<li>const string&amp;in str: the string to look for.</li>
</ul>
<h5>Returns:</h5>
<p>bool: true if the string ends with the specified search, false if not.</p>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	string suffix = &quot;test&quot;;
	string text = input_box(&quot;Test&quot;, &quot;Enter a string&quot;);
	if (text.is_empty()) {
		alert(&quot;Info&quot;, &quot;Nothing was entered.&quot;);
		exit();
	}
	if (text.ends_with(suffix))
		alert(&quot;Info&quot;, &quot;The entered string ends with &quot; + suffix);
	else
		alert(&quot;Info&quot;, &quot;The entered string does not end with &quot; + suffix);
}
</code></pre>
<h4>erase</h4>
<p>Remove a portion of a string, starting at a given index.</p>
<p>void string::erase(uint pos, int count = -1);</p>
<h5>Arguments:</h5>
<ul>
<li><p>uint pos: the position to start erasing from.</p>
</li>
<li><p>int count = -1: the number of characters to erase after the specified index. If -1, erases all characters starting at the given pos until the end of the string.</p>
</li>
</ul>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	string text = input_box(&quot;String&quot;, &quot;enter at least a 3-character string.&quot;);
	if (text.length() &lt; 3) {
		alert(&quot;Info&quot;, &quot;Your string must be at least three characters.&quot;);
		exit(1);
	}
	alert(&quot;Before removal, the string is&quot;, text);
	text.erase(2);
	alert(&quot;After removal, the string is&quot;, text);
}
</code></pre>
<h4>format</h4>
<p>Formats a string with placeholders.</p>
<p>string string::format(const ?&amp;in = null...);</p>
<h5>Arguments:</h5>
<ul>
<li>const ?&amp;in = null: Any stringable value. You can pass up to 16 parameters.</li>
</ul>
<h5>Returns:</h5>
<p>Returns the formatted string.</p>
<h5>Remarks:</h5>
<p>This method is useful in situations when:</p>
<ol>
<li><p>You want to have multiple formats for messages, such as short and long messages.</p>
</li>
<li><p>You don't want to use concatenation.</p>
</li>
<li><p>You want to use a placeholder more than once in a string.</p>
</li>
</ol>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	string[] greetings = {&quot;Hello %0! How are you?&quot;, &quot;Hola %0! ¿Cómo estás?&quot;};
	string[] messages = {&quot;You have %0 health&quot;, &quot;%0 health&quot;};
	alert(&quot;Greeting:&quot;, greetings[random(0, 1)].format(&quot;Literary&quot;));
	alert(&quot;Message:&quot;, messages[random(0, 1)].format(1000));
}
</code></pre>
<h4>insert</h4>
<p>Insert a string into another string at a given position.</p>
<p><code>void string::insert(uint pos, const string&amp;in other);</code></p>
<h5>Arguments:</h5>
<ul>
<li>uint pos: the index to insert the other string at.</li>
<li>const string&amp;in other: the string to insert.</li>
</ul>
<h4>is_alphabetic</h4>
<p>Checks whether a string contains only alphabetical characters and nothing else.</p>
<p>bool string::is_alphabetic(string encoding = &quot;UTF8&quot;);</p>
<h5>Arguments:</h5>
<ul>
<li>string encoding = &quot;UTF8&quot;: The encoding to check against, with the UTF8 encoding being cached for speed.</li>
</ul>
<h5>Returns:</h5>
<p>bool: true if the input string contains only alphabetic characters, false otherwise.</p>
<h5>Remarks:</h5>
<p>This function only returns true if the string contains only alphabetical characters in the given encoding. If a single other non-alphabetical character is encountered, this function will return false.</p>
<p>If this function is called on a string that contains data that is not in the specified encoding, the results are undefined.</p>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	alert(&quot;example&quot;, &quot;aabdslf&quot;.is_alphabetic()); // Should show true.
	string input = input_box(&quot;example&quot;, &quot;enter a string&quot;);
	if(input.empty()) {
		alert(&quot;Info&quot;, &quot;You must type a string.&quot;);
		exit(1);
	}
	if(input.is_alphabetic())
		alert(&quot;example&quot;, &quot;you typed a string that contains only alphabetical characters&quot;);
	else
		alert(&quot;example&quot;, &quot;this string contains more than just alphabetical characters&quot;);
}
</code></pre>
<h4>is_lower</h4>
<p>Checks whether a string is completely lowercase.</p>
<p>bool string::is_lower(string encoding = &quot;UTF8&quot;);</p>
<h5>Arguments:</h5>
<ul>
<li>string encoding = &quot;UTF8&quot;: The encoding to check against, with the UTF8 encoding being cached for speed.</li>
</ul>
<h5>Returns:</h5>
<p>bool: true if the input string is lowercase.</p>
<h5>Remarks:</h5>
<p>This function only returns true if the string contains only lowercase characters in the given encoding. If a single uppercase or punctuation character is encountered, this function will return false.</p>
<p>If this function is called on a string that contains data that is not in the specified encoding, the results are undefined.</p>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	alert(&quot;example&quot;, &quot;HELLO&quot;.is_lower()); // Should show false.
	string input = input_box(&quot;example&quot;, &quot;enter a string&quot;);
	if(input.is_empty())
		exit();
	if(input.is_lower())
		alert(&quot;example&quot;, &quot;you typed a lowercase string&quot;);
	else
		alert(&quot;example&quot;, &quot;you did not type a lowercase string&quot;);
}
</code></pre>
<h4>is_punctuation</h4>
<p>Checks whether a string contains only punctuation characters and nothing else.</p>
<p>bool string::is_punctuation(string encoding = &quot;UTF8&quot;);</p>
<h5>Arguments:</h5>
<ul>
<li>string encoding = &quot;UTF8&quot;: The encoding to check against, with the UTF8 encoding being cached for speed.</li>
</ul>
<h5>Returns:</h5>
<p>bool: true if the input string contains only punctuation characters.</p>
<h5>Remarks:</h5>
<p>This function only returns true if the string contains only punctuation characters in the given encoding. If a single alphanumeric or other non-punctuation character is encountered, this function will return false.</p>
<p>If this function is called on a string that contains data that is not in the specified encoding, the results are undefined.</p>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	alert(&quot;example&quot;, &quot;.?!&quot;.is_punctuation()); // Should show true.
	string input = input_box(&quot;example&quot;, &quot;enter a string&quot;);
	if(input.is_empty())
		exit();
	if(input.is_punctuation())
		alert(&quot;example&quot;, &quot;you typed a string that contains only punctuation characters&quot;);
	else
		alert(&quot;example&quot;, &quot;this string contains more than just punctuation&quot;);
}
</code></pre>
<h4>is_upper</h4>
<p>Checks whether a string is completely uppercase.</p>
<p>bool string::is_upper(string encoding = &quot;UTF8&quot;);</p>
<h5>Arguments:</h5>
<ul>
<li>string encoding = &quot;UTF8&quot;: The encoding to check against, with the UTF8 encoding being cached for speed.</li>
</ul>
<h5>Returns:</h5>
<p>bool: true if the input string is uppercase.</p>
<h5>Remarks:</h5>
<p>This function only returns true if the string contains only uppercase characters in the given encoding. If a single lowercase or punctuation character is encountered, this function will return false.</p>
<p>If this function is called on a string that contains data that is not in the specified encoding, the results are undefined.</p>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	alert(&quot;example&quot;, &quot;HELLO&quot;.is_upper()); // Should show true.
	string input = input_box(&quot;example&quot;, &quot;enter a string&quot;);
	if(input.is_empty())
		exit();
	if(input.is_upper())
		alert(&quot;example&quot;, &quot;you typed an uppercase string&quot;);
	else
		alert(&quot;example&quot;, &quot;you did not type an uppercase string&quot;);
}
</code></pre>
<h4>length</h4>
<p>Returns the length (how large a string is).</p>
<ol>
<li><p>uint string::length();</p>
</li>
<li><p>uint string::size();</p>
</li>
</ol>
<h5>returns:</h5>
<p>uint: The length of a string.</p>
<h5>Remarks:</h5>
<p>Note: This returns the length in bytes, rather than characters of any given text encoding.</p>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	string test = input_box(&quot;String Length Tester&quot;, &quot;Enter a string to see its length.&quot;);
	if (test.length() &lt;= 0)
		alert(&quot;String Length Tester&quot;, &quot;You appear to have provided an empty string!&quot;);
	else if (test.length() == 1)
		alert(&quot;String Length Tester&quot;, &quot;You appear to have only provided a single character!&quot;);
	else
		alert(&quot;String Length Tester&quot;, &quot;The provided string is &quot; + test.length()+&quot; characters!&quot;);
}
</code></pre>
<h4>lower</h4>
<p>Converts a string to lowercase.</p>
<p>string string::lower();</p>
<h5>Returns:</h5>
<p>string: the specified string in lowercase.</p>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	string text = input_box(&quot;Text&quot;, &quot;Enter the text to convert to lowercase.&quot;);
	if (text.empty()) {
		alert(&quot;Info&quot;, &quot;You typed a blank string.&quot;);
		exit(1);
	}
	alert(&quot;Your string lowercased is&quot;, text.lower());
}
</code></pre>
<h4>lower_this</h4>
<p>Converts a string to lowercase.</p>
<p>string&amp; string::lower();</p>
<h5>Returns:</h5>
<p>string&amp;: a reference to the specified string in lowercase.</p>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	string text = input_box(&quot;Text&quot;, &quot;Enter the text to convert to lowercase.&quot;);
	if (text.empty()) {
		alert(&quot;Info&quot;, &quot;You typed a blank string.&quot;);
		exit(1);
	}
	text = text.lower_this();
	alert(&quot;Your string lowercased is&quot;, text);
}
</code></pre>
<h4>replace</h4>
<p>Try to find any occurrences of a particular string, and replace them with a substitution in a given string object.</p>
<p><code>string string::replace(const string&amp;in search, const string&amp;in replacement, bool replace_all = true);</code></p>
<h5>Arguments:</h5>
<ul>
<li>const string&amp;in search: the string to search for.</li>
<li>const string&amp;in replacement: the string to replace the search text with (if found).</li>
<li>bool replace_all = true: whether or not all occurrences should be replaced, or only the first one.</li>
</ul>
<h5>Returns:</h5>
<p>string: the specified string with the replacement applied.</p>
<h4>replace_this</h4>
<p>Try to find any occurrences of a particular string, and replace them with a substitution in a given string object.</p>
<p><code>string&amp; string::replace_this(const string&amp;in search, const string&amp;in replacement, bool replace_all = true);</code></p>
<h5>Arguments:</h5>
<ul>
<li>const string&amp;in search: the string to search for.</li>
<li>const string&amp;in replacement: the string to replace the search text with (if found).</li>
<li>bool replace_all = true: whether or not all occurrences should be replaced, or only the first one.</li>
</ul>
<h5>Returns:</h5>
<p>string&amp;: a two-way reference to the specified string with the replacement applied.</p>
<h4>resize</h4>
<p>Resize a string to a particular size (in bytes).</p>
<p>void string::resize(uint new_size);</p>
<h5>Arguments:</h5>
<ul>
<li>uint new_size: the new size of the string (in bytes).</li>
</ul>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	string test = &quot;abcdef&quot;;
	alert(&quot;The string is&quot;, test.length() + &quot; characters&quot;);
	test.resize(3);
	alert(&quot;The string is&quot;, test.length() + &quot; characters&quot;);
}
</code></pre>
<h4>reverse</h4>
<p>Reverse a string.</p>
<p>string string::reverse(string encoding = &quot;UTF8&quot;);</p>
<h5>Arguments:</h5>
<ul>
<li>string encoding = &quot;UTF8&quot;: The string's encoding, with UTF8 cached for speed.</li>
</ul>
<h5>Returns:</h5>
<p>string: The specified string in reverse.</p>
<h5>Remarks:</h5>
<p>This function reverses the characters of a string based on a given encoding. To reverse the raw bytes of a string, for example if you are operating on binary data, see the reverse_bytes function instead.</p>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	string text = input_box(&quot;Text&quot;, &quot;Enter some text to reverse.&quot;);
	if (text.is_empty()) {
		alert(&quot;Info&quot;, &quot;nothing was entered.&quot;);
		exit();
	}
	string result = text.reverse();
	alert(&quot;Reversed string&quot;, result);
}
</code></pre>
<h4>reverse_bytes</h4>
<p>Reverses the raw bytes contained within a string.</p>
<p>string string::reverse_bytes();</p>
<h5>Returns:</h5>
<p>string: A copy of the string with it's bytes reversed.</p>
<h5>Remarks:</h5>
<p>If you want to reverse the characters within a string given an encoding such as UTF8, use the reverse method instead.</p>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	string raw = hex_to_string(&quot;1a2b3c4d&quot;);
	raw = raw.reverse_bytes();
	alert(&quot;reverse_bytes&quot;, string_to_hex(raw)); // Should show 4D3C2B1A.
	// Lets make it clear how this function differs from string::reverse. We'll make a string of emojis and show the results of both methods.
	string emojis = &quot;🦟🦗🐜🐝🐞🦂🕷&quot;;
	alert(&quot;emojis reversed properly&quot;, emojis.reverse()); // string::reverse takes the UTF8 encoding into account.
	alert(&quot;broken emojis&quot;, emojis.reverse_bytes()); // This string no longer contains valid character sequences, and so the emoticons will most certainly not show correctly. Aww you can see if you run this example that it seems even string::reverse_bytes() can't quite get rid of mosquitos though... 😀
}
</code></pre>
<h4>split</h4>
<p>Splits a string into an array at a given delimiter.</p>
<p>string[]@ string::split(const string&amp;in delimiter);</p>
<h5>Arguments:</h5>
<ul>
<li>const string&amp;in delimiter: the delimiter to split at.</li>
</ul>
<h5>Returns:</h5>
<p>string[]@: a handle to an array containing each part of the split string.</p>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	string test = &quot;welcome to the example&quot;;
	string[]@ parts = test.split(&quot; &quot;);
	alert(&quot;Parts&quot;, join(parts, &quot;, &quot;));
}
</code></pre>
<h4>starts_with</h4>
<p>Determines if a string starts with another string.</p>
<p>bool string::starts_with(const string&amp;in str);</p>
<h5>Arguments:</h5>
<ul>
<li>const string&amp;in str: the string to look for.</li>
</ul>
<h5>Returns:</h5>
<p>bool: true if the string starts with the specified search, false if not.</p>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	string prefix = &quot;abc&quot;;
	string text = input_box(&quot;Test&quot;, &quot;Enter a string&quot;);
	if (text.is_empty()) {
		alert(&quot;Info&quot;, &quot;Nothing was entered.&quot;);
		exit();
	}
	if (text.starts_with(prefix))
		alert(&quot;Info&quot;, &quot;The entered string starts with &quot; + prefix);
	else
		alert(&quot;Info&quot;, &quot;The entered string does not start with &quot; + prefix);
}
</code></pre>
<h4>trim_whitespace</h4>
<p>Trims any and all whitespace from the beginning and end of a string.</p>
<p>string string::trim_whitespace();</p>
<h5>Returns:</h5>
<p>string: the specified string, with any trailing/leading whitespace removed.</p>
<h5>Remarks:</h5>
<p>Any and all whitespace, including the tab character and new lines, will be removed.</p>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	string text = input_box(&quot;String&quot;, &quot;Enter a string&quot;);
	if (text.is_empty()) {
		alert(&quot;Info&quot;, &quot;You didn't enter a string.&quot;);
		exit();
	}
	string result = text.trim_whitespace();
	alert(&quot;Trimmed string&quot;, result);
}
</code></pre>
<h4>trim_whitespace_left</h4>
<p>Trims any and all whitespace from the left side of a string.</p>
<p>string string::trim_whitespace_left();</p>
<h5>Returns:</h5>
<p>string: the specified string, with the whitespace removed from the left side.</p>
<h5>Remarks:</h5>
<p>Any and all whitespace, including the tab character and new lines, will be removed.</p>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	string text = input_box(&quot;String&quot;, &quot;Enter a string&quot;);
	if (text.is_empty()) {
		alert(&quot;Info&quot;, &quot;You didn't enter a string.&quot;);
		exit();
	}
	string result = text.trim_whitespace_left();
	alert(&quot;Trimmed string&quot;, result);
}
</code></pre>
<h4>trim_whitespace_left_this</h4>
<p>Trims any and all whitespace from the left side of a string, returning a reference to it.</p>
<p>string&amp; string::trim_whitespace_left();</p>
<h5>Returns:</h5>
<p>string&amp;: a two-way reference to the specified string, with the whitespace removed from the left side.</p>
<h5>Remarks:</h5>
<p>Any and all whitespace, including the tab character and new lines, will be removed.</p>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	string text = input_box(&quot;String&quot;, &quot;Enter a string&quot;);
	if (text.empty()) {
		alert(&quot;Info&quot;, &quot;You didn't enter a string.&quot;);
		exit();
	}
	text = text.trim_whitespace_left();
	alert(&quot;Trimmed string&quot;, text);
}
</code></pre>
<h4>trim_whitespace_right</h4>
<p>Trims any and all whitespace from the right side of a string.</p>
<p>string string::trim_whitespace_right();</p>
<h5>Returns:</h5>
<p>string: the specified string, with the whitespace removed from the right side.</p>
<h5>Remarks:</h5>
<p>Any and all whitespace, including the tab character and new lines, will be removed.</p>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	string text = input_box(&quot;String&quot;, &quot;Enter a string&quot;);
	if (text.is_empty()) {
		alert(&quot;Info&quot;, &quot;You didn't enter a string.&quot;);
		exit();
	}
	string result = text.trim_whitespace_right();
	alert(&quot;Trimmed string&quot;, result);
}
</code></pre>
<h4>trim_whitespace_right_this</h4>
<p>Trims any and all whitespace from the right side of a string, returning a reference to it.</p>
<p>string&amp; string::trim_whitespace_right();</p>
<h5>Returns:</h5>
<p>string&amp;: a two-way reference to the specified string, with the whitespace removed from the right side.</p>
<h5>Remarks:</h5>
<p>Any and all whitespace, including the tab character and new lines, will be removed.</p>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	string text = input_box(&quot;String&quot;, &quot;Enter a string&quot;);
	if (text.empty()) {
		alert(&quot;Info&quot;, &quot;You didn't enter a string.&quot;);
		exit();
	}
	text = text.trim_whitespace_right();
	alert(&quot;Trimmed string&quot;, text);
}
</code></pre>
<h4>trim_whitespace_this</h4>
<p>Trims any and all whitespace from the beginning and end of a string, returning a reference to it.</p>
<p>string&amp; string::trim_whitespace_this();</p>
<h5>Returns:</h5>
<p>string&amp;: a reference to the specified string, with any trailing/leading whitespace removed.</p>
<h5>Remarks:</h5>
<p>Any and all whitespace, including the tab character and new lines, will be removed.</p>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	string text = input_box(&quot;String&quot;, &quot;Enter a string&quot;);
	if (text.empty()) {
		alert(&quot;Info&quot;, &quot;You didn't enter a string.&quot;);
		exit();
	}
	text = text.trim_whitespace_this();
	alert(&quot;Trimmed string&quot;, text);
}
</code></pre>
<h4>upper</h4>
<p>Converts a string to uppercase.</p>
<p>string string::upper();</p>
<h5>Returns:</h5>
<p>string: the specified string in uppercase.</p>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	string text = input_box(&quot;Text&quot;, &quot;Enter the text to convert to uppercase.&quot;);
	if (text.empty()) {
		alert(&quot;Info&quot;, &quot;You typed a blank string.&quot;);
		exit(1);
	}
	alert(&quot;Your string uppercased is&quot;, text.upper());
}
</code></pre>
<h4>upper_this</h4>
<p>Converts a string to uppercase.</p>
<p>string&amp; string::upper();</p>
<h5>Returns:</h5>
<p>string&amp;: a reference to the specified string in uppercase.</p>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	string text = input_box(&quot;Text&quot;, &quot;Enter the text to convert to uppercase.&quot;);
	if (text.empty()) {
		alert(&quot;Info&quot;, &quot;You typed a blank string.&quot;);
		exit(1);
	}
	text = text.upper_this();
	alert(&quot;Your string uppercased is&quot;, text);
}
</code></pre>
