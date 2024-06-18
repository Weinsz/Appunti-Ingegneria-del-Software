Oltre ad essere un processo utile per il rilevamento di potenziali errori, l'**[[Verifica e Convalida/Analisi statica/Analisi statica|Analisi statica]]** può anche contribuire a **guidare l'attività di testing**.
Per capire come, si nota che a partire dall'analisi statica è possibile fare queste osservazioni:
- affinché si presenti un **malfunzionamento** dovuto ad una **anomalia** in una **definizione**, deve esserci un **uso** che sfrutti il valore assegnato;
- un ciclo dovrebbe essere ripetuto se verrà **usato un valore definito all'iterazione prima**.

L’**analisi statica** può quindi aiutare a **selezionare i casi di test** basandosi sulle **sequenze definizione-uso** delle variabili, costruendo cioè dei **nuovi** [[Criteri di selezione|criteri di copertura]].

### Terminologia

- Dato un nodo $i$ del diagramma di flusso (ossia un *comando/riga del programma*), si chiama $\text{def}(i)$ l'**insieme delle variabili definite in $i$.**
- Data invece una variabile $x$ e un nodo $i$, si chiama $\text{du}(x, i)$ l'insieme dei nodi $j$ tali che:
	- $x\in \text{def}(i)$, cioè la variabile $x$ è **definita** nel nodo/riga $i$;
	- $x$ è **usata** nel nodo/riga $j$;
	- **esiste un cammino da $i$ a $j$ libero da definizioni di $x$**, ovvero che se seguito non sovrascrive il valore di $x$.

> [!NOTE] Quindi cos'è $\text{du}(x, i)$?
> In parole semplici, si tratta cioè dell’**insieme di nodi $j$** **che _potrebbero_ usare il valore di $x$** **definito in riga $i$**.