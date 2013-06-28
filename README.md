gotk3
=====

Package gotk3 provides Go bindings for GLib 2, GDK 3, and GTK+3.  Each
component is given its own subdirectory, which is used as the import
path for the package.

Care has been taken for memory management to work seamlessly with Go's
garbage collector without the need to use or understand GObject's
floating references.

## Sample Use

The following example can be found in `gtk/examples/simple/simple.go`.
Usage of additional features is also demonstrated in the
`gtk/examples/` directory.

```Go
package main

import (
	"github.com/conformal/gotk3/gtk"
	"log"
)

func main() {
	// Initialize GTK without parsing any command line arguments.
	gtk.Init(nil)

	// Create a new toplevel window, set its title, and connect it to the
	// "destroy" signal to exit the GTK main loop when it is destroyed.
	win, err := gtk.WindowNew(gtk.WINDOW_TOPLEVEL)
	if err != nil {
		log.Fatal("Unable to create window:", err)
	}
	win.SetTitle("Simple Example")
	win.Connect("destroy", func() {
		gtk.MainQuit()
	})

	// Create a new label widget to show in the window.
	l, err := gtk.LabelNew("Hello, gotk3!")
	if err != nil {
		log.Fatal("Unable to create label:", err)
	}

	// Add the label to the window.
	win.Add(l)

	// Set the default window size.
	win.SetDefaultSize(800, 600)

	// Recursively show all widgets contained in this window.
	win.ShowAll()

	// Begin executing the GTK main loop.  This blocks until
	// gtk.MainQuit() is run. 
	gtk.Main()
}
```

## Documentation

Each package's internal `go doc` style documentation can be viewed
online without installing this package by using the GoDoc site (links
to [glib](http://godoc.org/github.com/conformal/gotk3/glib),
[gdk](http://godoc.org/github.com/conformal/gotk3/gdk), and
[gtk](http://godoc.org/github.com/conformal/gotk3/gtk) documentation).

You can also view the documentation locally once the package is
installed with the `godoc` tool by running `godoc -http=":6060"` and
pointing your browser to
http://localhost:6060/pkg/github.com/conformal/gotk3

## Installation

The gtk package requires glib and gdk packages as dependencies, so
only one `go get` is necessary for complete installation.

```bash
$ go get github.com/conformal/gotk3/gtk
```
## TODO
- Add bindings for all of GTK+
- Add tests for each implemented binding
- Add examples for intent

## License

Package gotk3 is licensed under the liberal ISC License.
