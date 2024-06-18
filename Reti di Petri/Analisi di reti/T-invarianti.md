I **$T$-invarianti** sono concettualmente molto simili ai [[P-invarianti]] ma pongono alcuni **vincoli di invariabilità sulle sequenze di scatti *cicliche***, ovvero che **si possono ripetere** ciclicamente e portano alla situazione iniziale (**stato base**).

Partendo dall'equazione $m' = m + Cs$, si pone il vincolo $m' = m$ in quanto la sequenza deve tornare alla **marcatura iniziale**. Le **soluzioni del sistema** sono quindi: $$ Cs = 0 $$
con $C$ costante e $s$ un **vettore di incognite**, rappresentante una sequenza ammissibile.

Se si risolve il sistema e si trova un **vettore $s$ rappresentante una sequenza di scatti ammissibile**, allora tale sequenza è **ciclica**, per cui $s$ **è un $T$-invariante**.

> [!NOTE] Differenza coi P-invarianti
> A differenza dei P-invarianti (per i quali trovarne uno è **condizione sufficiente** purché sia valido: non li trovo tutti, ma quelli che trovo sono sicuro siano tali), per un T-invariante soddisfare l'equazione è **condizione necessaria ma non sufficiente** per la **validità** della sequenza; dunque non è detto siano tutte valide

Se una rete è **[[Limitatezza|limitata]]** e **copribile da T-invarianti**, allora è dimostrabile che la rete è anche **[[Vitalità di una transizione#^638d35|viva]]**.