---
title: Text-To-Speech
url: docs/references_builtin_texttospeech.html
---

<h1>Text-To-Speech</h1>
<h2>Text to speech</h2>
<p>This section contains references for the functionality that allows for speech output. Both direct speech engine support is available as well as outputting to screen readers.</p>
<h3>Notes on screen Reader Speech functions</h3>
<p>This set of functions lets you output to virtually any screen reader, either through speech, braille, or both. In addition, you can query the availability of speech/braille in your given screen reader, get the name of the active screen reader, and much more!</p>
<p>On Windows, we use the <a href="https://github.com/dkager/tolk">Tolk</a> library. If you want screen reader speech to work on Windows, you have to make sure Tolk.dll, nvdaControllerClient64.dll, and SAAPI64.dll are in the lib folder you ship with your games.</p>
<h2>classes</h2>
<h3>tts_voice</h3>
<p>This class provides a convenient way to communicate with all of the text-to-speech voices a user has installed on their system.</p>
<p>tts_voice();</p>
<h4>Remarks:</h4>
<p>NVGT implements a tiny <a href="https://github.com/mattiasgustavsson/libs/blob/main/speech.h">builtin fallback speech synthesizer</a> that is used either when there is no speech engine available on the system, or if it is explicitly set with the tts_voice::set_voice() function. It sounds terrible, and is only intended for emergencies, after all understandable speech is better than no speech at all. It was used heavily when porting NVGT to other platforms, because it allowed focus to be primarily fixed on getting nvgt to run while individual tts engine support on each platform could be added later. If you don't want your end users to be able to select this speech synthesizer, pass a blank string to this constructor.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	tts_voice v;
	v.speak_wait(&quot;Type some text and I'll repeat it. Leave the field blank to stop&quot;);
	string text = &quot;&quot;;
	while (true) {
		text = input_box(&quot;Text&quot;, &quot;Type some text to have the TTS speak.&quot;);
		if (text.empty()) break;
		v.speak(text);
	}
}
</code></pre>
<h4>Methods</h4>
<h5>get_speaking</h5>
<p>Check if the text to speech voice is currently speaking.</p>
<p>bool tts_voice::get_speaking();</p>
<h6>Returns:</h6>
<ul>
<li>bool: whether the tts voice is speaking. True if so, false if not.</li>
</ul>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	tts_voice v;
	alert(&quot;Is it speaking right now?&quot;, v.get_speaking());
	v.speak(&quot;I'm now saying something, I think...&quot;);
	wait(250);
	alert(&quot;How about now?&quot;, v.get_speaking());
}
</code></pre>
<h5>get_voice_count</h5>
<p>Get a count of all available text to speech voices, including the builtin.</p>
<p>int tts_voice::get_voice_count();</p>
<h6>Returns:</h6>
<ul>
<li>int: the number of tts voices.</li>
</ul>
<h6>Remarks:</h6>
<p>The default voice built into Nvgt is counted here so it's always one more than the available system voices.</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	tts_voice v;
	alert(&quot;result:&quot;, &quot;You have &quot;+v.get_voice_count()+&quot; voices&quot;);
}
</code></pre>
<h5>get_voice_name</h5>
<p>Get the name of a voice at a particular index.</p>
<p>string tts_voice::get_voice_name(int index);</p>
<h6>Parameters:</h6>
<ul>
<li>int index: the index of the voice to get the name of.</li>
</ul>
<h6>Returns:</h6>
<p>string: the name of the voice.</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	tts_voice v;
	if (v.voice_count &lt; 1) {
		alert(&quot;Oh no&quot;, &quot;Your system does not appear to have any TTS voices.&quot;);
		exit();
	}
	alert(&quot;The first voice on your system is&quot;, v.get_voice_name(0));
}
</code></pre>
<h5>get_volume</h5>
<p>Get the text to speech voice's volume (how loud it is).</p>
<p>int tts_voice::get_volume();</p>
<h6>Returns:</h6>
<p>int: the current volume in percentage.</p>
<h6>Remarks:</h6>
<p>0 is silent, 100 is loudest. If this hasn't been assigned, it will use the OS setting which may not be 100%. Beware if running old code, this is different from bgt having 0 be the max.</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	tts_voice v;
	v.set_volume(50);
	alert(&quot;the current volume is: &quot;, &quot;&quot;+v.get_volume());
}
</code></pre>
<h5>list_voices</h5>
<p>List all the available voices of the tts_voice object.</p>
<p>string[]@ tts_voice::list_voices();</p>
<h6>Returns:</h6>
<p>string[]@: a handle to an array containing all the voice names (as strings).</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	tts_voice v;
	string[]@ voices = v.list_voices();
	alert(&quot;Your available text-to-speech voices are&quot;, join(voices, &quot;, &quot;));
}
</code></pre>
<h5>refresh</h5>
<p>Refreshes the list of TTS voices installed on the system this object knows about.</p>
<p><code>bool tts_voice::refresh();</code></p>
<h6>Returns:</h6>
<p>bool: true if the list was successfully refreshed, false otherwise.</p>
<h5>set_rate</h5>
<p>Set the text to speech voice's playback rate (how fast it speaks).</p>
<p>void tts_voice::set_rate(int rate);</p>
<h6>Arguments:</h6>
<ul>
<li>int rate: the desired speech rate.</li>
</ul>
<h6>Remarks:</h6>
<p>-10 is slowest, 10 is fastest, with 0 being default speed, or 50 percent if you like. If this hasn't been manually assigned, it will use the OS setting which may not be 0. If moving in old bgt code, you may want to update it to use this method instead of the rate property.</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	tts_voice v;
	v.set_rate(0);
	v.speak(&quot;This is at fifty percent rate&quot;);
	v.set_rate(5);
	v.speak_wait(&quot;this is at seventy-five percent rate&quot;);
	//demonstrate setting it like it's a percentage, but note that it'll jump a bit because percentages have 100 values but there are only technically 21 choices, so implement this idea with an increment of 5 for best results.
	uint desired_rate=85;
	v.set_rate(desired_rate/5-10);
	int resulting_rate=v.get_rate();
	alert(&quot;after setting as 85 percent, the resulting rate now is:&quot;, resulting_rate);
}
</code></pre>
<h5>set_voice</h5>
<p>Set the voice of the TTS voice.</p>
<p><code>bool tts_voice::set_voice(int index);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int index: index of the voice to switch to.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the voice was successfully set, false otherwise.</p>
<h5>set_volume</h5>
<p>Set the text to speech voice's volume (how loud it is).</p>
<p>void tts_voice::set_volume(int volume);</p>
<h6>Arguments:</h6>
<ul>
<li>int volume: the desired volume level.</li>
</ul>
<h6>Remarks:</h6>
<p>0 is silent, 100 is loudest. If this hasn't been assigned, it will use the OS setting which may not be 100%. Beware if running old code, this is different from bgt having 0 be the max. It's better to use this instead of directly setting volume property.</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	tts_voice v;
	v.set_volume(50);
	v.speak(&quot;This is at 50 volume&quot;);
	v.set_volume(100);
	v.speak_wait(&quot;this is at 100 volume&quot;);
}
</code></pre>
<h5>speak</h5>
<p>Speak a string of text through the currently active TTS voice.</p>
<p>bool tts_voice::speak(const string &amp;in text, bool interrupt = false);</p>
<h6>Arguments:</h6>
<ul>
<li><p>const string&amp;in text: the text to be spoken.</p>
</li>
<li><p>bool interrupt = false: whether or not to interrupt the previously speaking speech to speak the new string.</p>
</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if speech was successful, false otherwise.</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	tts_voice v;
	v.speak(&quot;Hello, world!&quot;);
	while (v.speaking) {}
}
</code></pre>
<h5>speak_interrupt</h5>
<p>Speaks a string (forcefully interrupting) through the currently active text-to-speech voice.</p>
<p>bool tts_voice::speak_interrupt(const string&amp;in text);</p>
<h6>Arguments:</h6>
<ul>
<li>const string&amp;in text: the text to speak.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the speech was generated successfully, false otherwise.</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	int orig_ticks = ticks();
	tts_voice v;
	v.speak(&quot;This is an incredibly long string that will eventually get cut off by a much worse one.&quot;);
	while (v.speaking) {
		if ((ticks() - orig_ticks) &gt; 250)
			break;
	}
	v.speak_interrupt(&quot;You have been interrupted!&quot;);
	while (v.speaking) {}
}
</code></pre>
<h5>speak_to_file</h5>
<p>Outputs a string of text through the currently active TTS voice to a wave file.</p>
<p>bool tts_voice::speak_to_file(const string&amp;in filename, const string&amp;in text);</p>
<h6>Arguments:</h6>
<ul>
<li><p>const string&amp;in filename: the filename to write to.</p>
</li>
<li><p>const string&amp;in text: the text to synthesize.</p>
</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if synthesis was successful and the file was written, false otherwise.</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	// This is actually quite broken currently, it only ever writes  a 4 KB wav file. I think the problem is probably in speaking to memory in general, also see test/speak_to_file.nvgt.
	string filename = input_box(&quot;Filename&quot;, &quot;Enter the name of the file to save to (without the .wav extension).&quot;);
	if (filename.is_empty()) {
		alert(&quot;Error&quot;, &quot;You didn't type a filename.&quot;);
		exit();
	}
	string text = input_box(&quot;Text&quot;, &quot;Enter the text to synthesize.&quot;);
	if (text.is_empty()) {
		alert(&quot;Error&quot;, &quot;You didn't type any text.&quot;);
		exit();
	}
	tts_voice v;
	v.speak_to_file(filename + &quot;.wav&quot;, text);
	alert(&quot;Info&quot;, &quot;Done!&quot;);
}
</code></pre>
<h5>stop</h5>
<p>Stop the TTS voice, if currently speaking.</p>
<p>bool tts_voice::stop();</p>
<h6>Returns:</h6>
<p>bool: true if the voice was successfully stopped, false otherwise.</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	tts_voice v;
	v.speak(&quot;Hello there!&quot;);
	wait(500);
	v.stop();
}
</code></pre>
<h4>Properties</h4>
<h5>speaking</h5>
<p>Is the tts_voice currently speaking?</p>
<p>bool tts_voice::speaking;</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	tts_voice v;
	v.speak(&quot;Hello there! This is a very long string that will hopefully be spoken for at least a couple seconds&quot;);
	wait(500);
	alert(&quot;Example&quot;, v.speaking ? &quot;The TTS voice is currently speaking. Press OK to stop it&quot; : &quot;The TTS voice is not currently speaking&quot;);
}
</code></pre>
<h5>voice</h5>
<p>The number of the currently selected voice.</p>
<p>int tts_voice::voice;</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	tts_voice v;
	alert(&quot;Current voice index&quot;, v.voice);
	v.set_voice(0);
	alert(&quot;Current voice index&quot;, v.voice);
}
</code></pre>
<h5>voice_count</h5>
<p>Represents the total number of available tex-to-speech voices on your system.</p>
<p>int tts_voice::voice_count;</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	tts_voice v;
	alert(&quot;Your system has&quot;, v.voice_count + &quot; text-to-speech &quot; + (v.voice_count == 1 ? &quot;voice&quot; : &quot;voices&quot;));
}
</code></pre>
<h2>Functions</h2>
<h3>screen_reader_braille</h3>
<p>Brailles a string through the currently active screen reader, if supported.</p>
<p>bool screen_reader_braille(const string&amp;in text);</p>
<h4>Arguments:</h4>
<ul>
<li>const string&amp;in text: the text to braille.</li>
</ul>
<h4>Returns:</h4>
<p>bool: true if the function succeeded, false otherwise.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	screen_reader_braille(&quot;This message will only be brailled.&quot;);
}
</code></pre>
<h3>screen_reader_detect</h3>
<p>Returns the name of the currently active screen reader as a string.</p>
<p>string screen_reader_detect();</p>
<h4>Returns:</h4>
<p>string: the name of the given screen reader, or a blank string if none was found.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	string sr = screen_reader_detect();
	if (sr.is_empty())
		alert(&quot;Info&quot;, &quot;No screen reader found.&quot;);
	else
		alert(&quot;Info&quot;, &quot;The active screen reader is &quot; + sr);
}
</code></pre>
<h3>screen_reader_has_braille</h3>
<p>Determine if the active screen reader supports braille output.</p>
<p>bool screen_reader_has_braille();</p>
<h4>Returns:</h4>
<p>bool: true if the active screen reader supports braille, false otherwise.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	bool has_braille  = screen_reader_has_braille();
	if (has_braille)
		alert(&quot;Info&quot;, &quot;The currently active screen reader supports braille.&quot;);
	else
		alert(&quot;Info&quot;, &quot;The currently active screen reader does not support braille.&quot;);
}
</code></pre>
<h3>screen_reader_has_speech</h3>
<p>Determines if the active screen reader supports speech output.</p>
<p>bool screen_reader_has_speech();</p>
<h4>Returns:</h4>
<p>bool: true if the screen reader supports speech, false if not, or if no screen reader is active.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	bool has_speech = screen_reader_has_speech();
	if (has_speech)
		alert(&quot;Info&quot;, &quot;The active screen reader supports speech.&quot;);
	else
		alert(&quot;Info&quot;, &quot;The active screen reader does not support speech.&quot;);
}
</code></pre>
<h3>screen_reader_is_speaking</h3>
<p>Determine if the currently active screen reader (if any) is currently speaking.</p>
<p>bool screen_reader_is_speaking();</p>
<h4>Returns:</h4>
<p>bool: true if the currently active screen reader is speaking, false otherwise.</p>
<h4>Remarks:</h4>
<p>This function isn't foolproof, as some screen readers (e.g. NVDA) don't have a way to query this information.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	screen_reader_speak(&quot;Hello there, this is a very long string that will hopefully be spoken!&quot;, true);
	wait(50);
	bool speaking = screen_reader_is_speaking();
	if (speaking)
		alert(&quot;Info&quot;, &quot;The screen reader is speaking.&quot;);
	else
		alert(&quot;Info&quot;, &quot;The screen reader is not speaking.&quot;);
}
</code></pre>
<h3>screen_reader_output</h3>
<p>Speaks and brailles a string through the currently active screen reader, if supported.</p>
<p>bool screen_reader_output(const string&amp;in text, bool interrupt = true);</p>
<h4>Arguments:</h4>
<ul>
<li><p>const string&amp;in text: the text to output.</p>
</li>
<li><p>bool interrupt = true: Whether or not the previously spoken speech should be interrupted or not when speaking the new string.</p>
</li>
</ul>
<h4>Returns:</h4>
<p>bool: true if the function succeeded, false otherwise.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	screen_reader_output(&quot;This message will be both spoken and brailled!&quot;, true);
}
</code></pre>
<h3>screen_reader_speak</h3>
<p>Speaks a string through the currently active screen reader, if supported.</p>
<p>bool screen_reader_speak(const string&amp;in text, bool interrupt = true);</p>
<h4>Arguments:</h4>
<ul>
<li><p>const string&amp;in text: the text to speak.</p>
</li>
<li><p>bool interrupt = true: Whether or not the previously spoken speech should be interrupted or not when speaking the new string.</p>
</li>
</ul>
<h4>Returns:</h4>
<p>bool: true if the function succeeded, false otherwise.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	screen_reader_speak(&quot;This message will only be spoken.&quot;, true);
}
</code></pre>
<h2>Global Properties</h2>
<h3>SCREEN_READER_AVAILABLE</h3>
<p>reports if a screen reader is currently available.</p>
<p>const bool SCREEN_READER_AVAILABLE;</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	if (SCREEN_READER_AVAILABLE)
		alert(&quot;Info&quot;, &quot;A screen reader is available.&quot;);
	else
		alert(&quot;Info&quot;, &quot;A screen reader is not available.&quot;);
}
</code></pre>
