# vscode-arcadia

### Getting Started
To try it out, clone the repo somewhere & open the 
root folder in VSCode.  Run the extension in an 
Extension Development Host by pressing `F5`, or 
clicking `Debug` > `Start`.  This runs the compiled
extension.js file in the root folder.

Ensure Unity is up & an Arcadia project is loaded.
Then `⌘-shift-p` and run `Arcadia: REPL - Start`.

Once the REPL is active, you can 
- `Arcadia: REPL - Send Line` (`ctrl+, l`)
- `Arcadia: REPL - Send Selection` (`ctrl+, s`) or
- `Arcadia: REPL - Send File` (`ctrl+, f`) 
to send the current line, selection or file to the
REPL respectively.

> There's a bug with sending a selection encompassing 
multiple forms - only the first form is actually 
evaluated. Probably need to chunk input on newlines
and send as separate messages.

There is currently no in-REPL editing available, but 
you can open an empty file & use it as a scratch buffer.
The REPL doesn't care what syntax the file is set to, 
but you would need to set it Clojure to get syntax 
highlighting obviously.

### Development 
To make changes or just build fresh from source,
run `lein cljsbuild once` (or `auto` for continuous
compilation);

> NOTE: it took some fiddling to get a ClojureScript
working in a VSCode extension.
>
>I mostly followed the non-Figwheel parts of 
[this](https://github.com/bhauman/lein-figwheel/wiki/Node.js-development-with-figwheel),
but I found that the Google Closure library didn't load 
properly (specifically, provided namespaces got attached 
to `goog.global` but not attached to the global `goog` var).
>
>The trick to get it working was `:optimizations :simple` 
combined with `:output-wrapper true`. The other requirements 
are specifying `:main` and calling `(set! *main-cli-fn* -main)` 
from that namespace as documented on the ClojureScript 
NodeJS wiki page.