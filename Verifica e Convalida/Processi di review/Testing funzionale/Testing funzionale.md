Si introduce ora una **nuova attività di testing** che parte da presupposti completamente diversi rispetto a quelli del **testing strutturale**.

Il **test funzionale** infatti è un tipo di test che si concentra sulla verifica del comportamento del programma dal punto di vista dell'**utente finale**, senza considerare il suo funzionamento interno. In altre parole, si tratta di un approccio **black box** in cui non si ha (o comunque non si sfrutta) la conoscenza del codice sorgente. 

Talvolta questo può essere l'**unico approccio possibile** al testing, come nel caso di validazione del lavoro di un **committente esterno**; altre volte invece si decide volontariamente di farlo, concentrandosi sul **dominio delle informazioni** invece che sulla struttura di controllo.
Il test funzionale prende in considerazione le **specifiche** (e **non i requisiti**) del progetto per discriminare un **comportamento corretto** da uno scorretto. Esso permette infatti di identificare errori che **non possono essere individuati** con criteri strutturali, come per esempio funzionalità non implementate, flussi di esecuzione dimenticati o errori di interfaccia e di prestazioni.

Le tecniche di test funzionale si possono raggruppare in:
- **metodi basati su grafi**: oltre alle tecniche già viste [[Object oriented testing#^ee4313|in precedenza]], si può per esempio lavorare anche sui [[Sequence diagram|diagrammi di sequenza]], con una singola funzionalità dall'inizio della stimolazione alla terminazione;
- **suddivisioni del dominio in [[Classi d'equivalenza]]**: si possono raggruppare i valori del dominio che causano lo stesso comportamento in *classi d'equivalenza*, così da testare tutti i comportamenti distinti invece che tutti i possibili valori del dominio. Occorre fare attenzione a non fare l’inverso, ovvero a concentrarsi sui soli valori appartenenti ad una classe di equivalenza ignorando il resto; ne è un esempio il [[Category partition]]
- **analisi dei valori limite ([[Test di frontiera]])**: si testano tra tutti i possibili valori del dominio quelli **tra una categoria e l’altra**, in quanto essi possono più facilmente causare malfunzionamenti;
- **collaudo per confronto**: si confronta la *nuova versione* del programma con la vecchia, assicurandosi che non siano presenti peggioramenti. Non solo si possono confrontare gli eseguibili, ma anche **specifiche formali eseguibili** che rappresentino le caratteristiche importanti del software.

Non tutte le metodologie di **testing funzionale** ricadono però in una di queste categorie, e la più notevole è sicuramente il **[[Testing delle interfacce]]**.

Si vedono in dettaglio:
- [[Testing delle interfacce]]
- [[Classi d'equivalenza]]
- [[Test di frontiera]]
- [[Category partition]]
- [[Object orientation e testing funzionale]]