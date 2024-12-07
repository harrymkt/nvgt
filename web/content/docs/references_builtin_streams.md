---
title: Streams
url: docs/references_builtin_streams.html
---

<h1>Streams</h1>
<h2>datastreams</h2>
<p>Streams, also known as datastreams, are one of the primary ways of moving around and manipulating data in nvgt. With their convenient function calls, low memory footprint when dealing with large datasets and with their ability to connect to one another to create a chain of mutations on any data, datastreams are probably the most convenient method for data manipulation in NVGT that exist.</p>
<p>A datastream could be a file on disk, a file downloading from/uploading to the internet, a simple incapsulated string, or some sort of a manipulator such as an encoder, decryptor or compression stream.</p>
<p>Datastreams can roughly be split into 3 categories, or if you want to be really specific 2.5.</p>
<ul>
<li>sources: These streams are things like file objects, internet downloads, or really anything that either inputs new data into the application or outputs data from it. Thus, they can read, write or both depending on the properties of the stream.</li>
<li>readers: These streams only support read/input operations, an example may be a decoder. Usually these attach to another stream, read data from the connected stream, and mutate that data as the stream is read from.</li>
<li>writers: The polar opposite of readers, these streams usually connect to another stream E. a file object opened in writing mode where data gets mutated (usually encoded) before being written to the connected stream.</li>
</ul>
<p>Occasionally, you may see a reader referred to as a decoder, and a writer referred to as an encoder.</p>
<p>Particularly when considering reader and writer streams that manipulate data, you can typically chain any number of streams of the same type together to cause a sequence of data mutations to be performed in one function call. For example you could connect an inflating_reader to a hex_decoder that is in turn connected to a file object in read mode. From that point, calling any of the read functions associated with the inflating stream would automatically first read from the file, hex decode it, and decompress/inflate it as needed. Inversely, you could connect a deflating_writer to a hex encoder which is connected to a file object in write mode, causing any data written to the inflating stream to be compressed, hex encoded, and finally written to the file.</p>
<p>There are a few readers and writers that, instead of manipulating data in any way as they pass through, give you details about that data. You can see counting_reader and counting_writer as examples of this, these streams count the number of lines and characters that are read or written through them.</p>
<p>Lets put this together with a little demonstration. Say you have a compressed and hex encoded file with many lines in it, and you'd like to read the file while determining the line count as the file is read. You could execute the following, for example:</p>
<pre><code>counting_reader f(inflating_reader(hex_decoder(file(&quot;test.txt&quot;, &quot;rb&quot;))));
string result;
while(f.good()) {
	result += f.read(100);
	alert(&quot;test&quot;, &quot;currently on line &quot; + f.lines + &quot; on character position &quot; + f.pos);
}
f.close();
alert(&quot;test&quot;, &quot;The file contains a total of &quot; + f.lines + &quot; and after decoding, contains the following text: \n&quot; + result);
</code></pre>
<p>More datastreams could be added to the engine at any time.</p>
<p>Note that most datastreams do not support seeking as this would result in needing to store more data in memory than we are comfortable with just as a start, however file objects and raw datastreams that read from a string do support seeking, E source streams. Other than these stream types, you should assume that seek operations will not work unless noted otherwise for each type of stream.</p>
<p>The available datastreams are listed below in this subsection of the documentation.</p>
<h2>datastream</h2>
<p>The base class for all datastreams, this stream can read and write to an internal string buffer maintained by the class if constructed directly. Any other datastream can also be cast to the &quot;datastream&quot; type to facilitate passing datastreams of any type throughout the application, and thus any child datastreams such as encoders, file sources or any others will contain the functions listed here as they are derived from the datastream class.</p>
<ol>
<li><p>datastream();</p>
</li>
<li><p>datastream(string initial_data = &quot;&quot;, string encoding = &quot;&quot;, datastream_byte_order byteorder = STREAM_BYTE_ORDER_NATIVE);</p>
</li>
</ol>
<h3>Arguments (2):</h3>
<ul>
<li><p>string initial_data = &quot;&quot;: The initial contents of this stream derived from a string.</p>
</li>
<li><p>string encoding = &quot;&quot;: The text encoding used to read or write strings to this stream (see remarks), this argument appears in all non-empty child datastream constructors.</p>
</li>
<li><p>datastream_byte_order byteorder = STREAM_BYTE_ORDER_NATIVE: The byte order to read or write binary data to this stream using (see remarks), this argument appears in all non-empty child datastream constructors.</p>
</li>
</ul>
<h3>Remarks:</h3>
<p>If this class is directly instantiated, the effect is basically that the string class gets wrapped with streaming functions. The default datastream class will create an internal string object, and any data passed into the initial_data parameter will be copied to that internal string. Then, the read/write functions on the stream will do their work on the internal string object held by the datastream class, which can be read or retrieved in full at any time. Internally, this wraps the std::stringstream class in c++.</p>
<p>It must be noted, however, that this is the parent class for all other datastreams in nvgt. This means that any child datastream such as the file class can be cast to a generic datastream handle. In this case, the read/write functions for the casted handle will perform the function of the child stream which has been casted instead of on an internal string. This is the same for any other parent/child class relationship in programming, but it was mentioned here to avoid any confusion between the default datastream implementation and a datastream handle casted from a different stream.</p>
<p>The encoding argument, present in nearly all child datastream  constructors, controls what encoding if any strings should be converted to from UTF8 as they are written to the stream with the write_string() function or &lt;&lt; operator while the binary property on the stream is set to true, as well as what encoding to convert from when reading them with read_string() or the &gt;&gt; operator. If set to an empty string (the default), strings are left in UTF8 when writing, and already expected to be in UTF8 in a stream when reading from it.</p>
<p>The byteorder argument, again present in nearly all child datastream constructors, controls what endianness is used when reading/writing binary data from/to a stream, that is the read_int/write_float/similar functions when the binary property on the stream is set to true. When a value takes more than one byte, the endianness or byte order controls whether the bytes of that value are read/written from left to right or right to left, or in proper terms whether the most significant byte of the value should be written first. The values that can be accepted here are:</p>
<ul>
<li><p>STREAM_BYTE_ORDER_NATIVE (default): The byte order used by the system the script is running on.</p>
</li>
<li><p>STREAM_BYTE_ORDER_BIG_ENDIAN: The most significant byte is read/written first.</p>
</li>
<li><p>STREAM_BYTE_ORDER_NETWORK: Same as STREAM_BYTE_ORDER_BIG_ENDIAN, provided because this is indeed a very common name for the big endian byte order as it is typically used for data transmission.</p>
</li>
<li><p>STREAM_BYTE_ORDER_LITTLE_ENDIAN: The most significant byte is read/written last.</p>
</li>
</ul>
<p>Usually, you can leave the byteorder value at the default for most streams. However in some situations where you are transmitting binary data between systems running on different architectures, it may be better to set the transmitting and receiving streams of such an application to a common byte order that is not system native.</p>
<p>Though this was mentioned above, it's worth reiterating once more that all other stream types contain all of the functions listed in this base datastream class unless otherwise noted, and thus are not documented multiple times in child classes.</p>
<p>If an initial_data argument is provided when constructing a datastream, the stream will be set at the beginning, ready to read the initial data rather than at the end. If you wish to append more data to the datastream after it is constructed, you should call the seek_end() method on it first.</p>
<h3>Example:</h3>
<pre><code class="language-NVGT">void main() {
	datastream ds1(&quot;This is a demonstration.&quot;);
	alert(&quot;example&quot;, ds1.read()); // Will display &quot;This is a demonstration.&quot;
	datastream ds2;
	ds2.write(&quot;Hello there, &quot;);
	ds2.write(&quot;good bye.&quot;);
	ds2.seek(0);
	alert(&quot;example&quot;, ds2.read()); // Will display &quot;Hello there, good bye.&quot;
	// The following shows how this datastream can be used as an area to store encoded data.
	datastream encoded;
	hex_encoder h(encoded); // We attach the encoded datastream to a hex encoder.
	h.write(&quot;I am a hex string&quot;); // &quot;I am a hex string&quot; in hex is written to the datastream object called encoded.
	h.close();
	encoded.seek(0);
	alert(&quot;example&quot;, hex_decoder(encoded).read()); // We attach a hex_decoder to the encoded datastream and read from it, thus this will display &quot;I am a hex string&quot;.
}
</code></pre>
<h3>Methods</h3>
<h4>close</h4>
<p>Close a datastream, freeing any associated resources and leaving the datastream in an inactive state.</p>
<p>bool close(bool close_connected = false);</p>
<h5>arguments:</h5>
<ul>
<li>bool close_connected = false: Whether to also close any streams that are connected to this one (see remarks).</li>
</ul>
<h5>Returns:</h5>
<p>bool: true on success, false on failure such as if the stream is already closed.</p>
<h5>Remarks:</h5>
<p>Generally it is best to call this function when you are done working with any stream, particularly when dealing with files, encoders, or any stream that is opened in write mode. In reality there are a few streams, such as the default datastream class, where it is OK to not call the close method.</p>
<p>The reason that it is sometimes OK to not call the close function on a stream when you are done with it is because this function is automatically called in the internal destructor for any datastream, meaning when any datastream object is destroyed, it's close method will be called. For some streams like the default datastream class which is just wrapping a string, this is fine (you don't close a string, after all), but in many cases you will want to close a stream at a certain time before it is destroyed. For example closing an encoding stream may write a few final characters to a connected file stream as it is closing, meaning that the close method on the encoder must be called prior to the close function on the stream connected to it, something which you may not have control of when objects are getting destructed.</p>
<p>The close_connected argument controls whether to also close any streams that are connected to the stream that close is being called on. For the default datastream class that wraps a string or for any other datastream that doesn't connect to another one, this argument has no effect.</p>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	datastream ds;
	ds.close();
	alert(&quot;example&quot;, ds.active); // Will display false, as the stream is no longer active.
	alert(&quot;example&quot;, ds.write(&quot;this is a test&quot;)); // Will return 0 instead of a positive number of bytes written as the stream is not opened.
	ds.open();
	alert(&quot;example&quot;, ds.write(&quot;this is a test&quot;)); // Now returns 14, as expected.
	// Calling the close method a final time is not required for this example because it uses an instance of the default datastream class. It will be taken care of when the script exits.
}
</code></pre>
<h4>close_all</h4>
<p>Close a datastream as well as any that are connected to it.</p>
<p>bool close_all();</p>
<h5>Returns:</h5>
<p>bool: true if the stream and any connected to it could be closed, false otherwise.</p>
<h5>Remarks:</h5>
<p>This is exactly the same thing as calling the close method with the close_connected boolean argument set to true. On the default datastream class it will have no effect besides freeing the internal string, however you can look at the example below to see a case where there is an effect by calling close_all().</p>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	datastream ds;
	hex_encoder h(ds);
	h.write(&quot;hi&quot;);
	h.close_all(); // Will also close the datastream called ds because it is connected to the hex encoder.
	alert(&quot;example&quot;, ds.active); // Will display false, indicating that calling h.close_all() also caused ds.close() to implicitly be called.
}
</code></pre>
<h4>open</h4>
<p>Open a datastream, connecting it to a source or another stream depending on type.</p>
<p>bool open(...);</p>
<h5>Arguments:</h5>
<p>Same as in the constructor for the datastream you wish to open (see remarks).</p>
<h5>Returns:</h5>
<p>bool: Returns true if the stream could be opened, false otherwise.</p>
<h5>Remarks:</h5>
<p>Most datastreams can be closed and then reopened, or can be created in an uninitialized state meaning they must be opened to begin with.</p>
<p>All datastreams can be constructed in an already initialized/opened state, and the constructors that allow this for each stream will contain the exact same arguments as that streams associated open() function, and each streams constructor topics is where such arguments are documented.</p>
<p>For example, the true signature for the open function on the default datastream class is bool open(string initial_data = &quot;&quot;, string encoding = &quot;&quot;, datastream_byteorder byteorder = STREAM_BYTE_ORDER_NATIVE) while the signature of the open function for the file datastream is bool open(string filename, string mode, string encoding = &quot;&quot;, datastream_byte_order byteorder = STREAM_BYTE_ORDER_NATIVE).</p>
<p>As mentioned in the top level datastreams topic, the encoding and byteorder arguments are present in each stream and thus will not be redocumented for each one.</p>
<p>For all streams, this function will call the associated close() function prior to opening the requested resource if the stream is already active at this time. If it turns out that users do not desire this behaviour, it may be made optional or could get removed in the future.</p>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	datastream ds;
	if (!ds.open(&quot;this is a demonstration&quot;)) {
		alert(&quot;Oh no&quot;, &quot;Maybe this could happen for a file but it should never happen for a basic datastream!&quot;);
		exit();
	}
	alert(&quot;example&quot;, ds.read()); // Will display &quot;this is a demonstration&quot;.
}
</code></pre>
<h4>read</h4>
<p>Read raw bytes from a stream.</p>
<p>string read(uint amount = 0);</p>
<h5>Arguments:</h5>
<ul>
<li>uint amount = 0: The number of bytes to read, or 0 to read the entire stream.</li>
</ul>
<h5>Returns:</h5>
<p>string: The data that was read from the stream or an empty string on failure.</p>
<h5>Remarks:</h5>
<p>If the length of the string returned by this function is less than the number of bytes requested in the amount argument, either the end of the stream was reached or there was an error. You can check what happened by evaluating the fail or eof properties on the stream.</p>
<p>This is the lowest level method of reading from a stream. All other reading functions either read a certain datatype or come with some condition, for example this should not be confused with the read_string function which does not take a byte amount argument, but which instead either reads a binary number denoting the length of a string before reading that number of bytes or reads a single word from the stream based on the state of the stream's binary flag. If you want direct control over the read operation, use this function.</p>
<p>Typically it is only useful to call this function if the good property on the stream is true, therefor you can query the stream's good property in a loop to see if you should continue reading data if you are trying to perform some sort of buffered reading of a stream.</p>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	datastream ds(&quot;Hello there, I am a string wrapped in a sstream!&quot;);
	alert(&quot;example&quot;, ds.read(6)); // Will display Hello followed by a space.
	alert(&quot;example&quot;, ds.read()); // Will display there, I am a string wrapped in a sstream!
}
</code></pre>
<h4>write</h4>
<p>Write raw bytes to a stream.</p>
<p>uint write(string content);</p>
<h5>Arguments:</h5>
<ul>
<li>string content: the content that is to be written.</li>
</ul>
<h5>Returns:</h5>
<p>uint: the number of bytes written.</p>
<h5>Remarks:</h5>
<p>If needed, you can use the returned value to verify whether the data you intended to write to the stream was written successfully by checking whether the return value of this function matches the length of the data you passed to it.</p>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	// This time we'll use a file which is another type of datastream to show how the functions in this datastream class work on it's children.
	file f(&quot;test.txt&quot;, &quot;wb&quot;);
	string data = &quot;This is a test file&quot;;
	bool success = f.write(data) == data.length();
	f.close();
	alert(&quot;Information&quot;, &quot;The file with the data has been &quot; + (success? &quot;successfully&quot; : &quot;unsuccessfully&quot;) + &quot; written&quot;);
}
</code></pre>
<h3>Properties</h3>
<h4>active</h4>
<p>This property will be true if a stream is opened and ready for use, false otherwise.</p>
<p><code>const bool active;</code></p>
<h4>available</h4>
<p>This property returns the number of bytes immediately available to be read from a stream.</p>
<p>const int available;</p>
<h5>Remarks:</h5>
<p>This property may not be implemented in all streams, for example decoders. If it is unavailable, it will return 0.</p>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	datastream ds(&quot;example&quot;);
	alert(&quot;example&quot;, ds.available); // Displays 7.
	ds.read(2);
	alert(&quot;example&quot;, ds.available); // Now shows 5, as 2 of the 7 bytes have been read.
}
</code></pre>
<h4>eof</h4>
<p>This property will be true on a stream when it has no more data to read.</p>
<p>const bool eof;</p>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	datastream ds(&quot;hello&quot;);
	alert(&quot;example&quot;, ds.eof); // Will show false because we always start at the beginning of a default datastream, thus there is data to read.
	ds.read();
	alert(&quot;example&quot;, ds.eof); // Will now show true because any further .read calls will fail as we have reached the end of the stream.
	ds.seek(3);
	alert(&quot;example&quot;, ds.eof); // Will again show false because we are no longer at the end of the stream.
}
</code></pre>
<h4>good</h4>
<p>This property will be true when a datastream is ready to read or write, such as when the active property is true and the end of file has not been reached.</p>
<p>const bool good;</p>
<h5>Remarks:</h5>
<p>This property is specifically true so long as the stream is opened and the eof, fail, and bad properties all return false.</p>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	datastream ds(&quot;hello&quot;);
	alert(&quot;example&quot;, ds.good); // Will display true because there is data to read.
	ds.read();
	alert(&quot;example&quot;, ds.good); // Will now display false because the end of file has been reached, ds.eof is true now.
}
</code></pre>
<h2>file</h2>
<p>The file datastream is used to read and write files stored on the hard disk.</p>
<ol>
<li><code>file();</code></li>
<li><code>file(const string path, const string mode);</code></li>
</ol>
<h3>Arguments (1):</h3>
<ul>
<li>const string path: the filename to open.</li>
</ul>
<h3>Arguments (2):</h3>
<ul>
<li>const string path: the filename to open.</li>
<li>const string mode: the mode to open as.</li>
</ul>
<h3>Remarks:</h3>
<p>Usually when the file object is first created, it will not be active, that is, it will not be associated with a file on disk. To activate it, use the following methods:</p>
<ul>
<li>Call the open function.</li>
<li>use the second constructor.</li>
</ul>
<p>Please note that both methods require the filename that is to be associated and the mode to open, with the only difference being that it is harder to tell whether the file was opened successfully if you use the constructor rather than the open method. Using the second constructor makes it 1 line shorter. The possible open modes will not be documented in this remarks, you can see it in <code>file::open</code> method.</p>
<p>Remember that as with all datastreams, all methods in the base datastream class will work on the file class unless noted otherwise and thus will not be redocumented here.</p>
<h3>Methods</h3>
<h4>open</h4>
<p>This method will open a file for reading or writing.</p>
<p>bool file::open(string filename, string open_mode);</p>
<h5>Arguments:</h5>
<ul>
<li><p>string filename: the name of the file to open. This can be either an absolute or relative path.</p>
</li>
<li><p>string open_mode: the mode to open, see remarks.</p>
</li>
</ul>
<h5>Returns:</h5>
<p>bool: true on success, false on failure.</p>
<h5>Remarks:</h5>
<p>While on some operating systems (mostly windows) both the slash(<code>/</code>), and the backslash(<code>\</code>) can be used to specify the filename, it is very strongly recommended to use the / character for greatest cross platform compatibility.</p>
<p>The following is a list of valid open modes.</p>
<ul>
<li><p>a: append.</p>
</li>
<li><p>w: write.</p>
</li>
<li><p>r: read.</p>
</li>
<li><p>r+: read and write.</p>
</li>
</ul>
<p>For backwards compatibility with code that used a version of the file object from when there was a difference between text and binary file open modes, a b character is also accepted (for example rb) to indicate binary. The current stream implementation ignores this character other than to gracefully accept it rather than complaining that it is an invalid mode. You can use other text encoding APIs such as string_recode and the line_converting_reader if you really need to try recreating something similar to the old behavior.</p>
<p>The file will be created if the file does not exist if opened in either write or append mode. When opened in read mode, the file must exist in order to be successful.</p>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	file f;
	f.open(&quot;test.txt&quot;, &quot;wb&quot;);
	f.write(&quot;This is a test&quot;);
	f.close();
	alert(&quot;Information&quot;, &quot;The file has been written&quot;);
}
</code></pre>
<h3>Properties</h3>
<h4>size</h4>
<p>Determine the size (in bytes) of the file that is currently associated with this stream.</p>
<p>const uint64 size;</p>
<h5>Remarks:</h5>
<p>This property will be 0 if no file is associated with this stream, in which case you can use the datastream::active property on it to check the difference between a 0 byte file and an eronious result.</p>
<p>When files are opened in write mode, there could be periods where the written data has not yet been flushed to disk in which case this property may have a value which is a little bit behind. Experiments seem to indicate that this rarely if never happens, however it's worth putting the note here just encase anyone runs into it.</p>
<p>Note that a file_get_size() function exists in the engine which is usually better than this property unless you need to do more with a file than just get it's size.</p>
<h5>Example:</h5>
<pre><code class="language-NVGT">void main() {
	file f(&quot;size.nvgt&quot;, &quot;rb&quot;);
	if (!f.active) {
		alert(&quot;oops&quot;, &quot;couldn't load the file&quot;);
		return;
	}
	alert(&quot;size.nvgt is&quot;, f.size + &quot;b&quot;);
	f.close();
}
</code></pre>
