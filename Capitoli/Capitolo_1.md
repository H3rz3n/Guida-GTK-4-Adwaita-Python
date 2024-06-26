# Importare le librerie
Per poter iniziare ad utilizzare GTK è necessario importare nel nostro file Python alcune librerie utilizzando il seguente codice :

```python 
# IMPORTO I MODULI PRINCIPALI
import sys, gi

# SPECIFO LE VERSIONI DI GTK ED ADW CHE ANDREMO AD UTILIZZARE  
gi.require_version('Gtk', '4.0')
gi.require_version('Adw', '1')

# IMPORTO I MODULI SECONDARI DALLA RACCOLTA GI
from gi.repository import Gtk, Adw, Gdk, Pango, Gio, GLib
```
### Spiegazione del codice : 
Attraverso questo comando abbiamo importato i moduli ```sys``` e ```gi```, successivamente abbiamo specificato a quest'ultimo quali versioni vogliamo utilizzare di ```GTK``` e ```Adwaita```. 
Infine abbiamo importato i moduli :
```
Gtk, Adw, Gdk, Pango, Gio, GLib
```
Nonostante per la prima parte della guida siano necessari solo ```Gtk``` ed ```Adw```, penso sia meglio importare sin da subito tutto ciò che possa esserci utile nello sviluppare i nostri primi programmi.



# Concetto di classe, oggetto e funzione in Python
Prima di procedere oltre è necessario chiarire i concetti di funzione, classe e oggetto all'interno di Pyhton, in modo da poter comprendere meglio le strtture e la sintassi che andremo ad utilizzare successivamente.

## Concetto di funzione
La definizione più semplice e corretta che possiamo dare di una funzione all'interno di un linguaggio di programmazione è "insieme di istruzioni riutilizzabili". Difatti una funzione altro non è che un insieme di istruzioni che possiamo richiamare in un qualunque punto del nostro programma. Una funzione può essere sia utilizzata a priori senza passaggio di argomenti (variabili o costanti) dall'esterno, sia essere utilizzata acquisendo argomenti esterni. Inoltre è possibile far uscire dei dati dal suo interno attraverso l'istruzione return. In ogni caso, tutte le funzioni vanno dichiarate prima dell'inzio del programma principale o "main". Vediamo tre esempi di funzioni con le caratteristiche sopra elencate :

### Esempio di funzione senza passaggio di argomenti :
```python
# DEFINIZIONE DI UNA FUNZIONE SENZA PASSAGGIO DI ARGOMENTI
def funzione_1 () :

	# CONTENUTO DELLA FUNZIONE
	a = 2
	b = 5
	c = (a + b)*2
	print("funzione uno stampa sempre ",c)

# INZIO MAIN

# RICHIAMO LA FUNZIONE
funzione_1()
```

### Esempio di funzione con passaggio di argomenti :
```python
# DEFINIZIONE DI UNA FUNZIONE CON PASSAGGIO DI ARGOMENTI
def funzione_2 (a, b) :

	# CONTENUTO DELLA FUNZIONE
	c = (a + b)*2
  	print("funzione due stampa ", c, "a seconda dei parametri 'a' e 'b' che gli passiamo quando la richiamiamo")

# INIZIO MAIN

# DEFINISCO A E B A MIO PIACERE
a = 4
b = int(input("Inserisci numero B : "))

# RICHIAMO LA FUNZIONE PASSANDO GLI ARGOMENTI
funzione_2(a, b)
```

### Esempio di funzione con parametro return :
```python
# DEFINIZIONE DI UNA FUNZIONE CHE UTILIZZA RETURN
def funzione_3(b) :

	# CONTENUTO DELLA FUNZIONE
  	a = 3
  	c = (a + b)*2

  	# PERMETTO L'USCITA DELLA VARIABILE C DALLA FUNZIONE
  	return c

# INIZIO MAIN

# PRENDO IN INPUT B
b = int(input("Inserisci il numero B : "))

# COPIO LA VARIABILE C DELLA FUNZIONE NELLA VARIABILE D NEL MAIN
d = funzione_3(b)

# STAMPO LA VARIABILE D
print("Il risultato è : ", d)
```

### Introduzione e spiegazione delle tipologie di argomenti nelle funzioni :
È importante sapere che vi sono diversi tipologie di argomenti che possiamo passare alle funzioni ed ognuno ha caratteristiche specifiche a seconda delle per rispondere a varie esigenze. Spesso le varie tipologie possono anche essere utilizzate contemporaneamente, seppur richiedendo il giusto ordinamento. Analizziamo la lista completa e spieghiamole con alcuni esempi :

- **01 | Argomenti posizionali:** Quando utilizziamo gli argomenti posizionali comunichiamo alla funzione che le arriveranno un preciso numero di fonti di dati in un preciso ordine. Non vengono specificate le origini, ma gli argomenti passati alla funzione devono coincedere in numero con quelli che la funzione si aspetta di ricevere. Vediamo un esempio :
```python
# CREAZIONE DELLA FUNZIONE
def funzione_1 (argomento_1, argomento_2, argomento_3) :

  	# CONTENUTO DELLA FUNZIONE
  	print(argomento_1, argomento_2, argomento_3)

# MAIN

argomento_a = "3"
argomento_b = "ciao"
argomento_c = "True"

# RICHIAMO LA FUNZIONE
funzione_1 (argomento_b, argomento_c, argomento_a )

# GLI ARGOMENTI VENGONO CARICATI NELLA FUNZIONE
# CON LA SEGUENTE CORRISPONDENZA :
# ARGOMENTO_B = ARGOMENTO_1
# ARGOMENTO_C = ARGOMENTO_2
# ARGOMENTO_A = ARGOMENTO_3

```



- **02 | Argomenti per parola chiave:** Quando utilizziamo gli argomenti per parola chiave comunichiamo alla funzione di aspettarsi un numero definito di argomenti ed anche il nome/tipologia specifica dell'argomento che gli verrà passato. In questo caso gli argomenti possono essere passati alla funzione in un qualunque ordine poichè viene utilizzato come riferimento il nome dell'argomento. Vediamo un esempio :
```python
# CREAZIONE DELLA FUNZIONE
def funzione_2 (argomento_1, argomento_2, argomento_3) :

	# CONTENUTO DELLA FUNZIONE
  	print(argomento_1, argomento_2, argomento_3)

# MAIN

argomento_nome = "Mario"
argomento_cognome = "Rossi"
argomento_eta = "17"

# RICHIAMO LA FUNZIONE
funzione_2 (argomento_1 = argomento_nome, argomento_2 = argomento_cognome, argomento_3 = argomento_eta)

# GLI ARGOMENTI VENGONO CARICATI NELLA FUNZIONE
# CON LA SEGUENTE CORRISPONDENZA :
# ARGOMENTO_1 = ARGOMENTO_NOME
# ARGOMENTO_2 = ARGOMENTO_COGNOME
# ARGOMENTO_3 = ARGOMENTO_ETA
```


- **03 | Argomenti di default:** Quando utilizziamo gli argomenti di default stiamo comunicando alla funzione che gli forniremo uno o più dati in modo garantito. È importante sottolineare che i dati all'interno dell'argomento che noi forniamo possono essere sovrascritti in qualunque momento. Ciò che è garantito è solo un dato di base, il quale è utile per evitare di ricevere errori dalla funzione in caso non si passino tutti gli argomenti promessi. È importante però tenere a mente che *gli argomenti di default devono essere sempre gli ultimi passati alla funzione*. Vediamo un esempio :
```python
# CREAZIONE DELLA FUNZIONE
def funzione_3 (argomento_1, argomento_3, argomento_2 = "CIAO !") :

	# CONTENUTO DELLA FUNZIONE
	print(argomento_1, argomento_2, argomento_3)

# MAIN

argomento_a = "3"
argomento_b = "Salve !"
argomento_c = "True"

# RICHIAMO LA FUNZIONE
funzione_3 (argomento_a, argomento_c, argomento_b)

# GLI ARGOMENTI VENGONO CARICATI NELLA FUNZIONE
# CON LA SEGUENTE CORRISPONDENZA :
# ARGOMENTO_1 = ARGOMENTO_A
# ARGOMENTO_2 = ARGOMENTO_B
# ARGOMENTO_3 = ARGOMENTO_C
```



- **04 | Argomenti posizionali arbitrari:** Quando utilizziamo gli argomenti posizionali arbitrari sitamo comunicando alla funzione che non sappiamo quanti argomenti gli passeremo, ma che essi saranno passati in un preciso ordine. Questi dati veranno tenuti in memoria  dentro la funzione all interno di un tuple. Ciò implica che gli argomenti verranno archiviati all'interno della funzione in ordine di presentazione in un unica sezione. Lo standard informale e comune vuole si che utilizzi il parametro `*args` per passare i vari parametri, ma sintattatticamente parlando possiamo utilizzare un qualunque nome purchè sia preceduto da un asterisco. Vediamo un esempio :
```python
# CREAZIONE DELLA FUNZIONE
def funzione_4 (*args) :

	# STAMPIAMO TUTTE GLI ARGOMENTI CARICATI NELLA FUNZIONE
	for campo in args :
	print(campo)

# MAIN

argomento_a = "Lorenzo"
argomento_b = "Camilla"
argomento_c = "Gianmarco"

# RICHIAMO LA FUNZIONE
funzione_4 (argomento_a, argomento_c, argomento_b)

# GLI ARGOMENTI VENGONO CARICATI NELLA FUNZIONE
# CON LA SEGUENTE CORRISPONDENZA :
# ARGS =
#ARGOMENTO_A
#ARGOMENTO_C
#ARGOMENTO_B
```



- **05 | Argomenti per parola chiave arbitrari:** Quando utilizziamo gli argomenti per parola chiave arbitrari stiamo comunicando alla funzione che non sappiamo quanti argomenti gli passeremo, ma sappiamo il nome/tipologia di questi. Questi dati veranno tenuti in memoria dentro la funzione all interno di un dizionario. Ciò implica che gli argomenti verranno acquisiti e gestiti all'interno della funzione sequendo uno una schema chiave-valore, cioè in due sezioni. Lo standard informale e comune vuole si che utilizzi il parametro `*kwargs` per passare i vari parametri, ma sintattatticamente parlando possiamo utilizzare un qualunque nome purchè sia preceduto da due asterischi. Vediamo un esempio :
```python
# CREAZIONE DELLA FUNZIONE
def funzione_5 (**kwargs) :

	# STAMPIAMO TUTTE LE COMBINAZIONI CHIAVE-VALORE CARICATE NELLA FUNZIONE
	for chiave, valore in kwargs.items(): 
	print(chiave, ":", valore)

# MAIN

argomento_nome = "Mario"
argomento_cognome = "Rossi"
argomento_eta = "17"

# RICHIAMO LA FUNZIONE
funzione_5 (Nome = argomento_nome, Cognome = argomento_cognome, Eta = argomento_eta)

# GLI ARGOMENTI VENGONO CARICATI NELLA FUNZIONE
# CON LA SEGUENTE CORRISPONDENZA :
# KWARGS =
# CHIAVE    VALORE
#-------------------
# NOME      MARIO
# COGNOME   ROSSI
# ETA       17
```



- **06 | Argomenti *solo* per parola chiave:** Quando utilizziamo questa opzione la funzione accetterà solo argomenti per parola chiave. Per poter ottenere questa funzionalità è necessario dichiarare come primo argomento ad inizio funzione un asterisco. Vediamolo con un esempio :
```python
# CREAZIONE DELLA FUNZIONE
def funzione_6 (*, argomento_1, argomento_2, argomento_3) :

	# CONTENUTO DELLA FUNZIONE
	print(argomento_1, argomento_2, argomento_3)

# MAIN

argomento_nome = "Mario"
argomento_cognome = "Rossi"
argomento_eta = "17"

# RICHIAMO LA FUNZIONE
funzione_6 (argomento_1 = argomento_nome, argomento_2 = argomento_cognome, argomento_3 = argomento_eta)

# GLI ARGOMENTI VENGONO CARICATI NELLA FUNZIONE
# CON LA SEGUENTE CORRISPONDENZA :
# ARGOMENTO_1 = ARGOMENTO_NOME
# ARGOMENTO_2 = ARGOMENTO_COGNOME
# ARGOMENTO_3 = ARGOMENTO_ETA
```


## Concetto di classe ed oggetto
#### Introduzione e spiegazione del concetto di classe ed oggetto :
La classe è un concetto fondamentale della programmazione ad oggetti e può essere definita come il modello o progetto di un oggetto. Un buon esempio per comprendere il legame ed il funzionamento di classi ed oggetti è il seguente :
> Immaginiamo la classe come un kit molto completo per preparare le torte. In questo kit sono presenti lo stampo per la torta che funge da contenitore e da ricetta per la stessa (la classe), gli ingredienti (le proprietà / caratteristiche dell'oggetto) e le varie occasioni per cui  preparare la torta (i metodi della classe / funzioni dell'oggetto).
> Di conseguenza otteniamo :
> - Lo stampo / contenitore e ricetta della torta : **la classe**
> - L'insieme degli ingredienti della torta : **le proprietà / caratteristiche della classe**
> - Le varie occasioni per preparare la torta : **I metodi della classe / funzioni dell'oggetto**

La domanda che vi sorgerà spontanea è : "Dove e come rientra l'oggetto in questo insieme ?" **L'oggetto non è altro che la torta**. Approfondiamo meglio la questione con esempio semplificato :

```python
# CREAZIONE LA CLASSE DELLA TORTA
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
### Introduzione e spiegazione del costruttore __init__ e dell'argomento self
Ora che abbiamo una maggiore consapevolezza sul funzionamento logico di una classe passiamo ad una spiegazione più formale e tecnicamente accurata. L'oggetto per poter essere costruito a partire dalla classe necessita di un costruttore, del resto nessuna torta si prepara da sola. Ciò che consente alla classe di fornirci un oggetto è il metodo costruttore `__init__`, detto anche inizializzatore. Il metodo costruttore `__init__` per poter funzionare appieno necessita del parametro`self` al suo interno. Il parametro `self` serve a distingure le proprietà dell'oggetto da eventuali variabili locali di lavoro utilizzate all'interno della classe, le quali non devono essere considerate come proprietà dell'oggetto. Esso si chiama self poichè riferisce a se stesso, ossia al costruttore `__init___`, che le variabili che contengono self come apice sono delle proprietà di cui tenere conto quando il costruttore `__init__` andrà a generare il nostro oggetto. Vediamo meglio la sintassi ed il funzionamento di `__init__` e `self` con un esempio :
```python
# CREAZIONE LA CLASSE DELLA TORTA
class torta () :

 	# INSERISCO IL METODO COSTRUTTORE INIT
  	def __init__ (self) :

		# PROPRIETÀ DELLA TORTA...
    		self.grandezza = ""
    		self.gusto = ""
  
    		# VARIABILI DI LAVORO
		casa = ""
		barbabietola = ""
```





### Introduzione e spiegazione del passaggio di argomenti nelle classi
Il costruttore `__init__` oltre a self permette l'utilizzo di altri argomenti passati dal main del programma. Ciò ci permette di popolare di dati dinamicante le proprietà di una classe. Vediamolo meglio con un esempio :

```python
# CREAZIONE DELLA CLASSE
class torta ():

	# UTILIZZO DEL COSTRUTTORE INIT
	def __init__(self, grandezza, gusto, proprietario):

		# PROPRIETÀ DELLA CLASSE
		self.grandezza = grandezza
		self.gusto = gusto
		self.proprietario = proprietario

	# CREAZIONE DEL METODO (FUNZIONE) PER MOSTRARE L'OGGETTO	
	def stampa_info(self):

        	# UTILIZZO RETURN PER EVITARE UNA DOPPIA STAMPA
		return(f"La torta è grande {self.grandezza}, ha il gusto {self.gusto} ed appartiene a {self.proprietario}")

# INIZIO MAIN

# CREAZIONE DELL'OGGETTO DOLCE_1
dolce_1  = torta("20cm", "cioccolato", "Carlo")

# CREAZIONE DELL'OGGETTO DOLCE_2
dolce_2 = torta("30cm", "crema", "Arianna")

# STAMPO L'OGGETTO TORTA_1
print(dolce_1.stampa_info())

# STAMPO L'OGGETTO TORTA_2
print(dolce_2.stampa_info())
```





### Introduzione e spiegazione dell'ereditarietà delle classi
Ogni classe può "ereditare", ossia far suoi, le proprietà ed i metodi di un altra classe. Utilizzando l'ereditarietà delle classi è possibile risparmiare numerose righe di codice, incrementare la leggibilità del proprio lavoro e semplificare eventuali manutenzioni e modifiche. In caso di ereditarietà le classi vengono definite come genitori/madre e figlia/e, in cui la classe che eredità è la figlia e quella che fornice il codice è la madre. Possono esistere più classi figlie che ereditano da una stessa classe madre, ed a propria volta possono esistere classi figlie che ereditano da altre classi figlie. Vediamo la sintassi con un esempio :
```python
# CREAZIONE DELLA CLASSE GENITORE/MADRE
class dessert ():

    # UTILIZZO DEL COSTRUTTORE INIT
	def __init__(self, grandezza, gusto, proprietario):

		# PROPRIETÀ DELLA CLASSE MADRE
		self.grandezza = grandezza
		self.gusto = gusto
		self.proprietario = proprietario

# CREAZIONE DELLA CLASSE FIGLIA
# ESSA EREDITA LE PROPRIETÀ ED I METODI DELLA CLASSE MADRE DESSERT
class torta (dessert):

	# CREAZIONE DEL METODO (FUNZIONE) PER MOSTRARE L'OGGETTO	
	def stampa_info(self):

        	# UTILIZZO RETURN PER EVITARE UNA DOPPIA STAMPA
		return(f"La torta è grande {self.grandezza}, ha il gusto {self.gusto} ed appartiene a {self.proprietario}")

# INIZIO MAIN

# CREAZIONE DELL'OGGETTO DOLCE_1
dolce_1  = torta("20cm", "cioccolato", "Carlo")

# CREAZIONE DELL'OGGETTO DOLCE_2
dolce_2 = torta("30cm", "crema", "Arianna")

# STAMPO L'OGGETTO TORTA_1
print(dolce_1.stampa_info())

# STAMPO L'OGGETTO TORTA_2
print(dolce_2.stampa_info())
```





### Introduzione e spiegazione della funzione super()
Per poter aggiugere proprietà alla classe figlia, ed eventualmente al suo interno sovrascrivere alcune proprietà della classe madre, è necessario utilizzare la funzione `super()` subito dopo la funzione `init`. Essa inoltre ci permette di poter acquisire nuovi argomenti all'interno della classe figlia, rendendola quindi un espansione con tutte le funzionalità della classe madre.



Quando si utilizza l'ereditarietà è necessario utilizzare la funzione `super` per ereditare il costruttore `init` della classe madre. Il suo utilizzo ci consente di poter acquisire argomenti, aggiungere proprietà e modificare internamente alla classe figlia le proprietà della classe madre, rendendola quindi un espansione con tutte le funzionalità di quest'ultima. Vediamo il suo utilizzo con esempio :
```python
# CREAZIONE DELLA CLASSE GENITORE/MADRE
class dessert ():

    # UTILIZZO DEL COSTRUTTORE INIT
	def __init__ (self, grandezza, gusto, proprietario):

		# PROPRIETÀ DELLA CLASSE MADRE
		self.grandezza = grandezza
		self.gusto = gusto
		self.proprietario = proprietario

# CREAZIONE DELLA CLASSE FIGLIA
class torta (dessert):
    
	# UTILIZZO DEL COSTRUTTORE INIT NELLA CLASSE FIGLIA
	def __init__ (self,grandezza, gusto, proprietario, freschezza):
		
		# UTILIZZO LA FUNZIONE SUPER PER EREDITARE 
		# IL COSTRUTTORE INIT DELLA CLASSE MADRE
		super().__init__(grandezza, gusto, proprietario)

		# PROPRIETÀ DELLA CLASSE FIGLIA
		self.freschezza = freschezza


	# CREAZIONE DEL METOTO (FUNZIONE) PER MOSTRARE L'OGGETTO	
	def stampa_info(self):

	        # UTILIZZO RETURN PER EVITARE UNA DOPPIA STAMPA
		return(f"La torta è grande {self.grandezza}, ha il gusto {self.gusto} ed appartiene a {self.proprietario}. La torta è {self.freschezza}")

# INIZIO MAIN

# CREAZIONE DELL'OGGETTO DOLCE_1
dolce_1  = torta("20cm", "cioccolato", "Carlo", "appena fatta")

# CREAZIONE DELL'OGGETTO DOLCE_2
dolce_2 = torta("30cm", "crema", "Arianna", "fatta ieri")

# STAMPO L'OGGETTO TORTA_1
print(dolce_1.stampa_info())

# STAMPO L'OGGETTO TORTA_2
print(dolce_2.stampa_info())
```




## Creazione di una finestra di prova
Fatte queste doverese premesse, possiamo entrare nell'vivo dell'azione creando la nostra prima finestra di prova vuota utilizzando Gtk ed Adwaita. Creeremo due classi, una che conterrà la macro-finestra e che ci permetterà di mandare a schermo la finestra ed una con GTK, che sarà il contenitore in cui andremo ad inserire successivamente i vari elementi grafici, i widget.
- **Classe Adwaita:** Questa classe è la classe figlia di `Adw.Application`, ossia una classe con cui definiamo il nostro utilizzare Adwaita come tema per il nostro programma Gtk. Al suo interno si trovano il trigger Gtk per segnalare l'apertura e l'istruzione che manda a schermo la finestra.

- **Classe Gtk:** Questa classe è la classe figlia di `Gtk.ApplicationWindow`, ossia la classe con cui generiamo la finestra principale del nostro programma Gtk. Al suo interno troviamo due parametri che impostano il titolo della finestra e la sua dimensione all'apertura.

Nel main del programma sono presenti le istruzioni per generare la finestra ed avviarla, assieme all'istruzione per specificare l'ID del programma. Su quest ultimo dettaglio ci concentreremo successivamente, adesso vediamo il codice commentato :
  
```python
# IMPORTO I MODULI PRINCIPALI
import sys, gi

# SPECIFO LE VERSIONI DI GTK ED ADW CHE ANDREMO AD UTILIZZARE  
gi.require_version('Gtk', '4.0')
gi.require_version('Adw', '1')

# IMPORTO I MODULI SECONDARI DALLA RACCOLTA GI
from gi.repository import Gtk, Adw, Gdk, Pango, Gio, GLib



# CREAZIONE DELLA CLASSE CONTENITORE DEI WIDGET
class contenuto_finestra_principale (Gtk.ApplicationWindow):

	# UTILIZZO IL COSTRUTTORE INIT PER GENERARE L'OGGETTO
	def __init__ (self, *args, **kwargs):

		# UTILIZZO LA FUNZIONE SUPER PER IMPORTARE LE PROPRIETÀ DALLA CLASSE MADRE
		super().__init__ (*args, **kwargs)

		# PROPRIETÀ / CARATTERISTICHE DELLA FINESTRA PRINCIPALE

		# DEFINISCO LE DIMENSIONI DELLA FINESTRA ALL'AVVIO
		self.set_default_size(1280,720) #ORIZZONTALE-VERTICALE

		# DEFINISCO IL TITOLO DELLA FINESTRA
		self.set_title("Prima finestra Gtk + Adw")



# CREAZIONE DELLA CLASSE CHE MANDA A SCHERMO LA FINESTRA PRICIPALE
class genera_finestra_principale (Adw.Application):

	# UTILIZZO IL COSTRUTTORE INIT PER GENERARE L'OGGETTO
	def __init__(self, **kwargs):

		# UTILIZZO LA FUNZIONE SUPER PER IMPORTARE LE PROPRIETÀ DALLA CLASSE MADRE
		super().__init__(**kwargs)

		# VIENE RICHIAMATA LA FUNZIONE "CONNECT", CON IL QUALE SEGNALIAMO CHE LA FINESTRA È APERTA
		self.connect('activate', self.attivazione_finestra_principale)
	


	# DEFINISCO LA FUNZIONE / METODO DELLA CLASSE PER GENERARE LA FINESTRA PRINCIPALE
	def attivazione_finestra_principale(self, finestra_main):

		# CREAZIONE DELL'OGGETTO DELLA FINESTRA PRINCIPALE
		self.finestra_principale = contenuto_finestra_principale(application=finestra_main)

		# MANDO A SCHERMO LA FINESTRA CON LA FUNZIONE "PRESENT"
		self.finestra_principale.present()



# INZIO MAIN



# DEFINIZIONE DELL'ID DEL PROGRAMMA E DELLA VARIABILE CHE RAPPRESENTA LA FINESTRA DEL PROGRAMMA
finestra_main = genera_finestra_principale(application_id="com.primoprogrammaGTK.app")

# AVVIO DELLA FINESTRA PRINCIPALE
finestra_main.run(sys.argv)
```




























