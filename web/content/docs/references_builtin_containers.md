---
title: Containers
url: docs/references_builtin_containers.html
---

<h1>Containers</h1>
<p>In this documentation, we consider a container to be any generic class that has the primary purpose of storing more than one value.</p>
<h2>array</h2>
<p>This container stores a resizable list of elements that must all be the same type. In this documentation, &quot;T&quot; refers to the dynamic type that a given array was instanciated with.</p>
<ol>
<li><code>T[]();</code></li>
<li><code>array&lt;T&gt;();</code></li>
<li><code>array&lt;T&gt;(uint count);</code></li>
<li><code>array&lt;T&gt;({item1, item2, item3})</code></li>
</ol>
<h3>Arguments (3):</h3>
<ul>
<li>uint count: The initial number of items in the array which will be set to their default value upon array instanciation.</li>
</ul>
<h3>Arguments (4):</h3>
<ul>
<li>{item}: A list of elements that the array should be initialized with.</li>
</ul>
<h3>Remarks:</h3>
<p>Items in an array are accessed using what's known as the indexing operator, that is, <code>arrayname[index]</code> where index is an integer specifying what item you wish to access within the array. The biggest thing to keep in mind is that unlike many functions in NVGT which will silently return a negative value or some other error form upon failure, arrays will actually throw exceptions if you try accessing data outside the array's bounds. Unless you handle such an exception with a try/catch block, this results in an unhandled exception dialog appearing where the user can choose to copy the call stack before the program exits. The easiest way to avoid this is by combining your array accesses with healthy usage of the array.length() method to make sure that you don't access out-of-bounds data in the first place.</p>
<p>Data in arrays is accessed using 0-based indexing. This means that if 5 items are in an array, you access the first item with <code>array[0]</code> and the last with <code>array[4]</code>. If you are a new programmer this might take you a second to get used to, but within no time your brain will be calculating this difference for you almost automatically as you write your code, it becomes second nature and is how arrays are accessed in probably 90+% of well known programming languages. Just remember to use <code>array[array.size() -1]</code> to access the last item in the array, not <code>array[array.length()]</code> which would cause an index out of bounds exception.</p>
<p>There is a possible confusion regarding syntax ambiguity when declaring arrays which should be cleared up. What is the difference between <code>array&lt;string&gt; items</code> and <code>string[] items</code> and when should either one be used?</p>
<p>At it's lowest level, an array is a template class, meaning it's a class that can accept a dynamic type <code>(array&lt;T&gt;)</code>. This concept also exists with the grid, async, and other classes in NVGT.</p>
<p>However, AngelScript provides a convenience feature called the default array type. This allows us to choose just one template class out of all the template classes in the entire engine, and to make that 1 class much easier to declare than all the others using the bracket syntax <code>(T[])</code>, and this array class happens to be our chozen default array type in NVGT.</p>
<p>Therefore, in reality <code>array&lt;T&gt;</code> and <code>T[]</code> do the exact same thing, it's just that the first one is the semantically correct method of declaring a templated class while the latter is a highly useful AngelScript shortcut. So now when you're looking at someone's code and you see a weird instance of <code>array&lt;T&gt;</code>, you can rest easy knowing that you didn't misunderstand the code and no you don't need to go learning some other crazy array type, that code author just opted to avoid using the AngelScript default array type shortcut for one reason or another.</p>
<h3>Methods</h3>
<h4>empty</h4>
<p>Determine whether or not the array is empty.</p>
<ol>
<li><p>bool array::empty();</p>
</li>
<li><p>bool array::is_empty();</p>
</li>
</ol>
<h5>Returns:</h5>
<p>bool: true if the array is empty, false if not.</p>
<h5>Remarks:</h5>
<p>This method is functionally equivalent to <code>array.length() == 0</code>.</p>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	string[] items;
	bool insert = random_bool();
	if (insert)
		items.insert_last(1);
	alert(&quot;The array is&quot;, items.empty() ? &quot;empty&quot; : &quot;not empty&quot;);
}
</code></pre>
<h4>erase</h4>
<p>Remove an item from the array at a particular index.</p>
<p>void array::erase(uint index);</p>
<h5>Arguments:</h5>
<ul>
<li>uint index: the index of the item to delete.</li>
</ul>
<h5>Remarks:</h5>
<p>Passing an index that is less than 0 or greater or equal to the array's absolute length will result in an index out of bounds exception being thrown.</p>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	string[] items = {&quot;this&quot;, &quot;is&quot;, &quot;a&quot;, &quot;test&quot;};
	alert(&quot;The list currently contains&quot;, join(items, &quot;, &quot;));
	items.erase(random(0, 2));
	alert(&quot;The list currently contains&quot;, join(items, &quot;, &quot;));
}
</code></pre>
<h4>find</h4>
<p>Search for an item in an array.</p>
<ol>
<li><p>int find(const T&amp;in value);</p>
</li>
<li><p>int find(uint start_at, const T&amp;in value);</p>
</li>
</ol>
<h5>Arguments:</h5>
<ul>
<li><p>uint start_at: An optional index to begin searching from.</p>
</li>
<li><p>const T&amp;in value: The value to search for.</p>
</li>
</ul>
<h5>Returns:</h5>
<p>int: The index of the located item, or -1 if not found.</p>
<h5>Remarks:</h5>
<p>Be ware that this method will start getting slower the larger your array is, this is because this find method must search through every item in the array until it finds an item that equals what you are looking for.</p>
<p>Be sure to never write code like <code>string value = array[array.find(&quot;testing&quot;)];</code> or anything else where you call array.find() directly within the array's indexing operator. This is because array.find() could return -1, meaning that an index out of bounds exception will be thrown if you use the value returned by this function without verifying it first.</p>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	string text = &quot;this is a sentence made up of many words, sort of?&quot;;
	string[]@ elements = text.split(&quot; ,?.&quot;, false);
	int word = elements.find(&quot;sort&quot;);
	if (word &lt; 0) alert(&quot;Oh no not found&quot;, &quot;Someone should probably report this if they ever see it while running an unmodified version of this example...&quot;);
	else alert(&quot;found&quot;, &quot;The word sort is at index &quot; + word);
}
</code></pre>
<h4>insert_at</h4>
<p>Inserts an element into an array at a given position, moving other items aside to make room if necessary.</p>
<p>void array::insert_at(uint index, const T&amp;in value);</p>
<h5>Arguments:</h5>
<ul>
<li><p>uint index: the position to insert at.</p>
</li>
<li><p>const T&amp;in value: the element to be inserted.</p>
</li>
</ul>
<h5>Remarks:</h5>
<p>This method adds an element to the given position of an array. If you pass index 0, the item will be inserted at the beginning of the aray, and if you pass the array's absolute length, the item will be inserted at the end. Any values less than 0 or greater than the array's absolute length will result in an index out of bounds exception being thrown.</p>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	string[] names = {&quot;HTML&quot;, &quot;CSS&quot;};
	names.insert_at(0,&quot;Java Script&quot;);
	names.insert_at(2, &quot;php&quot;);
	alert(&quot;Languages&quot;, join(names, &quot;, &quot;));
}
</code></pre>
<h4>insert_last</h4>
<p>Appends an element to an array.</p>
<ol>
<li><p>void array::insert_last(const T&amp;in);</p>
</li>
<li><p>void array::push_back(const T&amp;in);</p>
</li>
</ol>
<h5>Arguments</h5>
<ul>
<li><type> element: the element to be inserted.</li>
</ul>
<h5>Remarks</h5>
<p>This method adds an element to the end of an array.</p>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	string[] names = {&quot;HTML&quot;, &quot;CSS&quot;};
	names.insert_last(&quot;Java Script&quot;);
	alert(&quot;Languages&quot;, join(names, &quot;, &quot;));
}
</code></pre>
<h4>length</h4>
<p>Returns the number of items in the array.</p>
<ol>
<li><p>uint array::length();</p>
</li>
<li><p>uint array::size();</p>
</li>
</ol>
<h5>Returns:</h5>
<p>uint: the number of items in the array.</p>
<h5>Remarks:</h5>
<p>This method returns the absolute number of elements in the array, that is, without taking 0-based indexing into account. For example an array containing {1, 2, 3} will have a length of 3, but you must access the last element with the index 2 and the first element with index 0, rather than using 3 for the last item and 1 for the first.</p>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	int[] items;
	for (uint i = 0; i &lt; random(1, 10); i++)
		items.insert_last(i);
	alert(&quot;The array contains&quot;, items.length() + &quot; &quot; + (items.length() == 1 ? &quot;item&quot; : &quot;items&quot;));
}
</code></pre>
<h4>remove_at</h4>
<p>Removes an element of an array by a given position.</p>
<p>void array::remove_at(uint index);</p>
<h5>Arguments:</h5>
<ul>
<li>uint index: the position to be removed.</li>
</ul>
<h5>Remarks:</h5>
<p>Please note that the position value is 0 base, and failure to define correct index will cause NVGT to throw &quot;index out of bounds&quot; exception.</p>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	string[] names = {&quot;HTML&quot;, &quot;CSS&quot;};
	names.remove_at(0);
	alert(&quot;Languages&quot;, join(names, &quot;, &quot;));
}
</code></pre>
<h4>remove_last</h4>
<p>Removes the last item from the array.</p>
<ol>
<li><code>void array::remove_last();</code></li>
<li><code>void array::pop_back();</code></li>
</ol>
<h5>Remarks:</h5>
<p>Calling this method on an empty array will throw an index out of bounds exception.</p>
<h4>remove_range</h4>
<p>Removes a group of items from an array, starting at a given  position and removing the specified number of items after it.</p>
<p>void array::remove_range(uint start, uint count);</p>
<h5>Arguments:</h5>
<ul>
<li><p>uint start: the index to start removing at.</p>
</li>
<li><p>uint count: the number of items to remove.</p>
</li>
</ul>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	string[] items = {&quot;there&quot;, &quot;are&quot;, &quot;a&quot;, &quot;few&quot;, &quot;items&quot;, &quot;that&quot;,&quot;will&quot;, &quot;disappear&quot;};
	alert(&quot;The array currently is&quot;, join(items, &quot;, &quot;));
	items.remove_range(1, 3);
	alert(&quot;The array is now&quot;, join(items, &quot;, &quot;));
}
</code></pre>
<h4>reserve</h4>
<p>allocates the memory needed to hold the given number of items, but doesn't initialize them.</p>
<p><code>void array::reserve(uint length);</code></p>
<h5>Arguments:</h5>
<ul>
<li>uint length: the size of the array you want to reserve.</li>
</ul>
<h5>Remarks:</h5>
<p>This method is provided because in computing, memory allocation is expensive. If you want to add 5000 elements to an array and you call array.insert_last() 5000 times without calling this reserve() method, you will also perform nearly 5000 memory allocations, and each one of those is a lot of work for the OS. Instead, you can call this function once with a value of 5000, which will perform only one expensive memory allocation, and now at least for the first 5000 calls to insert_last(), the array will not need to repetitively allocate tiny chunks of memory over and over again to add your intended elements. The importance of this cannot be stressed enough for large arrays, using the reserve() method particularly for bulk array inserts can literally speed your code up by hundreds of times in the area of array management.</p>
<h4>resize</h4>
<p>Resizes the array to the specified size, and initializes all resulting new elements to their default values.</p>
<p><code>void array::resize(uint length);</code></p>
<h5>Arguments:</h5>
<ul>
<li>uint length: how big to resize the array to</li>
</ul>
<h5>Remarks:</h5>
<p>If the new size is smaller than the existing number of elements, items will be removed from the bottom or the end of the aray until the array has exactly the number of items specified in the argument to this method.</p>
<h4>reverse</h4>
<p>Reverses the array, so the last item becomes the first and vice versa.</p>
<p>void array::reverse();</p>
<h5>Remarks:</h5>
<p>This method reverses the array in place rather than creating a new array and returning it.</p>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	string[] items = {&quot;This&quot;, &quot;is&quot;, &quot;a&quot;, &quot;test&quot;};
	alert(&quot;The array is currently&quot;, join(items, &quot;, &quot;));
	items.reverse();
	alert(&quot;The reversed array is&quot;, join(items, &quot;, &quot;));
}
</code></pre>
<h2>dictionary</h2>
<p>This container stores multiple pieces of data of almost any type, which are stored and referenced by unique keys which are just arbitrary strings.</p>
<ol>
<li><code>dictionary();</code></li>
<li><code>dictionary(\{\{&quot;key1&quot;, value1}, {&quot;key2&quot;, value2\}\});</code></li>
</ol>
<h3>Arguments (2):</h3>
<ul>
<li>\{\{&quot;key&quot;, value\}\}: default values to set in the dictionary, provided in the format shown.</li>
</ul>
<h3>Remarks:</h3>
<p>The idea behind a dictionary, or hash map / hash table as they are otherwise called, is that one can store some data referenced by a certain ID or key, before later retrieving that data very quickly given that same key used to store it.</p>
<p>Though explaining the details and guts of how hash maps work internally is beyond the scope of this documentation, here is an <a href="https://en.wikipedia.org/wiki/Hash_table">overly in depth wikipedia article</a> that is sure to teach you more than you ever wished to know about this data structure. Honestly unless you wish to write your own dictionary implementation yourself in a low level language and/or are specifically worried about the efficiency of storing vast amounts of similar data which could stress the algorithm, it's enough to know that the dictionary internally turns your string keys into integer hashes, which are a lot faster for the computer to compare than the characters in the key strings themselves. Combine this with clever use of small lists or buckets determined by even more clever use of bitwise operations and other factors, and what you're left with is a structure that can store thousands of keys while still being able to look up a value given a key so quickly it's like magic, at least compared to the least efficient alternative which is looping through your thousands of data points and individually comparing them in order to find just one value you wish to look up.</p>
<p>NVGT's dictionaries are unordered, meaning that the get_keys() method will likely not return a list of keys in the order that you added them. In cases where this is very important to you, you can create a string array along side your dictionary and manually store key names yourself and then loop through that array instead of the output of get_keys() when you want to enumerate a dictionary in an ordered fassion. Note, of course, that this makes the entire system less efficient as now deleting or updating a key in the dictionary requires you to loop through your string array and find the key that needs deleting or updating, and dictionaries exist exactly to avoid such an expensive loop, though the same efficiency is preserved when simply looking up a key in the dictionary without writing to it, which can be enough in many cases. While in most cases it's best to write code that does not rely on the ordering of items in a dictionary, this at least provides an option to choose between ordering and better efficiency, should you really need such a thing.</p>
<p>Look at the individual documented methods of this class for examples of it's usage.</p>
<h3>Methods</h3>
<h4>delete</h4>
<p>This method deletes the given key from the dictionary.</p>
<p>bool dictionary::delete(const string &amp;in key);</p>
<h5>Arguments:</h5>
<ul>
<li>const string &amp;in key: the key to delete.</li>
</ul>
<h5>Returns:</h5>
<p>bool: true if the key was successfully deleted, false otherwise.</p>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	dictionary data;
	data.set(&quot;nvgt&quot;, &quot;An audiogame engine using AngelScript&quot;);
	alert(&quot;Information&quot;, data.delete(&quot;nvgt&quot;)); //true
	alert(&quot;Information&quot;, data.delete(&quot;nvgt&quot;)); //false because the key is already deleted, another word, it does not exist.
}
</code></pre>
<h4>delete_all</h4>
<p>This method deletes all keys from the dictionary.</p>
<p><code>bool dictionary::delete_all();</code></p>
<h4>exists</h4>
<p>Returns whether a given key exists in the dictionary.</p>
<p>bool dictionary::exists(const string &amp;in key);</p>
<h5>Arguments:</h5>
<ul>
<li>const string &amp;in key: the key to look for.</li>
</ul>
<h5>Returns:</h5>
<p>bool: true if the key exists, false otherwise.</p>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	dictionary data;
	data.set(&quot;nvgt&quot;, &quot;An audiogame engine using AngelScript&quot;);
	alert(&quot;Information&quot;, data.exists(&quot;nvgt&quot;)); //true
	alert(&quot;Information&quot;, data.exists(&quot;gameengine&quot;)); //false
}
</code></pre>
<h4>get</h4>
<p>Gets the data from a given key.</p>
<p>bool dictionary::get(const string &amp;in key, ?&amp;out value);</p>
<h5>Arguments:</h5>
<ul>
<li><p>const string &amp;in key: the key to look for.</p>
</li>
<li><p>?&amp;out value: the variable for the value to be associated, see remarks.</p>
</li>
</ul>
<h5>Returns:</h5>
<p>bool: true if the dictionary retrieves the value of the key, false otherwise.</p>
<h5>Remarks:</h5>
<p>Please note that the value parameter should be a variable to receive the value. This means that dictionary will write to the variable, not read from.</p>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	dictionary data;
	data.set(&quot;nvgt&quot;, &quot;An audiogame engine using AngelScript&quot;);
	string result;
	if (!data.get(&quot;nvgt&quot;, result))
		alert(&quot;Error&quot;, &quot;Failed to retrieve the value of the key&quot;);
	else
		alert(&quot;Result is&quot;, result);
}
</code></pre>
<h4>get_keys</h4>
<p>Returns a string array containing the key names in the dictionary.</p>
<p>string[]@ dictionary::get_keys();</p>
<h5>Returns:</h5>
<p>string[]@: the  list of keys in the dictionary on success, 0 otherwise.</p>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	dictionary data;
	data.set(&quot;nvgt&quot;, &quot;An audiogame engine using AngelScript&quot;);
	string[]@ keys = data.get_keys();
	alert(&quot;Keys&quot;, join(keys, &quot;, &quot;));
}
</code></pre>
<h4>get_size</h4>
<p>Returns the size of the dictionary.</p>
<p>uint dictionary::get_size();</p>
<h5>Returns:</h5>
<p>uint: the size of the dictionary, another word, the total keys on success, 0 otherwise.</p>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	dictionary data;
	data.set(&quot;nvgt&quot;, &quot;An audiogame engine using AngelScript&quot;);
	alert(&quot;Dictionary size is&quot;, data.get_size());
}
</code></pre>
<h4>is_empty</h4>
<p>Returns whether the dictionary is empty.</p>
<p>bool dictionary::is_empty();</p>
<h5>Returns:</h5>
<p>bool: true if the dictionary is empty, false otherwise.</p>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	dictionary data;
	data.set(&quot;nvgt&quot;, &quot;An audiogame engine using AngelScript&quot;);
	alert(&quot;Information&quot;, data.is_empty()); //false
	data.delete_all();
	alert(&quot;Information&quot;, data.is_empty()); //true
}
</code></pre>
<h4>set</h4>
<p>Sets the data into a given key.</p>
<p><code>void dictionary::set(const string &amp;in key, const ?&amp;in value);</code></p>
<h5>Arguments:</h5>
<ul>
<li>const string &amp;in key: the key to use.</li>
<li>const ?&amp;in value: the value to set into this key.</li>
</ul>
<h5>Remarks:</h5>
<p>If the key already exists in the dictionary, its value will be overwritten.</p>
<h2>grid</h2>
<p>This type is essentially just a more convenient 2d array. One place it's super useful is when representing a game board.</p>
<ol>
<li><p>grid();</p>
</li>
<li><p>grid(uint width, uint height);</p>
</li>
<li><p>grid({repeat {repeat_same T\}\});</p>
</li>
</ol>
<h3>Arguments (2):</h3>
<ul>
<li><p>uint width: the width of the grid.</p>
</li>
<li><p>uint height: the height of the grid.</p>
</li>
</ul>
<h3>Remarks:</h3>
<p>One of the things that makes this class especially convenient is its opIndex overload. It's possible to index into a grid like:</p>
<p><code>my_grid[1, 2];</code></p>
<p>to access the value at (1, 2) on your grid.</p>
<h3>Example:</h3>
<pre><code class="language-NVGT">void main() {
	grid&lt;bool&gt; game_board(10, 10); // a 10x10 grid of booleans.
	game_board[4, 4] = true; // set the center of the board to true.
	alert(&quot;The center of the board is&quot;, game_board[4, 4]);
}
</code></pre>
<h3>Methods</h3>
<h4>height</h4>
<p>Returns the current height of the grid.</p>
<p>uint grid::height();</p>
<h5>Returns:</h5>
<p>uint: the height  of the grid.</p>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	grid&lt;int&gt; g(random(1, 10), random(1, 10));
	alert(&quot;Grid height is&quot;, g.height());
}
</code></pre>
<h4>resize</h4>
<p>Resize a grid to the given width and height.</p>
<p>void grid::resize(uint width, uint height);</p>
<h5>Arguments:</h5>
<ul>
<li><p>uint width: the width you want to resize the grid to.</p>
</li>
<li><p>uint height: the height you want to resize the grid to.</p>
</li>
</ul>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	grid&lt;int&gt; g(5, 5);
	alert(&quot;Original width and height&quot;, g.width() + &quot;, &quot; + g.height());
	g.resize(random(1, 100), random(1, 100));
	alert(&quot;New width and height&quot;, g.width() + &quot;, &quot; + g.height());
}
</code></pre>
<h4>width</h4>
<p>Returns the current width of the grid.</p>
<p>uint grid::width();</p>
<h5>Returns:</h5>
<p>uint: the width of the grid.</p>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	grid&lt;int&gt; g(random(1, 10), random(1, 10));
	alert(&quot;Grid width is&quot;, g.width());
}
</code></pre>
<h3>Operators</h3>
<h4>opIndex</h4>
<p>Get or set the value of a grid cell given an x and a y.</p>
<p>T&amp; grid::opIndex(uint row, uint column);</p>
<h5>Arguments:</h5>
<ul>
<li><p>uint row: the row (x value) to check.</p>
</li>
<li><p>uint column: the column (y value) to check.</p>
</li>
</ul>
<h5>Returns:</h5>
<p>T&amp;: a reference to the value at the given position. It is of whatever type your grid holds.</p>
<h5>Remarks:</h5>
<p>This function can throw index out of bounds errors, exactly like arrays can, so be careful.</p>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	grid&lt;int&gt; the_grid;
	the_grid.resize(5, 5);
	for (uint i = 0; i &lt; 5; i++) {
		for (uint j = 0; j &lt; 5; j++) {
			the_grid[i, j] = random(1, 100);
		}
	}
	alert(&quot;Info&quot;, &quot;The center is &quot; + the_grid[2, 2]);
}
</code></pre>
