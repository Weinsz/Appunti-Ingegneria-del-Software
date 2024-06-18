Si è accennato più volte al concetto di “**sequenza**” di operazioni su una variabile. Più formalmente, si definisce **sequenza di operazioni per la variabile $a$ secondo il cammino $p$** la concatenazione della tipologia delle istruzioni che coinvolgono tale variabile, e si indica con $\text{P}(p, a)$.

Considerando per esempio il seguente programma $C$:
```c
01  void main() {
02      float a, b, x, y;
03      read(x);
04      read(y);
05      a = x;
06      b = y;
07      while (a != b)
08          if (a > b)
09              a = a - b;
10          else
11              b = b - a;
12      write(a);
13  }
```

si può dire che:
$P([1,2,3,4,5,6,7,8,9,7,12,13],a)=$ $\boxed{a_2}\space\boxed{d_5}\space\boxed{u_7}\boxed{u_8}\space\boxed{u_9}\space\boxed{d_9}\boxed{u_7}\space\boxed{u_{12}}\space\boxed{a_{13}}$  

Eseguendo questo tipo di operazione **su tutte le variabili e per tutti i cammini** del programma si potrebbe verificare la presenza di eventuali **anomalie**, ma come noto **i cammini sono potenzialmente infiniti** quando il programma contiene **cicli e decisioni**: per scoprire quali percorsi segue effettivamente l’esecuzione del programma lo **si dovrebbe eseguire e quindi uscire dal campo dell’analisi statica**.

### Espressioni regolari

Però non tutto è perduto: un caso di cammini contenenti **cicli** e **decisioni** è possibile rappresentando un insieme di sequenze ottenute dal programma $P$ utilizzando delle **espressioni regolari**. Con $P([1\rightarrow],a)$ si indica infatti l'espressione regolare che rappresenta **tutti i cammini che partono da dall'istruzione 1 per la variabile $a$**.

Questo perché nelle espressioni regolari è possibile inserire, oltre che una serie di parentesi che isolano **sotto-sequenze**, anche due simboli particolari:
1. la **pipe** (|) che indica che i simboli (o le sotto-sequenze) alla propria destra e alla propria sinistra si escludono a vicenda, ne è presente solo uno;
2. l'**asterisco** (\*) che indica che il simbolo (o la sotto-sequenza) precedente **può essere ripetuto da $0$ a $n$ volte.**

Grazie a questi simboli è possibile rappresentare rispettivamente **decisioni** (*pipe*) e **cicli** (*asterisco*). Prendendo per esempio il codice precedente, è possibile costruire $P([1\rightarrow],a)$ come:
![[Esempio Regex.png]]
Si osservi come $\color{red}\boxed{u_7}$ **si ripeta due volte**: questo può rendere _fastidioso_ ricercare errori, per via della difficoltà di considerare **cammini multipli**. Comunque sia, una volta ottenuta un’espressione regolare è facile **verificare l’eventuale presenza di errori** applicando le solite [[Regole Data Flow]] (nell’esempio non ce n’erano).

Bisogna però fare attenzione a un’aspetto: le **espressioni regolari** così costruite rappresentano **tutti i cammini possibili** del programma, ma **non tutti e i soli cammini**! Trattandosi di oggetti puramente *matematici*, infatti, le espressioni regolari sono necessariamente **più generali** di qualunque programma: esse non tengono infatti conto degli **effetti che le istruzioni hanno sui dati** e delle relative **proprietà** che si possono inferire.

Riprendendo ad esempio l’espressione regolare sopra, essa contiene la sequenza nella quale il ciclo viene eseguito **infinite volte**, ma vedendo il programma è facile capire che tale comportamento **non sia possibile** in realtà: diminuendo progressivamente $a$ e $b$, a seconda di chi sia il maggiore, si può dimostrare che prima o poi i due convergeranno allo stesso valore **permettendo così di uscire dal ciclo**.

In effetti uno stesso programma può essere rappresentato tramite un **numero infinito di espressioni regolari valide**. Si potrebbe addirittura argomentare che l’espressione regolare $(\boxed{u}\space|:\boxed{d}\space|:\boxed{a})*$  possa rappresentare **qualsiasi programma**.

Allontanandosi però dai casi estremi, si dimostra essere **impossibile** scrivere un *algoritmo* che, dato un qualsiasi programma, riesca a generare un’espressione regolare che rappresenti **tutti e soli i suoi cammini possibili** senza osservare i valori delle variabili.
Bisogna dunque accontentarsi di trovare espressioni regolari che rappresentino **al meglio** l’esecuzione del programma, ovvero con il **minor numero di cammini impossibili** rappresentati.

Nell’[[Analisi Data Flow]] tramite **espressioni regolari** è dunque necessario tenere conto che il modello generato è un’**astrazione pessimistica**: se viene notificata la **presenza di un errore** non si può essere certi che esso ci sia veramente, in quanto esso potrebbe derivare da un **cammino non percorribile**.