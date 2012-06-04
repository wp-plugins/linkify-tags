=== Linkify Tags ===
Contributors: coffee2code
Donate link: http://coffee2code.com/donate
Tags: tags, link, linkify, archives, list, widget, template tag, coffee2code
License: GPLv2 or later
License URI: http://www.gnu.org/licenses/gpl-2.0.html
Requires at least: 2.8
Tested up to: 3.4
Stable tag: 2.0.3
Version: 2.0.3

Turn a list of tag IDs and/or slugs into a list of links to those tags.

== Description ==

Turn a list of tag IDs and/or slugs into a list of links to those tags.

The plugin provides a widget called "Linkify Tags" as well as a template tag, `c2c_linkify_tags()`, to easily indicate tags to list and how to list them.  Tags are specified by either ID or slug.  See other parts of the documentation for example usage and capabilities.

Links: [Plugin Homepage](http://coffee2code.com/wp-plugins/linkify-tags/) | [Plugin Directory Page](http://wordpress.org/extend/plugins/linkify-tags/) | [Author Homepage](http://coffee2code.com)


== Installation ==

1. Unzip `linkify-tags.zip` inside the `/wp-content/plugins/` directory for your site (or install via the built-in WordPress plugin installer)
1. Activate the plugin through the 'Plugins' admin menu in WordPress
1. Use the c2c_linkify_tags() template tag in one of your templates (be sure to pass it at least the first argument indicating what tag IDs and/or slugs to linkify -- the argument can be an array, a space-separate list, or a comma-separated list).  Other optional arguments are available to customize the output.


== Screenshots ==

1. The plugin's widget configuration.


== Frequently Asked Questions ==

= What happens if I tell it to list something that I have mistyped, haven't created yet, or have deleted? =

If a given ID/slug doesn't match up with an existing tag then that item is ignored without error.

= How do I get items to appear as a list (using HTML tags)? =

Whether you use the template tag or the widget, specify the following information for the appropriate fields/arguments:

Before text: `<ul><li>` (or `<ol><li>`)
After text: `</li></ul>` (or `</li></ol>`)
Between tags: `</li><li>`


== Template Tags ==

The plugin provides one template tag for use in your theme templates, functions.php, or plugins.

= Functions =

* `<?php c2c_linkify_tags( $tags, $before = '', $after = '', $between = ', ', $before_last = '', $none = '' ) ?>`
Displays links to each of any number of tags specified via tag IDs/slugs

= Arguments =

* `$tags`
A single tag ID/slug, or multiple tag IDs/slugs defined via an array, or multiple tags IDs/slugs defined via a comma-separated and/or space-separated string

* `$before`
(optional) To appear before the entire tag listing (if tags exist or if 'none' setting is specified)

* `$after`
(optional) To appear after the entire tag listing (if tags exist or if 'none' setting is specified)

* `$between`
(optional) To appear between tags

* `$before_last`
(optional) To appear between the second-to-last and last element, if not specified, 'between' value is used

* `$none`
(optional) To appear when no tags have been found.  If blank, then the entire function doesn't display anything

= Examples =

* These are all valid calls:

`<?php c2c_linkify_tags(43); ?>`
`<?php c2c_linkify_tags("43"); ?>`
`<?php c2c_linkify_tags("books"); ?>`
`<?php c2c_linkify_tags("43 92 102"); ?>`
`<?php c2c_linkify_tags("book movies programming-notes"); ?>`
`<?php c2c_linkify_tags("book 92 programming-notes"); ?>`
`<?php c2c_linkify_tags("43,92,102"); ?>`
`<?php c2c_linkify_tags("book,movies,programming-notes"); ?>`
`<?php c2c_linkify_tags("book,92,programming-notes"); ?>`
`<?php c2c_linkify_tags("43, 92, 102"); ?>`
`<?php c2c_linkify_tags("book, movies, programming-notes"); ?>`
`<?php c2c_linkify_tags("book, 92, programming-notes"); ?>`
`<?php c2c_linkify_tags(array(43,92,102)); ?>`
`<?php c2c_linkify_tags(array("43","92","102")); ?>`
`<?php c2c_linkify_tags(array("book","movies","programming-notes")); ?>`
`<?php c2c_linkify_tags(array("book",92,"programming-notes")); ?>`


* `<?php c2c_linkify_tags("43 92"); ?>`

Outputs something like:

`<a href="http://yourblog.com/archives/tags/books">Books</a>, <a href="http://yourblog.com/archives/tags/movies">Movies</a>`

* `<?php c2c_linkify_tags("43, 92", "<li>", "</li>", "</li><li>"); ?></ul>`

Outputs something like:

`<ul><li><a href="http://yourblog.com/archives/tags/books">Books</a></li><li><a href="http://yourblog.com/archives/tags/movies">Movies</a></li></ul>`

* `<?php c2c_linkify_tags(""); // Assume you passed an empty string as the first value ?>`

Displays nothing.

* `<?php c2c_linkify_tags("", "", "", "", "", "No related tags."); // Assume you passed an empty string as the first value ?>`

Outputs:

`No related tags.`


== Filters ==

The plugin exposes one action for hooking.

= c2c_linkify_tags (action) =

The 'c2c_linkify_tags' hook allows you to use an alternative approach to safely invoke `c2c_linkify_tags()` in such a way that if the plugin were to be deactivated or deleted, then your calls to the function won't cause errors in your site.

Arguments:

* same as for `c2c_linkify_tags()`

Example:

Instead of:

`<?php c2c_linkify_tags( "43, 92", 'Tags: ' ); ?>`

Do:

`<?php do_action( 'c2c_linkify_tags', "43, 92", 'Tags: ' ); ?>`


== Changelog ==

= 2.0.3 =
* Re-license as GPLv2 or later (from X11)
* Add 'License' and 'License URI' header tags to readme.txt and plugin file
* Remove ending PHP close tag
* Note compatibility through WP 3.4+

= 2.0.2 =
* Note compatibility through WP 3.3+
* Add link to plugin directory page to readme.txt
* Update copyright date (2012)

= 2.0.1 =
* Note compatibility through WP 3.2+
* Minor code formatting changes (spacing)
* Fix plugin homepage and author links in description in readme.txt

= 2.0 =
* Add Linkify Tags widget
* Rename `linkify_tags()` to `c2c_linkify_tags()` (but maintain a deprecated version for backwards compatibility)
* Rename 'linkify_tags' action to 'c2c_linkify_tags' (but maintain support for backwards compatibility)
* Add Template Tag, Screenshots, and Frequently Asked Questions sections to readme.txt
* Add screenshot of widget admin
* Changed Description in readme.txt
* Note compatibility through WP 3.1+
* Update copyright date (2011)

= 1.2 =
* Add filter 'linkify_tags' to respond to the function of the same name so that users can use the do_action() notation for invoking template tags
* Fix to prevent PHP notice
* Wrap function in if(!function_exists()) check
* Reverse order of implode() arguments
* Remove docs from top of plugin file (all that and more are in readme.txt)
* Note compatibility with WP 3.0+
* Minor tweaks to code formatting (spacing)
* Add Upgrade Notice section to readme.txt
* Remove trailing whitespace

= 1.1 =
* Add PHPDoc documentation
* Add title attribute to link for each tag
* Minor formatting tweaks
* Note compatibility with WP 2.9+
* Drop compatibility with WP older than 2.8
* Update copyright date
* Update readme.txt (including adding Changelog)

= 1.0 =
* Initial release


== Upgrade Notice ==

= 2.0.3 =
Trivial update: noted compatibility through WP 3.4+; explicitly stated license

= 2.0.2 =
Trivial update: noted compatibility through WP 3.3+ and minor readme.txt tweaks

= 2.0.1 =
Trivial update: noted compatibility through WP 3.2+ and minor code formatting changes (spacing)

= 2.0 =
Feature update: added widget, deprecated `linkify_tags()` in favor of `c2c_linkify_tags()`, renamed action from 'linkify_tags' to 'c2c_linkify_tags', added Template Tags, Screenshots, and FAQ sections to readme, noted compatibility with WP 3.1+, and updated copyright date (2011).

= 1.2 =
Minor update. Highlights: added filter to allow alternative safe invocation of function; verified WP 3.0 compatibility.
