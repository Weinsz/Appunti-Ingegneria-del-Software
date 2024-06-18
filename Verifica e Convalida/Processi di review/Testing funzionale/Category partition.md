La tecnica di **category partition** è una metodologia che permette di caratterizzare e identificare le [[Classi d'equivalenza]] del dominio di un problema a partire dalle sue **specifiche**. Può essere usata a **vari livelli** a seconda che si debbano realizzare test d'unità, test d'integrazione e/o [[Testing funzionale|test funzionali]].

Il metodo è composto da una **serie di passi** in sequenza:
1. **analisi delle specifiche**: in questa fase vengono identificate le **unità funzionali individuali** che possono essere verificate singolarmente; non necessariamente sono un'unica classe, è sufficiente che siano componenti facilmente separabili dal resto, sia a livello di testing che concettuale. Per ogni unità vengono quindi identificate delle caratteristiche, dette **categorie**, dei parametri e dell'ambiente in cui opera;
2. **scegliere dei valori**: per ogni categoria occorre scegliere quali sono i **valori sensati** su cui fare riferimento;
3. **determinare eventuali vincoli tra le scelte**, che non sono sempre indipendenti;
4. **scrivere test e documentazione**.

Per capire meglio ciascuna di tali fasi si dà un'esempio di utilizzo della tecnica di **category partition** prendendo come soggetto il comando `find` di Linux.


### Passo 1: analisi delle specifiche

Per prima cosa si analizzano le specifiche del comando:

>[!NOTE] `find <pattern> <file>`
> 
> Il comando find viene utilizzato per individuare una o più istanze di un determinato pattern in un file. Tutte le righe nel file che contengono il pattern vengono scritte sullo standard output. Una riga contenente il pattern viene scritta una sola volta, indipendentemente dal numero di volte in cui il pattern ricorre in essa.  
> 
> Il pattern è una qualsiasi sequenza di caratteri la cui lunghezza non supera la lunghezza massima di una riga nel file. Per includere uno spazio vuoto nel pattern, l'intero pattern deve essere racchiuso tra virgolette (`"`). Per includere una virgoletta nel pattern, è necessario utilizzare due virgolette (`""`) di seguito.

Vista la relativa semplicità, `find` è un’**unità funzionale individuale** che può essere verificata separatamente. Bisogna dunque individuarne i *parametri*: com'è chiaro dalla sintassi del comando essi sono due, il `pattern` da cercare e il `file` in cui farlo.

Ora ciascuno di tali parametri può possedere determinate caratteristiche, ed il compito di questa fase è **comprenderle ed estrarle**.
Tali caratteristiche possono essere di due tipi: **esplicite**, ovvero quelle ricavabili direttamente dalla **lettura delle specifiche**, e **implicite**, ovvero quelle che provengono dalla **nostra conoscenza** del dominio di applicazione e che quindi non vengono specificate.

Si può per esempio ottenere la seguente tabella:

|         Oggetto         | Caratteristiche esplicite                                                                                                           | Caratteristiche implicite                                                                      |
| :---------------------: | ----------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
|        `pattern`        | - lunghezza del pattern;<br>- pattern tra doppi apici;<br>- pattern contenente spazi;<br>- pattern contenente apici.                | - pattern tra apici con/senza spazi;<br>- più apici successivi inclusi nel pattern.            |
|   `file`  <br>(nome)    | Nessuna                                                                                                                             | - caratteri nel nome ammissibili o meno;<br>- file esistente (con permessi di lettura) o meno. |
| `file`  <br>(contenuto) | - numero occorrenze del pattern nel file;<br>- massimo numero di occorrenze del pattern in una linea;<br>- massima lunghezza linea. | - pattern sovrapposti;<br>- tipo del file.                                                     |

È importante **esplicitare le caratteristiche implicite** dei parametri dell’unità funzionale perché **le specifiche non sono mai complete** e solo così possiamo disporre di tutti gli elementi su cui ragionare nelle fasi successive.

Si deve prestare poi attenzione alla distinzione fatta tra il _nome_ del file e il suo _contenuto_: il primo infatti è un **parametro** che viene passato al comando per iniziarne l’esecuzione, mentre il secondo fa parte dell’**ambiente** in cui il comando opera ed è dunque soggetto ad una distinzione concettuale.

#### Alpha e Beta testing

Tuttavia spesso analizzare le specifiche non basta per comprendere tutte le variabili che entrano in gioco durante l'esecuzione di un programma. Bisogna infatti ricordare che ci sono moltissime altre *caratteristiche d'ambiente* che ancora **non sono state considerate**: la versione dell'OS, del browser, il tipo di architettura della macchina su cui gira il programma, ecc.

Perciò spesso la fase di [[Testing funzionale]] si divide in due fasi:
1. **alpha testing**: l’unità funzionale viene testata **in-house** su una macchina all’interno dello studio di sviluppo. In questa fase si considerano soprattutto le caratteristiche legate alle specifiche di cui sopra;
2. **beta testing**: per testare varie _configurazioni d’ambiente_ una versione preliminare del programma viene distribuita in un _ambiente variegato_ per osservare come esso si comporta sulle macchine di diversi utenti.

Per il momento però si considera solo la fase di **alpha testing** e le categorie ad essa relative.


### Passo 2: scegliere dei valori

Individuate le **caratteristiche** dei parametri e delle variabili d’ambiente da cui l’unità funzionale dipende, che prendono il nome di **categorie**, si passa quindi alla seconda fase.

In questa fase si devono identificare **tutti e i soli _casi significativi_ per ogni categoria**, ovvero quei valori della stessa che si ritiene abbia senso testare; poiché si tratta di un compito molto soggettivo è importante in questa fase avere **esperienza** e _know-how_ nel dominio d’applicazione.

Per capire meglio di cosa stiamo parlando si ritorna all'esempio considerando il parametro `pattern`. Per ciascuna delle sue categorie possono essere individuati vari casi significativi:
- **lunghezza del pattern**: vuoto | un solo carattere | più caratteri | più lungo di almeno una linea del file;
- **presenza di apici**: pattern non tra apici | tra apici | tra apici errati;
- **presenza di spazi**: nessuno spazio | uno spazio | molti spazi nel pattern;
- **presenza di apici interni**: nessun apice | un apice | molti apici nel pattern.

Da notare il _mantra_ già visto del “**nessuno**, **uno**, **molti**”, spesso molto utile in questa fase.

### Passo 3: determinare i vincoli tra le scelte

Trovati tutti i valori significativi delle categorie dell’unità funzionale, ***come possiamo costruire i casi di test da utilizzare per verificarne la correttezza?***

Si potrebbe pensare di testare **tutte le combinazioni** di valori significativi, facendo cioè il prodotto cartesiano tra le categorie. Nella pratica però risulterebbe in un numero esagerato di casi di test: già solo nel nostro semplice esempio questi sarebbero ben 1944, decisamente **troppi**.

Nel tentativo di evitare quest’**esplosione combinatoria** ci si accorge però che spesso le anomalie sorgono dall’interazione di **coppie di caratteristiche** indipendentemente dal valore assunto da tutte le altre: per esempio, un problema potrebbe presentarsi se si usa il browser _Edge_ sul sistema operativo _Linux_, indipendentemente da caratteristiche quali la dimensione dello schermo, l’architettura del processore ecc.

Per **ridurre** il numero di casi di test si sviluppa quindi la tecnica del _**pairwise testing**_, che riduce l’insieme delle configurazioni da testare a tutte le combinazioni di coppie possibili di valori. È quindi presente almeno un caso di test **per ogni coppia ipotizzabile** di valori: in rete e in Java sono presenti diversi [**strumenti**](https://www.pairwise.org/tools.html) che permettono di creare casi di test combinati con il metodo _pairwise_.

Un’ulteriore **tentativo** di ridurre il numero di casi di test prevede di definire una serie di _**vincoli**_ per la generazione delle coppie, escludendo particolari combinazioni di caratteristiche: così, per esempio si potrebbe escludere la coppia *"OS == Linux"* e *"browser == Edge"* perché sfruttando la conoscenza di dominio si sa che tale browser non è disponibile sul suddetto sistema operativo.
Per precisione, la creazione di vincoli prevede un **passaggio intermedio**: vengono definite una serie di **proprietà** (es. _NotEmpty_ o _Quoted_ per l’esempio su `find`) e si creano dei **vincoli logici** a partire da esse. I vincoli seguono poi una struttura tra le seguenti:
- **se**: si può **limitare l’uso di un valore** solo ai casi in cui è definita una **proprietà**. Per esempio, è inutile testare il caso _“il file non esiste”_ se la proprietà _NotEmpty_ si manifesta;
- **single**: alcune **caratteristiche prese singolarmente** anche se combinate con altre generano lo stesso risultato. Per esempio, se il file non contiene occorrenze del pattern cercato il risultato del programma è indipendente dal tipo di pattern cercato;
- **error**: alcune caratteristiche generano semplicemente **errore**, come per esempio se si omette un parametro come il nome file.


### Passo 4: scrivere i test

Fissati i vincoli e fatti i calcoli combinatori si procede a **enumerare iterativamente tutti i casi di test generati** continuando ad aggiungere **vincoli** fino ad arrivare ad un **numero ragionevole**.

Ovviamente i casi di test avranno poi bisogno di **valori specifici** per le caratteristiche: non basta dire “pattern con apici all’interno”, bisogna creare un pattern aderente a questa descrizione. Fortunatamente quest'operazione è solitamente molto facile, anche con l'uso di tool automatici.


### Conclusioni

Per quanto intuitiva e utile, la tecnica di **category partition** presenta due **criticità**:
1. individuare i **casi significativi** delle varie caratteristiche può essere difficile e si può sbagliare, anche utilizzando mantra come “_zero_, _uno_, _molti_”;
2. una volta generati i casi di test serve comunque un “**oracolo**” che fornisca la risposta giusta, ovvero quella che ci si attende dall’esecuzione sul caso di test. L’attività non è dunque _completamente_ automatizzabile.

Va però detto che esistono delle tecniche di **property-based testing** che cercano di eliminare la necessità di un oracolo considerando particolari **proprietà che dovrebbero sempre valere** durante l’esecuzione (***invarianti***) piuttosto che analizzare il risultato dell’esecuzione dei casi di test per determinare la correttezza del programma.