---
layout: default
title: "Manuale utente"
permalink: manuale_utente
---
**Per usare l'applicazione, seguire le istruzioni alla pagina *Downloads* per scaricare ed eseguire l'applicativo.**

#### **Collegamenti alle sezioni della pagina**
- <a href="#start">Iniziare ad usare l'applicazione</a>
- <a href="#spawn">Generare i punti di controllo in scena</a>
- <a href="#interact">Selezionare i punti di controllo e interagirvi</a>
- <a href="#simpleselection">Modalità Simple Selection</a>
- <a href="#coordinateinput">Inserire coordinate precise</a>
- <a href="#draggableaxes">Modalità Draggable Axes</a>
- <a href="#draw"><strong>Disegnare una superficie di Bezier</strong></a>
- <a href="#camera">Muovere la camera</a>
- <a href="#reviewbuttons">Lista comandi in forma tabulare</a>

**Nota**: le immagini presentano una didascalia visualizzabile posandovi sopra il cursore.

## **Manuale utente**

Una volta eseguita l'applicazione, ci si trova davanti alla seguente *scena*.
Ciò che è visualizzato in *scena* è ciò che è presente nel *mondo virtuale* in cui possiamo rappresentare una superficie di Bezier. Si noti che la *camera* usata sfrutta una *proiezione prospettiva* e non ortografica.

<div class='infoimagecontainer'>
<img class='infoimage' src="assets/images/StartingScreen.png">
<div class='infoimageoverlay'>
<div class='infoimagetext'>Questo è ciò che ci si trova davanti una volta avviata l'applicazione.
</div></div></div>

Si possono distinguere due zone fondamentali, la rappresentazione della scena dal punto di vista della *camera* e un pannello laterale, interfaccia mediante la quale l'utente può interagire con la scena.

<a name="start"></a>

### **Come iniziare ad usare l'applicazione?**
Si può iniziare cliccando sul pulsante con un apice di freccia, in alto a sinistra.

<div class='infoimagecontainer'>
<img class='infoimage' src="assets/images/SS_OpenPanel.png">
<div class='infoimageoverlay'>
<div class='infoimagetext'>Questo è il risultato dell'apertura del pannello laterale.
</div></div></div>

Il pannello laterale può essere richiuso premendo nuovamente sul pulsante con l'apice di freccia.

Si può notare come il pannello laterale esponga diverse funzionalità. Descriviamo ciascuna di esse nel dettaglio, con esempi e possibilità a disposizione dell'utente.

<a name="spawn"></a>

### **Spawn control points**
Il primo blocco del pannello laterale è dedicato alla **generazione dei punti di controllo**.
In particolare, ci consente di definire il bigrado della superficie di Bezier specificando un numero compreso tra 1 e 9. 
Si noti che un qualsiasi altro valore sarà considerato non valido.

Un esempio potrebbe essere quello di generare i punti del poliedro di controllo per una superficie di bigrado $$(2,3)$$, come nel seguente esempio:

<div class='infoimagecontainer'>
<img class='infoimage' src="assets/images/SpawnSection.png">
<div class='infoimageoverlay'>
<div class='infoimagetext'>Abbiamo riempito i campi per definire il grado della superficie di Bezier che vogliamo manipolare e disegnare.
</div></div></div>

Premere il pulsante **Spawn**, o il tasto **P** sulla tastiera, permetterà di generare i **p**unti di controllo nella scena. Segue un esempio del risultato che ci si può aspettare:

<div class='infoimagecontainer'>
<img class='infoimage' src="assets/images/SpawnResult.png">
<div class='infoimageoverlay'>
<div class='infoimagetext'>Si noti che vengono generati 3 × 4 punti, visto che si è richiesta una superficie di Bezier di bigrado (2,3).
</div></div></div>

I punti sono generati e rappresentati come sfere di raggio unitario, in modo da renderle più facilmente interagibili dall'utente.
Si noti che, anche chiudendo il pannello laterale, è possibile premere il tasto **P** sulla tastiera per generare un nuovo set di punti di controllo nelle posizioni iniziali. Questa operazione può tornare comoda nel caso si siano spostati i punti e li si voglia riportare nelle posizioni iniziali.
Si noti anche che le posizioni iniziali corrispondono a quelle di una griglia disposta sul piano xy del sistema di riferimento del mondo, ovvero il piano $$z=0$$. Ogni punto "sulla griglia" ha distanza pari a 2 unità dall'altro. 
Ad esempio, il punto $$P_{0,1}$$ avrà coordinate $$(2.0, 0.0, 0.0)^T$$, mentre il punto $$P_{2, 0}$$ avrà coordinate $$(0.0, 4.0, 0.0)^T$$.
Verifichiamo subito quanto detto, imparando come interagire con i punti del poliedro di controllo.

<a name="interact"></a>

### **Interagire con i punti**
Fare un *click-sinistro* su uno dei punti di controllo ci permette di selezionarlo.
Continuando con il nostro esempio, se clicchiamo con il punto più in alto e più a sinistra, otterremo la seguente situazione:

<div class='infoimagecontainer'>
<img class='infoimage' src="assets/images/SelectionResult.png">
<div class='infoimageoverlay'>
<div class='infoimagetext'>Si è selezionato il punto di controllo (2,0), in modalità "Simple selection".
</div></div></div>

Si può notare che una volta selezionato un punto, esso viene evidenziato in giallo e il pannello a sinistra permette di visualizzarne gli indici nella **griglia combinatoria** e la **posizione** rispetto al sistema di riferimento globale.
Per "deselezionare" il punto, si può premere **ESC** sulla tastiera.

Se si passa il cursore su altri punti non selezionati (operazione anche nota come *fare hovering*),un'etichetta a comparsa mostrerà gli indici del punto sotto il cursore.

<div class='infoimagecontainer'>
<img class='infoimage' src="assets/images/ExampleLabel.png">
<div class='infoimageoverlay'>
<div class='infoimagetext'>Facendo hovering sul punto (1,1), che non è quello selezionato, appare un'etichetta che consente di identificare quale punto si stia "sorvolando" con il cursore.
</div></div></div>

<a name="simpleselection"></a>

La **modalità di selezione e movimento attiva** in questo momento è detta **Simple Selection** (selezione semplice), come espresso nel pannello laterale.
Una volta selezionato un punto, lo si può **trascinare** cliccandoci nuovamente e muovendo il cursore mentre il tasto sinistro è premuto. 
Questo tipo di movimento è detto *semplice* perché è particolarmente rapido ed intuitivo; tuttavia, esso limita l'utente al muovere il punto in un piano parallelo a quello di proiezione della camera. 

Si può verificare quanto appena detto sapendo che tutti i punti sono sul piano $$z=0$$ e il piano di proiezione della camera, nelle condizioni iniziali, vi è parallelo.
In particolare, la camera è alle coordinate $$(0.0, 2.0, -15.0)^T$$ e il suo verso è coincidente con quello del versore che giace sull'asse z, ovvero $$(0.0, 0.0, 1.0)^T$$.
Spostare un qualsiasi punto per trascinamento, in questa situazione, non farà variare la coordinata z del punto selezionato nel pannello laterale.

<a name="coordinateinput"></a>

L'applicazione offre altri due modi per posizionare i punti di controllo nella scena.
Il più diretto e preciso, in realtà, è già in vista. Il pannello laterale mostra le coordinate attuali del punto selezionato, ma consente anche di modificare le singole coordinate nei rispettivi campi. Una volta selezionato un punto, infatti, si può **cliccare sulla coordinata che si desidera modificare**, scrivere il valore corrispondente e premere **Enter** (Invio) per confermare. Il punto selezionato si sposterà nella posizione desiderata con precisione.


Un esempio ci viene offerto dalla seguente immagine:
<div class='infoimagecontainer'>
<img class='infoimage' src="assets/images/FirstStepCollapse.png">
<div class='infoimageoverlay'>
<div class='infoimagetext'> In questa immagine, il punto (2,2) è stato già fatto collassare sul punto (2,1) e si sta selezionando il punto (2,0).
</div></div></div>
Il punto selezionato è il punto con indici (2,0) e ha coordinate $$(0.0, 4.0, 0.0)^T$$ come si nota nel pannello a sinistra.
Il risultato dopo aver cambiato la prima coordinata in $$2.0$$ e premuto **Invio** è il seguente:
<div class='infoimagecontainer'>
<img class='infoimage' src="assets/images/CollapsedControlPoints.png">
<div class='infoimageoverlay'>
<div class='infoimagetext'>Si noti che si è anche generata la superficie corrispondente, oltre a spostare il punto di controllo (2,0).
</div></div></div>

**Curiosità**: come si può notare dall'ultima immagine, l'applicazione è in grado di disegnare superfici di Bezier in cui alcuni punti di controllo sono collassati. Può essere interessante far collassare i punti della prima e dell'ultima riga di una superficie di Bezier di bigrado $$(2,2)$$ e osservarne il risultato, ad esempio.

<a name="draggableaxes"></a>

La terza **modalità di selezione e movimento** a disposizione è chiamata **Draggable Axes**.
<div class='infoimagecontainer'>
<img class='infoimage' src="assets/images/MovementTypeSwitch.png">
<div class='infoimageoverlay'>
<div class='infoimagetext'>La modalità è nota come <em>Draggable Axes</em> perché le <em>handle</em> che possono essere usate per spostare il punto lungo gli assi del sistema di riferimento locale possono ricordare gli assi e vi sono sovrapposte.
</div></div></div>

Per passare a questa modalità, si può cliccare sul menù a tendina presente nel pannello laterale sotto la voce **Control Point Movement Type** e selezionare **Draggable Axes**. Si noti che si può tornare alla modalità precedente, **Simple Selection**, quando si preferisce; in più, inserire le coordinate a mano rimane un'opzione sempre a vista e possibile se si tiene aperto il pannello laterale.

Nella modalità **Draggable Axes**, come si può notare nell'immagine, compaiono tre *maniglie* o **handle** che consentono di trascinare il punto di controllo selezionato soltanto lungo la direzione corrispondente.

**Curiosità**: a ciascuno degli assi è stato assegnato un colore specifico; se si assume che il colore sia espresso nel *formato RGB* e si fornisce come colore il versore corrispondente all'asse, si ottiene proprio questo tipo di colorazione. Ad esempio, il versore che indica l'asse x avrebbe componenti $$(1.0, 0.0, 0.0)^T$$, che, letto nel formato RGB, corrisponde a un colore con la "componente rossa" al massimo e le componenti verde e blu del tutto assenti.

Nella posizione attuale della camera vediamo solo due dei tre assi. Se si pensa a quanto detto fino ad ora, la cosa non dovrebbe stupirci: il sistema di riferimento locale ha gli assi paralleli a quelli del sistema di riferimento globale; poiché l'asse z è entrante rispetto allo schermo per la posizione iniziale della camera, esso è attualmente "nascosto" dal punto di controllo.

<a name="draw"></a>

### **Come disegnare una superficie di Bezier?**
Arriviamo al punto fondamentale dell'applicazione. Per **disegnare una superficie di Bezier** di bigrado dato e con i punti del poliedro di controllo disposti in scena, si può cliccare sul pulsante **Draw Bezier Surface** nel pannello laterale; diversamente, se il pannello è chiuso e si vuole essere più rapidi, si può **g**enerare la superficie premendo il tasto **G** sulla tastiera.

L'immagine seguente mostra un esempio a riguardo:
<div class='infoimagecontainer'>
<img class='infoimage' src="assets/images/FirstSurfaceResolution4.png">
<div class='infoimageoverlay'>
<div class='infoimagetext'>Qui i punti sono stati spostati in maniera casuale per ottenere una superficie abbastanza generica.
</div></div></div>

Si noti che, nel pannello laterale, si è impostata la **resolution** (o *risoluzione*) della superficie a 4, a scopo esemplificativo. Modificare questo parametro ci consente di valutare la superficie in più punti e visualizzarla in maniera più o meno precisa. Mantenendo gli stessi punti di controllo e alzando la risoluzione, si può ottenere una superficie molto meno "*spigolosa*" ai bordi:

<div class='infoimagecontainer'>
<img class='infoimage' src="assets/images/FirstSurfaceResolution30.png">
<div class='infoimageoverlay'>
<div class='infoimagetext'>La differenza può essere apprezzabile anche per piccole variazioni di risoluzione.
</div></div></div>

Finiamo di esplorare le opzioni che il pannello laterale offre all'utente.
Le superfici di Bezier possono essere colorate specificando un colore in formato RGB. Ciascuna componente è da considerarsi un numero intero positivo che varia tra 0 e 255. Ad esempio, se volessimo colorare la superficie di un verde chiaro, potremmo usare i seguenti colori:

<div class='infoimagecontainer'>
<img class='infoimage' src="assets/images/ChangeColor.png">
<div class='infoimageoverlay'>
<div class='infoimagetext'>Modificare le componenti del colore della superficie è come modificare le coordinate di un punto selezionato. 
</div></div></div>

### **Cosa succede dimenticando di inserire il bigrado della superficie?**
Nulla di grave. Il programma ricorderà all'utente di inserire il bigrado e generare i punti di controllo, senza i quali non è possibile generare una superficie.

<div class='infoimagecontainer'>
<img class='infoimage' src="assets/images/NoDegreesSpecified.png">
<div class='infoimageoverlay'>
<div class='infoimagetext'>"Il bigrado non è stato inserito correttamente, e non si sono potuti generare punti di controllo in scena. Riprova dopo averli inseriti."
</div></div></div>


### **Cosa succede dimenticando di generare i punti prima di disegnare la superficie?**
Un altro messaggio ricorda all'utente di generare i punti prima di disegnare una superficie.

<div class='infoimagecontainer'>
<img class='infoimage' src="assets/images/DrawBeforeSpawn.png">
<div class='infoimageoverlay'>
<div class='infoimagetext'>"Non ci sono punti di controllo. Generane qualcuno prima di disegnare una superficie." 
</div></div></div>

<a name="camera"></a>

### **Voglio guardare la superficie da un'altra angolazione; come si fa?**
L'applicazione consente di **muovere la camera** in giro per la scena e direzionarla diversamente.
Segue una lista di comandi utili.

<a name="reviewbuttons"></a>

| Tastiera | Effetto |
| R | Torna alla posizione iniziale |
| A | Sposta la camera verso sinistra |
| D | Sposta la camera verso destra |
| W | Sposta la camera in avanti |
| S | Sposta la camera indietro |
| Q | Alzare la camera |
| E | Abbassare la camera |
| P | Genera punti di controllo per una superficie di bigrado specificato |
| G | Disegna la superficie descritta mediante i punti di controllo in scena |

Per **ruotare la camera nella direzione desiderata** si può **cliccare con il tasto destro del mouse** in un punto qualsiasi della scena, tenerlo premuto e muovere il cursore.
In caso si possegga un Mac, si può **tenere premuto CTRL mentre si clicca e tiene premuto il mouse** per muovere la camera in una determinata direzione.

<div class='infoimagecontainer'>
<img class='infoimage' src="assets/images/RedDifferentAngle.png">
<div class='infoimageoverlay'>
<div class='infoimagetext'>Qui la camera è stata spostata per spostare i punti in maniera più pratica con la <em>selezione semplice</em>. 
</div></div></div>

Si noti che cosa succede se si passa alla modalità **Draggable Axes**:

<div class='infoimagecontainer'>
<img class='infoimage' src="assets/images/NoteAxesDirections.png">
<div class='infoimageoverlay'>
<div class='infoimagetext'>Le <em>handle</em> sono parallele agli assi del sistema di riferimento globale. 
</div></div></div>

Le **handle** rimangono parallele agli assi del sistema di riferimento globale, in modo che trascinandole si possa avere lo spostamento solo nella direzione dell'asse corrispondente. Si può verificare quanto appena detto provando a trascinare un punto per una delle maniglie e osservando come variano le coordinate del punto selezionato.

<div class='infoimagecontainer'>
<img class='infoimage' src="assets/images/ResetCamera.png">
<div class='infoimageoverlay'>
<div class='infoimagetext'>Se volessimo tornare alla posizione iniziale, possiamo premere <strong>R</strong> sulla tastiera. 
</div></div></div>

L'unica opzione del pannello laterale che non abbiamo ancora esaminato è **Show and modify Control Points** (*mostra e modifica i punti di controllo*). Spuntare questa opzione permette di nascondere i punti del poliedro di controllo alla vista e all'interazione, in modo tale che si possa osservare la superficie senza occlusioni.

<div class='infoimagecontainer'>
<img class='infoimage' src="assets/images/HiddenControlPoints.png">
<div class='infoimageoverlay'>
<div class='infoimagetext'> Esempio di superficie disegnata e priva di occlusioni.
</div></div></div>