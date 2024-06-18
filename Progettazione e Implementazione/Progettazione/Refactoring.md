Durante il refactoring vanno rispettate le seguenti regole:
- **le modifiche al codice non devono modificare le funzionalità**: il refactoring **deve** essere invisibile al cliente;
- **non possono essere inseriti test aggiuntivi** rispetto alla fase verde appena raggiunta.

Se la fase di refactoring sta richiedendo troppo tempo allora è possibile tornare all’ultima versione verde e **pianificare meglio** l’attività di refactoring, per esempio scomponendola in più step. Vale la regola del _“do it twice”_: il secondo approccio a un problema è solitamente più veloce e migliore.

Spesso le motivazioni dietro un refactoring sono:
- **precedente design molto complesso e poco leggibile**, per via della velocità nell'andare sul verde;
- **preparare il design di una feature** che non si integra bene nel design attuale: dopo aver raggiunto il verde in una feature, è possibile che la feature successiva sia difficile da integrare. In questo caso, se il refactoring non è banale bisogna fermarsi, tornare indietro ed evolvere il codice per facilitare l'iterazione successiva (**design for change**).
- presenza di **debito tecnico** sul lavoro fatto in precedenza, ovvero debolezze e scorciatoie che ostacolano notevolmente evoluzioni future. *"Ogni debito tecnico lo si ripaga con gli interessi"*.