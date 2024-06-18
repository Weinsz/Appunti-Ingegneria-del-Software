### Concetto e struttura

Lo scopo del **diagramma dei componenti** è rappresentare e raggruppare i componenti del sistema. **_"Componente"_** è un termine generale che include file, librerie, documenti, ecc. ma che è diverso dal concetto di **classe**.

Il diagramma include:
- **componenti**: rettangoli che rappresentano una funzione di sistema ben determinata, possono anche essere _annidati_;
- **interfacce**: cerchi che indicano le **interfacce implementate** o utilizzate dai componenti. I collegamenti con i componenti indicano la presenza di una **dipendenza**;
- **stereotipi**: racchiusi tra i caratteri `<<>>`, etichettano e identificano una serie di funzionalità appartenenti a uno stesso **gruppo**.

> Un componente può usarne un altro conoscendone solo l’interfaccia.

![Esempio component diagram](https://marcobuster.github.io/sweng/assets/11_component-diagram-example.png)

### Identificare i componenti

Di seguito delle linee guida per identificare e rappresentare correttamente i componenti:
- definire una **parte rimpiazzabile** del sistema;
- capire quali parti del sistema sono **rimpiazzabili facilmente** e/o sono versionate separatamente;
- identificare quali parti del sistema svolgono una **funzione ben determinata**;
- pensare in termini di **gerarchia dei componenti**;
- chiarire l’esistenza di **dipendenze con altri componenti** e di dipendenze con le **interfacce**.

Da notare che in questo caso si parla di **tipi di componenti**, e non di **istanze di componenti**, inoltre ciò che rappresenta questo diagramma va a richiamare il pattern [[Façade]], infatti in entrambi i casi vengono mascherate le interazioni tra componenti in modo da fornire una visualizzazione più semplice del sistema.