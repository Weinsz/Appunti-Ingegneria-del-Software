Per ora nella sezione di [[Verifica e convalida]] i programmi sono stati trattati come funzioni matematiche da un dominio di input a un altro di output. Questo è tutto sommato vero per ciò che riguarda i **linguaggi procedurali**: un programma in questo paradigma è composto da un insieme di funzioni e procedure che, preso un dato in ingresso, ne restituiscono uno in uscita. A meno di eventuali variabili globali condivise (*sconsigliatissime*), tali funzioni sono indipendenti l'una dall'altra e possono essere quindi **testate indipendentemente** come dei piccoli sottoprogrammi.

La situazione cambia invece per i **linguaggi object-oriented** (**OO**), che introducono i concetti di **classe** e **istanza**: in questi linguaggi gli oggetti sono l'**unione di stato e metodi**. Le tecniche di testing viste smettono di funzionare: la maggior parte delle volte testare i metodi isolatamente come funzioni da input ad output **perde di senso**, in quanto non si considera il contesto in cui essi operano, vale a dire lo **stato dell'oggetto** associato.

Bisogna dunque sviluppare una serie di **tecniche di test** specifiche per i **linguaggi OO**, in cui l’**unità testabile si sposti dalle procedure alle classi**.


### Ereditarietà e collegamento dinamico

Prima di capire **come** è possibile testare un'intera classe, si affrontano due punti critici che derivano dal funzionamento dei linguaggi a oggetti: l'**ereditarietà** e il **collegamento dinamico**.

#### Ereditarietà

Si immagina di avere una classe già completamente testata. Creando ora una sottoclasse di tale classe originale può sorgere un dubbio: *visto che  i metodi ereditati sono già stati testati nella classe genitore, ha senso testarli nella classe figlia?* 
Un simile quesito sorge nel caso di metodi di default appartenenti a un'interfaccia: *ha senso testare i metodi di default direttamente nell'interfaccia o è meglio testarli nelle classi concrete che implementano tale interfaccia?*
L'opinione diffusa è quella di **testare nuovamente tutti i metodi ereditati**: nelle sottoclassi e nelle classi che implementano delle interfacce con metodi di default, tali metodi opereranno infatti in **nuovi contesti**, per cui non vi è alcuna certezza che funzionino ancora a dovere. Inoltre, a causa del **collegamento dinamico**, non è nemmeno sicuro che eseguire lo stesso metodo nella classe base significa eseguire le stesse istruzioni nella classe ereditata.

In generale quindi **non si eredita l'attività di testing**, ma si possono invece ereditare i casi di test e relativi valori attesi (l'*oracolo*), ed è per questo opportuno **rieseguire i casi di test anche nelle sottoclassi**.

#### Collegamento dinamico

Un altro motivo per cui il testing object-oriented differisce fortemente da quello per linguaggi con paradigma imperativo è la preponderanza del **collegamento dinamico**, attraverso il quale le chiamate ai metodi vengono collegate a *runtime* in base al tipo effettivo degli oggetti. A livello teorico infatti tale meccanismo rende difficile stabilire *staticamente* tutti i possibili **cammini di esecuzione**, complicando la determinazione dei criteri di copertura.


### Testare una classe

Per **testare una classe**:
- la **si isola** usando più *classi stub* possibili per renderla eseguibile indipendentemente dal contesto;
- si implementano eventuali **metodi astratti** o non ancora implementati (*stub*);
- si aggiunge una funzione per permettere di estrarre ed esaminare lo stato dell'oggetto per **bypassare l'incapsulamento**;
- si costruisce una classe driver che permetta d'istanziare oggetti e chiamare i metodi secondo il **criterio di copertura** scelto;

Dall'ultimo punto si coglie che quindi sono stati creati dei criteri di copertura ad hoc per il **testing delle classi**, e si vedono sotto quali.

#### Copertura della classe

^ee4313

I **[[Implicazioni e relazioni tra criteri di copertura|criteri classici]]** già visti continuano a valere **ma non sono sufficienti**. Per testare completamente una classe occorre considerare lo **stato dell'oggetto**: in particolare, è comodo usare una [[State diagram|macchina a stati finiti]] che rappresenta gli *stati possibili* della classe e le relative *transizioni*, cioè le chiamate di metodi che cambiano lo stato.

Tale rappresentazione potrebbe esistere nella *documentazione* o essere creata specificatamente per l’attività di testing. Il seguente diagramma rappresenta per esempio una macchina a stati di una classe avente due metodi, $m1$ e $m2$:

![Grafo criteri di copertura](https://marcobuster.github.io/sweng/assets/13_criteri-copertura-grafo.png)

Ottenuta una rappresentazione di questo tipo, alcuni criteri di copertura che si possono considerare sono:
- **coprire tutti i nodi**: per ogni **stato** dell'oggetto deve cioè esistere almeno un caso di test che lo raggiunge;
- **coprire tutti gli archi**: per ogni stato e per ogni **metodo** deve cioè esistere almeno un caso di test che esegue tale metodo essendo in tale stato;
- **coprire tutte le coppie di archi input-output**: per ogni stato e per ogni **coppia di archi entranti e uscenti** deve esistere almeno un caso di test che arriva nello stato tramite quello entrante e lo lascia da quello uscente; si considera dunque pure il come si arriva nello stato;
- **coprire tutti i cammini identificabili nel grafo**: spesso i cammini in questione sono *infiniti*, cosa che rende l'applicazione di questo criterio **infattibile**.


### Tipo di testing: white o black box?

Si è assunto che il diagramma degli stati facesse parte delle **specifiche del progetto**. Se così fosse, allora il testing sopra descritto sarebbe **black box**: il diagramma rappresenta sì la classe, ma è ancora una sua **astrazione**, senza il **codice effettivo** che rappresenta lo stato o che implementa un certo metodo, ma solo le relazioni tra i diversi stati.

In caso invece il diagramma degli stati non sia fornito, il testing delle classi è comunque possibile attraverso tecniche di **reverse engineering** guidata da certe euristiche (che operano ad un livello di astrazione variabile), **estraendo informazioni sugli stati** di una *classe già scritta*. Spesso tali info non sono comprensibili per un umano, motivo per cui vengono invece usate da vari tool di testing automatico. In questo caso però il testing assume caratteristiche **white box**, in quanto il codice che implementava la classe era **noto prima di iniziare a testarlo**. 