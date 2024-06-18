Inizialmente è stato detto che esistono diversi dialetti per le reti di Petri. Una possibile **estensione** consiste infatti nel fissare una **capacità massima** rispetto al **numero di gettoni ammissibili in un posto**. Un esempio potrebbe essere quello in cui in un sistema possono essere presenti $k$ lettori contemporaneamente e non di più. 

Avendo la possibilità di definire una capacità dei posti, diventa possibile **forzare la limitatezza della rete**.

#### Come cambia la regola di abilitazione?

$$ \forall p \in \text{pre}(t) \quad M(p) \ge W(\langle p, t \rangle)$$
$$ \color{orange} \forall p \in \text{post}(t) \quad M(p) + W(\langle t, p \rangle)  \le K(p)$$

#### Tale estensione aumenta la potenza espressiva oppure è semplicemente una scorciatoia?

Quest'estensione non è altro che una **tecnica per facilitare la scrittura della rete**.

### Posto complementare

Un **posto complementare** è un posto avente **in uscita** un **arco di egual peso, ma di direzione opposta,** verso ognuna delle transizioni del posto considerato.
Formalmente, dato un posto $p$ si dice che un posto $p_c$ è il suo complementare se e solo se:
$$ \forall t \in \text{post}(p) \quad \exists \langle t, p_c \rangle \in F \quad W(\langle t, p_c \rangle)=W(\langle p, t \rangle) $$
$$ \forall t \in \text{pre}(p) \quad \exists \langle p_c, t \rangle \in F \quad W(\langle p_c, t \rangle)=W(\langle t, p \rangle) $$

Questa formula garantisce che la **somma** del numero di gettoni **tra il posto e il suo complementare** sia costante.

![[Capacità posti.png]]

Nella rete con capacità dei posti limitata per poter far scattare la transizione $t_0$, è necessario sia che i posti nel suo preset abbiano gettoni sufficienti sia che dopo il suo scatto il posto $p_0$ non superi il limite assegnatogli. 
Volendo scrivere la stessa rete utilizzando il metodo classico visto fino ad ora basta aggiungere un **posto complementare** che quindi rende le reti **equipollenti**, ossia aventi lo **stesso valore espressivo**.

Finché nel posto complementare esistono dei gettoni, la transizione $t_0$ può infatti scattare; quando però $P0_{comp}$ non avrà più gettoni, $t_0$ non sarà più abilitata e nel posto $p_0$ ci sarà il numero massimo di gettoni possibili. 

> [!NOTE] Proprietà della somma dei gettoni
> Notare come la somma dei gettoni del posto considerato sia esattamente la capacità massima scelta in precedenza.

### Problema con reti non *pure*

**La proprietà del posto complementare vale solo per le reti pure**, vale a dire:
$$ \forall t \in T \quad \text{pre}(t) \cap \text{post}(t) = \varnothing$$
ovvero _le reti che_ _**per ogni transizione**_ _hanno preset e postset disgiunti_.

Utilizzando i **posti complementari** è possibile rappresentare **solo le _reti pure equivalenti_**, ma _non tutte le reti in generale_: finché non sono presenti archi in entrata e uscita allo stesso posto dalla stessa transizione non sorge alcun tipo di problema.

#### Come è possibile superare questa limitazione? 

Si possono pensare due approcci:
1. si trova un altro approccio diverso dai posti complementari;
2. si cerca di dimostrare che una rete non pura ha sempre una equivalente rete pura; quindi, si procede a rimuovere la capacità utilizzando i posti complementari.

Entrambe le soluzioni non sono così immediate.
#### Come cambia qui la regola di abilitazione?

$$ \forall p \in \text{pre}(t) \quad M(p) \ge W(\langle p, t \rangle)$$
$$ \forall p \in \text{post}(t) \setminus \color{orange} \text{pre}(t) \color{white} \quad M(p) + W(\langle t, p \rangle)  \le K(p)$$
$$\color{orange} \forall p \in \text{post}(t) \cap \text{pre}(t) \quad M(p) + W(\langle t, p \rangle)  - W(\langle p, t \rangle) \le K(p)$$