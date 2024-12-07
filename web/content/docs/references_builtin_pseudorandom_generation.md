---
title: Pseudorandom Generation
url: docs/references_builtin_pseudorandom_generation.html
---

<h1>Pseudorandom Generation</h1>
<h2>Classes</h2>
<h3>random_interface</h3>
<p>Defines the class structure that is available in NVGT's object based pseudorandom number generators. A class specifically called random_interface does not exist in the engine, but instead this reference describes methods available in multiple classes that do exist (see remarks).</p>
<ol>
<li>random_interface();</li>
<li>random_interface(uint seed);</li>
</ol>
<h4>Arguments (2):</h4>
<ul>
<li>uint seed: The number used as the seed/starting point for the RNG, passing the same seed will yield the same sequence of random numbers.</li>
</ul>
<h4>Remarks:</h4>
<p>NVGT contains several different pseudorandom number generators which can all be instantiated as many times as the programmer needs.</p>
<p>These generators all share pretty much exactly the same methods by signature and are interacted with in the same way, and so it will be documented only once here. Small topics explaining the differences for each actual generator are documented below this interface.</p>
<p>These classes all wrap a public domain single header library called <a href="https://github.com/mattiasgustavsson/libs/blob/main/rnd.h">rnd.h</a> by mattiasgustavsson on Github. The explanations for each generator as well as the following more general explanation about all of them were copied verbatim from the comments in that header, as they are able to describe the generators best and already contain links to more details.</p>
<p>The library includes four different generators: PCG, WELL, GameRand and XorShift. They all have different characteristics, and you might want to use them for different things. GameRand is very fast, but does not give a great distribution or period length. XorShift is the only one returning a 64-bit value. WELL is an improvement of the often used Mersenne Twister, and has quite a large internal state. PCG is small, fast and has a small state. If you don't have any specific reason, you may default to using PCG.</p>
<h4>Methods</h4>
<h5>next</h5>
<p>Return the next random number from the generator.</p>
<p>uint next();</p>
<h6>Returns:</h6>
<p>uint or uint64 depending on generator: The next random number (can be any supported by the integer type used).</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	random_pcg r;
	alert(&quot;info&quot;, r.next());
}
</code></pre>
<h5>nextf</h5>
<p>Return the next random floating point number from the generator.</p>
<p>float nextf();</p>
<h6>Returns:</h6>
<p>float: The next random float (between 0.0 and 1.0).</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	random_gamerand r;
	alert(&quot;info&quot;, r.nextf());
}
</code></pre>
<h5>range</h5>
<p>Return the next random number from the generator with in a minimum and maximum range.</p>
<p>int range(int min, int max);</p>
<h6>Arguments:</h6>
<ul>
<li><p>int min: The minimum number that could be generated (inclusive).</p>
</li>
<li><p>int max: The maximum number that could be generated (inclusive).</p>
</li>
</ul>
<h6>Returns:</h6>
<p>int: A random number within the given range.</p>
<h6>Remarks:</h6>
<p>This function always works using 32 bit integers regardless of the generator used.</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	random_xorshift r;
	alert(&quot;info&quot;, r.range(1, 10));
}
</code></pre>
<h5>seed</h5>
<p>Seed the random number generator with a new starting point value.</p>
<p>void seed(uint new_seed = random_seed());</p>
<p>arguments:</p>
<ul>
<li>uint new_seed = random_seed(): The seed to use (may be uint64 depending on generator, if so will default to random_seed64).</li>
</ul>
<h6>Remarks:</h6>
<p>All pseudorandom number generators typically need to start from one tiny bit of real-world randomness or obscure value to properly get going.</p>
<p>By default, nvgt's random number generators are seeded by reading 4 random bytes from the operating system using it's provided API to do so. If you call this seed() function with no arguments, the rng will be re-seeded with a new random seed.</p>
<p>However, particularly when dealing with game recordings or online play, it can be useful to take control of the random number generator and cause it to replay values. This can be done by setting the seed of an RNG to a predetermined and reused value. This is because the rng is guaranteed to return the same set of numbers for a given seed, as the seed serves as the starting point for the RNG.</p>
<p>A common method for example may be to fetch the value of the ticks() or random_seed() function yourself, store the result in a variable, and use that variable to seed an rng. If you want someone else on the network to generate the same numbers for your online game, you need only to transmit that same stored ticks() or random_seed() value over the wire and have the receiver also seed the rng to that value. Now both clients are using the same seed, and from that point they will generate random numbers that are the same, so long as of course one end of the party doesn't somehow jump the gun and generate a random number that the other end does not, as now the clients would be out of sync. This is exactly why these random_xxx classes were provided, because it may be needed to generate different random numbers on each client while insuring that some special numbers (such as enemy spawns) always remain the same. Just create multiple random_xxx instances and share the seed with one while doing whatever you want with the other.</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">	void main() {
		uint seed = random_seed();
		random_well r(seed);
		int num = r.range(1, 100);
		alert(&quot;example&quot;, &quot;the number is &quot; + num);
		r.seed(seed); // Restore our original seed from before generating the number.
		alert(&quot;The new number will still be &quot; + num, r.range(1, 100));
		r.seed(); // internally choose a random seed.
		alert(&quot;unknown number&quot;, r.range(1, 100));
}
</code></pre>
<h3>random_gamerand</h3>
<p>GameRand</p>
<p>Based on the random number generator by Ian C. Bullard:</p>
<p>http://www.redditmirror.cc/cache/websites/mjolnirstudios.com_7yjlc/mjolnirstudios.com/IanBullard/files/79ffbca75a75720f066d491e9ea935a0-10.html</p>
<p>GameRand is a random number generator based off an &quot;Image of the Day&quot; posted by Stephan Schaem. More information here:</p>
<p>http://www.flipcode.com/archives/07-15-2002.shtml</p>
<p>Look at nvgt's random_interface documentation above to learn how to use this class.</p>
<h3>random_pcg</h3>
<p>PCG - Permuted Congruential Generator</p>
<p>PCG is a family of simple fast space-efficient statistically good algorithms for random number generation. Unlike many  general-purpose RNGs, they are also hard to predict.</p>
<p>More information can be found here:</p>
<p>http://www.pcg-random.org/</p>
<p>Look at nvgt's random_interface documentation above to learn how to use this class.</p>
<h3>random_well</h3>
<p>WELL - Well Equidistributed Long-period Linear</p>
<p>Random number generation, using the WELL algorithm by F. Panneton, P. L'Ecuyer and M. Matsumoto.</p>
<p>More information in the original paper:</p>
<p>http://www.iro.umontreal.ca/~panneton/WELLRNG.html</p>
<p>This code is originally based on WELL512 C/C++ code written by Chris Lomont (published in Game Programming Gems 7) and placed in the public domain.</p>
<p>http://lomont.org/Math/Papers/2008/Lomont_PRNG_2008.pdf</p>
<p>Look at nvgt's random_interface documentation above to learn how to use this class.</p>
<h3>random_xorshift</h3>
<p>XorShift</p>
<p>A random number generator of the type LFSR (linear feedback shift registers). This specific implementation uses the XorShift+ variation, and returns 64-bit random numbers.</p>
<p>More information can be found here:</p>
<p>https://en.wikipedia.org/wiki/Xorshift</p>
<p>Look at nvgt's random_interface documentation above to learn how to use this class.</p>
<h2>Functions</h2>
<h3>random</h3>
<p>Generates a pseudorandom number given a range.</p>
<p>int random(int min, int max);</p>
<h4>Arguments:</h4>
<ul>
<li><p>int min: the minimum possible number to generate.</p>
</li>
<li><p>int max: the maximum possible number to generate.</p>
</li>
</ul>
<h4>Returns:</h4>
<p>int: a random number in the given range.</p>
<h4>Remarks:</h4>
<p>Note that this function is a pseudorandom number generator. To learn more, click <a href="https://en.wikipedia.org/wiki/Pseudorandom_number_generator">here</a>.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	alert(&quot;Example&quot;, random(1, 100));
}
</code></pre>
<h3>random_bool</h3>
<p>Generates a true or false value pseudorandomly.</p>
<p>bool random_bool(int percent = 50);</p>
<h4>Arguments:</h4>
<ul>
<li>int percent = 50: the likelihood (as a percent from 0-100) of generating a true value. Defaults to 50.</li>
</ul>
<h4>Returns:</h4>
<p>bool: either true or false.</p>
<h4>Remarks;</h4>
<p>Note that this function is a pseudorandom number generator. To learn more, click <a href="https://en.wikipedia.org/wiki/Pseudorandom_number_generator">here</a>.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	alert(&quot;Example&quot;, random_bool() ? &quot;true&quot; : &quot;false&quot;);
}
</code></pre>
<h3>random_character</h3>
<p>Generates a random ascii character.</p>
<p>string random_character(const string&amp;in min_ascii, const string&amp;in max_ascii);</p>
<h4>Arguments:</h4>
<ul>
<li><p>const string&amp;in min_ascii: the minimum possible ascii character to be generated.</p>
</li>
<li><p>const string&amp;in max_ascii: the maximum possible ascii character.</p>
</li>
</ul>
<h4>Returns:</h4>
<p>string: a random ascii character in the given range.</p>
<h4>Remarks:</h4>
<p>If you pass a string with more than one byte in it to either of the arguments in this function, only the first byte is used.</p>
<p>Note that this function uses a pseudorandom number generator. To learn more, click <a href="https://en.wikipedia.org/wiki/Pseudorandom_number_generator">here</a>.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	alert(&quot;Your random alphabetical character is&quot;, random_character(&quot;a&quot;, &quot;z&quot;));
}
</code></pre>
<h3>random_seed</h3>
<p>Returns 4 or 8 random bytes from the operating system usually used for seeding random number generators.</p>
<ol>
<li><p>uint random_seed();</p>
</li>
<li><p>uint64 random_seed64();</p>
</li>
</ol>
<h4>Returns (1):</h4>
<p>uint: A 4 byte random number.</p>
<h4>Returns (2):</h4>
<p>uint64: An 8 byte random number.</p>
<h4>Remarks:</h4>
<p>A more detailed description on seeding random number generators is in the documentation for the random_interface::seed function.</p>
<p>To retrieve the random bytes in the first place, this function uses cryptographic APIs on windows and /dev/urandom on unix.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	uint seed = random_seed();
	alert(&quot;32 bit seed&quot;, seed);
	uint64 seed64 = random_seed64();
	alert(&quot;64 bit seed&quot;, seed64);
}
</code></pre>
