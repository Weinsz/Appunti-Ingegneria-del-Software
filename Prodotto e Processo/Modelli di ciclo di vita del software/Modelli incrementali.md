Un **modello incrementale** è un particolare [[Modelli iterativi|modello iterativo]] in cui nelle iterazioni è inclusa anche la consegna, permettendo così di sviluppare sw a poco a poco, rilasciandone di volta in volta parti che costruiscano **incrementalmente** il programma finito.

Da sottolineare la differenza tra incrementale e iterativo:
- **implementazione iterativa**: dopo aver raccolto le specifiche e aver progettato il sistema, iterativamente sviluppo i componenti, li integro nel prodotto finale, dunque consegno.
- **sviluppo incrementale**: l'iteratività interessa ogni fase, comprese quelle di specifica e realizzazione.

Lo sviluppo incrementale **riconosce la criticità** della variabilità dei requisiti e la integra nel processo. La manutenzione non è più quindi una particolarità ma viene vista come normale e perfettamente integrata nel modello. 
In tal senso, la richiesta di una nuova feature o la correzione di un errore generano gli stessi step di sviluppo.

Nel 1993 nasce, in contrapposizione al [[Modello a cascata]], il cosiddetto [[Modello a fontana]], che estende il concetto di iterazione permettendo in qualunque momento di **tornare alla fase iniziale**.
Vi sono poi altri modelli incrementali, come [[Pinball Life-Cycle]], i [[Modelli trasformazionali]], il [[Metamodello a spirale]] e il [[Modello COTS]].
## Problemi dei modelli incrementali

Non esiste il modello perfetto, infatti anche questi modelli hanno problemi.
Viene **complicato il lavoro di planning**: bisogna pianificare tutte le iterazioni e lo stato di avanzamento è meno visibile; inoltre, la ripetizione di alcune fasi richiede di avere sempre sul posto gli esperti in grado di eseguirle. Il processo di revisione ad ogni iterazione potrebbe non convergere mai a una versione finale, infatti a volte vengono tolte delle parti o il cliente cambia le richieste.

Ma cos'è un'iterazione, quanto dura? Tagliare verticalmente sulle funzionalità non è facile, soprattutto considerando che il prodotto quando viene consegnato deve essere funzionante e progettato per consentire l'aggiunta di nuove features facilmente. Vi sono diversi rischi dunque:
- voler aggiungerne troppe nella prima iterazione
- overhead dovuto a troppe iterazioni
- avere un eccessivo overlapping tra le iterazioni, ergo mancanza di tempo per ricevere il feedback dell'utente (es. Microsoft Office 2020 e 2019 vengono sviluppati contemporaneamente).
Paper a riguardo: [_From Waterfall to Iterative Development – A Challenging Transition for Project Managers_](https://bit.ly/3SYYs8y)
## Sviluppi futuri

Oggi lo sviluppo delle IA sta facendo enormi passi in avanti (ChatGPT, Copilot). Negli anni a venire sicuramente giocheranno un ruolo importante anche nella gestione del [[Processo di produzione del software|processo produttivo di un software]], o forse già ora?