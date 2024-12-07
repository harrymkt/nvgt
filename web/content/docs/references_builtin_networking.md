---
title: Networking
url: docs/references_builtin_networking.html
---

<h1>Networking</h1>
<h2>classes</h2>
<h3>http</h3>
<p>Facilitate HTTP requests from a simple, asynchronous interface.</p>
<p>http();</p>
<h4>Remarks:</h4>
<p>This is one of the easiest ways to perform an http request in NVGT without blocking the rest of your code.</p>
<p>Simply create an http object, call either it's get, head or post methods, then begin accessing properties on the object such  as progress, status_code or response_body to query and access details of the request.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">#include &quot;size.nvgt&quot;
#include &quot;speech.nvgt&quot;
void main() {
	// This script downloads the latest NVGT windows installer and saves it in the current working directory.
	http h;
	h.get(&quot;https://nvgt.zip/windows&quot;);
	file f;
	string filename = &quot;&quot;;
	show_window(&quot;downloading...&quot;);
	while (!h.complete) {
		wait(5);
		if (key_pressed(KEY_ESCAPE)) {
			f.close();
			file_delete(filename);
			return; // Destruction of the http object will cancel any requests in progress.
		}
		if (!f.active and h.status_code == 200) { // The file is available.
			string[]@ path = h.url.get_path_segments();
			filename = path.length() &gt; 0? path[-1] : &quot;http.txt&quot;;
			f.open(filename, &quot;wb&quot;);
		}
		if (f.active) f.write(h.response_body);
		if (key_pressed(KEY_SPACE)) speak(round(h.progress * 100, 2) + &quot;%&quot;);
	}
	int keep = question(filename, size_to_string(f.size) + &quot; downloaded, keep file?&quot;);
	f.close();
	if (keep != 1) file_delete(filename);
}
</code></pre>
<h4>Methods</h4>
<h5>get</h5>
<p>Initiate a get request.</p>
<p>bool get(spec::uri url, name_value_collection@ headers = null, http_credentials@ creds = null);</p>
<h6>Arguments:</h6>
<ul>
<li><p>spec::uri url: A valid URI which must have a scheme of either http or https.</p>
</li>
<li><p>name_value_collection@ headers = null: Pairs of extra http headers to pass on to the server.</p>
</li>
<li><p>http_credentials@ creds = null: Optional credentials to authenticate the request with.</p>
</li>
</ul>
<h6>Returns:</h6>
<p>bool: True if the request was initiated, or false if there was an error.</p>
<h6>Remarks:</h6>
<p>Once this method is called and returns true, you will usually want to wait until either http.complete returns true or http.running returns false before thoroughly handling the request. However http.progress, http.status_code, http.response_headers and http.response_body are accessible throughout the request's lifecycle to stream the data or get more detailed information.</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	// Fetch the latest version of NVGT.
	http h;
	if (!h.get(&quot;http://nvgt.gg/downloads/latest_version&quot;)) {
		alert(&quot;oops&quot;, &quot;request failed&quot;); // This class will contain more detailed error management facilities in the near future.
		return;
	}
	h.wait(); // You can also use the h.running or h.complete properties in a loop to execute code in the background while the request progresses.
	alert(&quot;nvgt latest version&quot;, h.response_body);
}
</code></pre>
<h5>reset</h5>
<p>Resets the http object to the state it was in at the time of it's construction, canceling any requests in progress.</p>
<p>void reset();</p>
<h6>Remarks:</h6>
<p>This method waits for the current request to cancel successfully, which is usually instant. However from time to time you could see a small delay as the request thread runs to the next point where it can check the cancelation event.</p>
<p>This method is implicitly called whenever the http object destructs.</p>
<pre><code class="language-NVGT">		// Example:
		void main() {
			http h;
			h.get(&quot;https://nvgt.gg&quot;);
			wait(20);
			h.reset();
			h.get(&quot;https://samtupy.com/ip.php&quot;);
			h.wait();
			if (h.status_code != 200) alert(&quot;oops &quot; + h.status_code, h.response_body);
			else alert(&quot;IP address displayed after http reset&quot;, h.response_body);
		}
</code></pre>
<h5>wait</h5>
<p>Waits for the current request to complete.</p>
<p><code>void wait();</code></p>
<h6>Remarks:</h6>
<p>If no request is in progress, this will return emmedietly. Otherwise, it will block code execution on the calling thread until the request has finished.</p>
<h4>Properties</h4>
<h5>progress</h5>
<p>Determine the percentage of the request download (from 0.0 to 1.0.</p>
<p><code>const float progress;</code></p>
<h6>Remarks:</h6>
<p>This property will be 0 if a request is not in progress or if it is not yet in a state where the content length of the download can be known, and -1 if the progress cannot be determined such as if the remote endpoint does not provide a Content-Length header.</p>
<h5>response_body</h5>
<p>Read and consume any new data from the current request.</p>
<p><code>const string response_body;</code></p>
<h6>Remarks:</h6>
<p>It is important to note that accessing this property will flush the buffer stored in the request. This means that for example you do not want to access http.response_body.length(); because the next time http.response_body is accessed it will be empty or might contain new data.</p>
<p>Proper usage is to continuously append the value of this property to a string or datastream in a loop while h.running is true or h.complete is false.</p>
<h3>network</h3>
<h4>methods</h4>
<h5>connect</h5>
<p>Attempt to establish a connection with a server, only works when set up as a client.</p>
<p><code>uint64 network::connect(const string&amp;in hostname, uint16 port);</code></p>
<h6>Arguments:</h6>
<ul>
<li>const string&amp;in hostname: the hostname/IP address to connect to.</li>
<li>uint16 port: the port to use.</li>
</ul>
<h6>Returns:</h6>
<p>uint64: the peer ID of the connection, or 0 on error.</p>
<h5>destroy</h5>
<p>Destroys the network object, freeing all its resources, active connections, etc.</p>
<p><code>void network::destroy();</code></p>
<h5>disconnect_peer</h5>
<p>Tell a peer to disconnect and completely disregard its message queue. This means that the peer will be told to disconnect without sending any of its queued packets (if any).</p>
<p><code>bool network::disconnect_peer(uint peer_id);</code></p>
<h6>Arguments:</h6>
<ul>
<li>uint peer_id: the ID of the peer to disconnect.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true on success, false otherwise.</p>
<h5>disconnect_peer_forcefully</h5>
<p>Forcefully disconnect a peer. Unlike <code>network::disconnect_peer()</code>, this function doesn't send any sort of notification of the disconnection to the remote peer, instead it closes the connection immediately.</p>
<p><code>bool network::disconnect_peer_forcefully(uint peer_id);</code></p>
<h6>Arguments:</h6>
<ul>
<li>uint peer_id: the ID of the peer to disconnect.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true on success, false otherwise.</p>
<h5>disconnect_peer_softly</h5>
<p>Send a disconnect packet for a peer after sending any remaining packets in the queue and notifying the peer.</p>
<p><code>bool network::disconnect_peer_softly(uint peer_id);</code></p>
<h6>Arguments:</h6>
<ul>
<li>uint peer_id: the ID of the peer to disconnect.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true on success, false otherwise.</p>
<h5>get_peer_address</h5>
<p>Returns the IP address of a particular peer.</p>
<p><code>string network::get_peer_address(uint peer_id);</code></p>
<h6>Arguments:</h6>
<ul>
<li>uint peer_id: the ID of the peer to check.</li>
</ul>
<h6>Returns:</h6>
<p>string: the IP address of the specified peer.</p>
<h5>get_peer_list</h5>
<p>Return a list of all peer ID's currently connected to the server.</p>
<p><code>uint[]@ network::get_peer_list();</code></p>
<h6>Returns:</h6>
<p>uint[]@: a handle to an array containing the ID of every peer currently connected to the server.</p>
<h5>request</h5>
<p>This is the function you'll probably be calling the most when you're dealing with the network object in NVGT. It checks if an event has occurred since the last time it checked. If it has, it returns you a network_event handle with info about it.</p>
<p><code>network_event@ network::request(uint timeout = 0);</code></p>
<h6>Arguments:</h6>
<ul>
<li>uint timeout = 0: an optional timeout on your packet receiving (see remarks for more information).</li>
</ul>
<h6>Returns:</h6>
<p>network_event@: a handle to a <code>network_event</code> object containing info about the last received event.</p>
<h6>Remarks:</h6>
<p>The timeout parameter is in milliseconds, and it determines how long Enet will wait for new packets before returning control back to the calling application. However, if it receives a packet within the timeout period, it will return and you'll be handed the packet straight away.</p>
<h5>send</h5>
<p>Attempt to send a packet over the network.</p>
<p><code>bool network::send(uint peer_id, const string&amp;in message, uint8 channel, bool reliable = true);</code></p>
<h6>Arguments:</h6>
<ul>
<li>uint peer_id: the ID of the peer to send to (specify 1 to send to the server from a client).</li>
<li>const string&amp;in message: the message to send.</li>
<li>uint8 channel: the channel to send the message on (see the main networking documentation for more details).</li>
<li>bool reliable = true: whether or not the packet should be sent reliably or not (see the main networking documentation for more details).</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the packet was successfully sent, false otherwise.</p>
<h5>send_reliable</h5>
<p>Attempt to send a packet over the network reliably.</p>
<p><code>bool network::send_reliable(uint peer_id, const string&amp;in message, uint8 channel);</code></p>
<h6>Arguments:</h6>
<ul>
<li>uint peer_id: the ID of the peer to send to (specify 1 to send to the server from a client).</li>
<li>const string&amp;in message: the message to send.</li>
<li>uint8 channel: the channel to send the message on (see the main networking documentation for more details).</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the packet was successfully sent, false otherwise.</p>
<h5>send_unreliable</h5>
<p>Attempt to send a packet over the network unreliably.</p>
<p><code>bool network::send_unreliable(uint peer_id, const string&amp;in message, uint8 channel);</code></p>
<h6>Arguments:</h6>
<ul>
<li>uint peer_id: the ID of the peer to send to (specify 1 to send to the server from a client).</li>
<li>const string&amp;in message: the message to send.</li>
<li>uint8 channel: the channel to send the message on (see the main networking documentation for more details).</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the packet was successfully sent, false otherwise.</p>
<h5>set_bandwidth_limits</h5>
<p>Set the incoming and outgoing bandwidth limits of the server (in bytes-per-second).</p>
<p><code>void network::set_bandwidth_limits(uint incoming, uint outgoing);</code></p>
<h6>Arguments:</h6>
<ul>
<li>uint incoming: the maximum number of allowed incoming bytes per second.</li>
<li>uint outgoing: the maximum number of allowed outgoing bytes per second.</li>
</ul>
<h5>setup_client</h5>
<p>Sets up the network object as a client.</p>
<p><code>bool network::setup_client(uint8 max_channels, uint16 max_peers);</code></p>
<h6>Arguments:</h6>
<ul>
<li>uint8 max_channels: the maximum number of channels used on the connection (up to 255).</li>
<li>uint16 max_peers: the maximum number of peers allowed by the connection (maximum is 65535).</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the client was successfully set up, false otherwise.</p>
<h5>setup_local_server</h5>
<p>Sets up the network object as a local server on localhost.</p>
<p><code>bool network::setup_local_server(uint16 bind_port, uint8 max_channels, uint16 max_peers);</code></p>
<h6>Arguments:</h6>
<ul>
<li>uint16 bind_port: the port to bind the server to.</li>
<li>uint8 max_channels: the maximum number of channels used on the connection (up to 255).</li>
<li>uint16 max_peers: the maximum number of peers allowed by the connection (maximum is 65535).</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the server was successfully set up, false otherwise.</p>
<h5>setup_server</h5>
<p>Sets up the network object as a server.</p>
<p><code>bool network::setup_server(uint16 bind_port, uint8 max_channels, uint16 max_peers);</code></p>
<h6>Arguments:</h6>
<ul>
<li>uint16 bind_port: the port to bind the server to.</li>
<li>uint8 max_channels: the maximum number of channels used on the connection (up to 255).</li>
<li>uint16 max_peers: the maximum number of peers allowed by the connection (maximum is 65535).</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the server was successfully set up, false otherwise.</p>
<h4>properties</h4>
<h5>active</h5>
<p>Determine if the network object is active (e.g. a setup_* method has successfully been called on it).</p>
<p><code>bool network::active;</code></p>
<h5>bytes_received</h5>
<p>The number of bytes this network object has received since being set up.</p>
<p><code>uint network::bytes_received;</code></p>
<h5>bytes_sent</h5>
<p>The number of bytes this network object has sent since being set up.</p>
<p><code>uint network::bytes_sent;</code></p>
<h5>connected_peers</h5>
<p>The number of peers currently connected to the server.</p>
<p><code>uint network::connected_peers;</code></p>
<h3>network_event</h3>
<p>This class represents an event received with the network object's <code>request()</code> method. It contains information such as the the ID of the peer that sent the event, the message the event was sent on, and the actual packet data itself.</p>
<h4>methods</h4>
<h5>opAssign</h5>
<p>This class implements the <code>opAssign()</code> operator overload, meaning it can be assigned with the &quot;=&quot; operator to another network_event.</p>
<p><code>network_event@ opAssign(network_event@ e);</code></p>
<h4>properties</h4>
<h5>channel</h5>
<p>The channel this event was sent on. See the main networking documentation for more information.</p>
<p><code>uint network_event::channel;</code></p>
<h5>message</h5>
<p>The data associated with this event (AKA the packet).</p>
<p><code>string network_event::message;</code></p>
<h5>peer_id</h5>
<p>The peer ID of the connection this event came from. See the main networking documentation for more information.</p>
<p><code>uint network_event::peer_id;</code></p>
<h5>type</h5>
<p>The type of the network event (see event types for more information).</p>
<p><code>int network_event::type;</code></p>
<h2>Constants</h2>
<h3>Event Types</h3>
<p>This is a list of all the constants supported as event types by NVGT's networking layer.</p>
<ul>
<li>event_type_none: no event.</li>
<li>event_type_connect: a new user wants to connect.</li>
<li>event_type_disconnect: a user wants to disconnect.</li>
<li>event_type_receive: a user sent a packet.</li>
</ul>
