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

- #### Titolo
Con la proprietà `title` possiamo impostare il titolo della finestra. Esso si dichiara nel file UI come nel seguente esempio :

```xml
<!-- CREAZIONE DELLA FINESTRA PRINCIPALE -->
<object class="GtkApplicationWindow" id="finestra_principale">

        <!-- DEFINISCO IL TITOLO DELLA FINESTRA -->
        <property name="title">Questo è il mio titolo</property>

<!-- CHIUSURA DELLA FINESTRA PRINCIPALE -->
</object>
```



- #### Larghezza di default
Con la proprietà `default-width` possiamo impostare la larghezza che avrà la finestra all'apertura. Essa si dichiara nel file UI come nel seguente esempio :

```xml
<!-- CREAZIONE DELLA FINESTRA PRINCIPALE -->
<object class="GtkApplicationWindow" id="finestra_principale">

        <!-- DEFINISCO LA LARGHEZZA DI DEFAULT DELLA FINESTRA -->
        <property name="default-width">800</property>

<!-- CHIUSURA DELLA FINESTRA PRINCIPALE -->
</object>
```



- #### Altezza di default
- #### Visibilità della barra dei menu
- #### Apertura a schermo intero
- #### Nascondi invece che chiudere
- #### Possibilità di ridimensionamento
- #### Dichiarazione della finestra genitore
- #### Impostare come finestra di dialogo
- #### Allineamento orizzontale
- #### Allineamento verticale
- #### Espansione verticale della finestra



## Quali sono i suoi metodi

























