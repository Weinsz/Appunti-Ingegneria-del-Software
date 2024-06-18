#### Il processo d'ispezione del sw funziona?

Prove empiriche parrebbero suggerire che la risposta sia **sì** e evidenziano anche che tale tecnica sia **particolarmente *cost-effective*** (conveniente). 

I vantaggi dell'uso di questa tecnica di [[Verifica e convalida]] sono numerosi:
- esiste un **processo rigoroso e dettagliato**;
- si basa sull'**accumulo di esperienza**, migliorandosi da sé col tempo grazie alle *checklist*;
- il processo integra una serie d'**incentivi sociali** che spingono l'**autore** del codice ad analizzarlo in modo critico;
- a differenza del testing dove è impossibile fare testing esaustivo, per la mente umana è possibile **astrarre il dominio completo dei dati**, considerandolo interamente, quindi in un certo senso tutti i casi di test; 
- è applicabile anche a **programmi incompleti**.

La software inspection funziona così bene che è spesso utilizzata come _baseline_ per **valutare altre tecniche** di verifica e convalida.

Questo non significa però che essa sia esente da **limiti**:
- il test può essere fatto **solo a livello di unità** (*unit testing*) in quanto la mente umana ha difficoltà a lavorare in situazioni in cui sono presenti **molte informazioni** (tantissime righe/pagine) contemporaneamente in assenza d'**astrazioni** e indirettezze.
- la software inspection **non è incrementale**: spesso infatti la fase di **follow-up** non è così efficace, in quanto il codice è cambiato talmente tanto che è necessario ricominciare da capo l'ispezione.

Ciò non toglie però che, al netto anche di essere "costosa" per le persone coinvolte, come afferma la **Legge di Fagan (L17)**:

> [!NOTE] Legge di Fagan (L17)
> Le ispezioni aumentano in maniera significativa la produttività, la qualità e la stabilità del progetto.
