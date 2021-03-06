# dynamic-templates
Example for dynamic loading/unloading of templates.

Background: When using DukeScript in a modular system like OSGi, templates can be added as part of a module (OSGi bundle).
When the module is installed (bundle activator), the template can be registered. Templates are stored in html files.
To save resources, the html file is only loaded when the template is first loaded via template binding. 
It is also possible to unregister the template, e.g. when a module is uninstalled thus freeing up resources.

Use like this:


```
Closeable templ = TemplateRegistration.register("a", "a.html");
// do sthg with it...
templ.close();
```

Registering will add a new script tag with src pointing to an external html file. 
The template will then be lazy loaded when first used.
Subsequent attempts to register a template with the same id will throw an IllegalStateException.

Unregistering will remove the script, which makes it eligible for gc. Only who registered the template first will 
 receive the Closeable as a handle and can deregister it.

