Per risolvere i problemi esposti in [[Approccio Ingegneristico]], si sviluppa una serie di processi per lo sviluppo sw. Essi non assicurano la bontà del programma finito, ma possono garantire la presenza di **proprietà desiderabili** del prodotto, vale a dire le **qualità**.

Le qualità del prodotto, che rappresentano un valore per le persone, si dividono in due tipi:
1. **qualità esterne**: vengono colte dal cliente
2. **qualità interne**: vengono colte solo dallo sviluppatore

Le qualità interne influenzano molto quelle esterne. Per esempio, se ho un codice efficiente, il mio sw sarà più veloce.

Distinzione tra **requisiti** e **specifiche**:
- **requisiti**: sono ciò che il cliente vuole dal software. Vengono spesso cambiati in corso d'opera o espressi erroneamente, infatti è necessaria un'interazione continua tra le parti.
- **specifiche**: sono ciò che è stato formalizzato dallo sviluppatore, a partire dai requisiti imposti dal cliente. Si tratta di una definizione più rigorosa di che cosa dovrà fare il sw. Inoltre, se i requisiti sono mal posti, anche le specifiche saranno sbagliate

## Qualità che un software dovrebbe avere ##

Un sw di **qualità** deve **funzionare, essere bello e farmi diventare ricco**.

- **Un sw deve funzionare:**
	1. **Correttezza**: un sw è corretto se soddisfa la specifica dei suoi **requisiti funzionali**. Proprietà matematica dimostrabile formalmente. ^f0fad0
	2. **Affidabilità**: un sw è affidabile quando ci si può fidare del suo funzionamento, che faccia ciò che gli è stato chiesto. Se è difficile perseverare la correttezza (**proprietà assoluta**), l'affidabilità è invece **relativa**: un sw può essere affidabile nonostante abbia errori (anche per colpa del cliente). Dunque è importante specificare nel contratto un range di tollerabilità. ^b2d6a2
	3. **Robustezza e/o Safety (innocuità)**: un sw è robusto se si comporta in modo accettabile anche in circostanze non previste nella specifica dei requisiti, senza generare effetti troppo negativi.
- **Un sw deve essere bello:**
	1. **Usabilità:** un sw è usabile o **user-friendly** se i suoi utenti lo considerano facile da usare. Si possono fare esperimenti per testare e quantificare il grado di usabilità del sw ponendolo di fronte ad altre persone ([[#^1f90c2|NN23]]). Si tratta di una qualità costosa per via delle risorse da impiegare, come analisi sia quantitative (tramite numeri/metriche) sia qualitative (feedback).
	2. **Prestazioni ed Efficienza:** l'efficienza è una **qualità interna** e misura come il sw utilizza le risorse del computer. La performance invece è una **qualità esterna** basata sui requisiti dell'utente. Ha effetto sull'usabilità, spesso considerata alla fine dello sviluppo visto che vari avanzamenti tecnologici possono efficientare algoritmi (non a livello di complessità) o processi prima costosi.
	3. **Verificabilità:** un sw è verificabile se le sue proprietà lo sono facilmente. Importante poter dimostrare la correttezza e la performance di un programma, per farlo serve anche che il sw sia **leggibile**. La verifica si può fare con **metodi formali o informali**, per esempio il **testing**. La verificabilità è una qualità interna, ma certe volte può essere esterna, esempio in ambiti la cui sicurezza è critica il cliente chiede la verificabilità di alcune proprietà.
- **Un sw deve farmi diventare ricco:**
	1. **Riusabilità:** le componenti del sw che costruiamo dovrebbero essere il più riusabili possibile: per farlo va aumentata l'adattabilità, evitando di legare troppo il sw allo specifico contesto. Si può avere anche un aumento dell'affidabilità e della verificabilità, in quanto il codice riutilizzato è stato già testato e verificato al momento della sua creazione. Utilizziamo un prodotto per costruirne un altro, ovviamente non sempre è sicuro per via dei contesti diversi ([[#^a30bef|MI15]]). **Es. Ariane 5**
	2. **Manutenibilità:** per manutenzione sw si intendono tutte le modifiche apportate al sw dopo il primo rilascio. Va divisa in due proprietà:
		1. **Riparabilità:** un sw è riparabile se i suoi difetti possono essere corretti con una quantità di lavoro ragionevole.
		2. **Evolvibilità:** un sw è evolvibile se può evolvere aggiungendo funzionalità. Importante da considerare sin dall'inizio. Studi rilevano come essa decresca col passare delle release [[#^1207b|(L27-28)]].
	3. **Perfettibilità:** migliorare le qualità del sw in modo da aumentare la qualità sia degli aspetti esterni che interni, senza alterare le funzionalità richieste dalle specifiche. Perfeziona quindi features senza aggiungerne/rimuoverne.

### Leggi rilevanti

- **Prima legge di R. Glass:** la mancanza di requisiti è la prima causa del fallimento di un progetto.
- **Legge di Nielsen-Norman NN23:** l'usabilità è misurabile. ^1f90c2
- **Legge di McIlroy MI15:** riutilizzare il sw permette di incrementare la produttività e la qualità. ^a30bef
- **Leggi di Lehman L27-28:** un sistema che viene usato cambierà. Un sistema che evolve incrementa la sua complessità a meno che non si lavori appositamente per ridurla. ^1207bd

### Debito tecnico

^461572

Durante lo sviluppo sw è facile incontrare problemi che possono essere risolti subito oppure dopo. Però maggiore è il numero di problemi irrisolti maggiore sarà il **debito tecnico** accumulato, che sarà più difficile da rimuovere e più complesso.
## Qualità del processo ##

> Un progetto è di qualità se segue un buon **processo**.

Con processo, mi riferisco al **Process** in [[Approccio Ingegneristico]]. Il prodotto sw è influenzato dal processo usato per svilupparlo, infatti si può parlare anche di **qualità del processo**.

Anche un processo deve funzionare, essere essere bello e farmi diventare ricco, ma bisogna interpretare queste parole in maniera differente.

Quali caratteristiche deve avere un processo di qualità?

- **Un processo deve funzionare:**
	1. **Robustezza:** un processo deve essere robusto agli imprevisti (cambio personale o di specifiche), attestato da certificazione come CMM: Capability Maturity Model
- **Un processo deve essere bello:**
	1. **Produttività:** metrica difficile da misurare. Numero di linee di codice e tempo-uomo sono fallaci
- **Un processo deve farmi diventare ricco:**
	1. **Tempismo**
		- **Scadenze:** un processo deve consegnare un prodotto in tempi stabiliti, in modo da rispettare i tempi del mercato. Conveniente la tecnica dello **sviluppo incrementale**, cioè la consegna frequente di parti sempre più grandi del prodotto, conquistando magari il cliente prima che sia finito.
		- **Volatilità dei requisiti:** possono cambiare nel tempo, va quindi mantenuto un equilibrio tra il loro sviluppo e aggiornamento, senza rischiare di lavorare a requisiti non più presenti.
		- **Cogliere l'attimo:** il progetto deve essere realizzato in relazione al contesto; meglio non sviluppare un sw già esistente e radicato, risulta poco produttivo.