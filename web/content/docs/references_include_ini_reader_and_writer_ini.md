---
title: INI Reader and Writer (ini.nvgt)
url: docs/references_include_ini_reader_and_writer_ini.html
---

<h1>INI Reader and Writer (ini.nvgt)</h1>
<h2>INI Reader and Writer</h2>
<p>This is a class designed to read and write INI configuration files.</p>
<p>I can't promise that the specification will end up being followed to the letter, but I'll try. At this time, though the order of keys and sections will remain the same, the whitespace, comment, and line structure of an externally created ini file may not remain in tact if that file is updated and rewritten using this include.</p>
<h2>classes</h2>
<h3>ini</h3>
<p>This constructor just takes an optional filename so you can load an INI file directly on object creation if you want. Note though that doing it this way makes it more difficult to instantly tell if there was a problem do to the lack of a return value, so you must then evaluate ini::get_error_line() == 0 to verify a successful load.</p>
<p><code>ini(string filename = &quot;&quot;);</code></p>
<h4>Arguments:</h4>
<ul>
<li>string filename = &quot;&quot;: an optional filename to load on object creation.</li>
</ul>
<h4>methods</h4>
<h5>clear_section</h5>
<p>Deletes all keys from the given section without deleting the section itself.</p>
<p><code>bool ini::clear_section(string section);</code></p>
<h6>Arguments:</h6>
<ul>
<li>string section: the name of the section to clear.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the section was successfully cleared, false if it doesn't exist.</p>
<h5>create_section</h5>
<p>Creates a new INI section with the given name.</p>
<p><code>bool ini::create_section(string section_name);</code></p>
<h6>Arguments:</h6>
<ul>
<li>string section_name: the name of the section to create.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the section was successfully created, false otherwise.</p>
<h5>delete_key</h5>
<p>Delete a key from a given section.</p>
<p><code>bool ini::delete_key(string section, string key);</code></p>
<h6>Arguments:</h6>
<ul>
<li>string section: the name of the section the key is stored in (if any).</li>
<li>string key: the name of the key to delete.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the key was successfully deleted, false and sets an error if the key you want to delete doesn't exist or if the key name is invalid.</p>
<h5>delete_section</h5>
<p>Delete the given section.</p>
<p><code>bool ini::delete_section(string section);</code></p>
<h6>Arguments:</h6>
<ul>
<li>string section: the name of the section to delete (set this argument to a blank string to delete all sectionless keys).</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the section was successfully deleted, false otherwise.</p>
<h5>dump</h5>
<p>Dump all loaded data into a string, such as what's used by the save function, or so that you can encrypt it, pack it or such things.</p>
<p><code>string ini::dump(bool indent = false);</code></p>
<h6>Arguments:</h6>
<ul>
<li>bool indent = false:  If this is set to true, all keys in every named section will be proceeded with a tab character in the final output.</li>
</ul>
<h6>Returns:</h6>
<p>string: the entire INI data as a string.</p>
<h5>get_bool</h5>
<p>Fetch a boolean value from the INI data given a section and key.</p>
<p><code>bool ini::get_bool(string section, string key, bool default_value = false);</code></p>
<h6>Arguments:</h6>
<ul>
<li>string section: the section to get the value from (if any).</li>
<li>string key: the key of the value.</li>
<li>bool default_value = false: the default value to return if the key isn't found.</li>
</ul>
<h6>Returns:</h6>
<p>bool: the value at the particular key if found, the default value if not.</p>
<h6>Remarks:</h6>
<p>All getters will use this format, and if one returns a default value (blank string, an int that equals 0, a boolean that equals false etc), and if you want to know whether the key actually existed, use the error checking system.</p>
<h5>get_double</h5>
<p>Fetch a double from the INI data given a section and key.</p>
<p><code>double ini::get_double(string section, string key, double default_value = 0.0);</code></p>
<h6>Arguments:</h6>
<ul>
<li>string section: the section to get the value from (if any).</li>
<li>string key: the key of the value.</li>
<li>double default_value = 0.0: the default value to return if the key isn't found.</li>
</ul>
<h6>Returns:</h6>
<p>double: the value at the particular key if found, the default value if not.</p>
<h6>Remarks:</h6>
<p>All getters will use this format, and if one returns a default value (blank string, an int that equals 0, a boolean that equals false etc), and if you want to know whether the key actually existed, use the error checking system.</p>
<h5>get_error_line</h5>
<p>Return the line the last error took place on if applicable. This does not clear the error information, since one may wish to get the line number and the text which are in 2 different functions. So make sure to call this function before <code>ini::get_error_text()</code> if the line number is something you're interested in retrieving.</p>
<p><code>int ini::get_error_line();</code></p>
<h6>Returns:</h6>
<p>int: the line number of the last error, if any. A return value of -1 means that this error is not associated with a line number, and 0 means there is no error in the first place.</p>
<h5>get_error_text</h5>
<p>Returns the last error message, almost always used if an INI file fails to load and you want to know why. This function also clears the error, so to figure out the line, call <code>ini::get_error_line()</code> before calling this.</p>
<p><code>string ini::get_error_text();</code></p>
<h6>Returns:</h6>
<p>string: the last error message, if any.</p>
<h5>get_string</h5>
<p>Fetch a string from the INI data given a section and key.</p>
<p><code>string ini::get_string(string section, string key, string default_value = &quot;&quot;);</code></p>
<h6>Arguments:</h6>
<ul>
<li>string section: the section to get the value from (if any).</li>
<li>string key: the key of the value.</li>
<li>string default_value = &quot;&quot;: the default value to return if the key isn't found.</li>
</ul>
<h6>Returns:</h6>
<p>string: the value at the particular key if found, the default value if not.</p>
<h6>Remarks:</h6>
<p>All getters will use this format, and if one returns a default value (blank string, an int that equals 0, a boolean that equals false etc), and if you want to know whether the key actually existed, use the error checking system.</p>
<h5>is_empty</h5>
<p>Determine if the INI object has no data in it.</p>
<p><code>bool ini::is_empty();</code></p>
<h6>Returns:</h6>
<p>bool: true if there is no data loaded into this ini object, false otherwise.</p>
<h5>key_exists</h5>
<p>Determine if a particular key exists in the INI data.</p>
<p><code>bool ini::key_exists(string section, string key);</code></p>
<h6>Arguments:</h6>
<ul>
<li>string section: the name of the section to look for the key in.</li>
<li>string key: the name of the key.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the specified key exists, false otherwise.</p>
<h6>Remarks:</h6>
<p>An error will be accessible from the error system if the given section doesn't exist.</p>
<h5>list_keys</h5>
<p>List all key names in a given section.</p>
<p><code>string[]@ ini::list_keys(string section);</code></p>
<h6>Arguments:</h6>
<ul>
<li>string section: the section to list keys from(pass a blank string for all sectionless keys as usual).</li>
</ul>
<h6>Returns:</h6>
<p>string[]@: a handle to an array containing all the keys.  An empty array means that the section is either blank or doesn't exist, the latter being able to be checked with the error system.</p>
<h5>list_sections</h5>
<p>List all section names that exist.</p>
<p><code>string[]@ list_sections(bool include_blank_section = false);</code></p>
<h6>Arguments:</h6>
<ul>
<li>bool include_blank_section = false: Set this argument to true if you wish to include the empty element at the beginning of the list for the keys that aren't in sections, for example for automatic data collection so you don't have to insert yourself when looping through.</li>
</ul>
<h6>Returns:</h6>
<p>string[]@: a handle to an array containing all the key names.</p>
<h5>list_wildcard_sections</h5>
<p>Returns all section names containing a wildcard identifier. This way if searching through a file containing many normal sections and a few wildcard sections, it is possible to query only the wildcards for faster lookup.</p>
<p><code>string[]@ ini::list_wildcard_sections();</code></p>
<h6>Returns:</h6>
<p>string[]@: a handle to an array containing all the wildcard sections.</p>
<h5>load</h5>
<p>Load an INI file.</p>
<p><code>bool ini::load(string filename, bool robust = true);</code></p>
<h6>Arguments:</h6>
<ul>
<li>string filename: the name of the ini file to load.</li>
<li>bool robust = true: if true, a temporary backup copy of the ini data will be created before saving, and it'll be restored on error. This is slower and should only be used when necessary, but insures 0 data loss.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the ini data was successfully loaded, false otherwise.</p>
<h5>load_string</h5>
<p>This function loads INI data stored as a string, doing it this way insures that ini data can come from any source, such as an encrypted string if need be.</p>
<p><code>bool ini::load_string(string data, string filename = &quot;*&quot;);</code></p>
<h6>Arguments:</h6>
<ul>
<li>string data: the INI data to load (as a string).</li>
<li>string filename = &quot;*&quot;: the new filename to set on the INI object, if any.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the data was successfully loaded, false otherwise.</p>
<h6>Remarks:</h6>
<p>Input data is expected to have CRLF line endings.</p>
<h5>reset</h5>
<p>Resets all variables to default. You can call this yourself and it is also called by loading functions to clear data from partially successful loads upon error.</p>
<p>`void ini::reset(bool make_blank_section = true);</p>
<h6>Arguments:</h6>
<ul>
<li>bool make_blank_section = true: this argument is internal, and exists because the <code>ini::load_string()</code> function creates that section itself.</li>
</ul>
<h5>save</h5>
<p>Save everything currently loaded to a file.</p>
<p><code>bool ini::save(string filename, bool indent = false);</code></p>
<h6>Arguments:</h6>
<ul>
<li>string filename: the name of the file to write to.</li>
<li>bool indent = false:  If this is set to true, all keys in every named section will be proceeded with a tab character in the final output.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the data was successfully saved, false otherwise.</p>
<h5>save_robust</h5>
<p>This function is similar to <code>ini::save()</code>, but it first performs a temporary backup of any existing data, then restores that backup if the saving fails. This is slower and should only be used when necessary, but should insure 0 data loss.</p>
<p><code>bool ini::save_robust(string filename, bool indent = false);</code></p>
<h6>Arguments:</h6>
<ul>
<li>string filename: the name of the file to write to.</li>
<li>bool indent = false:  If this is set to true, all keys in every named section will be proceeded with a tab character in the final output.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the data was successfully saved, false otherwise.</p>
<h5>section_exists</h5>
<p>Determine if a particular section exists in the INI data.</p>
<p>bool ini::section_exists(string section);`</p>
<h6>Arguments:</h6>
<ul>
<li>string section: the name of the section to check for.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the section exists, false if not.</p>
<h5>set_bool</h5>
<p>Set a boolean value in the INI data given a section name, a key and a value.</p>
<p><code>bool ini::set_bool(string section, string key, bool value);</code></p>
<h6>Arguments:</h6>
<ul>
<li>string section: the section to put this key/value pair in (leave blank to add at the top of the file without a section).</li>
<li>string key: the name of the key.</li>
<li>bool value: the value to set.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the value was successfully written, false otherwise.</p>
<h6>Remarks:</h6>
<p>All of the other setters use this format. If the key exists already, the value, of course, will be updated.</p>
<h5>set_double</h5>
<p>Set a double in the INI data given a section name, a key and a value.</p>
<p><code>bool ini::set_double(string section, string key, double value);</code></p>
<h6>Arguments:</h6>
<ul>
<li>string section: the section to put this key/value pair in (leave blank to add at the top of the file without a section).</li>
<li>string key: the name of the key.</li>
<li>double value: the value to set.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the double was successfully written, false otherwise.</p>
<h6>Remarks:</h6>
<p>All of the other setters use this format. If the key exists already, the value, of course, will be updated.</p>
<h5>set_string</h5>
<p>Set a string in the INI data given a section name, a key and a value.</p>
<p><code>bool ini::set_string(string section, string key, string value);</code></p>
<h6>Arguments:</h6>
<ul>
<li>string section: the section to put this key/value pair in (leave blank to add at the top of the file without a section).</li>
<li>string key: the name of the key.</li>
<li>string value: the value to set.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the string was successfully written, false otherwise.</p>
<h6>Remarks:</h6>
<p>All of the other setters use this format. If the key exists already, the value, of course, will be updated.</p>
<h4>properties</h4>
<h5>loaded_filename</h5>
<p>Contains the filename of the currently loaded INI data.</p>
<p><code>string loaded_filename;</code></p>
