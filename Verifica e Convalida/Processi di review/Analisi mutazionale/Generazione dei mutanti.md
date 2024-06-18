Idealmente i mutanti generati dovrebbero essere il **meno differenti possibile** dal programma di partenza (es. < in <=), ovvero dovrebbe esserci **un mutante per ogni singola anomalia** che sarebbe possibile inserire nel programma. Più sono simili più sono difficili da trovare le anomalie, ma **maggiore è il valore di essere riuscito a trovarle**.

Questo richiederebbe però di generare **infiniti mutanti**, mentre per mantenere la suite di test **eseguibile in tempi ragionevoli** il numero di mutanti non dovrebbe essere troppo elevato: un centinaio è una buona stima, ma sarebbe auspicabile un migliaio.
Considerato il numero limitato, è necessario quindi concentrarsi sulla **qualità dei mutanti generati**, dove questa aumenta quanto più i mutanti permettono di scovare degli errori. Perciò vengono creati degli specifici **operatori** che dato un programma restituiscono dei mutanti utili.


### Operatori mutanti

Gli **operatori mutanti** sono delle funzioni (o *piccoli programmi*) che dato un programma $P$ generano un insieme di mutanti $\Pi$. Essi operano eseguendo piccole **modifiche sintattiche** che modificano la **semantica del programma**, senza però causare errori di compilazione.

Tali **operatori** si distinguono in **classi** in base agli **oggetti su cui operano**:
- **costanti e variabili**, per esempio scambiando l'occorrenza di uno con l'altra;
- **operatori ed espressioni**, per esempio trasformando `<` in `<=`, oppure `true` in `false`;
- **comandi**, per esempio trasformando un `while` in `if`.

Alcuni operatori possono essere anche specifici su alcuni tipi di **applicazioni**, come:
- operatori per **sistemi concorrenti**: operano principalmente sulle primitive di sincronizzazione, come eseguire una `notify()` invece che una `notifyAll()`;
- operatori per **sistemi object-oriented**: operano principalmente sulle interfacce dei moduli.

Essendo la **generazione dei mutanti** un'attività tediosa, la si affida spesso a **[[Automazione dell'analisi mutazionale|tool automatici]]**. Esistono però numerosi **problemi di prestazioni**, in quanto per ogni mutante serve: 
- modificare il codice,
- ricompilarlo,
- controllare che non si sovrapponga allo *spazio di compilazione delle classi* di altri mutanti
- e fare una serie di altre operazioni che comportano un pesante *overhead*.

Per questo i tool moderni lavorano spesso sull'**eseguibile** in sé (sul *bytecode* per Java); sebbene questo **diminuisca il lavoro** da fare per ogni mutante, è possibile che il codice eseguibile così ottenuto sia un *programma che non sarebbe possibile generare attraverso la compilazione*. Si espande dunque l'universo delle possibili anomalie, comprendendo anche quelle **non ottenibili**, aspetto da tenere in considerazione nella valutazione della [[Criterio di copertura dei mutanti#^eb3f8d|metrica di copertura]].


### High Order Mutation

^5a042e

Normalmente i mutanti vengono generati introducendo una **singola modifica** al programma originale, mentre nella **variante HOM** (***High Order Mutation***) si applicano invece modifiche a del **codice già modificato**. 
Chiamata così perché quasi tutti gli approcci ai tradizionali test mutazionali sono stati condotti inserendo singoli e piccoli difetti in un programma per creare mutanti detti del *primo ordine*, mentre questa variante tratta questi mutanti del primo ordine come semplici casi speciali di mutanti di ordine superiore.

La giustificazione per tale tecnica è che esistono alcuni casi in cui **è più complesso** trovare errori dopo aver applicato più modifiche, rispetto ad applicarne una sola. Può essere che un errore mascheri parzialmente lo **stato inconsistente** dell'altro rendendo più difficile il rilevamento di malfunzionamenti, cosa che **porta a generare test ancora più approfonditi**. 

> [!NOTE] Qual è il successo di quest'attività quindi?
> - **Stato di successo del testing**: ho avuto risultato **corretto**, dunque più sono i casi in cui ho un caso corretto, più ho fiducia che il programma funzioni.
> - **Stato di successo dell'analisi mutazionale**: il discriminante è se ottengo un risultato **diverso** dal programma $P$, potrebbe per esempio essere giusta la mutazione e il programma sbagliato, o sbagliati entrambi; dunque **non si parla di correttezza** del programma, ci interessa distinguere per capire la bontà dell'attività di testing.

Sembra una cosa negativa, ma in realtà ha un **effetto positivo**: dice che per fare quest'attività di testing potrei anche **non sapere** il risultato corretto.
Si ha un programma e una mutazione in esecuzione:
- se danno lo stesso risultato: problema, il test non riesce a distinguerli
- se il risultato è diverso: bene, il test riesce a distinguerli

Questa caratteristica può essere usata per [[Automazione dell'analisi mutazionale|automatizzare]] parte del lavoro pesante della definizione di una suite di test.

Come ci si potrebbe aspettare, aggiungere più errori a un programma difettoso tende a rendere più probabile che il programma fallisca e, quindi, più probabile che il test riveli la combinazione di errori.