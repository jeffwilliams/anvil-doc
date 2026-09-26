# Why does Anvil use a REST API?

Anvil is inspired by Rob Pike's Acme editor. One of the things that Acme provides is an API that is exposed as a filesystem: the editor's state can be read and changed by reading and writing to files. This is a great way to provide an API for a few reasons.

First, extending Acme means running a separate process that interacts with Acme through the filesystem. Since the extending program is a separate process, any severe issues in the program are limited to that process and so Acme is insulated from them. Contrast this to approaches where the editor provides a scripting language that is hosted in the editor itself, or where the editor loads compiled plugin code into it's process in the same thread; if the extension hangs due to I/O delays or coding errors, then the editor in its entirety hangs as well. Crashes in the extension crash the editor.

Second, since filesystem access is such a fundamental operation, no special library is needed and any programming language can be used to write extensions, including shell scripts. Extending Acme is more accessible to any user since users can write in whatever language they are most comfortable in, or choose the language that is most convenient to solve the problem.

Finally, extensions can be written and modified on the fly without needing to have Acme reload startup scripts or reload plugins. If you find an issue, just modify the code and run it again.

However, providing a filesystem API is not trivial. While I'd love to have something like this for Anvil, I instead comprimised by providing a REST API. It provides similar insulation from the extending program, and though it is not as convenient as providing a filesystem, I hope it has much of the value. Most languages provide standard libraries to communicate with HTTP servers, and REST operations are ubiquitous and simple enough to make using such an API convenient. 

You can even use it through shell scripts, via curl for [example](../../downloads/Format).

