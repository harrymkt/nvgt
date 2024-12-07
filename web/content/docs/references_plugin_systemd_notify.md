---
title: systemd_notify
url: docs/references_plugin_systemd_notify.html
---

<h1>systemd_notify</h1>
<p>Wrapper for the sd_notify Linux function which can be useful if you are writing a systemd service. On Windows you can include this plugin and compile your game, this function will do nothing. On Linux though, values will be sent to systemd as described in the sd_notify man page (see remarks) when this function is called.</p>
<p>int systemd_notify(string state);</p>
<h2>Arguments:</h2>
<ul>
<li>string state: the message to send to systemd.</li>
</ul>
<h2>Returns:</h2>
<p>int: the value returned by sd_notify.</p>
<h2>Remarks:</h2>
<p>For more information about systemd, see its man page: https://man7.org/linux/man-pages/man3/sd_notify.3.html</p>
<h2>Example:</h2>
<pre><code class="language-NVGT">#pragma plugin systemd_notify
#pragma platform linux
void main() {
	if (PLATFORM.lower() == &quot;linux&quot;)
		systemd_notify(&quot;WATCHDOG=1&quot;); // Only useful within a systemd service.
	else
		alert(&quot;Info&quot;, &quot;This example only works on Linux&quot;);
}
</code></pre>
