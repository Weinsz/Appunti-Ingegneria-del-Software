La **conservatività** è una proprietà di una rete rispetto a una **funzione** $H$ che assegna un **peso** a ogni posto della rete, e ognuno di questi pesi è *positivo*.

#### Conservatività rispetto a una funzione
Una rete $P/T$ con marcatura iniziale $M_0$ si dice **conservativa rispetto a una funzione di pesi** $H : P \rightarrow \mathbb N^+$ se e solo se:
$$ \forall M \in R(P/T, M_0) \quad \sum_{p \in P} H(p) M(p) = \sum_{p \in P} H(p) M_0(p)$$

Cioè, per ogni marcatura $M$ raggiungibile dalla marcatura iniziale $M_0$ e data una funzione $H$, si dice che la rete è **conservativa** se la sommatoria dei gettoni di ogni posto pesati per la funzione $H$ è **costante**.

#### Conservatività rispetto a una marcatura

Una rete $P/T$ con marcatura iniziale $M_0$ è **conservativa** in una marcatura $M$ (*fissata*) se esiste almeno una funzione $H$ per cui è **conservativa**.


### Conservatività $\Rightarrow$ [[Limitatezza]]

Esiste un **legame tra conservatività e limitatezza**: una rete che garantisce la **conservatività** è limitata, ma non è detto il viceversa; dunque la limitatezza è una condizione necessaria ma non sufficiente per la conservatività.

#### Dimostrazione

Assumendo che $\sum_{p \in P} H(p) M_0(p) = k$ (per la marcatura iniziale), allora, data la conservatività vale:  $$\forall M \in R(P/T, M_0) \quad \sum_{p \in P} H(p) M(p) = \sum_{p \in P} H(p) M_0(p) = k$$
Quindi scegliendo uno dei posti, esempio $p' \in P$, allora vale: $$ \sum_{p \in P \setminus \{p'\}} H(p) M(p) \space + H(p')M(p') = k$$, dunque: $$ H(p')M(p') = k \space - \sum_{p \in P \setminus \{p'\}}H(p) M(p) \le k$$ $$ H(p')M(p') \le k $$
questa vale per qualsiasi $p \in P$, in quanto scelto a caso, dunque:  $$ \forall p \in P\quad H(p)M(p) \le k $$
$$ \forall p \in P \quad  M(p) \le \frac{k}{H(p)} \le k $$

Quindi, se esiste almeno una marcatura di $p$ il cui numero di gettoni è diverso da $0$, il suo contributo è positivo ma limitato da k. Questo vale per ogni posto all’interno della rete, riconducendosi di conseguenza alla definizione di [[Limitatezza]].

### Rete strettamente conservativa

La **conservatività stretta** è un caso particolare di conservatività.
Una rete $P/T$ si dice **strettamente conservativa** se è **conservativa** rispetto a una funzione $H$ che assegna tutti pesi uguali (**ad es. 1**):
$$ \forall M \in R(P/T, M_0) \quad \sum_{p \in P}1 \cdot  M(p)=\sum_{p \in P}1\cdot M_0(p)$$

La sommatoria del numero di gettoni per ogni posto in una _qualsiasi marcatura $M$_ è **costante**, ovvero è uguale alla sommatoria dei gettoni della marcatura iniziale $M_0$ per ogni posto. 
In altre parole, dopo lo scatto di una transizione viene forzata la **distruzione del gettone in ingresso** e la **generazione di un altro in uscita**.

Matematicamente questo concetto si può esprimere anche tramite questa espressione:
$$
\forall t \in T \text{ (non morta)}\quad \sum_{p \in \operatorname{pre}(t)} W(\langle p,  t \rangle) = \sum_{p \in \operatorname{post}(t)} W(\langle t, p \rangle)
$$

> [!NOTE] Differenza tra le due espressioni sopra
> Le due espressioni sopra esprimono lo stesso concetto, ma la prima si riferisce alle **marcature** (stati) analizzando dinamicamente calcolando gli stati raggiungibili mentre l’altra all’**aspetto topologico** della rete (ovvero i pesi degli archi).

Si precisa che per quanto riguarda la seconda formula, è più generale rispetto alla prima, ma **potrebbe erroneamente considerare non strettamente conservative** reti che **invece lo sono**.