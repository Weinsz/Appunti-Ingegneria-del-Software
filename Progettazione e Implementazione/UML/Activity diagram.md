### Concetto e struttura

Gli **activity diagram** nascono per rappresentare **sistemi concorrenti**, inoltre presentano una conformazione simile agli [[State diagram]], ma con varie differenze:
- al posto degli stati vi sono le **attività**;
- non si usano più le transizioni etichettate tramite eventi – queste sono quasi tutte **implicitamente temporizzate** (quando un’attività termina si passa alla prossima implicitamente);
- possono esserci **_azioni_ dentro le attività**;
- le _attività_ possono rappresentare **elementi esterni** al sistema.

La peculiarità che distingue questo tipo di diagrammi con lo state diagram è la **capacità di collegarsi con attività esterne** (ovvero non fatte dal sistema), questo fa sì che sia possibile utilizzare gli activity diagram come **collante** con e tra diversi casi d’uso.

Inoltre la **visuale parzialmente informale**, eppure leggermente più tecnica e profonda rispetto ai [[Use case diagram]], rende gli **activity diagram un ottimo mezzo di comunicazione interna** (per esempio con un manager).

### Livelli di astrazione

Si possono utilizzare i diagrammi delle attività per:
- descrivere la logica interna di un **business process** (caso più comune);
- descrivere il **flusso interno di un metodo**, con eventuali indicazioni di (pseudo)concorrenza;
- dettagliare il **flusso di un caso d’uso**, ovvero chiarire meglio il suo flusso di esecuzione rispetto ad altri diagrammi, come [[Sequence diagram]]. Questa rappresentazione è estremamente utile nei casi in cui, ad esempio, la concorrenza è un fattore rilevante.

È chiaro quindi che questo diagramma è utilizzabile ovunque, partendo dalla descrizione di piccole parti di codice fino ad arrivare alla descrizione generale nel sistema comprendendo le interazioni che ha con l’esterno.

### Sincronizzazione

[![](https://marcobuster.github.io/sweng/mdbook-plantuml-img/af21c24b0a7dd37b2206fbc231700165b0029223.svg)]

Attraverso l’uso di **barre** si possono stabilire dei punti di sincronizzazione (**JOIN** e **FORK**).  
I JOIN, se non diversamente specificato, vengono considerati in _**AND**_, ovvero per proseguire è necessario che terminino entrambe le attività.

Però si possono porre dei **vincoli diversi** per stabilire i criteri di soddisfacimento della barra di sincronizzazione (come un **_OR_**).

Si noti come gli activity diagram (a differenza di altri) **hanno sempre un inizio e una fine**, cosi come i diagrammi di sequenza, ma introducendo la **concorrenza**.

### Decisioni

[![](https://marcobuster.github.io/sweng/mdbook-plantuml-img/7e32d1534e172edc3dafc74e788073383a9c586e.svg)](https://marcobuster.github.io/sweng/mdbook-plantuml-img/7e32d1534e172edc3dafc74e788073383a9c586e.svg)

Si possono specificare nel flusso di esecuzione dei momenti di **decisione**. I rami d’azione intraprendibili in questi frangenti sono rappresentati tramite degli archi.

Le **decisioni** devono rispettare due proprietà:
1. gli archi collegati alla decisione devono essere **mutualmente esclusivi**;
2. l’**unione** delle condizioni di decisione deve essere sempre vera.

È bene puntualizzare che i punti di decisione sono _veri_ momenti di decisione umana: ciò significa che non vi è conoscenza sulla decisione che verrà presa siccome sarà dovuta a qualcuno di esterno e non dal sistema.

Questo fa capire la **differenza tra le decisioni e le guardie** dello [[State diagram]], infatti in questo caso non è possibile che vi sia sovrapposizione tra le risposte alle decisioni, mentre nello state diagram invece le guardie non garantivano di coprire tutte le situazioni che potevano verificarsi.

### Swim lane

Si può partizionare il diagramma al fine di rappresentare, sulle singole _activity_, delle particolari responsabilità che è bene dividere dalle altre. Queste vengono visualizzate tramite delle _“corsie”_ verticali che identificano _chi_ svolge una determinata attività.

![Swim lane esempio](https://marcobuster.github.io/sweng/assets/11_activity-swim-lane-example.png)