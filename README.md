Recent change:

Acme supports a built-in Edit command which accepts Sam editing
commands.  I modified sam.el to follow a similar approach so that
Emacs user can enjoy Sam capability without issuing a standalone
`~~~Sam~~~` window.

To enable this feature for a particular buffer, please enable
sam-edit-mode and then issue command `sam-eval-last-command`.  Binding
it to a key would be useful:

`(global-set-key (kbd "C-c e") 'sam-eval-last-command)`

Some examples:
```
20                            go to line 20
-/^/+#10                      go to column 10
0/hello/                      search for hello from the beginning
-/hello/                      search for hello backward
$-/hello/                     search for the last hello
,x/\n/d                       join all lines without spaces
+-                            expand current dot into whole line
,x/PATTERN/c/REPLACEMENT/     replace PATTERNs with REPLACEMENTs
,x a/\n/                      double all line spaces
x/^/ a/ /                     indent selected block with space/tab
x/^ /d                        remove indentation in selected block
< echo -e -n "\x41"           insert ascii code 0x41
,> wc -l                      cound lines
0 < date                      insert date at the beginning
,|sort                        sort the whole file
,x/TODAY/ < date              replace TODAY with real date
,x g/^\n$/d                   remove empty lines
,x/[a-zA-Z_][a-zA-Z_0-9]*/ g/n/ v/../ c/num/   replace variable n with num
```

------------------------------------------------------------------------------

This is an emulation of Rob Pike's Sam text editor in Emacs developed by Rick
Sladkey.  I happened to get this copy long time ago and I realized it is very
difficult to find this software nowadays on Internet.  In order to avoid
missing it again I put it here.  I had attempted to contact Rick Sladkey using
the email information in the software code but cannot find him.  Based on the
comments in the code, it seems that the license (the same as Emacs) allows me
to share it.  Please contact me if anyone has concern or new information.

The following is the comments in the software code.


sam.el -- emulate the sam text editor                    -*- Emacs-Lisp -*-
Copyright (C) 1993 Rick Sladkey <jrs@world.std.com>

This file is not part of Emacs but is distributed under
the same conditions as Emacs.

Emacs is free software; you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation; either version 2, or (at your option)
any later version.

Emacs is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.


LCD Archive Entry:
sam|Rick Sladkey|jrs@world.std.com|
Emulate the sam text editor Using Emacs|
11-Dec-1993|0.5|~/modes/sam.el.Z|

(defconst sam-version "sam v0.5 - 93-12-11")

Problems or Omissions:

can insert-buffer-substring be useful?

command grouping

missing simultaneous undo in multiple buffers

current directory for shell commands

buffer commands should use buffer-file-name

no support for a named pipe for commands

none of the special mouse features are implemented

multiple windows into a file don't really have separate dots

gracefully handle more syntax errs (e.g. "s")

gracefully handle empty or missing editing buffer

syntax errors cause unclearable in progress commands
