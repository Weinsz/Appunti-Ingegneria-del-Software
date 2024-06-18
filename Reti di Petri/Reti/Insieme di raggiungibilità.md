L'**insieme di raggiungibilità** $R$ di una rete $P/T$ a partire da una marcatura $M$ è **il più piccolo insieme di marcature** tale che:
- $M \in R(P/T, M)$
- $(M' \in R(P/T, M) \land \exists t \in T \space | \space M'\space [\space t> M'') \Longrightarrow M'' \in R(P/T, M)$

Questa definizione induttiva viene interpretata nel seguente modo:
- **passo base**: la marcatura $M$ appartiene all’insieme di raggiungibilità $R(P/T,M)$ (dove $M$ indica la marcatura iniziale, mentre $P/T$ indica la rete posti-transizioni);
- **passo induttivo**: se $M'$ appartiene all’insieme di raggiungibilità (quindi si dice che _è raggiungibile_) ed esiste una transizione della rete tale per cui è abilitata in $M'$ e porta in $M''$ — per cui con uno scatto è possibile passare dalla marcatura $M'$ alla marcatura $M''$ — _allora_ anche quest’ultima è **raggiungibile**.
Procedendo **ricorsivamente** con questa definizione è possibile ottenere tutte le marcature raggiungibili.