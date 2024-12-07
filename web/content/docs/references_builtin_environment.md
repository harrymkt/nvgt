---
title: Environment
url: docs/references_builtin_environment.html
---

<h1>Environment</h1>
<p>In this reference, the environment section specifically refers to the script/system environment that your program is being run on. Examples could include the current line number in the nvgt script being compiled, the operating system being run on or fetching the value of a shell environment variable.</p>
<h2>Functions</h2>
<h3>chdir</h3>
<p>Change the current working directory.</p>
<p>bool chdir(const string&amp;in new_directory);</p>
<h4>Arguments:</h4>
<ul>
<li>const string&amp;in new_directory: The directory you'd like to change into. Note that this directory must already exist.</li>
</ul>
<h4>Returns:</h4>
<p>bool: true if NVGT could set the current working directory to the specified directory; false otherwise.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	string directory = input_box(&quot;Chdir Test&quot;, &quot;Enter a valid path to a directory: &quot;);
	// Could we switch to it?
	if (chdir (directory))
		alert(&quot;Success&quot;, &quot;That directory is valid and could be switch to.&quot;);
	else 
		alert(&quot;Failure&quot;, &quot;The directory could not be switched to. Check that you have typed the name correctly and that the directory exists.&quot;);
}
</code></pre>
<h3>cwdir</h3>
<p>Check the current working directory.</p>
<p>string cwdir();</p>
<h4>Returns:</h4>
<p>string: a string containing the current working directory.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	alert(&quot;Current Working Directory is&quot;, cwdir());
}
</code></pre>
<h3>environment_variable_exists</h3>
<p>Check if the given environment variable exists.</p>
<p>bool environment_variable_exists(const string&amp;in name);</p>
<h4>Arguments:</h4>
<ul>
<li>const string&amp;in name: the name of the environment variable to check.</li>
</ul>
<h4>Returns:</h4>
<p>bool: true if the specified environment variable exists, false otherwise.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	bool exists = environment_variable_exists(&quot;PATH&quot;);
	if (exists)
		alert(&quot;Info&quot;, &quot;The PATH variable exists.&quot;);
	else
		alert(&quot;Info&quot;, &quot;The PATH variable does not exist.&quot;);
}
</code></pre>
<h3>expand_environment_variables</h3>
<p>Expand environment variables.</p>
<p>string expand_environment_variables(const string&amp;in variables);</p>
<h4>Arguments:</h4>
<ul>
<li>const string&amp;in variables: A string containing the variable(s) you wish to expand.</li>
</ul>
<h4>Returns:</h4>
<p>string: the expanded environment variable(s) if successful or an empty string if not.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	// The end goal here is to obtain the user's home directory on the running system if possible. This logic happens in a below function; here we just display the result.
	alert(&quot;Result&quot;, get_home_directory());
}
string get_home_directory() {
	if (system_is_windows) return expand_environment_variables(&quot;%USERPROFILE%&quot;);
	else if (system_is_unix) return expand_environment_variables(&quot;$HOME&quot;);
	else return &quot;Unknown&quot;;
}
</code></pre>
<h3>get_preferred_locales</h3>
<p>Get a list of the user's preferred locales.</p>
<p>string[]@ get_preferred_locales();</p>
<h4>Returns:</h4>
<p>string[]@: a handle to an array containing the locale names (as strings).</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	string[]@ locales = get_preferred_locales();
	string result; // To be shown to the user.
	for (uint i = 0; i &lt; locales.length(); i++)
		result += locales[i] + &quot;,\n&quot;;
	// Strip off the trailing comma and new line.
	result.trim_whitespace_right_this();
	result.erase(result.length() - 1);
	alert(&quot;Info&quot;, &quot;The locales on your system are: &quot; + result);
}
</code></pre>
<h3>system_power_info</h3>
<p>Determine the state of the system's battery.</p>
<p>system_power_state system_power_info(int&amp;out seconds = void, int&amp;out percent = void);</p>
<h4>Arguments:</h4>
<ul>
<li><p>int&amp;out seconds = void: Where to store the number of remaining charge time in seconds.</p>
</li>
<li><p>int&amp;out percent = void: Where to store the percentage of battery charge remaining.</p>
</li>
</ul>
<h4>Returns:</h4>
<p>system_power_state: One of POWER_STATE_ERROR, POWER_STATE_UNKNOWN, POWER_STATE_ON_BATTERY, POWER_STATE_NO_BATTERY, POWER_STATE_CHARGING or POWER_STATE_CHARGED.</p>
<h4>Remarks:</h4>
<p>This could be useful for various reasons, such as backing up game data on low battery or showing extra mercy to online game players who run out of battery power who you might otherwise punish/tag for unlawful disconnection.</p>
<p>If the battery percentage or time remaining cannot be determined, that value will be set to -1.</p>
<p>Whether a time or percentage is available is up to the underlying operating system.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">// Utility function to convert a system_power_state to a string.
string describe_power_state(system_power_state st) {
	switch (st) {
		case POWER_STATE_ERROR: return &quot;error&quot;;
		case POWER_STATE_ON_BATTERY: return &quot;on battery&quot;;
		case POWER_STATE_NO_BATTERY: return &quot;no battery&quot;;
		case POWER_STATE_CHARGING: return &quot;charging&quot;;
		case POWER_STATE_CHARGED: return &quot;charged&quot;;
		default: return &quot;unknown&quot;;
	}
}
void main() {
	system_power_state old_state = system_power_info();
	show_window(describe_power_state(old_state));
	while (!key_pressed(KEY_ESCAPE) and !key_pressed(KEY_AC_BACK)) {
		wait(5);
		int seconds, percent;
		system_power_state st = system_power_info(seconds, percent);
		if (st != old_state) show_window(describe_power_state(st));
		old_state = st;
		if (key_pressed(KEY_SPACE)) {
			string time_str = seconds &gt; -1? &quot; (&quot; + timespan(seconds, 0).format() + &quot;)&quot; : &quot;&quot;;
			screen_reader_speak(percent &gt; -1? percent + &quot;%&quot; + time_str : &quot;unable to determine battery percent&quot;);
		}
	}
}
</code></pre>
<h3>write_environment_variable</h3>
<p>Write to an environment variable.</p>
<p>void write_environment_variable(const string&amp;in variable, const string&amp;in value);</p>
<h4>Arguments:</h4>
<ul>
<li><p>const string&amp;in variable: The environment variable you wish to write to.</p>
</li>
<li><p>const string&amp;in value: The value you wish to write to this variable.</p>
</li>
</ul>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	write_environment_variable(&quot;NVGT_Test_for_docs&quot;, &quot;Testing&quot;);
	alert(&quot;Result&quot;, read_environment_variable(&quot;NVGT_Test_for_docs&quot;));
}
</code></pre>
<h2>Global Properties</h2>
<h3>COMMAND_LINE</h3>
<p>COMMAND_LINE returns anything that is passed as command line arguments. Note that it returns anything after the application name, and keep in mind that you will have to parse the output yourself (basic example below).</p>
<p>const string COMMAND_LINE;</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	const string[]@ arguments = COMMAND_LINE.split(&quot; &quot;);
	// Did we get any arguments?
	if (arguments[0] == &quot;&quot;)
		alert(&quot;Command Line&quot;, &quot;No arguments provided.&quot;);
	else
		alert(&quot;Command Line&quot;, &quot;The first argument is &quot; + arguments[0]);
}
</code></pre>
<h3>PLATFORM</h3>
<p>This property returns a string containing the current platform, such as &quot;Windows NT&quot;.</p>
<p>const string PLATFORM;</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	alert(&quot;Your current Platform  is&quot;, PLATFORM);
}
</code></pre>
<h3>PLATFORM_ARCHITECTURE</h3>
<p>This property returns a string containing the current platform architecture, such as &quot;AMD64&quot;.</p>
<p>const string PLATFORM_ARCHITECTURE;</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	alert(&quot;Your current Platform architecture is&quot;, PLATFORM_ARCHITECTURE);
}
</code></pre>
<h3>PLATFORM_DISPLAY_NAME</h3>
<p>This property returns a string containing the current platform display name, such as &quot;Windows 8&quot;.</p>
<p>const string PLATFORM_DISPLAY_NAME;</p>
<h4>Remarks:</h4>
<p>Due to a backwards compatibility problem in windows, this function by default will cap out at Windows 8 even if the user is running a newer version of Windows. If determining the most modern windows version on the user's system is important to you, you can create a gamename.exe.manifest file to target your app for modern windows. Here is some <a href="https://learn.microsoft.com/en-us/windows/win32/sysinfo/targeting-your-application-at-windows-8-1">microsoft documentation</a> that explains how, you can probably just use the example manifest provided there.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	alert(&quot;Your current Platform display name is&quot;, PLATFORM_DISPLAY_NAME);
}
</code></pre>
<h3>PLATFORM_VERSION</h3>
<p>This property returns a string containing the current platform version, such as &quot;6.2 (Build 9200)&quot;.</p>
<p>const string PLATFORM_VERSION;</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	alert(&quot;Your current Platform version is&quot;, PLATFORM_VERSION);
}
</code></pre>
<h3>PROCESSOR_COUNT</h3>
<p>This property returns the number of processors on your system. Note that this returns the number of threads, not physical cores.</p>
<p>const uint PROCESSOR_COUNT;</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	alert(&quot;Processor Threads Count&quot;, PROCESSOR_COUNT);
}
</code></pre>
<h3>system_is_chromebook</h3>
<p>This property is true if the application is running on a Google Chromebook.</p>
<p>const bool system_is_chromebook;</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	if(system_is_chromebook)
		alert(&quot;example&quot;, &quot;This application is running on a chromebook!&quot;);
	else
		alert(&quot;example&quot;, &quot;This application is not running on a chromebook.&quot;);
}
</code></pre>
<h3>system_is_tablet</h3>
<p>This property is true if the application is running on any device that identifies itself as a tablet.</p>
<p>const bool system_is_tablet;</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	if(system_is_tablet)
		alert(&quot;example&quot;, &quot;This application is running on a tablet!&quot;);
	else
		alert(&quot;example&quot;, &quot;This application is not running on a tablet.&quot;);
}
</code></pre>
<h3>system_is_unix</h3>
<p>This property is true if the application is running on a unix operating system, which in regards to NVGT's platforms is almost everything other than windows.</p>
<p>const bool system_is_unix;</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	if(system_is_unix)
		alert(&quot;example&quot;, &quot;This application is running on a unix operating system!&quot;);
	else
		alert(&quot;example&quot;, &quot;This application is probably running on windows, or in any case not a unix operating system&quot;);
}
</code></pre>
<h3>system_is_windows</h3>
<p>This property is true if the application is running on a windows operating system.</p>
<p>const bool system_is_windows;</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	if(system_is_windows)
		alert(&quot;example&quot;, &quot;This application is running on windows!&quot;);
	else
		alert(&quot;example&quot;, &quot;This application is not running on windows.&quot;);
}
</code></pre>
<h3>system_node_id</h3>
<p>This property returns the node ID, or another words, primary MAC address, of your system.</p>
<p>const string system_node_id;</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	alert(&quot;Your system node/host ID is&quot;, system_node_id);
}
</code></pre>
<h3>system_node_name</h3>
<p>This property returns the node name, or another word, host name, of your system.</p>
<p>const string system_node_name;</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	alert(&quot;Your system node/host name is&quot;, system_node_name);
}
</code></pre>
