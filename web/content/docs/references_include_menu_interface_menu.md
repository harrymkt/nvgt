---
title: Menu Interface (menu.nvgt)
url: docs/references_include_menu_interface_menu.html
---

<h1>Menu Interface (menu.nvgt)</h1>
<h2>Classes</h2>
<h3>menu</h3>
<p>This class gives you an easy way to create a typical menu based on the audio_form list control item, including some nice aditional options such as navigation sounds, wrapping, and more.</p>
<h4>Methods</h4>
<h5>add_item</h5>
<p>Add an item to the menu.</p>
<p><code>bool menu::add_item(string text, string id = &quot;&quot;, int position = -1);</code></p>
<h6>Arguments:</h6>
<ul>
<li>string text: the text of the item to add to the menu.</li>
<li>string id = &quot;&quot;: the ID of the item.</li>
<li>int position = -1: the position to insert the new item at (-1 = end of menu).</li>
</ul>
<h6>Returns:</h6>
<p>int: the  position of the new item in the menu.</p>
<h5>intro</h5>
<p>Produces the intro sequence for the menu. It is not  required to call this function if you don't want to.</p>
<p><code>void menu::intro();</code></p>
<h5>monitor</h5>
<p>Monitors the menu; handles keyboard input, the callback, sounds and more. Should be called in a loop as long as the menu is active.</p>
<p><code>bool menu::monitor();</code></p>
<h6>Returns:</h6>
<p>bool: true if the menu should keep running, or false if it has been exited or if an option has been selected.</p>
<h5>reset</h5>
<p>Resets the menu to it's default state.</p>
<p><code>void menu::reset(bool reset_settings = false);</code></p>
<h6>Arguments:</h6>
<ul>
<li>bool reset_settings = false: If this is enabled, the sounds and other such properties are cleared.</li>
</ul>
<h4>Properties</h4>
<h5>automatic_intro</h5>
<p>If this is true, the intro function will be automatically called the first time the monitor method is invoqued, then the variable will be set to false. It can be set to true again at any time to cause the intro sequence to repeat, or the intro function can be called manually.</p>
<p>bool menu::automatic_intro;`</p>
<h5>click_sound</h5>
<p>The sound played when the user changes positions in the menu.</p>
<p><code>string menu::click_sound;</code></p>
<h5>close_sound</h5>
<p>The sound played when the user escapes out of the menu.</p>
<p><code>string menu::close_sound;</code></p>
<h5>edge_sound</h5>
<p>The sound which plays when the user attempts moving beyond the border of a menu while wrapping is disabled.</p>
<p><code>string menu::edge_sound;</code></p>
<h5>focus_first_item</h5>
<p>If this is false, the user will be required to press an arrow key to focus either the first or last item of the menu after the intro function has been called. Otherwise they will be focused on the first item.
This is disabled by default.</p>
<p><code>bool menu::focus_first_item;</code></p>
<h5>intro_text</h5>
<p>The text spoken when the void intro() function is called.</p>
<p><code>string menu::intro_text;</code></p>
<h5>open_sound</h5>
<p>The sound played when the void intro() function is called.</p>
<p><code>string menu::open_sound;</code></p>
<h5>pack_file</h5>
<p>Optionally set this to a pack containing sounds.</p>
<p><code>pack menu::pack_file;</code></p>
<h5>select_sound</h5>
<p>The sound played when the user chooses an option in the menu.</p>
<p><code>string menu::select_sound;</code></p>
<h5>wrap</h5>
<p>If the user moves beyond an edge of the menu, set this to true to jump them to the other edge, or false to play an edge sound and repeat the last item.
By default this is set to false.</p>
<p><code>bool menu::wrap;</code></p>
<h5>wrap_delay</h5>
<p>How much time (in ms) should the menu block when wrapping. Defaults to 10ms.</p>
<p><code>uint menu::wrap_delay;</code></p>
<h5>wrap_sound</h5>
<p>The sound played when the menu wraps (only happens when bool wrap = true).</p>
<p><code>string menu::wrap_sound;</code></p>
