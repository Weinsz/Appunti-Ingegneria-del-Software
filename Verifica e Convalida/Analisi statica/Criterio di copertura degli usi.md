Un test $T$ soddisfa il **criterio di copertura degli usi** se e solo se per ogni nodo $i$ e ogni variabile $x \in \text{def}(i)$, $T$ include un caso di test che esegue un cammino libero da definizioni da $i$ **ad ogni elemento di $\text{du}(i,x)$.**

Sembra simile al [[Criterio di copertura delle definizioni]], con la differenza che ora bisogna coprire **tutti** i potenziali usi di una variabile definita. Questo appare ancora più chiaro osservando la formula matematica:
$$
\begin{align*}
T \in C_{\text{usi}} \Longleftrightarrow&
\forall{i}\in P,\space\forall{x}\in\text{def}(i),\ \forall{j}\in\text{du}(i,x),\\\
&\exists{t}\in T \text{ che esegue un cammino da i a j senza ulteriori definizioni di x}
\end{align*}
$$

Si noti però che il criterio di copertura degli usi **non implica il criterio di copertura delle definizioni**, perché nel caso in cui non esistano $j\in\text{du}(i,x)$ l'uso del $\forall$ è più permissivo del $\exists$ dell'altro criterio: quest'ultimo richiedeva infatti che per ogni definizione esistesse **almeno un uso**, mentre il criterio di copertura degli usi non pone tale clausola, dato che **se non ci sono usi il $\forall$ è sempre vero**. Viene quindi da sé che questo criterio non copre neanche il [[Criterio di copertura dei comandi]].

Si riconsideri nuovamente il programma in $C$ visto in precedenza come esempio:
```c
01  void main() {
02      float a, b, x, y;
03      read(x);
04      read(y);
05      a = x;
06      b = y;
07      while (a != b)
08          if (a > b)
09              a = a - b;
10          else
11              b = b - a;
12      write(a);
13  }
```

Come prima, si considera la variabile $a$ e i relativi insiemi dei nodi degli usi $\text{du}(i,a)$ per ogni sua definizione:
1. $\text{du}(5,a)= 7,8,9,11,12$;
- $\text{du}(9,a) = 7,8,9,11,12$.

Per ogni definizione occorre coprire **tutti gli usi**:

| $\text{du}(5,a)$                                                                                                                   | $\text{du}(9,a)$                                                                                      |
| ---------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| $\boxed{d_5}\space\color{#7CFC00}\boxed{u_7}\space\boxed{u_8}\space\boxed{u_{11}}$$\boxed{u_7}\space\color{#7CFC00}\boxed{u_{12}}$ | $...\boxed{d_9}\color{#7CFC00}\space\boxed{u_7}\space\boxed{u_8}\space\boxed{u_9}\color{white}...$    |
| $...\boxed{d_5}\space\boxed{u_7}\space\boxed{u_8}\space\color{#7CFC00}\boxed{u_9}\color{white}...$                                 | $...\boxed{d_9}\space\boxed{u_7}\space\boxed{u_8}\space\color{#7CFC00}\boxed{u_{11}}\color{white}...$ |
|                                                                                                                                    | $...\boxed{d_9}\space\boxed{u_7}...\space\color{#7CFC00}\boxed{u_{12}}\color{white}...$               |

Un test che soddisfa totalmente il criterio può essere il seguente: $$T=⟨4,8⟩,⟨12,8⟩,⟨12,4⟩$$
Questo esempio permette di notare qualcosa sulla natura dei cicli: dovendo testare ogni percorso al loro interno **è necessario fare almeno due iterazioni**.

Può quindi sorgere un dubbio: **è meglio che le due iterazioni siano fatte nello stesso caso di test o in casi di test separati?** Ovvero, è meglio **minimizzare** i **casi di test** o le **iterazioni per caso**?

Opinione diffusa è quella secondo cui è preferibile **minimizzare le iterazioni per caso**: partizionando le casistiche in diversi casi di test è possibile rilevare con più precisione gli errori, riducendo il **tempo di debug**.
In alcune situazioni però aumentare il numero di iterazioni può diminuire il tempo di esecuzione totale dei test, in quanto dovendo riavviare il programma per ciascun caso di test la **somma dei tempi di startup** può diventare significativa per software molto massicci.