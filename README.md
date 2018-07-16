# IG-Template2  
Author:  Eric Haas

A template for building an FHIR Implemenation Guide(IG) using the IG publisher and profile spreadsheets.  This is based on the design of the [Argonaut](http://www.fhir.org/guides/argonaut/r2/) and [US-Core](http://hl7.org/fhir/us/core/) IGs.    See the [FHIR IG publisher documentation](http://wiki.hl7.org/index.php?title=IG_Publisher_Documentation)  for how to set up your local environment.

See below for a directory tree

The `source` directory contains all the new and edited content for creating an IG.  This is include pages,resources and examples , and custom navigation and logos, images and even stylesheets.  The `framework` directory and several template files located in the root directory ( for example `sd.html`) hold the static content for IG and they don't need to be changed to produce an IG.  If you want to customize your IG then you may have to edit these files and you are on your own.
The published output is in the docs directory for [GitHub Pages](https://help.github.com/articles/configuring-a-publishing-source-for-github-pages/) which is the easiest way to share your content.  See below if you are using the [ig autopublisher](https://github.com/Healthedata1/auto-ig-builder).

Shows how to create:

- Profiles
- Extensions ( complex and simple )
- CodeSystems
- ValueSets
- Logical Models [todo]
- ConformanceStatements

And the Jekyll templates and static pages to go with them...


### Rendered IG-Template at
https://healthedata1.github.io/IG-Template2/

## Setup instructions


[FHIR-IGPub-filebuilder](https://github.com/Healthedata1/FHIR-IGPub-filebuilder) can be used to automate the creation and updating of the `ig.json` and `ig.xml` files based on the content in the definitions.csv file and in `resources` and `examples` directories.  See the inline comments for how to use.  

## IG Generation Workflow using IG Template2 and IG Definitions builder

1. locally start in IG-Template2 directory

1. run bash file `pub3.sh` with argument of directory name where source resource, examples and pages are located

- Optional Parameters
  - -d create definitions file, will trigger definitions.py to run and create new ig.xml and ig.json file in both IG-Template2 and in source directory
  - -s parameter = source directory assuming sharing same root directory if give relative path. no source will look for source directory in current directory
  - -t parameter = N/A for no terminology server (run faster and offline) default is default fhir term server.

  e.g. to create a new ig.json and ig.xml based on the definitions.csv file  in the ../Argo-Scheduling directory and run without a term server:
       bash pub3.sh -d -s Argo-Scheduling -t

1. Output will be in IG-Template2 docs folder
1. for [autopublishing from GitHib](https://github.com/Healthedata1/auto-ig-builder) will need to:
   -  add these (static) files and folders to source:
      - base.html
      - dependencies
      - ex.html
      - format.html
      - framework
      - generated_output
      - sd-definitions.html
      - sd-mappings.html
      - sd.html
   -  upload generated_output/txCache to Git
   -  add output folder and don't need to upload docs
   -  update definitions file to specify output instead of docs
   (actually is may be easier to add the source files to the Template and rename it)
1. autogenerated includes will be in source pages/\_includes directory
1. Updates to pages will trigger ig-publisher to rebuild

Directory tree structure:

~~~

.
├── README.md
├── base.html
├── definitions.csv
├── docs
├── ex.html
├── format.html
├── framework
│   ├── _includes
│   │   ├── breadcrumbs.html
│   │   ├── container-end.html
│   │   ├── container-start.html
│   │   ├── footer.html
│   │   ├── header.html
│   │   ├── img.html
│   │   ├── navbar.html
│   │   └── profile-tabs.html
│   ├── _layouts
│   │   ├── default.html
│   │   └── fhir-artifact.html
│   └── assets
│       ├── css
│       │   ├── bootstrap-fhir.css
│       │   ├── bootstrap-glyphicons.css
│       │   ├── bootstrap.css
│       │   ├── jquery-ui.css
│       │   ├── jquery-ui.min.css
│       │   ├── jquery-ui.structure.css
│       │   ├── jquery-ui.structure.min.css
│       │   ├── jquery-ui.theme.css
│       │   ├── jquery-ui.theme.min.css
│       │   ├── project.css
│       │   ├── pygments-manni.css
│       │   └── xml.css
│       ├── fonts
│       │   ├── glyphiconshalflings-regular.eot
│       │   ├── glyphiconshalflings-regular.otf
│       │   ├── glyphiconshalflings-regular.svg
│       │   ├── glyphiconshalflings-regular.ttf
│       │   └── glyphiconshalflings-regular.woff
│       ├── ico
│       │   ├── apple-touch-icon-57-precomposed.png
│       │   ├── apple-touch-icon-72-precomposed.png
│       │   ├── apple-touch-icon-114-precomposed.png
│       │   ├── apple-touch-icon-144-precomposed.png
│       │   ├── favicon.ico
│       │   └── favicon.png
│       ├── images
│       │   ├── cat.jpg
│       │   ├── fhir-logo-www.png
│       │   ├── fhir-logo.png
│       │   ├── hl7-logo.png
│       │   ├── logo_ansinew.jpg
│       │   ├── search.png
│       │   ├── stripe.png
│       │   └── target.png
│       └── js
│           ├── anchor.min.js
│           ├── bootstrap.min.js
│           ├── fhir.js
│           ├── html5shiv.js
│           ├── jquery-1.11.1.js
│           ├── jquery-1.11.1.min.js
│           ├── jquery-1.11.1.min.map
│           ├── jquery-ui.js
│           ├── jquery-ui.min.js
│           ├── jquery.js
│           ├── respond.min.js
│           └── xml.js
├── generated_output
│   ├── qa
│   ├── temp
│   └── txCache
├── ig.json
├── my_notes
│   ├── dir_tree.txt
│   ├── full_tree.txt
│   └── local_workflowmd
├── pub-notx.sh
├── pub.sh
├── pub2.sh
├── pub3.sh
├── sd-definitions.html
├── sd-mappings.html
├── sd.html
└── source
    ├── examples
    │   └── obs.xml
    ├── pages
    │   ├── _includes
    │   │   ├── LogicalModel-intro.md
    │   │   ├── LogicalModel-search.md
    │   │   ├── LogicalModel-summary.md
    │   │   ├── bt-intro.md
    │   │   ├── bt-search.md
    │   │   ├── bt-summary.md
    │   │   ├── extension-blah-intro.md
    │   │   ├── extension-blah-search.md
    │   │   ├── extension-blah-summary.md
    │   │   ├── extension-complex-intro.md
    │   │   ├── extension-complex-search.md
    │   │   ├── extension-complex-summary.md
    │   │   ├── foo-intro.md
    │   │   ├── foo-search.md
    │   │   ├── foo-summary.md
    │   │   ├── ifr-intro.md
    │   │   ├── ifr-search.md
    │   │   ├── ifr-summary.md
    │   │   ├── logo.md
    │   │   ├── menu.md
    │   │   ├── nav-tabs.html
    │   │   ├── publish-box.html
    │   │   ├── template-basic-intro.md
    │   │   ├── template-basic-search.md
    │   │   └── template-basic-summary.md
    │   ├── assets
    │   │   ├── css
    │   │   └── images
    │   │       └── org_logo.jpg
    │   ├── capstatements.md
    │   ├── downloads.md
    │   ├── guidance.md
    │   ├── history.md
    │   ├── index.md
    │   ├── page_template_library
    │   │   ├── capstatements.md
    │   │   ├── downloads.md
    │   │   ├── examples.md
    │   │   ├── extensions.md
    │   │   ├── guidance.md
    │   │   ├── history.md
    │   │   ├── index.md
    │   │   ├── operations.md
    │   │   ├── profiles.md
    │   │   ├── searchparams.md
    │   │   ├── security.md
    │   │   ├── structuremaps.md
    │   │   ├── terminology.md
    │   │   ├── toc.md
    │   │   └── todo.md
    │   ├── profiles.md
    │   ├── structuremaps.md
    │   ├── terminology.md
    │   ├── toc.md
    │   └── todo.md
    └── resources
        ├── bt-profile-spreadsheet.xml
        ├── capabilitystatement-client.xml
        ├── capabilitystatement-server.xml
        ├── drafts
        │   ├── patient-on-usprofile-spreadsheet.xml
        │   ├── searchparameter-blah.xml
        │   ├── structuredefinition-template-basic2.xml
        │   └── structuredefinition-template-profile-on-profile2.xml
        ├── identifier-free-reference-profile-spreadsheet.xml
        ├── ig.xml
        ├── logical-model-xpreadsheet.xml
        ├── structuremap-Foo.xml
        └── template-profile-spreadsheet.xml

25 directories, 133 files

~~~