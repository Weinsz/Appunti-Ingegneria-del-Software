### Quando non va utilizzato [[eXtreme Programming (XP)|XP]]

**Kent Beck** non esclude mai la possibilità di usarlo: egli sostiene che è possibile provare a utilizzarlo sempre (pur non essendo sempre possibile *"provare"*), a patto che vengano rispettati i [[Prodotto e Processo/eXtreme Programming/Tecniche/Tecniche|12 punti]].

Da ciò si può concludere che [[Metodologie Agile|Agile]] non si può usare quando:
- l'ambiente non permette l'applicazione dei 12 punti (es. team in luoghi diversi)
- ci sono **barriere manageriali** (es. team troppo numerosi)
- ci sono **barriere tecnologiche**, come quando per esempio non è possibile utilizzare una macchina specifica condivisa da tutte le coppie per i test, ostacolando l’[[Integrazione continua]].
- ci sono **troppi stakeholders** diversi e tra loro in contrasto
- situazioni in cui la consegna incrementale non è sensata (es. una centrale nucleare, coff coff Chernobyl).

### Critiche da Meyer

Di seguito sono elencate alcune critiche all’XP fatte da Meyer:
- **Sottovalutazione dell'up-front**: cioè la progettazione iniziale prima di partire; per Meyer, a parte casi eccezionali (dev o manager molto bravi), la progettazione non può essere fatta in modo **totalmente incrementale**. Questo problema nell'esperienza del prof non è così presente, ma potrebbe essere *survivorship bias*
- **Sopravvalutazione delle user stories**: secondo Meyer sono **troppo specifiche** per sostituire i **requisiti**
- **Mancata evidenziazione delle dipendenze tra user stories**: esse dovrebbero essere indipendenti tra loro, ma questo non è quasi mai possibile; nel design classico si utilizzano i diagrammi di Gantt per chiarire tutte le dipendenze tra i diversi punti del sistema da realizzare
- **TDD può portare a una visione troppo ristretta**
- **Cross functional team**: se i team sono troppo disomogenei, con tante singole figure specializzate in un campo e queste devono collaborare in coppia, ci possono essere dei problemi.

Questi punti cercano di evidenziare la **mancanza di approfondimento** e chiarezza dell’XP su alcuni aspetti dell’approccio a un **lavoro fornito ad un cliente**.
### Mesi uomo

Tra i manager è comune pensare che la stima temporale in mesi uomo sia visualizzata come un ramo di iperbole, quindi col tempo che diminuisce in modo esponenziale all'aumentare dei mesi uomo.
Tale stima però non considera i tempi di **overhead**, impiegato per la comunicazione e il resto che non sia implementazione. **I mesi uomo non sono quindi una metrica valida**, ma sono utili solo **a posteriori** per valutare se un approccio a un problema si è dimostrato valido.

Nella realtà, **all’aumentare delle persone aumenta il bisogno di comunicare**, quindi non sempre porta ad un aumento lineare della **produttività**. Quando il lavoro è strettamente sequenziale e non parallelizzabile, anche all’aumentare delle persone il tempo non cambia, anzi **si rischia di rallentarlo**.

**In caso di ritardi** nell’avanzamento del progetto, invece che aggiungere personale rischiando di peggiorare la situazione, posso:
- Discutere la **deadline** col cliente, se possibile
- Diminuire la **portata** del progetto
- Diminuire la **qualità** del progetto, diminuendo il testing (**fortemente sconsigliato ma accade spesso**).

Nel mondo dello sviluppo sw spesso c’è un **numero ideale di persone** per un progetto, dopo il quale avere persone in più causa solo confusione, rallentando i tempi a causa della comunicazione. Il numero può anche essere grande, ma dipende dall’entità del progetto (esempio: space shuttle).

In generale, le metodologie Agile iniziano a **non funzionare più** se il team è **più grande di 8-10 persone**, e bisogna poi esplorare altre pratiche.