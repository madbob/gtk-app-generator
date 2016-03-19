# gtk-app-generator

Generates a new application from a template, hiding all the boring copy-paste stuff from the developer. Includes templates for Gjs and PyGObject applications that handle autotools, i18n, gtkbuilder, gsettings, appdata, desktop files, etc.

It's a command line utility written in Python + standard library. 

## How to use

Generate a new application skeleton, running the generator tool from the repository, eg.

```
./gtk-app-generator.py com.github.user.FancyApplication -N "The Application Name" -B fancy-application -o ~/gnome --summary "A short description of the app" --url http://www.example.com/fancy-application
```

This will create a folder under `~/gnome/` called `fancy-application`, and initialize it with an GIT repository. It will take care of the initial commit too.

Switch to the application repository and set it up

```
./autogen.sh --prefix=/usr/local --libdir=/usr/local/lib64
make
```

Interesting files to edit:

 * `data/` is for data files, and `src/` for source files
 * `data/app-menu.ui` has the application menu, in GtkBuilder format
 * `data/main.ui` has the header bar and one empty grid for the application, you'll probably want to replace this with something appropriate to your app
 * `data/com.github.user.FancyApplication.appdata.xml.in` is the appdata description (for gnome-software), and `data/com.github.user.FancyApplication.desktop.in` is the desktop file (for the gnome-shell app picker)
 * `data/com.github.user.FancyApplication.gschema.xml` has the GSettings schemas
 * If you need to add one source module, edit `src/Makefile.am`
 * If you need to add one data file that can be loaded by the application (eg. CSS or image), edit `src/com.github.user.FancyApplication.gresource.xml`. You don't need to edit `data/Makefile.am`, it will be compiled and distributed automatically

