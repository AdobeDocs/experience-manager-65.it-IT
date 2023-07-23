---
title: Creazione di moduli adattivi accessibili
seo-title: Creating accessible adaptive forms
description: AEM Forms fornisce strumenti e strumenti per creare moduli adattivi accessibili e consente di rispettare gli standard di accessibilità.
seo-description: AEM Forms provides you tools and to create accessible adaptive forms and helps comply with accessibility standards.
uuid: 6472bc2d-47ca-4883-88b7-5de0b758fd00
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 1e95c66b-d132-4c44-a1dc-31fd09af8113
docset: aem65
feature: Adaptive Forms
exl-id: e755159f-374f-42b8-b28b-e8864df44f9d
source-git-commit: e7a3558ae04cd6816ed73589c67b0297f05adce2
workflow-type: tm+mt
source-wordcount: '2111'
ht-degree: 0%

---

# Creazione di moduli adattivi accessibili{#creating-accessible-adaptive-forms}

<span class="preview"> L’Adobe consiglia di utilizzare l’acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [creazione di un nuovo Forms adattivo](/help/forms/using/create-an-adaptive-form-core-components.md) o [aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base. </span>

## Introduzione {#introduction}

Un modulo accessibile è un modulo utilizzabile da tutti, inclusi gli utenti con esigenze speciali. Forms adattivo include una serie di funzioni e funzionalità che migliorano l’usabilità per gli utenti con funzionalità diverse. Creare l’accessibilità nei moduli adattivi non solo consente al pubblico di contenuti di essere il più ampio possibile, ma è anche un requisito necessario quando si forniscono documenti in aree geografiche in cui è richiesta la conformità agli standard di accessibilità. Aiuta gli sviluppatori di moduli AEM Forms a rispettare gli standard di accessibilità.

Durante la creazione di un modulo adattivo, l’autore deve considerare i seguenti punti per creare un modulo adattivo accessibile:

* Controllare il modulo con lo strumento di test di accessibilità di Nome accessibile e Descrizione (ANDI)
* Fornire etichette appropriate per i controlli modulo
* Fornisci equivalenti di testo per le immagini
* Fornire un contrasto del colore sufficiente
* Verificare che i controlli del modulo siano accessibili da tastiera

## Prerequisito

È necessario uno strumento di accessibilità, ad esempio **Ispettore nome e descrizione (ANDI) accessibile** e un **Tema del modulo adattivo sviluppato per risolvere i problemi relativi all’accessibilità** per creare un modulo adattivo accessibile.

### Scarica e installa lo strumento di test di accessibilità

Lo strumento ANDI (Accessible Name and Description Inspector) consente di identificare e risolvere i problemi correlati alla conformità per l’accessibilità nel contenuto Web. È lo strumento consigliato nelle linee guida Trusted Tester v5 del Department of Homeland Security. È stato sviluppato dal Dipartimento della Social Security Administration&#x200B; degli Stati Uniti per verificare la conformità alla Sezione 508 dei contenuti web. Lo strumento:

* Consente di rilevare i problemi di accessibilità&#x200B; in una pagina web
* Fornisce suggerimenti per migliorare l’accessibilità&#x200B;
* Rileva problemi di accessibilità della tastiera e di contrasto dei colori
* Identifica chiaramente i contenuti degli assistenti vocali in conformità agli standard

ANDI funziona con tutti i principali browser Internet. Vedi, [Documentazione di ANDI](https://www.ssa.gov/accessibility/andi/help/install.html) per istruzioni dettagliate su come configurare e utilizzare lo strumento.

### Scarica e installa il tema Ultramarine-Accessible

Il tema Ultramarine-Accessible è un tema di riferimento. Illustra come correggere il contrasto dei colori e altri problemi correlati all’accessibilità in un modulo adattivo. L’Adobe consiglia di creare un tema personalizzato per l’ambiente di produzione in base agli stili approvati dall’organizzazione. Per caricare il tema nell’istanza AEM, effettua le seguenti operazioni:

1. Scarica il pacchetto del tema.
1. Accedi a **[!UICONTROL Experience Manager]** > **[!UICONTROL Navigazione]** ![Navigazione](assets/Smock_Compass_18_N.svg) > **[!UICONTROL Forms]** sull’istanza AEM.
1. Tocca **[!UICONTROL Crea]** > **[!UICONTROL Caricamento file]**. Seleziona e carica il file x Ultramarine-Accessible-Theme.zip. Carica il tema nell’istanza AEM.

## Rendere accessibile un modulo adattivo

Per rendere accessibile un modulo adattivo, è necessario concentrarsi su quattro aspetti chiave: navigazione da tastiera, contrasto dei colori, testo alternativo significativo per le immagini ed etichette appropriate per i controlli Forms. Per rendere accessibili i moduli adattivi esistenti, effettua le seguenti operazioni:

### 1. Applicare un tema accessibile ed eseguire correzioni aggiuntive

Applica al modulo adattivo esistente il tema Accessibile in modalità ultramarina. Per applicare il tema:

1. Apri il modulo adattivo per la modifica.
1. Seleziona un componente e tocca l’icona principale. Nel menu di scelta rapida, tocca **[!UICONTROL Contenitore modulo adattivo]** quindi tocca l’icona configura.
1. Seleziona il tema Ultramarine-Accessible nel browser delle proprietà e tocca **[!UICONTROL Salva]** icona.
1. Aggiorna la finestra del browser. Il tema viene applicato al modulo adattivo.

Dopo aver applicato un tema accessibile, esegui le correzioni aggiuntive elencate di seguito. Le correzioni si aggiungono alle correzioni di accessibilità trattate nel tema accessibile:

1. Aggiungi un testo alternativo significativo per l’immagine del logo nel modulo adattivo.

   Fornisci un testo alternativo significativo per le immagini nei componenti intestazione e piè di pagina del modello di modulo adattivo. Quando si corregge il modello e lo si utilizza per creare un modulo adattivo, i moduli adattivi ereditano tutte le correzioni relative all’accessibilità applicate all’intestazione e al piè di pagina del modello.  Per un modulo adattivo esistente, apporta modifiche a livello di modulo adattivo. Le modifiche apportate a un modello di modulo adattivo non passano automaticamente a un modulo adattivo esistente.

1. Aggiungi al modulo adattivo un componente intestazione contenente il nome del modulo. Se la struttura del modulo specifica il nome di una società, aggiungere anche un componente intestazione separato per il nome della società.

   La maggior parte degli strumenti di accessibilità informa gli utenti sulla gerarchia dei contenuti per aiutarli a comprendere la struttura della pagina web. Per fornire una struttura gerarchica al testo, imposta diversi livelli di intestazione per il nome dell’organizzazione e il testo del nome del modulo nel modulo adattivo. Inoltre, utilizza un componente Testo prima di ogni pannello e sezione con un livello di intestazione appropriato per creare una gerarchia.

   ![Come applicare uno stile di intestazione](assets/apply-style.gif)

1. Modifica il colore di sfondo del piè di pagina per utilizzare un contrasto appropriato in conformità agli standard di accessibilità per migliorare la visibilità e la leggibilità del testo. È possibile utilizzare ANDI per individuare problemi di contrasto dei colori nel modulo. Inoltre, non utilizzare caratteri molto piccoli. I caratteri piccoli sono difficili da leggere.

1. Sostituisci i componenti di scelta dello switch e dell’immagine nel modulo adattivo esistente con il componente di scelta (radio).

1. Sostituisci il componente stepper numerico nel modulo adattivo esistente con il componente casella numerica.

1. Sostituisci il campo di immissione data con il campo del selettore data.

1. Imposta i pattern di visualizzazione, convalida e modifica per il componente del selettore data. Impostare inoltre un messaggio di errore di convalida personalizzato. Ad esempio, è stata specificata una data non valida. Il formato corretto della data è AAAA-MM-GG.

1. Imposta il testo di accessibilità personalizzato per il componente Selezione data. Ad esempio, immetti la data di nascita. Gli assistenti vocali leggono questi testi personalizzati di accessibilità.

1. Utilizza una descrizione breve invece di una descrizione lunga per i componenti del modulo adattivo. Una descrizione lunga aggiunge un pulsante della guida. Assicurati che il modulo adattivo non disponga di alcun pulsante Aiuto.

1. Aggiungere testo personalizzato per l&#39;accesso facilitato a tutte le celle di sola lettura delle tabelle. Disattivare inoltre tutte le celle di sola lettura delle tabelle.

1. Rimuovi gli eventuali campi di firma scarabocchio nel modulo adattivo. Configura il modulo adattivo per utilizzare Adobe Sign per un’esperienza di firma digitale fluida.

### 2. Fornire etichette appropriate per i controlli dei moduli {#provide-proper-labels-for-form-controls}

L’etichetta o il titolo di un componente identifica ciò che il componente modulo rappresenta. Ad esempio, il testo &quot;Nome&quot; indica agli utenti che devono immettere il proprio nome in un campo di testo. Per essere accessibile agli assistenti vocali, l’etichetta è associata a livello di programmazione a un componente modulo. In alternativa, il controllo modulo viene configurato con informazioni aggiuntive sull&#39;accessibilità.

L’etichetta percepita dagli assistenti vocali non deve necessariamente essere la stessa della didascalia visiva. In alcuni casi può essere utile specificare meglio lo scopo del controllo. Per ogni oggetto campo di un modulo, è possibile utilizzare le opzioni di accesso facilitato per specificare ciò che l&#39;assistente vocale annuncia per identificare il campo modulo specifico.

Per utilizzare l&#39;opzione Accessibilità, effettuare le seguenti operazioni:

1. Seleziona un componente e tocca ![cmppr](assets/cmppr.png).
1. Clic **[!UICONTROL Accessibilità]** nella barra laterale per scegliere l’opzione di accessibilità desiderata.

### Opzioni di accessibilità nei componenti del modulo {#accessibility-options-in-form-components}

![Opzioni di accessibilità nei componenti del modulo](assets/accessibility-options.png)

**Testo personalizzato** Gli autori dei moduli forniscono il contenuto nel campo di testo personalizzato dell’opzione di accessibilità. La tecnologia per l’accessibilità, come gli assistenti vocali, utilizza questo testo personalizzato. L’utilizzo dell’impostazione Titolo è l’opzione migliore nella maggior parte degli scenari. Valuta la possibilità di creare un testo di Reader con schermo personalizzato solo quando non è possibile utilizzare il titolo o una breve descrizione.

**Breve descrizione** Per la maggior parte dei componenti, la breve descrizione viene visualizzata in fase di runtime quando l’utente passa il puntatore sul componente. È possibile impostare questa opzione nel campo breve descrizione in opzione contenuto della Guida.

**Titolo** Utilizza questa opzione per consentire ad AEM Forms di utilizzare l’etichetta visiva associata al campo del modulo come testo per la lettura dello schermo.

**Nome** È possibile specificare un valore nel campo Nome della scheda Associazione. Il nome non può contenere spazi.

**Nessuno** Selezionando Nessuno, l’oggetto modulo non avrà un nome nel modulo pubblicato. Nessuna è un&#39;impostazione consigliata per i controlli modulo.

>[!NOTE]
>
>* Il pulsante di opzione e la casella di controllo possono avere solo due opzioni per l&#39;accessibilità, ovvero Testo personalizzato e Titolo.
>* Per i moduli adattivi basati su XFA, l’opzione di accessibilità viene ereditata dalle opzioni di accessibilità impostate in XDP. Le descrizioni comandi da XDP sono mappate a Descrizione breve e la didascalia a Titolo. Le altre opzioni funzionano nello stato corrente.

### 3. Fornire equivalenti testuali per le immagini {#provide-text-equivalents-for-images}

Le immagini possono aiutare alcuni utenti a comprendere meglio la situazione. Tuttavia, per gli utenti che utilizzano utilità per la lettura dello schermo, le immagini riducono l’accessibilità del modulo. Se scegli di utilizzare le immagini, fornisci descrizioni testuali per tutte le immagini.

Verificare che il testo descriva l&#39;oggetto e il relativo scopo nel modulo. Un assistente vocale legge questo testo alternativo quando incontra un’immagine. Per un&#39;immagine deve essere sempre specificato un testo alternativo.

Seleziona un componente immagine e tocca ![cmppr](assets/cmppr.png). Nella barra laterale, in Proprietà, specifica il testo alternativo per un’immagine.

![Testo alternativo per un&#39;immagine](assets/image-properties.png)

### 4. Fornire un contrasto del colore sufficiente {#provide-sufficient-color-contrast}

Per la progettazione dell’accessibilità è necessario considerare ulteriori linee guida sull’utilizzo dei colori. Gli autori di moduli possono utilizzare i colori per migliorare l&#39;aspetto dei moduli evidenziandone i diversi componenti. Tuttavia, un uso improprio del colore può rendere una forma difficile o impossibile da leggere da persone con abilità diverse.

Gli utenti con problemi di vista si affidano a un contrasto elevato tra testo e sfondo per leggere contenuti digitali. Senza un contrasto sufficiente, un modulo può diventare difficile, se non impossibile, da leggere per alcuni utenti.

Si consiglia di utilizzare i colori predefiniti per il carattere e lo sfondo, ovvero il contenuto in nero su sfondo bianco. Se modificate i colori predefiniti, scegliete un colore di primo piano scuro su uno sfondo chiaro o viceversa.

Consulta [Creazione di temi personalizzati per i moduli adattivi](/help/forms/using/creating-custom-adaptive-form-themes.md), per ulteriori informazioni sulla modifica del contrasto e del tema dei colori per i moduli adattivi.

### 5. Assicurarsi che i controlli del modulo siano accessibili da tastiera {#ensure-that-form-controls-are-keyboard-accessible}

Un modulo accessibile può essere compilato completamente utilizzando solo la tastiera o un dispositivo di input equivalente. Gli utenti con mobilità ridotta o problemi di vista potrebbero non avere altra scelta se non quella di utilizzare la tastiera e molti utenti che possono utilizzare il mouse preferiscono l&#39;input da tastiera. Consentendo l&#39;utilizzo di vari metodi di input, non solo si creano moduli accessibili, ma si creano anche moduli più adatti alle preferenze di tutti gli utenti.

In AEM Forms sono disponibili le seguenti scelte rapide da tastiera.

| Azione | Scelta rapida da tastiera |
|---|---|
| Spostare il cursore in avanti in un modulo | Tabulazione |
| Spostare il cursore all&#39;indietro in un modulo | Maiusc+Tab |
| Passa al pannello successivo | Alt+Freccia destra |
| Passa al pannello precedente | Alt+Freccia sinistra |
| Reimpostare i dati compilati in un modulo | ALT+R |
| Inviare un modulo | ALT+S |

Sono inoltre disponibili vari tasti di scelta rapida per **[!UICONTROL Selettore data]** in Adaptive Forms. Per attivare i tasti di scelta rapida, toccare **[!UICONTROL Selettore data]** componente e tocca ![Configura](assets/configure-icon.svg) per aprire le proprietà. In **[!UICONTROL Pattern]** , selezionare un motivo di visualizzazione utilizzando la **[!UICONTROL Tipo]** e **[!UICONTROL Pattern]** elenchi a discesa. Salva le proprietà per abilitare l&#39;utilizzo dei tasti di scelta rapida per **[!UICONTROL Selettore data]** componente.

Per il componente Selezione data in Adaptive Forms sono disponibili i seguenti tasti di scelta rapida da tastiera:

| Azione | Scelta rapida da tastiera |
|---|---|
| <ul><li>Visualizzare le opzioni del componente Selezione data quando lo stato attivo della scheda evidenzia l’icona del calendario</li><li>Esegui l’evento clic quando lo stato attivo della scheda evidenzia un’opzione</li> | Spazio o Invio |
| Nascondi le opzioni del componente Selettore data | Esc |
| <ul><li>Sposta il cursore in avanti tra le opzioni disponibili nel componente Selettore data.</li><li>Imposta lo stato attivo della scheda sull’icona del calendario quando il campo di immissione data è attivo</li> | Tabulazione |
| Sposta il cursore all’indietro tra le opzioni disponibili nel componente Selettore data | Maiusc+Tab |
| <ul><li>Visualizzare le opzioni del componente Selezione data quando lo stato attivo della scheda evidenzia il campo di immissione della data</li><li>Sposta il cursore verso il basso nel calendario disponibile nel componente Selettore data</li> | Freccia giù |
| Sposta il cursore verso l’alto nel calendario disponibile nel componente Selettore data | Freccia Su |
| Sposta il cursore all’indietro nel calendario disponibile nel componente Selettore data | Freccia sinistra |
| Sposta il cursore in avanti nel calendario disponibile nel componente Selezione data | Freccia destra |
| Eseguire l&#39;azione per la didascalia disponibile tra le frecce di navigazione destra e sinistra nel calendario | Maiusc + Freccia Su |
| Esegui l&#39;azione per l&#39;icona freccia di navigazione a destra ![freccia destra](assets/right-navigation-icon.svg) disponibile nel calendario | Maiusc + Freccia sinistra |
| Esegui l&#39;azione per l&#39;icona freccia di navigazione a sinistra ![freccia sinistra](assets/left-navigation-icon.svg) disponibile nel calendario | Maiusc + Freccia destra |

## Utilizzare lo strumento di accessibilità per individuare i problemi di accessibilità rimanenti

La funzione ANDI (Accessible Name and Description Inspector) consente di identificare e risolvere i problemi correlati alla conformità in materia di accessibilità in un modulo adattivo. Per utilizzare lo strumento ANDI per individuare i problemi di accessibilità in un modulo adattivo:

1. Apri il modulo adattivo in modalità anteprima.
1. Fai clic sull’icona dello strumento ANDI con segnalibro. Lo strumento ANDI analizza il modulo adattivo e visualizza i problemi di accessibilità. Per informazioni dettagliate su come utilizzare lo strumento, consulta [Documentazione di ANDI](https://www.ssa.gov/accessibility/andi/help/howtouse.html).
1. Rivedi e risolvi i problemi segnalati da ANDI.
