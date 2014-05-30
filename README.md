Bootstrap 3.1.1 Template for Interchange
========================================

This is the Div based Demo for Interchange that modernizes the old
standard template. It makes use of several newer technologies. jQuery is
included by default. All table-related layout has been replaced with
divs. Built on the [Bootstrap Framework, version
3.1.1](http://getbootstrap.com/getting-started/#download).

This is phase 2 of the above modernization. This template is using 
bootstrap 3, which was a substantially changed css version from 
bootstrap 2.* . Many things have been changed.

You can [download a customized
Bootstrap](http://getbootstrap.com/customize/), and drop it
into the html/bootstrap directory, to load your own colors, etc.

Created by [Perusion](http://perusion.com), based on the earlier
standard demo.

Copyright (C) 2013 Hanson Investments, Inc. d/b/a Perusion

This program is offered without warranty of any kind.
See file LICENSE for redistribution terms.

Requirements:
-------------

Works best with the latest Interchange source, unless there is a release
after Dec 24, 2013:
	http://ftp.icdevgroup.org/interchange-nightly.tar.gz

Usage:
------

Clone the repository (or download the ZIP file and extract) to your
Interchange directory (e.g. /usr/local/interchange). From there, run:

	bin/makecat --demotype=strap30 [your-catalog-name]

        (If you cloned the repository, you should manually remove the
        .git directory from your catalog root, after installation.)

Some of the changes include:
----------------------------

	* reflects items from initial bootstrap 2 conversion. 
	** reflects changes as of bootstrap 3.0

	Attempted to make catalog and directory structures more version control, (git) friendly.

	** This catalog template is a standalone template, and is designed to run display correctly
	with only bootstrap.css (or bootstrap.min.css). You can modify existing style or even design
	completely new theme by adding a strap3.css file. A sample file is included and can be
	activated by uncommenting the line in

		include/structure/head

	[comment]Uncomment to use additional css for mods or even entire theme
	<link rel="stylesheet" media="all" href="__CSS_DIR__/strap3.css">
	[/comment]

	**Moved entire head section to 

		include/structure/head

	to make editing more convenient. Same head section is used in all templates.

	** Removed some components that no longer work with this layout, or are out moded.
		product_flyout

	** Modified structure of components so that they can be placed horizontally, or vertically
	by passing a class in the page like this

	[control-set]
	[component]random[/component]
	[class]col-sm-12[/class]
	[output]bottom[/output]
	[/control-set]

	The way the templates are laid out, the horizontal placements, top and bottom components,
	are housed in a bootstrap "row" class, so you would want to pass a col- class to keep
	proper spacing. The left and right components, should be housed within a "row"
	class, as they are already in a col class. The control default is row, so you do not have to pass
	anything for those.

	<div class="[control class row]">

	** Javascript inline as well as linked, is now loaded via script after all elements 
	have been loaded. We have a function in the head section, "getScript(url,success)", 
	which is set up to first load JQUERY_LATEST, then load bootstrap.min.js, then to load 
	any Jquery that is coded into various scratch variables. They are currently:

				[scratch jquery_after]
				[scratch jquery_inpage]
				[scratch jquery_components]

	as named, they are intended to load jquery or javascript to all templates from jquery after,
	in the current page only from jquery_inpage, and from components from jquery_components.
	There is also additional code to accomodate older IE7 and IE8 browsers loading some scripts
	that adjust for bootstrap functions that are not supported in those browsers.

	**there are examples of how to load script in the demo, in index page, and in templates/components/product_tree

	[tmp jquery_inpage]
	[scratch jquery_inpage]
		$(document).ready( function (){
			//alert("Test in page js");
		});
	[/tmp]

	[tmp jquery_components]
	[scratch jquery_components]
	$('#nav_menu .collapse').on('show.bs.collapse', function () {
		$(this).prev().find(".glyphicon").removeClass("glyphicon-chevron-right").addClass("glyphicon-chevron-down");
	});
	//The reverse of the above on hidden event:
	$('#nav_menu .collapse').on('hide.bs.collapse', function () {
		$(this).prev().find(".glyphicon").removeClass("glyphicon-chevron-down").addClass("glyphicon-chevron-right");
	});
	[/tmp]


    **  The html doc_root directory now named "repos_for_html" in the template, is copied to the
		appropriate html docs location by makecat ... using the answers you supply to the following question:

		SampleHtml? /home/username/www/strap30

		This by default will *not* add a "repos_for_html" to your catalog directory. It will add the following
		directories and files to your html doc root:
		
		css/        
		fonts/      
		images/     
		index.html  
		js/


		If you are using version control on your catalog, it is recommended to create a directory like
		"repos_for_html" in the catalog directory, and regularly update it with the contents of your 
		html docs prior to commiting a version. Something like and rsync script, cronjob, ic job, or 
		even just:

		cp -a /home/username/www/strap30/*  /home/username/catalogs/strap30/repos_for_html/

	*	Templates all use HTML 5 based document.

	*	Consolidated LEFTRIGHT, LEFTONLY, NOLEFT TOP & BOTTOM variables
		into single TOP & BOTTOM. No longer need "templates/regions", 
		and moved defines into existing "variables/".
		Changes in templates can still be hard coded in BOTTOM, but the 
		long present but seldom used "display_class" in individual page
		headers is more often used.

	*	Templates leftright, leftonly, noleft, and newly added rightonly, formerly located in 
		"include/layout" have been moved to more appropriately named
		"templates/". This to consolidate directory structure and make 
		location of templates more intuitive. Can be easily changed to 
		be more backward compatible if desired by simply editing 
		"variable/BOTTOM"

	**  Templates have been radically modernized, jquery is delayed and loaded at the
		end of page load, several scratch variables have been added to the jquery loading
		to allow inclusion of jquery from the page content, components, and other locations.


	* New directory repos_for_html/css added to allow central location for possibly mult
		css files.

	* New directory repos_for_html/js added to allow central location for possibly mult
		script files.

	* New directory repos_for_html/fonts added to allow central location for possibly mult
		font files.

	*	No longer using THEME_CSS.

	**	New default directories and related variables added for javascript, css, and fonts:

		CSS_DIR	/strap30/css
		JS_DIR	/strap30/js
		FONT_DIR	/strap30/fonts

		Variables used in all template HEAD sections.

	**	Using bootstrap.css.min as default css, using strap30.css as cascaded
	sheet specific to Interchange and catalog implementation. You should only
	edit strap30.css, so that new versions of bootstrap.css appear, they can
	simply be inserted.

    ** All look/feel configuration is done by CSS. It should be quite
      possible to completely change the look simply by editing
      _CSS_DIR_/strap30.css and templates/layout/*.

    ** There is no longer any color scheme and no THEME/STYLE
      variable. Therefore the regions/ directory has been removed.

    * The default for left-hand side is a product tree, for the top
      bar is a flydown/out menu. Each are editable from within the UI.
	  ** added category display to product tree, which supports an
	  exploding menu, more compatible with pad and mobile layouts.

    ** The template layout is contained in templates/layout/*, and
      by [set display_class]leftonly[/set] you can change the type
      within the page.

    * The page title, and page banner can be set anywhere before
      the page footer.

    * There is an alternative multi-page checkout which has received
      quite a bit of testing.

    * UPS lookup for Canada and the US is supported out of the box.

    * US Postal international shipping is supported.

    * Customer service pages have been spiffed up and improved a bit.

    * If you install Text::Query, the search boxes will use
      Altavista-style search language.

    * Advanced search page improved quite a bit.

    ** Search in top bar includes autosuggest. IC isolated script: sug
	located in cgi-bin/ allows quick suggestions via ajax using direct 
	db query, avoiding overhead of IC.
	While this file is automatically placed in your CGI BIN, it
	does NOT have proper permissions to execute out of the box. This is because
	each system will vary, and it is up to the user to set proper permissions.
	Additionally, the file itself will need to be edited to point to the proper
	database, database table, database fields, and catalog.

	** Profiles moved from etc/ to include/profiles

    * All shipping files/databases moved to products/ship.

    * No more etc/after.cfg -- all configuration in catalog.cfg.

    * A few new feature demonstrations included.

    * Some files have been moved to unclutter the top level
      of the pages/ directory.

    * Other minor changes.

	** Added directive to point some non-version-tracked type files
	to separate directory. This directs at least catalogname.structure 
	and status.catalogname to a separate directory and out of catalog root.

	RunDir	run


	NOTES RE NVEND and new templates

	#20140409 starting notes for strap30 upgrade

	Added code to Interpolate to facilitate a cleaner implementation of more list using link_template
	While <UL><li> is currently elements of choice for list, kept backwards compatible for numeric flat list.
	Current item used to be simply enclosed with 
	
	<strong>1</strong>

	But that would not allow use of list style in template. So we need to commit changes to Interpolate.pm
	sub more_link_template and sub more_link

	Either of the more-list configurations below can be used. 
	

	[more-list]
		[link-template]<li class="$CLASS$"><a href="$URL$">$ANCHOR$</a></li>[/link-template]
		<ul class="pagination pagination-centered">{PREV_LINK}{MORE_LIST}{NEXT_LINK}</ul>
	[/more-list]

	[more-list]
	[more]
	[/more-list]


The intent is to slowly document each of the areas of this template with
online help to provide a constantly-improving catalog application for
use by Interchange users not wishing to greatly change the foundation.


