---
title: Introduzione alla gestione dei moduli
seo-title: Introduction to managing forms
description: AEM Forms fornisce gli strumenti per gestire il Forms adattivo e le relative risorse. Questo articolo ti introduce alle funzionalità chiave di gestione dei moduli e agli elementi dell’interfaccia utente.
seo-description: AEM Forms provides tools to manage Adaptive Forms and related assets. This article introduces you to the key forms management capabilities and user interface elements.
uuid: 2275a0b6-b31e-4d8e-8154-ccdfff3705aa
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager, introduction
discoiquuid: c0e4c9bb-e12a-4f9a-a8fa-1a8ad41d3995
docset: aem65
exl-id: 3e063456-7f96-483d-86a3-6a414746db8a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1564'
ht-degree: 1%

---

# Introduzione alla gestione dei moduli {#introduction-to-managing-forms}

AEM [!DNL Forms] fornisce un’interfaccia utente semplificata ma potente per creare e gestire moduli, documenti, temi, lettere, frammenti di documento, dizionari di dati e risorse correlate. Consente di gestire l’intero ciclo di vita di moduli, documenti e risorse correlate, dal desktop di uno sviluppatore all’offerta su un server portale per gli utenti finali. Puoi utilizzare il AEM [!DNL Forms] interfaccia utente a:

* AEM di accesso [!DNL Forms] componenti
* AEM di accesso [!DNL Forms] configurazioni

>[!NOTE]
>
>Per informazioni dettagliate su altri strumenti e opzioni di AEM, vedi [Authoring](/help/sites-authoring/author.md).

## Accedere ai componenti di AEM Forms {#access-aem-forms-components}

Oltre alle opzioni per la creazione di moduli, documenti e risorse correlate, AEM fornisce opzioni per la creazione di siti, risorse, la gestione di un’istanza AEM e altro ancora. Puoi fare clic su ![adobeexperiencemanager](assets/adobeexperiencemanager.png) Logo di Experience Manager per accedere a tutti gli strumenti disponibili. Oltre ai collegamenti alle console di altri componenti, contiene anche collegamenti per AEM [!DNL Forms]. Per passare a AEM [!DNL Forms], fai clic sul logo dell’Experience Manager ![adobeexperiencemanager](assets/adobeexperiencemanager.png) > navigazione ![bussola](assets/compass.png) > **[!UICONTROL Forms]**. Vengono visualizzati i collegamenti alle console seguenti:

* Moduli e documenti
* Temi
* Lettere
* Frammenti del documento
* Dizionari dati

   ![Console AEM Forms](assets/aem_forms_console_new.png)

### Moduli e documenti  {#forms-documents}

Forms &amp; Documents fornisce opzioni per creare una comunicazione interattiva, un modulo adattivo, un frammento di modulo adattivo e un set di moduli. Solo per AEM [!DNL Forms] in JEE, Forms &amp; Documents offre un’opzione per importare file dall’archiviazione locale e AEM di sincronizzazione [!DNL Forms] risorse con Workbench.

Il pulsante crea è il punto di partenza del processo di creazione o caricamento di AEM [!DNL Forms] risorsa. Fornisce le opzioni per creare:

* **Comunicazione interattiva**: Una comunicazione interattiva è una corrispondenza digitale, un&#39;istruzione o un documento personalizzati, interattivi e compatibili con i dispositivi basati su HTML. Le comunicazioni interattive sono adattabili in natura e cambiano layout e design automaticamente in base al dispositivo e alle impostazioni dell&#39;utente. Per informazioni dettagliate, consulta [Panoramica delle comunicazioni interattive](/help/forms/using/interactive-communications-overview.md)

* **Modulo adattivo:** Un modulo adattivo è un modulo coinvolgente e reattivo. È possibile creare un modulo adattivo per adattarsi dinamicamente agli input degli utenti aggiungendo o rimuovendo sezioni di modulo in base alla risposta dell’utente, al dispositivo o all’ambiente di lavoro. La [Introduzione alla creazione di moduli adattivi](../../forms/using/introduction-forms-authoring.md) questo articolo fornisce informazioni dettagliate sui moduli adattivi.

* **Frammento di modulo adattivo:** Sebbene ogni modulo sia progettato per uno scopo specifico, la maggior parte dei moduli contiene alcuni segmenti comuni, ad esempio per fornire dati personali come nome e indirizzo, dettagli sulla famiglia, dettagli sul reddito e così via. Puoi creare una singola risorsa per tali sezioni. Questi segmenti riutilizzabili e autonomi sono denominati frammenti di modulo adattivi. Per informazioni dettagliate, consulta [frammenti di modulo adattivi](../../forms/using/adaptive-form-fragments.md) articolo.

* **Set di moduli:** Un set di moduli è una raccolta di moduli di HTML5 raggruppati e presentati agli utenti finali come un unico set di moduli. Quando gli utenti finali iniziano a compilare un set di moduli, i moduli vengono spostati da un modulo all’altro senza problemi. Alla fine, un utente può inviare tutti i moduli, come un’unica entità, con un solo clic. Per informazioni dettagliate, consulta [Set di moduli in AEM Forms](../../forms/using/formset-in-aem-forms.md).

* **Cartella:** AEM [!DNL Forms] l’interfaccia utente utilizza le cartelle per disporre le risorse. Supporta due tipi di cartelle:

   * **Cartella generale:** Queste cartelle vengono utilizzate per le risorse create in AEM [!DNL Forms] interfaccia utente. Queste cartelle non hanno una struttura di cartelle rigida. In queste cartelle è possibile rinominare, creare sottocartelle e memorizzare moduli adattivi, comunicazioni interattive, frammenti di moduli adattivi, modelli di modulo (XDP), PDF forms, documenti e risorse correlate.
   * **Cartella Forms Workflow:** Le cartelle del flusso di lavoro di Forms vengono create quando i processi di Workbench (archivi di LiveCycle) vengono migrati e sincronizzati con AEM [!DNL Forms] interfaccia utente. Non è consentito rinominare, creare una sottocartella, creare una comunicazione interattiva, un frammento di modulo adattivo o una comunicazione interattiva. Non è inoltre consentito eliminare una cartella di versione o creare e caricare un modulo adattivo, un frammento di modulo adattivo o una comunicazione interattiva in parallelo alla cartella della versione.

   ![cartelle](assets/folders.png)

   **A.** Cartella generale **B.** Cartella Forms Workflow

Il pannello Forms e Documento fornisce inoltre le opzioni per:

* **Importa file dall&#39;archiviazione locale:** È possibile importare PDF forms e documenti, modelli di modulo (moduli XFA) e altre risorse (schema immagine e XML per XSD). Per istruzioni dettagliate, consulta [Importazione ed esportazione di risorse in AEM Forms](../../forms/using/import-export-forms-templates.md).
* **Sincronizza le risorse AEM Forms con Workbench:** È possibile utilizzare l’opzione File da Workbench per sincronizzare le risorse tra l’interfaccia utente di AEM Forms e Workbench. Garantisce la disponibilità di tutte le risorse in AEM [!DNL Forms] l’interfaccia utente e la selezione delle risorse dell’archivio crx di Workbench.

### Temi  {#themes}

Un tema contiene dettagli di stile per componenti e pannelli. I temi hanno un&#39;identità indipendente. È quindi possibile riutilizzare un tema in più moduli adattivi. È possibile specificare gli stili per un componente o modificare le proprietà CSS per vari componenti utilizzati nei moduli. Gli stili includono proprietà quali colori di sfondo, colori dello stato, trasparenza e dimensioni. È possibile salvare le personalizzazioni in un tema e trascinarle sui componenti del modulo come predefinito. Quando si aggiunge un tema al modulo, lo stile specificato si riflette sui componenti corrispondenti del modulo. Con AEM 6.2 [!DNL Forms], è possibile creare temi e applicarli ai moduli.

Per informazioni sulla creazione e l&#39;utilizzo dei temi, vedi [Temi in AEM Forms](../../forms/using/themes.md).

### Lettere  {#letters}

Un AEM [!DNL Forms] La lettera è una corrispondenza sicura, personalizzata e interattiva. Puoi utilizzare AEM [!DNL Forms] per assemblare rapidamente le lettere (dette anche corrispondenze) da contenuti pre-approvati e personalizzati in un processo semplificato.

Per informazioni sulla creazione e l&#39;utilizzo delle lettere, vedere [Crea lettera](../../forms/using/create-letter.md).

### Frammenti del documento {#document-fragments}

I frammenti di documento sono parti o componenti riutilizzabili di una corrispondenza che consente di comporre lettere. I frammenti di documento sono di tipo testo, elenco, condizione e frammento di layout. Per informazioni sulla creazione e l&#39;utilizzo dei frammenti di documento, vedere [creazione di frammenti di documento](/help/forms/using/document-fragments.md).

### Dizionari dati {#data-dictionaries}

In genere, gli utenti aziendali non richiedono la conoscenza delle rappresentazioni dei metadati come XSD (schema XML) e le classi Java. Tuttavia, in genere richiedono l&#39;accesso a queste strutture di dati e attributi per creare soluzioni. AEM [!DNL Forms] utilizza un dizionario dati che consente agli utenti aziendali di utilizzare informazioni provenienti da origini dati back-end senza conoscere i dettagli tecnici relativi ai modelli di dati sottostanti.

Per informazioni sulla creazione e l’utilizzo dei dizionari dati, vedere creazione [articolo del dizionario dati](../../forms/using/data-dictionary.md)

## Accesso AEM [!DNL Forms] Configurazioni {#accessing-aem-forms-configurations}

AEM pannello strumenti contiene gli strumenti per vari componenti. Per passare agli strumenti specifici di AEM Forms, fai clic sul logo di Experience Manager ![adobeexperiencemanager](assets/adobeexperiencemanager.png) > strumenti ![martello](assets/hammer.png) > **[!UICONTROL Forms]**. Vengono visualizzati gli strumenti per eseguire le seguenti funzioni:

* **Configura cartella osservata:** Un amministratore può configurare una cartella di rete, nota come cartella controllata, in modo che quando un utente inserisce un file (ad esempio un file PDF) nella cartella controllata, venga avviata un’operazione preconfigurata e il file venga manipolato. Per informazioni dettagliate, consulta [Creare e configurare una cartella controllata](/help/forms/using/creating-configure-watched-folder.md).
* **Configura il servizio offline dell&#39;app Forms:** AEM [!DNL Forms] il servizio app offline memorizza in cache i percorsi o gli URL delle risorse utilizzate in un modulo. La memorizzazione nella cache di percorsi o URL delle risorse utilizzate in un modulo migliora le prestazioni lato server. Per configurare il componente offline lato server dell&#39;app AEM Forms, vedi [Utilizzo della modalità offline](/help/forms/using/work-offline-mode.md).

   ![Strumenti AEM Forms](assets/aem_forms_tools_new.png)

* **Configura PDF Generator:** Un amministratore può configurare AEM [!DNL Forms] Impostazioni di PDF Generator, aggiungere account utente e importare o esportare la configurazione in PDF Generator.
* **Pubblicare Risorse Di Gestione Corrispondenza:** AEM [!DNL Forms] consente di pubblicare contemporaneamente tutte le lettere, i frammenti di documento e i dizionari di dati e le relative dipendenze da un’istanza di authoring. Le risorse pubblicate includono tutte le risorse di Gestione Corrispondenza e le relative dipendenze. Per informazioni dettagliate, consulta [Pubblicazione e annullamento della pubblicazione di moduli e documenti](../../forms/using/publishing-unpublishing-forms.md#publishallthecorrespondencemanagementassets).
* **Esporta risorse di gestione della corrispondenza:** Puoi scaricare come pacchetto tutte le risorse di Gestione Corrispondenza e le relative dipendenze da un AEM [!DNL Forms] istanza. Per i passaggi dettagliati vedi [Importazione ed esportazione di risorse in AEM Forms](../../forms/using/import-export-forms-templates.md#importandexportassetsincorrespondencemanagement)

## Elementi comuni dell’interfaccia utente {#commonelements}

* **Barra a sinistra:** Fai clic sull’icona della barra a sinistra ![ringhiera](assets/railleftpng.png) per visualizzare le funzionalità Timeline e Riferimenti di AEM [!DNL Forms].

   * **Timeline:** Puoi aggiungere e visualizzare i commenti a una risorsa disponibile per la revisione nella timeline. Per istruzioni dettagliate, vedi [Creazione e gestione di revisioni per le risorse nei moduli](../../forms/using/create-reviews-forms.md).
   * **Riferimenti:** Un AEM [!DNL Forms] la risorsa può essere utilizzata in più AEM [!DNL Forms] risorse. Ad esempio, un frammento di documento può essere utilizzato in più lettere. I riferimenti sono un elenco di risorse (altri moduli o risorse) in cui viene utilizzata la risorsa selezionata e anche l’elenco delle altre risorse in uso.

* **Breadcrumb:** Una Breadcrumb rappresenta il titolo della console o della cartella corrente. È possibile fare clic sull’opzione Breadcrumb per spostarsi tra i livelli di cartelle più alti nella gerarchia.
* **Cambia visualizzazione:** Fai clic sull’icona Cambia visualizzazione ![elenco viste](assets/viewlist.png) o ![scheda](assets/viewcard.png) per passare rapidamente dalla visualizzazione a elenco a quella a schede. Per ulteriori informazioni sui componenti comuni dell’interfaccia utente, consulta [Authoring](/help/sites-authoring/author.md).
* **Ricerca:** Opzione di ricerca ![ricerca](assets/search.png) fornisce la possibilità di trovare e passare rapidamente ai contenuti e strumenti necessari. Digita il nome del contenuto o della funzionalità del prodotto e seleziona dai suggerimenti, ad esempio, digita &quot;Documents&quot; per trovare e navigare rapidamente in **[!UICONTROL Forms e documenti]** o la console Frammenti documento. Per ulteriori informazioni sulla ricerca, consulta AEM 6.2 [ricerca](/help/sites-authoring/search.md) articolo

* **Barra delle azioni**: Quando selezioni una risorsa, la barra delle azioni viene visualizzata sopra l’elenco delle risorse. Contiene tutti gli strumenti di gestione per la risorsa selezionata. Passa il puntatore del mouse su un&#39;icona dello strumento per visualizzare la descrizione che ne descrive le funzionalità

>[!NOTE]
>
>Quando un utente esegue una ricerca in una qualsiasi console di Forms e documenti, la barra a sinistra contiene solo **Filtri e opzioni**. Puoi utilizzare Filtri e opzioni per eseguire ricerche avanzate.

* **Barra delle azioni**: Quando selezioni una risorsa, la barra delle azioni viene visualizzata sopra l’elenco delle risorse. Contiene tutti gli strumenti di gestione per la risorsa selezionata. Passa il puntatore del mouse su un&#39;icona dello strumento per visualizzare la descrizione che ne descrive le funzionalità

   ![Barra delle azioni per un modulo adattivo](assets/action_toolbar_new.png)

   Barra delle azioni per un modulo adattivo
