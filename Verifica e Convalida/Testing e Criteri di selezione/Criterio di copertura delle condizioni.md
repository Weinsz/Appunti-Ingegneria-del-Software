Un test $T$ soddisfa il **criterio di copertura delle condizioni** se e solo se ogni **singola condizione** (effettiva) viene resa sia vera che falsa in corrispondenza di almeno un caso di test $t \in T$.

**Metrica**: similmente ai precedenti, è la **percentuale delle condizioni che sono state rese sia vere che false su quelle per cui è possibile farlo**.

Per quanto simile, si tratta di un criterio diverso dal [[Criterio di copertura delle decisioni]]: in caso di **condizioni composte** (es. `x != 0 && y < 3`), la **copertura delle decisioni** imporrebbe che l'**intera condizione** sia resa sia vera che falsa, mentre la **copertura delle condizioni** richiede di rendere vere e false le **singole condizioni atomiche** in almeno un caso di test.

> [!NOTE] NON implica i criteri precedenti
> Ciò **non impone** quindi di seguire tutti i percorsi sul diagramma di flusso e fa sì che questo criterio **non implica** il soddisfacimento di nessuno dei precedenti.

#### Pseudocodice

```c
01  void main(){
02      float x, y;
03      read(x);
04      read(y);
05      if (x != 0 || y > 0)
06          y = y / x;
07      else
08          y = (y + 2) / x
09      y = y / x;
10      write(x);
11      write(y);
12  }
```

#### Diagramma di flusso di esecuzione

![Esempio criterio decisioni](https://marcobuster.github.io/sweng/assets/13_criteri-copertura-esempio-3.png)

Nell'esempio del codice, il test $⟨0,5⟩,⟨5,−5⟩$ soddisfa al 100% il **criterio di copertura delle condizioni**, in quanto `x != 0` è falsificato da $⟨0,5⟩$, mentre  `y > 0` è verificato da $⟨0,5⟩$ e falsificato $⟨5,-5⟩$. Tuttavia, **la decisione è sempre vera**.

| x       | y        | decisione |
| ------- | -------- | --------- |
| $0$ (F) | $5$ (T)  | T         |
| $5$ (T) | $-5$ (F) | T         |

Sono infatti presenti anomalie alla riga 6 (possibile divisione per zero) e alla riga 8 (overflow e divisione per zero), ma i comandi contenuti in quest'ultima non sono coperti. Ora più che mai quindi, la **copertura delle condizioni non garantisce la correttezza del programma**.