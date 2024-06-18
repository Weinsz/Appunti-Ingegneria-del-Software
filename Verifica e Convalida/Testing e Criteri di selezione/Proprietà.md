## Criterio di selezione

Il ragionamento che si fa (o le regole che si danno) nel selezionare un sottoinsieme di $D$, sperando che approssimi il test ideale.

### Affidabilità

Un criterio di selezione $C$ si dice **affidabile** se presi due test $T_1$ e $T_2$ in base al criterio allora o **entrambi hanno successo o nessuno dei due** (cioè o entrambi rilevano uno o più malfunzionamenti per il programma $P$ o nessuno dei due).
$$
\boxed{\text{affidabile}(C, P) \Longleftrightarrow (\forall T_1 \in C, \forall T_2 \in C \text{ }\text{ }\text{successo}(T_1, P) \Leftrightarrow \text{successo}(T_2, P))}
$$


### Validità

Un criterio di selezione $C$ si dice **valido** se, qualora $P$ non sia corretto, allora esiste almeno un test $T$ selezionato in base al criterio $C$ che ha **successo** (cioè rileva uno o più malfunzionamenti per il programma $P$).
$$
\boxed{\text{valido}(C, P) \Longleftrightarrow (\lnot \text{ok}(P, D) \Rightarrow \exists T \in C \text{ }\text{ }\text{successo}(T, P))}
$$


### Esempio

```java
static int raddoppia(int par) {
    int risultato;
    risultato = (par * par);
    return risultato;
}
```

Un criterio che seleziona:
- "i sottoinsiemi di $0, 2$" è **affidabile** perché il programma funziona sia con $0$ sia con $2$, ma **non è valido**, in quanto so che il programma non è corretto e **non esiste un test** che trovi malfunzionamenti;
- "i sottoinsiemi di $0, 1, 2, 3, 4$" **non è affidabile** perché i risultati dei casi di test non sono tutti coerenti (es. il test $T_1 = 0,1$ non ha **successo**, mentre $T_2 = 0, 3$ sì), ma è **valido** in quanto esiste almeno un test che rileva i malfunzionamenti;
- "i sottoinsiemi finiti di $D$ con almeno un valore maggiore di $18$" è **affidabile**, poiché i risultati dei casi di test sono tutti coerenti, ed è anche **valido** perché rileva i malfunzionamenti.

In questo caso la ricerca di un **criterio valido e affidabile** era semplice perché conoscevamo già l’anomalia. Però non si può dire lo stesso di un qualunque programma $P$ in quanto **non si conoscono i malfunzionamenti a priori** e dunque è molto più difficile trovare criteri validi e affidabili.

### Criterio valido e affidabile

L’obiettivo sarebbe quindi quello di **trovare un criterio valido e affidabile sempre**. Tuttavia ciò è purtroppo impossibile in quanto un criterio di questo tipo **selezionerebbe test ideali**, che sappiamo non esistere.

Si immagini infatti di avere un **criterio valido e affidabile** e che un test selezionato da esso **non abbia successo**. Sapendo che:
- non avendo **successo** allora non sono stati trovati malfunzionamenti;
- essendo il criterio **affidabile** allora allora tutti gli altri test selezionati da quel criterio non troveranno malfunzionamenti;
- essendo il criterio **valido** allora se ci fosse stato un malfunzionamento almeno uno dei test lo avrebbe trovato ($\lnot True \Rightarrow False$, dunque $\text{valido}(C, P) \Leftrightarrow True$)
allora il programma è **corretto**, ovvero si è trovato un test che quando non ha successo implica la correttezza del programma: in poche parole, un **test ideale**. Esiste quindi un altro modo per implicare la [[Verifica e Convalida/Testing e Criteri di selezione/Definizioni#^16c407|correttezza]] di un programma:
$$
\boxed{\text{affidabile}(C, P) \land \text{valido}(C, P) \land(T \in C) \land \lnot \text{ }\text{successo}(T, P) \Longrightarrow \text{ok}(P, D))}
$$

In conclusione, trovare un criterio che sia **contemporaneamente** affidabile e valido significherebbe trovare un criterio che selezioni **test ideali**, che sappiamo non esistere per [[Verifica e Convalida/Testing e Criteri di selezione/Definizioni#^de3ff2|la tesi di Dijkstra]]. 

**Dovremo dunque accontentarci di criteri che garantiscano solo una delle due caratteristiche.**