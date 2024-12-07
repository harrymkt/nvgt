---
title: Music System (music.nvgt)
url: docs/references_include_music_system_music.html
---

<h1>Music System (music.nvgt)</h1>
<h2>Music System</h2>
<p>This is an include that allows you to easily control music in your game. It can play anything from a stinger to a full music track, control looping, automatic playing, etc.</p>
<h2>classes</h2>
<h3>music_manager</h3>
<h4>methods</h4>
<h5>loop</h5>
<p>Updates the state of the music manager. This has to be called in your main loop, probably with the value of <code>ticks()</code> passed to it.</p>
<p><code>void music_manager::loop(uint64 t);</code></p>
<h6>Arguments:</h6>
<ul>
<li>uint64 t: the current tick count (you can most likely just make this parameter <code>ticks()</code>).</li>
</ul>
<h5>play</h5>
<p>Play a music track with particular parameters.</p>
<p><code>bool music_manager::play(string track);</code></p>
<h6>Parameters:</h6>
<ul>
<li>string track: the music track to play, including any options (see remarks for more information about option syntax).</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the track was able to start playing, false otherwise.</p>
<h6>Remarks:</h6>
<p>Music tracks are specified using a very simple string format (&quot;filename; flag; flag; option1=value; option2=value; flag; option3=value...&quot;).</p>
<p>Options are delimited by &quot;; &quot; excluding quotes. The only required setting is the track's main filename, which must be the first option provided. It does not matter in what order any other options or flags are set, the only rule is that the track's configuration string must start with it's main filename.</p>
<p>The difference between a flag and an option is that a flag is usually just a simple switch E. &quot;stinger; &quot;, while an option usually consists of a key/value pair e. &quot;startpos=2.9&quot;</p>
<p>When dealing with fades, values are usually in milliseconds, while when dealing with track durations they are usually specified in float seconds E.G. 4.555 for 4555 milliseconds.</p>
<p>####### List of possible options:</p>
<ul>
<li>stinger; disables looping</li>
<li>loop; causes the track to loop the main file</li>
<li>repeat_intro; If this, intro, and repeat are specified, causes the intro track to play again at the repeat point rather than the main track</li>
<li>instaplay; If a track is previously playing, causes this one to instantly begin playing instead of the default behavior of fading out and delaying the playback of this track (see switch_predelay and switch_f below), this sets those 2 variables to 0.</li>
<li>f=ms; causes the track to fade in at first play, ms=number of milliseconds the fade should take to complete</li>
<li>p=pitch; Sets the pitch of this track, defaults to 100. If this track streams from the internet, make sure not to set this too high as this could result in playing more of the sound than has been downloaded.</li>
<li>v=volume; sets the starting volume for this entire track (0=full -100=silent)</li>
<li>intro=filename; causes the audio file specified here to play before the main track file. By default the main track will begin playing immediately after the intro track ends unless intro_end is specified.</li>
<li>repeat=s; How many seconds before the end of the main track should the track repeat again? s=number of seconds (can include milliseconds like 4.681). When the track repeats, it will play overtop the remainder of the currently ending track. repeat=0 is the same as the loop flag, repeat=anything&lt;0 is the same as stinger. If multiple of repeat, loop, stinger are specified, only the one specified last will take effect.</li>
<li>repeat_f=ms; If repeat is specified and is greater than 0, this option causes the end of the currently playing track to fade out as the repeated track begins to play, and specifies how many ms that fade should take to complete.</li>
<li>predelay=s; how many seconds (can include milliseconds) before the track should begin after it starts playing?</li>
<li>switch_predelay=s; Same as above, but only applies if a track was previously playing and the music system switches to this one. Defaults to 300. This and predelay are added together, but this variable is handled by the music manager instead of by this music track unlike predelay.</li>
<li>switch_f=ms; If the music system is playing a track and then switches to this one, how many milliseconds should it take for the previously playing track to fade out? Defaults to 400.</li>
<li>intro_end=s; if intro is specified but the audio track specified by intro does not seamlessly transition into the main track, how many seconds (can include milliseconds) before the intro ends should the main track begin playing? The main track will not interrupt the remainder of the intro but will play overtop of it if this option is specified.</li>
<li>startpos=s; How many seconds (can include milliseconds) into either the intro track if specified else the main track should the audio begin playing E. seek?</li>
</ul>
<h5>set_load_callback</h5>
<p>This system was originally made for Survive the Wild which needs to read sound data from strings not packs most of the time, so this class implements something more complicated than a music.pack variable being set. Someone feel free to add this functionality though or I may do later. Instead, we set a callback which receives a sound object and a filename, and calls the appropriate load method on that sound for your situation. Not needed if your sounds are simply on disk. A short example of a load callback is below.</p>
<p><code>void music_manager::set_load_callback(load_music_sound@ cb);</code></p>
<h6>Arguments:</h6>
<ul>
<li>load_music_sound@ cb: your load callback. The syntax of it is <code>sound@ load_music_sound(sound@ sound_to_load, string filename_to_load);</code>. See remarks for an example.</li>
</ul>
<h6>Remarks:</h6>
<p>This is a basic example of how to write and set up a sound loading callback for use with the music manager.</p>
<pre><code>sound@ music_load(sound@ sound_to_load, string filename_to_load) {
	// Usually a sound object will be provided to this function from the music manager. Encase not,
	if (@sound_to_load is null) @sound_to_load = sound();
	if( !sound_to_load.load(filename_to_load, pack_file)) return null; // indicates error.
	return s; // Return a handle to the loaded sound.
}

// ...

your_music_manager.set_load_callback(music_load);
</code></pre>
<h5>stop</h5>
<p>Stops any currently playing music.</p>
<p><code>void music_manager::stop(int fade = 0);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int fade = 0: the fade duration of the currently playing music (in milliseconds).</li>
</ul>
<h4>properties</h4>
<h5>playing</h5>
<p>Determine if the music manager is currently playing a track or not.</p>
<p><code>bool music_manager::playing;</code></p>
<h5>volume</h5>
<p>Controls the volume of any currently playing music in this music manager.</p>
<p><code>float music_manager::volume;</code></p>
