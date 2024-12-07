---
title: User Data Storage and Retrieval (settings.nvgt)
url: docs/references_include_user_data_storage_and_retrieval_settings.html
---

<h1>User Data Storage and Retrieval (settings.nvgt)</h1>
<h2>Classes</h2>
<h3>settings</h3>
<p>This class is designed to save and load data from files in various formats, specified by the company and product.</p>
<p><code>settings();</code></p>
<h4>Remarks:</h4>
<p>When this object is first constructed, it will not be active. To activate it you must call the <code>setup</code> method, specifying the company name, product name, and optionally the format you wish to use. Please see the setup method documentation for more information and a list of supported formats.</p>
<h4>Methods</h4>
<h5>setup</h5>
<p>This method will setup your company and/or product, and thus the object will be activated, allowing you to interact with the data of the product.</p>
<p><code>bool settings::setup(const string company, const string product, const bool local_path, const string format = &quot;ini&quot;);</code></p>
<h6>Arguments:</h6>
<ul>
<li>const string company: the name of your company. This is the main folder for all your products related to this company.</li>
<li>const string product: the name of your product. This will be the subfolder under the company.</li>
<li>const bool local_path: toggles whether the data should be saved in the path where the script is being executed, or in the appdata.</li>
<li>const string format = &quot;ini&quot;: the format you wish to use, see remarks.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true on success, false on failure.</p>
<h6>Remarks:</h6>
<p>The following is a list of supported formats:</p>
<ul>
<li><code>ini</code>: default format (.ini).</li>
<li><code>json</code>: JSON format (.json).</li>
<li><code>nvgt</code>: this format will use built-in dictionary (.dat).</li>
</ul>
<p>Note that it does not currently allow you to modify the extentions, for instance, .savedata, .sd, etc. In the future it might be possible and will be documented as soon as it gets implemented.</p>
<h5>close</h5>
<p>This method closes the settings object and therefore the object will be deactivated. From then on you will no longer be able to interact with the data of the company and/or products anymore unless you resetup with <code>settings::setup</code> method.</p>
<p><code>bool settings::close(bool save_data = true);</code></p>
<h6>Arguments:</h6>
<ul>
<li>bool save_data = true: toggles whether the data should be saved before closing.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true on success, false on failure.</p>
<h5>dump</h5>
<p>This method will manually save the data.</p>
<p><code>bool settings::dump();</code></p>
<h6>Returns:</h6>
<p>bool: true on success, false on failure.</p>
<h6>Remarks:</h6>
<p>Especially if you have the <code>instant_save</code> property set to false, you need to call this function to save the data manually. Alternatively, the data will be saved if you close the object with <code>settings::close</code> method and set the <code>save_data</code> parameter to true, which is default.</p>
<h5>exists</h5>
<p>Determines whether the key exists in the data.</p>
<p><code>bool settings::exists(const string&amp;in key);</code></p>
<h6>Arguments:</h6>
<ul>
<li>const string&amp;in key: the key to look for.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the key exists, false otherwise.</p>
<h5>has_other_products</h5>
<p>Determines whether this company has other products (i.e it has more than 1 products).</p>
<p><code>bool settings::has_other_products();</code></p>
<h6>Returns:</h6>
<p>bool: true if the company has more than 1 products, false on failure.</p>
<h5>read_number</h5>
<p>Reads the data by a given key, number as value.</p>
<p><code>double settings::read_number(const string&amp;in key, double default_value = 0);</code></p>
<h6>Arguments:</h6>
<ul>
<li>const string&amp;in key: the key to look for.</li>
<li>double default_value = 0: the value to return if the key could not be retrieved.</li>
</ul>
<h6>Returns:</h6>
<p>double: the data of the key or default value if the key could not be retrieved.</p>
<h5>read_string</h5>
<p>Reads the data by a given key.</p>
<p><code>string settings::read_string(const string&amp;in key, const string&amp;in default_value = &quot;&quot;);</code></p>
<h6>Arguments:</h6>
<ul>
<li>const string&amp;in key: the key to look for.</li>
<li>const string&amp;in default_value = &quot;&quot;: the value to return if the key could not be retrieved.</li>
</ul>
<h6>Returns:</h6>
<p>string: the data of the key or default value if the key could not be retrieved.</p>
<h5>remove_product</h5>
<p>This method removes the current product.</p>
<p><code>bool settings::remove_product();</code></p>
<h6>Returns:</h6>
<p>bool: true on success, false on failure</p>
<h6>Remarks:</h6>
<p>This method will delete the directory of the current product if there are other products in the company. Otherwise, the company directory will be deleted.</p>
<h5>remove_value</h5>
<p>This method removes the key from the data.</p>
<p><code>bool settings::remove_value(const string&amp;in value_name);</code></p>
<h6>Arguments:</h6>
<ul>
<li>const string&amp;in value_name: the key to remove.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true on success, false on failure</p>
<h5>write_number</h5>
<p>this method writes into the data by a given key, number as value.</p>
<p><code>bool settings::write_number(const string&amp;in key, double number);</code></p>
<h6>Arguments:</h6>
<ul>
<li>const string&amp;in key: the key to write to.</li>
<li>double number: the number to write.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true on success, false on failure</p>
<h5>write_string</h5>
<p>this method writes into the data by a given key.</p>
<p><code>bool settings::write_string(const string&amp;in key, const string&amp;in value);</code></p>
<h6>Arguments:</h6>
<ul>
<li>const string&amp;in key: the key to write to.</li>
<li>const string&amp;in value: the value to write.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true on success, false on failure</p>
<h4>Properties</h4>
<h5>active</h5>
<p>Returns true if the settings object is active (i.e it is possible to use). You cannot use the settings object if this property is false.</p>
<p><code>bool settings::active;</code></p>
<h5>company_name</h5>
<p>The name of your company. This will be the main folder to save all products related to this company.</p>
<p><code>string settings::company_name;</code></p>
<h5>encryption_key</h5>
<p>The key to use if you want the data to be encrypted. By default, no encryption key is specified.</p>
<p><code>string settings::encryption_key;</code></p>
<h5>instant_save</h5>
<p>Toggles whether the data file should be automatically saved as soon as you add the data. true is default option. Turning this off will have to be saved manually using <code>settings::dump</code> method.</p>
<p><code>bool settings::instant_save;</code></p>
<h5>local_path</h5>
<p>Toggles whether the data should be saved in the path where the script is being executed, or in the appdata. false is default.</p>
<p><code>bool settings::local_path;</code></p>
<h5>product</h5>
<p>The name of your product.</p>
<p><code>string settings::product;</code></p>
