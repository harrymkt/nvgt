---
title: BGT Compatibility Layer (bgt_compat.nvgt)
url: docs/references_include_bgt_compatibility_layer_bgt_compat.html
---

<h1>BGT Compatibility Layer (bgt_compat.nvgt)</h1>
<h2>BGT Compatibility Layer</h2>
<p>This is an include file that attempts to make old BGT games run in NVGT with minimal modifications, mainly by remapping function names and writing a few convenience wrappers. All function signatures are exactly how they would've been in BGT unless otherwise noted.</p>
<p>Below, you'll find a list of everything this include does, as well as a reference for what each item roughly maps to in native nVGT.</p>
<h3>Key constants:</h3>
<ul>
<li>KEY_PRIOR: KEY_PAGEUP.</li>
<li>KEY_NEXT: KEY_PAGEDOWN.</li>
<li>KEY_LCONTROL: KEY_LCTRL.</li>
<li>KEY_RCONTROL: KEY_RCTRL.</li>
<li>KEY_LWIN: KEY_LGUI.</li>
<li>KEY_RWIN: KEY_RGUI.</li>
<li>KEY_LMENU: KEY_LALT.</li>
<li>KEY_RMENU: KEY_RALT.</li>
<li>KEY_LBRACKET: KEY_LEFTBRACKET.</li>
<li>KEY_RBRACKET: KEY_RIGHTBRACKET.</li>
<li>KEY_NUMPADENTER: KEY_NUMPAD_ENTER.</li>
<li>KEY_DASH: KEY_MINUS.</li>
</ul>
<h3>Math functions:</h3>
<ul>
<li>absolute: abs.</li>
<li>cosine: cos.</li>
<li>sine: sin.</li>
<li>tangent: tan.</li>
<li>arc_cosine: acos.</li>
<li>arc_sine: asin.</li>
<li>arc_tangent: atan.</li>
<li>power: pow.</li>
<li>square_root: sqrt.</li>
<li>ceiling: ceil.</li>
</ul>
<h3>Screen reader speech:</h3>
<p>Note that these functions don't map cleanly to how NVGT's API works. As such, substitutions will not be provided here. It is recommended that you use NVGT's built-in screen reader speech functions if you can, they're much more efficient, and much more powerful.</p>
<h4>Constants:</h4>
<ul>
<li>JAWS.</li>
<li>WINDOW_EYES.</li>
<li>SYSTEM_ACCESS.</li>
<li>NVDA.</li>
</ul>
<h4>Functions:</h4>
<ul>
<li>screen_reader_is_running.</li>
<li>screen_reader_speak.</li>
<li>screen_reader_speak_interrupt.</li>
<li>screen_reader_stop_speech.</li>
</ul>
<h3>String functions:</h3>
<ul>
<li>string_len: string.length.</li>
<li>string_replace: string.replace.</li>
<li>string_left: string.substr.</li>
<li>string_right: string.slice.</li>
<li>string_trim_left: string.substr.</li>
<li>string_trim_right: string.slice.</li>
<li>string_mid: string.substr.</li>
<li>string_is_lower_case: string.is_lower.</li>
<li>string_is_upper_case: string.is_upper.</li>
<li>string_is_alphabetic: string.is_alphabetic.</li>
<li>string_is_digits: string.is_digits.</li>
<li>string_is_alphanumeric: string.is_alphanumeric.</li>
<li>string_reverse: string.reverse.</li>
<li>string_to_lower_case: string.lower.</li>
<li>string_to_upper_case: string.upper.</li>
<li>string_split: string.split.</li>
<li>string_contains: string.find.</li>
<li>get_last_error_text: Superseded by exceptions.</li>
<li>string_to_number: parse_float.</li>
<li>string_compress: string_deflate.</li>
<li>string_decompress: string_inflate.</li>
</ul>
<h3>String encryption/decryption:</h3>
<p>Note that these functions don't work with existing BGT data.</p>
<ul>
<li>string_encrypt.</li>
<li>string_decrypt.</li>
</ul>
<h3>UI functions:</h3>
<ul>
<li>show_game_window: show_window.</li>
<li>is_game_window_active: is_window_active.</li>
</ul>
