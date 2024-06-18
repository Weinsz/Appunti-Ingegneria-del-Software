Nel [[Criterio di copertura degli usi]] si è richiesto di testare **un cammino** da ogni definizione ad ogni suo uso, ma come noto i cammini tra due istruzioni di un programma possono essere **molteplici**. Potrebbe dunque sorgere l’idea di **testarli tutti**: da questa intuizione nasce il **criterio di copertura dei cammini DU**.

$$
\begin{align*}
T \in C_{\text{pathDU}} \Longleftrightarrow&
\forall{i}\in P,\space\forall{x}\in\text{def}(i),\ \forall{j}\in\text{du}(i,x),\\\
& \forall\space\text{cammino da i a j senza ulteriori definizioni di x} \\\
&\exists{t}\in T \text{ che lo esegue}
\end{align*}
$$

> [!NOTE] Impraticabile
> Questo criterio può essere **utile da ipotizzare**, ma a causa dell’esplosione combinatoria del numero dei cammini è considerato **impraticabile**.



