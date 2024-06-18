Conosciuto nelle sue versioni commerciali anche come:
- **USDP**: Unified Software Development Process
- **RUP**: Rational Unified Process

È un modello di processo definito dagli stessi creatori di UML, un modello _Object Oriented_ (**OO**), quindi ottimo da utilizzare in contemporanea. Esistono anche altri modelli **OO** come ad esempio _“Object Oriented Software Process”_ (**OOSP**).

In base al livello di astrazione nel quale ci troviamo è un metamodello che può essere definito:
- **Sequenziale**: dato che si compone di 4 nuove fasi che vengono ripetute in sequenza, e vengono chiamate:
    1. **Inception**;
    2. **Elaboration**;
    3. **Construction**;
    4. **Transition**.
- **Iterativo**: ogni fase è svolta in maniera iterativa; in ogni iterazione si ripetono (in modo più o meno presente) le diverse attività che già conosciamo.
- **Incrementale**: alla fine delle 4 fasi si arriva ad una “release” e successivamente si riprende dalla prima (in modo iterativo, appunto) per proseguire con lo sviluppo.

### Fasi

![Unified Process phases](https://marcobuster.github.io/sweng/assets/06_unified-process-phases.png)

Le diverse righe rappresentano le attività già studiate, viste in tutti gli altri [[Modelli di ciclo di vita del software|modelli]], e in questo modello vengono chiamate _workflow_ o _activity_. Questi _workflow_ non si susseguono come nei casi precedenti, ma si sovrappongono (**over-lapping**) all’interno delle diverse fasi. 
È possibile definire lo scopo di una fase ma non in maniera precisa, ad esempio la fase di *Construction* rappresenta prevalentemente la parte di creazione del codice all’interno del progetto (*Implementation*), ma come è possibile notare nel grafico anche tutti gli altri workflows sono presenti anche se in modo meno predominante.

Questo schema permette di comprendere la complessità di un processo, ma che riconosce la necessità di un rigore, ovvero dei momenti in cui è necessario concentrarsi in modo maggiore su certe attività, infatti sono presenti delle **milestone**, cioè dei documenti che indicano la fine di una certa fase (si intende la fine della fase nell’iterazione corrente, infatti tutte le fasi vengono rieseguite ad ogni iterazione).

Le attività sono tutte troppo intersecanti tra loro, perciò è definito come **metamodello**, infatti non potrà essere seguito alla lettera ma dovrà essere adattato in base alle esigenze del progetto e del team di sviluppo. Può essere addirittura reso [[Metodologie Agile|agile]] con le opportune modifiche.