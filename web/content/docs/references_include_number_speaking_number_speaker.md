---
title: Number Speaking (number_speaker.nvgt)
url: docs/references_include_number_speaking_number_speaker.html
---

<h1>Number Speaking (number_speaker.nvgt)</h1>
<h2>classes</h2>
<h3>number_speaker</h3>
<p>The <code>number_speaker</code> object is used to facilitate natural and smooth number speech. It is best to use this class if you're developing a game with voice acting.</p>
<p>number_speaker();</p>
<h4>Remarks:</h4>
<p>The <code>number_speaker</code> class searches for sound files that match the spoken components of a number as closely as possible, separating words with an underscore. For instance, if the number is 72, it'll first check for a file named seventy_two.wav. If this file is not available, it'll search for seventy.wav and two.wav and combine them.</p>
<p>This system allows you to record as many number sounds as desired to achieve flawless spoken output. Alternatively, you can record only essential numbers, such as zero.wav to nineteen.wav, twenty.wav to ninety.wav, and optionally hundred.wav, thousand.wav, and million.wav. You can also record a file named minus.wav to distinguish between positive and negative numbers, as well as and.ogg to have the word &quot;and&quot; spoken if the include_and parameter is enabled.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">#include &quot;number_speaker.nvgt&quot;
void main() {
	// Speak a number using speak_wait.
	number_speaker test;
	test.speak_wait(350);
}
</code></pre>
<h4>methods</h4>
<h5>speak</h5>
<p>This method will speak a number.</p>
<p>int number_speaker::speak(double the_number);</p>
<h6>Arguments:</h6>
<ul>
<li>double the_number: the number to speak.</li>
</ul>
<h6>Returns:</h6>
<p>int: 0 on success, -1 on failure.</p>
<h6>Remarks:</h6>
<p>The speak method searches for sound files based on the values stored in the prepend and append properties, determining the most appropriate sound files to use by performing multiple searches based on the given number.</p>
<p>When this function is called, it returns immediately, allowing the script to continue running while the number is being spoken. To ensure that numbers are spoken smoothly and fluently, it is necessary to call the speak_next method continuously.</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">#include &quot;number_speaker.nvgt&quot;
void main() {
	number_speaker number;
	number.speak(350);
	while(number.speak_next()==1) {
		wait(5);
	}
}
</code></pre>
<h5>speak_next</h5>
<p>This method is used to check the status of a number that is currently being spoken or has already been spoken, and, if necessary, initiates the playback of the next number.</p>
<p>int number_speaker::speak_next();</p>
<h6>Returns:</h6>
<p>int: 0 if there are no more files to be played, 1 if there are more files to be played or if the last file is still playing, and -1 if an error occurs.</p>
<h6>Remarks:</h6>
<p>The speak_next method works in conjunction with the speak method and should be used continuously while the number is being spoken.</p>
<p>This method functions not only as a status indicator but also as a trigger, checking and playing numbers as needed. To ensure that the numbers are spoken smoothly and fluently, it is essential to perform this check at regular intervals, approximately every 5 milliseconds.</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">#include &quot;number_speaker.nvgt&quot;
void main() {
	// Speak a number using speak and speak_next.
	number_speaker test;
	test.speak(350);
	while(test.speak_next()==1) {
		wait(5);
	}
}
</code></pre>
<h5>speak_wait</h5>
<p>This method will speak a number and wait until the number is fully read before returning.</p>
<p>int number_speaker::speak_wait(double the_number);</p>
<h6>Arguments:</h6>
<ul>
<li>double the_number: the number to speak.</li>
</ul>
<h6>Returns:</h6>
<p>int: 0 on success, -1 on failure.</p>
<h6>Remarks:</h6>
<p>The speak_wait method searches for sound files based on the values stored in the prepend and append properties, determining the most appropriate sound files to use by performing multiple searches based on the given number.</p>
<p>The speak_wait function pauses execution until the number has been fully spoken before returning. This means that the script execution is halted for the duration of the reading. To avoid this, you can use the speak and speak_next methods instead.</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">#include &quot;number_speaker.nvgt&quot;
void main() {
	// Speak a number using speak_wait.
	number_speaker test;
	test.speak_wait(350);
}
</code></pre>
<h5>stop</h5>
<p>This method stops any number that is currently being spoken.</p>
<p>void number_speaker::stop();</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">#include &quot;number_speaker.nvgt&quot;
void main() {
	// Speak a number using speak and speak_next, stopping it prematurely if the user presses space.
	number_speaker test;
	test.speak(350);
	while(test.speak_next()==1) {
		if(key_pressed(KEY_SPACE))
			test.stop();
		wait(5);
	}
}
</code></pre>
<h5>set_sound_object</h5>
<p>This method allows you to specify an existing sound object to be used for any auditory feedback in the number speaker.</p>
<p>bool number_speaker::set_sound_object(sound@ handle);</p>
<h6>Arguments:</h6>
<ul>
<li>sound@ handle: a reference to an existing sound object that will be utilized for all future sound output.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true on success, false on failure.</p>
<h6>Remarks:</h6>
<p>The object specified in this function will handle all future auditory feedback provided by the number speaker. If this method is not called, an internal sound object will be used by default for sound output.</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">#include &quot;number_speaker.nvgt&quot;
void main() {
	sound test;
	number_speaker number;
	number.set_sound_object(test);
	number.speak_wait(350);
}
</code></pre>
<h4>properties</h4>
<h5>append</h5>
<p>This string will be appended to any loaded number file. The default extension is .wav, so you only need to change this if your number files use a different extension.</p>
<p><code>string number_speaker::append;</code></p>
<h5>prepend</h5>
<p>This string will be prepended to any loaded number file. It is useful if your number files are stored in a separate directory or if the filenames include a specific prefix.</p>
<p><code>string number_speaker::prepend;</code></p>
<h5>include_and</h5>
<p>This boolean determines whether the word &quot;and&quot; should be included in the appropriate places in the output. If set to true, you must create a file named and.wav, unless the extension (e.g., the append property) is something other than .wav. The default value is false.</p>
<p><code>bool number_speaker::include_and;</code></p>
<h5>pack_file</h5>
<p>The pack file to use in the object.</p>
<p><code>pack@ number_speaker::pack_file = null;</code></p>
