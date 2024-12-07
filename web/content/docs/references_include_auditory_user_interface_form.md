---
title: Auditory User Interface (form.nvgt)
url: docs/references_include_auditory_user_interface_form.html
---

<h1>Auditory User Interface (form.nvgt)</h1>
<h2>Classes</h2>
<h3>audio_form</h3>
<p>This class facilitates the easy creation of user interfaces that convey their usage entirely through audio.</p>
<h4>Notes:</h4>
<ul>
<li>many of the methods in this class only work on certain types of controls, and will return false and set an error value if used on invalid types of controls. This will generally be indicated in the documentation for each function.</li>
<li>Exceptions are not used here. Instead, we indicate errors through <code>audio_form::get_last_error()</code>.</li>
<li>An audio form object can have up to 50 controls.</li>
</ul>
<h4>Methods</h4>
<h5>activate_progress_timer</h5>
<p>Activate progress updates on a progress bar control.</p>
<p><code>bool audio_form::activate_progress_timer(int control_index);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the index of the progress bar.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the progress bar was successfully activated, false otherwise.</p>
<h5>add_list_item</h5>
<p>Add a string item to a list control.</p>
<ol>
<li><code>bool audio_form::add_list_item(int control_index, string option, int position = -1, bool selected = false, bool focus_if_first = true);</code></li>
<li><code>bool audio_form::add_list_item(int control_index, string option, string id, int position = -1, bool selected = false, bool focus_if_first = true);</code></li>
</ol>
<h6>Arguments (1):</h6>
<ul>
<li>int control_index: the control index of the list to add to.</li>
<li>string option: the item to add to the list.</li>
<li>int position = -1: the position to insert the new item at (-1 = end of list).</li>
<li>bool selected = false: should this item be selected by default?</li>
<li>bool focus_if_first = true: if this item is the first in the list and no other item gets explicitly focused, this item will be focused.</li>
</ul>
<h6>Arguments (2):</h6>
<ul>
<li>int control_index: the control index of the list to add to.</li>
<li>string option: the item to add to the list.</li>
<li>string id: the ID of the item in the list.</li>
<li>int position = -1: the position to insert the new item at (-1 = end of list).</li>
<li>bool selected = false: should this item be selected by default?</li>
<li>bool focus_if_first = true: if this item is the first in the list and no other item gets explicitly focused, this item will be focused.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the item was successfully added, false otherwise.</p>
<h6>Remarks:</h6>
<p>This function only works on list controls.</p>
<h5>clear_list</h5>
<p>Clear a list control of all its items.</p>
<p><code>bool audio_form::clear_list(int control_index);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the index of the list to clear.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the list was successfully cleared, false otherwise.</p>
<h5>create_button</h5>
<p>Creates a new button and adds it to the audio form.</p>
<p><code>int audio_form::create_button(string caption, bool primary = false, bool cancel = false, bool overwrite = true);</code></p>
<h6>Arguments:</h6>
<ul>
<li>string caption: the label to associate with the button.</li>
<li>bool primary = false: should this button be activated by pressing enter anywhere in the form?</li>
<li>bool cancel = false: should this button be activated by pressing escape anywhere in the form?</li>
<li>bool overwrite = true: overwrite any existing primary/cancel settings.</li>
</ul>
<h6>Returns:</h6>
<p>int: the control index of the new button, or -1 if there was an error. To get error information, look at <code>audio_form::get_last_error();</code>.</p>
<h5>create_checkbox</h5>
<p>Creates a new checkbox and adds it to the audio form.</p>
<p><code>int audio_form::create_checkbox(string caption, bool initial_value = false, bool read_only = false);</code></p>
<h6>Arguments:</h6>
<ul>
<li>string caption: the text to be read when tabbing over this checkbox.
*( bool initial_value = false: the initial value of the checkbox (true = checked, false = unchecked).</li>
<li>bool read_only = false: can the user check/uncheck this checkbox?</li>
</ul>
<h6>Returns:</h6>
<p>int: the control index of the new checkbox, or -1 if there was an error. To get error information, see <code>audio_form::get_last_error();</code>.</p>
<h5>create_input_box</h5>
<p>Creates an input box control on the audio form.</p>
<p><code>int audio_form::create_input_box(string caption, string default_text = &quot;&quot;, string password_mask = &quot;&quot;, int maximum_length = 0, bool read_only = false, bool multiline = false, bool multiline_enter = true);</code></p>
<h6>Arguments:</h6>
<ul>
<li>string caption: the label of the input box (e.g. what will be read when you tab over it?).</li>
<li>string default_text = &quot;&quot;: the text to populate the input box with by default (if any).</li>
<li>string password_mask = &quot;&quot;: a string to mask typed characters with, (e.g. &quot;star&quot;). Mainly useful if you want your field to be password protected. Leave blank for no password protection.</li>
<li>int maximum_length = 0: the maximum number of characters that can be typed in this field, 0 for unlimited.</li>
<li>bool read_only = false: should this text field be read-only?</li>
<li>bool multiline = false: should this text field have multiple lines?</li>
<li>bool multiline_enter = true: should pressing enter in this field insert a new line (if it's multiline)?</li>
</ul>
<h6>Returns:</h6>
<p>int: the control index of the new input box, or -1 if there was an error. To get error information, look at <code>audio_form::get_last_error();</code>.</p>
<h5>create_keyboard_area</h5>
<p>Creates a new keyboard area and adds it to the audio form.</p>
<p><code>int audio_form::create_keyboard_area(string caption);</code></p>
<h6>Arguments:</h6>
<ul>
<li>string caption: the text to be read when tabbing onto the keyboard area.</li>
</ul>
<h6>Returns:</h6>
<p>int: the control index of the new keyboard area, or -1 if there was an error. To get error information, see <code>audio_form::get_last_error();</code>.</p>
<h5>create_link</h5>
<p>Creates a new link and adds it to the audio form.</p>
<p><code>int audio_form::create_link(string caption, string url);</code></p>
<h6>Arguments:</h6>
<ul>
<li>string caption: the label of the link.</li>
<li>string url: The link to open.</li>
</ul>
<h6>Returns:</h6>
<p>int: the control index of the new link, or -1 if there was an error. To get error information, see <code>audio_form::get_last_error();</code>.</p>
<h6>Remarks:</h6>
<p>The link control is similar to buttons, but this opens the given link when pressed. This also speaks the error message if the link cannot be opened or the link isn't an actual URL. If you want the maximum possible customization, use <code>audio_form::create_button</code> method instead.</p>
<h5>create_list</h5>
<p>Creates a new list control and adds it to the audio form.</p>
<p><code>int audio_form::create_list(string caption, int maximum_items = 0, bool multiselect = false, bool repeat_boundary_items = false);</code></p>
<h6>Arguments:</h6>
<ul>
<li>string caption: the label to attach to this list.</li>
<li>int maximum_items = 0: the maximum number of allowed items, 0 for unlimited.</li>
<li>bool multiselect = false: can the user select multiple items in this list?</li>
<li>bool repeat_boundary_items = false: do items repeat if you press the arrow keys at the edge of the list?</li>
</ul>
<h6>Returns:</h6>
<p>int: the control index of the new list, or -1 if there was an error. To get error information, look at <code>audio_form::get_last_error();</code>.</p>
<h5>create_progress_bar</h5>
<p>Creates a new progress bar control and adds it to the audio form.</p>
<p><code>int audio_form::create_progress_bar(string caption, int speak_interval = 5, bool speak_global = true);</code></p>
<h6>Arguments:</h6>
<ul>
<li>string caption: the label to associate with the progress bar.</li>
<li>int speak_interval = 5: how often to speak percentage changes.</li>
<li>bool speak_global = true: should progress updates be spoken even when this control doesn't have keyboard focus?</li>
</ul>
<h6>Returns:</h6>
<p>int: the control index of the new progress bar, or -1 if there was an error. To get error information, look at <code>audio_form::get_last_error();</code>.</p>
<h5>create_slider</h5>
<p>Creates a new slider control and adds it to the audio form.</p>
<p><code>int audio_form::create_slider(string caption, double default_value = 50, double minimum_value = 0, double maximum_value = 100, string text = &quot;&quot;, double step_size = 1);</code></p>
<h6>Arguments:</h6>
<ul>
<li>string caption: the text to be spoken when this slider is tabbed over.</li>
<li>double default_value = 50: the default value to set the slider to.</li>
<li>double minimum_value = 0: the minimum value of the slider.</li>
<li>double maximum_value = 100: the maximum value of the slider.</li>
<li>string text = &quot;&quot;: extra text to be associated with the slider.</li>
<li>double step_size = 1: the value that will increment/decrement the slider value.</li>
</ul>
<h6>Returns:</h6>
<p>int: the control index of the new slider, or -1 if there was an error. To get error information, see <code>audio_form::get_last_error();</code>.</p>
<h5>create_status_bar</h5>
<p>Creates a new status bar and adds it to the audio form.</p>
<p><code>int audio_form::create_status_bar(string caption, string text);</code></p>
<h6>Arguments:</h6>
<ul>
<li>string caption: the label of the status bar.</li>
<li>string text: the text to display on the status bar.</li>
</ul>
<h6>Returns:</h6>
<p>int: the control index of the new status bar, or -1 if there was an error. To get error information, see <code>audio_form::get_last_error();</code>.</p>
<h5>create_subform</h5>
<p>Creates a new sub form and adds it to the audio form.</p>
<p>int audio_form::create_subform(string caption, audio_form@ f);</p>
<h6>Arguments:</h6>
<ul>
<li><p>string caption: the label to associate with the sub form.</p>
</li>
<li><p>audio_form@ f: an object pointing to an already created form.</p>
</li>
</ul>
<h6>Returns:</h6>
<p>int: the control index of the new sub form control, or -1 if there was an error. To get error information, look at <code>audio_form::get_last_error();</code>.</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">#include &quot;form.nvgt&quot;
// some imaginary global application variables.
bool logostart = true, menuwrap = false, firespace = false, radar = true;
// First, lets make a class which stores a category name and the form that the category is linked to.
class settings_category {
	string name;
	audio_form@ f;
	settings_category(string n, audio_form@ f) {
		this.name = n;
		@this.f = @f;
	}
}
void settings_dialog() {
	// Define some categories and settings on each category like this:
	audio_form fc_general;
	fc_general.create_window();
	int f_logostart = fc_general.create_checkbox(&quot;Play &amp;logo on startup&quot;, logostart);
	int f_menuwrap = fc_general.create_checkbox(&quot;Wrap &amp;menus&quot;, menuwrap);
	audio_form fc_gameplay;
	fc_gameplay.create_window();
	int f_firespace = fc_gameplay.create_checkbox(&quot;Use space instead of control to &amp;fire&quot;, firespace);
	int f_radar = fc_gameplay.create_checkbox(&quot;Enable the &amp;radar&quot;, firespace);
	// Add as many categories as you want this way.
	audio_form f; // The overarching main form.
	f.create_window(&quot;Settings&quot;, false, true);
	int f_category_list = f.create_tab_panel(&quot;&amp;Category&quot;); // The user will select categories from here. Note: you can also use create_list.
	int f_category_display = f.create_subform(&quot;General settings&quot;, @fc_general); // Now by default, the main form embeds the general category form right there.
	int f_ok = f.create_button(&quot;&amp;Save settings&quot;, true);
	int f_cancel = f.create_button(&quot;Cancel&quot;, false, true);
	// Now lets create a structured list of categories that can be browsed based on the class above.
	settings_category@[] categories = {
		settings_category(&quot;General&quot;, @fc_general),
		settings_category(&quot;Gameplay&quot;, @fc_gameplay)
	};
	// And then add the list of categories to the form's list.
	for (uint i = 0; i &lt; categories.length(); i++) {
		f.add_list_item(f_category_list, categories[i].name);
	}
	// Focus the form's list position on the general category, then set the form's initial focused control to the category list.
	f.set_list_position(f_category_list, 0);
	f.focus(0);
	settings_category@ last_category = @categories[0]; // A handle to the currently selected category so we can detect changes to the selection.
	// Finally this is the loop that does the rest of the magic.
	while (!f.is_pressed(f_cancel)) {
		wait(5);
		f.monitor();
		int pos = f.get_list_position(f_category_list);
		settings_category@ selected_category = null;
		if (pos &gt; -1 and pos &lt; categories.length())
			@selected_category = @categories[pos];
		if (@last_category != @selected_category) {
			last_category.f.subform_control_index = -1; // Later improvements to audio form will make this line be handled internally.
			last_category.f.focus_silently(0); // Make sure that if the category is reselected, it is focused on the first control.
			@last_category = @selected_category;
			f.set_subform(f_category_display, @selected_category.f);
			f.set_caption(f_category_display, selected_category.name + &quot; settings&quot;);
		}
		// The following is a special feature I came up with in stw which makes it so that if you are in the category list, keyboard shortcuts from the entire form will work regardless of category.
		if (f.get_current_focus() == f_category_list and key_down(KEY_LALT) or key_down(KEY_RALT)) {
			for (uint i = 0; i &lt; categories.length(); i++) {
				if (categories[i].f.check_shortcuts(true)) {
					f.set_list_position(f_category_list, i);
					@last_category = @categories[i];
					f.set_subform(f_category_display, @last_category.f);
					f.set_caption(f_category_display, last_category.name + &quot; settings&quot;);
					f.focus(f_category_display);
					break;
				}
			}
		}
		// Now we can finally check for the save button.
		if (f.is_pressed(f_ok)) {
			logostart = fc_general.is_checked(f_logostart);
			menuwrap = fc_general.is_checked(f_menuwrap);
			firespace = fc_gameplay.is_checked(f_firespace);
			radar = fc_gameplay.is_checked(f_radar);
			return;
		}
	}
}
// Lets make this thing run so we can see it work.
void main() {
	show_window(&quot;test&quot;);
	settings_dialog();
}
</code></pre>
<h5>create_window</h5>
<p>Creates a window to show audio form controls.</p>
<ol>
<li><p>void audio_form::create_window();</p>
</li>
<li><p>void audio_form::create_window(string window_title, bool change_screen_title = true, bool say_dialog = true, bool silent = false);</p>
</li>
</ol>
<h6>Arguments (2):</h6>
<ul>
<li><p>string window_title: the title of the window.</p>
</li>
<li><p>bool change_screen_title = true: whether or not the main window's title should be set as well.</p>
</li>
<li><p>bool say_dialog = true: whether or not the window should be reported as a dialog (in the context of the audio form).</p>
</li>
<li><p>bool silent = false: should this window be shown silently?</p>
</li>
</ul>
<h6>Example:</h6>
<pre><code class="language-NVGT">#include &quot;form.nvgt&quot;
#include &quot;speech.nvgt&quot;
void main() {
	audio_form f;
	f.create_window(&quot;Test&quot;);
	wait(50); // Give screen readers time to speak the window title.
	int f_exit = f.create_button(&quot;exit&quot;);
	f.focus(f_exit);
	while (true) {
		wait(5);
		f.monitor();
		if (f.is_pressed(f_exit))
			exit();
	}
}
</code></pre>
<h5>delete_control</h5>
<p>Removes a control with a particular index from the audio form.</p>
<p><code>bool audio_form::delete_control(int control_index);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the index of the control to delete.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the control was successfully deleted, false otherwise.</p>
<h5>delete_list_item</h5>
<p>Remove an item from a list control.</p>
<p><code>bool audio_form::delete_list_item(int control_index, int list_index, bool reset_cursor = true, bool speak_deletion_status = true);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the index of the list to remove the item from.</li>
<li>int list_index: the index of the item to remove.</li>
<li>bool reset_cursor = true: should the user's cursor position be reset to the top of the list upon success?</li>
<li>bool speak_deletion_status = true: should the user be informed of the deletion via speech feedback?</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the item was successfully deleted, false otherwise.</p>
<h5>delete_list_selections</h5>
<p>Unselect any currently selected items in a list control.</p>
<p><code>bool audio_form::delete_list_selections(int control_index, bool reset_cursor = true, bool speak_deletion_status = true);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the index of the list to unselect items in.</li>
<li>bool reset_cursor = true: should the user's cursor position be reset to the top of the list upon success?</li>
<li>bool speak_deletion_status = true: should the user be informed of the unselection via speech feedback?</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the selection was successfully cleared, false otherwise.</p>
<h5>edit_list_item</h5>
<p>Edits the value of a list item.</p>
<p><code>bool audio_form::edit_list_item(int control_index, string new_option, int position);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the index of the list containing the item.</li>
<li>string new_option: the new text of the item.</li>
<li>int position: the item's index in the list.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the item's value was successfully updated, false otherwise.</p>
<h5>edit_list_item_id</h5>
<p>Modifies the ID of a list item.</p>
<p><code>bool audio_form::edit_list_item_id(int control_index, string new_id, int position);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the index of the list containing the item.</li>
<li>string new_id: the new ID of the list item.</li>
<li>int position: the item's index in the list.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the item's ID was successfully updated, false otherwise.</p>
<h5>focus</h5>
<p>Set a particular control to have the keyboard focus, and notify the user.</p>
<p><code>bool audio_form::focus(int control_index);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the index of the control to focus.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the control was successfully focused, false otherwise.</p>
<h5>focus_interrupt</h5>
<p>Set a particular control to have the keyboard focus, and notify the user (cutting off any previous speech).</p>
<p><code>bool audio_form::focus_interrupt(int control_index);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the index of the control to focus.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the control was successfully focused, false otherwise.</p>
<h5>focus_silently</h5>
<p>Set a particular control to have the keyboard focus, without notifying the user.</p>
<p><code>bool audio_form::focus_silently(int control_index);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the index of the control to focus.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the control was successfully focused, false otherwise.</p>
<h5>get_cancel_button</h5>
<p>Get the control index of the cancel button (e.g. the button activated when pressing escape anywhere on an audio form).</p>
<p><code>int audio_form::get_cancel_button();</code></p>
<h6>Returns:</h6>
<p>int: the control index of the cancel button.</p>
<h5>get_caption</h5>
<p>Get the caption of a control.</p>
<p><code>string audio_form::get_caption(int control_index);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the index of the control to query.</li>
</ul>
<h6>Returns:</h6>
<p>string: the caption of the control.</p>
<h5>get_checked_list_items</h5>
<p>Get a list of all currently checked items in a list control.</p>
<p><code>int[]@ audio_form::get_checked_list_items(int control_index);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the index of the list to query.</li>
</ul>
<h6>Returns:</h6>
<p>int[]@: handle to an array containing the index of every checked item in the list.</p>
<h6>Remarks:</h6>
<p>This function only works on multiselect lists. If you want something that also works on single-select lists, see <code>get_list_selections()</code>.</p>
<h5>get_control_count</h5>
<p>Returns the number of controls currently present on the form.</p>
<p><code>int audio_form::get_control_count();</code></p>
<h6>Returns:</h6>
<p>int: the number of controls currently on the form.</p>
<h5>get_control_type</h5>
<p>Returns the type of a control.</p>
<p><code>int audio_form::get_control_type(int control_index);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the index of the control to get the type of.</li>
</ul>
<h6>Returns:</h6>
<p>int: the type of the control (see control_types for more information).</p>
<h5>get_current_focus</h5>
<p>Get the control index of the control with the keyboard focus.</p>
<p><code>int audio_form::get_current_focus();</code></p>
<h6>Returns:</h6>
<p>int: the control index that currently has the keyboard focus.</p>
<h5>get_custom_type</h5>
<p>Get the custom type of the control, if available.</p>
<p><code>string audio_form::get_custom_type(int control_index);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the control you want to check.</li>
</ul>
<h6>Returns:</h6>
<p>string: the custom type set on this control if available, an empty string otherwise.</p>
<h5>get_default_button</h5>
<p>Get the control index of the default button (e.g. the button activated when pressing enter anywhere on an audio form).</p>
<p><code>int audio_form::get_default_button();</code></p>
<h6>Returns:</h6>
<p>int: the control index of the default button.</p>
<h5>get_last_error</h5>
<p>Get the last error that was raised from this form.</p>
<p><code>int audio_form::get_last_error();</code></p>
<h6>Returns:</h6>
<p>int: the last error code raised by this audio_form ( see audioform_errorcodes for more information).</p>
<h6>Remarks:</h6>
<p>As noted in the introduction to this class, exceptions are not used here. Instead, we indicate errors through this function.</p>
<h5>get_line_column</h5>
<p>Get the current line column of an input box.</p>
<p><code>int audio_form::get_line_column(int control_index);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the index of the input box to retrieve the line column from.</li>
</ul>
<h6>Returns:</h6>
<p>int: The line column of the input box, or -1 if there was an error.</p>
<h6>Remarks:</h6>
<p>This method only works on input boxes.</p>
<h5>get_line_number</h5>
<p>Get the current line number of an input box.</p>
<p><code>int audio_form::get_line_number(int control_index);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the index of the input box to retrieve the line number from.</li>
</ul>
<h6>Returns:</h6>
<p>int: The line number of the input box, or -1 if there was an error.</p>
<h6>Remarks:</h6>
<p>This method only works on input boxes.</p>
<h5>get_link_url</h5>
<p>Retrieves the URL of the link control.</p>
<p><code>string audio_form::get_link_url(int control_index);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the index of the control.</li>
</ul>
<h6>Returns:</h6>
<p>string: the URL.</p>
<h6>Remarks:</h6>
<p>This method only works on link control.</p>
<h5>get_list_count</h5>
<p>Get the number of items contained in a list control.</p>
<p><code>int audio_form::get_list_count(int control_index);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: index of the list control to query.</li>
</ul>
<h6>Returns:</h6>
<p>int: the number of items in the list.</p>
<h5>get_list_index_by_id</h5>
<p>Get the index of a list item by its ID.</p>
<p><code>int audio_form::get_list_index_by_id(int control_index, string id);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the index of the list.</li>
<li>string id: the ID of the item to query.</li>
</ul>
<h6>Returns:</h6>
<p>int: the index of the item, -1 on error.</p>
<h5>get_list_item</h5>
<p>Get the text of a particular list item.</p>
<p><code>string audio_form::get_list_item(int control_index, int list_index);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the index of the list.</li>
<li>int list_index: the index of the item to get.</li>
</ul>
<h6>Returns:</h6>
<p>string: the text of the item.</p>
<h5>get_list_item_id</h5>
<p>Get the ID of a particular list item.</p>
<p><code>string audio_form::get_list_item_id(int control_index, int list_index);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the index of the list.</li>
<li>int list_index: the index of the item to get.</li>
</ul>
<h6>Returns:</h6>
<p>string: the ID of the item.</p>
<h5>get_list_position</h5>
<p>Get the user's currently focused item in a list control.</p>
<p><code>int audio_form::get_list_position(int control_index);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the index of the list.</li>
</ul>
<h6>Returns:</h6>
<p>int: the user's current cursor position in the list.</p>
<h5>get_list_selections</h5>
<p>Get a list of all items currently selected in a list control.</p>
<p><code>int[]@ audio_form::get_list_selections(int control_index);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the index of the list to query.</li>
</ul>
<h6>Returns:</h6>
<p>int[]@: handle to an array containing the index of every selected item in the list (see remarks).</p>
<h6>Remarks:</h6>
<p>In the context of this function, a selected item is any item that  is checked (if the list supports multiselection), as well as the currently selected item. If you want to only get the state of checked list items, see the <code>get_checked_list_items()</code> function.</p>
<h5>get_progress</h5>
<p>Get the value of a progress bar.</p>
<p><code>int audio_form::get_progress(int control_index);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the index of the progress bar to query.</li>
</ul>
<h6>Returns:</h6>
<p>int: the current value of the progress bar.</p>
<h6>Remarks:</h6>
<p>This method only works on progress bar controls.</p>
<h5>get_slider</h5>
<p>Get the value of a slider.</p>
<p><code>double audio_form::get_slider(int control_index);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the index of the slider to query.</li>
</ul>
<h6>Returns:</h6>
<p>double: the current value of the slider. In case of error, this may return -1. To get error information, see <code>audio_form::get_last_error();</code>.</p>
<h6>Remarks:</h6>
<p>This method only works on slider control.</p>
<h5>get_slider_maximum_value</h5>
<p>Get the maximum value of a slider.</p>
<p><code>double audio_form::get_slider_maximum_value(int control_index);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the index of the slider to query.</li>
</ul>
<h6>Returns:</h6>
<p>double: the maximum allowable value the slider may be set to. In case of error, this may return -1. To get error information, see <code>audio_form::get_last_error();</code>.</p>
<h6>Remarks:</h6>
<p>This method only works on slider control.</p>
<h5>get_slider_minimum_value</h5>
<p>Get the minimum value of a slider.</p>
<p><code>double audio_form::get_slider_minimum_value(int control_index);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the index of the slider to query.</li>
</ul>
<h6>Returns:</h6>
<p>double: the minimum allowable value the slider may be set to. In case of error, this may return -1. To get error information, see <code>audio_form::get_last_error();</code>.</p>
<h6>Remarks:</h6>
<p>This method only works on slider control.</p>
<h5>get_text</h5>
<p>Get the text from an input box or status bar.</p>
<p><code>string audio_form::get_text(int control_index);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the index of the control to retrieve the text from.</li>
</ul>
<h6>Returns:</h6>
<p>string: The text from the control, or an empty string if there was an error.</p>
<h6>Remarks:</h6>
<p>This method only works on input boxes and status bars.</p>
<h5>has_custom_type</h5>
<p>Determines whether the control has its custom type set.</p>
<p><code>bool audio_form::has_custom_type(int control_index);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the control you want to check.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the control has its custom type set, false otherwise.</p>
<h6>Remarks:</h6>
<p>Please note that this method is equivalent to <code>audio_form::get_custom_type(control_index).empty()</code></p>
<h5>is_checked</h5>
<p>Get the state of a checkbox.</p>
<p><code>bool audio_form::is_checked(int control_index);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the index of the control to query.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the checkbox is checked, false otherwise.</p>
<h6>Remarks:</h6>
<p>This function only works on checkbox controls.</p>
<h5>is_disallowed_char</h5>
<p>Determines whether the text of a given control contains characters that are not allowed, set by the <code>audio_form::set_disallowed_chars</code> method.</p>
<p><code>bool audio_form::is_disallowed_char(int control_index, string char, bool search_all = true);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the index of the control.</li>
<li>string char: one or more characters to query</li>
<li>bool search_all = true: toggles whether to search character by character or to match the entire string.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the text of the control contains disallowed characters, false otherwise.</p>
<h6>Remarks:</h6>
<p>The <code>search_all</code> parameter will match the characters depending upon its state. If set to false, the entire string will be searched. If set to true, it will loop through each character and see if one of them contains disallowed character. Thus, you will usually set this to true. One example you might set to false is when the form only has 1 character length, but it is not required, it is looping each character already. However, it is also a good idea to turn this off for the maximum possible performance if you're sure that the input only requires 1 length of characters.</p>
<h5>is_enabled</h5>
<p>Determine if a particular control is enabled or not.</p>
<p><code>bool audio_form::is_enabled(int control_index);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the index of the control to query.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the control is enabled, false if it's disabled.</p>
<h5>is_list_item_checked</h5>
<p>Determine if the list item at a particular index is checked or not.</p>
<p><code>bool audio_form::is_list_item_checked(int control_index, int item_index);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the index of the list containing the item to be checked.</li>
<li>int item_index: the index of the item to check.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the item exists and is checked, false otherwise.</p>
<h5>is_multiline</h5>
<p>Determine if a particular control is multiline or not.</p>
<p><code>bool audio_form::is_multiline(int control_index);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the index of the control to query.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the control is multiline, false otherwise.</p>
<h6>Remarks:</h6>
<p>This function only works on input boxes.</p>
<h5>is_pressed</h5>
<p>Determine if a particular button was just pressed.</p>
<p><code>bool audio_form::is_pressed(int control_index);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the index of the control to query.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the button was just pressed, false otherwise.</p>
<h6>Remarks:</h6>
<p>This function only works on button controls.</p>
<h5>is_read_only</h5>
<p>Determine if a particular control is read-only or not.</p>
<p><code>bool audio_form::is_read_only(int control_index);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the index of the control to query.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the control is read-only, false if it's not.</p>
<h6>Remarks:</h6>
<p>This function only works on input boxes and checkboxes.</p>
<h5>is_visible</h5>
<p>Determine if a particular control is visible or not.</p>
<p><code>bool audio_form::is_visible(int control_index);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the index of the control to query.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the control is visible, false if it's invisible.</p>
<h5>monitor</h5>
<p>Processes all keyboard input, and dispatches all events to the form. Should be called in your main loop.</p>
<p><code>int audio_form::monitor();</code></p>
<h6>Returns:</h6>
<p>int: this value can be ignored for users of this class; it's used internally for subforms.</p>
<h5>pause_progress_timer</h5>
<p>Pause updating of a progress bar control.</p>
<p><code>bool audio_form::pause_progress_timer(int control_index);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the index of the progress bar.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the progress bar was paused, false otherwise.</p>
<h5>set_button_attributes</h5>
<p>Set the primary and cancel flags of a button.</p>
<p>`bool audio_form::set_button_attributes(int control_index, bool primary, bool cancel, bool overwrite = true);</p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the index of the button to update.</li>
<li>bool primary: should this button be made primary (e.g. pressing enter from anywhere on the form activates it)?</li>
<li>bool cancel: should this button be made the cancel button (e.g. should pressing escape from anywhere on the form always activate it?).</li>
<li>bool overwrite = true: should the previous primary and cancel buttons (if any) be overwritten?</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the attributes were successfully set, false otherwise.</p>
<h5>set_caption</h5>
<p>Sets the caption of a control.</p>
<p><code>bool audio_form::set_caption(int control_index, string caption);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the index of the control.</li>
<li>string caption: the caption to set on the control (see remarks for more infromation).</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the caption was successfully set, false otherwise.</p>
<h6>Remarks:</h6>
<p>The caption is read every time a user focuses this particular control.</p>
<p>It is possible to associate hotkeys with controls by putting an &quot;&amp;&quot; symbol in the caption. For example, setting the caption of a button to &quot;E&amp;xit&quot; would assign the hotkey alt+x to focus it.</p>
<h5>set_checkbox_mark</h5>
<p>Set the state of a checkbox (either checked or unchecked).</p>
<p><code>bool audio_form::set_checkbox_mark(int control_index, bool checked);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the control index of the checkbox.</li>
<li>bool checked: whether the checkbox should be set to checked or not.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the operation was successful, false otherwise. To get error information, look at <code>audio_form::get_last_error();</code>.</p>
<h5>set_custom_type</h5>
<p>Sets a custom type for a control.</p>
<p><code>bool audio_form::set_custom_type(int control_index, string custom_type);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the index of the control.</li>
<li>string custom_type: a custom text type to set on the control.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the custom text type was successfully set, false otherwise.</p>
<h5>set_default_controls</h5>
<p>Sets default and cancel buttons for this form.</p>
<p><code>bool set_default_controls(int primary, int cancel);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int primary: the control index of the button to make primary.</li>
<li>int cancel: the control index of the cancel button.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the controls were successfully set, false otherwise.</p>
<h5>set_default_keyboard_echo</h5>
<p>Sets the default keyboard echo of controls on your form.</p>
<p><code>bool audio_form::set_default_keyboard_echo(int keyboard_echo, bool update_controls = true);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int keyboard_echo: the keyboard echo mode to use (see text_entry_speech_flags for more information).</li>
<li>bool update_controls = true: whether or not this echo should be applied to any controls that already exist on your form.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the echo was successfully set, false otherwise.</p>
<h5>set_disallowed_chars</h5>
<p>Sets the whitelist/blacklist characters of a control.</p>
<p><code>bool audio_form::set_disallowed_chars(int control_index, string chars, bool use_only_disallowed_chars = false, string char_disallowed_description = &quot;&quot;);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the index of the control.</li>
<li>string chars: the characters to set.</li>
<li>bool use_only_disallowed_chars = false: sets whether the control should only use the characters in this list. true means use only characters that are in the list, and false means allow only characters that are not in the list.</li>
<li>string char_disallowed_description = &quot;&quot;: the text to speak when an invalid character is inputted.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the characters were successfully set, false otherwise.</p>
<h6>Remarks:</h6>
<p>Setting the <code>use_only_disallowed_chars</code> parameter to true will restrict all characters that are not in the list. This is useful to prevent other characters in number inputs.</p>
<p>Setting the chars parameter to empty will clear the characters and will switch back to default.</p>
<p>Please note that these character sets will also restrict the text from being pasted if the clipboard contains disallowed characters.</p>
<h5>set_enable_go_to_index</h5>
<p>Toggles whether the control can use go to line functionality.</p>
<p><code>bool audio_form::set_enable_go_to_index(int control_index, bool enabled);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the index of the control.</li>
<li>bool enabled: enables the go to line functionality.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the state was successfully set, false otherwise.</p>
<h5>set_enable_search</h5>
<p>Toggles whether the control can use search functionality.</p>
<p><code>bool audio_form::set_enable_search(int control_index, bool enabled);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the index of the control.</li>
<li>bool enabled: enables the search functionality.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the state was successfully set, false otherwise.</p>
<h5>set_keyboard_echo</h5>
<p>Set the keyboard echo for a particular control.</p>
<p><code>bool audio_form::set_keyboard_echo(int control_index, int keyboard_echo);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the index of the control to modify.</li>
<li>int keyboard_echo: the keyboard echo mode to use (see text_entry_speech_flags for more information).</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the keyboard echo was successfully set, false otherwise.</p>
<h5>set_link_url</h5>
<p>Sets the URL of the link control.</p>
<p><code>bool audio_form::set_link_url(int control_index, string new_url);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the index of the control.</li>
<li>string new_url: the URL to set.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true on success, false on failure.</p>
<h6>Remarks:</h6>
<p>This method only works on link control.</p>
<h5>set_list_multinavigation</h5>
<p>Configures how the multi-letter navigation works in a list control.</p>
<p><code>bool audio_form::set_list_multinavigation(int control_index, bool letters, bool numbers, bool nav_translate = true);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the index of the list control.</li>
<li>bool letters: can the user navigate with letters?</li>
<li>bool numbers: can the user navigate with the numbers.</li>
<li>bool nav_translate = true: should the letters work with the translated alphabet in use?</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the settings were successfully set, false otherwise.</p>
<h5>set_list_position</h5>
<p>Set the user's cursor in a list control.</p>
<p><code>bool audio_form::set_list_position(int control_index, int position = -1, bool speak_new_item = false);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the index of the list.</li>
<li>int position = -1: the new cursor position (-1 for no selection).</li>
<li>bool speak_new_item = false: should the user be notified of the selection change via speech?</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the cursor position was successfully set, false otherwise.</p>
<h5>set_list_properties</h5>
<p>Sets the properties of a list control.</p>
<p><code>bool audio_form::set_list_propertyes(int control_index, bool multiselect=false, bool repeat_boundary_items=false);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the index of the list.</li>
<li>bool multiselect = false: can the user select multiple items in this list?</li>
<li>bool repeat_boundary_items = false: do items repeat if you press the arrow keys at the edge of the list?</li>
</ul>
<h6>Returns:</h6>
<p>bool: true on success, false on failure.</p>
<h5>set_progress</h5>
<p>Sets the progress percentage on the progress control.</p>
<p><code>bool audio_form::set_progress(int control_index, int value);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the index of the control.</li>
<li>int value: the percentage to set.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true on success, false on failure.</p>
<h6>Remarks:</h6>
<p>This method only works on progress control.</p>
<h5>set_slider</h5>
<p>Sets the value of the slider control.</p>
<p><code>bool audio_form::set_slider(int control_index, double value, double min = -1, double max = -1);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the index of the control.</li>
<li>double value: the value to set.</li>
<li>double min = -1: the minimum value to set. This can be omitted.</li>
<li>double max = -1: the maximum value to set. This can be omitted.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true on success, false on failure.</p>
<h6>Remarks:</h6>
<p>This method only works on slider control.</p>
<h5>set_state</h5>
<p>Set the enabled/visible state of a control.</p>
<p><code>bool audio_form::set_state(int control_index, bool enabled, bool visible);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the index of the control.</li>
<li>bool enabled: is the control enabled (e.g. if it's a button, being disabled would make the button unpressable).</li>
<li>bool visible: can the user access the control with the navigation commands?</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the state was successfully set, false otherwise.</p>
<h5>set_subform</h5>
<p>Sets a sub form to use on the current form.</p>
<p>bool audio_form::set_subform(int control_index, audio_form@ f);</p>
<h6>Arguments:</h6>
<ul>
<li><p>int control_index: the control index of the sub form created with <code>audio_form::create_subform</code> method.</p>
</li>
<li><p>audio_form@ f: an object pointing to an already created form.</p>
</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the operation was successful, false otherwise. To get error information, look at <code>audio_form::get_last_error();</code>.</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">#include &quot;form.nvgt&quot;
// some imaginary global application variables.
bool logostart = true, menuwrap = false, firespace = false, radar = true;
// First, lets make a class which stores a category name and the form that the category is linked to.
class settings_category {
	string name;
	audio_form@ f;
	settings_category(string n, audio_form@ f) {
		this.name = n;
		@this.f = @f;
	}
}
void settings_dialog() {
	// Define some categories and settings on each category like this:
	audio_form fc_general;
	fc_general.create_window();
	int f_logostart = fc_general.create_checkbox(&quot;Play &amp;logo on startup&quot;, logostart);
	int f_menuwrap = fc_general.create_checkbox(&quot;Wrap &amp;menus&quot;, menuwrap);
	audio_form fc_gameplay;
	fc_gameplay.create_window();
	int f_firespace = fc_gameplay.create_checkbox(&quot;Use space instead of control to &amp;fire&quot;, firespace);
	int f_radar = fc_gameplay.create_checkbox(&quot;Enable the &amp;radar&quot;, firespace);
	// Add as many categories as you want this way.
	audio_form f; // The overarching main form.
	f.create_window(&quot;Settings&quot;, false, true);
	int f_category_list = f.create_tab_panel(&quot;&amp;Category&quot;); // The user will select categories from here. Note: you can also use create_list.
	int f_category_display = f.create_subform(&quot;General settings&quot;, @fc_general); // Now by default, the main form embeds the general category form right there.
	int f_ok = f.create_button(&quot;&amp;Save settings&quot;, true);
	int f_cancel = f.create_button(&quot;Cancel&quot;, false, true);
	// Now lets create a structured list of categories that can be browsed based on the class above.
	settings_category@[] categories = {
		settings_category(&quot;General&quot;, @fc_general),
		settings_category(&quot;Gameplay&quot;, @fc_gameplay)
	};
	// And then add the list of categories to the form's list.
	for (uint i = 0; i &lt; categories.length(); i++) {
		f.add_list_item(f_category_list, categories[i].name);
	}
	// Focus the form's list position on the general category, then set the form's initial focused control to the category list.
	f.set_list_position(f_category_list, 0);
	f.focus(0);
	settings_category@ last_category = @categories[0]; // A handle to the currently selected category so we can detect changes to the selection.
	// Finally this is the loop that does the rest of the magic.
	while (!f.is_pressed(f_cancel)) {
		wait(5);
		f.monitor();
		int pos = f.get_list_position(f_category_list);
		settings_category@ selected_category = null;
		if (pos &gt; -1 and pos &lt; categories.length())
			@selected_category = @categories[pos];
		if (@last_category != @selected_category) {
			last_category.f.subform_control_index = -1; // Later improvements to audio form will make this line be handled internally.
			last_category.f.focus_silently(0); // Make sure that if the category is reselected, it is focused on the first control.
			@last_category = @selected_category;
			f.set_subform(f_category_display, @selected_category.f);
			f.set_caption(f_category_display, selected_category.name + &quot; settings&quot;);
		}
		// The following is a special feature I came up with in stw which makes it so that if you are in the category list, keyboard shortcuts from the entire form will work regardless of category.
		if (f.get_current_focus() == f_category_list and key_down(KEY_LALT) or key_down(KEY_RALT)) {
			for (uint i = 0; i &lt; categories.length(); i++) {
				if (categories[i].f.check_shortcuts(true)) {
					f.set_list_position(f_category_list, i);
					@last_category = @categories[i];
					f.set_subform(f_category_display, @last_category.f);
					f.set_caption(f_category_display, last_category.name + &quot; settings&quot;);
					f.focus(f_category_display);
					break;
				}
			}
		}
		// Now we can finally check for the save button.
		if (f.is_pressed(f_ok)) {
			logostart = fc_general.is_checked(f_logostart);
			menuwrap = fc_general.is_checked(f_menuwrap);
			firespace = fc_gameplay.is_checked(f_firespace);
			radar = fc_gameplay.is_checked(f_radar);
			return;
		}
	}
}
// Lets make this thing run so we can see it work.
void main() {
	show_window(&quot;test&quot;);
	settings_dialog();
}
</code></pre>
<h5>set_text</h5>
<p>Sets the text of the control.</p>
<p><code>bool audio_form::set_text(int control_index, string new_text);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int control_index: the index of the control.</li>
<li>string new_text: the text to set.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true on success, false on failure.</p>
<h6>Remarks:</h6>
<p>This method only works on input field, slider, and status bar.</p>
<h4>Properties</h4>
<h5>active</h5>
<p>Determine if the form is currently active.</p>
<p><code>bool audio_form::active;</code></p>
<h2>Enums</h2>
<h3>audioform_errorcodes</h3>
<p>This enum contains any error values that can be returned by the <code>audio_form::get_last_error();</code> function.</p>
<ul>
<li>form_error_none: No error.</li>
<li>form_error_invalid_index: you provided a control index that doesn't exist.</li>
<li>form_error_invalid_control: you are attempting to do something on an invalid control.</li>
<li>form_error_invalid_value: You provided an invalid value.</li>
<li>form_error_invalid_operation: you tried to perform an invalid operation.</li>
<li>form_error_no_window: you haven't created an audio_form window yet.</li>
<li>form_error_window_full: the window is at its maximum number of controls</li>
<li>form_error_text_too_long: the text provided is too long.</li>
<li>form_error_list_empty: indicates that a list control is empty.</li>
<li>form_error_list_full: indicates that a list control is full.</li>
<li>form_error_invalid_list_index: the list has no item at that index.</li>
<li>form_error_control_invisible: the specified control is invisible.</li>
<li>form_error_no_controls_visible: no controls are currently visible.</li>
</ul>
<h3>control_event_type</h3>
<p>Lists all possible event types that can be raised.</p>
<ul>
<li>event_none: no event.</li>
<li>event_focus: a control gained keyboard focus.</li>
<li>event_list_cursor: the cursor changed in a list control.</li>
<li>event_text_cursor: the cursor changed in an input box.</li>
<li>event_button: a button was pressed.</li>
<li>event_checkbox: a checkbox's state has changed.</li>
<li>event_slider: a slider's value has been changed.</li>
</ul>
<h3>control_types</h3>
<p>This is a complete list of all control types available in the audio form, as well as a brief description of what they do.</p>
<ul>
<li>ct_button: a normal, pressable button.</li>
<li>ct_input: any form of text box.</li>
<li>ct_checkbox: a checkable/uncheckable control.</li>
<li>ct_progress: a progress bar that can both beep and speak.</li>
<li>ct_status_bar: a small informational area for your users to get information quickly.</li>
<li>ct_list: a list of items.</li>
<li>ct_slider: a slider, adjustable to a given percent with the arrow keys.</li>
<li>ct_form: a child form.</li>
<li>ct_keyboard_area: an area that captures all keys from the user (minus a few critical ones like tab and shift+tab) and lets you handle them, useful for embedding your game controls within your UI.</li>
</ul>
<h3>text_edit_mode_constants</h3>
<p>This is a list of constants that specify text editing modes, used mainly with <code>audio_form::edit_text();</code>.</p>
<ul>
<li>edit_mode_replace: replace text.</li>
<li>edit_mode_trim_to_length: trim the final text to a given length.</li>
<li>edit_mode_append_to_end: append text to the end.</li>
</ul>
<p>See the <code>audio_form::edit_text();</code> documentation for more information.</p>
<h3>text_entry_speech_flags</h3>
<p>This enum provides constants to be used with the character echo functionality in input boxes.</p>
<ul>
<li>textflag_none: no echo.</li>
<li>textflag_characters: echo characters only.</li>
<li>textflag_words: echo words only.</li>
<li>textflag_characters_words: echo both characters and words.</li>
</ul>
<h2>Global Properties</h2>
<h3>audioform_input_disable_ralt</h3>
<p>Set whether or not the right Alt key should be disabled in input boxes, mostly useful for users with non-english keyboards.</p>
<p><code>bool audioform_input_disable_ralt;</code></p>
<h3>audioform_keyboard_echo</h3>
<p>Set the default echo mode for all the forms. Default is <code>textflag_characters</code></p>
<p><code>int audioform_keyboard_echo;</code></p>
<h3>audioform_word_separators</h3>
<p>A list of characters that should be considered word boundaries for navigation in an input box.</p>
<p><code>string audioform_word_separators;</code></p>
