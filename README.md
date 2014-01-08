Neos-Plugin-DMF.SeoTool
=======================

This plugin provides some useful NodeType properties for pages. Navigation labels, link titles and some meta content like description and canonical tags will be provided.

## Installation
Clone this repository into your application folder:

    * cd ROOT/Packages/Application
    * git clone git@github.com:dohomi/Neos-Plugin-DMF.SeoTool.git DMF.SeoTool

Then check if the plugin needs to get activated inside of your package management. Check if the plugin is listed:

    ./flow package:list
    ./flow package:activate dmf/seotool

### Use of this plugin
You will see additional fields inside of your page properties. You can fill them out and after this you need to adjust your
Root.ts2 inside of your site package

    page = Page {
        head {
            (...)
            titleTag < DMF.SeoTool:PageTitle

            metadata < DMF.SeoTool:MetaContent

            canonicalReference < DMF.SeoTool:Canonical
            canonicalReference.alwaysInclude = 1
        }

        body {
            (...)
            content {
                (...)
                websiteTitle =  ${q(node).filter('[instanceof TYPO3.Neos.NodeTypes:Page]').property('websiteTitle')}
            }
        }
    }

Inside of your page template you can include the websiteTitle like following sample code:

    <f:if condition="{content.websiteTitle}">
        <h1 class="page-header">{content.websiteTitle}</h1>
    </f:if>
