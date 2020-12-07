---
layout: default
title: Teoria
permalink: teoria
---
# **Manuale teorico**
## **Cosa è una superficie di Bezier?**
Una superficie di Bezier è una funzione di due variabili, di cui siamo in grado di rappresentare il supporto grazie a questa applicazione.

La generica **superficie di Bezier di bigrado** $$(h,k)$$ può essere scritta come:

$$\displaystyle \vec P(u,v)=\sum_{i=0}^{h}\sum_{j=0}^{k}B_i^h(u)B_j^k(v)\vec P_{i,j}$$

### **Come è definita una superficie di Bezier?**
Una superficie di Bezier $$\vec P(u,v)$$ è una funzione di due variabili definita sul quadrato unitario del piano $$uv$$ e avente valori in $$\mathbb{E}^3$$, lo spazio affine; possiamo anche scrivere: 

$$\vec P(u,v) \colon [0,1] \times [0,1] \to \mathbb{E}^3$$

### **Come descriviamo una superficie di Bezier?**
Una superficie di Bezier può essere descritta mediante un **poliedro di controllo**, a cui appartengono $$(h+1) \cdot (k+1)$$ punti, esprimibili nella forma generica:

$$\{\vec P_{i,j}\}$$

con $$i=0,\dots, h$$ e $$j=0,\dots, k$$.
La coppia $$(h,k)$$ con $$h \ge 1, k \ge 1$$ è detta **bigrado** della superficie di Bezier.
L'applicazione permette di definire il bigrado della superficie da disegnare e generare un poligono di controllo opportuno, che possa essere modificato a piacere per definire la superficie.

**Curiosità**: nonostante si siano introdotte a lezione in seguito ai fogli semplici di superficie e partendo da una superficie detta **quadrica a sella** corrispondente a una superficie di Bezier di bigrado $$(1,1)$$, non tutte le superfici di Bezier sono fogli semplici di superficie.

### **Cosa viene moltiplicato per i punti del poliedro di controllo?**
Abbiamo già definito, la generica superficie di Bezier di bigrado $$(h,k)$$ come:

$$\displaystyle \vec P(u,v)=\sum_{i=0}^{h}\sum_{j=0}^{k}B_i^h(u)B_j^k(v)\vec P_{i,j}$$

ma non si è ancora chiarito cosa siano i coefficienti espressi nella formula, come $$B_i^h(u)$$ o $$B_j^k(v)$$.
$$B_n^m(w)$$ è detto **polinomio di Bernstein n-esimo di grado m** ed è una funzione della variabile generica $$w$$. Tale polinomio può essere scritto come:

$$B_n^m(w) = \binom{m}{n} w^n(1-w)^{m-n} \space\space\space con \space n = 0,\dots, m$$

O, se si preferisce, in forma più estesa:

$$B_n^m(w) = \frac{m!}{n!(m-n)!} w^n(1-w)^{m-n} \space\space\space con \space n = 0,\dots, m$$

### **Posso scegliere il bigrado della superficie a piacere?**
Sostanzialmente, sì. La formulazione generale presentata è valida quando si sceglie $$h = k$$, ma esistono modi per renderla valida anche in altre situazioni.
Per arrivare alla formulazione generale, si trattano i punti del poliedro di controllo come se fossero disposti su una **griglia combinatoria**, che viene usata dall'**algoritmo di Casteljau**. Se $$h \neq k$$, questa griglia è _rettangolare_ e non è possibile concludere "rigorosamente" l'algoritmo.
Nell'applicazione, si è scelto di usare la tecnica dell'**innalzamento di grado**. 
Con questa tecnica, ad esempio, una griglia di $$4 \times 3$$ punti corrispondente a una superficie di bigrado $$(3,2)$$ può essere _mascherata_ come una griglia di $$4 \times 4$$ punti, ovvero come se fosse una superficie di bigrado $$(3,3)$$.

I punti considerati, chiaramente, dovranno rispettare delle condizioni specifiche. 
Considerando le quattro righe di tre punti dell'esempio di cui sopra, saremmo interessati ad aggiungere una colonna di punti, o un punto per ogni riga, a seconda di come si preferisce vederla. Manterremo il primo e l'ultimo punto della riga i-esima - $$\vec Q_{i,0} = \vec P_{i,0}$$ e $$\vec Q_{i,4} = \vec P_{i,3}$$ - e aggiungeremo tra di essi i punti:

$$\vec Q_{i,j} = \frac{j}{4-j} (\vec P_{i,j} - \vec P_{i,j-1}) \space\space\space con \space j = 1, 2, 3$$

Ovviamente è anche possibile aggiungere una riga di punti, o un punto per ogni colonna, in caso l'innalzamento di grado sia necessario per l'altra dimensione della griglia.

Il procedimento può essere ripetuto più volte per mascherare una superficie di grado $$h \neq k$$ nel caso $$\vert h-k\vert > 1$$. Questo è ciò che viene fatto dall'applicazione, in maniera trasparente all'utente, quando si decide di controllare una griglia di punti rettangolare, e dunque di lavorare con una superficie di Bezier di bigrado $$(h,k)$$ con $$h \neq k$$.

### **Perché usare una superficie di Bezier?**
Le superfici di Bezier hanno diversi pregi; ad esempio:

- se si desidera trasformare una superficie di Bezier mediante un'**affinità**, si possono trasformare i soli punti del poliedro di controllo per ottenere la superficie trasformata usando i punti trasformati;
- l'intera superficie di Bezier è contenuta nell'involucro convesso individuato dai punti del poliedro di controllo;
- vale la **proprietà di suddivisione**: preso un valore specifico lungo $$u$$ o lungo $$v$$, ad esempio $$\overline u$$, esso identifica due _"sottosuperfici"_ che sono di Bezier e che hanno punti del loro poliedro di controllo sia nuovi che facenti parte del poliedro di controllo originario; in più, si può notare che i due poliedri di controllo risultanti sono più piccoli e _"aderenti"_ alle porzioni di superficie che convergono;
- se tutti i punti del poliedro di controllo sono complanari ed equamente distanziati lungo le direzioni corrispondenti al crescere di $$h$$ e $$k$$, il foglio è una porzione di piano.

### **Perché non dovrei usare sempre una superficie di Bezier per descrivere superfici al computer?**
Le superfici di Bezier non sono esenti da difetti. 
Anzitutto, il poliedro di controllo può essere manipolato per ottenere una superficie "desiderabile", ma senza mai avere un vero controllo locale; modificare anche uno solo dei punti del poliedro di controllo significa dover ricalcolare la superficie nella sua interezza. In più, le superfici di Bezier non sono lo strumento adatto a risolvere problemi di interpolazione di una griglia di punti nello spazio.
Si può aggiungere, inoltre, che una superficie "_complessa_" - come potrebbe esserlo una superficie ondulata - può essere descritta solo con superfici di bigrado alto: eseguire questo genere di calcoli può impattare negativamente sulle performance.

### **Note sulle scelte progettuali**
Quando si valutano diverse coppie $$(u,v)$$ nel quadrato unitario al fine di ottenere punti del supporto della superficie che possano essere rappresentati graficamente, la computazione può risultare particolarmente impegnativa anche per CPU moderne.
Si è scelto di spostare questo genere di computazione sulla **GPU**, *graphics processing unit*, più comunemente nota come *scheda grafica*. Le proprietà di questa *unità di elaborazione* consentono di parallelizzare l'esecuzione della computazione su un gran numero di *core*; in più, i core di una GPU sono particolarmente efficienti nello svolgere operazioni matematiche, caratteristica che torna utile nel valutare la superficie, espressa matematicamente, in un numero elevato di punti.

Mentre la valutazione delle parte dipendente dalle variabili $$u$$ e $$v$$ viene fatta completamente su GPU, si è notato e sfruttato che parte dei coefficienti della formula rimane costante e sarebbe stata ricalcolata per ogni punto seguendo un approccio più basilare.
Al fine di rendere più efficiente questa computazione, appena prima di disegnare la superficie, si valutano i coefficienti binomiali usati nella formula e il loro prodotto per i punti corrispondenti; di seguito, i coefficienti vengono passati alla GPU, che termina la computazione valutando le funzioni di $$u$$ e $$v$$ e moltiplicandole in maniera ordinata per i rispettivi coefficienti.

Per esemplificare quanto detto, si pensi alla superficie di Bezier di bigrado $$(1,1)$$ e a come possa essere scritta come:

$$ \begin{aligned}
\vec P(u,v) = 
&\color{red} \binom{1}{0} \binom{1}{0} \color{black} &u^0(1-u)^{1-0} &v^0(1-v)^{1-0} &\color{red} \vec P_{0,0} \color{black} \space + \\
&\color{red} \binom{1}{0} \binom{1}{1} \color{black} &u^0(1-u)^{1-0} &v^1(1-v)^{1-1} &\color{red} \vec P_{0,1} \color{black} \space + \\ 
&\color{red} \binom{1}{1} \binom{1}{0} \color{black} &u^1(1-u)^{1-1} &v^0(1-v)^{1-0} &\color{red} \vec P_{1,0} \color{black} \space + \\ 
&\color{red} \binom{1}{1} \binom{1}{1} \color{black} &u^1(1-u)^{1-1} &v^1(1-v)^{1-1} &\color{red} \vec P_{1,1} \color{black} =  \\\\

= &\color{red} \binom{1}{0} \binom{1}{0} \color{black} & (1-u) &(1-v) &\color{red} \vec P_{0,0} \color{black} \space + \\
&\color{red} \binom{1}{0} \binom{1}{1} \color{black} & (1-u) &v &\color{red} \vec P_{0,1} \color{black} \space + \\ 
&\color{red} \binom{1}{1} \binom{1}{0} \color{black} & u &(1-v) &\color{red} \vec P_{1,0} \color{black} \space + \\ 
&\color{red} \binom{1}{1} \binom{1}{1} \color{black} & u &v &\color{red} \vec P_{1,1} \color{black} \space \\ 
\end{aligned}$$

I termini in rosso sono i termini considerabili costanti e pre-calcolabili su CPU.

**Si noti che, come diretta conseguenza di questa scelta progettuale, è necessario usare una GPU per poter rappresentare la superficie nell'applicazione sviluppata.**
In caso non si abbia una GPU adeguata, la superficie potrebbe non essere visualizzata. 
Ad ogni modo, ogni computer "recente" è dotato di un unità simile e non dovrebbe avere problemi nella visualizzazione.

L'applicazione è stata sviluppata in **[Unity](https://unity.com/)**, usando C# per il codice eseguito su CPU e HLSL per il _compute shader_ eseguito su GPU.
L'engine usa un **sistema di riferimento sinistrorso**, come si può notare mentre si manipolano le coordinate dei punti di controllo o mentre si visualizzano delle _handle_ (o _maniglie_) che rappresentano dei sistemi di riferimento locali rispetto ai punti di controllo.
Questo implica che, se si pensa a un _sistema di riferimento cartesiano monometrico_ xyz, l'asse x sarà descritto da un versore che indica la "destra" del sistema mondo, l'asse y da un versore che indica il "su" e l'asse z da un versore che spiega come muoversi "avanti" nel sistema mondo. Essendo un sistema sinistrorso, detti $$\vec i$$ e $$\vec j$$ rispettivamente i versori che indicano direzione e verso degli assi x e y, il versore che descrive l'asse z in direzione e verso può essere ottenuto come prodotto vettoriale dei versori $$\vec i$$ e $$\vec j$$, usando la regola della mano sinistra. 