---
title: Token Generation (token_gen.nvgt)
url: docs/references_include_token_generation_token_gen.html
---

<h1>Token Generation (token_gen.nvgt)</h1>
<h2>Token generation include</h2>
<p>Allows you to easily generate random strings of characters of any length in a given mode, and possibly custom function if you want to generate only certain characters.</p>
<h2>Enums</h2>
<h3>token_gen_flag</h3>
<p>This enum holds various constants that can be passed to the mode parameter of the generate_token function in order to control what characters appear in results.</p>
<ul>
<li>TOKEN_CHARACTERS = 1: Allows for characters, a-zA-Z</li>
<li>TOKEN_NUMBERS = 2: Allows for numbers, 0-9</li>
<li>TOKEN_SYMBOLS = 4: Uses only symbols, `~!@#$%^&amp;*()_+=-[]{}/.,;:|?&gt;&lt;</li>
</ul>
<h4>Remarks:</h4>
<p>These are flags that should be combined together using the bitwise OR operator. To generate a token containing characters, numbers and symbols, for example, you would pass <code>TOKEN_CHARACTERS | TOKEN_NUMBERS | TOKEN_SYMBOLS</code> to the mode argument of generate_token. The default flags are <code>TOKEN_CHARACTERS | TOKEN_NUMBERS</code>.</p>
<h2>Functions</h2>
<h3>generate_token</h3>
<p>Generates a random string of characters (a token).</p>
<p>string generate_token(int token_length, int mode = TOKEN_CHARACTERS | TOKEN_NUMBERS)</p>
<h4>Arguments:</h4>
<ul>
<li><p>int token_length: the length of the token to generate.</p>
</li>
<li><p>int mode = TOKEN_CHARACTERS | TOKEN_NUMBERS: allows you to specify which characters you would like in the generated token (see remarks).</p>
</li>
</ul>
<h4>returns:</h4>
<p>String: a random token depending on the modes.</p>
<h4>Remarks:</h4>
<p>This function uses the <code>generate_custom_token</code> function to generate. The characters used to generate the token will depend on the modes you specified. See <code>token_gen_flags</code> enum constants for a list of supported modes that can be passed to the mode parameter.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">#include &quot;token_gen.nvgt&quot;
void main() {
	alert(&quot;Info&quot;, &quot;Your token is: &quot; + generate_token(10));
	alert(&quot;Info&quot;, &quot;Numbers only token is: &quot; + generate_token(10, TOKEN_NUMBERS));
	alert(&quot;Info&quot;, &quot;Characters only token is: &quot; + generate_token(10, TOKEN_CHARACTERS));
}
</code></pre>
<h3>generate_custom_token</h3>
<p>Generates a random string of characters (a token) while allowing you to directly specify the characters you wish to use in the generation.</p>
<p>string generate_custom_token(int token_length, string characters);</p>
<h4>Arguments:</h4>
<ul>
<li><p>int token_length: the length of the token to generate.</p>
</li>
<li><p>string characters: a list of characters to generate.</p>
</li>
</ul>
<h4>returns:</h4>
<p>String: a random token.</p>
<h4>Remarks:</h4>
<p>If the <code>characters</code> string is empty or <code>token_length</code> is set to 0 or less, an empty string is returned.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">#include &quot;token_gen.nvgt&quot;
void main() {
	alert(&quot;Info&quot;, &quot;Your A to C token is: &quot; + generate_custom_token(10, &quot;abc&quot;));
	alert(&quot;Info&quot;, &quot;A to C with capitals included token is: &quot; + generate_custom_token(10, &quot;abcABC&quot;));
}
</code></pre>
