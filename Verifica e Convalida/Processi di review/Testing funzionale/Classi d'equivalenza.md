La tecnica delle **classi d'equivalenza** si pone l'obiettivo di dividere il dominio del programma in **classi di dati**, ovvero gruppi di valori di input che **dovrebbero stimolare il programma nello stesso modo**. Non si tratta quindi di classi d'equivalenza degli output, cioè valori che dati in input al programma forniscono lo stesso risultato, quanto piuttosto di valori che dati in pasto al programma forniscono un risultato diverso ma **prodotto nello stesso modo**.

Una volta individuate le classi di dati l'obiettivo sarebbe quindi di estrarre da esse casi di test in modo da testare il programma in tutti i suoi funzionamenti standard.
In realtà dunque si cercano di individuare casi di test che rivelino eventuali **classi d'equivalenza di errori**, cioè insiemi di valori che generano malfunzionamenti per lo stesso motivo. Classi di equivalenza di questo tipo sono solitamente più **stabili** rispetto alle normali in quanto il risultato ottenuto, vale a dire l'errore, è spesso lo stesso o molto simile.

> [!NOTE] Definizione più formale
> Una **classe di equivalenza** rappresenta un **insieme di stati validi o non validi** per i dati in input e un insieme di stati validi per i dati di output, dove per dato si intendono valori, intervalli o insiemi di valori correlati.

È importante comprendere anche i possibili **stati non validi** in quanto bisogna testare che il programma reagisca bene all’input mal formattato. Ogni dominio avrà quindi almeno due classi di equivalenza:
1. la classe degli **input validi**
2. la classe degli **input non validi**

Per fare un esempio si può considerare un programma che chiede in input un **codice PIN di 4 cifre**. Il suo dominio può quindi essere suddiviso in due semplici classi di equivalenza:
1. PIN corretto;
2. tutti i numeri di 4 cifre diversi dal PIN.

Volendo fare un altro esempio, se ci si aspetta che i valori in input ricadano in un intervallo, per esempio $[100,700]$, si può definire:
- la classe d'equivalenza *valida* $x \in [100,700]$,
- e la classe d'equivalenza *non valida* $x \notin [100,700]$.
Per voler aumentare la **granularità** si può però spezzare la classe degli input non validi in due, ottenendo una classe valida e due non valide:
1. $x \in[100,700]$;
2. $x<100$;
3. $x>700$.

Come si vede, la **scelta** delle classi di equivalenza da considerare **non è univoca** e richiede un minimo di conoscenza di dominio. 
Alternativamente esistono delle tecniche standard di individuazione delle classi di equivalenza a partire dalle **specifiche** che prendono il nome di [[Category partition]].