Risulta in qualche modo intuitivo considerare la **relazione di concorrenza** come la relazione opposta a quella di [[Conflitto]]: due transizioni $t_1$ e $t_2$ sono in:
- **concorrenza strutturale** $\Longleftrightarrow \text{pre}(t_1) \cap \text{pre}(t_2) = \varnothing$   
- **concorrenza effettiva in una marcatura M** $\Longleftrightarrow$:
	- $M\space [ t_1 > \land \space M\space [ t_2 >$
	- $\forall p \in \operatorname{pre}(t_1) \cap \operatorname{pre}(t_2) \mid M(p) \ge W(\langle p, \\ t_1 \rangle) + W(\langle  p, \\ t_2\rangle)$.

Quest’ultima formula indica che due identificatori delle **transizioni** sono in **concorrenza effettiva** se e solo se, per tutti i posti che hanno in comune, c’è un numero di **gettoni sufficienti per farle scattare entrambe**.

In questo caso **non esiste alcun legame tra concorrenza strutturale ed effettiva**, diversamente da quanto si è visto in precedenza per le relazioni di [[Conflitto]]. Se si verificano le condizioni per avere una concorrenza strutturale è **possibile** che le due transizioni **non siano abilitate** (invalidata prima condizione), oppure se si verificano le condizioni per avere concorrenza effettiva è **possibile** che $t_1$ e $t_2$ abbiano posti in comune che posseggano abbastanza gettoni per entrambe.

Questo però non esclude il fatto che sia possibile avere concorrenza strutturale ed effettiva contemporaneamente, infatti di seguito sono riportati degli esempi che confermano ciò:

![Esempio concorrenza](https://marcobuster.github.io/sweng/assets/14_esempio-concorrenza.png)

![[Concorrenza.png]]

> [!NOTE] Differenza concettuale col conflitto
> Se nel caso della relazione di [[Conflitto]] non si avevano **sufficienti gettoni** per far scattare entrambe le transizioni, invece qui con la concorrenza se ne hanno abbastanza da farle scattare, ma **non è chiaro l'ordine** di scatto (in quanto le transizioni nelle reti P/T non possono scattare in contemporanea).

Ovviamente è anche possibile che non ci sia alcun tipo di concorrenza: è sufficiente che due transizioni abbiano in comune un posto e una delle due non sia abilitata (come T2-T6 e T3-T4 nell'esempio).