#Version 0.8.6
 
 
* System Requirements: Eclipse 3.3+, JDK 1.5+.  The intent is for this software to be used with FlexBuilder 3 or 4, but there are no actual dependencies.
 
* Install (several ways to install) 
 
* Add a remote update site through Help->Software Updates:
http://flexformatter.googlecode.com/svn/trunk/FlexFormatter/FlexPrettyPrintCommandUpdateSite.  The 
exact instructions differ depending on which version of Eclipse you are using.
You should be able to turn on Eclipse auto updates and 
be notified when a new version is published.  You may have to set up proxy 
settings in the Eclipse preferences if you are behind a corporate 
firewall.  Note: if you are running Eclipse 3.5 and the update site doesn't work
for you, try adding "/site.xml" on the end and see if that helps.  
 
* Download the zip file and extract the 3 plugins jars into the 
Eclipse plugins directory (Eclipse 3.3) or the dropins 
directory (Eclipse 3.4+) and restart Eclipse (with -clean 
if you are using 3.3).  Enough people have had problems with this with Eclipse 3.4+ that I recommend only using the update site.
 
 
 
* Usage See the docs page for a usage doc that describes the
options.  https://sourceforge.net/apps/mediawiki/flexformatter/index.php?title=Preferences
There is also usage doc in the ? (question mark) help on the
preference pages.
 
* Bugs: Undoubtedly.  If you find something, create a 
bug/feature report through the 'tracker'.

 
-----------------------------------------------------------------------------------------------------------
#Change log

###0.8.6

6/20/2011
####New Features

* Added setting to not indent the 'case' keyword for switch statements.  On the Actionscript 'tweaks' page.  This probably only makes sense for 'cuddled' braces.
* Extended the semantics of 'No newlines before break/continue/expressions' settings to include 'else' and loops.  These options are buried under the 'Braces/Line breaks' section.
* Added option to not indent the closing tag if it has been forced to a newline in mxml.  This is on the "Custom attribute order" dialog.
* Added option to control spaces around equals in metatags.  On Actionscript 'tweaks' page.
* Added ability to associated getters and setters without requiring the sort option.  This is in the ActionScript Rearranging settings.  Should work for both simple settings and creating advanced member selectors.

####Fixes

* Format on save (autoformat) would stop working sometimes.  I tracked down one case where this happened if you issue an undo/redo when it's not legal.

###0.8.5

5/11/2011
####New Features

* Comment wrapping.  See the new 'Comments' tab under 'Actionscript'.  You must disable the "keep relative indent for comments" option to see enable the wrapping options.
* Added ability to keep tags other than Bindable on same line with properties (see table on Tweaks page)
* Added Gnu-style brace indent for statements.  Only applies to statements, not package/class/function.

####Fixes

* Now ensure document ends with newline if whole document is formatted.  This is for consistency with the command line operation.
* Now honor spaces around '=' on metatags.

###0.8.4

4/11/2011
####New Features

* None

####Fixes

* New feature to remove unused namespaces would remove mx/fx/s, so I hardcoded in for now NOT to remove those to prevent surprises.

###0.8.3

4/10/2011
####New Features

* Now a setting to control breaking before or after operators
* Setting under "Advanced wrapping" to wrap each (every) argument to a function call if the maximum line length is reached
* Ditto for parameters in function declarations
* Options to wrap arrays with or without alignment
* Options to wrap object declarations with or without alignment
* New command (toolbar icon and option in mxml prefs) to remove unused namespace declarations in mxml files.

####Fixes

* One regression introduced in 0.8.1 for specifying a charset when running from the command line. 

###0.8.2

3/12/2011
####New Features

* Flags to control whether carriage returns are added to expression/throws statements after an 'if'.  Buried under the advanced 'brace style' settings.
* Added option to control whether end ;/]/) of a wrapped expression gets unindented.
* Added ability to override options per project.  This should also allow pushing the per-project options files to source control.
* Added ability in rearranging to grab only getter/setter functions and then their associated properties.  Before, you could only grab the properties and then add the getters/setters to the group.

####Fixes

* Parser now supports '@' symbol before metatags in Actionscript code.  Apparently this is kind of a gray area in FlashBuilder, but does work.
* Fixed handling of indent for function expressions

###0.8.1

2/17/2011
####New Features

* Added flag on command line to allow specifying of input file charset.  These are Java charset strings (ex. "UTF8")
* Added handling for a single file on the command line instead of requiring a directory.
* Parameter assignment can now be specified separately for wrapping.
* Const fields can now be selected for rearranging on the custom members dialog
* Option to control blank lines before/after script within the CDATA block.
* Option to add blank lines before the closing tag of a block (if it has children)
* Options for whether to add a carriage return to if/loops for simple structures (break/return/continue) that don't already contain a carriage return (buried under the 'Braces' twistie) 

####Fixes

* The option to keep the end of the CDATA block with the end mx:Script tag didn't work in all cases.
* The '.' in a Vector declaration could be used as a split point for line wrapping. 
* Bug with copyright placement on files with imports but no package statement.
* Bug with formatting of the selected lines (crash dialog) that was introduced a few releases ago.  I think it only happened with the '=' alignment or brace add/remove
 
###0.8.0

1/22/2011
####New Features

* NONE: this release is to fix a critical bug with the experimental brace removal feature

####Fixes

* !!!If the Smart Add/Remove braces feature is enabled, empty blocks may be removed, causing invalid code!  Do not use prior releases if you have enabled this option!
* Smart Add/Remove braces feature would leave blank lines if a removed brace was on a line by itself.
* Smart Add/Remove braces didn't work correctly if removing braces in mxml files.  Breakpoints might be lost.
 
###0.7.9

1/16/2011
####New Features

* Option to only add braces to if/loops for 'non-simple' statements
* Option to allow braces to removed for simple statements
* Dialog pops up to indicate successful import of formatter preferences
* Option to control indenting of CDATA block in script tag

####Fixes

* Items with a 'text' attribute had a problem with controlling attribute ordering.  This was a regression in 0.7.7, I believe.
* Adjusted a code path that was causing another two jars to be required when running from the command line (with the current set of command line jars).

###0.7.8

12/5/2010
####New Features

* Options to add blank lines inside start brace and end brace of functions
* More options for spaces inside parens. Thanks to Andrew for the work.
* Option to align end of line comments on a column.

####Fixes

* Fixed bug where two /* comments on the same line got an extra return added between them.
* Added handling to ignore non-breaking spaces (which are apparently easy to add on Macs).
* inline regular expressions starting with /> weren't parsing correctly

###0.7.7 
11/9/2010
####New Features 
 
* Options for mxml/as to preserve relative indent of lines inside multiline comments (see tweaks)
* Added 'other' category to mxml attribute ordering; allows placement of extra attributes in middle of attribute list

####Fixes 
 
* parser didn't properly handle metadatas with qualified names (ex. [MessageHandler(selector = MessageChannel.PNL)]
* A few parser bugs around :: operator where I cleaned up the parser.

 
###0.7.6 
8/25/2010
####New Features 
 
* Option to align '=' in variable declarations (on Tweaks preference page)
* Option to add braces to cases in switch statements (on Tweaks preference page).
* Option to add blank lines before 1st import in package scope.
* Example code in preference page is now editable (there's a new checkbox above each text area).  It won't stick between invocations, but you can paste in the current file you are editing or add particular syntax to see the effects of changing settings.
* Option to control spaces inside the binding braces in mxml attributes
* Option to 'format' the bound variables inside mxml attributes.  Will add spaces inside method parens, for example.
* Option to leave whitespace between the end of a line and a comment on the line (either // or /* */)

####Fixes 
 
* Bug with rearranging ActionScript within MXML code.  In some cases, an error dialog will pop up indicating an internal error.  This is annoying, although the code will end up formatted correctly anyway.
* Vector initializers not supported (ex. var v:Vector.<int>=new <int>[1,2,3];

 
 
###0.7.5 
8/3/2010
####New Features 
 
* New mxml option to disable formatting within some tags.  On 'Special tags' tab.  Useful for fx:XML
* New option for spaces before function calls

####Fixes 
* Fixed 'case' formatting to line up braces with case keyword.  Braces were indented a tab.
* Metatags containing attributes named 'default' didn't parse correctly.
* Fixed bug with rearranging code in certain cases with import statements with no trailing semicolon
* Fixed indenting of Functions defined as part of a method call (i.e. function expressions)

 
###0.7.4 
6/22/2010
####New Features 
* New option (ActionScript->Tweaks->Add braces to conditional statements) to add braces if there no braces.  There is no inverse option, so use with care.
* New option to add blank lines before comments in mxml files
* Added ability to exclude entire file from formatting: Include the following string in an Actionscript or MXML comment anywhere in the file. {FlexFormatter:IgnoreFile}

####Fixes 
 
* Fixed comments in mxml files to be kept with the following line.  This was broken if options like 'Spaces between sibling tags' were used.
* Fixed code to not pull in extra Eclipse classes if run from the command line.
* Updated the 'Set to Adobe Standards' button to add a lot more mxml standards from the Cairngorm site.

 
###0.7.3 
5/2/2010
####New Features 
 
* New option (on Auto Format page) to allow batch formatting to not pop up a dialog at the end.

####Fixes 
 
* Fixed minor bug where there was no space between the 'new' operator and a parenthesized expression
* Fixed nested switch statements to indent correctly
* Added category to update site so that it doesn't appear that the formatter can't be installed

 
###0.7.2 
3/16/2010
####New Features 
 
* Member selectors can now select sort members by type (the String type name in the declaration)
* Member selectors can now select members by metadata tag (ex. all the 'Bindable' items)
* New toolbar icons (thanks to Mat Blanchet)

####Fixes 
 
* default xml namespace didn't honor the 'spaces around assignment' setting
* no space after asterisk in for loop control
* made member selector dialog scrollable since it has gotten too tall.

 
###0.7.1 
2/1/2010
####New Features 
 
* Member selectors can now select members by type (the String type name in the declaration)
* Member selectors can now select 1-parameter functions by name or type of the parameter (again, based on the String name/type in the code)
* Ability to put 'while' on a new line for do..while loops
* Extra setting to make mxml attributes wrap to the max line length even if you are using the "keep < n attrs on a single line" setting
* The 'Rearranging' toolbar button now affects ActionScript code in .mxml files.
* Member selectors can now pre-select items to make ordering with the predefined selectors easier.

####Fixes 
 
* Small bug with the number of blank lines after a copyright statement is inserted, if an existing copyright had to be removed.
* Return statement fixed to always have a space after the 'return' keyword

 
 
###0.7.0 
1/20/2010
####New Features 
 
* Ability to add section header comments to code.  This is part of rearranging and is configured on the "Headers/Spans" tab and the "Elements" tab.
* Ability to add copyright header comment to Actionscript files.  This is part of rearranging and is configured on the "Copyright" tab.
* Ability to group getter/setter methods with their associated property.  This is part of rearranging and is enabled by a checkbox on the Properties detail tab.

####Fixes 
 
* Now allow functions and properties to be named '$' or '_'.  These caused parse errors.
* Fixed rearranging of code to rearrange class metatags according to the ordering table.  Metatags on other elements were properly ordered.
* Multiple consecutive /* comments had the first line of the second comment pulled up to the end line of the previous comment.

 
 
###0.6.33 
12/13/2009
####New Features 
 
* No new features this week, just some bug fixes.

####Fixes 
 
* Changed parsing of Strings to be more lenient and not require escaping of backslashes since Adobe apparently doesn't require it.
* parse error: default xml namespaces didn't allow expressions as the assignment value.
* parse error: for loops only allowed declarations in the initializer, not expressions 
* fixes for some problems involving missing (but implicit) semicolons

 
###0.6.32 
####New Features 
 
* Added plain xmlns to the default 'xml namespaces' group for mxml attributes.  
* Added ability to autosync back to auto sync file to maintain preferences.  With this setting, saving the preferences dialog also writes back to the autosync file.
* Added option to capture 'state' attributes as part of mxml attribute groups.  State attributes are ones that have a '.' in them, like 'event.mouseUp'

####Fixes 
 
* Conditional code blocks inside the class declaration area weren't parsing in some cases.
* Rearranging code would add an extra newline after lines ending with a line comment (//)
* Static initializers weren't accounted for in the rearranging code.
* Rearranging failed on interfaces
* Using bulk formatting from the package explorer/navigator context menu failed in some situations because of files with no extension (which is common in subversion source control)

 
 
###0.6.31 
####New Features 
 
* Extended rearrange AS code while formatting to include ActionScript blocks in mxml files.
* New option to allow adding blank lines before the child tag of all tags
* New option to allow adding blank lines before the child tag of listed tags

####Fixes 
 
* The namespace specifier (::) wasn't always allowed in the grammar.  For example, to annotate a function name.
* Rearranging could move imports incorrectly if they were loose in the ActionScript file (i.e. top level).  They were moved into the package scope, if it existed, which was wrong.

 
###0.6.30 
####Fixes 
 
* Namespace access to functions and properties wasn't supported properly in the grammar.  Ex. mx_internal::funcCall();

 
###0.6.29 
####New Features 
 
* The setting is now enabled to let you do rearranging while formatting an entire AS file.
* New option to control spaces between function name and open paren of the formal parameter list
* Added new setting to control other extensions that can be formatted as XML (using the mxml options, but not formatting CData sections).

####Fixes 
 
* Bug in FlashBuilder 4 with rename of a class causing an exception.  I moved "format on save" to occur on the main thread instead of a worker thread.
* Fixed bulk format (from explorer context menu) to work in Flex Explorer and from the top level (a project).
* Added check for conditional compiler blocks and make rearrange fail in that case, because the rearrange code can't handle it.  This is a pretty rare language feature, so I expect low impact.
* Rearranging and adding asdoc failed for files that contained e4x items with tag attributes.  Fixed grammar.

 
 
###0.6.28 
####New Features 
 
* Added new setting for mxml groups that allows you to set the number of attributes per line for each group if you are using that wrapping option.  Previously, you could only use the default 'n' from the main page.
* Added an entirely new ActionScript wrapping algorithm based on operator precedence.  This affects the old-style wrapping some (because there are more split-points).
* More options for ActionScript rearranging to allow you to select functions or properties with different attributes to control how they are ordered.
* I've split out the options for newlines before braces further.

####Fixes 
* Added some more split points to the wrapping algorithm because object declarations weren't wrappable.
 

 
 
###0.6.27 
####New Features 
 
* Option to add blank lines between sibling mxml tags.  This is probably more useful than the previous option to add blanks before certain tags, but both options can be used together.

####Fixes 
 
* Conditional compilation blocks around ActionScript members weren't supported in the grammar.  
* Fixed 'Indent' with no selection to maintain the current cursor position instead of selected the entire line.  This more closely matches the Java behavior of indent.
* grammar didn't support expression evaluations as attribute names in e4x.

 
###0.6.26 
####New Features 
 
* Moved rearranging preferences into main formatter preferences.  Rearranging is still a separate option from formatting, but the options can now be imported/exported.
* Number of tabs in hanging indent now configurable.
* Added import/export of preferences from/to string to allow users on some operating systems (some Macs apparently) to export settings.

####Fixes 
 
* 'case' keyword followed by a negative integer as case selector lost the whitespace between them.
* e4x tags fixed to not add newlines in the middle of text content
* e4x fixed to draw up tags onto single line correctly (for the keep on single line setting)

 
###0.6.25 
####New Features 
 
* Ability to filter out files from the auto-formatting on save.  See the auto format preference page.  
* Added ability to format event handlers in mxml.  This is configurable, so you can add additional tags if I missed some, or remove ones that are problematic.
* Setting to supply blank lines before tags now allows regex tag names, so you don't have to list all tags.  Ex. "mx:.*"
* New ability to exclude sections of AS code from formatting using comment markers.  Search for the command "exclude block from formatting" in the <preferences>/General/Keys dialog to map this command.
* Added some syntax coloring to the pref page so it looks nicer.

 
####Fixes 
 
* Text content inside e4x tags could get extra spaces added in some cases.

 
###0.6.24 
####New Features 
 
* Now, rearrange and asdoc comments should work in Actionscript files with no package/classes.  Before, you would get a parse error.
* New setting (on Actionscript 'tweak' tab) that tells the formatter to not remove extra spaces around declaration '='.  This is to allow you to preserve decls that are lined up.

 
####Fixes 
 
* ASDoc generator for whole file would add a comment to an item even if the item already had one.  I thought this was already working, but it's fixed now.
* ASDoc comments now contain fewer blank lines.  If a tag doesn't exist (like throws), then the blank comment line is removed.
* Longstanding bug with 'don't put else and if on same line'.  Now, the if statement should be indented under the else instead of lined up with it.
* Another longstanding bug with else after brackets.  If you had a statement containing brackets (like a for loop), the else would be cuddled next to it rather than on a new line.
* Remove ctrl+shift+R accelerator for rearrange since it overrode the "open resource" command.  You can map rearrange to another keystroke if you wish.

 
###0.6.23 
####New Features 
* none
 
####Fixes 
 
* mxml regression causing extra blank lines in mxml tags with text content
* Accidentally built one plugin with jdk1.6 requirement.

 
###0.6.21 
####New Features 
* none
 
####Fixes 
 
* User reported problems with files using only \r as line delimiter.  Apparently this is the default delimiter for Mac, but is not used by FlexBuilder.  Fixed hopefully.
* Problems in FlashBuilder 4 due to its generation of files with mixed line delimiters.
* Updated default special tag lists in mxml to include the 'fx' versions.  Users with existing settings will have to restore defaults for those tag tables or add the tags themselves if they are using the new fx tag set.
* Rearrange command on a non-as file displayed error msg then continued with parse instead of exiting.

 
###0.6.20 
####New Features 
 
* 2 new buttons for adding ASDoc to class elements.  This only works in ActionScript files (.as).  One button adds the comments to all methods that don't already have them (based on the preference page settings).  The other button adds a comment to the current class/method/property.  On the preference page, there are also templates to let you control to some extent what is generated.  This is EXPERIMENTAL. Feedback through the tracker/forums is welcome.
* Another new button for rearranging actionscript elements. Again, there is a preference page that lets you control the order of elements and modifiers on elements.   This is EXPERIMENTAL.  Feedback through the tracker/forums is welcome.  I expect to integrate this with the formatter proper (as an optional pre-format step) at some point, but there is too great a potential for corrupting code at this point.
* Added an option to allow non-indenting of package elements.  This matches the look of the Adobe samples, although not their editor auto indent behavior.

 
####Fixes 
 
* Added keystroke bindings to map the keys by default in FlashBuilder.  I did not add Ctrl+I since that already is in use.
* Fixed several e4x bugs
* Parser failed with methods named "get" or "set".  Fixed to allow that, as well as some other surprises, like "override".

 
###0.6.19 
####New Features 
 
* Option for adding blank lines before each property declaration. This is an Adobe coding convention, although it seems a little draconian.
* Option for spaces before/after declaration colon.  I've split this out as an "advanced" setting for those who need this flexibility.
* Option for keeping some blank lines even when otherwise deleting. I think this will help those who want to remove extra blank lines  while still keeping blank lines they've added in random places.

 
####Fixes 
 
* I found some bugs with blank line handling that sometimes caused the wrong number of blank lines when used in conjunction with expression that had the "format without changing/removing  newlines" setting.  I think it's better now.

 
###0.6.18 
####New Features 
 
* New option for always generating indent whitespace, even on blank lines.
* New option for controlling spaces between control keyword and the following parenthesis.
* New button on preferences page to change options to the Adobe formatting standards where I'm aware of a standard and can support it.  Other options are not affected.
* New option to allow auto-updating of preferences from a file in the project.  See the "Update Checker" preference page and the help text in the '?' help.
  
 
####Fixes 
 
* Nested uses of the Vector type that are now supported.

 
###0.6.17 (optional release) 
####New Features 
* None. There are no new settings and pretty minor bug fixes, so this should be considered an optional release.
 
####Fixes 
 
* Operators &&= and ||= were missing from the Actionscript grammar, so I added them.
* There was a bug that caused line comments (//) to be incorrectly put in column 1 instead of being indented in some cases.  This was a regression in version 0.6.16 only.
* Fixed mxml wrapping to wrap if the attribute is going to cross the max line length limit (instead of wrapping after an attribute breaches the limit).

 
###0.6.16 
####New Features 
 
* Added new "tweak" setting to allow separate control of spaces around '=' for optional parameters.  
* Added context menu item for files/folders in navigator view to allow formatting/indenting of a tree of files.  It is slow, but easier than doing it by hand.  There are also instructions on the the documentation page for how to format from the command line.
* New setting to allow mxml tags with <=n attributes to be kept on one line.  This is useful if you have specified wrapping options for most tags but want to ignore the wrapping options (but not ordering options) for short tags.
* Added new format mode: format without removing line breaks.  This mode uses the wrapping hint for line length, but doesn't remove existing line breaks from the element.
* Added option for blank spaces before the end of an empty tag (/>)
* Added option to allow blank lines to be added before user-specified mxml tags.

 
####Fixes 
 
* Code from 0.6.15 to preserve indents in non-AS CDATA sections didn't add a linebreak after the CDATA section, so the following tag could end up on the same line with the end of the CDATA tag.

 
###0.6.15 (experimental release) 
####New Features 
 
* Added "advanced" options to allow setting of spaces inside parens, brackets, and braces separately to better to support the Adobe standards.  There is a checkbox that controls whether to use the main setting or to use the 'advanced' individual settings.  I hope this economizes on space and is reasonably intuitive.
* Added option to control whether empty statements (';') are put on new line or kept on line with control statement.

 
####Fixes 
 
* Fixed grammar to support conditional compiler directives (ex. Config::debug)
* Fixed format to keep multiple metatags near the item they modify.  The previous code worked with a single tag, but not with multiple tags.
* Changed behavior of "lines before functions" to not add the lines if the function is the first time in the class. Previously, I had made a previous change for control statements within blocks.  I'm not planning to change the "lines before classes" setting, since the normal case for that is a class at the top of the file. 
* Fixed grammar to allow double negation operators.  Ex. !!true
* Fixed mxml formatter to not change the indentation of CDATA sections that aren't inside mx:Script blocks.  You can enable the old indentation behavior by adding a tag (the inner most tag around the CDATA block) to the "Tags to always format" list.

 
###0.6.14 
####New Features 
 
* Added new setting for "spaces after label colon".  Now, there is a separate setting for spaces around a variable declaration colon and labels (code labels, case labels, Object labels).
* Reworked preference page (again) to group items and make slightly better use of screen real estate.
* Add context (F1) help to preference page and related dialogs.

 
####Fixes 
 
* Text operators like 'as' keyword did not always get surrounded by a space if the adjacent character was a ')'. Fixed to always surround with a space.
* Single line comments (//) were indented wrong in if right before an end brace ('}').  Typically for empty methods with a comment in them.
* Fixed problem with using FlexBuilder rename refactoring in combination with AutoFormat on save.  This has probably been an issue for several releases.  People with the experimental 0.6.13 release got worse behavior.
   
 
###0.6.13 (experimental release) 
####Fixes 
 
* Formatting/indenting removed breakpoints and other line-based annotations.  
* Annoying scrolled position with autoformat on save.  Should be fixed to maintain both line and relative position on screen
* Removed spaces inside the [ char of a directive because the Actionscript editor doesn't color the keyword if there is a space after the opening bracket.  I don't believe the space interferes with the compile, but it seems better to remove it for the moment.
* Space between return and ';' ("return ;"). Should be "return;"

 
###0.6.12 
 
####New Features:
 
* Ability to use regular expressions to specify attributes in groups.
* Ability to create groups of attributes and specify sort/wrapping settings for them. (0.6.11)
* Option to put [bindable] tags on line with bound item or line before. (0.6.11)
* Option for setting number of spaces inside parentheses 

 
###(0.6.11) 
 
####Fixes 
 
* Now treat variable declarations as part of 'general expressions' for purposes of the wrapping options. 
* "namespace" was not allowed in package names.  I was treating it as a reserved word.  Now allow it and others that are similar ("default", "to", "internal", etc.).
* Fixed to treat custom attribute ordering correctly when all of the attributes in a tag are handled in the  custom ordering, and the order ends with a newline.
* Command line formatting would zero-out a file if there were parse errors.  Added code to fail to format in that case.

 
###0.6.10 
####New Features:
 
* Changed behavior of Format command/button to format entire file if no selection, or selected lines if there is a selection.  This matches the Java formatter behavior in Eclipse.
* Breaking change to handling of attribute order dialog.  Now, you can specify groups of attributes at once.  You can push the 1st attribute to start on the line below the tag start by including a \n as the first entry.
* You can specify tags that should not have any of their text contents modified (not even indented).  Or you can specify tags whose text content can be indented and where newlines aren't significant.  

 
####Fixes:
 
* I royally screwed up the "format on save" functionality in the 0.6.8 release.  This release incorporates the fixes in the experimental 0.6.9 release.
* Fixed bug where special '*' type specifier wasn't parsed correctly if it was followed by '='.  Found mention of this on a Russian language blog.
* A multiline comment before the package statement would pull the package keyword up on the last line of the comment.
* MXML tags that had text content (like VO tags or String) were getting extra newlines added, which caused compile or runtime errors when whitespace was illegal. Ex. the mx:Number tag.
* The default behavior for 'general expressions' is to adjust whitespace and indent, but not to change newlines. However, this setting was broken, meaning that all expressions get pulled up onto 1 line by default.  Fixed to honor setting.
* The 'if' keyword always had a space before the open paren and the other keywords had no spaces.  Fixed to consistently have one space.
* Nested functions bodies were getting an extra indent.

 
###0.6.8 
####New Features 
 
* Ability to format/indent on save (settings on new preference page
* Split preference page into some tabs to be a little more screen friendly
* Added ability to add spaces around colons (':')

 
####Fixes:
 
* Removed extra blank line generation in ActionScript formatter when formatting the entire file or at end of file
* Fixed single line and multiline comments that are at the end of a line to not be pushed down to the next line

 
###0.6.7 
 
* Line delimiters were not being preserved and certain 
interactions with the Eclipse editor could lead to a lost 
trailing character (usually > or ;).  This problem also 
existed in 0.6.5.

 
###0.6.6 
 
* added keybindings (ctrl+shift+f and ctrl+i) and added to AS context tmenu (I couldn't get it added to the mxml context menu)
* added support for Vector.&lt;type&gt; syntax
* now prevent labeled statement from adding a return before the statement it's associated with
* added ability to wrap method calls/method decls/array decls to the first wrapped item
* added ability to wrap xml tags with a standard hanging indent
* fixed bug that prevented left braces from formatting after class and package decls
* added "preserve blank lines" feature for mxml
* miscellaneous other fixes

 
###0.6.5 
 
* The original version had problems with the "format" option on the boundary between MXML and ActionScript.  A Format of the entire document would work, but a format of selected lines might fail, especially if one of the lines was the end of an ActionScript block.  I believe it's more solid now.  However, event the original version didn't lose data; it just put up an error message and failed to format the code.  The Indent operation didn't suffer from the same bug.

 
###0.6.4 
 
* Initial public release
