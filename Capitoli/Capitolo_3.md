# Guida ai widget : La finestra principale - GtkApplicationWindow
È giunto il momento di introdurre tutti i principali widget di Gtk, vedere il loro utilizzo ed i loro parametri. Iniziamo il nostro percorso approfondendo il widget più importante di tutti, la nostra finestra principale.

## A cosa serve e caratteristiche di base del widget
GtkApplicationWindow è una derivazione di GtkWindow il quale rappresenta la finestra del nostro programma. Esso è il contenitore che racchiude al suo interno tutti i widget dell'interfaccia, difatti tutti i widget sono considerati suoi figli, gerarchicamente parlando, all'interno del file UI. Di default GtkApplicationWindow utilizza come titolo il nome del file da cui è stato evocato.



## Rappresentazione grafica
<p align="center">
  <img src="https://github.com/H3rz3n/Guida-GTK-4-Adwaita-Python/blob/main/Immagini/GtkApplicationWindow.png" alt="GtkApplicationWindow GUI"/>
</p>



## Come si dichiara nel file UI
Per poter utilizzare GtkApplicationWindow all'interno del file UI è sufficiente utilizzare la seguente sintassi :
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

    <!-- CHIUSURA DELLA FINESTRA PRINCIPALE -->
    </object>

<!-- FINE DELL'INTERFACCIA -->
</interface>
```



## Quali sono le sue proprietà
Le principali proprietà di GtkApplicationWindow sono le seguenti :

### Titolo
Con la proprietà `title` possiamo impostare il titolo della finestra. Essa accetta caratteri alfanumerici e punteggiatura, di default il titolo della finestra corrispende al nome del file python da cui viene evocata e si dichiara nel file UI come nel seguente esempio :

```xml
<!-- CREAZIONE DELLA FINESTRA PRINCIPALE -->
<object class="GtkApplicationWindow" id="finestra_principale">

        <!-- DEFINISCO IL TITOLO DELLA FINESTRA -->
        <property name="title">Questo è il mio titolo</property>

<!-- CHIUSURA DELLA FINESTRA PRINCIPALE -->
</object>
```



### Larghezza della finestra all'apertura
Con la proprietà `default-width` possiamo impostare la larghezza che avrà la finestra all'apertura. Essa accetta solo valori numerici interi positivi e si dichiara nel file UI come nel seguente esempio :

```xml
<!-- CREAZIONE DELLA FINESTRA PRINCIPALE -->
<object class="GtkApplicationWindow" id="finestra_principale">

        <!-- DEFINISCO LA LARGHEZZA DI DEFAULT DELLA FINESTRA -->
        <property name="default-width">800</property>

<!-- CHIUSURA DELLA FINESTRA PRINCIPALE -->
</object>
```



### Altezza della finestra all'apertura
Con la proprietà `default-height` possiamo impostare l'altezza che avrà la finestra all'apertura. Essa accetta solo valori numerici interi positivi e si dichiara nel file UI come nel seguente esempio :

```xml
<!-- CREAZIONE DELLA FINESTRA PRINCIPALE -->
<object class="GtkApplicationWindow" id="finestra_principale">

        <!-- DEFINISCO L'ALTEZZA DI DEFAULT DELLA FINESTRA -->
        <property name="default-height">800</property>

<!-- CHIUSURA DELLA FINESTRA PRINCIPALE -->
</object>
```



### Visibilità della barra dei menu
Con la proprietà `show-menubar` possiamo impostare se mostrare o meno la barra dei menu all'interno della finestra. Essa accetta solo valori booleani `True` o `False`, il valore di default è `True` e si dichiara nel file UI come nel seguente esempio :

```xml
<!-- CREAZIONE DELLA FINESTRA PRINCIPALE -->
<object class="GtkApplicationWindow" id="finestra_principale">

        <!-- DEFINISCO SE MOSTRARE O MENO LA BARRA DEI MENU DELLA FINESTRA -->
        <property name="show-menubar">False</property>

<!-- CHIUSURA DELLA FINESTRA PRINCIPALE -->
</object>
```



### Apertura a schermo intero
Con la proprietà `fullscreened` possiamo impostare se mostrare la finestra a schermo intero senza bottoni di controllo delle dimensioni. Essa accetta solo valori booleani `True` o `False`, il valore di default è `False` e si dichiara nel file UI come nel seguente esempio :

```xml
<!-- CREAZIONE DELLA FINESTRA PRINCIPALE -->
<object class="GtkApplicationWindow" id="finestra_principale">

        <!-- DEFINISCO SE MOSTRARE LA FINESTRA A SCHERMO INTERO -->
        <property name="fullscreened">True</property>

<!-- CHIUSURA DELLA FINESTRA PRINCIPALE -->
</object>
```

### Apertura della finestra massimizzata
Con la proprietà `maximized` possiamo impostare se mostrare la finestra massimizzata e con bottoni di controllo delle dimensioni. Essa accetta solo valori booleani `True` o `False`, il valore di default è `False` e si dichiara nel file UI come nel seguente esempio :

```xml
<!-- CREAZIONE DELLA FINESTRA PRINCIPALE -->
<object class="GtkApplicationWindow" id="finestra_principale">

        <!-- DEFINISCO SE MOSTRARE LA FINESTRA MASSIMIZZATA -->
        <property name="maximized">True</property>

<!-- CHIUSURA DELLA FINESTRA PRINCIPALE -->
</object>
```

### Nascondi invece che chiudere
Con la proprietà `hide-on-close` possiamo impostare la finestra in modo tale che se chiusa dall'utente non interrompa il programma che rappresenta. Essa accetta solo valori booleani `True` o `False`, il valore di default è `False` e si dichiara nel file UI come nel seguente esempio :

```xml
<!-- CREAZIONE DELLA FINESTRA PRINCIPALE -->
<object class="GtkApplicationWindow" id="finestra_principale">

        <!-- DEFINISCO SE NON CHIUDERE IL PROCESSO ALLA CHIUSURA DELLA FINESTRA -->
        <property name="hide-on-close">True</property>

<!-- CHIUSURA DELLA FINESTRA PRINCIPALE -->
</object>
```

### Possibilità di ridimensionamento
Con la proprietà `resizable` possiamo impostare la finestra per negare all'utente la possibilità di ridimensionamento della stessa. Essa accetta solo valori booleani `True` o `False`, il valore di default è `True` e si dichiara nel file UI come nel seguente esempio :


```xml
<!-- CREAZIONE DELLA FINESTRA PRINCIPALE -->
<object class="GtkApplicationWindow" id="finestra_principale">

        <!-- DEFINISCO SE PERMETTERE ALL'UTENTE DI RIDIMENSIONARE LA FINESTRA -->
        <property name="resizable">False</property>

<!-- CHIUSURA DELLA FINESTRA PRINCIPALE -->
</object>
```

### Allineamento orizzontale
Con la proprietà `halign` possiamo impostare l'allineamento orizzontale del contenuto della finestra. Essa accetta come valori solo :
- `center` (allineamento al centro),
- `start` (allineamento all'inizio del verso di scrittura, per gli occidentali sinistra),
- `end` (allineamento alla fine del verso di scrittura, per gli occidentali destra),
- `fill` (allineamento volto a rimepire tutto lo spazio possibile, allinea al centro se non può espandere il contenuto della finestra),
- `baseline-center` (allineamento volto a rimepire tutto lo spazio possibile, allineando in base al riferimento fornito),
- `baseline-fill` (allineamento in base al riferimento fornito),
il valore di default è `start` e si dichiara nel file UI come nel seguente esempio :

```xml
<!-- CREAZIONE DELLA FINESTRA PRINCIPALE -->
<object class="GtkApplicationWindow" id="finestra_principale">

        <!-- DEFINISCO L'ALLINEAMENTO ORIZZONTALE DEL CONTENUTO DELLA FINESTRA -->
        <property name="halign">center</property>

<!-- CHIUSURA DELLA FINESTRA PRINCIPALE -->
</object>
```

### Allineamento verticale
Con la proprietà `` possiamo impostare

### Espansione verticale della finestra
Con la proprietà `` possiamo impostare






























