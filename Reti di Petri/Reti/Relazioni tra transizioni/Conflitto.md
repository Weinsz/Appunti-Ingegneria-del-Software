Due transizioni $t_1$ e $t_2$ sono in:
- **conflitto strutturale**  $\Longleftrightarrow \text{pre}(t_1) \cap \text{pre}(t_2) \neq \varnothing$   
- **conflitto effettivo in una marcatura M** $\Longleftrightarrow$:
	- $M\space [ t_1 > \land \space M\space [ t_2 >$
	- $\exists p \in \operatorname{Pre}(t_1) \cap \operatorname{Pre}(t_2) \mid M(p) < W(\langle p, \\ t_1 \rangle) + W(\langle  p, \\ t_2\rangle)$ 

Analizzando i due tipi di conflitto è possibile notare che:
- due transizioni sono in **conflitto strutturale** se l’intersezione dei due preset non è vuota e quindi hanno posti in ingresso in comune: possono quindi interferire tra loro. Il conflitto strutturale dipende solo dalla **topologia della rete**, infatti non vengono citate le **marcature**;
- due transizioni sono in **conflitto effettivo** se sono entrambe abilitate in una marcatura $M$ ed esiste un **posto in ingresso in comune ai due preset** tale per cui il numero di gettoni in quel posto è minore della somma dei pesi dei due flussi che vanno dal posto alla transizione, quindi il **posto in ingresso non ha abbastanza gettoni** per far **scattare** entrambe le transizioni. Entrano quindi in conflitto sulla disponibilità di gettoni nel preset.


Esiste una versione **rilassata** della definizione di conflitto esplicitata dalla seguente formula:
$$
M\space [ t_1 > \land \space M\space [ t_2 > \land \space \lnot M\space[\space t_1t_2 >
$$

Questa proposizione indica che il conflitto è presente se $t_1$ e $t_2$ sono abilitate in una marcatura M e non è possibile la sequenza $t_1 t_2$ a partire da $M$. Ma cosa vuol dire che è una _versione rilassata_? Per capirlo si osservi l’esempio sottostante (nell'esempio $t_0$ indica $t_2$):

![[Conflitto 1.png]]

Secondo le definizioni di conflitto che sono state date, in questa rete di Petri è presente un **conflitto per la prima definizione di conflitto effettivo** data ma non più per la definizione rilassata, per via dell'arco che va da $t_1$ a $p_1$ (senza il quale sarebbe presente un **conflitto sia per la prima definizione che per la seconda**), in quanto dopo lo scatto di $t_1$ quest’ultima è ancora abilitata e può far scattare $t_0$, e quindi non rientra più sotto la definizione rilassata di conflitto.

Lasciando da parte la definizione rilassata, è facile osservare a questo punto che la definizione per il **conflitto strutturale** si basa solo sui preset, ignorando quindi qualsiasi arco in uscita, mentre quella per il **conflitto effettivo** ragiona **anche** sugli effetti dello scatto delle transizioni. Si noti che **la presenza di un conflitto strutturale non implica** obbligatoriamente **la presenza di un conflitto effettivo** in quanto quest’ultimo per esistere necessita che venga soddisfatta una **condizione in più**. Al contrario invece un **conflitto effettivo implica la presenza di un conflitto strutturale** in quanto le condizioni di quest’ultimo sono comprese in quelle del conflitto effettivo.

Di seguito viene mostrato un esempio di conflitto _effettivo_ e _strutturale_.

![[Conflitto effettivo e strutturale.png]]