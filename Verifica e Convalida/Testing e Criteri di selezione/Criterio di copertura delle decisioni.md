Un test $T$ soddisfa il **criterio di copertura delle decisioni** se e solo se ogni **decisione** (effettiva) viene resa sia vera che falsa in corrispondenza di almeno un caso di test $t \in T$.

**Metrica:** frazione delle **decisioni che sono state rese sia vere che false su quelle per cui è possibile farlo**.


> [!NOTE] Implica la copertura dei comandi
> Dovendo attraversare ogni possibile flusso di controllo, 
> **il criterio di copertura delle decisioni $\Rightarrow$ il criterio di copertura dei comandi.**

 Dunque se un test soddisfa la copertura delle decisioni, allora soddisfa anche la copertura dei comandi (ma **non è garantito l’inverso**).

Estraendo il codice in un diagramma di flusso infatti è possibile coprire tutte le decisioni **se e solo se** ogni arco, e quindi ogni nodo, viene attraversato.

#### Pseudocodice

```c
01  void main(){
02      float x, y;
03      read(x);
04      read(y);
05      if (x != 0 && y > 0)
06          x = x + 10;
07      else
08          y = y / x
09      write(x);
10      write(y);
11  }
```

#### Diagramma di flusso di esecuzione

![Esempio criterio decisioni](https://marcobuster.github.io/sweng/assets/13_criteri-copertura-esempio-2.png)

Dall’esempio nel codice, un test che soddisfi il suddetto criterio potrebbe includere $⟨3,7⟩,⟨3,−2⟩$. 
Nonostante sia un criterio *migliore* del precedente, la copertura delle decisioni **non garantisce la correttezza** del programma. Nell'esempio il caso $⟨0,5⟩$ eseguirebbe comunque una **divisione per zero**.