# AEM Clientlib Async

See [http://www.nateyolles.com/blog/2016/06/custom-aem-html5-async-clientlibs](http://www.nateyolles.com/blog/2016/06/custom-aem-html5-async-clientlibs) for a detailed description regarding this project and how Sightly clientlibs work.

Create AEM clientlibs that can output `async`, `defer`, `onload` and `crossorigin` attributes on your HTML script elements. The new clientlib component works with or without [clientlib minification](http://localhost:4502/system/console/configMgr/com.day.cq.widget.impl.HtmlLibraryManagerImpl).

The Sightly templates were updated to accept the new Sightly expression options and the ClientLib Java class was updated to accept the new bindings.

* /ui.apps/src/main/content/jcr_root/apps/clientlib-async/sightly/templates/clientlib.html
* /ui.apps/src/main/content/jcr_root/apps/clientlib-async/sightly/templates/graniteClientLib.html
* /ui.apps/src/main/content/jcr_root/apps/clientlib-async/sightly/templates/ClientLibUseObject.java

The sample page using the new clientlib component:

* /ui.apps/src/main/content/jcr_root/apps/clientlib-async-sample/components/structure/page/page.html

Included is a sample JavaScript file which loads asynchronously and excutes a function on load: 

* /ui.apps/src/main/content/jcr_root/etc/designs/clientlib-async-sample/clientlib-async-sample/script.js

## Install

A package is provided in the `/package` folder. Install it with Package Manager at [http://localhost:4502/crx/packmgr/index.jsp](http://localhost:4502/crx/packmgr/index.jsp) or you can copy the `/apps/clientlib-async` folder into your project.

## How to build

You can build and deploy to a running AEM instance with default values of port `4502`, user `admin` and password `admin`. Navigate to the `/demo` directory and run:

    mvn clean install -PautoInstallPackage

## View sample

After building and deploying, navigate to the sample page at [http://localhost:4502/content/clientlib-async-sample/en.html](http://localhost:4502/content/clientlib-async-sample/en.html). View the source to verify that the `clientlib-async-sample.js` script element has the `async` void attribute and the `onload` attribute with a value of `sayHello()`.

## Using the updated clientlibs

Use the clientlibs in your Sightly markup just as you would before (see [Sightly intro part 5: FAQ](http://blogs.adobe.com/experiencedelivers/experience-management/sightly-intro-part-5-faq/)), however, you will update the value of the data-sly-use option to point to the new clientlib component.

```
<head data-sly-use.clientLib="${'/apps/clientlib-async/sightly/templates/clientlib.html'}">

<!--/* for css+js */-->
<meta data-sly-call="${clientLib.all @ categories='your.clientlib'}" data-sly-unwrap></meta>

<!--/* only js */-->
<meta data-sly-call="${clientLib.js @ categories='your.clientlib'}" data-sly-unwrap></meta>

<!--/* only css */-->
<meta data-sly-call="${clientLib.css @ categories='your.clientlib'}" data-sly-unwrap></meta>

</head>
```

## Using 'async', 'defer', 'onload' and 'crossorigin'

Valid values for `loading` are `async` and `defer`. Valid values for `crossorigin` are `anonymous` and `use-credentials`.

```
<!--/* async */-->
<meta data-sly-call="${clientLib.js @ categories='your.clientlib', loading='async'}" data-sly-unwrap></meta>

<!--/* defer */-->
<meta data-sly-call="${clientLib.js @ categories='your.clientlib', loading='defer'}" data-sly-unwrap></meta>

<!--/* defer and onload */-->
<meta data-sly-call="${clientLib.js @ categories='your.clientlib', loading='defer', onload='myFunction()'}" data-sly-unwrap></meta>

<!--/* crossorigin */-->
<meta data-sly-call="${clientLib.all @ categories='your.clientlib', crossorigin='anonymous'}" data-sly-unwrap></meta>
```

## License

The project is licensed under Apache License 2.0.