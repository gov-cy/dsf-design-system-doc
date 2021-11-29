# dsf-design-system
Gov.cy DSF design system code  documentation

This is the readme for the dsf-design-system-docs repository. 
Demo: https://gov-cy.github.io/dsf-design-system-docs

## Updating Documentation

The documentation site resides in the `docs` folder and is controlled by the `data\pages.json` and markdown files contained in the `content` folder. The system uses templates defined in the `appTemplates.js` file. 

### pages.json

Check below a sample structure of the file with comments to help identify what is each element

```json
{
    "defaultPage" : "index", //defines the default page if no page id is defined in url
    "menus" : //define the menus here to be referenced in the `pages` section
        {//can define different menus.
            "general": { 
                "DOMId": "topMenu" //the DOM id of the element that the menu will be rendered in 
                ,"items" : [//the menu items. Always define label in all languages and appropriate url. URL is `#p/{page.id}`
                    {"id" :"styles", "label":{"en":"Styles","el": "Style EL"}, "url" :"#p/styles"}
                    ,{"id" :"components", "label":{"en":"Components","el":"Components"}, "url" :"#"}
                    ,{"id" :"patterns", "label":{"en":"Patterns","el":"Patterns"}, "url" :"#"}
                ]
            }
            ,"styles" : {
                "DOMId": "sideMenu" 
                ,"items" :[
                    {"id" :"styles.layout", "label":{"en":"Layout","el":"Layout EL"}, "url" :"#p/styles.layout"}
                    ,{"id" :"styles.page.layout", "label":{"en":"Page layout","el":"Page layout"}, "url" :"#"}
                    ,{"id" :"styles.colour", "label":{"en":"Colour","el":"Colour"}, "url" :"#"}
                ]
            }
        }
    ,"pages" : {// define the pages 
        "index":{ //index must be the same as id 
            "id":"index",//page id
            "menus" : ["general"],//the menus of the page. Empty array if non 
            "template" : "3_3", // template reference
            "MDcontent" : [ //Markdown content. Can define more than one in a document
                {
                    "DOMId" : "main", //the DOM id of the element that the content will be rendered in 
                    "MDFile" : {"en":"content/index-en.MD","el":"content/index-el.MD"} //markdown path reference for all languages
                }
            ]
        },
        "styles":{
            "id":"styles",
            "menus" : ["general", "styles"],
            "template" : "1_3_sidemenu",
            "MDcontent" : [
                {
                    "DOMId" : "main",
                    "MDFile" : {"en" : "content/styles-en.MD", "el": "content/styles-el.MD"}
                }
            ]
        }
    }
}
```

### appTemplates.js

This file defines the templates used by the app. Check below a sample structure of the file with comments to help identify what is each element.

```js

DSFTemplates = 
{
    "templates": {//contains the template HTML to be referenced in the `pages` section
        "3_3" : "<main id='main'></main><div id='components'></div>"
        ,"1_3_sidemenu" : "<div class='row'><main class='col-md-9 order-md-last' id='main'></main>"
            +"<aside class='col-md-3 order-md-first'><nav class='nav flex-column' id='sideMenu'></nav></aside></div>"
    },
    "header" : { //Header HTML for each language. Use the appropriate language code. This is global for all pages
        "en": "<div>Header <form><select id='changeLangSel'><option value='en' selected>English</option><option value='el'>Ελληνικά</option></select></form></div>"
        ,"el" : "<div>Τίτλος <form><select id='changeLangSel'><option value='en'>English</option><option value='el' selected>Ελληνικά</option></select></form></div>"
    },
    "footer" : { //the footer HTML for each language. Use the appropriate language code. This is global for all pages
        "en": "<div>Footer</div>"
        ,"el" : "<div>Φούτερ</div>"
    }
};

```

### How to add a documentation page?

1. Create a markdown file with documentation and/or HTML. If you need to create in multiple languages create one file for each language. 
2. Update `pages.json` file with details under `pages`.
3. If you need to add it to a menu, make sure to update the appropriate entrien in the `menus` as needed. 