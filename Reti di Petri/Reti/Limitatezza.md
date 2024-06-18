Una proprietà importante delle reti di Petri è la **limitatezza**: indica se le possibili evoluzioni della rete possono essere **limitate** o **illimitate**, quindi se gli stati raggiungibili sono in **numero finito o infiniti**. Volendo dare una definizione più formale è possibile dire che una rete $P/T$ con marcatura $M$ si dice **limitata** se e solo se:
$$
\exists k \in \mathbb N\quad \forall M' \in R(P/T, M) \quad \forall p \in P \quad M'(p) \le k
$$
cioè se è possibile fissare un **limite al numero di gettoni** della rete, con qualsiasi evoluzione della rete. Così si può dire che la **rete è limitata**. 
Se ciò non si verifica, esiste almeno un posto in cui è possibile aumentare **tendenzialmente all’infinito** il numero di gettoni. Va sottolineato che la limitatezza di una rete può dipendere dalla sua **marcatura iniziale**.

![[Limitatezza.png]]

### Da reti di Petri a automi

Precedentemente è stato mostrato come a partire da un automa a stati finiti sia possibile ricavare una rete di Petri, ma è possibile fare **il contrario**? 
**Se la rete è limitata allora l’insieme di raggiungibilità è finito**, di conseguenza è possibile definire una corrispondente FSM che prende ogni marcatura raggiungibile come un proprio _stato_ e ne traccia le *transizioni di stato* dell’automa conseguenti alla transizione scattata nella rete di Petri. Due considerazioni:
- gli **stati** sono le possibili marcature dell’insieme di raggiungibilità;
- le **transizioni** sono gli eventi che permettono il passaggio da una configurazione alla successiva.

Riuscire a passare dalle reti di Petri agli automi permette di utilizzare i **tool di analisi** che sfruttano proprietà già consolidate per gli automi. L’unico problema è che **questo approccio vale solo per reti limitate**.