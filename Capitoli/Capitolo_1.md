## Importare le librerie
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
Prima di procedere oltre è necessario chiarire i concetti di funzione, classe e oggetto all'interno di Pyhton, in modo da poter comprendere meglio le strtture e la sintassi ch andremo ad utilizzare.

### Concetto di funzione
La definizione più semplice e corretta che possiamo dare di una funzione all'interno di un linguaggio di programmazione è "insieme di istruzioni riutilizzabili". Difatti una funzione altro non è che un insieme di istruzioni che possiamo richiamare a comando in un qualunque punto del nostro programma. Una funzione può essere utilizza a priori senza passaggio di variabili dall'esterno, può essere utilizzata acquisendo varibili esterne ed è possibile far uscire dei dati dal suo interno attraverso l'istruzione return. In ogni caso, tutte e funzioni vanno dichiarate prima dell'inzio del programma principale o "main". Vediamo tre esempi di funzioni con queste caratteristiche :

Esempio di funzione senza passaggio di variabili :
```
# DEFINIZIONE DI UNA FUNZIONE SENZA PASSAGGIO DI VARIABILI
def funzione_1 () :
  a = 2
  b = 5
  c = (a + b)*2
  print("funzione uno stampa sempre ",c)

# INZIO MAIN

# RICHIAMO LA FUNZIONE
funzione_1()
```

Esempio di funzione con passaggio di variabili :
```
# DEFINIZIONE DI UNA FUNZIONE CON PASSAGGIO DI VARIABILI
def funzione_2 (a, b) :
  c = (a + b)*2
  print("funzione due stampa ", c, "a seconda dei parametri "a" e "b" che gli passiamo quando la richiamiamo")

# INIZIO MAIN

# DEFINISCO A E B A MIO PIACERE
a = 4
b = input("Inserisci numero B : ")

# RICHIAMO LA FUNZIONE PASSANDO LE VARIABILI
funzione_2(a, b)
```

Un altra cosa utile da ricordare è il funzionamento dell'istruzione "return" all'interno delle funzioni. Essa ci permette di portare fuori dalla funzione uno più valori, siano essi numeri, stringhe o booleani. Vediamo un esempio dell'uso di return :
```
# DEFINIZIONE DI UNA FUNZIONE CHE UTILIZZA RETURN
def funzione_3(b) :
  a = 3
  c = (a + b)*2

  # PERMETTO L'USCITA DELLA VARIABILE C DALLA FUNZIONE
  return c

# INIZIO MAIN

b = input("Inserisci il numero B : ")
# COPIO LA VARIABILE C DELLA FUNZIONE NELLA VARIABILE D DEL PROGRAMMA
d = funzione_3(b) 
print("Il risultato è : ", d)
```



### Concetto di classe ed oggetto
La classe è un concetto fondamentale della programmazione ad oggetti e può essere definita come il modello o progetto di un oggetto. Un buon esempio per comprendere il legame ed il funzionamento di classi ed oggetti è il seguente :
> Immaginiamo la classe come un kit molto completo per preparare le torte. In questo kit sono presenti lo stampo per la torta che funge da contenitore e da ricetta per la stessa (la classe), gli ingredienti (le proprietà / caratteristiche dell'oggetto) e le varie occasioni per cui  preparare la torta (i metodi della classe / funzioni dell'oggetto).
> Di conseguenza otteniamo :
> - Lo stampo / contenitore e ricetta della torta : **la classe**
> - L'insieme degli ingredienti della torta : **le proprietà / caratteristiche della classe**
> - Le varie occasioni per preparare la torta : **I metodi della classe / funzioni dell'oggetto**

La domanda che vi sorgerà spontanea è : "Dove e come rientra l'oggetto in questo insieme ?" **L'oggetto non è altro che la torta**. Noi possiamo avere avere una classe in grado di fornire diversi gusti di torte. Approfondiamo meglio la questione con esempio semplificato :

```
# CREO LA CLASSE DELLA TORTA
class torta () :

  # DEFINISCO LE PROPRIETÀ / CARATTERISTICHE DELLA TORTA
  grandezza = ""
  gusto = ""

  # DEFINISCO ALCUNE OCCASIONI PER CUI VIENE REALIZZATA
  def compleanno () :
    print("Tanti auguri ! Ecco la tua torta !")

  def successo_lavorativo () :
    print("Complimenti per il tuo successo ! Ecco la tua torta !")
  
```
Ora che abbiamo una maggiore consapevolezza sul funzionamento logico di una classe passiamo ad una spiegazione più formale e tecnicamente accurata. L'oggetto per poter essere costruito a partire dalla classe necessita di un costruttore, del resto nessuna torta si prepara da sola. Ciò che consente alla classe di fornirci un oggetto è il metodo costruttore `__init__`, detto anche inizializzatore. Il metodo costruttore `__init__` per poter funzionare appieno necessita del parametro`self` al suo interno. Il parametro self serve a distingure le proprietà dell'oggetto da eventuali variabili locali di lavoro utilizzate all'interno della classe, le quali non devono essere considerate come proprietà dell'oggetto. Esso si chiama self poichè riferisce a se stesso, ossia al costruttore `__init___`, che le variabili che contengono self come apice sono delle proprietà di cui tenere conto quando il costruttore `__init__` andrà a generare il nostro oggetto. Vediamo meglio la sintassi ed il funzionamento di `__init__` e `self` con un esempio :
```
# CREO LA CLASSE DELLA TORTA
classe torta () :

  # INSERISCO IL METODO COSTRUTTORE
  def __init__(self)

    # PROPRIETÀ VARIE DELLA TORTA...
    self.grandezza = ""
    self.gusto = ""
  
    # VARIABILI DI LAVORO
    casa = ""
    barbabietola = ""
```
Adesso che abbiamo chiarito come viene generato un oggetto è necessario riempire le proprietà all'interno della classe con dati utili. Per farlo dobbiamo fornire alla funzione `__init__` la predisposizione per accettare dati dall'esterno della classe. Per fare ciò dobbiamo passare al costruttore altri argomenti oltre a `self` e ci sono tipi di argomenti che possiamo usare a seconda delle nostre esigenze :



- **Argomenti posizionali:** Utilizzando gli argomenti posizionali semplicemente si dice alla funzione che le arriveranno tre fondi di dati in un preciso ordine. Non vengono specificate le origini e viene a priori definito il numero di argomenti che verranno passati, i quali devono coincedere con quelli che la funzione si aspetta. Vediamo un esempio :
```
def funzione_1 (argomento_1, argomento_2, argomento_3) :
  # CONTENUTO DELLA FUNZIONE

#MAIN

argomento_a = 3
argomento_b = "ciao"
argomento_c = "True"

#RICHIAMO LA FUNZIONE
funzione_1 (argomento_b, argomento_c, argomento_a ) # ARGOMENTO_B = ARGOMENTO_1; ARGOMENTO_C = ARGOMENTO_2; ARGOMENTO_A = ARGOMENTO_3

```



- **Argomenti per parola chiave:** Utilizzando di argomenti per parola chiave comunichiamo alla funzione di aspettarsi un numero definito di argomenti ed anche il nome specifico dell'argomento che gli verrà passato. In questo caso gli argomenti possono essere passati alla funzione in un qualunque ordine poichè viene utilizzato come riferimento il nome dell'argomento. Vediamo un esempio :
```
ciao
```

































