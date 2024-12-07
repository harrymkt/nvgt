---
title: Date and Time
url: docs/references_builtin_date_and_time.html
---

<h1>Date and Time</h1>
<h2>Classes</h2>
<h3>datetime</h3>
<p>This class stores an instance in time represented as years, months, days, hours, minutes, seconds, milliseconds and microseconds.</p>
<p>The class stores time independent of timezone, and thus uses UTC by default. You can use a calendar object in place of this one if you need to check local time, however it is faster to calculate time without needing to consider the timezone and thus any time difference calculations should be done with this object instead of calendar.</p>
<ol>
<li><code>datetime();</code></li>
<li>datetime(double julian_day);</li>
<li>datetime(int year, int month, int day, int hour = 0, int minute = 0, int second = 0, int millisecond = 0, int microsecond = 0);</li>
</ol>
<h4>Arguments (2):</h4>
<ul>
<li>double julian_day: The julian day to set the time based on.</li>
</ul>
<h4>Arguments (3):</h4>
<ul>
<li>int year: the year to set.</li>
<li>int month: the month to set.</li>
<li>int day: the day to set.</li>
<li>int hour = 0: the hour to set (from 0 to 23).</li>
<li>int minute = 0: the minute to set (from 0 to 59).</li>
<li>int second = 0: the second to set (0 to 59).</li>
<li>int millisecond = 0: the millisecond to set (0 to 999).</li>
<li>int microsecond = 0: the microsecond to set (0 to 999).</li>
</ul>
<h4>Methods</h4>
<h5>format</h5>
<p>Formats the contents of a datetime object as a string given any number of format specifiers.</p>
<p>string format(string fmt, int timezone_difference = UTC);</p>
<h6>Arguments:</h6>
<ul>
<li>string fmt: A string describing how the datetime object should be formatted (see remarks).</li>
</ul>
<h6>Returns:</h6>
<p>string: The formatted date/time.</p>
<h6>Remarks:</h6>
<p>The date time formatter in NVGT comes from the Poco C++ libraries, the below remarks other than anything directly mentioning NVGT were copied verbatim from the Poco documentation.</p>
<p>The format string is used as a template to format the date and is copied character by character except for the following special characters, which are replaced by the corresponding value.</p>
<ul>
<li><p>%w - abbreviated weekday (Mon, Tue, ...)</p>
</li>
<li><p>%W - full weekday (Monday, Tuesday, ...)</p>
</li>
<li><p>%b - abbreviated month (Jan, Feb, ...)</p>
</li>
<li><p>%B - full month (January, February, ...)</p>
</li>
<li><p>%d - zero-padded day of month (01 .. 31)</p>
</li>
<li><p>%e - day of month (1 .. 31)</p>
</li>
<li><p>%f - space-padded day of month ( 1 .. 31)</p>
</li>
<li><p>%m - zero-padded month (01 .. 12)</p>
</li>
<li><p>%n - month (1 .. 12)</p>
</li>
<li><p>%o - space-padded month ( 1 .. 12)</p>
</li>
<li><p>%y - year without century (70)</p>
</li>
<li><p>%Y - year with century (1970)</p>
</li>
<li><p>%H - hour (00 .. 23)</p>
</li>
<li><p>%h - hour (00 .. 12)</p>
</li>
<li><p>%a - am/pm</p>
</li>
<li><p>%A - AM/PM</p>
</li>
<li><p>%M - minute (00 .. 59)</p>
</li>
<li><p>%S - second (00 .. 59)</p>
</li>
<li><p>%s - seconds and microseconds (equivalent to %S.%F)</p>
</li>
<li><p>%i - millisecond (000 .. 999)</p>
</li>
<li><p>%c - centisecond (0 .. 9)</p>
</li>
<li><p>%F - fractional seconds/microseconds (000000 - 999999)</p>
</li>
<li><p>%z - time zone differential in ISO 8601 format (Z or +NN.NN)</p>
</li>
<li><p>%Z - time zone differential in RFC format (GMT or +NNNN)</p>
</li>
<li><p>%% - percent sign</p>
</li>
</ul>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	datetime dt;
	alert(&quot;example&quot;, &quot;The current date/time is &quot; + dt.format(&quot;%Y/%m/%d, %h:%M:%S %A %Z&quot;));
}
</code></pre>
<h5>reset</h5>
<p>Resets this datetime object to the current date and time.</p>
<p>void reset();</p>
<h6>Remarks:</h6>
<p>The expression d.reset() is equivalent to the expression d = datetime(); this is only a convenience function.</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	datetime d;
	d.set(2024, 3, 9, 1, 24, 49);
	alert(&quot;The datetime object is currently set to&quot;, d.year + &quot;/&quot; + d.month + &quot;/&quot; + d.day + &quot;, &quot; + d.hour + &quot;:&quot; + d.minute + &quot;:&quot; + d.second);
	d.reset();
	alert(&quot;The datetime object is now set to&quot;, d.year + &quot;/&quot; + d.month + &quot;/&quot; + d.day + &quot;, &quot; + d.hour + &quot;:&quot; + d.minute + &quot;:&quot; + d.second);
}
</code></pre>
<h5>set</h5>
<p>Set the date and time of the datetime object.</p>
<p>datetime&amp; datetime::set(int year, int month, int day, int hour = 0, int minute = 0, int second = 0, int millisecond = 0, int microsecond = 0);</p>
<h6>Arguments:</h6>
<ul>
<li><p>int year: the year to set.</p>
</li>
<li><p>int month: the month to set.</p>
</li>
<li><p>int day: the day to set.</p>
</li>
<li><p>int hour = 0: the hour to set (from 0 to 23).</p>
</li>
<li><p>int minute = 0: the minute to set (from 0 to 59).</p>
</li>
<li><p>int second = 0: the second to set (0 to 59).</p>
</li>
<li><p>int millisecond = 0: the millisecond to set (0 to 999).</p>
</li>
<li><p>int microsecond = 0: the microsecond to set (0 to 999).</p>
</li>
</ul>
<h6>Returns:</h6>
<p>datetime&amp;: A reference to the datetime object allowing for chaining calls together.</p>
<h6>Remarks:</h6>
<p>This method will throw an exception if the date or time is invalid. You can use the datetime_is_valid global function which takes similar arguments to this one and returns a boolean if you want to verify any values before passing them to this method.</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	datetime d;
	d.set(2024, 3, 9, 1, 24, 49);
	alert(&quot;The datetime object is currently set to&quot;, d.year + &quot;/&quot; + d.month + &quot;/&quot; + d.day + &quot;, &quot; + d.hour + &quot;:&quot; + d.minute + &quot;:&quot; + d.second);
}
</code></pre>
<h5>week</h5>
<p>Returns the currently set week number within the year of the datetime object.</p>
<p>int week(int first_day_of_week = 1);</p>
<h6>Arguments:</h6>
<ul>
<li>int first_day_of_week = 1: Determines whether 0 (sunday) or 1 (monday) begins the week.</li>
</ul>
<h6>Returns:</h6>
<p>int: The week number within the year (0 to 53).</p>
<h6>Remarks:</h6>
<p>The first_day_of_week argument controls whether the week counter increases by 1 upon reaching Sunday or Monday. Passing other values to this function has undefined results.</p>
<p>Week 1 of the year begins in whatever week contains January 4th.</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	datetime dt(2016, 9, 17);
	alert(&quot;example&quot;, &quot;week &quot; + dt.week()); // Will display 37.
}
</code></pre>
<h4>Operators</h4>
<h5>opAdd</h5>
<p>Return a new datetime object with a duration of time represented as a timespan added to it.
<code>datetime opAdd(const timespan&amp;in);</code></p>
<h5>opAddAssign</h5>
<p>Add a duration represented as a timespan to a datetime object.
<code>datetime&amp; opAddAssign(const timespan&amp;in);</code></p>
<h5>opCmp</h5>
<p>Compare a datetime object relationally to another one.
<code>int opCmp(const datetime&amp; other);</code></p>
<h5>opEquals</h5>
<p>Check if a datetime object is equal to another datetime object.
<code>bool opEquals(const datetime&amp; other);</code></p>
<h5>opSub</h5>
<ol>
<li>Return a new datetime object with a duration of time represented as a timespan subtracted from it.</li>
<li>Return a duration represented by a timespan by subtracting 2 datetime objects from each other.</li>
<li><code>datetime opSub(const timespan&amp;in);</code></li>
<li><code>timespan opSub(const datetime&amp;in);</code></li>
</ol>
<h5>opSubAssign</h5>
<p>Subtract a duration represented as a timespan from a datetime object.
<code>datetime&amp; opSubAssign(const timespan&amp;in);</code></p>
<h4>Properties</h4>
<h5>AM</h5>
<p>A boolean which is true if the datetime object is set to an hour before noon (ante meridiem).</p>
<p>const bool AM;</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	datetime d;
	d.set(2024, 5, 8, 14, 18);
	alert(&quot;The datetime's AM value was set to&quot;, d.AM);
}
</code></pre>
<h5>day</h5>
<p>Represents the current day of the datetime object.</p>
<p>const uint day;</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	datetime d;
	d.set(2024, 5, 8);
	alert(&quot;The datetime's set day is&quot;, d.day);
}
</code></pre>
<h5>hour</h5>
<p>Represents the current hour (from 0 to 23) of the datetime object.</p>
<p>const uint hour;</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	datetime d;
	d.set(d.year, d.month, d.day, 13, 47, 19);
	alert(&quot;The set hour of the datetime object is&quot;, d.hour);
}
</code></pre>
<h5>hour12</h5>
<p>Represents the current hour (from 0 to 12) of the datetime object.</p>
<p>const uint hour12;</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	datetime d;
	d.set(d.year, d.month, d.day, 13, 47, 19);
	alert(&quot;In 12 hour time, the set hour of the datetime object is&quot;, d.hour12);
}
</code></pre>
<h5>julian_day</h5>
<p>Represents the current timestamp held by the datetime object in julian days.</p>
<p>const double julian_day;</p>
<h6>Remarks:</h6>
<p>The <a href="http://en.wikipedia.org/wiki/Julian_day">julian day</a> measures, including decimal fractions, the amount of time that has passed (in years) since Monday, January 1st, 4713 BC at 12 PM Universal Time.</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	datetime d;
	d.set(2024, 5, 8, 16, 17, 18);
	alert(&quot;The julian day represented by this datetime object is&quot;, d.julian_day);
}
</code></pre>
<h5>microsecond</h5>
<p>Represents the current microsecond of the datetime object.</p>
<p>const uint microsecond;</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	datetime d;
	d.set(d.year, d.month, d.day, 12, 47, 19, 217, 962);
	alert(&quot;The set microsecond value of the datetime object is&quot;, d.microsecond);
}
</code></pre>
<h5>millisecond</h5>
<p>Represents the current millisecond of the datetime object.</p>
<p>const uint millisecond;</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	datetime d;
	d.set(d.year, d.month, d.day, 12, 47, 19, 217);
	alert(&quot;The set millisecond value of the datetime object is&quot;, d.millisecond);
}
</code></pre>
<h5>minute</h5>
<p>Represents the current minute of the datetime object.</p>
<p>const uint minute;</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	datetime d;
	d.set(d.year, d.month, d.day, 12, 47, 19);
	alert(&quot;The set minute of the datetime object is&quot;, d.minute);
}
</code></pre>
<h5>month</h5>
<p>Represents the current month of the datetime object.</p>
<p>const uint month;</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	datetime d;
	d.set(2024, 5, 8);
	alert(&quot;The datetime's set month is&quot;, d.month);
}
</code></pre>
<h5>PM</h5>
<p>A boolean which is true if the datetime object is set to an hour after noon (post meridiem).</p>
<p>const bool PM;</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	datetime d;
	d.set(2024, 5, 8, 14, 18);
	alert(&quot;The datetime's set PM value is&quot;, d.PM);
}
</code></pre>
<h5>second</h5>
<p>Represents the current second of the datetime object.</p>
<p>const uint second;</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	datetime d;
	d.set(d.year, d.month, d.day, 12, 47, 19);
	alert(&quot;The set second of the datetime object is&quot;, d.second);
}
</code></pre>
<h5>timestamp</h5>
<p>Represents the datetime object as a timestamp object.</p>
<p>const timestamp timestamp;</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	datetime d;
	d.set(d.year, d.month, d.day, 12, 47, 19);
	alert(&quot;The current timestamp represented by the datetime object is&quot;, d.timestamp / SECONDS);
}
</code></pre>
<h5>UTC_time</h5>
<p>Determines the UTC based time point stored in the datetime object.</p>
<p>const int64 UTC_time;</p>
<h6>Remarks:</h6>
<p>UTC based time begins on October 15, 1582 at 12 AM and uses an accuracy of 100 nanoseconds.</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	datetime dt;
	alert(&quot;example&quot;, &quot;The current UTC time value is &quot; + dt.UTC_time);
}
</code></pre>
<h5>weekday</h5>
<p>Represents the current day of the week (from 0 to 6) calculated by the datetime object.</p>
<p>const uint weekday;</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	datetime d;
	d.set(2024, 5, 8);
	alert(&quot;The datetime's set day of the week is&quot;, d.weekday);
}
</code></pre>
<h5>year</h5>
<p>Represents the current year of the datetime object.</p>
<p>const uint year;</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	datetime d;
	d.set(2024, 5, 8);
	alert(&quot;The datetime's set year is&quot;, d.year);
}
</code></pre>
<h5>yearday</h5>
<p>Represents the current day of the year calculated by the datetime object.</p>
<p>const uint yearday;</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	datetime d;
	d.set(2024, 5, 8);
	alert(&quot;The datetime's set day of the year is&quot;, d.yearday);
}
</code></pre>
<h3>timestamp</h3>
<p>Stores a unix timestamp with microsecond accuracy and provides methods for comparing them.</p>
<ol>
<li>timestamp();</li>
<li>timestamp(int64 epoch_microseconds);</li>
</ol>
<h4>Arguments 2:</h4>
<ul>
<li>int64 epoch_microseconds: the initial value of the timestamp</li>
</ul>
<h4>Remarks:</h4>
<p>If a timestamp object is initialize with the default constructor, it will be set to the system's current date and time.
The unix epoch began on January 1st, 1970 at 12 AM UTC.</p>
<h4>Methods</h4>
<h5>has_elapsed</h5>
<p>determine whether the given number of microseconds has elapsed since the time point stored in this timestamp.</p>
<p>bool has_elapsed(int64 microseconds);</p>
<h6>Arguments:</h6>
<ul>
<li>int64 microseconds: the number of microseconds to check elapsed status of</li>
</ul>
<h6>Returns:</h6>
<p>bool: Whether the given number of milliseconds has elapsed</p>
<h6>Remarks:</h6>
<p>This method serves as a shorthand version of executing <code>bool has_elapsed = timestamp() - this &gt;= microseconds;</code></p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	timestamp ts;
	alert(&quot;test&quot;, &quot;will you keep the alert box opened for 10 seconds?&quot;);
	if (ts.has_elapsed(10 * SECONDS)) alert(&quot;good job&quot;, &quot;You kept the alert box opened for 10 seconds!&quot;);
	else alert(&quot;oh no&quot;, &quot;looks like a bit of character development in regards to the trait of patience is in order...&quot;);
}
</code></pre>
<h5>update</h5>
<p>Reset this timestamp to the system's current date and time.</p>
<p>void update();</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	timestamp ts;
	ts -= 60 * SECONDS;
	alert(&quot;timestamp before reset&quot;, ts / SECONDS);
	ts.update();
	alert(&quot;current timestamp&quot;, ts / SECONDS);
}
</code></pre>
<h4>Operators</h4>
<h5>opImplConv</h5>
<p>Implicitly convert the timestamp to a 64 bit integer containing a raw microsecond accuracy unix epoch.
int64 opImplConv();</p>
<h4>Properties</h4>
<h5>elapsed</h5>
<p>Determine the difference of time in microseconds between this timestamp's value and now.</p>
<p>const int64 elapsed;</p>
<h6>Remarks:</h6>
<p>This property is a shorthand version of the expression <code>int64 elapsed = timestamp() - this;</code></p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	datetime dt(2013, 11, 29, 1, 2, 3);
	alert(&quot;example&quot;, dt.format(DATE_TIME_FORMAT_RFC850) + &quot; was &quot; + (dt.timestamp.elapsed / DAYS) + &quot; days ago&quot;);
}
</code></pre>
<h5>UTC_time</h5>
<p>Determines a UTC based time point based on the value stored in the timestamp object.</p>
<p>const int64 UTC_time;</p>
<h6>Remarks:</h6>
<p>UTC based time begins on October 15, 1582 at 12 AM and uses an accuracy of 100 nanoseconds.</p>
<h6>Example:</h6>
<pre><code class="language-NVGT">void main() {
	timestamp ts;
	alert(&quot;example&quot;, &quot;The current UTC time value is &quot; + ts.UTC_time);
}
</code></pre>
<h2>Functions</h2>
<h3>datetime_days_of_month</h3>
<p>Returns the number of days in a given month, a year is also required so that leap year can be handled correctly.</p>
<p>int datetime_days_of_month(int year, int month);</p>
<h4>Arguments:</h4>
<ul>
<li><p>int year: The year involved in this calculation due to leap year.</p>
</li>
<li><p>month: The month to fetch the number of days of (from 1 to 12).</p>
</li>
</ul>
<h4>Returns:</h4>
<p>int: The number of days in the month provided with leap year accounted for, or 0 if invalid/out of range arguments are provided.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	for(int i = 1; i &lt;= 12; i++) {
		alert(&quot;month &quot; + i + &quot; no leap year&quot;, datetime_days_of_month(2023, i));
		if (i == 2) alert(&quot;month &quot; + i + &quot; leap year&quot;, datetime_days_of_month(2024, i));
	}
	alert(&quot;invalid&quot;, datetime_days_of_month(2015, 17)); // Will show 0 (there are not 17 months in the year)!
}
</code></pre>
<h3>datetime_is_leap_year</h3>
<p>Determine whether a given year is a leap year.</p>
<p>bool datetime_is_leap_year(int year);</p>
<h4>Arguments:</h4>
<ul>
<li>int year: The year to check the leap year status of.</li>
</ul>
<h4>Returns:</h4>
<ul>
<li>bool: true if the given year is a leap year, false otherwise.</li>
</ul>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	for(int year = 2019; year &lt; 2026; year ++) {
		alert(&quot;example&quot;, year+&quot; is &quot; + (datetime_is_leap_year(year)? &quot;a leap year!&quot; : &quot;not a leap year.&quot;));
	}
}
</code></pre>
<h3>datetime_is_valid</h3>
<p>Check whether the components of a date/time are valid.</p>
<p>bool datetime_is_valid(int year, int month, int day, int hour = 0, int minute = 0, int second = 0, int millisecond = 0, int microsecond = 0);</p>
<h4>Arguments:</h4>
<ul>
<li><p>int year: the year to check.</p>
</li>
<li><p>int month: the month to check (from 1 to 12).</p>
</li>
<li><p>int day: the day to check (from 1 to 31).</p>
</li>
<li><p>int hour = 0: the hour to check (from 0 to 23).</p>
</li>
<li><p>int minute = 0: the minute to check (from 0 to 59).</p>
</li>
<li><p>int second = 0: the second to check (0 to 59).</p>
</li>
<li><p>int millisecond = 0: the millisecond to check (0 to 999).</p>
</li>
<li><p>int microsecond = 0: the microsecond to check (0 to 999).</p>
</li>
</ul>
<h4>Returns:</h4>
<p>bool: true if the given arguments make up a valid date and time, false otherwise.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	alert(&quot;example 1&quot;, datetime_is_valid(2023, 2, 29)); // Will display false (not a leap year!)
	alert(&quot;example 2&quot;, datetime_is_valid(2020, 2, 29)); // Will display true, is a leap year.
	alert(&quot;example 3&quot;, datetime_is_valid(2020, 6, 31)); // Will display false (June has 30 days).
	alert(&quot;example 4&quot;, datetime_is_valid(2020, 7, 31, 13, 71, 59)); // Will display false (invalid time values).
}
</code></pre>
<h3>parse_datetime</h3>
<p>Parse a string into a datetime object given a format specifier.</p>
<ol>
<li><p>datetime parse_datetime(string fmt, string datetime_to_parse, int&amp; timezone_difference);</p>
</li>
<li><p>datetime parse_datetime(string datetime_to_parse, int&amp; timezone_difference);</p>
</li>
</ol>
<h4>Arguments:</h4>
<ul>
<li><p>string fmt (1): The format specifier string.</p>
</li>
<li><p>string datetime_to_parse: The string containing a date/time to parse according to the given format specifier, or automatically if one is not provided.</p>
</li>
<li><p>int&amp; timezone_difference: A reference to an integer which will store any timezone offset parsed from the provided string.</p>
</li>
</ul>
<h4>Returns:</h4>
<p>datetime: A datetime object containing the parsed information.</p>
<h4>Remarks:</h4>
<p>This function may throw an exception if an invalid date/time is provided. You can use the global <code>bool datetime_is_valid_format(string str)</code> function to attempt validating user input before passing it as an argument here.</p>
<p>If you use the version of this function without a format specifier, it will try to automatically determine the format of the date/time using several available standard formats.</p>
<p>This function will clean the input string such as trimming whitespace before parsing is attempted.</p>
<p>Internally, this wraps the DateTimeParser functionality in the Poco c++ libraries. Their documentation says the following, copied verbatim, about this parsing engine, though note in NVGT DateTime:::makeUTC is called datetime.make_UTC, for example.</p>
<p>This class provides a method for parsing dates and times from strings. All parsing methods do their best to parse a meaningful result, even from malformed input strings.</p>
<p>The returned DateTime will always contain a time in the same timezone as the time in the string. Call DateTime::makeUTC() with the timeZoneDifferential returned by parse() to convert the DateTime to UTC.</p>
<p>Note: When parsing a time in 12-hour (AM/PM) format, the hour (%h) must be parsed before the AM/PM designator (%a, %A), otherwise the AM/PM designator will be ignored.</p>
<p>See the DateTimeFormatter class for a list of supported format specifiers.</p>
<p>In addition to the format specifiers supported by DateTimeFormatter, an additional specifier is supported: %r will parse a year given by either two or four digits. Years 69-00 are interpreted in the 20th century (1969-2000), years 01-68 in the 21th century (2001-2068).</p>
<p>Note that in the current implementation all characters other than format specifiers in the format string are ignored/not matched against the date/time string. This may lead to non-error results even with nonsense input strings. This may change in a future version to a more strict behavior.</p>
<p>If more strict format validation of date/time strings is required, a regular expression could be used for initial validation, before passing the string to DateTimeParser.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	int tzd;
	datetime dt = parse_datetime(&quot;2024-03-19 13:19:51&quot;, tzd);
	alert(&quot;example&quot;, &quot;the parsed time is &quot; + dt.format(&quot;%W, %B %d %Y at %H:%M:%S&quot;));
	dt = parse_datetime(&quot;%Y/%m/%d %H:%M:%S&quot;, &quot;2024/03/19 13:19:51&quot;, tzd);
	alert(&quot;example&quot;, &quot;the parsed time is &quot; + dt.format(&quot;%W, %B %d %Y at %H:%M:%S&quot;));
}
</code></pre>
<h3>timestamp_from_UTC_time</h3>
<p>Create a timestamp object from a UTC time point.</p>
<p>timestamp timestamp_from_UTC_time(int64 UTC_time);</p>
<h4>Arguments:</h4>
<ul>
<li>int64 UTC_time: The UTC time point (see remarks).</li>
</ul>
<h4>Returns:</h4>
<p>timestamp: A timestamp derived from the given value.</p>
<h4>Remarks:</h4>
<p>UTC based time begins on October 15, 1582 at 12 AM and uses an accuracy of 100 nanoseconds.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	calendar c(2017, 2, 3, 4, 5, 6);
	alert(&quot;initial calendar&quot;, c.format(DATE_TIME_FORMAT_RFC1123));
	timestamp ts = timestamp_from_UTC_time(c.UTC_time);
	calendar c2 = ts;
	alert(&quot;new calendar&quot;, c2.format(DATE_TIME_FORMAT_RFC1123));
}
</code></pre>
<h2>Global Properties</h2>
<h3>DATE_DAY</h3>
<p>Returns the number of the current day through the month.</p>
<p>const int DATE_DAY;</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	alert(&quot;example&quot;, &quot;It is day &quot; + DATE_DAY + &quot; of &quot; + DATE_MONTH_NAME);
}
</code></pre>
<h3>DATE_MONTH</h3>
<p>Returns the month set on the system, from 1 to 12.</p>
<p>const int DATE_MONTH;</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	alert(&quot;example&quot;, &quot;the month is &quot; + DATE_MONTH);
}
</code></pre>
<h3>DATE_MONTH_NAME</h3>
<p>Returns the name of the current month.</p>
<p>const string DATE_MONTH_NAME;</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	alert(&quot;example&quot;, &quot;the month is &quot; + DATE_MONTH_NAME);
}
</code></pre>
<h3>DATE_WEEKDAY</h3>
<p>Returns the number of the current day through the week.</p>
<p>const int DATE_WEEKDAY;</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	alert(&quot;example&quot;, &quot;It is day &quot; + DATE_WEEKDAY + &quot; of the week&quot;);
}
</code></pre>
<h3>DATE_WEEKDAY_NAME</h3>
<p>Returns the name of the current day.</p>
<p>const string DATE_WEEKDAY_NAME;</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	alert(&quot;example&quot;, &quot;It is &quot; + DATE_WEEKDAY_NAME + &quot; today&quot;);
}
</code></pre>
<h3>DATE_YEAR</h3>
<p>Returns the 4 digit year set on the system.</p>
<p>const int DATE_YEAR;</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	alert(&quot;example&quot;, &quot;the year is &quot; + DATE_YEAR);
}
</code></pre>
<h3>SCRIPT_BUILD_TIME</h3>
<p>Contains the timestamp when the calling nvgt program was compiled.</p>
<p>const timestamp SCRIPT_BUILD_TIME;</p>
<h4>Remarks:</h4>
<p>This property will be set to the time when NVGT launched if it is accessed by a script running from source. Otherwise, it will contain a timestamp set to when the .nvgt script was compiled into an executable.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	if (!SCRIPT_COMPILED) {
		alert(&quot;oops&quot;, &quot;This only works in compiled scripts.&quot;);
		return;
	}
	alert(&quot;Script compiled on&quot;, datetime(SCRIPT_BUILD_TIME).format(DATE_TIME_FORMAT_RFC850));
}
</code></pre>
<h3>TIME_HOUR</h3>
<p>Returns the current hour, in 24-hour format.</p>
<p>const int TIME_HOUR;</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	alert(&quot;Example&quot;, &quot;It is currently &quot; + TIME_HOUR + &quot;:00&quot;);
}
</code></pre>
<h3>TIME_MINUTE</h3>
<p>Returns the current minute.</p>
<p>const int TIME_MINUTE;</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	alert(&quot;Example&quot;, &quot;It is currently &quot; + TIME_HOUR + &quot;:&quot; + TIME_MINUTE);
}
</code></pre>
<h3>TIME_SECOND</h3>
<p>Returns the current second.</p>
<p>const int TIME_SECOND;</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	alert(&quot;Example&quot;, &quot;It is currently &quot; + TIME_HOUR + &quot;:&quot; + TIME_MINUTE + &quot;:&quot; + TIME_SECOND);
}
</code></pre>
<h3>TIME_SYSTEM_RUNNING_MILLISECONDS</h3>
<p>Represents the number of milliseconds since the system booted up.</p>
<p>uint64 TIME_SYSTEM_RUNNING_MILLISECONDS;</p>
<h4>Remarks:</h4>
<p>Note that unlike something like <code>GetTickCount()</code> from the Windows API, this value is given as an unsigned 64-bit integer, so it would take an almost impossible amount of uptime to make it overflow.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	alert(&quot;Your computer has been up for&quot;, TIME_SYSTEM_RUNNING_MILLISECONDS + &quot; MS&quot;);
}
</code></pre>
<h3>timer_default_accuracy</h3>
<p>Set or retrieve the default accuracy used for timers.</p>
<p>uint64 timer_default_accuracy = MILLISECONDS;</p>
<h4>Remarks:</h4>
<p>Internally NVGT always uses a clock with microsecond accuracy to track time, meaning that microseconds is the highest accuracy that timer objects support. However in many cases, microsecond accuracy is not desired and causes a user to need to type far too many 0s than they would desire when handling elapsed time. Therefor NVGT allows you to set a devisor/multiplier that is applied to any timer operation as it passes between NVGT and your script.</p>
<p>The accuracy represented here is just a number of microseconds to divide values returned from timer.elapsed by before returning them to your script, as well as the number of microseconds to multiply by if one uses the timer.force function.</p>
<p>If this property is changed, any timers that already exist will remain unaffected, and only newly created timers will use the updated value.</p>
<p>Some useful constants are provided to make this property more useful:</p>
<ul>
<li><p>MILLISECONDS: 1000 microseconds</p>
</li>
<li><p>SECONDS: 1000 MILLISECONDS</p>
</li>
<li><p>MINUTES: 60 SECONDS</p>
</li>
<li><p>HOURS: 60 MINUTES</p>
</li>
<li><p>DAYS: 24 HOURS.</p>
</li>
</ul>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	timer_default_accuracy = SECONDS;
	alert(&quot;example&quot;, &quot;about to wait for 1100ms&quot;);
	timer t;
	wait(1100);
	alert(&quot;example&quot;, t.elapsed); // Will show 1.
	timer_default_accuracy = 250; // You can set this to arbitrary values if you so wish.
	timer t2;
	wait(1); // or 1000 microseconds.
	alert(&quot;example&quot;, t2.elapsed); // Will display a number slightly higher than 4 as the wait call takes some extra microseconds to return.
}
</code></pre>
<h3>TIMEZONE_BASE_OFFSET</h3>
<p>Determine the system's timezone offset from UTC in seconds, excluding any daylight saving time alterations.</p>
<p>const int TIMEZONE_BASE_OFFSET;</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	alert(TIMEZONE_NAME, &quot;base offset is &quot; + TIMEZONE_BASE_OFFSET);
}
</code></pre>
<h3>TIMEZONE_DST_NAME</h3>
<p>Retrieve the name of the timezone currently set on the system that is displayed when daylight saving time is in effect.</p>
<p>const string TIMEZONE_STANDARD_NAME;</p>
<h4>Remarks:</h4>
<p>This will always return the version of the timezone name that is shown when daylight saving time is active, even if daylight saving time is not actually in effect.</p>
<p>If the current timezone does not use daylight saving time, the value of this property is somewhat undefined but is most likely to equal TIMEZONE_STANDARD_NAME. The undefined value condition is a result of directly querying the operating system's API for this information, different platforms might react in slightly different ways to the absants of daylight savings support in a timezone.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	alert(&quot;timezone example&quot;, &quot;Currently in &quot; + TIMEZONE_NAME + &quot;, which is usually called &quot; + TIMEZONE_STANDARD_NAME + &quot; though it is known as &quot; + TIMEZONE_DST_NAME + &quot;when daylight saving time is in effect.&quot;);
}
</code></pre>
<h3>TIMEZONE_DST_OFFSET</h3>
<p>Determine the DST alteration offset in seconds if daylight saving time is active in the system's current timezone.</p>
<p>const int TIMEZONE_DST_OFFSET;</p>
<h4>Remarks:</h4>
<p>If daylight saving time usually moves the clock an hour forward in your timezone when it is active, for example, this value will return 3600.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	timespan t(TIMEZONE_DST_OFFSET, 0);
	alert(TIMEZONE_NAME, &quot;The clock is being altered by &quot; + t.hours + &quot; hours, &quot; + t.minutes + &quot; minutes, and &quot; + t.seconds + &quot; seconds due to daylight saving time.&quot;);
}
</code></pre>
<h3>TIMEZONE_NAME</h3>
<p>Retrieve the name of the timezone currently set on the system.</p>
<p>const string TIMEZONE_NAME;</p>
<h4>Remarks:</h4>
<p>This contains the value of either TIMEZONE_STANDARD_NAME or TIMEZONE_DST_NAME, depending on whether daylight saving time is currently in effect. If the timezone does not support daylight saving time, this always yields TIMEZONE_STANDARD_NAME.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	alert(&quot;timezone example&quot;, &quot;Currently in &quot; + TIMEZONE_NAME + &quot;, which is usually called &quot; + TIMEZONE_STANDARD_NAME + &quot; though it is known as &quot; + TIMEZONE_DST_NAME + &quot;when daylight saving time is in effect.&quot;);
}
</code></pre>
<h3>TIMEZONE_OFFSET</h3>
<p>Determine the system's current timezone offset from UTC in seconds.</p>
<p>const int TIMEZONE_OFFSET;</p>
<h4>Remarks:</h4>
<p>This is also the sum of TIMEZONE_BASE_OFFSET + TIMEZONE_DST_OFFSET, provided for convenience.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	alert(TIMEZONE_NAME, &quot;offset from UTC: &quot; + timespan(TIMEZONE_OFFSET, 0).format());
}
</code></pre>
<h3>TIMEZONE_STANDARD_NAME</h3>
<p>Retrieve the name of the timezone currently set on the system that is displayed when daylight saving time is not in effect.</p>
<p>const string TIMEZONE_STANDARD_NAME;</p>
<h4>Remarks:</h4>
<p>This will always return the version of the timezone name that is shown when daylight saving time is not active, even if daylight saving time is truly in effect.</p>
<h4>Example:</h4>
<pre><code class="language-NVGT">void main() {
	alert(&quot;timezone example&quot;, &quot;Currently in &quot; + TIMEZONE_NAME + &quot;, which is usually called &quot; + TIMEZONE_STANDARD_NAME + &quot; though it is known as &quot; + TIMEZONE_DST_NAME + &quot;when daylight saving time is in effect.&quot;);
}
</code></pre>
