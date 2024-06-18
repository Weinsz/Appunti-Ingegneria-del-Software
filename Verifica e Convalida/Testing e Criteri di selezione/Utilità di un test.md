Abbandonata la vana speranza di un criterio di selezione universalmente valido che permetta di testare alla perfezione qualunque programma, si va a vedere cosa significa **usare un criterio di selezione per costruire un test**. Come noto, un test è un insieme di casi di test, cioè specifici input appartenenti al dominio del programma: 
> Un criterio di selezione governa dunque **quanti e quali casi di test vengono aggiunti** al test che si sta costruendo.

**Quali sono le caratteristiche che rendono utile un caso di test, ovvero che rendono “possibile” o “probabile” che il caso di test evidenzi un malfunzionamento causato da un’anomalia?** 

Un **caso di test utile** deve:
- **eseguire il comando contenente l'anomalia**, non è altrimenti possibile che si manifesti il malfunzionamento;
- l’esecuzione di tale comando deve portare il sistema in uno **stato scorretto/inconsistente**;
- lo stato inconsistente **deve propagarsi fino all’uscita** del codice in esame in modo da **produrre un output diverso da quello atteso**.

Un buon criterio di selezione dovrà quindi selezionare test contenenti casi di test utili, ma quanti dovrebbe contenerne? Per capirlo, a ogni criterio è infatti possibile associare una metrica legata alle caratteristiche del codice, nello specifico, che misuri la **copertura del test** che si sta costruendo, e che ci permetta di decidere *quando smettere di aggiungere casi di test, quali casi è opportuno aggiungere e di confrontare la bontà di test diversi*. 
Si aggiungeranno infatti solo casi di test che permettano di **aumentare la metrica di copertura**, la quale più aumenta meglio è.