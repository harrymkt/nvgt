---
title: Instance Management (instance.nvgt)
url: docs/references_include_instance_management_instance.html
---

<h1>Instance Management (instance.nvgt)</h1>
<h2>Instance Management</h2>
<p>This include provides the <code>instance</code> class, which allows you to manage the way multiple instances of your game are handled. For example, you could use this class to check if your game is already running, or stop it from running until only one instance exists.</p>
<h2>Classes</h2>
<h3>instance</h3>
<h4>Methods</h4>
<h5>wait_until_standalone</h5>
<p>This method will make any instances of your game block until there's only one instance still alive.</p>
<p><code>void instance::wait_until_standalone();</code></p>
<h4>Properties</h4>
<h5>is_already_running</h5>
<p>Determines if an instance of the application is already running.</p>
<p>bool instance::is_already_running;</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">#include &quot;instance.nvgt&quot;
void main() {
	instance example(&quot;instance_checker_example&quot;);
	if (example.is_already_running) {
		alert(&quot;Info&quot;, &quot;The script is already running.&quot;);
		exit();
	}
	alert(&quot;Info&quot;, &quot;After you press OK, you'll have 15 seconds to run this script again to see the result&quot;);
	wait(15000);
}
</code></pre>
