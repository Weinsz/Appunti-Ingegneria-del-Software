
Nelle attività di **verifica e convalida** si cercano degli **errori**, ma questo termine può assumere più significati in base al contesto. Dunque è importante capire di quale tipo di **errore** si sta parlando, andando a introdurre termini diversi, come **malfunzionamento, difetto, sbaglio**.

Esistono dei glossari e vocabolari di terminologia comune redatti dalla IEEE, ad esempio *Systems and software engineering — Vocabulary*, che possono essere adottati dagli sviluppatori come standard in modo da snellire la comunicazione tra di loro.


### Malfunzionamento (o guasto, *failure*)

Un **malfunzionamento** è uno **scostamento dal corretto funzionamento** del programma.
**Non dipende dal codice** e in generale non ci si accorge di esso osservando il codice ma solo da un punto di vista più esterno, usando il programma.

Il malfunzionamento potrebbe riguardare sia le **specifiche** (quindi relativo alla fase di **verifica**) sia i **requisiti** (fase di **convalida**, cioè non rispetta le aspettative). Secondo il vocabolario sopracitato:

> [!NOTE] failure
> 1. cessazione della capacità di un prodotto di eseguire una funzione richiesta o della sua incapacità di eseguire entro limiti precedentemente specificati.
>    _ISO/IEC 25000:2005, Software Engineering — Software product Quality Requirements and Evaluation (SQuaRE) — Guide to SQuaRE.4.20._
> 2. un evento in cui un sistema o un componente del sistema non esegue una funzione richiesta entro i limiti specificati.
>    
> _NOTA: Un malfunzionamento può verificarsi quando si incontra un difetto._

#### Esempio

Di seguito è illustrato un esempio di malfunzionamento:
```java
static int raddoppia(int par) {
    int risultato;
    risultato = (par * par);
    return risultato;
}

static void main(String[] args) {
    int risultato = raddoppia(3);
    System.out.println(risultato);  // 9
}
```

La funzione dovrebbe ritornare il doppio del numero in ingresso, ma se passiamo 3 in argomento verrà ritornato 9.


### Difetto (o anomalia, *fault*)

Un **difetto** è il **punto del codice** che causa il verificarsi del **malfunzionamento**.
Si nota che è **condizione necessaria** (ma non sufficiente) per il verificarsi di un malfunzionamento.

> [!NOTE] fault
> 1. una manifestazione di un errore nel software.
> 2. un passaggio, un processo o una definizione di dati errata in un programma per computer. 
> 3. un difetto in un dispositivo o componente hardware. Sinonimo: *bug*
>    
> _NOTA: Un difetto, se riscontrato, può causare un malfunzionamento._

Nell’esempio di codice precedente, il difetto è in `risultato = (par * par)`.

Il **difetto** è **condizione non sufficiente** per il verificarsi di un malfunzionamento in quanto, ad esempio, **non si verificano malfunzionamenti** in caso l'argomento passato in `raddoppia` sia 0 o 2. In quei casi il raddoppio avverrebbe in maniera corretta. 
Un altro esempio di questa proprietà è il caso in cui esistano _“più anomalie che si compensano”_: se si sta utilizzando una libreria per operazioni su temperature in gradi Fahrenheit, ponendo il caso che si stia partendo da gradi Celsius, dovrà essere effettuata una conversione. Se in questa conversione è presente un difetto che però si riflette allo stesso modo in fase di riconversione per restituire il risultato, i due difetti combinati non si manifestano in un malfunzionamento.

Spesso i difetti/anomalie si annidano nella gestione di casi particolari o eccezionali del programma (*edge cases*), in quanto il flusso di controllo ordinario è solitamente il più testato.


### Sbaglio (*mistake*)

Uno **sbaglio** è la **CAUSA** di un **difetto/anomalia** ed è solitamente un **errore umano**.

> [!NOTE] mistake
> 1. un'azione umana che produce un risultato errato  
> 
> NOTA: La disciplina della tolleranza alle anomalie distingue tra un'azione umana (uno sbaglio), la sua manifestazione (un difetto/anomalia hw o sw), il risultato dell'anomalia (un malfunzionamento) e la misura in cui il risultato è errato (l'errore).

Riferito al codice sopra, possibili sbagli possono essere:
- **errori di battitura** (scrivere `*` invece di `+`);
- **concettuali** (non sapere cosa significa raddoppiare);
- relativi alla **padronanza del linguaggio** (non sapere che `*` non è il simbolo dell'addizione).

Risulta fondamentale capire quale sia **la causa di uno sbaglio** in modo da poter intraprendere azioni correttive per il futuro (es. studiare meglio la sintassi del linguaggio).

#### Esempio emblematico: Ariane 5

Il primo volo di prova del razzo Ariane 5 è fallito a causa di un problema al software di controllo che ha portato all’autodistruzione del missile.
- **Malfunzionamento**: il razzo esploso e non si voleva che accadesse.
- **Difetto (anomalia)**: il malfunzionamento si è verificato per un'eccezione di **overflow**, sollevatosi durante una conversione **da un 64 bit `float` a un 16 bit signed `int`** che indicava il valore della *velocità orizzontale*. Questo ha bloccato sia l’unità principale che il backup dell’unità stessa.
- **Sbaglio**: tale eccezione non veniva gestita perché questa parte del software era stata ereditata dal predecessore Ariane 4, la cui traiettoria faceva sì che non si raggiungessero mai velocità orizzontali non rappresentabili con `int` 16 bit. La variabile incriminata non veniva protetta per gli _“ampi margini di sicurezza”_, a posteriori di certo non così ampi.

Il comportamento della variabile non era mai stato analizzato coi dati relativi alla traiettoria da seguire.