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


```









