Gli altri modelli erano **descrittivi**, ora invece si vedranno modelli più **prescrittivi**.
Le metodologie agili **nascono dal basso**, da chi sviluppa, per colmare un disagio prevalente nell'uso dei metodi classici e tradizionali. Dunque è un mix di buone pratiche o idee che già ci sono nell'ingegneria del sw classica. Infatti esiste un **manifesto**.

## [Manifesto](https://agilemanifesto.org/iso/it/manifesto.html)

Nelle parole di Fowler e i suoi collaboratori, per migliorare il modo in cui viene sviluppato il software, è necessario dare più importanza ad alcuni valori rispetto agli altri:

![[Manifesto Agile.png]]
**Libro: Agile!** di Bertrand **Meyer**

Drastico cambiamento rispetto allo sviluppo tradizionale, che si evolve anche in un business model diverso.
- Piuttosto che farsi pagare a **programma finito**, gli sviluppatori vengono **pagati a tempo di sviluppo**, dando però la garanzia al cliente di lavorare durante tale periodo esclusivamente per lui e al massimo delle proprie capacità. 
- Al **rapporto conflittuale col cliente**, in cui ciascuno cerca di fregare l'altro, si sostituisce dunque una collaborazione più estesa in cui anche [[Cliente sul posto|il cliente diventa parte del team di sviluppo]].

Di seguito alcuni dei più famosi metodi Agile.

### Lean Software

L'azienda Toyota investì risorse per migliorare il suo processo produttivo. Nacque così il progetto *Lean Manufacturing*, che mirava ad una produzione di massa stile americana, ma cercando di ridurre gli sprechi al massimo, data la scarsità di risorse del Paese. Da ciò presero ispirazione anche alcuni dev agile, che idearono il concetto di **lean software**, con l'obiettivo di **ridurre gli sprechi**, rimuovendo tutti quei sottoprodotti non consegnati al cliente (es. testing, prototipi…) e che non generano valore. Toyota incentivò il riutilizzo per più tempo possibile degli stessi strumenti; parallelamente, i dev dovranno evitare di produrre funzionalità (codice) inutili, puntando invece a riusare il codice pre-esistente o framework per facilitare il lavoro.

Come per Toyota, anche nell'ing. del sw l'utilizzo della **parallelizzazione dei processi** porta grossi vantaggi, per esempio sarà più facile trovare prima dei possibili errori, e quindi bloccare altri processi prima che vengano terminati, limitando sprechi. Altro metodo: **posticipare le scelte vincolanti** in modo da risparmiare risorse; più possibilità mi lascio aperte, più mi sarà facile adattarmi, a patto però che l'adattamento sia rapido.

Infine oltre al processo si cercherà di prendersi cura degli sviluppatori: l'azienda vorrà quindi investire nel loro benessere per tenerseli buoni e fedeli, in modo che possano anche lavorare meglio.

### Kanban
![Kanban](https://marcobuster.github.io/sweng/assets/02_kanban.jpg)

**Obiettivo:** **minimizzare il lavoro in corso** (*work in progress*), cioè concentrarsi in ogni momento su una sola cosa per evitare continui *context-switch* che costituiscono una perdita di tempo, che accumulandosi può generare un grosso overhead. Le attività possono per esempio essere organizzate in una tabella con 5 colonne:

| **Backlog**              | **To-Do**                                | In Esecuzione | Testing | Fatto |
| ------------------------ | ---------------------------------------- | ------------- | ------- | ----- |
| Richieste<br>dal cliente | Attività da fare<br>in questa iterazione |               |         |       |
La tabella dà a colpo d'occhio info sullo stato del progetto per chiunque. Ogni **card (storia)** è assegnata a un dev (o coppia nel [[Pair programming]]), in modo che nella colonna *In Esecuzione* ci sia solo una card per dev (o coppia). Qualora il lavoro di un dev blocchi quello di un altro, quest'ultimo dovrà dare una mano a chi sta lavorando sulla funzionalità di cui lui ha bisogno.

### Scrum 

^934e12

Importante che l'intero team si concentri sull'**iterazione attuale** in maniera organizzata, infatti ogni membro deve sapere con precisione cosa fare, **senza un continuo cambio di richieste dal cliente**. 

Per fare ciò, **bisogna fissare i requisiti** durante le iterazioni, che devono essere **brevi**, da 2 a 4 settimane, in modo da permettere ai dev di lavorare in maniera stabile, senza doversi adattare continuamente a nuove richieste. Solo **al termine di ogni iterazione** si permetterà al cliente di rimettere in discussione i requisiti.

### Crystal

^dc1741

Sebbene non sia molto apprezzata o usata, questa tecnica introduce l'interessante concetto di **comunicazione osmotica** . Nel [[Modello a cascata]] la comunicazione è fatta tramite **documenti rigidi** ed è settorializzata. Con Crystal invece la conoscenza viene vista come se fosse appartenente all'intero team ([[Proprietà collettiva]]), e non al singolo, questo perché viene condivisa tra i vari membri, come per **osmosi**. Così il codice e le sue responsabilità non appartengono più al singolo dev ma al gruppo, dunque ogni persona deve curare ogni parte del progetto.

In questo modo il processo si irrobustisce: l'assenza di una persona non rompe più tutto. Il [[Pair programming]] si basa su questo concetto, tra i due componenti la conoscenza è condivisa; Crystal estende il concetto all'intero team.
Si capisce facilmente però che questa tecnica funziona solo con team piccoli (max 8/10 persone), anche se altre metodologie agili come SAFE tentino di scalarla a team più grandi.

### [[eXtreme Programming (XP)]]
