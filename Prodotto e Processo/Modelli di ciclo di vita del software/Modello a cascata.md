## Caratteristiche e punti di forza
![Modello a cascata](https://marcobuster.github.io/sweng/assets/02_waterfall-model.png)
**Storia**: Nato negli anni '50 e diventato famoso negli anni '70 grazie allo sviluppo del grosso sw per la difesa aerea, chiamato **SAGE** (_Semi-Automated Ground Environment_).

Il modello a cascata organizza le fasi in **step sequenziali**, come una catena di montaggio. Viene forzata la **progressione lineare**, ma **non è previsto tornare indietro** a uno step prima.

Pur variando tanto, la maggior parte dei processi che segue questo modello include almeno le seguenti fasi in quest'ordine:
1. **Requisiti**
2. **Progetto**
3. **Codifica**
4. **Testing**
5. **Prodotto**

Ogni step produce un **output**, detto **semilavorato**, dato in input allo step successivo. Proprio per questo il modello a cascata è detto **document-based**: tra una fase e l'altra si crea un documento, che è il mezzo di trasmissione dell'informazione. Ciò permette una **buona separazione dei compiti** tra dipendenti che lavorano al progetto: ognuno è infatti specializzato in una sola fase, e una volta prodotto il documento, il suo coinvolgimento finisce e può essere assegnato ad altri lavori. Così è facile capire che il modello a cascata ha introdotto un certo rigore, mai visto fino ad allora nello sviluppo sw, dando così importanza anche alla **documentazione** del lavoro.

La linearità del modello rende possibile **pianificare i tempi** con precisione e monitorare lo stato di avanzamento in ogni fase e stimare la rispettiva durata, determinando così il tempo di completamento del progetto. Tuttavia è una stima a senso unico: una volta finita una fase non si può ridurre il tempo speso, in caso di problemi si può solo provare ad assorbire il ritardo.
## Criticità
^criticita

Sebbene questo modello abbia il grande pregio di aver posto l'attenzione sulla comunicazione tra gli elementi del progetto nel periodo storico in cui il modello di sviluppo più diffuso era di tipo _code-and-fix_, esso soffre di diverse criticità.
- **Non prevede una fase di manutenzione**: il sw prodotto assume di non dover apportare modifiche al progetto dopo averlo consegnato, impedendo quindi di tornare indietro. Ovviamente quest'assunzione viene quasi sempre smontata: ogni sw è destinato ad evolvere, [[Qualità del software#^1207bd|più un sw viene usato più cambia]]. Una volta finito lo sviluppo si possono rilasciare piccole patch che però disallineano la documentazione prodotta precedentemente col sw reale.
- Soffre di generale **rigidità**, che mal si sposa con la flessibilità richiesta dall'ambiente di sviluppo sw. Il non poter tornare indietro implica un **congelamento dei sottoprodotti/semilavorati**; questo è particolarmente critico per le stime e specifiche fatte nelle prime fasi, che sono fisiologicamente le più incerte.
- **Monoliticità**: la pianificazione è orientata al singolo rilascio, con eventuale manutenzione solo sul codice. Ovviamente è una visione fallace (sw destinato ad evolvere).

## Who’s Afraid of The Big Bad Waterfall?
Libro: **The Leprechauns of Software Engineeering** di **Laurent Bossavit**.

Il modello a cascata non è mai stato veramente elogiato, ma è sempre stato utilizzato come **paragone negativo** per proporre altri modelli o varianti. Nel tempo la sua presentazione è stata erroneamente attribuita al paper [_“Managing the development of large software systems: concepts and techniques”_](https://dl.acm.org/doi/10.5555/41765.41801) di W.W. Royce, di cui veniva citata solo la prima figura. Royce stava a dire il vero presentando quel modello per descrivere la sua esperienza nello sviluppo, per poi proporre altri concetti più moderni, come lo sviluppo incrementale, che non sono però mai stati colti dalla comunità scientifica.
Anche noi usiamo questo modello solo come paragone negativo, anche se alcuni suoi aspetti si sono mantenuti come **linee guida generali**, come l'ordine delle fasi.
Esistono due tipi di modelli:
- **prescrittivi**: forniscono indicazioni precise e **obbligatorie** da seguire per svolgere un processo;
- **descrittivi:** colgono certi aspetti e caratteristiche di particolari processi esistenti, ma **non obbligano** a seguirli rigorosamente.
Tutti i modelli ricadono nel descrittivo, mentre i modelli **[[Metodologie Agile|Agile]]** tendono a essere più di tipo prescrittivo.

## Riepilogo Pro e Contro

| Pro                               | Contro                     |
| --------------------------------- | -------------------------- |
| Document-based                    | Rigidità                   |
| Buona suddivisione compiti        | Congelamento sottoprodotti |
| Semplice pianificazione dei tempi | Monoliticità               |
