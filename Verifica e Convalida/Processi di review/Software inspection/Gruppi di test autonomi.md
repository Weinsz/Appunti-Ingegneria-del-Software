Una convinzione comune è che colui che ha sviluppato un pezzo di codice sia la persona meno adatta a testarlo, come afferma la **Legge di Weinberg (L23)**:
> Uno sviluppatore non è adatto a testare il suo codice.

Di conseguenza, spesso si preferisce che il testing sia affidato a un **gruppo di tester autonomi**. Questo implica infatti una serie di **vantaggi**, sia **tecnici** che **psicologici**:
#### Vantaggi tecnici
- **maggiore specializzazione**: si evita così di richiedere che i propri dev siano anche **esperti di testing**;
- **maggiore conoscenza delle tecniche di [[Verifica e convalida]]** e dei relativi tool: chi fa di lavoro il **tester** acquisisce competenze specifiche sui tool di testing, spesso complessi, oltre che sui concetti di [[Criteri di selezione|copertura]] e [[Analisi mutazionale|mutazioni]].

#### Vantaggi psicologici:
- **distacco dal codice**: a causa dell'assenza di modelli mentali precedenti su come il sw dovrebbe operare, un tester esterno meno *biased* pone maggiore attenzione sugli aspetti spesso tralasciati; 
- **indipendenza nella valutazione**: una persona che testa il **proprio** codice è **incentivata a non trovare** molti errori in quanto potrebbe suggerire un lavoro di dubbia qualità in fase di sviluppo. Un **gruppo specializzato** nel testing è invece incentivato a trovarne il più possibile per giustificare il loro impiego.

### Svantaggi

Ci sono tuttavia anche una serie di **svantaggi** legati all’avere un gruppo di tester autonomo.
Innanzitutto, i problemi più ovvi sono legati all'**aspetto tecnico**: il fatto che i tester diventino specializzati nel testing implica che **perderanno** col tempo la **capacità di progettare e codificare**, oltre a possedere una **minore conoscenza dei requisiti** del progetto.

Nell’analisi di Elisabeth Hendrickson denominata “[**Better testing — worse quality?**](https://web.archive.org/web/20220526084408/http:/testobsessed.com/wp-content/uploads/2011/04/btwq.pdf)” viene analizzata poi la tecnica sotto un **punto di vista psicologico**: 
#### Com'è possibile che un maggior investimento nel team di testing porti a un calo delle prestazioni in termini di numero di errori nel codice?

La risposta parrebbe dipendere dal concetto di **responsabilità**: pur essendo vero che l'attività di testing è compito dei tester, è vero anche che è lo sviluppatore stesso che ha il compito di fare **test d'unità** del proprio codice; il team di testing dovrebbe occuparsi solo del **[[Testing funzionale]] o d'integrazione**. Spesso però, a fronte di un aumento del personale nel team di testing e specialmente con una **deadline vicina**, il team di sviluppo tende a **dare la responsabilità** di trovare gli errori ai tester, **abbassando la qualità del codice**.

Il team di testing troverà sì gli errori, riconsegnando il codice agli sviluppatori per correggerli, ma questo passaggio ulteriore implica una **notevole perdita di tempo e risorse**.
Inoltre, la presenza di un team di testing dedicato può generare **pressioni negative** sul team di sviluppo: ogni sviluppatore potrebbe sentirsi sotto costante valutazione da parte del team di testing.


### Possibili alternative

Una possibile soluzione alle criticità appena evidenziate consisterebbe nella **rotazione del personale** e delle mansioni: una stessa persona potrebbe ricoprire il ruolo di sviluppatore per un progetto e di tester per un altro. Questo approccio mostra diversi vantaggi, tra cui:
- **evitare le pressioni negative**: ricoprendo diversi ruoli in diversi progetti, il personale non si dovrebbe sentire giudicato o giudicante;
- **evitare il progressivo depauperamento tecnico** dovuto all'eccessiva specializzazione in una sola direzione;
- **evitare lo svuotamento dei ruoli**.

C’è però da considerare: 
- un certo **aumento dei costi di formazione** per via del **raddoppio delle responsabilità** individuali
- un parallelo **aumento della difficoltà di pianificazione**: potrebbe succedere che la stessa persona debba lavorare a più progetti **contemporaneamente**, dovendo quindi dividere il proprio tempo e le proprie competenze.

Un’altra possibile **alternativa** consiste nella **condivisione del personale**, che prevede che all'interno del team siano gli stessi sviluppatori a occuparsi del **testing**, ricoprendo diversi ruoli: ciò permette di **sopperire** al problema di **scarsa conoscenza del software** in esame e del relativo **dominio applicativo** ma, oltre a far riemergere le **criticità** individuate precedentemente, aumenta le **difficoltà nella gestione dei ruoli**.