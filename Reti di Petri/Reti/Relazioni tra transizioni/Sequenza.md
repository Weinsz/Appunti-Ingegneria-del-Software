Una transizione $t_1$ è **in sequenza** con una transizione $t_2$ in una marcatura $M$ se e solo se:
$$
M\space[\space t_1 > \land \space \lnot M\space[\space t_2 > \land \space M\space[\space t_1 t_2 > 
$$

Questa formula indica che:
- $t_1$ è **abilitata** in $M$
- $t_2$  **non è abilitata** in $M$
- $t_2$ è abilitata nella marcatura $M'$ prodotta dallo scatto $M\space[\space t_1 > M'$

Si può notare una **relazione d’ordine non simmetrica** in cui _lo scatto di $t_1$_ è una **condizione sufficiente** per cui $t_2$ possa scattare: questo tipo di relazione permette quindi di creare un **ordine di scatto** delle transizioni. 
È condizione **sufficiente e non necessaria** perché osservando l’esempio sottostante è facile capire che lo scatto di t0 non è necessario per far si che t2 scatti: infatti anche se dovesse avvenire lo scatto di t1, la transizione t2 diventerebbe comunque abilitata.

![Sequenza](https://marcobuster.github.io/sweng/assets/14_sequenza.png)

Esempio di relazioni in sequenza:
![[Esempio relazione sequenza.png]]