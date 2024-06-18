Un test $T$ soddisfa il **criterio di $n$-copertura** se e solo se **ogni cammino del grafo** contenente al massimo un **numero di iterazioni** di ogni ciclo non superiore a $n$ viene percorso per almeno un caso di test $t \in T$.

La definizione sopra **non significa che il test deve eseguire $n$ volte un ciclo**, ma che per ogni numero $k$ compreso tra $0$ e $n$ deve esistere un caso di test che esegue tale ciclo $k$ volte. 
Si sta quindi **limitando il numero massimo di percorrenze** dei cicli. Di conseguenza, al crescere di $n$ il **numero di casi di test aumenta** molto rapidamente. Inoltre, fissare $n$ a livello di programma può non essere un’azione così semplice: il numero d’iterazioni che necessita un ciclo per essere testato a fondo può essere **molto differente** da caso a caso.

### Caso con $n = 2$

Per cercare di minimizzare il numero di test spesso il criterio applicato è quello di **$2$-copertura dei cicli**. Si tratta infatti del numero minimo che permette comunque di testare tutte le casistiche principali:
- $k =$ zero iterazioni;
- $k =$ 1 iterazione;
- $k =$ _più di una_ iterazione.

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


Il caso $n=2$ è cioè il **minimo** per considerare casistiche non banali: dando uno sguardo all’esempio sopra, infatti, con $n=1$ il ciclo `while` sarebbe stato indistinguibile da una semplice selezione `if`; testando due iterazioni si incominciano a testare le **vere caratteristiche del ciclo**. Esso permette cioè di testare non solo i comandi che compongono il ciclo, ma anche le sue **pre/post-condizioni** ed eventuali **invarianti**.

A differenza del [[Criterio di copertura dei cammini]], il **criterio di n-copertura** è considerato **applicabile** a programmi reali.