---
title: Audio
url: docs/references_builtin_audio.html
---

<h1>Audio</h1>
<h2>Classes</h2>
<h3>sound</h3>
<h4>Methods</h4>
<h5>close</h5>
<p>Closes an opened sound, making the sound object available to be reloaded with a new one.</p>
<p>bool sound::close();</p>
<h6>Returns:</h6>
<p>bool: true if the sound could be closed, false otherwise for example if there is no sound opened.</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	sound s;
	s.load(&quot;C:/windows/media/ding.wav&quot;);
	alert(&quot;example&quot;, s.close()); // Will display true since a sound was previously opened.
	alert(&quot;example&quot;, s.close()); // Will now display false since the previous operation freed the sound object of any attached sound.
}
</code></pre>
<h5>load</h5>
<p>Loads a sound file with the specified settings.</p>
<ol>
<li><code>bool sound::load(string filename, pack@ soundpack = null, bool allow_preloads = true);</code></li>
<li><code>bool sound::load(sound_close_callback@ close_cb, sound_length_callback@ length_cb, sound_read_callback@ read_cb, sound_seek_callback@ seek_cb, string data, string preload_filename = &quot;&quot;);</code></li>
</ol>
<h6>Arguments (1):</h6>
<ul>
<li>string filename: the name/path to the file that is to be loaded.</li>
<li>pack@ soundpack = null: a handle to the pack object to load this sound from, if any.</li>
<li>bool allow_preloads = true: whether or not the sound system should preload sounds into memory on game load.</li>
</ul>
<h6>Arguments (2):</h6>
<ul>
<li>sound_close_callback@ close_cb: the close callback to use with the sound (see remarks).</li>
<li>sound_length_callback@ length_cb: the length callback to use with the sound (see remarks).</li>
<li>sound_read_callback@ read_cb: the read callback to use with the sound (see remarks).</li>
<li>sound_seek_callback@ seek_cb: the seek callback to use with the sound (see remarks).</li>
<li>string data: the audio data of the sound.</li>
<li>string preload_filename = &quot;&quot;: the name of the file to be preloaded (if any).</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the sound was successfully loaded, false otherwise.</p>
<h6>Remarks:</h6>
<p>The syntax for the sound_close_callback is:</p>
<blockquote>
<p>void sound_close_callback(string user_data);</p>
</blockquote>
<p>The syntax for the sound_length_callback is:</p>
<blockquote>
<p>uint sound_length_callback(string user_data);</p>
</blockquote>
<p>The syntax for the sound_read_callback is:</p>
<blockquote>
<p>int sound_read_callback(string &amp;out buffer, uint length, string user_data);</p>
</blockquote>
<p>The syntax for the sound_seek_callback is:</p>
<blockquote>
<p>bool sound_seek_callback(uint offset, string user_data);</p>
</blockquote>
<h5>load_url</h5>
<p>Load the specified URL.</p>
<p>bool sound::load_url(string url);</p>
<h6>Arguments:</h6>
<ul>
<li>string url: the URL to load (should be the direct link to a sound or stream).</li>
</ul>
<h6>Returns:</h6>
<p>Bool: True if the URL was successfully loaded; false otherwise.</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	sound s;
	bool success = s.load_url(&quot;https://example.com/my_sound.mp3&quot;);
	alert(&quot;Result&quot;, &quot;The sound was &quot; + (success == false? &quot;not &quot; : &quot;&quot;) + &quot;successfully loaded.&quot;);
}
</code></pre>
<h5>pause</h5>
<p>Pauses the sound.</p>
<p><code>bool sound::pause();</code></p>
<h6>Returns:</h6>
<p>bool: true if the sound was paused, false otherwise.</p>
<h5>play</h5>
<p>Starts playing the sound.</p>
<p><code>bool sound::play();</code></p>
<h6>Returns:</h6>
<p>bool: true if the sound was able to start playing, false otherwise.</p>
<h5>play_looped</h5>
<p>Starts playing the sound repeatedly.</p>
<p><code>bool sound::play_looped();</code></p>
<h6>Returns:</h6>
<p>bool: true if the sound was able to start playing, false otherwise.</p>
<h5>play_wait</h5>
<p>Starts playing the sound, blocking the calling thread until it's finished.</p>
<p><code>bool sound::play_wait();</code></p>
<h6>Returns:</h6>
<p>bool: true if the sound has successfully loaded and finished playing, false otherwise.</p>
<h5>seek</h5>
<p>Seeks to a particular point in the sound.</p>
<p><code>bool sound::seek(float ms);</code></p>
<h6>Arguments:</h6>
<ul>
<li>float ms: the time (in MS) to seek to.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the seeking was successful, false otherwise.</p>
<h5>set_position</h5>
<p>Sets the sound's position in 3d space.</p>
<p><code>bool sound::set_position(float listener_x, float listener_y, float listener_z, float sound_x, float sound_y, float sound_z, float rotation, float pan_step, float volume_step);</code></p>
<h6>Arguments:</h6>
<ul>
<li>float listener_x: the x position of the listener.</li>
<li>float listener_y: the y position of the listener.</li>
<li>float listener_z: the z position of the listener.</li>
<li>float sound_x: the x position of the sound.</li>
<li>float sound_y: the y position of the sound.</li>
<li>float sound_z: the z position of the sound.</li>
<li>float rotation: the rotation of the listener (in radians).</li>
<li>float pan_step: the pan step (e.g. how extreme the panning is).</li>
<li>float volume_step: the volume step (very similar to pan_step but for volume).</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the position was successfully set, false otherwise.</p>
<h5>stop</h5>
<p>Stops the sound, if currently playing.</p>
<p><code>bool sound::stop();</code></p>
<h6>Returns:</h6>
<p>bool: true if the sound was successfully stopped, false otherwise.</p>
<h4>Properties</h4>
<h5>active</h5>
<p>Determine if the sound has successfully been loaded or not.</p>
<p><code>bool sound::active;</code></p>
<h5>length</h5>
<p>Get the length of a sound (in milliseconds).</p>
<p><code>float sound::length;</code></p>
<h5>loaded_filename</h5>
<p>Obtain the path of sound file that has been loaded.</p>
<p><code>string sound::loaded_filename;</code></p>
<h5>paused</h5>
<p>Determine if the sound is paused.</p>
<p><code>bool sound::paused;</code></p>
<h5>playing</h5>
<p>Determine if the sound is currently playing.</p>
<p><code>bool sound::playing;</code></p>
<h5>sliding</h5>
<p>Determine if a sound is sliding or not.</p>
<p><code>sound::sliding;</code></p>
<h2>Functions</h2>
<h3>get_sound_input_devices</h3>
<p>Return an array of strings listing all input sound devices on the system.</p>
<p>string[]@ get_sound_input_devices();</p>
<h4>Returns:</h4>
<p>string[]@: A handle to an array listing all available input devices.</p>
<h4>Remarks:</h4>
<p>After listing devices with this function, you can set the sound_input_device global engine property to whatever index in the returned array contains the name of the device you want to set.</p>
<p>This list will always include a no sound device. If you don't want the user to be able to select it, feel free to not allow them to move their cursor to that item or not add it to your menus etc, but remember to pay attention to the index difference this may create when setting the sound_output_device property, namely just remember that setting sound_output_device = 0 will set the system to no sound, and setting the device to 1 will always be the first real device in the system, or the default device at least on windows.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	string[]@ devices = get_sound_input_devices();
	devices.remove_at(0); // Don't allow the user to select no sound.
	alert(&quot;devices&quot;, &quot;The following devices are installed on your system: &quot; + join(devices, &quot;, &quot;));
}
</code></pre>
<h3>get_sound_output_devices</h3>
<p>Return an array of strings listing all output sound devices on the system.</p>
<p>string[]@ get_sound_output_devices();</p>
<h4>Returns:</h4>
<p>string[]@: A handle to an array listing all available output devices.</p>
<h4>Remarks:</h4>
<p>After listing devices with this function, you can set the sound_output_device global engine property to whatever index in the returned array contains the name of the device you want to set.</p>
<p>This list will always include a no sound device. If you don't want the user to be able to select it, feel free to not allow them to move their cursor to that item or not add it to your menus etc, but remember to pay attention to the index difference this may create when setting the sound_output_device property, namely just remember that setting sound_output_device = 0 will set the system to no sound, and setting the device to 1 will always be the first real device in the system, or the default device at least on windows.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	string[]@ devices = get_sound_output_devices();
	devices.remove_at(0); // Don't allow the user to select no sound.
	alert(&quot;devices&quot;, &quot;The following devices are installed on your system: &quot; + join(devices, &quot;, &quot;));
}
</code></pre>
<h2>Global Properties</h2>
<h3>sound_default_mixer</h3>
<p>Represents the default mixer object for all your sounds to use.</p>
<p><code>mixer@ sound_default_mixer;</code></p>
<h3>sound_default_pack</h3>
<p>The default value passed to the second argument of sound::load, in other words, a handle to an open pack object that all future sounds will load from unless otherwise specified individually.</p>
<p><code>pack@ sound_default_pack = null;</code></p>
<h3>sound_global_hrtf</h3>
<p>Controls weather to use steam audio's functionality. If this property is set to false, the sound_environment class will be quite useless and sounds will use very basic panning.</p>
<p><code>bool sound_global_hrtf;</code></p>
<p>Changes take nearly instant effect from the time this property is modified.</p>
