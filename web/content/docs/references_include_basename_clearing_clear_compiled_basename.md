---
title: Basename Clearing (clear_compiled_basename.nvgt)
url: docs/references_include_basename_clearing_clear_compiled_basename.html
---

<h1>Basename Clearing (clear_compiled_basename.nvgt)</h1>
<h2>clear_compiled_basename.nvgt</h2>
<p>This is to solve an edge case you probably won't have to deal with. If you want to have a config.nvgt file for your project for example that defines the compiled_basename pragma, but then you include such a config script in a utility program for your project, there is no way to override the pragma from within that utility script which is not your main project application. Unfortunately pragmas in a file are evaluated before the includes, so you can't override this in a utility programs' main code file.</p>
