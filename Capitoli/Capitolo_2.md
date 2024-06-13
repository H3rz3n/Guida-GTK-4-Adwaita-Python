# A cosa serve e come scegliere un ID programma
Negli applicativi GNOME ogni software possiede un proprio 'ID programma (application ID in inglese). Esso è unico per ogni software, in modo similare alla targa per un automobile, e svolge le seguenti funzioni :

- È il principale metodo di identificazione utilizzato dal sistema operativo, permettendogli di conoscere correttamente se è aperta un istanza del programma.
- È necessario per il corretto passaggio di messaggi bidirezionale tra applicativo e sistema all'interno di D-Bus.
- È il nome del collegamento desktop e per l'app launcher.
- È necessario per interaggire correttamente con le impostazioni di sistema, sia in lettura che eventualmente in scrittura.
- È necessario per permettere al sistema di trasmettere all'utente eventuali notifiche push inviate dal programma.
- È il nome dell'applicativo nella pacchettizzazione flatpack.

Ora che abbiamo visto una panoramica degli usi ed abbiamo consapevolezza della sua importanza passiamo a comprendere come scegliere correttamente l'application ID per il nostro futuro programma. La standard informale vuole che si utilizzino nomi basati nomi di dominio presenti nei DNS pubblici. Prima di scegliere un nome è meglio controllare che il nome di dominio associato non sia già stato registrato da qualcuno, poichè anche se il proprietario non ha attualmente un app con quell'ID potrebbe averlo in futuro. In generale è buona norma utilizzare come ID solo domi di dominio di cui si è proprietari, in modo da evitare qualunque conflitto. Inoltre, ci sono solo 4 semplici regole da seguire per evitare confitti e malfunzionamenti :

- L'ID deve essere composto da *almeno* due sezioni di testo separate tra loro da un punto `.` . Es. `com.pizza`, `com.pizza.app`
- Ogni sezione dell'ID deve essere composta unicamente da caratteri alfanumerici (A-Z, 0-9), con in aggiunta a questi la possibilità di utilizzare il trattino alto `-` e basso `_`. Inoltre non deve iniziare con una cifra.
- Non è consentito l'uso di spazi all'interno delle sezioni.
- Complessivamente l'intero ID deve essere più piccolo di 255 caratteri.
