=======================================================================
=                                                                     =
=                                                                     =
=  Notepad 2e - light-weight Scintilla-based text editor for Windows  =
=                                                                     =
=                                                                     =
=                                                    Notepad2 4.2.25  =
=                                       (c) Florian Balmer 2004-2011  =
=                                        http://www.flos-freeware.ch  =
=                                                                     =
=  Extended edition (c) 2013-2015                                     =
=                                                                     =
=                                            by Proger_XP and haccel  =
=                              https://github.com/ProgerXP/Notepad2e  =
=                                                                     =
=======================================================================


The Notepad2 Source Code

  This package contains the full source code of Notepad2 4.2.25 for
  Windows. Project files for Visual C++ 7.0 are included. Chances are
  that Notepad2 can be rebuilt with other development tools, including
  the free Visual C++ Express Edition, but I haven't tested this.


Rebuilding from the Source Code

  Notepad2 4.2.25 is based on Scintilla 2.24 [1].

  [1] http://www.scintilla.org

  To be able to rebuild Notepad2, the source code of the Scintilla
  editing component has to be unzipped to the "scintilla" subdirectory
  of the Notepad2 source code directory.

  Many of the Scintilla lexing modules are not used by Notepad2. Run
  LinkLex.js to adapt the list (in "scintilla/src/Catalogue.cxx") and
  make linking work properly.


Creating a Compact Executable Program File

  Linking to the system CRT slightly improves disk footprint, memory
  usage and startup because the pages for the system CRT are already
  loaded and shared in memory. To achieve this, the release version of
  Notepad2.exe is built using the Windows Driver Kit (WDK) 7.1.0 tools,
  available as a free download from Microsoft. The appropriate build
  scripts can be found in the "wdkbuild" subdirectory. Set %WDKBASEDIR%
  to the directory of the WDK tools on your system.


How to add or modify Syntax Schemes

  The Scintilla documentation has an overview of syntax highlighting,
  and how to write your own lexing module, in case the language you
  would like to add is not currently supported by Scintilla.

  Add your own lexer data structs to the global pLexArray (Styles.c),
  then adjust NUMLEXERS (Styles.h) to the new total number of syntax
  schemes. Include the "scintilla/lexers/Lex*.cxx" file required for
  your language into your project. Ensure the new module is initialized
  (in "scintilla/src/Catalogue.cxx"), either by manually uncommenting
  the corresponding LINK_LEXER() macro call, or by updating and
  re-running LinkLex.js.


Copyright

  See License.txt for details about distribution and modification.

  If you have any comments or questions, please drop me a note:
  florian.balmer@gmail.com

  (c) Florian Balmer 2004-2011
  http://www.flos-freeware.ch

  (c) Proger_XP and co. 2013-2015
  http://proger.me


Changes of the Extended edition

  Current Word Highlighting - with customizable formatting (rectangle,
  border, etc.) and colors. 3 modes: one occurrence in document, two
  or more but all are visible, multiple with some hidden under scroll.
  MaxSearchDistance INI setting controls maximum lookahead/behind
  distance to prevent performance degradation on very large files.

  Vim-like Edit > Find Next/Previous Word (Ctrl+[Shift]+8) for quick
  case-insensitive navigation between highlighted words (independent of
  this mode settings). Seeks to next/previous word if none at cursor.

  Find (Ctrl+F) now has Grep/Ungrep buttons (working on regexp too).
  In case of active selection these operate on selected lines only.

  Open Previous (Alt+G) - lets you toggle between two most recent
  History files with one keystroke.

  Open Dialog allows opening by prefix - so instead of typing the full
  file name or selecting with your mouse you can only type name's
  beginning and hit Enter or click Open to open the first matching file.
  This is disabled by default - set OpenDialogByPrefix to 1 in the INI.

  Better Save To Dialog - new file extension is determined first by
  DefaultExtension INI setting (as before) but then if current file was
  previously opened from or saved to disk its old extension is used as
  default (even if it's empty). If new file name ends on period file is
  saved without extension.

  Open/Save File dialogs now start with the path of last opened file.

  Added File > Open Next/Previous (no hotkeys but with available toolbar
  buttons) to open files going before/after current in its directory.

  Now remember Insert Tag (Alt+X) - now Opening and Closing tags are
  retained until Notepad is closed.

  Insert HTML Tag (Alt+X) now skips whitespace within the selection.

  Case-insensitive Find for Cyrillic characters - previously search was
  always case-sensitive regardless of Match case flag.

  When Find scrolls to a location it makes sure to preserve at least
  33% of the visible space above and below the match.

  Trimming Go To - now in Line and Column first number substring is
  extracted and used to navigate. For example, "abc567.89" will navigate
  to 567.

  Go To Absolute Offset - extension of Goto (Ctrl+G) dialog. Respects
  different charsets to the best extent possible.

  File > Launch > Command (Ctrl+R) now retains the path until another
  file is opened.

  File Shell Menu (Alt+R) - invokes Explorer's context menu for
  currently opened file.

  Rename To (Alt+F6) - acts as Save As but deletes original file on
  success.

  Intelligent Enclose Selection (Alt+Q). When "before" string consists
  of one of { ( [ < then "after" is set to the same number of } ) ] >.
  When "before" consists of one of:
             ` ~ ! @ # % ^ * - _ +  = | \ / : ; " ' , . ?
  ...then "after" is set to "before" string (wiki/Markdown editing).

  Added Edit > Block > Unwrap Brackes At Cursor (Ctrl+Shift+3) to
  compliment Ctrl+3-5. Removes brackets of type ( { [ < around current
  caret position (whichever type comes first). Respects nesting.

  Added Edit > Block > Unwrap Quotes At Cursor (Ctrl+Shift+4) to
  compliment Ctrl+1-2/6. Removes matching " ' ` around the caret (text
  is scanned to the left to determine the quote type). Does not account
  for nesting or escaping. Multiline.

  Insert HTML/XML Tag (Alt+X) supports { ( [ in addition to < when auto
  filling Closing tag: {{#if var}} -> {{/if}}, [quote] -> [/quote].
  It also skips leading non-word symbols when determining tag name:
  {{ #if }} or {{#if}} -> {{/if}}, not {{/}} as in the original.

  Added Edit > Special > Strip HTML Tags (Shift+Alt+X) to remove
  <tags> inside selection or if there's none - first leftmost tag.

  Added Edit > Special > Escape HTML (Ctrl+Shift+Alt+X) to turn < > &
  into &lt; &gt; &amp; respectively inside selection or everywhere.

  Ctrl+Wheel Scroll - very handy to navigate long scripts. Roll the
  wheel while holding Ctrl down to scroll through entire pages (similar
  to Page Up/Down).

  Notepad has a hidden feature of web search: set WebTemplate1-2 keys
  in Notepad2.ini to https://google.com/search?q=%s and then press
  Ctrl+Shift+1-2 with active text selection to navigate to that URL
  (with %s replaced but not URL-encoded).

  File > Encoding > UTF-8 now has Shift+F8 hotkey assigned.

  File > Line Endings > Unix now has Alt+F8 hotkey assigned.

  Edit > Copy Add (Ctrl+E) now uses single line break and when pressed
  without active selection appends the entire line.

  Now Retain caret position and selection when file is re-coded (File >
  Encoding menu items).

  Find/Replace dialogs' Search String input responds to Ctrl+Backspace.

  Go To Last Change (Ctrl+Shift+Z) - moves caret to the position of last
  Undo action.

  Replace Settings in All Instances - very useful if you have dozens of
  Notepad windows open and need to change settings in one of them;
  select this to make all others reload them from disk (not from this
  instance).

  Reload Settings from Disk (Alt+F7) - replace all settings in current
  window with fresh version read from Notepad2.ini.

  Added Ruby syntax scheme highlighting.

  CSS syntax scheme improvements:

    - Added CSS 3 properties.

    - Enabled //-inline comments (Ctrl+Q) that are used in LESS, SASS
      and other preprocessors.

    - Fixed brackets of nested rules that were not matching in some
      cases (visually and with Ctrl+B).


###
