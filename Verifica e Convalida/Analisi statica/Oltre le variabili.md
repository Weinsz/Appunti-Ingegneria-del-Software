L’[[Analisi Data Flow]] si può estendere anche su altri _“oggetti”_, non solo variabili.  
Per esempio, è possibile prevedere le seguenti operazioni su un **file**:

- $\boxed{a}$  (**apertura**): specializzata in per lettura o per scrittura;
- $\boxed{c}$ (**chiusura**);
- $\boxed{l}$ (**lettura**);
- $\boxed{s}$ (**scrittura**).

Date queste operazioni si possono individuare una serie di regole, come per esempio:
1. $\boxed{l}$, $\boxed{s}$ e $\boxed{c}$  devono essere precedute da $\boxed{a}$  senza $\boxed{c}$ intermedie;
2. $\boxed{a}$ deve essere seguita da $\boxed{c}$ prima di un’altra $\boxed{a}$;
3. legami tra tipo di apertura (per lettura o per scrittura) e relative operazioni.

È interessante notare il **legame** tra l’attività di **analisi del flusso di dati** e i diagrammi [[UML]] a [[State diagram|stati finiti]]: un _oggetto_ risponde a una certa _tipologia di eventi_, può essere in diversi _stati_ e in certi _stati_ non sono ammesse alcune _operazioni_. Si noti come nessuna delle due discipline entra comunque nel merito del **valore delle variabili**, relegato ad un’analisi a **runtime**.

### Criterio di copertura del budget

Di frequente nei **contesti reali** l’unico criterio applicato è quello di **copertura del budget**: 
si continuano a creare casi di test finché non sono finite le **risorse** (tempo e soldi). 

Questa tecnica ovviamente **non fornisce alcuna garanzia sull’efficacia dei test**, ed è sicuramente **sconsigliata**.