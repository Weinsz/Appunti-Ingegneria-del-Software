### Terminologia nella comunicazione

La maggior parte dei problemi che si verificano durante lo sviluppo di un progetto sono causati da **problemi di comunicazione**. Ci possono essere incomprensioni quando le informazioni passano da una figura all'altra, come quando ci si interfaccia tra cliente, analista e programmatore.
**Il programmatore dovrà adattare il proprio linguaggio** per farsi comprendere dal cliente, prestando maggiore attenzione alla formalità e alla chiarezza della comunicazione con il passare del tempo. Più i concetti sono spiegati chiaramente, più è difficile riscontrare problemi successivamente: è dunque necessario far attenzione alla **terminologia** usata.

### Correttezza

#### Quando un programma si definisce corretto?

Considerando un **generico programma $P$** come una funzione da un insieme di dati $D$ (**dominio**) a un insieme di dati $R$ (**codominio**), allora:
- $P(d)$ indica **l'esecuzione di $P$** su un certo input $d$;
- il risultato $P(d)$ è **corretto** se soddisfa le **specifiche**, altrimenti è scorretto;
- $\text{ok}(P, d)$ indica la **correttezza** di $P$ per il dato $d$

quindi:
$$
\boxed{P \text{ è corretto} \Longleftrightarrow \forall d \in D \text{ }\text{ok}(P, d) \Longleftrightarrow \text{ok}(P, D)}
$$

^16c407

> [!NOTE] A parole:
> un programma è **corretto** quando/sse per ogni dato del dominio vale $\text{ok}(P,d)$, cioè P è corretto per tutti i dati del dominio.
> 
> Di conseguenza, per indicare la **correttezza del programma $P$** si usa la notazione $\text{ok}(P, D)$ che appunta indica che $P$ è corretto per qualunque $d\in{D}$.


### Definizione di un test

Durante l'attività di [[Verifica e Convalida/Analisi statica/Testing|Testing]] si sottopone il programma a una serie di stimolazioni per vederne il comportamento in queste circostanze.
Eseguire un test vuol dire quindi eseguire il programma con una serie di input appartenenti al suo dominio e confrontare i risultati ottenuti con quello atteso secondo le specifiche.

> [!NOTE] Definizione più rigorosa
> Un **test** è un **sottoinsieme del dominio dei dati** e un singolo **caso di test** è un elemento del sottoinsieme. Un test sono quindi **più stimolazioni**, mentre un caso di test ne è una **singola**.

Matematicamente:
- un test $T$ per un programma $P$ è un **sottoinsieme** del suo dominio $D$;
- un elemento $t$ di un test $T$ è detto **caso di test**;
- l'esecuzione di un test consiste nell'**esecuzione del programma $\forall t \in T \subseteq D$**.

Un programma $P$ **supera o passa un test** se:
$$
\boxed{\text{ok}(P, T) \Longleftrightarrow \forall t \in T \text{ }\text{ok}(P, t)}
$$

> [!NOTE] A parole:
> quindi un programma è **corretto per un test** quando/sse **per ogni caso di test** esso (il programma) è corretto.

Lo scopo dei test è però **ricercare comportamenti anomali** nel programma per poterli correggere, si dice quindi che

un test $T$ ha **successo** se:
$$
\boxed{\text{successo}(T,P) \Longleftrightarrow \exists t \in T \text{ }\text{ }\lnot \text{ ok}(P, t)}
$$

>[!NOTE] A parole:
>un test $T$ ha **successo** se rileva uno o più **malfunzionamenti** presenti nel programma $P$.


### Test ideale

**Se un test non rileva alcun malfunzionamento non significa che il programma sia corretto**.

Come visto tra le [[Verifica e Convalida/Tecniche#^4dc587|Tecniche]], il test è un'attività ottimistica e normalmente **il passaggio di un test non garantisce l'assenza di difetti/anomalie.** 
Questo smette però di essere vero nel caso di **test ideali**.

Un test $T$ si definisce **ideale** per $P$ **se e solo se**
$$
\boxed{\text{ok}(P, T) \Rightarrow \text{ok}(P, D)}
$$
ovvero se il **superamento del test** implica la **correttezza del programma**.

Purtroppo però in generale **è impossibile trovare un test ideale**, come suggerito dalla seguente ipotesi universalmente accettata:
>[!NOTE] Tesi di Dijkstra
> Il test di un programma può rilevare la presenza di malfunzionamenti, ma non può dimostrarne l'assenza.
> 
> Quindi **non esiste un algoritmo che dato un programma arbitrario $P$ generi un test ideale finito**.
> Il caso $T=D$ non va considerato.

^de3ff2

Si noti come la tesi escluda esplicitamente il **test esaustivo $T=D$**, restringendosi a considerare solo i **test finiti**, in quanto il dominio $D$ potrebbe essere infinito. Per capire il motivo di questa distinzione:
```java
static int sum(int a, int b) {
    return a + b;
}
```

In Java un `int` è espresso su 32 bit, quindi il dominio di questa semplice funzione somma ha cardinalità $2^{32}\cdot 2^{32}=2^{64}∼2\cdot10^{19}$. Considerando quindi un tempo di esecuzione ottimistico di *1 ns* per ogni caso di test, un test esaustivo che provi tutte le possibili combinazioni di interi impiegherebbe più di **600 anni** per essere eseguito per intero.

> Il **test esaustivo** è quindi **impraticabile**.