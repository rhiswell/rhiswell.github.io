# Tips on Doxygen


```bash
# Create default configuration file 'Doxyfile'
doxygen -g

# Generate html/ or latex/
doxygen Doxygen

# Useful configurations

# If the EXTRACT_ALL tag is set to YES, doxygen will assume all entities in
# documentation are documented, even if no documentation was available. Private
# class members and static file members will be hidden unless the
# EXTRACT_PRIVATE respectively EXTRACT_STATIC tags are set to YES.
# Note: This will also disable the warnings about undocumented members that are
# normally produced when WARNINGS is set to YES.
# The default value is: NO.

EXTRACT_ALL            = YES

# If the EXTRACT_PRIVATE tag is set to YES, all private members of a class will
# be included in the documentation.
# The default value is: NO.

EXTRACT_PRIVATE        = YES

# If the EXTRACT_STATIC tag is set to YES, all static members of a file will be
# included in the documentation.
# The default value is: NO.

EXTRACT_STATIC         = YES

# If the SOURCE_BROWSER tag is set to YES then a list of source files will be
# generated. Documented entities will be cross-referenced with these sources.
#
# Note: To get rid of all source code in the generated output, make sure that
# also VERBATIM_HEADERS is set to NO.
# The default value is: NO.

SOURCE_BROWSER         = YES

# If you want full control over the layout of the generated HTML pages it might
# be necessary to disable the index and replace it with your own. The
# DISABLE_INDEX tag can be used to turn on/off the condensed index (tabs) at top
# of each HTML page. A value of NO enables the index and the value YES disables
# it. Since the tabs in the index contain the same information as the navigation
# tree, you can set this option to YES if you also set GENERATE_TREEVIEW to YES.
# The default value is: NO.
# This tag requires that the tag GENERATE_HTML is set to YES.

DISABLE_INDEX          = YES

# The GENERATE_TREEVIEW tag is used to specify whether a tree-like index
# structure should be generated to display hierarchical information. If the tag
# value is set to YES, a side panel will be generated containing a tree-like
# index structure (just like the one that is generated for HTML Help). For this
# to work a browser that supports JavaScript, DHTML, CSS and frames is required
# (i.e. any modern browser). Windows users are probably better off using the
# HTML help feature. Via custom style sheets (see HTML_EXTRA_STYLESHEET) one can
# further fine-tune the look of the index. As an example, the default style
# sheet generated by doxygen has an example that shows how to put an image at
# the root of the tree instead of the PROJECT_NAME. Since the tree basically has
# the same information as the tab index, you could consider setting
# DISABLE_INDEX to YES when enabling this option.
# The default value is: NO.
# This tag requires that the tag GENERATE_HTML is set to YES.

GENERATE_TREEVIEW      = YES

# If the GENERATE_LATEX tag is set to YES, doxygen will generate LaTeX output.
# The default value is: YES.

GENERATE_LATEX         = NO

# If the CALL_GRAPH tag is set to YES then doxygen will generate a call
# dependency graph for every global function or class method.
#
# Note that enabling this option will significantly increase the time of a run.
# So in most cases it will be better to enable call graphs for selected
# functions only using the \callgraph command. Disabling a call graph can be
# accomplished by means of the command \hidecallgraph.
# The default value is: NO.
# This tag requires that the tag HAVE_DOT is set to YES.

CALL_GRAPH             = YES

# The INPUT tag is used to specify the files and/or directories that contain
# documented source files. You may enter file names like myfile.cpp or
# directories like /usr/src/myproject. Separate the files or directories with
# spaces. See also FILE_PATTERNS and EXTENSION_MAPPING
# Note: If this tag is empty the current directory is searched.

INPUT                  = ../

# The RECURSIVE tag can be used to specify whether or not subdirectories should
# be searched for input files as well.
# The default value is: NO.

RECURSIVE              = YES

# The STRIP_FROM_PATH tag can be used to strip a user-defined part of the path.
# Stripping is only done if one of the specified strings matches the left-hand
# part of the path. The tag can be used to show relative paths in the file list.
# If left blank the directory from which doxygen is run is used as the path to
# strip.
#
# Note that you can specify absolute paths here, but also relative paths, which
# will be relative from the directory where doxygen is started.
# This tag requires that the tag FULL_PATH_NAMES is set to YES.

STRIP_FROM_PATH        = ../
```

Refs:
- Doxygen usage example for C. http://fnch.users.sourceforge.net/doxygen_c.html.
- Doxygen quickstart in 10 minutes. http://cedar-renjun.github.io/2014/03/21/learn-doxygen-in-10-minutes/.
- Relative files paths in doxygen-generated documentation. https://stackoverflow.com/questions/6261366/relative-files-paths-in-doxygen-generated-documentation.
- Doxygen does not find files when when specifying Source directory. https://stackoverflow.com/questions/18249741/doxygen-does-not-find-files-when-when-specifying-source-directory.