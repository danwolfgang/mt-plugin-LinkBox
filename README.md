# LinkBox, a plugin for Melody and Movable Type

## Overview

Manage and publish multiple blogrolls (lists of links).


## Features

* Create and Manage LinkBoxes
* Add links with label for each to LinkBox
* Plugin preferences for:
    * list style: "ul" or "ol"
    * link list sort order: order added or alphabetical
* Tags to output LinkBoxes


## Requirements

* Melody 1.0 or newer
* Movable Type 4.x


## Documentation

### Deploying Link Boxes with Themes

The following YAML structure is an example of a link box named "Blogroll" that is bundled with a hypothetical theme named BloggerTemplates.

    template_sets:
        blogger_templates:
            label: BloggerTemplates
            linklists:
                blogroll:
                    label: Blogroll
                    links:
                        google:
                            label: Google
                            url: http://www.google.com
                            description: Big search engine.
                            order: 1
                        slashdot:
                            label: Slashdot
                            url: http://slashdot.org
                            description: Old as the hills tech news site.
                            order: 3
                        melody:
                            label: Open Melody Software Group
                            url: http://openmelody.org
                            description: The OMSG website
                            order: 2

The following simple facts should clarify how LinkBox handles this YAML:

1. A link box does not need any links under it.
2. A link only needs two attributes: label and url.
3. The order attribute controls the actual order in which LinkBox will display the content.
4. The default value for order is "0" which means that links without an order attribute will take precedent over this with one.
5. LinkBox will not alter or remove an existing link list with the same name.

### Container Tags

* `mt:LinkBoxes` - Loops over linkboxes for the blog and name provided
* `mt:LinkBoxLinks` - Loops over links for the linkbox in context

### Function Tags

* `mt:LinkBox` - Returns a single linkbox specified by name (or it grabs the latest one) as a html list.

    Attributes:
    
    * `blog_id` - optional blog id
    * `name` - optional name of list
    * `list_style` - "ul" (default) or "ol" (can be specified in plugin settings as well)
    * `sort_order` - "added" (default) or "alpha" (can be specified in plugin settings as well)

* `mt:LinkBoxDescription` - description for the linkbox in context
* `mt:LinkBoxName` - name for the linkbox in context
* `mt:LinkBoxLinkURL` - URL for the link in context
* `mt:LinkBoxLinkName` - name for the link in context
* `mt:LinkBoxLinkDescription` - description for the link in context

### Examples

#### All LinkBoxs

    <mt:LinkBoxes>
        <div class="linkbox-container">
            <h3><$mt:LinkBoxName encode_html="1"$></h3>
            <ul class="linkbox">
        <mt:LinkBoxLinks>
                <li>
            <mt:If tag="MTLinkBoxLinkURL">
                        <a href="<mt:LinkBoxLinkURL encode_html="1">"><$mt:LinkBoxLinkName encode_html="1"$></a>
            <mt:Else>
                        <$mt:LinkBoxLinkName encode_html="1"$>
            </mt:If>
            <mt:If tag="MTLinkBoxLinkDescription">
                        <span><$mt:LinkBoxLinkDescription encode_html="1"$></span>
            </mt:If>
                </li>
        </mt:LinkBoxLinks>
            </ul>
        </div>
    </mt:LinkBoxes>

#### Specific LinkBox

    <$mt:Var name="linkbox_label" value="Favorite Sites"$>
    <div class="linkbox-container">
        <h3><$mt:Var name="linkbox_label"$></h3>
        <$mt:LinkBox name="$linkbox_label"$>
    </div>


## Installation

1. Move the LinkBox plugin directory to the MT `plugins` directory.
2. Move the LinkBox mt-static directory to the `mt-static/plugins` directory.

Should look like this when installed:

    $MT_HOME/
        plugins/
            LinkBox/
        mt-static/
            plugins/
                LinkBox/

[More in-depth plugin installation instructions](http://tinyurl.com/easy-plugin-install).


## Desired Features

* add `mt:LinkBox` attributes to `mt:LinkBoxes` tag


## Support

This plugin is not an official Six Apart, Ltd. release, and as such support from Six Apart, Ltd. for this plugin is not available.

## Authors

Six Apart, Ltd., OpenMelody Software Group

## Copyright

* 2009 Six Apart, Ltd.
* 2011 OpenMelody Software Group

## License

[Artistic License 2.0](http://www.opensource.org/licenses/artistic-license-2.0.php)


