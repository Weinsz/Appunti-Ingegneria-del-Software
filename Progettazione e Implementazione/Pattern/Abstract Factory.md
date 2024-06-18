- **Tipologia:** Creazionale
- **Scopo:** Consente di produrre famiglie di oggetti correlati senza specificarne le classi concrete. Di fatto si tratta di una fabbrica di fabbriche, che raggruppa le fabbriche singole collegate/dipendenti.

> Il pattern Abstract Factory fornisce un modo per incapsulare un gruppo di singole factory che hanno un tema comune senza specificare le loro classi concrete.
> -Wikipedia

Si tratta di una generalizzazione del [[Factory Method]] pattern che si usa quando, al posto di creare un solo oggetto aderente a un'interfaccia, è necessario **creare più oggetti aderenti a varie interfacce**, i cui tipi concreti siano però compatibili tra di loro.

### Esempio

Si immagini di aver progettato un'app cross-platform e di doverne creare la UI: dovrà avere stili diversi in base all'OS su cui viene eseguita. Non conoscendo su quale OS si starà operando, il resto dell'app gestirà gli elementi dell'UI tramite delle opportune interfacce che nascondano il tipo concreto delle istanze, il quale determinerà lo stile della loro rappresentazione: sarà però cruciale che **tutti gli elementi della UI condividano lo stesso stile** per motivi estetici.

Ecco dunque che entra in gioco il pattern **Abstract Factory**, che è in grado di fornire un'**interfaccia per creare famiglie di oggetti compatibili tra loro senza specificare la loro classe concreta**, così da garantire una certa **omogeneità** all’insieme.

Per fare ciò il pattern propone di creare un’interfaccia `AbstractFactory` contenente la definizione di un [[Factory Method]] per ogni tipo di prodotto astratto (`Product`) e una serie di `ConcreteFactory` che restituiranno dei `ConcreteProduct` in uno specifico stile: in questo modo, interagendo con una Factory concreta un Client potrà ottenere in modo a lui trasparente una serie di prodotti concreti coerenti in stile tra di loro.

[![](https://marcobuster.github.io/sweng/mdbook-plantuml-img/e042c830630551a7fa0bcc9e4fef561b10a64171.svg)]

Tornando al problema della UI, volendo sfruttare l’**Abstract Factory** pattern bisogna creare un’interfaccia `GUIFactory` che contenga la dichiarazione di due metodi creazionali, `createButton()` e `createCheckbox()`: questi permetteranno al client di creare un bottone e una checkbox nello stile specificato dalla classe concreta della factory; per ciascuno di tali elementi dell’UI dobbiamo dunque creare un’interfaccia prodotto, ovvero rispettivamente le interfacce `Button` e `Checkbox`. All’interno delle classi factory concrete tali metodi creazionali restituiranno però dei prodotti concreti nello stile specifico della factory da cui sono prodotti: così, per esempio, una `MacFactory` (stile di Mac OS) creerà `MacButton` e `MacCheckbox`, mentre una `WinFactory` (stile di Windows) creerà `WindowsButton` e `WinCheckbox`.

In questo modo la nostra applicazione dovrà possedere al suo interno unicamente un riferimento alla factory adatta all'OS su cui sta girando e potrà creare tramite essa tutti gli elementi di UI di cui avrà bisogno senza preoccuparsi di specificare ogni volta lo stile: la factory concreta glielo restituirà sempre nello stile selezionato inizialmente.

![Esempio abstract factory](https://marcobuster.github.io/sweng/assets/09_esempio-abstract-factory.png)


### Pro e Contro

#### Pro
- Puoi essere certo che i prodotti che ricevi da una fabbrica sono compatibili tra loro.
- Evita lo stretto accoppiamento tra prodotti concreti e codice client.
- [[Conoscenze preliminari#^62f6b3|Single Responsibility Principle]]
- [[Conoscenze preliminari#^14625c|Open/Closed Principle]]

#### Contro
- Il codice potrebbe diventare più complicato di quanto dovrebbe, poiché insieme al pattern vengono introdotte molte nuove interfacce e classi.


Molti progetti iniziano utilizzando il [[Factory Method]] (meno complicato e più personalizzabile tramite sottoclassi) e si evolvono verso Abstract Factory o [[Builder]] (più flessibile, ma più complicato).

Abstract Factory può fungere da alternativa a [[Façade]] quando si desidera solo nascondere il modo in cui gli oggetti del sottosistema vengono creati dal codice client.