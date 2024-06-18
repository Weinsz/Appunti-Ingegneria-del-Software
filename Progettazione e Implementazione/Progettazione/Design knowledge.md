Si tratta della **conoscenza del design architetturale di un progetto**. Si può utilizzare:

0. la **memoria**: non è affidabile perché nel tempo si erode, specialmente in coppia;
1. i **documenti di design** (linguaggio naturale o diagrammi): se non viene aggiornato di pari passo col codice, che è un operazione fastidiosa e onerosa, resta disallineato, risultando più dannoso che altro;
2. le **piattaforme di discussione** (*version control, issue management*): possono aiutare ma le informazioni sono sparse in luoghi diversi e quindi difficili da reperire, poi rimane il problema di mantenere aggiornate queste informazioni;
3. gli **[[UML]]**: tramite diagrammi UML si è cercato di sfruttare l’approccio _**generative programming**_, ovvero la generazione automatica del codice a partire da specificazioni di diagrammi, ma con l’esperienza si è visto che non funziona;
4. il **codice** stesso: tramite la lettura del codice è possibile capire il design ma è difficile rappresentare le ragioni delle scelte effettuate.

Dunque è bene sfruttare tutte le tecniche sopra proposte **combinandole**, partendo dal codice; inoltre è importante scrivere della **documentazione** per spiegare le ragioni dietro le scelte effettuate e non le scelte in sé, che **si possono dedurre dal codice**.

### Condivisione

Per condividere tali scelte di design (il know how) si può sfruttare:

0. **metodi**: pratiche come **[[Metodologie Agile|Agile]]** o l'**[[Conoscenze preliminari#^6e76cf|Object Orientation]]** stessa, che può essere un metodo astratto per condividere scelte di design;
1. **[[Design Pattern|design pattern]]**: fondamentali per la condivisione e sono utili anche per generare un **vocabolario comune** (sfruttando termini noti a tutti per descrivere i ruoli dei componenti) e **aiutano l'implementazione**, in quanto i pattern hanno metodologie note per essere implementati. I pattern non si concentrano sulle prestazioni di un particolare sistema ma sulla **generalità** e la **riusabilità** di **soluzioni a problemi comuni**;
2. **principi**: per esempio i [[Conoscenze preliminari#^d4ff78|principi SOLID]].