### Definizione informale

Un **vantaggio** delle reti di Petri è che possono essere viste in modo informale dal cliente. Risulta infatti facile rappresentare una rete di Petri come un grafo in cui ogni nodo rappresenta o un **posto** o una **transizione**, mentre gli archi i collegamenti presenti tra le transizioni e i posti. Il grafo è **bipartito**, cioè un grafo in cui i nodi di un tipo sono messi in relazione **solo** coi nodi dell'altro tipo.

Per ogni posto è assegnato uno specifico numero di **gettoni** (o ***token***), eventualmente anche infiniti.

> [!NOTE] Stato
> La **disposizione dei gettoni nei posti** in un dato momento nella rete ne determina il suo stato complessivo.

![[Rete informale.png]]

Per far **evolvere** lo stato della rete, l'**assegnamento dei gettoni deve poter variare**. La trasformazione di uno stato è effettuata dallo **scatto di una transizione**:
- una transizione si dice **abilitata** quando la **somma dei gettoni dei posti collegati in ingresso** è maggiore di un certo numero;
- una transizione **scatta** quando, dopo essere stata *abilitata*, consuma i gettoni dei posti collegati in ingresso e ne genera altri all'interno dei posti collegati in uscita.

> [!NOTE] Importante, da non confondere
> È importante notare come i gettoni **non si spostano** da un posto a un altro conseguentemente a uno scatto, ma vengono **distrutti** nei posti in ingresso alla transizione e **generati** nei posti in uscita. Quest’ultima considerazione è importante per capire che i gettoni _non sono necessariamente sempre dello stesso numero in ingresso e in uscita_.

Tramite questo **modello operativo** è **facile mostrare al cliente** quando cambia qualcosa all'interno del sistema, perché risulta più intuitivo rispetto a un linguaggio logico e descrittivo.

Lo **svantaggio** è che fornisce **informazioni parziali** su **come** il sistema compie le azioni che dovrebbe eseguire, rischiando di essere una via di mezzo tra **specifica** e **documento di design**. Si può comunque chiamare specifica perché viene **definito totalmente** il comportamento del sistema, senza ambiguità.

La rete descritta è dunque una **macchina di riferimento** da usare come **confronto** per stabilire la **validità del sistema** sotto esame, come se fosse un **oracolo**.


### Definizione matematica

Come già detto, esistono numerosi *dialetti* di **reti di Petri**. In questo caso vediamo le **PT net** (*reti con posti e transizioni*) che sono le più classiche, successivamente verranno descritte delle estensioni e riduzioni di queste reti.

Una rete di Petri classica è una 5-upla $[P, T; F, W, M_0]$, dove:
- $P$ è l'insieme degli **identificatori dei posti**;
- $T$ è l'insieme degli **identificatori delle transizioni**;
- $F$ è l'insieme delle **relazioni di flusso**;
- $W$ è la **funzione peso** che associa un peso ad ogni flusso;
- $M_0$ è la **marcatura iniziale**, ovvero l'assegnamento inziale dei gettoni.

In generale, si definisce come **marcatura** una particolare *configurazione dell'assegnamento dei gettoni* all'interno della rete di Petri, sia essa iniziale o una sua evoluzione.

> [!NOTE] Nota
> Da notare che P e T a livello matematico sono degli insiemi di **identificatori** che non si sovrappongono (dato che si tratta di entità differenti) a cui poi verrà assegnato un significato, quindi precedentemente sono stati associati a posti e transizioni, ma di fatto sono tutti **identificatori**.

Data la 5-tupla appena descritta esistono le seguenti proprietà:
- $P \cap T = \varnothing$;
- $P \cup T \neq \varnothing$; (una rete in cui non c’è nulla non è una rete: almeno un posto o una transizione ci devono essere);
- $F \subseteq (P \times T) \cup (T \times P)$;
- $W : F \rightarrow \mathbb N \setminus \{ 0 \}$;
- $M_0 : P \rightarrow \mathbb N$.

Inoltre:
- $\text{pre}(a) = \{ d \in (P \cup T) \space | \space \langle d, a \rangle \in F \}$. Dunque, il **preset** di un nodo $a$ è l'insieme degli elementi $d$ appartenenti all'unione di posti e transizioni tali che esiste una relazione di flusso tra $d$ e $a$ appartenente a $F$. In pratica, questo insieme **preset** rappresenta l'insieme degli **identificatori antecedenti ad $a$**.
-  $\text{post}(a) = \{ d \in (P \cup T) \space | \space \langle a, d \rangle \in F \}$. Dunque, simmetricamente, questo insieme **postset** rappresenta l'insieme degli **identificatori successivi ad $a$**.

Tutto ciò rappresenta la **parte statica** delle reti di Petri, ovvero quando vengono osservate in un preciso istante di tempo in base alla topografia/struttura della rete, senza considerare i cambiamenti che potrebbero avvenire al loro interno (**parte dinamica**).


### Comportamento dinamico

#### Abilitata

Una transizione $t \in T$ è **abilitata** in una marcatura $M$ se e solo se:
$$
\forall p \in \text{pre}(t)\quad M(p) \ge W(\langle p, t \rangle).
$$
In notazione, $M\space[t>$ vuol dire che $t$ è **abilitata** nella marcatura $M$.

Significa che *per ogni elemento $p$ collegato in ingresso a $t$ esiste un **numero di gettoni** maggiore o uguale del **peso dell'arco** che collega $p$ e $t$*.
Di conseguenza, **non è necessario conoscere l’intera rete** per poter affermare che una transizione sia abilitata o meno, ma è sufficiente controllare la zona che comprende i posti appartenenti al preset: proprietà di **località dell'analisi**.


#### Scatto

Lo **scatto** di una transizione $t \in T$ in una marcatura $M$ produce nel momento successivo una nuova marcatura $M'$ tale per cui:
$$
\begin{align}
&\forall p \in \text{pre}(t) \setminus \text{post}(t) \quad M'(p) = M(p) - W(\langle p, t \rangle) \\
&\forall p \in \text{post}(t) \setminus \text{pre}(t) \quad M'(p) = M(p) + W(\langle t, p \rangle) \\
&\forall p \in \text{pre}(t) \cap \text{post}(t) \quad M'(p) = M(p) - W(\langle p, t \rangle) + W(\langle t, p \rangle) \\
&\forall p \in P \setminus \text{pre}(t) \cup \text{post}(t) \quad M'(p) = M(p)
\end{align}
$$
In notazione, $M\space [\space t > M'$ significa che lo scatto di $t$ nella marcatura $M$ produce una nuova marcatura $M'$.

> [!NOTE] Importante
> È importante notare come una **transizione può scattare** nel caso in cui non abbia alcun elemento nel suo preset (nessun $p$), perché rileggendo la clausola di abilitazione, se non c'è nessun posto è comunque verificata e quindi abilitata, e **può scattare**; questo significa che la transizione in questione **non possiede prerequisiti** per scattare.