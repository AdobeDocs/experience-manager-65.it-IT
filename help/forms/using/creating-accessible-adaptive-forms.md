---
title: Creazione di moduli adattivi con accesso facilitato
seo-title: Creazione di moduli adattivi con accesso facilitato
description: ' AEM Forms fornisce strumenti e consente di creare moduli adattivi con accesso facilitato e rispetta gli standard di accessibilità.'
seo-description: ' AEM Forms fornisce strumenti e consente di creare moduli adattivi con accesso facilitato e rispetta gli standard di accessibilità.'
uuid: 6472bc2d-47ca-4883-88b7-5de0b758fd00
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 1e95c66b-d132-4c44-a1dc-31fd09af8113
docset: aem65
translation-type: tm+mt
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '1792'
ht-degree: 0%

---


# Creazione di moduli adattivi con accesso facilitato{#creating-accessible-adaptive-forms}

## Introduzione {#introduction}

Un modulo con accesso facilitato è un modulo utilizzabile da tutti, compresi gli utenti con esigenze particolari. L&#39;Forms adattivo include una serie di funzionalità che migliorano l&#39;usabilità per gli utenti con capacità diverse. La creazione dell&#39;accessibilità nei moduli adattivi non solo consente al pubblico di accedere al contenuto nel modo più ampio possibile, ma anche quando si forniscono documenti in aree geografiche in cui è richiesta la conformità agli standard di accessibilità.  Guida di AEM Forms agli sviluppatori di moduli conformi agli standard di accessibilità.

Durante la creazione di un modulo adattivo, per creare un modulo adattivo con accesso facilitato l’autore deve tenere conto dei seguenti punti:

* Verificare il modulo con lo strumento di verifica dell&#39;accessibilità di Ispettore nome e descrizione accessibile (ANDI)
* Fornire etichette corrette per i controlli modulo
* Specifica equivalenti di testo per le immagini
* Fornire un contrasto di colore sufficiente
* Verificare che i controlli modulo siano accessibili tramite tastiera

## Prerequisito

Per creare un modulo adattivo accessibile è necessario uno strumento di accesso facilitato, ad esempio **Nome e finestra di ispezione descrizione accessibile (ANDI)** e un tema per modulo adattivo **sviluppato per risolvere problemi correlati all&#39;accessibilità**.

### Download e installazione dello strumento di test dell&#39;accessibilità

Lo strumento Andi (Accessible Name and Description Inspector) consente di identificare e risolvere i problemi di conformità relativi all’accessibilità nel contenuto Web. È lo strumento consigliato in Trusted Tester v5 linee guida del Dipartimento della Sicurezza Interna. È stato sviluppato dal Dipartimento di Sicurezza Sociale &#x200B; Stati Uniti per verificare la conformità Sezione 508 dei contenuti web. Lo strumento:

* Consente di rilevare &#x200B; problemi di accessibilità in una pagina Web
* Fornisce suggerimenti per migliorare l&#39;accessibilità &#x200B;
* Rileva problemi di accessibilità e contrasto dei colori della tastiera
* Identifica chiaramente il contenuto dell&#39;assistente vocale in conformità con gli standard

ANDI funziona con tutti i principali browser Internet. Per istruzioni dettagliate su come configurare e utilizzare lo strumento, vedere la [documentazione ANDI](https://www.ssa.gov/accessibility/andi/help/install.html).

### Scaricare e installare il tema Ultramarine-Accessible

Il tema Ultramarine-Accessible è un tema di riferimento. Questo documento illustra come correggere il contrasto del colore e altri problemi di accessibilità in un modulo adattivo.  Adobe consiglia di creare un tema personalizzato per l&#39;ambiente di produzione in base agli stili approvati dall&#39;organizzazione. Per caricare il tema nell’istanza AEM, effettuate le seguenti operazioni:

1. Scaricate il pacchetto di temi.
1. Andate a **[!UICONTROL Experience Manager]** > **[!UICONTROL Navigazione]** ![Navigazione](assets/Smock_Compass_18_N.svg) > **[!UICONTROL Forms]** nell&#39;istanza AEM.
1. Toccate **[!UICONTROL Crea]** > **[!UICONTROL Caricamento file]**. Selezionate e caricate il file x Ultramarine-Accessible-Theme.zip. Il tema viene caricato nell’istanza AEM.

## Rendere un modulo adattivo accessibile

È necessario concentrarsi su quattro aspetti chiave: navigazione tramite tastiera, contrasto del colore, testo alternativo significativo per le immagini ed etichette appropriate per i controlli dei moduli per rendere accessibile un modulo adattivo. Per rendere accessibili i moduli adattivi esistenti, effettuate le seguenti operazioni:

### 1. Applicazione di un tema accessibile ed esecuzione di correzioni aggiuntive

Applicate il tema Accessibile da Ultramarine al modulo adattivo esistente. Per applicare il tema:

1. Aprire il modulo adattivo per la modifica.
1. Selezionate un componente e toccate l’icona principale. Nel menu di scelta rapida, toccate **[!UICONTROL Contenitore modulo adattivo]**, quindi toccate l&#39;icona di configurazione.
1. Selezionate il tema accessibile da Ultramarine nel browser delle proprietà e toccate l&#39;icona **[!UICONTROL Save]**.
1. Aggiorna la finestra del browser. Il tema viene applicato al modulo adattivo.

Dopo aver applicato un tema accessibile, eseguite le seguenti correzioni aggiuntive elencate. I problemi risolti sono in aggiunta ai problemi di accessibilità risolti nel tema accessibile:

1. Aggiungete un testo alternativo significativo per l&#39;immagine del logo nel modulo adattivo.

   Fornire un testo alternativo significativo per le immagini nei componenti di intestazione e piè di pagina del modello di modulo adattivo. Quando si fissa il modello e lo si utilizza per creare un modulo adattivo, i moduli adattivi ereditano tutte le correzioni relative all&#39;accessibilità applicate all&#39;intestazione e al piè di pagina del modello.  Per un modulo adattivo esistente, apportare modifiche a livello di modulo adattivo. Le modifiche apportate a un modello di modulo adattivo non passano automaticamente a un modulo adattivo esistente.

1. Aggiungete al modulo adattivo un componente di intestazione contenente il nome del modulo. Se la struttura del modulo specifica il nome di una società, aggiungere anche un componente di intestazione separato per il nome della società.

   La maggior parte degli strumenti di accessibilità informa gli utenti della gerarchia dei contenuti per aiutarli a comprendere la struttura della pagina Web. Impostare livelli di intestazione diversi per il nome dell’organizzazione e il testo del nome del modulo nel modulo adattivo, in modo da fornire una struttura gerarchica a tale testo. Inoltre, usate un componente Testo prima di ciascun pannello e sezione con un livello di intestazione appropriato per creare una gerarchia.

   ![Come applicare uno stile di intestazione](assets/apply-style.gif)

1. Modificare il colore di sfondo del piè di pagina per utilizzare il contrasto appropriato in conformità agli standard di accessibilità per migliorare la visibilità e la leggibilità del testo. È possibile utilizzare ANDI per individuare problemi di contrasto dei colori nel modulo. Inoltre, non utilizzate caratteri molto piccoli. I font di piccole dimensioni sono difficili da leggere.

1. Sostituite i componenti switch e immagine selezionati nel modulo adattivo esistente con il componente selezionato (radio).

1. Sostituite il componente stepper numerico nel modulo adattivo esistente con un componente casella numerica.

1. Sostituire il campo di immissione data con il campo di selezione data.

1. Impostare pattern di visualizzazione, convalida e modifica per il componente di selezione della data. Inoltre, impostare un messaggio di errore di convalida personalizzato. Ad esempio, hai specificato una data non valida. Il formato corretto della data è AAAA-MM-GG.

1. Imposta testo di accessibilità personalizzato per il componente del selettore data. Ad esempio, Immettete la data di nascita. Gli assistenti vocali leggono questi testi di accessibilità personalizzati.

1. Per i componenti per moduli adattivi, utilizzate una descrizione breve invece di una descrizione lunga. Una lunga descrizione aggiunge il pulsante della guida. Verificare che nel modulo adattivo non sia presente alcun pulsante di Aiuto.

1. Aggiungere testo di accesso facilitato personalizzato a tutte le celle di sola lettura delle tabelle. Inoltre, disabilitare tutte le celle di sola lettura delle tabelle.

1. Rimuovere eventuali campi firma script nel modulo adattivo. Configurare il modulo adattivo per utilizzare  Adobe Sign per un&#39;esperienza di firma digitale senza soluzione di continuità.

### 2. Specificare le etichette corrette per i controlli modulo {#provide-proper-labels-for-form-controls}

L’etichetta o il titolo di un componente identifica il contenuto rappresentato dal componente modulo. Ad esempio, il testo &quot;Nome&quot; indica agli utenti che devono immettere il proprio nome in un campo di testo. Per essere accessibile dagli assistenti vocali, l&#39;etichetta è associata a un componente modulo a livello di programmazione. In alternativa, il controllo modulo è configurato con ulteriori informazioni di accesso facilitato.

L&#39;etichetta percepita dagli assistenti vocali non deve necessariamente corrispondere alla didascalia visiva. In alcuni casi, potrebbe essere necessario essere più specifici sullo scopo del controllo. Per ciascun oggetto campo di un modulo, le opzioni di accessibilità possono essere utilizzate per specificare ciò che l&#39;assistente vocale annuncia per identificare il campo modulo specifico.

Per utilizzare l&#39;opzione Accessibilità, procedere come segue:

1. Selezionate un componente e toccate ![cmppr](assets/cmppr.png).
1. Fare clic su **[!UICONTROL Accessibilità]** nella barra laterale per scegliere l&#39;opzione di accessibilità desiderata.

### Opzioni di accessibilità nei componenti modulo {#accessibility-options-in-form-components}

![Opzioni di accessibilità nei componenti modulo](assets/accessibility-options.png)

**Gli autori di** TextForm personalizzati forniscono il contenuto dell&#39;opzione di accesso facilitato Campo di testo personalizzato. La tecnologia di supporto, ad esempio gli assistenti vocali, utilizza questo testo personalizzato. L’utilizzo dell’impostazione Titolo è l’opzione migliore nella maggior parte degli scenari. Valutare la possibilità di creare testo personalizzato dell&#39;Reader dello schermo solo quando si utilizza il Titolo o se non è possibile inserire una breve descrizione.

**Breve** descrizionePer la maggior parte dei componenti, la breve descrizione viene visualizzata in fase di esecuzione quando l&#39;utente passa il puntatore sul componente. Potete impostare questa opzione nel campo della descrizione breve, sotto l&#39;opzione di contenuto della guida.

**** Titolo: utilizzate questa opzione per consentire a  AEM Forms di utilizzare l&#39;etichetta visiva associata al campo modulo come testo dell&#39;assistente vocale.

**** Nome: è possibile specificare un valore nel campo Nome della scheda Binding. Il nome non può contenere spazi.

**** Nessuno: se si seleziona Nessuno, l&#39;oggetto modulo non ha un nome nel modulo pubblicato. Nessuna impostazione consigliata per i controlli modulo.

>[!NOTE]
>
>* I pulsanti di scelta e le caselle di controllo possono avere solo due opzioni per l&#39;accessibilità, ovvero Testo personalizzato e Titolo.
>* Per i moduli adattivi basati su XFA, l&#39;opzione di accessibilità è ereditata dalle opzioni di accessibilità impostate in XDP. Le descrizioni comandi di XDP sono mappate sulla descrizione breve e la didascalia sono mappate su Titolo. Le altre opzioni funzionano allo stesso modo.


### 3. Specifica equivalenti di testo per le immagini {#provide-text-equivalents-for-images}

Le immagini possono aiutare a migliorare la comprensione per alcuni utenti. Tuttavia, per gli utenti che utilizzano gli assistenti vocali, le immagini riducono l&#39;accessibilità del modulo. Se scegliete di utilizzare le immagini, fornite descrizioni testuali per tutte le immagini.

Assicurarsi che il testo descriva l&#39;oggetto e la sua funzione nel modulo. Un assistente vocale legge questo testo alternativo quando incontra un&#39;immagine. Un&#39;immagine deve sempre avere un testo alternativo specificato.

Selezionate un componente immagine e toccate ![cmppr](assets/cmppr.png). Nella barra laterale, in Proprietà, specificate il testo alternativo per un’immagine.

![Testo alternativo per un’immagine](assets/image-properties.png)

### 4. Contrasto colore sufficiente {#provide-sufficient-color-contrast}

La progettazione dell&#39;accessibilità prevede la considerazione di ulteriori linee guida per l&#39;utilizzo del colore. Gli autori dei moduli possono utilizzare i colori per migliorare l&#39;aspetto dei moduli, evidenziando diversi componenti. Tuttavia, un uso improprio del colore può rendere un modulo difficile o impossibile da leggere da persone con capacità diverse.

Gli utenti con problemi di vista si affidano a un contrasto elevato tra il testo e lo sfondo per la lettura di contenuti digitali. Senza un contrasto sufficiente, un modulo può diventare difficile, se non impossibile, da leggere per alcuni utenti.

Si consiglia di utilizzare i colori di font e sfondo predefiniti, ossia il contenuto in nero su uno sfondo bianco. Se modificate i colori predefiniti, scegliete un colore di primo piano scuro su un colore di sfondo chiaro o viceversa.

Per ulteriori informazioni sulla modifica del contrasto dei colori e del tema per i moduli adattivi, vedere [Creazione di temi personalizzati per i moduli adattivi.](/help/forms/using/creating-custom-adaptive-form-themes.md)

### 5. Verificare che i controlli modulo siano accessibili tramite tastiera {#ensure-that-form-controls-are-keyboard-accessible}

Un modulo con accesso facilitato può essere compilato completamente utilizzando solo la tastiera o un dispositivo di input equivalente. Gli utenti con mobilità ridotta o problemi di vista possono non avere altra scelta se non utilizzare la tastiera e molti utenti che possono utilizzare il mouse preferiscono l&#39;input della tastiera. Consentendo l&#39;uso dei vari metodi di immissione, non solo si creano moduli con accesso facilitato, ma si creano anche moduli più adatti alle preferenze di tutti gli utenti.

In  AEM Forms sono disponibili le seguenti scelte rapide da tastiera.

| Azione | Scelte rapide da tastiera |
|---|---|
| Spostare il cursore in avanti all&#39;interno di un modulo | Scheda |
| Spostare il cursore all&#39;indietro all&#39;interno di un modulo | Maiusc+Tab |
| Passa al pannello successivo | Alt+Freccia destra |
| Passa al pannello precedente | Alt+Freccia sinistra |
| Reimpostare i dati compilati in un modulo | Alt+R |
| Invio di un modulo | Alt+S |

## Utilizzate lo strumento di accessibilità per individuare i problemi di accessibilità rimanenti

Ispettore nome e descrizione accessibile (ANDI) consente di identificare e risolvere i problemi di conformità relativi all’accessibilità in un modulo adattivo. Per utilizzare lo strumento ANDI per individuare i problemi di accessibilità in un modulo adattivo:

1. Aprite il modulo adattivo in modalità di anteprima.
1. Fare clic sull&#39;icona dello strumento ANDI con segnalibro. Lo strumento ANDI analizza il modulo adattivo e visualizza i problemi di accessibilità. Per informazioni dettagliate sull&#39;utilizzo dello strumento, consultare la [documentazione ANDI](https://www.ssa.gov/accessibility/andi/help/howtouse.html).
1. Esaminare e risolvere i problemi segnalati da ANDI.