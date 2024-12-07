---
title: touch gesture management (touch.nvgt)
url: docs/references_include_touch_gesture_management_touch.html
---

<h1>touch gesture management (touch.nvgt)</h1>
<h2>Classes</h2>
<h3>touch_gesture_manager</h3>
<p>Detects and then converts raw touch screen finger data into gesture events which can be detected by your application or even converted to keyboard input.</p>
<p>touch_gesture_manager();</p>
<h4>Remarks:</h4>
<p>This is the highest level interface NVGT offers to accessing touch screens. It looks at what fingers are touching the screen and where, and by monitoring that data over time, derives gestures such as swipes and taps from that data before passing them along to whatever interface you register to receive them.</p>
<p>An interface is included by default (see the touch_keyboard_interface class), which convertes these events into simulated keyboard input for you so that adding touch support to your game becomes as simple as mapping gesture names to keycode lists.</p>
<p>The basic usage of this class is to create an instatnce of it somewhere, before attaching any number of touch_interface instances to the manager and finally calling manager.monitor() within the loops of your programs to receive gesture events.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">#include&quot;touch.nvgt&quot;
#include&quot;speech.nvgt&quot;
touch_gesture_manager touch;
void main() {
	show_window(&quot;touch screen test&quot;);
	//attach multiple keys to a single gesture.
	int[] t = {KEY_TAB, KEY_LSHIFT};
	touch_keyboard_interface testsim(touch, \{\{&quot;swipe_left1f&quot;, KEY_LEFT}, {&quot;swipe_right1f&quot;, KEY_RIGHT}, {&quot;swipe_up1f&quot;, KEY_UP}, {&quot;swipe_down1f&quot;, KEY_DOWN}, {&quot;double_tap1f&quot;, KEY_RETURN}, {&quot;tripple_tap1f&quot;, t}, {&quot;swipe_left2f&quot;, KEY_ESCAPE}, {&quot;swipe_right2f&quot;, KEY_Q}, {&quot;double_tap2f&quot;, KEY_SPACE\}\});
	touch.add_touch_interface(testsim);
	dictionary@d = \{\{&quot;double_tap1f&quot;, KEY_X}, {&quot;double_tap2f&quot;, KEY_Z\}\};
	// Demonstrate registering an interface for only a portion of the screen.
	touch.add_touch_interface(touch_keyboard_interface(touch, d, 0.5, 1.0, 0.5, 1.0));
	while (!key_pressed(KEY_ESCAPE) and !key_pressed(KEY_AC_BACK)) {
		wait(5);
		touch.monitor();
		if (key_pressed(KEY_LEFT)) speak(&quot;left&quot;);
		if (key_pressed(KEY_RIGHT)) speak(&quot;right&quot;);
		if (key_pressed(KEY_DOWN)) speak(&quot;down&quot;);
		if (key_pressed(KEY_UP)) speak(&quot;up&quot;);
		if (key_pressed(KEY_TAB)) {
			speak(&quot;tripple tap&quot;);
			if (key_down(KEY_LSHIFT) or key_down(KEY_RSHIFT)) speak(&quot;you are holding down shift&quot;, false);
		}
		if (key_pressed(KEY_SPACE)) speak(&quot;double tap 2 fingers&quot;);
		if (key_pressed(KEY_ESCAPE)) exit();
		if (key_pressed(KEY_Q)) speak(&quot;swipe right 2 fingers&quot;);
		if (key_pressed(KEY_RETURN)) speak(&quot;you just double tapped the screen!&quot;, false);
		if (key_pressed(KEY_X)) speak(&quot;You just double tapped another part of the screen!&quot;);
		if (key_pressed(KEY_Z)) speak(&quot;You just double tapped with 2 fingers on another part of the screen!&quot;);
	}
}
</code></pre>
<h4>Methods</h4>
<h5>is_available</h5>
<p>Determine whether any touch devices are available to receive events from.</p>
<p>bool is_available();</p>
<h6>Returns:</h6>
<p>bool: true if at least one touch device is available on the system, false otherwise.</p>
<h6>Remarks:</h6>
<p>It is worth noting that due to circumstances outside our control, sometimes touch devices don't appear in the list until after you have touched them at least once. Therefor you should not use this method at program startup to determine with finality that no touch device is available, but could instead use it during program lifetime to monitor for whether touch support appears or disappears.</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">touch_gesture_manager touch;
void main() {
	wait(1000); // Give the user some time to touch the screen to make sure it appears.
	if (!touch.is_available()) alert(&quot;warning&quot;, &quot;This system does not appear to support touch screen devices&quot;);
}
</code></pre>
<h5>monitor</h5>
<p>Check for the latest touch events.</p>
<p><code>void monitor();</code></p>
<h6>Remarks:</h6>
<p>This function must be called in all of your game's loops in order for the system to work properly. Not doing this will lead to undefined behavior.</p>
<h5>set_interfaces</h5>
<p>Sets the list of interfaces that will receive touch events.</p>
<p><code>bool set_touch_interfaces(touch_interface@[]@ interfaces, bool append = false);</code></p>
<h6>Arguments:</h6>
<ul>
<li><code>touch_interface@[]@ interfaces</code>: A list of interfaces that will receive touch events.</li>
<li><code>bool append = false</code>: Determines whether to append to the list of existing interfaces Vs. replacing it.</li>
</ul>
<h6>Returns:</h6>
<p>bool: True if a change was made to the interface list, false otherwise.</p>
<h6>Remarks:</h6>
<p>You can pass multiple interfaces to a gesture manager because different interfaces can receive different events for various parts of the screen. An interface can simply return false in it's <code>is_bounds</code> method at any time to pass the gesture event to the next handler in the chain. Gesture interfaces are evaluated from newest to oldest.</p>
<h3>touch_keyboard_interface</h3>
<p>Convert gesture events to simulated keyboard input.</p>
<p><code>touch_keyboard_interface(touch_gesture_manager@parent, dictionary@map, float minx = TOUCH_UNCOORDINATED, float maxx = TOUCH_UNCOORDINATED, float miny = TOUCH_UNCOORDINATED, float maxy = TOUCH_UNCOORDINATED);</code></p>
<h4>Arguments:</h4>
<ul>
<li>touch_gesture_manager@ parent: A handle to the manager you intend to add this interface to, parameter subject for removal in future.</li>
<li>dictionary@ map: A mapping of gestures to keycode lists (see remarks).</li>
<li>float minx, maxx, miny, maxy = TOUCH_UNCOORDINATED: The bounds of this interface, default for entire screen or custom.</li>
</ul>
<h4>Remarks:</h4>
<p>This interface works by receiving a mapping of gesture names or IDs to lists of keycodes that should be simulated.</p>
<p>The basic format of gesture IDs consists of a gesture name followed by a number of fingers and the letter f. For example, to detect a 2 finger swipe right gesture, you would use the key &quot;swipe_right2f&quot; in the mapping dictionary. The available gesture names are as follows:</p>
<ul>
<li>swipe_left</li>
<li>swipe_right</li>
<li>swipe_up</li>
<li>swipe_down</li>
<li>double_tap</li>
<li>tripple_tap</li>
</ul>
