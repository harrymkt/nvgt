---
title: Profiling and Debugging
url: docs/references_builtin_profiling_and_debugging.html
---

<h1>Profiling and Debugging</h1>
<h2>Functions</h2>
<h3>c_debug_message</h3>
<p>Print a message to the C debugger.</p>
<p>void c_debug_message(const string&amp;in message);</p>
<h4>Arguments:</h4>
<ul>
<li>const string&amp;in message: The message to print to the C debugger's console.</li>
</ul>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	c_debug_message(&quot;I am a debug message&quot;);
	c_debug_break();
}
</code></pre>
<h3>get_call_stack</h3>
<p>Get the call stack (list of functions called) at the current point in time in your script.</p>
<p>string get_call_stack();</p>
<h4>Returns:</h4>
<p>string: a formatted list of the call stack.</p>
<h4>Remarks:</h4>
<p>In the context of a catch block, it's better to use the <code>last_exception_call_stack</code> property. If you use <code>get_call_stack()</code>, you'll get the callstack where you are in the try statement, as opposed to the call stack that actually caused the exception being caught.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">// Define some example functions.
void test1() {test2();}
void test2() {test3();}
void test3() {
	alert(&quot;Call stack&quot;, get_call_stack());
}
void main() {
	test1();
}
</code></pre>
<h3>get_call_stack_size</h3>
<p>Get the size of the call stack.</p>
<p>int get_call_stack_size();</p>
<h4>Returns:</h4>
<p>int: the size of the call stack (i.e. how many functions deep are you currently?)</p>
<h4>Remarks:</h4>
<p>This function doesn't work in the context of exceptions. If you call it in a catch block, you'll most likely get the call stack in the try block, not what actually threw the exception.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void test1() {test2();}
void test2() {test3();}
void test3() {test4();}
void test4() {
	alert(&quot;Call stack size is&quot;, get_call_stack_size());
}
void main() {
	test1();
}
</code></pre>
<h3>get_exception_file</h3>
<p>Get the name/path of the source file where the exception occurred.</p>
<p>string get_exception_file();</p>
<h4>Returns:</h4>
<p>string: the name/path of the file where the exception was thrown.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	try {
		// Throw an index-out-of-bounds error.
		string[] arr = {&quot;a&quot;, &quot;test&quot;};
		string item = arr[2];
	}
	catch {
		alert(&quot;Exception file path&quot;, get_exception_file());
	}
}
</code></pre>
<h3>get_exception_function</h3>
<p>Get the Angelscript function signature of the function that threw the exception.</p>
<p>string get_exception_function();</p>
<h4>Returns:</h4>
<p>string: the Angelscript function signature of the throwing function.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	try {
		// Throw an index-out-of-bounds error.
		string[] arr = {&quot;a&quot;, &quot;test&quot;};
		string item = arr[2];
	}
	catch {
		alert(&quot;Exception function signature&quot;, get_exception_function());
	}
}
</code></pre>
<h3>get_exception_info</h3>
<p>Get informative information about an exception, for example &quot;index-out-of-bounds&quot;.</p>
<p>string get_exception_info();</p>
<h4>Returns:</h4>
<p>string: information about the exception currently being caught.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	try {
		// Throw an index-out-of-bounds error.
		string[] arr = {&quot;a&quot;, &quot;test&quot;};
		string item = arr[2];
	}
	catch {
		alert(&quot;Exception info&quot;, get_exception_info());
	}
}
</code></pre>
<h3>get_exception_line</h3>
<p>Get the line an exception occurred on.</p>
<p>int get_exception_line();</p>
<h4>Returns:</h4>
<p>int: the line number the exception occurred on.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	try {
		// Throw an index-out-of-bounds error.
		string[] arr = {&quot;a&quot;, &quot;test&quot;};
		string item = arr[2];
	}
	catch {
		alert(&quot;Exception line&quot;, get_exception_line());
	}
}
</code></pre>
<h3>is_debugger_present</h3>
<p>Determines if your app is being ran through a debugger.</p>
<p>bool is_debugger_present();</p>
<h4>Returns:</h4>
<p>bool: true if a debugger is present, false otherwise.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	bool present = is_debugger_present();
	if (present)
		alert(&quot;Info&quot;, &quot;A debugger is present.&quot;);
	else
		alert(&quot;Info&quot;, &quot;A debugger is not present.&quot;);
}
</code></pre>
<h3>throw</h3>
<p>Throws an exception with a particular message.</p>
<p>void throw(const string&amp;in msg);</p>
<h4>Arguments:</h4>
<ul>
<li>const string&amp;in msg: the message to include in your exception.</li>
</ul>
<h4>Remarks:</h4>
<p>This is presently slightly limited, the only value of the exception you can set is the message. There are plans to expand this in the future.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	throw(&quot;Something went horribly wrong&quot;);
}
</code></pre>
<h2>Global Properties</h2>
<h3>last_exception_call_stack</h3>
<p>Returns the call stack of the currently thrown exception.</p>
<p>string last_exception_call_stack;</p>
<h4>Remarks:</h4>
<p>In the context of a catch block, it's better to use this property over <code>get_call_stack()</code>. In a catch block, <code>get_call_stack()</code> will return the callstack where you are in the try statement, as opposed to the call stack that actually caused the exception being caught.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void test1() {test2();}
void test2() {throw(&quot;I am an exception&quot;);}
void main() {
	try {
		test1();
	}
	catch {
		alert(&quot;Call stack&quot;, last_exception_call_stack);
	}
}
</code></pre>
<h3>SCRIPT_COMPILED</h3>
<p>Determine if the script is compiled or not. I.e., are you running from source?</p>
<p>bool SCRIPT_COMPILED;</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	alert(&quot;Example&quot;, SCRIPT_COMPILED ? &quot;The script is currently compiled&quot; : &quot;The script is not currently compiled&quot;);
}
</code></pre>
<h3>SCRIPT_CURRENT_FILE</h3>
<p>Returns the current file your script is running form.</p>
<p>string SCRIPT_CURRENT_FILE;</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	alert(&quot;Your script is contained in&quot;, SCRIPT_CURRENT_FILE);
}
</code></pre>
<h3>SCRIPT_CURRENT_FUNCTION</h3>
<p>Returns the signature of the current function in your script.</p>
<p>string SCRIPT_CURRENT_FUNCTION;</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	alert(&quot;The current function is&quot;, SCRIPT_CURRENT_FUNCTION);
	random_func(&quot;&quot;, 0, 0, 0);
}
// Function with random unused parameters to showcase the function signatures.
bool random_func(const string&amp; in a, int b, uint64 c, uint8 = 1) {
	alert(&quot;The current function is&quot;, SCRIPT_CURRENT_FUNCTION);
	return true;
}
</code></pre>
<h3>SCRIPT_CURRENT_LINE</h3>
<p>Returns the current line in your script as it's executing.</p>
<p>string SCRIPT_CURRENT_LINE;</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	alert(&quot;The current line is&quot;, SCRIPT_CURRENT_LINE);
}
</code></pre>
<h3>SCRIPT_EXECUTABLE</h3>
<p>Returns the path of the executable running your script.</p>
<p>string SCRIPT_EXECUTABLE;</p>
<h4>Remarks:</h4>
<p>If you're running from source, this will return the path to your NVGT binary.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	alert(&quot;The executable path of the script is&quot;, SCRIPT_EXECUTABLE);
}
</code></pre>
