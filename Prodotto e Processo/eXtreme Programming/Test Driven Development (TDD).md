Tecnica di progettazione del sw che mira a far emergere **dal basso** il design più semplice in grado di risolvere un dato problema. Non si tratta né di un'attività di verifica né di scrittura del codice, quanto piuttosto di un approccio alla scrittura dei test.

Il TDD si fonda su due concetti fondamentali:
> TDD = **test-first + baby steps**

Il significato di quest'espressione è che per scrivere codice che esalti la semplicità della soluzione è necessario **scrivere prima il test rispetto al codice** (*test-first*) e procedere a piccoli passi (*baby
steps*), realizzando cioè piccole parti di codice, testandole e solo allora andando avanti.
Questa tecnica ha come obiettivo stabilire un **ciclo di feedback istantaneo**: così facendo è meno probabile perdere tempo su una soluzione sbagliata, e pure in caso di errore è più facile individuare cosa lo genera e come risolverlo.

Per applicare quest'approccio test-driven allo sviluppo sw, il TDD ha sviluppato questo mantra: **rosso, verde, refactoring**. Quando si scrive codice bisogna seguire le seguenti 3 fasi:
1. Ogni volta che si deve aggiungere una feature **si scrive prima il test** che la provi; non essendo ancora stata sviluppata, tale test dovrà fallire (<span style="Color: red">rosso</span>). In questa fase si crea già una parte di specifica, perché descrive l'utilità della nuova feature o della parte di codice che si sta creando.
   L'eccessivo tempo impiegato in questa fase sta a significare che il problema è troppo complesso, ed è quindi necessario suddividerlo. Cerco quindi di mettermi nei panni del cliente, per capire esattamente come voglia che il sw funzioni e come debba rispondere a certi input.
2. Si cerca poi di **soddisfare il test il prima possibile**, facendolo diventare <span style="Color: green">verde</span>. Si ottiene così del codice corretto ma non bello, come una prima bozza: serve però come feedback del fatto che l'algoritmo scelto funziona. Nonostante la rapidità nello sviluppo di questa soluzione, si deve comunque tenere conto, almeno minimamente, delle proprie scelte implementative, in quanto fungeranno da base per il prossimo step.
3. Infine si fa un'azione di **refactoring** (fattorizzazione), ovvero riorganizzando e riscrivendo il codice per migliorarlo, assicurandosi però che il test funzioni sempre (cioè resti <span style="Color: green">verde</span>).

Questo ciclo va ripetuto ogni 2-10 minuti: ciò obbliga a concentrarsi su task semplici evitando di perdersi in costruzioni sw complicate che magari nemmeno funzionano. Si preferisce fare prima qualche piccolo progresso (*increment*) e poi (*then*) semplificare per migliorare il codice (*simplify*).

L'uso del TDD come tecnica di progettazione garantisce due importanti vantaggi:
1. Spesso capita di scrivere codice difficilmente testabile, ma scrivendo prima il test e poi il codice, aiuta a progettare prodotti la cui correttezza può essere dimostrata.
2. Scrivere prima i test inoltre aiuta a definire chiaramente le interfacce del programma e come queste comunicano tra loro; diversamente, potremmo avere dipendenze complicate da rimuovere.