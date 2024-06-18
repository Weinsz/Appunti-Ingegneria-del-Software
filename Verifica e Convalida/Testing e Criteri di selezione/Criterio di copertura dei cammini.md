Un test $T$ soddisfa il criterio di copertura dei cammini se e solo se ogni cammino del grafo di controllo del programma viene percorso per almeno un caso di test $t \in T$.

**Metrica**: frazione tra i **cammini percorsi e quelli effettivamente percorribili**.

> [!NOTE] NON è applicabile
> Criterio molto generale ma spesso **impraticabile**, anche per programmi semplici: la presenza di cicli imporrebbe infatti di **testare tutti gli infiniti cammini** che li attraversano un numero arbitrario di volte. Il criterio è quindi in pratica considerato **non applicabile**.

#### Pseudocodice

```c
01  void main() {
02      float a, b, x, y;
03      read(x);
04      read(y);
05      a = x;
06      b = y;
07      while (a != b) {
08          if (a > b)
09              a = a - b;
10          else
11              b = b - a;
12      }
13      write(a);
14  }
```

#### Diagramma di flusso di esecuzione

![Esempio criteri di copertura](https://marcobuster.github.io/sweng/assets/13_criteri-copertura-esempio-4.png)

