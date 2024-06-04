# Guida all'utilizzo di GTK 4.0 ed Adwaita 1.0 in Python
Questo repository vuole essere una semplice introduzione all'uso di GTK 4 ed Adwaita con il linguaggio Python. Attraverso brevi spiegazioni ed esempi scopriremo le fondamenta della programmazione ad oggetti attraverso l'uso di GTK 4 ed Adwaita fino ad arrivare alla creazione di programmi per GNU-Linux perfettamente integrati in GNOME.


## Librerie da importare
Per poter iniziare ad utilizzare GTK è necessario importare nel nostro file Python alcune librerie utilizzando il seguente codice :
```
  import sys, gi
  
  gi.require_version('Gtk', '4.0')
  gi.require_version('Adw', '1')
  
  from gi.repository import Gtk, Adw, Gdk, Pango, Gio, GLib
```
#### Spiegazione del codice : 
Attraverso questo comando abbiamo importato i moduli ```sys``` e ```gi```, successivamente abbiamo chiesto a quest'ultimo di importare i successivi moduli utilizzando le versioni di ```GTK``` e ```Adwaita``` nelle versione a noi necessarie. 
Infine abbiamo importato i moduli :
```
Gtk, Adw, Gdk, Pango, Gio, GLib
```
Nonostante per la prima parte siano necessari sono ```Gtk``` ed ```Adw```, penso sia meglio importare sin da subito tutto ciò che possa esserci utile nello sviluppare i nostri primi programmi.



## Concetto di classe, oggetto e funzione in Python
