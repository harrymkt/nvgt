---
title: Security
url: docs/references_builtin_security.html
---

<h1>Security</h1>
<h2>Functions</h2>
<h3>string_aes_decrypt</h3>
<p>Decrypts a string using the AES 256 bit CBC algorithm.</p>
<p>string string_aes_decrypt(const string&amp;in the_data, const string&amp;in the_key)</p>
<h4>Arguments:</h4>
<ul>
<li><p>const string&amp;in the_data: The data to be decrypted.</p>
</li>
<li><p>const string&amp;in the_key: The key to decrypt the data with.</p>
</li>
</ul>
<h4>Returns:</h4>
<p>string: decrypted text on success or an empty string on failure.</p>
<h4>Remarks:</h4>
<p>The Advanced Encryption Standard (AES) is a publicly available algorithm for encrypting data which is trusted world wide at the time of implementation into NVGT. This algorithm takes as input some plain text or binary data, then converts that data into unreadable bytes given an encryption key known only to the programmer. Only with the correct encryption key can the data returned from this function be converted (deciphered) back into the original, unencrypted data.</p>
<p>For anyone interested in more details or who wants more control over the AES encryption such as by providing your own initialization vector, see the aes_encrypt datastream class which gives this control. In the case of this high level encryption function, NVGT will derive an initialization vector from the encryption key provided using hashes, bitwise math, and any other custom security functions a c++ programmer wishes to add to their own version of NVGT. For most users, this is not a concern and most will not even need to know what an initialization vector is to safely use the encryption provided by this function.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	string encrypted_text = string_aes_encrypt(string_base64_decode(&quot;SGVsbG8sIEkgYW0gYSBzdHJpbmch&quot;), &quot;nvgt_example_key_for_docs&quot;); // We encrypt our example string after decoding it with base64; only encoded as such to prevent seeing unreadable characters.
	string decrypted_text = string_aes_decrypt(encrypted_text, &quot;wrong_nvgt_example_key_for_docs&quot;);
	// Show that the text could not be decrypted because the wrong key was provided.
	alert(&quot;example&quot;, decrypted_text); // The dialog will be empty because decrypted_text is an empty string due to decryption failure.
	// Now show how the text can indeed be decrypted with the proper key.
	decrypted_text = string_aes_decrypt(encrypted_text, &quot;nvgt_example_key_for_docs&quot;);
	alert(&quot;example&quot;, decrypted_text);
}
</code></pre>
<h3>string_aes_encrypt</h3>
<p>Encrypts a string using the AES 256 bit CBC algorithm.</p>
<p>string string_aes_encrypt(const string&amp;in the_data, const string&amp;in the_key)</p>
<h4>Arguments:</h4>
<ul>
<li><p>const string&amp;in the_data: The data to be encrypted.</p>
</li>
<li><p>const string&amp;in the_key: The key to encrypt the data with.</p>
</li>
</ul>
<h4>Returns:</h4>
<p>string: Encrypted ciphertext on success or an empty string on failure.</p>
<h4>Remarks:</h4>
<p>The Advanced Encryption Standard (AES) is a publicly available algorithm for encrypting data which is trusted world wide at the time of implementation into NVGT. This algorithm takes as input some plain text or binary data, then converts that data into unreadable bytes given an encryption key known only to the programmer. Only with the correct encryption key can the data returned from this function be converted (deciphered) back into the original, unencrypted data.</p>
<p>For anyone interested in more details or who wants more control over the AES encryption such as by providing your own initialization vector, see the aes_encrypt datastream class which gives this control. In the case of this high level encryption function, NVGT will derive an initialization vector from the encryption key provided using hashes, bitwise math, and any other custom security functions a c++ programmer wishes to add to their own version of NVGT. For most users, this is not a concern and most will not even need to know what an initialization vector is to safely use the encryption provided by this function.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	string plaintext = &quot;Hello, I am a string!&quot;;
	string encrypted_text = string_aes_encrypt(plaintext, &quot;nvgt_example_key_for_docs&quot;);
	// Prove that the text was encrypted by showing a base64 encoded version of it to the user. We encode the encrypted data for display because it may contain unprintable characters after encryption.
	alert(&quot;example&quot;, string_base64_encode(encrypted_text));
	string decrypted_text = string_aes_decrypt(encrypted_text, &quot;wrong_nvgt_example_key_for_docs&quot;);
	// Show that the text could not be decrypted because the wrong key was provided.
	alert(&quot;example&quot;, decrypted_text); // The dialog will be empty because decrypted_text is an empty string due to decryption failure.
	// Now show how the text can indeed be decrypted with the proper key.
	decrypted_text = string_aes_decrypt(encrypted_text, &quot;nvgt_example_key_for_docs&quot;);
	alert(&quot;example&quot;, decrypted_text);
}
</code></pre>
