**Non volendo testare tutte le combinazioni di condizioni**, ci si rende presto conto che certe combinazioni sono **più rilevanti** di altre: se modificando una sola condizione atomica si riesce a **modificare l’esito della decisione**, allora è **molto significativa**, indipendentemente dalla sua dimensione. Il criterio così ottenuto prende il nome di **criterio di copertura delle decisioni e condizioni modificate**.

Per ogni condizione base devono quindi esistere due casi di test che modificano il valore di una sola condizione base e che portino a un diverso esito della decisione: così inoltre il criterio **implica** quello [[Criterio di copertura delle decisioni e condizioni|delle decisioni e condizioni]].

Si può dimostrare che se si hanno $N$ condizioni base **sono sufficienti $N+1$ casi di test** per soddisfare il criterio, decisamente meno di quelli richiesti dal [[Criterio di copertura delle condizioni composte]].

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

| x       | y        | decisione |
| ------- | -------- | --------- |
| $0$ (F) | $-5$ (F) | F         |
| $0$ (F) | $5$ (T)  | T         |
| $5$ (T) | $-5$ (F) | T         |

Tolto caso **vero - vero** perché con un singolo cambio di condizione
non era possibile cambiare decisione