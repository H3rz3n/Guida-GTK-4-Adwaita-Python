# A cosa serve e come scegliere un ID programma
Negli applicativi GNU-Linux ogni software possiede un proprio ID programma (application ID in inglese). Esso è univoco per ogni software, in modo similare alla targa per un automobile, e svolge le seguenti funzioni :

- È il principale metodo di identificazione utilizzato dal sistema operativo, permettendogli di conoscere correttamente se è aperta un istanza del programma e di gestirlo nel window manager.
- È necessario per il corretto passaggio di messaggi bidirezionale tra applicativo e sistema all'interno di D-Bus.
- È il nome identificativo del collegamento desktop e per l'app launcher.
- È necessario per interaggire correttamente con le impostazioni di sistema, sia in lettura che eventualmente in scrittura.
- È necessario per permettere al sistema di trasmettere all'utente notifiche push generate dal programma.
- È il nome identificativo dell'applicativo nella pacchettizzazione flatpack.

Ora che abbiamo visto una panoramica degli usi ed abbiamo una maggiore consapevolezza della sua importanza passiamo a comprendere come scegliere correttamente l'application ID per il nostro futuro programma. Lo standard informale vuole che si utilizzino ID basati nomi di dominio presenti nei DNS pubblici. Prima di scegliere un nome è meglio controllare che il nome di dominio associato non sia già stato registrato da qualcuno, poichè anche se il proprietario non ha attualmente un app con quell'ID potrebbe averla in futuro. In generale è buona norma utilizzare come ID solo i nomi di dominio di cui si è proprietari, in modo da evitare qualunque conflitto. Per scrivere il nostro ID, ci sono 4 semplici regole da seguire per evitare confitti e malfunzionamenti :

- L'ID deve essere composto da *almeno* due sezioni di testo separate tra loro da un punto `.` . Es. `com.pizza`, `com.pizza.app`
- Ogni sezione dell'ID deve essere composta unicamente da caratteri alfanumerici (A-Z, 0-9), con in aggiunta a questi la possibilità di utilizzare il trattino alto `-` e basso `_`. Inoltre non deve iniziare con una cifra.
- Non è consentito l'uso di spazi all'interno delle sezioni.
- Complessivamente l'intero ID deve essere più corto di 255 caratteri.

Nel caso in cui non sia possibile scegliere un ID basato su un dominio in nostro possesso si possono utilizzare soluzioni creative come il proprio nome utente su GitHub `com.github.nickname.blabla.app` o nomi analoghi basati su altre piattaforme. È importante ricordare che l'ID programma **non è il nome del nostro programma per il pubblico**, di conseguenza dato che esso solo è un indicatore ad uso del sistema è preferibile essere creativi ed unici anche a discapito dell'attraenza commerciale del nome scelto per l'ID.




# Introduzione ed utilizzo dei file UI
Quando si utilizza Gtk, per implementare i vari elementi grafici (widget) all'interno del programma vi sono due soluzioni tecniche che conducono alo stesso risultato:
- Scrivere il contenuto della finestra all'interno di un file `.py` come abbiamo fatto con la finestra di prova.
- Scrivere il contenuto della finestra all'interno di un file `.ui` dedicato.
Lo standard utilizzato negli applicativi GNOME è il secondo, di  conseguenza sarà anche quello che utilizzeremo da qui in poi per scrivere i nostri programmi di prova. Questa soluzione tecnica ha alcuni vantaggi, essa ci consente di semplificare in parte la scrittura e l'organizzazione dei widget e soprattutto ci permette una maggiore semplificazione e pulizia del file python in cui risiede il codice delle varie funzioni del programma.

## Cosa è un file .UI
Un file `.UI` è un file scritto in codice XML che consente di implementare in modo più semplice l'interfaccia grafica, permettendoci di separarla dalla parte logica del programma. Accetta  al suo interno solo caratteri appartenenti allo standard UTF-8 e rispetta una struttura gerarchica in cui è necessario prestare molta attenzione alla sintassi utilizzata in quanto in programma molto complessi rischia di diventare confusionaria. Il file `.ui` può avere un qualunque nome di nostro piacere, come ad esempio `finestra_principale.ui` o `nomeprogramma.ui`. Esso viene caricato all'interno del codice python utilizzando utilizzando la funzione di Gtk `GtkBuilder()`. Passiamo a vedere un piccolo esempio e successivamente ad analizzarne la sintassi :
```xml
<!-- SPECIFICHIAMO LA VERSIONE DI XML E LO STANDARD DI CARATTERI -->
<?xml version="1.0" encoding="UTF-8"?>


<!-- INIZIO DELL'INTERFACCIA -->
<interface>

    <!-- SPECIFICO LE LIBRERIE RICHIESTE -->
    <requires lib="gtk" version="4.0"/>
    <requires lib="Adw" version="1.0"/>

    <!-- CREAZIONE DELLA FINESTRA PRINCIPALE -->
    <object class="GtkApplicationWindow" id="finestra_principale">

        <!-- SPECIFICO LE PROPRIETÀ DELLA FINESTRA PRINCIPALE -->

        <!-- DEFINISCO IL TITOLO DELLA FINESTRA -->
        <property name="title">Finestra di prova in file .UI</property>

        <!-- DEFINISCO LA LARGHEZZA DI DEFAULT DELLA FINESTRA -->
        <property name="default-width">1280</property>

        <!-- DEFINISCO L'ALTEZZA DI DEFAULT DELLA FINESTRA -->
        <property name="default-height">720</property>

    <!-- CHIUSURA DELLA FINESTRA PRINCIPALE -->
    </object>

<!-- FINE DELL'INTERFACCIA -->
</interface>
```
Analizziamo meglio quanto scritto procedendo in ordine di gerarchia :
- Abbiamo specificato quale versione di XML e quale codifica di caratteri useremo;
- Abbiamo aperto la scrittura dell'interfaccia;
- Abbiamo specificato le librerie e le versioni specifiche delle stesse che andremo ad utilizzare;
- Abbiamo creato il nostro primo oggetto, la finestre principale;
- Abbiamo specificato le proprietà *titolo*, *larghezza all'apertura* ed *altezza all'apertura*;
- Abbiamo chiuso l'oggetto finestra principale;
- Abbiamo chiuso la scrittura dell'interfaccia;

Con queste poche righe di codice abbiamo definito la stessa identica finestra di prova che abbiamo generato nel capitolo 1. Adesso non ci resta che integrarla correttamente nel nostro eseguibile python. Per farlo vediamo il seguente esempio, ricordandoci di sostituire il percorso assoluto in cui si trova il nostro file .UI :
```python
# IMPORTO I MODULI PRINCIPALI
import sys, gi

# SPECIFO LE VERSIONI DI GTK ED ADW CHE ANDREMO AD UTILIZZARE  
gi.require_version('Gtk', '4.0')
gi.require_version('Adw', '1')

# IMPORTO I MODULI SECONDARI DALLA RACCOLTA GI
from gi.repository import Gtk, Adw, Gdk, Pango, Gio, GLib




# DEFINISCO LA CLASSE CHE PERMETTE LA CREAZIONE E MESSA SCHERMO DELLA FINESTRA PRINCIPALE
class genera_finestra_principale(Adw.Application):

    # IMPORTO GLI ATTRIBUTI DELLA CLASSE MADRE "ADW.APPLICATION" UTILIZZANDO LA FUNZIONE INIT E LA SUPERCLASSE
    def __init__(self, **kwargs):
        super().__init__(**kwargs)

        # RICHIAMO LA FUNZIONE "CONNECT" UTILIZZANDO COME PARAMETRI "ACTIVATE" E LA FUNZIONE DI GENERAZIONE DELLA FINESTRA PRINCIPALE 
        self.connect('activate', self.attivazione_finestra_principale)




    # AVVIO DELLA FUNZIONE CHE GENERA LA FINESTRA PRINCIPALE E LA MANDA A SCHERMO
    def attivazione_finestra_principale (self, app):

        # AVVIO LA FUNZIONE BUILDER PER LEGGERE IL FILE UI DELLA FINESTRA PRINCIPALE
        builder = Gtk.Builder()

        # IMPORTO IL FILE UI CHE RAPPRESENTA LA FINESTRA PRINCIPALE
		#builder.add_from_file("/percorso/assoluto/tuo/file/prova.ui")
        builder.add_from_file("/home/lorenzo/Documenti/prova_guida.ui")
		
        # OTTENGO LA FINESTRA PRINCIPALE ED I SUOI CHILD DAL FILE UI
        self.finestra_principale = builder.get_object("finestra_principale")
    
        # IMPOSTO LA FINESTRA PRINCIPALE COME PARTE DEL PROGRAMMA PER FAR CHIUDERE IL PROGRAMMA ALLA CHIUSURA DELLA FINESTRA
        self.finestra_principale.set_application(self)

        # MANDO A SCHERMO LA FINESTRA PRINCIPALE ED I SUOI CHILD
        self.finestra_principale.present()



# INZIO MAIN



# DEFINIZIONE DELL'ID DEL PROGRAMMA E DELLA VARIABILE CHE RAPPRESENTA LA FINESTRA DEL PROGRAMMA
finestra_main = genera_finestra_principale(application_id="com.primoprogrammaGTK.app")

# AVVIO DELLA FINESTRA PRINCIPALE
finestra_main.run(sys.argv)
```

Se ci soffermiamo ad analizzare meglio il codice python, notiamo che abbiamo elimitato la classe `contenuto_finestra_principale` ed all'interno di `genera_finestra_principale` abbiamo integrato la funzione GtkBuilder() per leggere, ottenere dal file l'oggetto `finestra_principale` e successivamente mandarlo a schermo. Con questa scrittura abbiamo notevomente automentato la leggibilità del nostro programma e semplificato la futura manutenzione ed espansione del codice.

## Gerarchia all'interno del file UI
La scrittura di un file UI si basa sul rispettare un precisa gerachia e sintassi. Ogni volta che inseriamo un oggetto o un parametro esso andrà sia aperto che chiuso, diponendolo in un preciso ordine. Vediamolo meglio con un esempio :
```xml
<!-- SPECIFICHIAMO LA VERSIONE DI XML E LO STANDARD DI CARATTERI -->
<?xml version="1.0" encoding="UTF-8"?>

<!-- INIZIO DELL'INTERFACCIA -->
<interface>

        <!-- APERTURA DELL'OGGETTO 1-->
        <object>

             <!-- PROPRIETÀ DELL'OGGETTO 1-->
            <property></property>

            <!-- APERTURA DELLA DICHIARAZIONE FIGLIO DELL'OGGETTO 2 -->
            <child>

                <!-- APERTURA DELL'OGGETTO 2 -->
                <object>

                    <!-- PROPRIETÀ DELL'OGGETTO 2-->
                    <property></property>

                    <!-- APERTURA DELLA DICHIARAZIONE FIGLIO DELL'OGGETTO 3 -->
                    <child>

                        <!-- APERTURA DELL'OGGETTO 3 -->
                        <object>

                            <!-- PROPRIETÀ DELL'OGGETTO 3-->
                            <property></property>
                    
                        <!-- CHIUSURA DELL'OGGETTO 3 -->
                        </object>
                
                    <!-- CHIUSURA DELLA DICHIARAZIONE FIGLIO DELL'OGGETTO 3 -->
                    </child>
                    
                <!-- CHIUSURA DELL'OGGETTO 2 -->
                </object>
                
            <!-- CHIUSURA DELLA DICHIARAZIONE FIGLIO DELL'OGGETTO 2 -->
            </child>
            
        <!-- CHIUSURA DELL'OGGETTO 1 -->
        </object>

<!-- FINE DELL'INTERFACCIA -->
</interface>
```


# Piccolo riassunto delle buone norme di programmazione
Sia che sia la tua prima esperienza di programmazione, sia che tu sia già un programmatore affermato, è sempre buona prassi tenere a mente alcuni semplici consigli per poter scrivere codice di qualità e che sia chiaro per te e per gli altri. Vediamo di tutto alcuni consigli generali :
- **Provare il codice ogni volta che si esegue qualche modifica:** In questo modo avrai subito chiaro cosa generi eventuali errori.
- **Commentare tutto il codice che si scrive:** In modo da tenere traccia in modo semplice del funzionamento e delle logiche del programma. Questo è fondamentale tanto per gli altri utenti **quanto per te stesso** quando dovrai approciarti ad un tuo programma in futuro per eventuali manutenzioni e migliorie.
- **Seguire il principio di natura:** Esso ci dice di non fare con più ciò che puoi fare con meno. Questo è un principio fondamentale dell'ottimizzazione e ci consente di scrivere codice semplice, efficace, facilmente leggibile e leggero.
- **Utilizzare nomi comprensbili e didascalici all'interno del codice:** In questo modo aumenterà di molto la leggibilità e sarà più semplice individuare eventuali errori.
- **Prestare molta attenzione alla sintassi:** Ogni qualvolta che si aprono delle parentesi o una sezione avere cura di chiuderle subito in modo da evitare fastidiosi errori di sintassi.











