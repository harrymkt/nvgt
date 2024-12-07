---
title: Filesystem
url: docs/references_builtin_filesystem.html
---

<h1>Filesystem</h1>
<p>This section contains documentation of functions and properties that allow you to check the existance of / delete a file, create / enumerate directories, and in other ways interact with and/or manipulate the filesystem.</p>
<p>If you wish to specifically read and write files, you should look at the file datastream class.</p>
<h2>Functions</h2>
<h3>directory_create</h3>
<p>Creates a directory if it doesn't already exist.</p>
<p>bool directory_create(const string&amp;in directory);</p>
<h4>Arguments:</h4>
<ul>
<li>const string&amp;in directory: path to the directory to create (can be nested, relative or absolute).</li>
</ul>
<h4>Returns:</h4>
<p>bool: true if the directory was successfully created or already exists, false otherwise.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	if (directory_exists(&quot;test&quot;)) {
		alert(&quot;Info&quot;, &quot;The test directory already exists; nothing to do&quot;);
		exit();
	}
	if (directory_create(&quot;test&quot;)) {
		alert(&quot;Info&quot;, &quot;Directory created. Deleting...&quot;);
		alert(&quot;Info&quot;, directory_delete(&quot;test&quot;) ? &quot;Success&quot;: &quot;Fail&quot;);
	}
	else
		alert(&quot;Error&quot;, &quot;Couldn't create the directory.&quot;);
}
</code></pre>
<h3>directory_delete</h3>
<p>Deletes a directory.</p>
<p><code>bool directory_delete(string directory);</code></p>
<h4>Arguments:</h4>
<ul>
<li>string directory: the directory to delete.</li>
</ul>
<h4>Returns:</h4>
<p>bool: true if the directory was successfully deleted, false otherwise.</p>
<h3>directory_exists</h3>
<p>Query whether or not a directory exists.</p>
<p>bool directory_exists(const string&amp;in directory);</p>
<h4>Arguments:</h4>
<ul>
<li>const string&amp;in directory: the directory whose existence will be checked (can be a relative or absolute path).</li>
</ul>
<h4>Returns:</h4>
<p>bool: true if the directory exists, false otherwise.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	alert(&quot;Directory exists&quot;, directory_exists(&quot;test&quot;) ? &quot;There is a test folder in the current directory&quot; : &quot;There is not a test folder in the current directory&quot;);
}
</code></pre>
<h3>file_copy</h3>
<p>Coppies a file from one location to another.</p>
<p><code>bool file_copy(const string&amp;in source_filename, const string&amp;in destination_filename);</code></p>
<h4>Arguments:</h4>
<ul>
<li>const string&amp;in source_filename: the path/name of the file to be coppied.</li>
<li>const string&amp;in destination_filename: the path (including filename) to copy the file to.</li>
</ul>
<h4>Returns:</h4>
<p>bool: true if the file was successfully coppied, false otherwise.</p>
<h3>file_delete</h3>
<p>Deletes a file.</p>
<p><code>bool file_delete(const string&amp;in filename);</code></p>
<h4>Arguments:</h4>
<ul>
<li>const string&amp;in filename: the name of the file to delete.</li>
</ul>
<h4>Returns:</h4>
<p>bool: true if the file was successfully deleted, false otherwise.</p>
<h3>file_exists</h3>
<p>Check for the existence of a particular file.</p>
<p><code>bool file_exists(const string&amp;in file_path);</code></p>
<h4>Arguments:</h4>
<ul>
<li>const string&amp;in file_path: the path to the file to query.</li>
</ul>
<h4>Returns:</h4>
<p>bool: true if the file exists, false otherwise.</p>
<h3>file_get_contents</h3>
<p>Reads the entire content of a file and returns it as a string.</p>
<p>string file_get_contents(string filename)</p>
<h4>Arguments:</h4>
<ul>
<li>string filename: the name of the file to read.</li>
</ul>
<h4>Returns:</h4>
<p>The contents of the file on success, an empty string on failure.</p>
<h4>Remarks:</h4>
<p>This is a convenience function, though it is currently the only way to read an Android asset. If you wish to access a file with more control, see the file datastream class.</p>
<p>Be careful to avoid reading files that are too large with this function, as the entire file will be in memory in order to return it as a continguous string.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	string filename = input_box(&quot;Filename&quot;, &quot;Enter the name of a file to read.&quot;, &quot;&quot;);
	string contents = file_get_contents(filename);
	if (contents == &quot;&quot;)
		alert(&quot;Example&quot;, &quot;Either the file was not found, or it contained no text.&quot;);
	else {
		clipboard_set_text(contents);
		alert(&quot;Example&quot;, &quot;The contents of the file is now on your clipboard.&quot;);
	}
}
</code></pre>
<h3>file_get_date_created</h3>
<p>Get a datetime object representing the creation date of a particular file.</p>
<p>datetime file_get_date_created(const string&amp;in filename);</p>
<h4>Arguments:</h4>
<ul>
<li>const string&amp;in filename; the name of the file to check.</li>
</ul>
<h4>Returns:</h4>
<p>datetime: an initialized datetime object, with all its fields set to the creation date of the file.</p>
<h4>Remarks:</h4>
<p>The date returned is in UTC, not your local timezone.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	datetime dt = file_get_date_created(&quot;file_get_date_created.nvgt&quot;);
	alert(&quot;file_get_date_created.nvgt was created on&quot;, dt.year + &quot;-&quot; + dt.month + &quot;-&quot; + dt.day + &quot;, &quot; + dt.hour +&quot;:&quot; + dt.minute + &quot;:&quot; + dt.second);
}
</code></pre>
<h3>file_get_date_modified</h3>
<p>Get a datetime object representing the modification date of a particular file.</p>
<p>datetime file_get_date_modified(const string&amp;in filename);</p>
<h4>Arguments:</h4>
<ul>
<li>const string&amp;in filename: the name of the file to check.</li>
</ul>
<h4>Returns:</h4>
<p>datetime: an initialized datetime object, with all its fields set to the modification date of the file.</p>
<h4>Remarks:</h4>
<p>The date returned is in UTC, not your local timezone.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	datetime dt = file_get_date_modified(&quot;file_get_date_modified.nvgt&quot;);
	alert(&quot;file_get_date_modified.nvgt was modified on&quot;, dt.year + &quot;-&quot; + dt.month + &quot;-&quot; + dt.day + &quot;, &quot; + dt.hour +&quot;:&quot; + dt.minute + &quot;:&quot; + dt.second);
}
</code></pre>
<h3>file_get_size</h3>
<p>Get the size of a file (in bytes).</p>
<p>int64 file_get_size(const string&amp;in filename);</p>
<h4>Arguments:</h4>
<ul>
<li>const string&amp;in filename: the name/path of the file to get the size of.</li>
</ul>
<h4>Returns:</h4>
<p>int64: the size of the file (in bytes).</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	alert(&quot;file_get.size.nvgt is&quot;, file_get_size(&quot;file_get_size.nvgt&quot;) + &quot; bytes&quot;);
}
</code></pre>
<h3>file_put_contents</h3>
<p>Writes a string to a file.</p>
<p>bool file_put_contents(string filename, string content, bool append = false)</p>
<h4>Arguments:</h4>
<ul>
<li><p>string filename: the name of the file to write to.</p>
</li>
<li><p>string content: the content to write.</p>
</li>
<li><p>bool append = false: specifies whether the current contents of the file should be overwritten when writing.</p>
</li>
</ul>
<h4>Returns:</h4>
<p>bool: true on success, false on failure.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	if (!file_put_contents(&quot;example.txt&quot;, &quot;This is an example&quot;))
		alert(&quot;Example&quot;, &quot;Failed to write the file.&quot;);
	else
		alert(&quot;Example&quot;, &quot;Successfully wrote the example file.&quot;);
}
</code></pre>
<h3>get_preferences_path</h3>
<p>Determines the best location to store user data for your game, creating the directory for you if necessary.</p>
<p>string get_preferences_path(string company_name, string product_name);</p>
<h4>Arguments:</h4>
<ul>
<li><p>string company_name: The name of your organization, can be blank.</p>
</li>
<li><p>string product_name: The name of your game or application.</p>
</li>
</ul>
<h4>Remarks:</h4>
<p>This is the recommended way to determine where your game should store application data. While other properties exist such as DIRECTORY_APPDATA which can be used to compose your own path if you desire, this function is generally more robust and platform agnostic than trying to prepare your own storage path using directory constants. This also frees you from needing to check for the existance of the directory before writing to it.</p>
<p>The company name and product name should never change for an application once you start using them, lest players lose access to their previous save data due to the directory changing names. The company name can be blank if you wish to only create one level of new directories in the users appdata, though this is generally not recommended to avoid clutter.</p>
<p>Both the company and product name are expected to contain only spaces and alphanumeric characters if you wish to be as platform agnostic as possible.</p>
<p>You should not assume that DIRECTORY_APPDATA + &quot;/&quot; + company_name + &quot;/&quot; + product_name will be the same as the directory returned by this function, or even that both the company and product names will be used all the time. On android, for example, this function always just returns the app's internal storage path.</p>
<p>This function is also registered as the alias DIRECTORY_PREFERENCES, for those who prefer the old style of directory constants naming.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	string path = get_preferences_path(&quot;&quot;, &quot;documentation example&quot;);
	alert(&quot;test&quot;, &quot;data will be stored at &quot; + path);
	directory_delete(path); // In this example we don't actually want this directory to save.
}
</code></pre>
<h3>glob</h3>
<p>Return a list of files and directories on the filesystem given a path glob.</p>
<p>string[]@ glob(const string&amp;in path_pattern, glob_options options = GLOB_DEFAULT);</p>
<h4>Arguments:</h4>
<ul>
<li><p>const string&amp;in path_pattern: The pattern to match files and directories with (Unix shell like, see remarks).</p>
</li>
<li><p>glob_options options: A bitwise of glob_options enum constants that influence the behavior of this function (see remarks).</p>
</li>
</ul>
<h4>Returns:</h4>
<p>string[]@: A list of all matching files and directories that match the given path pattern, an empty array on no matches or failure.</p>
<h4>Remarks:</h4>
<p>This function provides for one of the easiest ways to enumerate the filesystem in NVGT, particularly because the path patterns provided can actually cause semi-recursive directory searches. The search starts at the current working directory unless an absolute path is given.</p>
<p>The glob patterns have simple rules:</p>
<ul>
<li><p>path separators must be matched exactly, * will not cause a recursive lookup</p>
</li>
<li><p>* matches any sequence of characters</p>
</li>
<li><p>? matches any single character</p>
</li>
<li><p>[set] matches any characters between the brackets</p>
</li>
<li><p>[!set] matches any characters that are not listed between the brackets</p>
</li>
<li><p><code>\*, \[, \] etc</code> exactly match a special character usually used as part of the glob expression</p>
</li>
</ul>
<p>There is no guarantee that the items returned will appear in any particular order in the array.</p>
<p>The following glob_options constance are defined:</p>
<ul>
<li><p>GLOB_DEFAULT: the default options</p>
</li>
<li><p>GLOB_IGNORE_HIDDEN: do not match when directory entries begin with a .</p>
</li>
<li><p>GLOB_FOLLOW_SYMLINKS: traverse even across symbolic links if the given pattern demands it</p>
</li>
<li><p>GLOB_CASELESS: match case insensitively</p>
</li>
</ul>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	// List all .nvgt files within the filesystem documentation directory.
	string[]@ items = glob(&quot;../*/*.nvgt&quot;);
	alert(&quot;files found&quot;, string(items));
}
</code></pre>
<h2>Global Properties</h2>
<h3>DIRECTORY_APPDATA</h3>
<p>Property that returns the user's roaming application directory, which is usually where game data can be written to.</p>
<p>const string DIRECTORY_APPDATA;</p>
<h4>remarks:</h4>
<p>A slash character is already appended to the directory returned by this property.</p>
<p>This function may return different values depending on the operating system the application is being run on.</p>
<ul>
<li><p>On Windows, usually C:\Users%username%\appdata\roaming/.</p>
</li>
<li><p>on macOS, usually ~/Library/Preferences/.</p>
</li>
<li><p>on Linux, usually ~/.config/.</p>
</li>
<li><p>on Android, the app's internal storage path.</p>
</li>
</ul>
<p>In any case, the directory returned should be writable.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	alert(&quot;example&quot;, &quot;data for the game could be stored at &quot; + DIRECTORY_APPDATA + &quot;my_game/&quot;);
}
</code></pre>
<h3>DIRECTORY_TEMP</h3>
<p>Property that returns the system's temporary directory, a place where short-term data can be stored.</p>
<p>const string DIRECTORY_TEMP;</p>
<h4>remarks:</h4>
<p>A slash character is already appended to the directory returned by this property.</p>
<p>This function may return different values depending on the operating system the application is being run on.</p>
<ul>
<li><p>On Windows, usually C:\Users%username%\appdata\local\temp/.</p>
</li>
<li><p>on macOS and Linux systems, usually /tmp/.</p>
</li>
<li><p>on Android, the app's cache path.</p>
</li>
</ul>
<p>In any case the directory returned should be writable, though you should expect things you store there to be deleted by external factors at any time.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	alert(&quot;example&quot;, &quot;a temporary file for the game could be stored at &quot; + DIRECTORY_TEMP + &quot;filename.txt&quot;);
}
</code></pre>
