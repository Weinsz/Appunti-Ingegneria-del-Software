Un test $T$ soddisfa il **criterio di copertura delle decisioni e condizioni** se solo se **ogni decisione** vale sia vera che falsa e **ogni condizione** compresa nelle decisioni del programma vale sia vero che falso **per diversi casi di test $t \in T$.**

Intuitivamente, è l'**intersezione del [[Criterio di copertura delle decisioni]] con il [[Criterio di copertura delle condizioni]]**, perciò il soddisfacimento di questo criterio **implica** sia quello di copertura delle condizioni che quello delle decisioni (che a sua volta **implica quello dei comandi**).

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

Nell'esempio, il test $⟨0,−5⟩,⟨5,5⟩$ soddisfa il **criterio di copertura delle decisioni e condizioni**.

| x       | y        | decisione |
| ------- | -------- | --------- |
| $0$ (F) | $-5$ (F) | F         |
| $5$ (T) | $5$ (T)  | T         |

Rileva l’anomalia alla riga 8 ma non quella a riga 6. **Non garantisce** quindi neanche in questo caso la **correttezza** del programma.