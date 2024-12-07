---
title: User Interface
url: docs/references_builtin_user_interface.html
---

<h1>User Interface</h1>
<p>This section contains all functions that involve directly interacting with the user, be that by showing a window, checking the state of a key, or placing data onto the users clipboard. These handle generic input such as from the keyboard, and also generic output such as an alert box.</p>
<h2>Window management notes:</h2>
<ul>
<li>You can only have one NVGT window showing at a time.</li>
<li>without an nvgt window, there is no way to capture keyboard and mouse input from the user.</li>
<li>It is strongly advised to always put <code>wait(5);</code> in your main loops. This prevents your game from hogging the CPU, and also prevents weird bugs with the game window sometimes freezing etc.</li>
</ul>
<h2>Enums</h2>
<h3>key_code</h3>
<p>This is a complete list of possible keycodes in NVGT, as well as a short description of what they are. These are registered in the key_code enum, meaning you can use this type to pass any value listed here around though it is also safe to use unsigned integers.</p>
<h4>Letter keys</h4>
<ul>
<li>KEY_UNKNOWN: unknown.</li>
<li>KEY_A: the A key.</li>
<li>KEY_B: the B key.</li>
<li>KEY_C: the C key.</li>
<li>KEY_D: the D key.</li>
<li>KEY_E: the E key.</li>
<li>KEY_F: the F key.</li>
<li>KEY_G: the G key.</li>
<li>KEY_H: the H key.</li>
<li>KEY_I: the I key.</li>
<li>KEY_J: the J key.</li>
<li>KEY_K: the K key.</li>
<li>KEY_L: the L key.</li>
<li>KEY_M: the M key.</li>
<li>KEY_N: the N key.</li>
<li>KEY_O: the O key.</li>
<li>KEY_P: the P key.</li>
<li>KEY_Q: the Q key.</li>
<li>KEY_R: the R key.</li>
<li>KEY_S: the S key.</li>
<li>KEY_T: the T key.</li>
<li>KEY_U: the U key.</li>
<li>KEY_V: the V key.</li>
<li>KEY_W: the W key.</li>
<li>KEY_X: the X key.</li>
<li>KEY_Y: the Y key.</li>
<li>KEY_Z: the Z key.</li>
</ul>
<h4>Number keys</h4>
<ul>
<li>KEY_1: the 1 key.</li>
<li>KEY_2: the 2 key.</li>
<li>KEY_3: the 3 key.</li>
<li>KEY_4: the 4 key.</li>
<li>KEY_5: the 5 key.</li>
<li>KEY_6: the 6 key.</li>
<li>KEY_7: the 7 key.</li>
<li>KEY_8: the 8 key.</li>
<li>KEY_9: the 9 key.</li>
<li>KEY_0: the 0 key.</li>
</ul>
<h4>Special keys</h4>
<ul>
<li>KEY_RETURN: the Return (or enter) key.</li>
<li>KEY_ESCAPE: the Escape key.</li>
<li>KEY_BACK: the Backspace key.</li>
<li>KEY_TAB: the Tab key.</li>
<li>KEY_SPACE: the Space key.</li>
<li>KEY_MINUS: the Minus (dash) key.</li>
<li>KEY_EQUALS: the Equals key.</li>
<li>KEY_LEFTBRACKET: the Left Bracket key.</li>
<li>KEY_RIGHTBRACKET: the Right Bracket key.</li>
<li>KEY_BACKSLASH: the Backslash key.</li>
<li>KEY_NONUSHASH: the Non-US Hash key.</li>
<li>KEY_SEMICOLON: the Semicolon key.</li>
<li>KEY_APOSTROPHE: the Apostrophe key.</li>
<li>KEY_GRAVE: the Grave key.</li>
<li>KEY_COMMA: the Comma key.</li>
<li>KEY_PERIOD: the Period key.</li>
<li>KEY_SLASH: the Slash key.</li>
<li>KEY_CAPSLOCK: the Caps Lock key.</li>
</ul>
<h4>Function keys</h4>
<ul>
<li>KEY_F1: the F1 key.</li>
<li>KEY_F2: the F2 key.</li>
<li>KEY_F3: the F3 key.</li>
<li>KEY_F4: the F4 key.</li>
<li>KEY_F5: the F5 key.</li>
<li>KEY_F6: the F6 key.</li>
<li>KEY_F7: the F7 key.</li>
<li>KEY_F8: the F8 key.</li>
<li>KEY_F9: the F9 key.</li>
<li>KEY_F10: the F10 key.</li>
<li>KEY_F11: the F11 key.</li>
<li>KEY_F12: the F12 key.</li>
<li>KEY_F13: the F13 key.</li>
<li>KEY_F14: the F14 key.</li>
<li>KEY_F15: the F15 key.</li>
<li>KEY_F16: the F16 key.</li>
<li>KEY_F17: the F17 key.</li>
<li>KEY_F18: the F18 key.</li>
<li>KEY_F19: the F19 key.</li>
<li>KEY_F20: the F20 key.</li>
<li>KEY_F21: the F21 key.</li>
<li>KEY_F22: the F22 key.</li>
<li>KEY_F23: the F23 key.</li>
<li>KEY_F24: the F24 key.</li>
</ul>
<h4>Arrow keys</h4>
<ul>
<li>KEY_RIGHT: the Right Arrow key.</li>
<li>KEY_LEFT: the Left Arrow key.</li>
<li>KEY_DOWN: the Down Arrow key.</li>
<li>KEY_UP: the Up Arrow key.</li>
</ul>
<h4>Numpad keys</h4>
<ul>
<li>KEY_NUMLOCKCLEAR: the Num Lock key.</li>
<li>KEY_NUMPAD_DIVIDE: the numpad divide key.</li>
<li>KEY_NUMPAD_MULTIPLY: the numpad multiply key.</li>
<li>KEY_NUMPAD_MINUS: the numpad minus key.</li>
<li>KEY_NUMPAD_PLUS: the numpad plus key.</li>
<li>KEY_NUMPAD_ENTER: the numpad enter key.</li>
<li>KEY_NUMPAD_1: the Numpad 1 key.</li>
<li>KEY_NUMPAD_2: the Numpad 2 key.</li>
<li>KEY_NUMPAD_3: the Numpad 3 key.</li>
<li>KEY_NUMPAD_4: the Numpad 4 key.</li>
<li>KEY_NUMPAD_5: the Numpad 5 key.</li>
<li>KEY_NUMPAD_6: the Numpad 6 key.</li>
<li>KEY_NUMPAD_7: the Numpad 7 key.</li>
<li>KEY_NUMPAD_8: the Numpad 8 key.</li>
<li>KEY_NUMPAD_9: the Numpad 9 key.</li>
<li>KEY_NUMPAD_0: the Numpad 0 key.</li>
<li>KEY_NUMPAD_PERIOD: the Numpad Period key.</li>
</ul>
<h4>Modifier keys</h4>
<ul>
<li>KEY_LCTRL: the Left Control key.</li>
<li>KEY_LSHIFT: the Left Shift key.</li>
<li>KEY_LALT: the Left Alt key.</li>
<li>KEY_LGUI: the left windows/command/super key (depending on platform).</li>
<li>KEY_RCTRL: the Right Control key.</li>
<li>KEY_RSHIFT: the Right Shift key.</li>
<li>KEY_RALT: the Right Alt key.</li>
<li>KEY_RGUI: the right windows/command/super key (depending on platform).</li>
</ul>
<h4>Miscellaneous keys</h4>
<ul>
<li>KEY_MODE: the Mode key.</li>
<li>KEY_APPLICATION: the Application key.</li>
<li>KEY_POWER: the Power key.</li>
<li>KEY_PRINTSCREEN: the Print Screen key.</li>
<li>KEY_SCROLLLOCK: the Scroll Lock key.</li>
<li>KEY_PAUSE: the Pause key.</li>
<li>KEY_INSERT: the Insert key.</li>
<li>KEY_HOME: the Home key.</li>
<li>KEY_PAGEUP: the Page Up key.</li>
<li>KEY_DELETE: the Delete key.</li>
<li>KEY_END: the End key.</li>
<li>KEY_PAGEDOWN: the Page Down key.</li>
</ul>
<h4>Media keys</h4>
<ul>
<li>KEY_MUTE: the Mute key.</li>
<li>KEY_VOLUMEUP: the Volume Up key.</li>
<li>KEY_VOLUMEDOWN: the Volume Down key.</li>
<li>KEY_MEDIA_NEXT_TRACK: the next track key.</li>
<li>KEY_MEDIA_PREVIOUS_TRACK: the previous track key.</li>
<li>KEY_MEDIA_STOP: the stop media key.</li>
<li>KEY_MEDIA_PLAY: the play media key.</li>
<li>KEY_MUTE: the mute key.</li>
<li>KEY_MEDIA_SELECT: the media select key.</li>
</ul>
<h4>Browser and Application keys</h4>
<ul>
<li>KEY_AC_SEARCH: the AC Search key.</li>
<li>KEY_AC_HOME: the AC Home key.</li>
<li>KEY_AC_BACK: the AC Back key.</li>
<li>KEY_AC_FORWARD: the AC Forward key.</li>
<li>KEY_AC_STOP: the AC Stop key.</li>
<li>KEY_AC_REFRESH: the AC Refresh key.</li>
<li>KEY_AC_BOOKMARKS: the AC Bookmarks key.</li>
</ul>
<h4>Additional keys</h4>
<ul>
<li>KEY_MEDIA_EJECT: the eject key.</li>
<li>KEY_SLEEP: the sleep key.</li>
<li>KEY_MEDIA_REWIND: the media rewind key.</li>
<li>KEY_MEDIA_FAST_FORWARD: the media fast forward key.</li>
<li>KEY_SOFTLEFT: the Soft Left key.</li>
<li>KEY_SOFTRIGHT: the Soft Right key.</li>
<li>KEY_CALL: the Call key.</li>
<li>KEY_ENDCALL: the End Call key.</li>
<li>KEY_AC_SEARCH: the AC Search key.</li>
<li>KEY_AC_HOME: the AC Home key.</li>
<li>KEY_AC_BACK: the AC Back key.</li>
<li>KEY_AC_FORWARD: the AC Forward key.</li>
<li>KEY_AC_STOP: the AC Stop key.</li>
<li>KEY_AC_REFRESH: the AC Refresh key.</li>
<li>KEY_AC_BOOKMARKS: the AC Bookmarks key.</li>
</ul>
<h3>key_modifier</h3>
<p>This is a complete list of supported key modifiers and their descriptions. These are registered in the key_modifier enum, so you can use that type to pass any value listed here around.</p>
<ul>
<li><p>KEYMOD_NONE: no modifier.</p>
</li>
<li><p>KEYMOD_LSHIFT: left shift key.</p>
</li>
<li><p>KEYMOD_RSHIFT: right shift key.</p>
</li>
<li><p>KEYMOD_LCTRL: left control key.</p>
</li>
<li><p>KEYMOD_RCTRL: right control key.</p>
</li>
<li><p>KEYMOD_LALT: left alt key.</p>
</li>
<li><p>KEYMOD_RALT: right alt key.</p>
</li>
<li><p>KEYMOD_LGUI: left windows/command/super key (depending on platform).</p>
</li>
<li><p>KEYMOD_RGUI: right windows/command/super key (depends on platform).</p>
</li>
<li><p>KEYMOD_NUM: numlock key.</p>
</li>
<li><p>KEYMOD_CAPS: capslock key.</p>
</li>
<li><p>KEYMOD_MODE: input switch mode (only on certain keyboards).</p>
</li>
<li><p>KEYMOD_SCROLL: scroll lock key.</p>
</li>
<li><p>KEYMOD_CTRL: either control key.</p>
</li>
<li><p>KEYMOD_SHIFT: either shift key.</p>
</li>
<li><p>KEYMOD_ALT: either alt key.</p>
</li>
<li><p>KEYMOD_GUI: either windows/command/super key.</p>
</li>
</ul>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	show_window(&quot;Example&quot;);
	wait(50); // Give the screen readers enough time to speak the window title before speaking.
	screen_reader_output(&quot;Press alt+f4 to close this window.&quot;, true);
	while (true) {
		wait(5);
		if (keyboard_modifiers &amp; KEYMOD_ALT &gt; 0 &amp;&amp; key_pressed(KEY_F4))
			exit();
	}
}
</code></pre>
<h3>message_box_flags</h3>
<p>This is an enumeration of possible flags to be passed to the message_box(), alert(), question(), and similar functions.</p>
<ul>
<li>MESSAGE_BOX_ERROR: the message box should act like an error dialog.</li>
<li>MESSAGE_BOX_WARNING: the message box should act like a warning dialog.</li>
<li>MESSAGE_BOX_INFORMATION: the message box should act like an informative dialog.</li>
<li>MESSAGE_BOX_BUTTONS_LEFT_TO_RIGHT: arrange the buttons in the dialog from left to right.</li>
<li>MESSAGE_BOX_BUTTONS_RIGHT_TO_LEFT: arrange the buttons from right-to-left in the message box.</li>
</ul>
<h3>touch_device_type</h3>
<p>These are the possible types of touch input devices.</p>
<ul>
<li>TOUCH_DEVICE_INVALID = -1: Returned if an invalid ID is passed to get_touch_device_type.</li>
<li>TOUCH_DEVICE_DIRECT: A touch screen with window-relative coordinates.</li>
<li>TOUCH_DEVICE_INDIRECT_ABSOLUTE: A trackpad with absolute device coordinates.</li>
<li>TOUCH_DEVICE_INDIRECT_RELATIVE: A trackpad with screen cursor-relative coordinates.</li>
</ul>
<h2>Functions</h2>
<h3>alert</h3>
<p>Display a message box with an OK button to the user.</p>
<p>int alert(const string&amp;in title, const string&amp;in text, bool can_cancel = false, uint flags = 0);</p>
<h4>Arguments:</h4>
<ul>
<li><p>const string&amp;in title: the title of the dialog.</p>
</li>
<li><p>const string&amp;in text: the text of the dialog.</p>
</li>
<li><p>bool can_cancel = false: determines if a cancel button is present.</p>
</li>
<li><p>uint flags = 0: a combination of flags (see message_box_flags for more information).</p>
</li>
</ul>
<h4>Returns:</h4>
<p>int: the number of the button that was pressed, either OK or cancel.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	alert(&quot;Hello&quot;, &quot;I am a standard alert&quot;);
	alert(&quot;Hi&quot;, &quot;And I'm a cancelable one&quot;, true);
}
</code></pre>
<h3>android_request_permission</h3>
<p>Request a permission from the Android operating system either synchronously or asynchronously.</p>
<p><code>bool android_request_permission(string permission, android_permission_request_callback@ callback = null, string callback_data = &quot;&quot;);</code></p>
<h4>Arguments:</h4>
<ul>
<li>string permission: A permission identifier such as android.permission.RECORD_AUDIO.</li>
<li>android_permission_request_callback@ callback = null: An optional function that should be called when the user responds to the permission request (see remarks).</li>
<li>string callback_data = &quot;&quot;: An arbitrary string that is passed to the given callback function.</li>
</ul>
<h4>Returns:</h4>
<p>bool: true if the request succeeded (see remarks), false otherwise or if this function was not called on Android.</p>
<h4>Remarks:</h4>
<p>The callback signature this function expects is registered as :
<code>funcdef void android_permission_request_callback(string permission, bool granted, string user_data);</code></p>
<p>This function behaves very differently depending on whether you've provided a callback or not. If you do not, this function blocks the thread that called it until the user responds to the permission request, in which case it returns true or false depending on whether the user has actually granted the permission. On the other hand if you do provide a callback, the instant return value of this function only indicates whether the request has been made rather than whether the permission has been granted, as that information will be provided later in the given callback.</p>
<p>Beware that the callback you provide might get invoked on any thread, thus the provision of a more simple, blocking alternative. If you do provide a callback, you are responsible for handling any data races that may result.</p>
<h3>android_show_toast</h3>
<p>Shows an Android toast notification, small popups that are unique to that operating system.</p>
<p><code>bool android_show_toast(const string&amp;in message, int duration, int gravity = -1, int x_offset = 0, int y_offset = 0);</code></p>
<h4>Arguments:</h4>
<ul>
<li>const string&amp;in message: The message to display.</li>
<li>int duration: 0 for short or 1 for long, all other values are undefined.</li>
<li>int gravity = -1: One of <a href="https://developer.android.com/reference/android/view/Gravity">the values on this page</a> or -1 for no preference.</li>
<li>int x_offset = 0, int y_offset = 0: Only used if gravity is set, see Android developer documentation.</li>
</ul>
<h4>Returns:</h4>
<p>bool: true if the toast was shown, false otherwise or if called on a platform other than Android.</p>
<h4>Remarks:</h4>
<p><a href="https://developer.android.com/guide/topics/ui/notifiers/toasts">Learn more about android toasts notifications here.</a></p>
<h3>clipboard_get_text</h3>
<p>Returns the text currently on the user's clipboard.</p>
<p>string clipboard_get_text();</p>
<h4>Returns:</h4>
<p>string: The text on the user's clipboard, as UTF_8.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	string text = clipboard_get_text();
	if (text == &quot;&quot;)
		alert(&quot;Info&quot;, &quot;Your clipboard is empty&quot;);
	else
		if (text.length() &gt; 1024)
			alert(&quot;Info&quot;, &quot;Your clipboard contains a long string. It is &quot; + text.length() + &quot; characters&quot;);
		else
			alert(&quot;Info&quot;, &quot;Your clipboard contains &quot; + text);
}
</code></pre>
<h3>clipboard_set_raw_text</h3>
<p>Sets the text on the user's clipboard, using the system encoding.</p>
<p>bool clipboard_set_raw_text(const string&amp;in text);</p>
<h4>Arguments:</h4>
<ul>
<li>const string&amp;in text: the text to copy, assumed to be in the system's encoding.</li>
</ul>
<h4>Returns:</h4>
<p>Bool: true on success, false on failure.</p>
<h4>Remarks:</h4>
<p>To copy UTF-8 text, see clipboard_set_text().</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	string text = input_box(&quot;Text&quot;, &quot;Enter the text to copy.&quot;);
	clipboard_set_raw_text(text);
	if (text == &quot;&quot;)
		alert(&quot;Info&quot;, &quot;Your clipboard has been cleared.&quot;);
	else
		alert(&quot;Info&quot;, &quot;Text copied&quot;);
}
</code></pre>
<h3>clipboard_set_text</h3>
<p>Sets the text on the user's clipboard.</p>
<p>bool clipboard_set_text(const string&amp;in text);</p>
<h4>Arguments:</h4>
<ul>
<li>const string&amp;in text: the text to copy, assumed to be UTF_8.</li>
</ul>
<h4>Returns:</h4>
<p>Bool: true on success, false on failure.</p>
<h4>Remarks:</h4>
<p>To copy text in the system encoding, see clipboard_set_raw_text().</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	string text = input_box(&quot;Text&quot;, &quot;Enter the text to copy.&quot;);
	clipboard_set_text(text);
	if (text == &quot;&quot;)
		alert(&quot;Info&quot;, &quot;Your clipboard has been cleared.&quot;);
	else
		alert(&quot;Info&quot;, &quot;Text copied&quot;);
}
</code></pre>
<h3>destroy_window</h3>
<p>Destroys the currently shown window, if it exists.</p>
<p>bool destroy_window();</p>
<h4>Returns:</h4>
<p>bool: true if the window was successfully destroyed, false otherwise.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	alert(&quot;Info&quot;, &quot;Pressing SPACE will destroy the window&quot;);
	show_window(&quot;Example&quot;);
	while (true) {
		wait(5); // Don't hog all the CPU time.
		if (key_pressed(KEY_SPACE)) {
			destroy_window();
			wait(2000); // Simulate doing things while the window isn't active.
			exit();
		}
	}
}
</code></pre>
<h3>exit</h3>
<p>Completely shut down your application, returning a particular exit code to your operating system in the process.</p>
<p>void exit(int exit_code = 0);</p>
<h4>Arguments:</h4>
<ul>
<li>int exit_code = 0: the exit code to return to your operating system.</li>
</ul>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	show_window(&quot;Example&quot;);
	screen_reader_output(&quot;Press escape to exit.&quot;, true);
	while (true) {
		wait(5);
		if (key_pressed(KEY_ESCAPE)) {
			screen_reader_output(&quot;Goodbye.&quot;, true);
			wait(500);
			exit();
		}
	}
}
</code></pre>
<h3>focus_window</h3>
<p>Attempt to bring your NVGT window to the foreground.</p>
<p>bool focus_window();</p>
<h4>Returns:</h4>
<p>bool: true if the window was successfully focused, false otherwise.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	timer focuser;
	show_window(&quot;Focus every 5 seconds example&quot;);
	while (true) {
		wait(5);
		if (key_pressed(KEY_ESCAPE)) exit();
		if (focuser.has_elapsed(5000)) {
			focuser.restart();
			focus_window();
		}
	}
}
</code></pre>
<h3>get_characters</h3>
<p>Determine any printable characters typed into the games window since this function's lass call.</p>
<p>string get_characters();</p>
<h4>Returns:</h4>
<p>string: Any characters typed since this function was last called, or an empty string if none are available.</p>
<h4>Remarks:</h4>
<p>This is the function one would use if they wished to integrate a virtual text field of any sort into their games or applications.</p>
<p>Unlike functions such as key_down or keys_pressed, this function focuses specifically on textual content which has been input to the application. A character returned from this function, for example, could be anything from the space bar to an emoticon inserted using the windows emoji picker.</p>
<p>A typical use case would involve calling this function once per iteration of your game loop and storing any new characters that are typed into a buffer that composes a chat message or a username or anything else requiring virtual text input.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	string buffer;
	show_window(&quot;get_characters example&quot;);
	while (!key_pressed(KEY_ESCAPE)) {
		wait(5);
		string char = get_characters();
		if (!char.empty()) {
			buffer += char;
			screen_reader_speak(char, true); // You need to process this further for screen readers, such as replacing . with period and other punctuation.
		}
		if (key_pressed(KEY_RETURN)) {
			screen_reader_speak(&quot;You typed &quot; + (!buffer.empty()? buffer : &quot;nothing&quot;), true);
			buffer = &quot;&quot;;
		}
	}
}
</code></pre>
<h3>get_touch_device_name</h3>
<p>Determine the name of a touch device given it's ID.</p>
<p><code>string get_touch_device_name(uint64 device_id);</code></p>
<h4>Returns:</h4>
<p>string : The name of the given device, or an empty string on failure.</p>
<h3>get_touch_device_type</h3>
<p>Determine the type of a touch device given it's ID.</p>
<p><code>touch_device_type get_touch_device_name(uint64 device_id);</code></p>
<h4>Returns:</h4>
<p>touch_device_type: The type of the given device, or TOUCH_DEVICE_TYPE_INVALID if a bad ID is given.</p>
<h3>get_touch_devices</h3>
<p>Enumerate all available touch input devices on the system.</p>
<p>uint64[]@ get_touch_devices();</p>
<h4>Returns:</h4>
<p>uint64[]@: An array of touch device IDs, may be empty of no touch devices are available.</p>
<h4>Remarks:</h4>
<p>You can pass any of the IDs returned from this function to the get_touch_device_type, get_touch_device_name, or query_touch_device functions.</p>
<p>Note that on some platforms, certain touch devices might not become available until they first receive input. For example this is true with the Android touch screen.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	uint64[]@ devices = get_touch_devices();
	if (devices.length() &lt; 1) {
		alert(&quot;no devices&quot;, &quot;There are no detectable touch devices on your system.&quot;);
		exit();
	}
	for (uint i = 0; i &lt; devices.length(); i++)
		alert(&quot;device &quot; + devices[i], get_touch_device_name(devices[i]));
}
</code></pre>
<h3>get_window_os_handle</h3>
<p>Returns the native handle used by the operating system to manage NVGT's window.</p>
<p>uint64 get_window_os_handle();</p>
<h4>Returns:</h4>
<p>uint64: An HWND / NSWindow* / similar handle that the operating system uses to manage the window.</p>
<h4>Remarks:</h4>
<p>This function is only useful for someone trying to do something advanced, usually involving passing the identifier for the game window to a system API function or something similar. If you don't understand what this function does, you should probably avoid it for the present.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	// Lets set the window title using the windows API, typically you'd use show_window a second time for this.
	show_window(&quot;hello&quot;);
	uint64 handle = get_window_os_handle();
	library lib;
	lib.load(&quot;user32&quot;);
	lib.call(&quot;int SetWindowTextA(uint64, ptr)&quot;, handle, &quot;example window&quot;);
	wait(500); // Let the user observe the change before exiting.
}
</code></pre>
<h3>get_window_text</h3>
<p>Returns the title of your window.</p>
<p>string get_window_text();</p>
<h4>Returns:</h4>
<p>string: the title of your window.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	string[] possible_titles = {&quot;Hello world&quot;, &quot;NVGT test&quot;, &quot;My game&quot;, &quot;Example&quot;, &quot;Window title example&quot;};
	show_window(possible_titles[random(0, possible_titles.length() - 1)]);
	while (true) {
		wait(5);
		if (key_pressed(KEY_ESCAPE)) exit();
		if (key_pressed(KEY_SPACE)) {
			screen_reader_output(&quot;The window title currently is: &quot; + get_window_text(), true);
			show_window(possible_titles[random(0, possible_titles.length() - 1)]); // Randomize the title again.
		}
	}
}
</code></pre>
<h3>idle_ticks</h3>
<p>Obtain the time passed in milliseconds since a user has pressed a key or used the mouse.</p>
<p>uint64 idle_ticks();</p>
<h4>returns</h4>
<p>uint64: the number of milliseconds since a user has last interacted with the machine.</p>
<h4>remarks</h4>
<p>This function can serve as a useful utility to verify whether a user has been away from the keyboard.</p>
<p>It is currently integrated for windows and MacOS. On linux, it will always return 0 until further notice.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	int64 t;
	show_window(&quot;Idle test&quot;);
	wait(50);
	screen_reader_speak(&quot;Press space to check the idle time and escape to exit.&quot;, true);
	while (!key_pressed(KEY_ESCAPE)) {
		wait(5);
		if (key_pressed(KEY_SPACE))
			screen_reader_speak(&quot;You have been idle for %0 milliseconds&quot;.format(t), true);
		t = idle_ticks();
	}
}
</code></pre>
<h3>info_box</h3>
<p>Displays a dialog to the user consisting of a read-only text field and a close button.</p>
<p>bool info_box(const string&amp;in title, const string&amp;in label, const string&amp;in text, uint64 flags = 0);</p>
<h4>Arguments:</h4>
<ul>
<li><p>const string&amp;in title: the title of the dialog.</p>
</li>
<li><p>const string&amp;in label: the text to display above the text field.</p>
</li>
<li><p>const string&amp;in text: the text to display in the text field.</p>
</li>
<li><p>uint64 flags = 0: a combination of flags, see message_box_flags for more information.</p>
</li>
</ul>
<h4>Returns:</h4>
<p>bool: true if the user pressed the close button, false otherwise.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	info_box(&quot;Test&quot;, &quot;Information&quot;, &quot;this is a\r\nlong string\r\nthat can be split\r\nacross lines&quot;);
}
</code></pre>
<h3>input_box</h3>
<p>Displays a dialog to the user consisting of an input field, an OK button and a cancel button.</p>
<p>string input_box(const string&amp;in title, const string&amp;in text, const string&amp;in default_text = &quot;&quot;, uint64 flags = 0);</p>
<h4>Arguments:</h4>
<ul>
<li><p>const string&amp;in title: the title of the input box.</p>
</li>
<li><p>const string&amp;in text: the text to display above the text field.</p>
</li>
<li><p>const string&amp;in default_text = &quot;&quot;: the contents to populate the text box with by default.</p>
</li>
<li><p>uint64 flags = 0: a combination of flags, see message_box_flags for more information.</p>
</li>
</ul>
<h4>Returns:</h4>
<p>string: the text that the user typed.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	string name = input_box(&quot;Name&quot;, &quot;What is your name?&quot;, &quot;John Doe&quot;);
	if (name.is_empty()) {
		alert(&quot;Error&quot;, &quot;You didn't type a name, unidentified person!&quot;);
		exit();
	}
	alert(&quot;Hi&quot;, name + &quot;!&quot;);
}
</code></pre>
<h3>install_keyhook</h3>
<p>Attempts to install NVGT's JAWS keyhook.</p>
<p>bool install_keyhook(bool allow_reinstall = true);</p>
<h4>Arguments:</h4>
<ul>
<li>bool allow_reinstall = true: whether or not this function will reinstall the hook on subsequent calls.</li>
</ul>
<h4>Returns:</h4>
<p>bool: true if the keyhook was successfully installed, false otherwise.</p>
<h4>Remarks:</h4>
<p>This keyhook allows NVGT games to properly capture keyboard input while the JAWS for Windows screen reader is running.</p>
<p>Note that installing it when JAWS is not running may yield unintended consequences, such as functionality of other screen readers being slightly limited while in your game window.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	bool success = install_keyhook();
	if (success) {
		alert(&quot;Info&quot;, &quot;The keyhook was successfully installed!&quot;);
		uninstall_keyhook();
	}
	else
		alert(&quot;Info&quot;, &quot;The keyhook was not successfully installed.&quot;);
}
</code></pre>
<h3>is_console_available</h3>
<p>Determine if your application has access to a console window or not.</p>
<p>bool is_console_available();</p>
<h4>Returns:</h4>
<p>bool: true if your application has access to a console window, false otherwise.</p>
<h4>Remarks:</h4>
<p>If this function returns false, it is very likely that any output passed to the print or println functions or the cout/cerr datastreams will be silently dropped.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	if (is_console_available()) println(&quot;hello from the console!&quot;);
	else alert(&quot;console unavailable&quot;, &quot;hello from the user interface!&quot;);
}
</code></pre>
<h3>is_window_active</h3>
<p>Determines if your game's window is active (i.e. has the keyboard focus).</p>
<p>bool is_window_active();</p>
<h4>Returns:</h4>
<p>bool: true if your game window has the keyboard focus, false if not.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	show_window(&quot;Test&quot;);
	wait(1000); // Give the user time to alt+tab away if they so choose.
	bool active = is_window_active();
	if (active)
		alert(&quot;Info&quot;, &quot;Your game window is active.&quot;);
	else
		alert(&quot;Info&quot;, &quot;Your game window is not active.&quot;);
}
</code></pre>
<h3>is_window_hidden</h3>
<p>Determines if your game's window is hidden or not.</p>
<p>bool is_window_hidden();</p>
<h4>Returns:</h4>
<p>bool: true if your game window is hidden, false if it's shown.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	show_window(&quot;Test&quot;);
	bool hide = random_bool();
	if (hide) hide_window();
	alert(&quot;The window is&quot;, is_window_hidden() ? &quot;hidden&quot; : &quot;shown&quot;);
}
</code></pre>
<h3>key_down</h3>
<p>Determine if a particular key is held down.</p>
<p>bool key_down(uint key);</p>
<h4>Arguments:</h4>
<ul>
<li>uint key: the key to check.</li>
</ul>
<h4>Returns:</h4>
<p>bool: true if the key is down at all, false otherwise.</p>
<h4>Remarks:</h4>
<p>For a complete list of keys that can be passed to this function, see input constants.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	show_window(&quot;Example&quot;);
	while (true) {
		wait(5);
		if (key_down(KEY_SPACE))
			screen_reader_output(&quot;space&quot;, true);
		if (key_pressed(KEY_ESCAPE))
			exit();
	}
}
</code></pre>
<h3>key_pressed</h3>
<p>Determine if a particular key is pressed.</p>
<p>bool key_pressed(uint key);</p>
<h4>Arguments:</h4>
<ul>
<li>uint key: the key to check.</li>
</ul>
<h4>Returns:</h4>
<p>bool: true if the key was just pressed, false otherwise.</p>
<h4>Remarks:</h4>
<p>For a complete list of keys that can be passed to this function, see input constants.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	show_window(&quot;Example&quot;);
	while (true) {
		wait(5);
		if (key_pressed(KEY_SPACE))
			screen_reader_output(&quot;You just pressed space!&quot;, true);
		if (key_pressed(KEY_ESCAPE))
			exit();
	}
}
</code></pre>
<h3>key_released</h3>
<p>Determine if a particular key was just released.</p>
<p>bool key_released(uint key);</p>
<h4>Arguments:</h4>
<ul>
<li>uint key: the key to check.</li>
</ul>
<h4>Returns:</h4>
<p>bool: true if the key was just released, false otherwise.</p>
<h4>Remarks:</h4>
<p>For a complete list of keys that can be passed to this function, see input constants.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	show_window(&quot;Example&quot;);
	while (true) {
		wait(5);
		if (key_released(KEY_SPACE))
			screen_reader_output(&quot;you just released the space key&quot;, true);
		if (key_pressed(KEY_ESCAPE))
			exit();
	}
}
</code></pre>
<h3>key_repeating</h3>
<p>Determine if a particular key is repeating (i.e. it's being held, but wasn't just pressed).</p>
<p>bool key_repeating(uint key);</p>
<h4>Arguments:</h4>
<ul>
<li>uint key: the key to check.</li>
</ul>
<h4>Returns:</h4>
<p>bool: true if the key is repeating, false otherwise.</p>
<h4>Remarks:</h4>
<p>For a complete list of keys that can be passed to this function, see input constants.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	show_window(&quot;Example&quot;);
	while (true) {
		wait(5);
		if (key_repeating(KEY_SPACE))
			screen_reader_output(&quot;space&quot;, true);
		if (key_pressed(KEY_ESCAPE))
			exit();
	}
}
</code></pre>
<h3>key_up</h3>
<p>Determine if a particular key is up.</p>
<p>bool key_up(uint key);</p>
<h4>Arguments:</h4>
<ul>
<li>uint key: the key to check.</li>
</ul>
<h4>Returns:</h4>
<p>bool: true if the key is up, false otherwise.</p>
<h4>Remarks:</h4>
<p>For a complete list of keys that can be passed to this function, see input constants.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	int last_spoken = ticks(); // Speak periodically to avoid overwhelming the user (or their screen reader).
	show_window(&quot;Example&quot;);
	while (true) {
		wait(5);
		if (key_up(KEY_SPACE) &amp;&amp; (ticks() - last_spoken) &gt;= 500) {
			last_spoken = ticks();
			screen_reader_output(&quot;space is up&quot;, true);
		}
		if (key_pressed(KEY_ESCAPE))
			exit();
	}
}
</code></pre>
<h3>keys_down</h3>
<p>Returns a handle to an array of keys that are held down.</p>
<p><code>uint[]@ keys_down();</code></p>
<h4>Returns:</h4>
<p>uint[]@: a handle to an array containing keys that are held down.</p>
<h4>Remarks:</h4>
<p>For a complete list of keys that can be returned by this function, see input constants.</p>
<h3>keys_pressed</h3>
<p>Returns a handle to an array of keys that were just pressed.</p>
<p><code>uint[]@ keys_pressed();</code></p>
<h4>Returns:</h4>
<p>uint[]@: a handle to an array containing keycodes that were just pressed.</p>
<h4>Remarks:</h4>
<p>For a complete list of keys that can be returned by this function, see input constants.</p>
<h3>keys_released</h3>
<p>Returns a handle to an array of keys that were just released.</p>
<p><code>uint[]@ keys_released();</code></p>
<h4>Returns:</h4>
<p>uint[]@: a handle to an array containing keycodes that were just released.</p>
<h4>Remarks:</h4>
<p>For a complete list of keys that can be returned by this function, see input constants.</p>
<h3>message_box</h3>
<p>Displays a customizable message box.</p>
<p>int message_box(const string&amp;in title, const string&amp;in text, string[]@ buttons, uint flags = 0);</p>
<h4>Arguments:</h4>
<ul>
<li><p>const string&amp;in title: the title of the message box.</p>
</li>
<li><p>const string&amp;in text: the text of the message box.</p>
</li>
<li><p>string[]@ buttons: a string array of button names, see remarks for more info.</p>
</li>
<li><p>uint flags = 0: a combination of flags (see message_box_flags for more information).</p>
</li>
</ul>
<h4>Returns:</h4>
<p>int: the number of the button that was pressed, according to its position in the buttons array.</p>
<h4>Remarks:</h4>
<p>Notes on button syntax:</p>
<ul>
<li><p>A grave character (`) prepending button text is default enter key.</p>
</li>
<li><p>A tilde character (~) before text means default cancel.</p>
</li>
</ul>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	message_box(&quot;Hello there&quot;, &quot;I am a message box with two buttons&quot;, {&quot;`OK&quot;, &quot;~Cancel&quot;});
}
</code></pre>
<h3>open_file_dialog</h3>
<p>Displays a dialog from which a user may select a file to open.</p>
<p>string open_file_dialog(string filters = &quot;&quot;, string default_location = &quot;&quot;)</p>
<h4>Arguments:</h4>
<ul>
<li><p>string filters = &quot;&quot;: A list of file extension filters (see remarks).</p>
</li>
<li><p>string default_location = &quot;&quot;: The absolute initial directory to select files from (empty for OS default).</p>
</li>
</ul>
<h4>Returns:</h4>
<p>string: The path to a file or an empty string on failure/cancelation.</p>
<h4>Remarks:</h4>
<p>The file extension filters are specified in the format description:extension|description:extension|description:extension1;extension2;extension3... You can also use the filter * as an all files filter. for example: audio files:mp3;wav;ogg|text files:txt;rtf;md|all files:* would produce 3 items in the file type combo box, those being audio files, text files and all files.</p>
<p>On some platforms it might be possible for the user to select a file that does not yet exist, so you should check for that condition yourself after the user selects a file just to be safe if that is important to you.</p>
<p>This function is blocking, though we plan to add a version of the API in the future that uses a callback function or an event you can wait on if you wish to use this dialog asynchronously.</p>
<p>You should only call this function on your application's main thread, which is what happens by default unless you use any of NVGT's threading facilities.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	string location = open_file_dialog(&quot;NVGT scripts:nvgt&quot;, cwdir());
	if (location.empty()) return;
	alert(&quot;example&quot;, &quot;you selected &quot; + location);
}
</code></pre>
<h3>query_touch_device</h3>
<p>Check what fingers are in contact with a touch device and where they are on the screen, if any.</p>
<p>touch_finger[]@ query_touch_device(uint64 device_id = 0);</p>
<h4>Arguments:</h4>
<ul>
<li>uint64 device_id = 0: The device to query, 0 for the last device that received input.</li>
</ul>
<h4>Returns:</h4>
<p>touch_finger[]@: An array of structures containing touch coordinates and pressure (see remarks).</p>
<h4>Remarks:</h4>
<p>Each structure in the returned array represents a finger, thus the length of the array indicates how many fingers are touching the device.</p>
<p>Touch_finger objects contain only 4 properties. Int64 id is a unique identifier of the finger that will remain the same as long as the finger touches the devices, float x and float y contain the coordinates of the finger on the device, and the float pressure property indicates how much force or pressure the finger is being applied to the device with.</p>
<p>Usage of this structure other than to receive touch input is not endorsed by the NVGT developers and may lead to unexpected results, most notably creating a touch_finger instance manually will likely set it's properties to random uninitialized memory on the stack. You have been warned.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	// Report the number of fingers touching the device.
	show_window(&quot;touch example&quot;);
	tts_voice tts;
	int prev_finger_count = 0;
	tts.speak(&quot;ready&quot;, true);
	while (!key_pressed(KEY_ESCAPE) and !key_pressed(KEY_AC_BACK)) {
		wait(5);
		touch_finger[]@ fingers = query_touch_device(); // This will query the last device that was touched.
		if (fingers.length() != prev_finger_count) {
			tts.speak(fingers.length() + (fingers.length() != 1? &quot; fingers&quot; : &quot; finger&quot;), true);
			prev_finger_count = fingers.length();
		}
	}
}
</code></pre>
<h3>question</h3>
<p>Display a yes/no dialog box to the user.</p>
<p>int question(const string&amp;in title, const string&amp;in text, bool can_cancel = false, uint flags = 0);</p>
<h4>Arguments:</h4>
<ul>
<li><p>const string&amp;in title: the title of the dialog.</p>
</li>
<li><p>const string&amp;in text: the text of the dialog.</p>
</li>
<li><p>bool can_cancel = false: determines if a cancel button is present alongside the other buttons.</p>
</li>
<li><p>uint flags = 0: a combination of flags (see message_box_flags for more information).</p>
</li>
</ul>
<h4>Returns:</h4>
<p>int: the number of the button that was pressed (1 for yes, 2 for no).</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	int res = question(&quot;Hello there&quot;, &quot;Do you like pizza?&quot;);
	alert(&quot;Info&quot;, &quot;You clicked &quot; + (res == 1 ? &quot;yes&quot; : &quot;no&quot;));
}
</code></pre>
<h3>refresh_window</h3>
<p>Updates the game window, pulling it for any new events and responding to messages from the operating system.</p>
<p><code>void refresh_window();</code></p>
<h4>Remarks:</h4>
<p>You do not need to call this function yourself so long as you use the recommended wait() function in your game's loops, as wait() implicitly calls this function. We provide refresh_window() standalone unless you want to use your own / a different sleeping mechanism such as nanosleep, in which case you do need to manually pull the window using this function.</p>
<p>For UI windows to function on the vast mejority of operating systems, they must maintain a constant stream of communication between the operating system and the program that created them. If a window stops receiving and handling such communications for even a few seconds, it will first become laggy before the operating system decides that the window has gone dead and begins reporting that the application is in a not responding or busy state.</p>
<p>To solve this problem in NVGT applications, refresh_window() is provided to do all of this message handling for you in one repeated function call. This function will pull the operating system for any new messages or events and process them, updating the states of functions like key_pressed, get_characters etc. If it is not repeatedly called in some way, your entire application will be disfunctional.</p>
<h3>save_file_dialog</h3>
<p>Displays a dialog from which a user may select a location to save a file.</p>
<p>string save_file_dialog(string filters = &quot;&quot;, string default_location = &quot;&quot;)</p>
<h4>Arguments:</h4>
<ul>
<li><p>string filters = &quot;&quot;: A list of file extension filters (see remarks).</p>
</li>
<li><p>string default_location = &quot;&quot;: The absolute initial directory to select from (empty for OS default).</p>
</li>
</ul>
<h4>Returns:</h4>
<p>string: The path to save to or an empty string on failure/cancelation.</p>
<h4>Remarks:</h4>
<p>The file extension filters are specified in the format description:extension|description:extension|description:extension1;extension2;extension3... You can also use the filter * as an all files filter. for example: audio files:mp3;wav;ogg|text files:txt;rtf;md|all files:* would produce 3 items in the file type combo box, those being audio files, text files and all files.</p>
<p>Keep in mind that the user may select a file that already exists if they wish to overwrite it.</p>
<p>This function is blocking, though we plan to add a version of the API in the future that uses a callback function or an event you can wait on if you wish to use this dialog asynchronously.</p>
<p>You should only call this function on your application's main thread, which is what happens by default unless you use any of NVGT's threading facilities.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	string location = save_file_dialog(&quot;text files (*.txt):txt|all files:*&quot;);
	if (location.empty()) return;
	alert(&quot;example&quot;, &quot;you selected &quot; + location);
}
</code></pre>
<h3>select_folder_dialog</h3>
<p>Displays a dialog from which a user may select a folder.</p>
<p>string select_folder_dialog(string default_location = &quot;&quot;)</p>
<h4>Arguments:</h4>
<ul>
<li>string default_location = &quot;&quot;: The absolute initial directory to select from (empty for OS default).</li>
</ul>
<h4>Returns:</h4>
<p>string: The path to a folder or an empty string on failure/cancelation.</p>
<h4>Remarks:</h4>
<p>Be aware that on some platforms, the user might be able to select a directory that does not yet exist.</p>
<p>This function is blocking, though we plan to add a version of the API in the future that uses a callback function or an event you can wait on if you wish to use this dialog asynchronously.</p>
<p>You should only call this function on your application's main thread, which is what happens by default unless you use any of NVGT's threading facilities.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	string location = select_folder_dialog();
	if (location.empty()) return;
	alert(&quot;example&quot;, &quot;you selected &quot; + location);
}
</code></pre>
<h3>set_application_name</h3>
<p>This function lets you set the name of your application. This is a name that's sent to your operating system in certain instances, for example in volume mixer dialogs or when an app goes not responding. It does not effect the window title or anything similar.</p>
<p><code>bool set_application_name(const string&amp;in application_name);</code></p>
<h4>Arguments:</h4>
<ul>
<li>const string&amp;in application_name: the name to set for your application.</li>
</ul>
<h4>Returns:</h4>
<p>bool: true if the name was successfully set, false otherwise.</p>
<h3>show_window</h3>
<p>Shows a window with the specified title.</p>
<p>bool show_window(const string&amp;in title);</p>
<h4>Arguments:</h4>
<ul>
<li>const string&amp;in title: the title of the window.</li>
</ul>
<h4>Returns:</h4>
<p>bool: true if window creation was successful, false otherwise.</p>
<h4>Remarks:</h4>
<p>This window doesn't do any event processing by default. As such, you have to create a loop in order to keep it alive.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	alert(&quot;Info&quot;, &quot;Press escape to close the window.&quot;);
	show_window(&quot;Example&quot;);
	while (true) {
		wait(5); // Don't hog all the CPU.
		if (key_pressed(KEY_ESCAPE))
			exit();
	}
}
</code></pre>
<h3>total_keys_down</h3>
<p>Returns the total number of keys that are currently held down.</p>
<p>int total_keys_down();</p>
<h4>Returns:</h4>
<p>int: the number of keys currently held down.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	int check_time = 1000, orig_ticks = ticks();
	show_window(&quot;Example&quot;);
	while (true) {
		wait(5);
		if ((ticks() - orig_ticks) &gt;= check_time) {
			orig_ticks = ticks();
			int key_count  = total_keys_down();
			screen_reader_output(key_count + &quot; &quot; + (key_count == 1 ? &quot;key is&quot; : &quot;keys are&quot;) + &quot; currently held down.&quot;, true);
		}
		if (key_pressed(KEY_ESCAPE))
			exit();
	}
}
</code></pre>
<h3>uninstall_keyhook</h3>
<p>Uninstall's NVGT's JAWS keyhook.</p>
<p>void uninstall_keyhook();</p>
<h4>Remarks:</h4>
<p>This keyhook allows NVGT games to properly capture keyboard input while the JAWS for Windows screen reader is running.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	install_keyhook();
	alert(&quot;Info&quot;, &quot;Keyhook installed. Uninstalling...&quot;);
	uninstall_keyhook();
	alert(&quot;Done&quot;, &quot;Keyhook uninstalled.&quot;);
}
</code></pre>
<h3>urlopen</h3>
<p>Opens the specified URL in the appropriate application, for example an https:// link in your web browser, or a tt://link in TeamTalk.</p>
<p>bool urlopen(const string&amp;in url);</p>
<h4>Arguments:</h4>
<ul>
<li>const string&amp;in url: The URL to open.</li>
</ul>
<h4>Returns:</h4>
<p>bool: true if the URl was successfully opened, false otherwise.</p>
<h4>Remarks:</h4>
<p>What application this function opens depends on what the user has set on their system; there's no way for you to control it.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	urlopen(&quot;https://nvgt.gg&quot;);
}
</code></pre>
<h3>wait</h3>
<p>Waits for a specified number of milliseconds.</p>
<p>void wait(int milliseconds);</p>
<h4>Arguments:</h4>
<ul>
<li>int milliseconds: the number of milliseconds to wait for.</li>
</ul>
<h4>Remarks:</h4>
<p>This function blocks the thread it's ran from, meaning no other work can happen on that thread until the wait period is over.</p>
<p>Since this function internally calls refresh_window() if it's being run on the main thread, it is strongly advised to always put <code>wait(5);</code> in your main loops. This prevents your game from hogging the CPU, and also makes sure that the window remains responsive and has been updated with the latest input events from the user.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	alert(&quot;Info&quot;, &quot;Once you press OK, I will wait for 2000 milliseconds (2 seconds).&quot;);
	wait(2000);
	alert(&quot;Info&quot;, &quot;2000 milliseconds passed!&quot;);
}
</code></pre>
