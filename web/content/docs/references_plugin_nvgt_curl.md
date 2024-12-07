---
title: nvgt_curl
url: docs/references_plugin_nvgt_curl.html
---

<h1>nvgt_curl</h1>
<h2>classes</h2>
<h3>internet_request</h3>
<h4>properties</h4>
<h5>bytes_downloaded</h5>
<p>The number of bytes currently downloaded with this internet_request.</p>
<p><code>double internet_request::bytes_downloaded;</code></p>
<h5>bytes_uploaded</h5>
<p>The number of bytes that have been uploaded with this internet_request.</p>
<p><code>double internet_request::bytes_uploaded;</code></p>
<h5>complete</h5>
<p>Determine if the active request has completed yet or not.</p>
<p><code>bool internet_request::complete;</code></p>
<h5>download_percent</h5>
<p>The current percentage downloaded.</p>
<p><code>double internet_request::download_percent;</code></p>
<h5>download_size</h5>
<p>The size of the data you're downloading (in bytes).</p>
<p><code>double internet_request::download_size;</code></p>
<h5>follow_redirects</h5>
<p>Should your request follow HTTP redirects?</p>
<p><code>bool internet_request::follow_redirects;</code></p>
<h5>in_progress</h5>
<p>Determine if the request is currently in progress.</p>
<p><code>bool internet_request::in_progress;</code></p>
<h5>max_redirects</h5>
<p>The maximum number of redirects to perform before giving up.</p>
<p><code>int internet_request::max_redirects;</code></p>
<h5>no_curl</h5>
<p>Tells you if libcurl was successfully able to initialize this request, do not use this object if this property is false!</p>
<p><code>bool no_curl;</code></p>
<h5>status_code</h5>
<p>Represents the HTTP status code returned by this request.</p>
<p><code>int internet_request::status_code;</code></p>
<h5>upload_percent</h5>
<p>The percentage uploaded.</p>
<p><code>double internet_request::upload_percent;</code></p>
<h5>upload_size</h5>
<p>The size of your upload (in bytes).</p>
<p><code>double internet_request::upload_size;</code></p>
<h2>functions</h2>
<h3>curl_url_decode</h3>
<p>Decode an encoded URL using curl.</p>
<p><code>string curl_url_decode(string url);</code></p>
<h4>Arguments:</h4>
<ul>
<li>string url: the URL to decode.</li>
</ul>
<h4>Returns:</h4>
<p>string: the decoded URL.</p>
<h4>Remarks:</h4>
<p>This functionality exists natively in NVGT too, the curl functions are just provided here for completeness. For more information, see the built-in <code>url_decode()</code> function.</p>
<h3>curl_url_encode</h3>
<p>Encode a URL using curl.</p>
<p><code>string curl_url_encode(string url);</code></p>
<h4>Arguments:</h4>
<ul>
<li>string url: the URL to encode.</li>
</ul>
<h4>Returns:</h4>
<p>string: the encoded URL.</p>
<h4>Remarks:</h4>
<p>This functionality exists natively in NVGT too, the curl functions are just provided here for completeness. For more information, see the built-in <code>url_encode()</code> function.</p>
