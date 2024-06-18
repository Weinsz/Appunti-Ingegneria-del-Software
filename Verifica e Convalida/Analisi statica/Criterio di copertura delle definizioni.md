Un test $T$ soddisfa il **criterio di copertura delle definizioni** se e solo se per ogni nodo $i$ e ogni variabile $x \in \text{def}(i)$, $T$ include un caso di test che esegue un cammino libero da definizioni da $i$ ad **almeno uno degli elementi di $\text{du}(i,x)$**.

Ci si vuole dunque assicurare di testare tutte le definizioni, assicurandosi che funzionino **osservando almeno un uso** del valore da loro assegnato.
Matematicamente si può dire che:
$$
\begin{align*}
T \in C_{\text{def}} \Longleftrightarrow&
\forall{i}\in P,\space\forall{x}\in\text{def}(i),\space\exists{j}\in\text{du}(i,x),\\\
&\exists{t}\in T \text{ che esegue un cammino da i a j senza ulteriori definizioni di x}
\end{align*}
$$

Si considera l’esempio già visto in precedenza, considerando la variabile $a$:
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

Partiamo definendo gli insiemi dei nodi degli usi $\text{du}(i,a)$:
1. $\text{du}(5,a)= 7,8,9,11,12$;
- $\text{du}(9,a) = 7,8,9,11,12$.

Si tratta solo di **un caso** il fatto che in questo esempio tali insiemi siano uguali.
In ogni caso, **l’obiettivo è _per ognuna delle due definizioni_ ottenere un uso di tale definizione**:
1. Per la prima definizione la soluzione è banale, a riga 7 la variabile $a$ viene letta sempre: $\boxed{d_5}\space\boxed{u_7}$
2. Per la seconda invece è necessario scegliere un valore tale per cui il flusso di esecuzione entri almeno una volta nel ciclo ed esegua almeno una volta la riga 9:  $\boxed{d_9}\space\boxed{u_7}$.

Un test che soddisfa totalmente il criterio può essere il seguente:
$$T=⟨8,4⟩$$

Come si vede, il **criterio di copertura delle definizioni** non copre tutti i comandi e di conseguenza **non implica il criterio di copertura dei comandi**.