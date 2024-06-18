### Classificazione

Nell'ambito della **verifica e convalida** è possibile classificare le tecniche di analisi in due categorie:
1. **tecniche statiche**: basate sull'analisi degli elementi sintattici del codice. Es. metodi formali, [[Analisi Data Flow]] e [[Modelli statistici]];
2. **tecniche dinamiche**: basate sull'esecuzione del programma. Es. [[Verifica e Convalida/Analisi statica/Testing|Testing]] e [[Debugging]].

In generale, **è più facile determinare tecniche dinamiche** rispetto a quelle **statiche**. Per contro, una volta ideate e a patto di avere dimensioni del codice ragionevoli e costrutti sintattici non troppo complessi, **le tecniche statiche sono più veloci** nell'analizzare il codice e soprattutto più complete, dato che le tecniche dinamiche lavorano sui possibili stati del programma (potenzialmente infiniti).

Ovviamente diverse metodologie di verifica e convalida avranno i rispettivi pro e contro. 
#### Come si possono dunque confrontare queste tecniche?

![Classificazione tecniche verifica e convalida](https://marcobuster.github.io/sweng/assets/12_classificazione-tecniche-di-verifica-e-convalida.jpg)

Sopra è possibile osservare una **piramide a 3 dimensioni** che riassume dove si posizionano le tecniche di [[Verifica e convalida]] relativamente le une con le altre.
La **cima** della piramide rappresenta il **punto ideale** a cui tendere, nel quale è possibile affermare di esser riusciti a verificare perfettamente una proprietà arbitraria attraverso una prova logica (dal lato **statico**) o una ricerca esaustiva su tutti gli stati del problema (dal lato **dinamico**).

Tale punto ideale è **praticamente impossibile** da raggiungere per la stragrande maggioranza dei problemi che siamo interessati a risolvere. Bisogna scegliere **da quale versante** iniziare la scalata della piramide: **lato verde** (approccio **statico**) o **lato blu** (approccio **dinamico**).

Più ci si posiziona verso il basso, più si degenera in:
- **estrema semplificazione delle proprietà** (in basso a sinistra): si stanno in qualche modo **rilassando** eccessivamente gli obiettivi che si vogliono raggiungere.
  
  Ad esempio, se si vuole dimostrare che si sta usando un **puntatore correttamente** e nel farlo si sta semplicemente controllando che non valga `null`, **è cambiata la proprietà** che si vuole come obiettivo, vale a dire, controllare che un puntatore non valga `null` **non significa che lo si stia usando correttamente**.
- **estrema inaccuratezza pessimistica** (in basso al centro): è dovuta all'approccio pessimistico che ha come mantra:
> *Se non riesco a dimostrare l'assenza di un problema allora assumo che il problema ci sia.*

Ad esempio, si manifesta nei compilatori quando non riescono a dimostrare che una determinata funzione che deve ritornare un valore ritorni effettivamente un valore per tutti i possibili cammini `if`/`else if`/ecc.

-  **estrema inaccuratezza ottimistica** (in basso a destra): è dovuta all'approccio ottimistico che ha come mantra:
> *Se non riesco a dimostrare la presenza di un problema allora assumo che il problema non ci sia.* ^4dc587

Si tratta di una possibile deriva degli approcci legati al [[Verifica e Convalida/Analisi statica/Testing|Testing]]: con esso si cercano malfunzionamenti, se a seguito dei test non ne vengono trovati allora si assume che il programma funzioni correttamente.

A metà strada tra questi **estremi** si posizionano quindi **le varie tecniche di verifica e convalida**, ciascuna più o meno legata ai tre approcci sopra descritti. 
Tra queste si evidenziano le **dimostrazioni con metodi formali, il testing e il debugging**.


### Metodi formali

L'approccio dei **metodi formali** tenta di dimostrare l'**assenza di difetti/anomalie** nel prodotto finale. Si possono utilizzare diverse tecniche, come:
- [[Analisi Data Flow]]
- dimostrazione di correttezza delle specifiche logiche


### Testing

Il [[Verifica e Convalida/Analisi statica/Testing|Testing]] è l’insieme delle tecniche che si prefiggono di rilevare **malfunzionamenti**. 

> [!NOTE] Importante
Attraverso il testing **non si può dimostrare la [[Qualità del software#^f0fad0|correttezza]] ma solo aumentare la _fiducia_ dei clienti** rispetto all’**[[Qualità del software#^b2d6a2|affidabilità]]** del prodotto.

Le **tecniche di testing** possono essere molto varie e si raggruppano in:
- **white box**: si ha **accesso al codice da testare** e si possono cercare **difetti/anomalie** guardandolo da un **punto di vista interno**; viene anche detto **testing strutturale**;
- **black box**: **non si ha accesso al codice** ma si può testare e cercare malfunzionamenti **tramite le interfacce (di programmazione) esterne** (es. componenti dati da una ditta esterna);
- **gray box**: non si ha accesso al codice ma si ha solo **un'idea dell'implementazione** ad alto livello. Ad esempio, se so che il sistema segue il pattern [[Model View Controller (MVC)]] ci si può aspettare che determinate stimolazioni portino a chiamate/query al database mentre altre no. **Sapere com'è strutturata l'architettura mi può dare idee su come testarla.**

Si noti che il [[Test Driven Development (TDD)]] adotta una filosofia di testing completamente **black box**: imponendo che venga scritto prima il test del codice questo non può assumere niente sul funzionamento interno dell’oggetto di testing. Invece un caso di **white box** è quando, una volta scritto il codice e certi test, ci si accorge di non aver considerato un certo caso e si fa un altro test.


### Debugging

Dato un _programma_ e un _malfunzionamento noto e riproducibile_, il [[Debugging]] permette di localizzare le **anomalie** che causano i **malfunzionamenti**. A differenza del testing, infatti, è richiesta la conoscenza a priori di un malfunzionamento prima di procedere con il debugging.

Molto spesso viene usato il **debugging al posto del testing**, almeno a livello di terminologia: questo è un problema perché il debugging non è fatto per la “grande esecuzione”, ma al contrario, per esaminare in maniera granulare (a volte anche passo passo per istruzioni macchina) una determinata **sezione di codice in esecuzione** con lo scopo di trovare l’anomalia che provoca un malfunzionamento. 
Se si usassero le tecniche di debugging per effettuare il testing il **tempo speso sarebbe enorme**: il debugging osserva infatti _stati interni_ dell’esecuzione e, per rilevare un malfunzionamento, in questo modo sarebbe necessario osservare tutti i possibili - e potenzialmente infiniti - stati del programma.

Due possibili approcci al debugging sono:
1. partendo da un malfunzionamento _noto_ e _riproducibile_, si avvia una procedura di analisi basata sulla **produzione degli stati intermedi** dell’esecuzione del programma: _passo passo_ (a livello a piacere, da istruzione macchina a chiamata di funzione) si controllano tutti gli stati di memoria alla ricerca di uno inconsistente;
2. _**divide-et-impera**_: **il codice viene smontato** sezione per sezione e componente per componente in modo da poter trovare il punto contenente l’**anomalia**. Si possono mettere **breakpoint** o _“print tattiche”_.