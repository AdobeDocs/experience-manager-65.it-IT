---
title: Creazione di moduli adattivi con accesso facilitato
seo-title: Creazione di moduli adattivi con accesso facilitato
description: AEM Forms fornisce gli strumenti necessari per creare moduli adattivi accessibili e contribuisce a rispettare gli standard di accessibilità.
seo-description: AEM Forms fornisce gli strumenti necessari per creare moduli adattivi accessibili e contribuisce a rispettare gli standard di accessibilità.
uuid: 6472bc2d-47ca-4883-88b7-5de0b758fd00
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 1e95c66b-d132-4c44-a1dc-31fd09af8113
docset: aem65
feature: Moduli adattivi
translation-type: tm+mt
source-git-commit: 7a3f54d90769708344e6751756b2a12ac6c962d7
workflow-type: tm+mt
source-wordcount: '2078'
ht-degree: 1%

---


# Creazione di moduli adattivi accessibili{#creating-accessible-adaptive-forms}

## Introduzione {#introduction}

Un modulo accessibile è un modulo utilizzabile da tutti, inclusi gli utenti con esigenze particolari. Adaptive Forms include una serie di funzioni e funzionalità che migliorano l&#39;usabilità per gli utenti con capacità diverse. La creazione dell’accessibilità nei moduli adattivi non solo consente al pubblico di accedere al contenuto nel modo più ampio possibile, ma è anche un requisito per la fornitura di documenti in aree geografiche in cui viene richiesto di rispettare gli standard di accessibilità. Aiuto per gli sviluppatori di moduli per conformarsi agli standard di accessibilità.

Durante la creazione di un modulo adattivo, l’autore deve considerare i seguenti punti per creare un modulo adattivo accessibile:

* Controllare il modulo con lo strumento di test dell’accessibilità di Nome e Descrizione accessibile (ANDI)
* Fornire etichette appropriate per i controlli del modulo
* Fornire equivalenti testuali per le immagini
* Fornire un contrasto di colore sufficiente
* Verificare che i controlli modulo siano accessibili da tastiera

## Prerequisito

Per creare un modulo adattivo accessibile, è necessario uno strumento di accessibilità come **Nome e descrizione accessibili (ANDI)** e un tema **Modulo adattivo sviluppato per risolvere i problemi relativi all’accessibilità** .

### Scarica e installa lo strumento di test dell’accessibilità

Lo strumento di ispezione nome e descrizione accessibile (ANDI) consente di identificare e risolvere i problemi relativi alla conformità in materia di accessibilità nei contenuti web. È lo strumento consigliato sotto le linee guida di Trusted Tester v5 del Dipartimento della Sicurezza Interna. È sviluppato dal dipartimento di amministrazione della sicurezza sociale &#x200B; Stati Uniti per verificare la conformità Sezione 508 dei contenuti web. Lo strumento:

* Consente di rilevare i problemi di accessibilità &#x200B; in una pagina web
* Fornisce suggerimenti per migliorare l&#39;accessibilità &#x200B;
* Rileva problemi di accessibilità e contrasto del colore della tastiera
* Identifica chiaramente il contenuto dell’assistente vocale in conformità agli standard

ANDI funziona con tutti i principali browser Internet. Per istruzioni dettagliate su come configurare e utilizzare lo strumento, consulta la [documentazione di ANDI](https://www.ssa.gov/accessibility/andi/help/install.html) .

### Scarica e installa il tema Ultramarine-Accessible

Il tema Ultramarina-Accessibile è un tema di riferimento. Questo aiuta a dimostrare come correggere il contrasto del colore e altri problemi di accessibilità in un modulo adattivo. Adobe consiglia di creare un tema personalizzato per l’ambiente di produzione in base agli stili approvati dall’organizzazione. Esegui i seguenti passaggi per caricare il tema nell’istanza AEM:

1. Scarica il pacchetto tematico.
1. Passa a **[!UICONTROL Experience Manager]** > **[!UICONTROL Navigazione]** ![Navigazione](assets/Smock_Compass_18_N.svg) > **[!UICONTROL Forms]** nell&#39;istanza AEM.
1. Tocca **[!UICONTROL Crea]** > **[!UICONTROL Caricamento file]**. Seleziona e carica il file x Ultramarine-Accessible-Theme.zip . Carica il tema nella tua istanza AEM.

## Rendere un modulo adattivo accessibile

È necessario concentrarsi su quattro aspetti principali: navigazione da tastiera, contrasto del colore, testo alternativo significativo per le immagini ed etichette appropriate per i controlli dei moduli per rendere un modulo adattivo accessibile. Per rendere accessibili i moduli adattivi esistenti, effettua le seguenti operazioni:

### 1. Applicare un tema accessibile ed eseguire correzioni aggiuntive

Applica il tema Ultramarine-Accessible al modulo adattivo esistente. Per applicare il tema:

1. Apri il modulo adattivo per la modifica.
1. Seleziona un componente e tocca l’icona principale. Nel menu di scelta rapida, tocca **[!UICONTROL Contenitore modulo adattivo]** e quindi tocca l’icona di configurazione.
1. Seleziona il tema Ultramarine-Accessible nel browser delle proprietà e tocca l&#39;icona **[!UICONTROL Salva]** .
1. Aggiorna la finestra del browser. Il tema viene applicato al modulo adattivo.

Dopo aver applicato un tema accessibile, esegui le seguenti correzioni aggiuntive elencate. Le correzioni sono in aggiunta alle correzioni di accessibilità trattate nel tema accessibile:

1. Aggiungi un testo alternativo significativo per l’immagine del logo nel modulo adattivo.

   Fornire un testo alternativo significativo per le immagini nei componenti di intestazione e piè di pagina del modello di modulo adattivo. Quando si corregge il modello e lo si utilizza per creare un modulo adattivo, i moduli adattivi ereditano tutte le correzioni relative all’accessibilità applicate all’intestazione e al piè di pagina del modello.  Per un modulo adattivo esistente, apportare modifiche a livello di modulo adattivo. Le modifiche apportate a un modello di modulo adattivo non passano automaticamente a un modulo adattivo esistente.

1. Aggiungi al modulo adattivo un componente di intestazione contenente il nome del modulo. Se la struttura del modulo specifica il nome di una società, aggiungere un componente di intestazione separato anche per il nome della società.

   La maggior parte degli strumenti di accessibilità informa gli utenti della gerarchia dei contenuti per aiutarli a comprendere la struttura della pagina web. Impostare diversi livelli di intestazione per il nome dell’organizzazione e il testo del nome del modulo nel modulo adattivo per fornire una struttura gerarchica a questo testo. Inoltre, per creare una gerarchia, utilizza un componente Testo prima di ciascun pannello e sezione con un livello di intestazione appropriato.

   ![Come applicare uno stile di intestazione](assets/apply-style.gif)

1. Modificare il colore di sfondo del piè di pagina per utilizzare un contrasto adeguato in conformità agli standard di accessibilità per migliorare la visibilità e la leggibilità del testo. È possibile utilizzare ANDI per trovare problemi di contrasto del colore nel modulo. Inoltre, non utilizzare caratteri molto piccoli. I caratteri piccoli sono difficili da leggere.

1. Sostituisci i componenti di scelta dell’interruttore e dell’immagine nel modulo adattivo esistente con il componente di scelta (radio).

1. Sostituisci il componente passo numerico nel modulo adattivo esistente con il componente casella numerica.

1. Sostituisci il campo di immissione data con il campo del selettore data.

1. Impostare pattern di visualizzazione, convalida e modifica per il componente del selettore data. Inoltre, impostare un messaggio di errore di convalida personalizzato. Ad esempio, è stata specificata una data non valida. Il formato corretto della data è AAAA-MM-GG.

1. Imposta il testo di accessibilità personalizzato per il componente del selettore data. Ad esempio, Inserisci la data di nascita. Gli assistenti vocali leggono questi testi personalizzati di accessibilità.

1. Per i componenti per moduli adattivi, utilizza una descrizione breve anziché una descrizione lunga. Una lunga descrizione aggiunge il pulsante della guida. Assicurarsi che nel modulo adattivo non sia presente alcun pulsante di aiuto.

1. Aggiunta di testo di accesso facilitato personalizzato a tutte le celle di sola lettura delle tabelle. Inoltre, disattivare tutte le celle di sola lettura delle tabelle.

1. Rimuovere i campi firma scarabocchio, se presenti nel modulo adattivo. Configura il modulo adattivo per utilizzare Adobe Sign per un’esperienza di firma digitale fluida.

### 2. Fornire etichette appropriate per i controlli del modulo {#provide-proper-labels-for-form-controls}

L’etichetta o il titolo di un componente identifica ciò che rappresenta il componente modulo. Ad esempio, il testo &quot;Nome&quot; indica agli utenti che devono immettere il proprio nome in un campo di testo. Per essere accessibile agli assistenti vocali, l’etichetta è associata a un componente modulo a livello di programmazione. In alternativa, il controllo modulo è configurato con ulteriori informazioni di accesso facilitato.

L’etichetta percepita dagli assistenti vocali non deve necessariamente corrispondere alla didascalia visiva. In alcuni casi, potrebbe essere utile specificare in modo più specifico lo scopo del controllo. Per ciascun oggetto campo di un modulo, le opzioni di accessibilità possono essere utilizzate per specificare gli annunci dell’assistente vocale relativi all’identificazione del campo modulo specifico.

Per utilizzare l’opzione Accessibilità, attenersi alla seguente procedura:

1. Seleziona un componente e tocca ![cmppr](assets/cmppr.png).
1. Fai clic su **[!UICONTROL Accessibilità]** nella barra laterale per scegliere l&#39;opzione di accessibilità desiderata.

### Opzioni di accessibilità nei componenti modulo {#accessibility-options-in-form-components}

![Opzioni di accessibilità nei componenti modulo](assets/accessibility-options.png)

**Gli autori di** moduli di testo personalizzati forniscono il contenuto dell’opzione di accesso facilitato Campo di testo personalizzato. La tecnologia per l’accessibilità, ad esempio gli assistenti vocali, utilizza questo testo personalizzato. L’utilizzo dell’impostazione Titolo è l’opzione migliore nella maggior parte degli scenari. È consigliabile creare un testo personalizzato del Reader di schermate solo quando si utilizza il Titolo o se non è possibile utilizzare una breve descrizione.

**Breve** descrizionePer la maggior parte dei componenti, la breve descrizione viene visualizzata in fase di runtime quando l’utente passa il puntatore sul componente. È possibile impostare questa opzione nel campo breve descrizione, sotto l&#39;opzione di contenuto della guida.

**** TitoloUtilizza questa opzione per consentire ad AEM Forms di utilizzare l’etichetta visiva associata al campo modulo come testo per l’assistente vocale.

**** NomeÈ possibile specificare un valore nel campo Nome della scheda Binding. Il nome non può contenere spazi.

**** Se si seleziona Nessuno, l’oggetto modulo non avrà un nome nel modulo pubblicato. Nessuna impostazione consigliata per i controlli modulo.

>[!NOTE]
>
>* I pulsanti di scelta e le caselle di controllo possono avere solo due opzioni di accessibilità, ovvero Testo personalizzato e Titolo.
>* Per i moduli adattivi basati su XFA, l’opzione di accessibilità viene ereditata dalle opzioni di accessibilità impostate in XDP. Le descrizioni comandi da XDP sono mappate su Descrizione breve e Didascalia sono mappate su Titolo. Le altre opzioni funzionano così com&#39;è.


### 3. Fornire equivalenti testuali per le immagini {#provide-text-equivalents-for-images}

Le immagini possono aiutare a migliorare la comprensione per alcuni utenti. Tuttavia, per gli utenti che utilizzano assistenti vocali, le immagini riducono l’accessibilità del modulo. Se scegli di utilizzare le immagini, fornisci descrizioni testuali per tutte le immagini.

Assicurarsi che il testo descriva l’oggetto e il relativo scopo nel modulo. Questo testo alternativo viene letto da un assistente vocale quando incontra un’immagine. Un’immagine deve sempre avere un testo alternativo specificato.

Seleziona un componente immagine e tocca ![cmppr](assets/cmppr.png). Nella barra laterale, in Proprietà, specifica il testo alternativo per un’immagine.

![Testo alternativo per un’immagine](assets/image-properties.png)

### 4. Fornire un contrasto di colore sufficiente {#provide-sufficient-color-contrast}

Il design per l’accessibilità prevede la considerazione di ulteriori linee guida per l’utilizzo del colore. Gli autori dei moduli possono utilizzare i colori per migliorare l’aspetto dei moduli, evidenziando vari componenti. Tuttavia, un uso improprio del colore può rendere un modulo difficile o impossibile da leggere da persone con capacità diverse.

Gli utenti con problemi di vista si affidano a un contrasto elevato tra il testo e lo sfondo per la lettura dei contenuti digitali. Senza un contrasto sufficiente, per alcuni utenti è difficile leggere un modulo, se non impossibile.

Si consiglia di utilizzare i colori predefiniti del font e dello sfondo, ovvero il contenuto in colore nero su sfondo bianco. Se modificate i colori predefiniti, scegliete un colore di primo piano scuro su un colore di sfondo chiaro o viceversa.

Per ulteriori informazioni sulla modifica del contrasto del colore e del tema per i moduli adattivi, consulta [Creazione di temi personalizzati per i moduli adattivi.](/help/forms/using/creating-custom-adaptive-form-themes.md)

### 5. Assicurarsi che i controlli modulo siano accessibili da tastiera {#ensure-that-form-controls-are-keyboard-accessible}

È possibile compilare completamente un modulo accessibile utilizzando solo la tastiera o un dispositivo di input equivalente. Gli utenti a mobilità ridotta o con problemi di vista possono non avere altra scelta se non utilizzare la tastiera e molti utenti che possono utilizzare un mouse, preferiscono l&#39;input da tastiera. Consentendo l’uso dei vari metodi di immissione, non solo è possibile creare moduli con accesso facilitato, ma è anche possibile creare moduli più adatti alle preferenze di tutti gli utenti.

In AEM Forms sono disponibili le seguenti scelte rapide da tastiera.

| Azione | Scelta rapida da tastiera |
|---|---|
| Spostare il cursore in avanti all’interno di un modulo | Scheda |
| Spostare il cursore all’indietro all’interno di un modulo | Maiusc+Tab |
| Passa al pannello successivo | Alt+Freccia destra |
| Passa al pannello precedente | Alt+Freccia sinistra |
| Reimpostare i dati compilati in un modulo | Alt+R |
| Inviare un modulo | Alt+S |

In Forms adattivo sono inoltre disponibili vari tasti di scelta rapida da tastiera per il componente **[!UICONTROL Selezione data]** . Per abilitare i tasti di scelta rapida, tocca il componente **[!UICONTROL Selezione data]** e tocca ![Configura](assets/configure-icon.svg) per aprire le proprietà. Nella sezione **[!UICONTROL Pattern]**, seleziona un pattern di visualizzazione utilizzando gli elenchi a discesa **[!UICONTROL Tipo]** e **[!UICONTROL Pattern]**. Salva le proprietà per abilitare l’uso dei tasti di scelta rapida per il componente **[!UICONTROL Selezione data]** .

Per il componente Selezione data in Forms adattivo sono disponibili i seguenti tasti di scelta rapida da tastiera:

| Azione | Scelta rapida da tastiera |
|---|---|
| <ul><li>Visualizza le opzioni del componente Selettore data quando l’icona del calendario è evidenziata dalla scheda</li><li>Esegui l’evento clic quando lo stato attivo della scheda evidenzia un’opzione</li> | Space o Enter |
| Nascondi le opzioni del componente Selettore data | Esc |
| <ul><li>Sposta il cursore in avanti attraverso le opzioni disponibili nel componente Selezione data .</li><li>Imposta lo stato attivo della scheda sull&#39;icona del calendario quando il campo di immissione della data è attivo</li> | Scheda |
| Sposta il cursore all’indietro tra le opzioni disponibili nel componente Selettore data | Maiusc+Tab |
| <ul><li>Visualizza le opzioni del componente Selezione data quando lo stato attivo della scheda evidenzia il campo di immissione data</li><li>Sposta il cursore verso il basso nel calendario disponibile nel componente Selettore data</li> |  Freccia giù |
| Sposta il cursore verso l’alto nel calendario disponibile nel componente Selettore data | Freccia su |
| Sposta il cursore all’indietro nel calendario disponibile nel componente Selettore data | Freccia sinistra |
| Sposta il cursore in avanti nel calendario disponibile nel componente Selettore data | Freccia destra |
| Esegui l’azione per la didascalia disponibile tra le frecce di navigazione a destra e a sinistra nel calendario | Maiusc+Freccia su |
| Esegui l&#39;azione per l&#39;icona della freccia di navigazione a destra ![freccia a destra](assets/right-navigation-icon.svg) disponibile nel calendario | Maiusc+Freccia sinistra |
| Esegui l&#39;azione per l&#39;icona della freccia di navigazione a sinistra ![freccia a sinistra](assets/left-navigation-icon.svg) disponibile nel calendario | Maiusc+Freccia destra |

## Utilizza lo strumento di accessibilità per trovare i problemi di accessibilità rimanenti

Ispettore nome e descrizione accessibile (ANDI, Accessible Name and Description Inspector) consente di identificare e correggere i problemi relativi all’accessibilità in un modulo adattivo. Per utilizzare lo strumento ANDI per trovare i problemi di accessibilità in un modulo adattivo:

1. Apri il modulo adattivo in modalità anteprima.
1. Fare clic sull&#39;icona dello strumento ANDI segnalibro. Lo strumento ANDI analizza il modulo adattivo e visualizza i problemi di accessibilità. Per informazioni dettagliate su come utilizzare lo strumento, consulta la documentazione di [ANDI](https://www.ssa.gov/accessibility/andi/help/howtouse.html).
1. Rivedi e risolvi i problemi segnalati da ANDI.