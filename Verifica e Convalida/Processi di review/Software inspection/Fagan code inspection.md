Si tratta di una metodologia sviluppata da Michael Fagan all'IBM negli anni '70 e prevede che un **gruppo di esperti** esegua una serie di passi per verificare la correttezza del codice al fine di individuare possibili errori, incongruenze o altri problemi.
La **Fagan code inspection** è inoltre la **più diffusa** tra le tecniche di **ispezione**, oltre ad essere la più rigorosa e definita.


### Ruoli

Essendo un'attività di gruppo, nella Fagan code inspection vengono identificati diversi ruoli:
- **Moderatore**: è colui che *coordina* i meeting, *sceglie* i partecipanti e ha la *responsabilità* di far rispettare le regole. Di solito è una persona che lavora a un **progetto diverso** da quello in esame in modo da evitare conflitti d'interesse.
- **Readers e Testers**: non sono persone diverse, ma a seconda dei momenti i partecipanti possono coprire uno di questi due ruoli:
	- i primi *leggono il codice* al gruppo,
	- i secondi *cercano difetti* al suo interno;
	La lettura del codice è una vera e propria *parafrasi*, cioè un'interpretazione del codice nella quale si spiega quello che fa ma seguendo comunque la sua struttura.
- **Autore**: è colui che ha *scritto* il codice **sotto ispezione**; è un partecipante passivo che risponde solo a possibili *domande*. Ruolo simile a quello del [[Cliente sul posto|cliente]] in [[eXtreme Programming (XP)|XP]]: è pronto a rispondere a qualsiasi domanda per **accelerare il lavoro altrui**.



### Processo

Definiti i **ruoli**, secondo la tecnica **Fagan code inspection** il processo si compone così come segue:
1. **Planning**: in questa prima fase il **moderatore** sceglie i partecipanti, definendo i loro **ruoli** e il tempo da allocare all'ispezione, pianificando anche i vari incontri.
2. **Overview**: viene fornito a tutti i partecipanti del **materiale** sul progetto per permettere loro di farsi un'idea del **contesto** in cui l'**oggetto dell'ispezione** si inserisce, in **preparazione** della riunione effettiva.
3. **Preparation**: i partecipanti poi comprendono il codice e la sua struttura autonomamente sulla base anche del materiale distribuito nella fase precedente.
4. **Inspection**: la vera e propria fase d'**ispezione**, in cui si verifica che il codice soddisfi le regole definite e si segnalano eventuali anomalie o altri problemi. Il gruppo di esperti *esamina/parafrasa* il codice riga per riga, *confrontandolo* con le **specifiche** e cercando di *individuare* errori, incongruenze o altri problemi.
5. **Rework**: una volta scovati i malfunzionamenti o problemi, l'autore del codice si occupa di correggere i difetti individuati.
6. **Follow-up**: possibile re-ispezione del nuovo codice ottenuto dopo le correzioni della fase precedente.

La maggior parte delle fasi è abbastanza auto-esplicativa, ma è bene dare uno sguardo più approfondito all’attività di **ispezione** vera e propria.


#### Ispezione

**Obiettivo**: trovare e registrare i difetti **senza correggerli**.
La tentazione è sicuramente fortissima ma non è compito dei partecipanti alla riunione. Ciascuno di loro potrebbe infatti avere le proprie idee e preferenze e metterli d'accordo potrebbe non essere facile: si preferisce dunque che sia l'autore del codice a correggere successivamente.

Per evitare di perdere ulteriormente tempo sono previste **al massimo 2 sessioni d'ispezione di 2 ore al giorno**, durante le quali lavorare approssimativamente a **150 linee di codice all'ora**. Quest'ultimo vincolo è **molto variabile** in quanto cambia in base al linguaggio, al progetto, all'attenzione ai dettagli richiesta e alla complessità.

Una possibilità prevista in questa fase è anche quella di fare **test a mano**: si analizza il **flusso di controllo** del programma su una serie di casi di test così da verificarne il funzionamento.
Ancora più predominante è però l’uso di una serie di **checklist**.
#### Checklist

Rispetto all'attività di [[Utilità di un test|testing]], che a partire dai malfunzionamenti permetteva di risalire ai difetti e dunque agli sbagli commessi, il ragionamento per le **checklist** è inverso: si parte dagli sbagli che più frequentemente hanno portato certe anomalie nel codice e si controlla che nessuno di questi sia stato commesso di nuovo.

In letteratura è reperibile la **conoscenza** di tutto ciò che è meglio evitare poiché in passato ha portato **più volte ad avere anomalie** nel codice. Tale conoscenza è raccolta in **checklist comuni** per i vari linguaggi.

L’**ispezione del codice** funziona molto bene, questo anche perché tali checklist possono essere **redatte internamente** all’azienda, in base all'esperienza pregressa e alla storia di un certo progetto. Man mano che il progetto evolve, l’**individuazione di un nuovo sbaglio** si traduce in un’**evoluzione della checklist**: dalla prossima ispezione si controllerà di non aver commesso lo stesso errore.

#### Esempio Nasa

La NASA nel suo [_Software Formal Inspections Guidebook_](https://marcobuster.github.io/sweng/14_review/assets/13_nasa-software-inspection.pdf) (1993) ha formalizzato circa **2.5 pagine di checklist** per $C$ e 4 pagine per Fortran.

Sono divise in _functionality_, _data usage_, _control_, _linkage_, _computation_, _maintenance_ e _clarity_.

Di seguito sono elencati alcuni esempi dei punti di queste checklist:
> -  [ ]  Does each module have a single function?
> -  [ ]  Does the code match the Detailed Design?
> -  [ ]  Are all constant names upper case?
> -  [ ]  Are pointers not `typecast` (except assignment of `NULL`)?
> -  [ ]  Are nested `#include` files avoided?
> -  [ ]  Are non-standard usage isolated in subroutines and well documented?
> -  [ ]  Are there sufficient comments to understand the code?


### Struttura di incentivi/non disturbanti

Perché l'ispezione del codice com'è stata descritta funzioni bene, occorre prevedere una serie di **dinamiche positive** di incentivi non disturbanti al suo interno.

In particolare, è importante sottolineare che i **difetti trovati non devono essere utilizzati** per la **valutazione del personale**, in modo da evitare che i programmatori *nascondano* i difetti nel proprio codice, e remare contro  mina la *qualità* del prodotto.

D'altro canto si possono invece considerare per la **valutazione di readers e testers** i difetti trovati dopo l'ispezione, in modo che questi siano incentivati a fare l'ispezione più accurata possibile.
Non c'è invece il premio per chi di loro due trova gli errori, perché uno potrebbe far aggiungere $n$ errori per un tornaconto economico personale.