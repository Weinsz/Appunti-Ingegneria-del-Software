Si tratta di una tecnica [[eXtreme Programming (XP)]] controintuitiva, in quanto dal punto di vista del manager/cliente si pagano due persone per fare il lavoro di una, ma non funziona così.

Ci sono molti vantaggi:
- **ci si controlla a vicenda** su ogni aspetto (codice, regole XP, idee);
- mentre il **pilota** attua le idee, il **navigatore** pensa a cosa fare subito dopo: forma di [[Prodotto e Processo/eXtreme Programming/Tecniche/Refactoring|Refactoring]];
- favorisce l'**inserimento di nuovo personale**: piuttosto che lasciare i nuovi da soli, vengono affiancati e incitati a osservare e interagire con esperti che stanno lavorando;
- fa ottenere una [[Proprietà collettiva]] (**conoscenza osmotica**), come descritta da [[Metodologie Agile#^dc1741|Crystal]]. Un altro punto importante sono i **commenti naïve** (fatti da programmatori junior) che permettono di chiarire concetti basilari, dati spesso per scontati, e offrire nuovi punti di vista.

Si potrebbe pensare sia uno spreco di personale, ma raddoppiare il numero di persone raddoppia davvero la produttività? **No**, è stimato invece che la produttività aumenti circa del 50%. Dunque la programmazione a coppie, con una piccola perdita di produttività, offre tutti i vantaggi sopracitati. Per esempio nel singolo giorno si perde un po' più di tempo, ma nell'iterazione si hanno più vantaggi: si fanno meglio le cose.

Diversi studi si sono chiesti se la produttività calcolata puntualmente sia una metrica sensata. Secondo molti non lo è, perché al termine di un'iterazione ciò che sembra poco produttivo in realtà poi lo è di più: il tempo non impiegato in [[Verifica e convalida|verifica, convalida]] e [[Prodotto e Processo/eXtreme Programming/Tecniche/Refactoring|refactoring]] è largamente assorbito dall'**[[Software inspection|ispezione continua del codice]]** (non automatica) svolta nelle sessioni di pair programming. Questa tecnica cerca dunque di minimizzare i danni possibili.

### Critiche di Meyer

**Bertrand Meyer**, nel suo libro _“Agile! The Good, the Hype and the Ugly”_, scrive:

> **Applicata con giudizio, la programmazione in coppia può essere senza dubbio utile**. Molti sviluppatori apprezzano l'opportunità di programmare insieme a un collega, in particolare per affrontare una parte spinosa di un compito. Le tecniche di base, in particolare l'idea di esprimere i propri pensieri ad alta voce per ottenere un feedback immediato, sono ben comprese e ampiamente applicate. (Come manager, sento regolarmente da uno sviluppatore: 'Su questo problema vorrei impegnarmi in un giro di programmazione in coppia con X', e la trovo una buona idea.) 
>  
> Ciò che lascia perplessi è l'insistenza dei sostenitori di XP sul fatto che questa tecnica sia l'unico modo per sviluppare software e debba essere applicata in ogni momento. **Tale insistenza non ha senso**, per due ragioni.
> 
> Il primo è l’**inconcludenza dell’evidenza empirica**, sopracitata. Certo, la mancanza di dati viene spesso utilizzata come pretesto per bloccare l’introduzione di nuove tecniche. Quando un’idea è ovviamente produttiva, non dovremmo aspettare prove massicce e incontrovertibili. Ma qui c’è in realtà una discreta quantità di prove empiriche, e non mostra un vantaggio significativo per la programmazione in coppia. Essa può essere utile in alcune circostanze, ma se fosse sempre la soluzione gli studi lo dimostrerebbero. In assenza di prove scientifiche, una mossa universale si basa sull’ideologia, non sulla ragione.
> 
> La seconda ragione, che potrebbe anche spiegare perché i risultati degli studi variano, è che **le persone sono diverse**. Molti eccellenti programmatori amano interagire con qualcun altro quando scrivono programmi; e molti altri non lo fanno. Quelli del secondo tipo vogliono pensare in profondità, indisturbati. La visione agile generale è che la comunicazione dovrebbe essere incoraggiata e che i giorni del genio solitario e silenzioso sono finiti. Bene; ma se nel vostro team c'è un programmatore eccezionale che nei passaggi critici ha bisogno di pace, tranquillità e solitudine, lo cacciate dal team, o lo costringete a lavorare in un modo che per lui può essere una tortura?
> 
> Una cosa è esigere che le persone spieghino il loro lavoro agli altri; un'altra, piuttosto pericolosa, è **forzare un unico modello di lavoro**, soprattutto in uno sforzo intellettuale altamente creativo e stimolante. Quando Linus Torvalds scriveva Linux, era praticamente da solo; ciò non gli ha impedito di mostrare il suo codice e, in seguito, di coinvolgere migliaia di persone a collaborare alla sua realizzazione.