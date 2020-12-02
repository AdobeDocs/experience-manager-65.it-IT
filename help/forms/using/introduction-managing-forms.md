---
title: Introduzione alla gestione dei moduli
seo-title: Introduzione alla gestione dei moduli
description: ' AEM Forms fornisce strumenti per gestire l’Forms adattivo e le risorse correlate. Questo articolo illustra le funzionalità chiave per la gestione dei moduli e gli elementi dell''interfaccia utente.'
seo-description: ' AEM Forms fornisce strumenti per gestire l’Forms adattivo e le risorse correlate. Questo articolo illustra le funzionalità chiave per la gestione dei moduli e gli elementi dell''interfaccia utente.'
uuid: 2275a0b6-b31e-4d8e-8154-ccdfff3705aa
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager, introduction
discoiquuid: c0e4c9bb-e12a-4f9a-a8fa-1a8ad41d3995
docset: aem65
translation-type: tm+mt
source-git-commit: 46f2ae565fe4a8cfea49572eb87a489cb5d9ebd7
workflow-type: tm+mt
source-wordcount: '1593'
ht-degree: 1%

---


# Introduzione alla gestione dei moduli {#introduction-to-managing-forms}

AEM [!DNL Forms] fornisce un&#39;interfaccia utente semplificata ma potente per creare e gestire moduli, documenti, temi, lettere, frammenti di documento, dizionari di dati e risorse correlate. Consente di gestire l&#39;intero ciclo di vita di moduli, documenti e risorse correlate, dal desktop dello sviluppatore all&#39;offerta
su un server portale per gli utenti finali. È possibile utilizzare l&#39;interfaccia AEM [!DNL Forms] per:

* Accesso AEM [!DNL Forms] componenti
* Accedi alle configurazioni [!DNL Forms]

>[!NOTE]
>
>Per informazioni dettagliate su altri strumenti e opzioni AEM, vedere [Authoring](/help/sites-authoring/author.md).

## Accesso  componenti AEM Forms {#access-aem-forms-components}

Oltre alle opzioni per creare moduli, documenti e risorse correlate, AEM offre opzioni per creare siti, risorse, gestire un&#39;istanza AEM e altro ancora. Potete fare clic sul logo ![adobeexperience emanager](assets/adobeexperiencemanager.png)  Experience Manager per passare a tutti gli strumenti disponibili. Oltre ai collegamenti alle console di altri componenti, contiene anche collegamenti per AEM [!DNL Forms]. Per passare a AEM [!DNL Forms], fare clic sul logo  Experience Manager ![adobeexperience emanager](assets/adobeexperiencemanager.png) > navigazione ![bussola](assets/compass.png) > **[!UICONTROL Forms]**. Vengono visualizzati i collegamenti delle console seguenti:

* Moduli e documenti
* Temi
* Lettere
* Frammenti del documento
* Dizionari dati

   ![ AEM Forms Console](assets/aem_forms_console_new.png)

### Moduli e documenti  {#forms-documents}

Forms e documenti offre opzioni per la creazione di comunicazioni interattive, moduli adattivi, frammenti di modulo adattivi e set di moduli. Solo per AEM [!DNL Forms] su JEE, Forms &amp; Documents offre la possibilità di importare file dall&#39;archivio locale e sincronizzare AEM [!DNL Forms] risorse con Workbench.

Il pulsante Crea rappresenta il punto di partenza del processo di creazione o caricamento AEM risorsa [!DNL Forms]. Fornisce le opzioni per creare:

* **Comunicazione** interattiva: Una comunicazione interattiva è una corrispondenza digitale, un&#39;istruzione o un documento personalizzati, interattivi e compatibili con i dispositivi basati su HTML. Le comunicazioni interattive sono di natura reattiva e modificano automaticamente layout e progettazione in base al dispositivo e alle impostazioni dell&#39;utente. Per informazioni dettagliate, vedere [Panoramica sulle comunicazioni interattive](/help/forms/using/interactive-communications-overview.md)

* **Modulo adattivo:** Un modulo adattivo è un modulo coinvolgente e reattivo. È possibile creare un modulo adattivo per adattarlo dinamicamente agli input dell&#39;utente aggiungendo o rimuovendo sezioni del modulo in base alla risposta dell&#39;utente, al dispositivo o all&#39;ambiente di lavoro. L&#39;articolo [Introduzione alla creazione di moduli adattivi](../../forms/using/introduction-forms-authoring.md) contiene informazioni dettagliate sui moduli adattivi.

* **Frammento di modulo adattivo:** sebbene ogni modulo sia progettato per uno scopo specifico, nella maggior parte dei moduli sono presenti alcuni segmenti comuni, ad esempio per fornire dati personali come nome e indirizzo, dati sulla famiglia, informazioni sul reddito e così via. Potete creare una singola risorsa per tali sezioni. Questi segmenti autonomi e riutilizzabili sono denominati frammenti di modulo adattivi. Per informazioni dettagliate, vedere l&#39;articolo [frammenti di modulo adattivo](../../forms/using/adaptive-form-fragments.md).

* **Set di moduli:** Un set di moduli è un insieme di moduli HTML5 raggruppati e presentati come un singolo set di moduli agli utenti finali. Quando gli utenti finali iniziano a compilare un set di moduli, il passaggio dei moduli è semplice e diretto da un modulo all&#39;altro. Alla fine, un utente può inviare tutti i moduli, come una singola entità, con un solo clic. Per informazioni dettagliate, vedere [Modulo impostato in  AEM Forms](../../forms/using/formset-in-aem-forms.md).

* **Cartella:** AEM interfaccia  [!DNL Forms] utente utilizza le cartelle per disporre le risorse. Supporta due tipi di cartelle:

   * **Cartella generale:** queste cartelle vengono utilizzate per le risorse create all’interno AEM’interfaccia  [!DNL Forms] utente. Queste cartelle non hanno una struttura di cartelle rigida. In queste cartelle è possibile rinominare, creare sottocartelle e memorizzare moduli adattivi, comunicazioni interattive, frammenti di modulo adattivi, modelli di modulo (XDP), PDF forms, documenti e risorse correlate.
   * **cartella di Forms Workflow:le cartelle dei flussi di lavoro** Forms vengono create quando i processi di Workbench (archivi di LiveCycle) vengono migrati e sincronizzati con AEM&#39;interfaccia  [!DNL Forms] utente. Non è consentito rinominare, creare una sottocartella, creare una comunicazione interattiva, un frammento di modulo adattivo o una comunicazione interattiva. Non è inoltre consentito eliminare una cartella della versione, creare e caricare un modulo adattivo, un frammento di modulo adattivo o una comunicazione interattiva in parallelo alla cartella della versione.

   ![folder](assets/folders.png)

   **A.Cartella** generale  **B.** Forms Workflow

Il pannello Forms e Documento offre inoltre opzioni per:

* **Importare file dall&#39;archivio locale:** È possibile importare PDF forms e documenti, modelli di modulo (moduli XFA) e altre risorse (schema immagine e XML per XSD). Per istruzioni dettagliate, consultate [Importazione ed esportazione di risorse in  AEM Forms](../../forms/using/import-export-forms-templates.md).
* **Sincronizzare  risorse AEM Forms con Workbench:** è possibile utilizzare l&#39;opzione File da Workbench per sincronizzare le risorse tra &#39;interfaccia utente di AEM Forms e Workbench. Garantisce la disponibilità di tutte le risorse nell&#39;interfaccia AEM [!DNL Forms] utente e nella selezione delle risorse del repository crx di Workbench.

### Temi  {#themes}

Un tema contiene dettagli di stile per componenti e pannelli. I temi hanno un&#39;identità indipendente. È quindi possibile riutilizzare un tema su più moduli adattivi. È possibile specificare gli stili per un componente o modificare le proprietà CSS per i vari componenti utilizzati nei moduli. Gli stili includono proprietà quali i colori di sfondo, i colori dello stato, la trasparenza e le dimensioni. È possibile salvare le personalizzazioni in un tema e trascinarle sui componenti del modulo come un predefinito. Quando si aggiunge il tema al modulo, lo stile specificato si riflette sui componenti corrispondenti del modulo. Con AEM 6.2 [!DNL Forms] è possibile creare temi e applicarli ai moduli.

Per informazioni sulla creazione e l&#39;uso dei temi, vedere [Temi in  AEM Forms](../../forms/using/themes.md).

### Lettere  {#letters}

Una lettera [!DNL Forms] AEM è una corrispondenza sicura, personalizzata e interattiva. È possibile utilizzare AEM [!DNL Forms] per assemblare rapidamente lettere (dette anche corrispondenze) sia da contenuti pre-approvati che personalizzati in un processo semplificato.

Per informazioni sulla creazione e l&#39;uso delle lettere, vedere [Crea lettera](../../forms/using/create-letter.md).

### Frammenti del documento {#document-fragments}

I frammenti di documento sono parti o componenti riutilizzabili di una corrispondenza mediante le quali è possibile comporre le lettere. I frammenti di documento sono di tipo testo, elenco, condizione e frammento di layout. Per informazioni sulla creazione e l&#39;uso dei frammenti di documento, vedere [creazione di frammenti di documento](/help/forms/using/document-fragments.md).

### Dizionari dati {#data-dictionaries}

In genere, gli utenti aziendali non necessitano di conoscenze sulle rappresentazioni di metadati come XSD (schema XML) e le classi Java. Tuttavia, in genere richiedono l&#39;accesso a queste strutture di dati e attributi per creare soluzioni. AEM [!DNL Forms] utilizza un dizionario dati che consente agli utenti aziendali di utilizzare informazioni provenienti da origini dati back-end senza conoscere i dettagli tecnici relativi ai modelli di dati sottostanti.

Per informazioni sulla creazione e l&#39;uso dei dizionari di dati, vedere Creazione di [articolo del dizionario di dati](../../forms/using/data-dictionary.md)

## Accesso alle AEM [!DNL Forms] configurazioni {#accessing-aem-forms-configurations}

AEM pannello degli strumenti contiene strumenti per vari componenti. Per passare  strumenti specifici di AEM Forms, fare clic sul logo  Experience Manager ![adobeexperience emanager](assets/adobeexperiencemanager.png) > strumenti ![martello](assets/hammer.png) > **[!UICONTROL Forms]**. Vengono visualizzati gli strumenti per eseguire le seguenti funzioni:

* **Configura cartella esaminata:** un amministratore può configurare una cartella di rete, nota come cartella esaminata, in modo che quando un utente inserisce un file (ad esempio un file PDF) nella cartella esaminata, venga avviata un’operazione preconfigurata e il file venga manipolato. Per informazioni dettagliate, vedere [Creare e configurare una cartella controllata](/help/forms/using/creating-configure-watched-folder.md).
* **Configura Forms App Offline Service:** Il servizio  [!DNL Forms] app AEM offline memorizza nella cache i percorsi o gli URL delle risorse utilizzate in un modulo. La memorizzazione nella cache di percorsi o URL delle risorse utilizzate in un modulo migliora le prestazioni lato server. Per configurare il componente offline lato server dell&#39;app  AEM Forms, vedi [Utilizzo della modalità offline](/help/forms/using/work-offline-mode.md).

   ![ strumenti AEM Forms](assets/aem_forms_tools_new.png)

* **Configurare PDF Generator:** un amministratore può configurare AEM impostazioni di  [!DNL Forms] PDF Generator, aggiungere account utente e importare o esportare la configurazione in PDF Generator.
* **Pubblica risorse di gestione della corrispondenza:** AEM  [!DNL Forms] consente di pubblicare contemporaneamente tutte le lettere, i frammenti di documento e i dizionari di dati e le relative dipendenze da un’istanza di autore. Le risorse pubblicate includono tutte le risorse Gestione corrispondenza e le relative dipendenze. Per informazioni dettagliate, vedere [Pubblicazione e annullamento della pubblicazione di moduli e documenti](../../forms/using/publishing-unpublishing-forms.md#publishallthecorrespondencemanagementassets).
* **Esporta risorse di gestione della corrispondenza:** puoi scaricare tutte le risorse di gestione della corrispondenza e le relative dipendenze come pacchetto da un’ [!DNL Forms] istanza AEM. Per i passaggi dettagliati, consultate [Importazione ed esportazione di risorse in  AEM Forms](../../forms/using/import-export-forms-templates.md#importandexportassetsincorrespondencemanagement)

## Elementi comuni dell&#39;interfaccia utente {#commonelements}

* **Barra a sinistra:** potete fare clic sull&#39;icona della barra a sinistra  ![](assets/railleftpng.png) a sinistra per visualizzare le funzionalità Timeline e Riferimenti di AEM  [!DNL Forms].

   * **Timeline:** potete aggiungere e visualizzare commenti su una risorsa disponibile per la revisione nella timeline. Per istruzioni dettagliate, vedere [Creazione e gestione di revisioni per le risorse nei moduli](../../forms/using/create-reviews-forms.md).
   * **Riferimenti:** una  [!DNL Forms] risorsa AEM può essere utilizzata in più  [!DNL Forms] risorse AEM. Ad esempio, un frammento di documento può essere utilizzato in più lettere. I riferimenti sono un elenco di risorse (altri moduli o risorse) in cui è utilizzata la risorsa selezionata e un elenco di altre risorse in uso.

* **Breadcrumb:** Una Breadcrumb rappresenta il titolo della console o della cartella corrente. Potete fare clic sull’opzione Breadcrumb per spostarvi tra il livello di cartelle più alto nella gerarchia.
* **Vista Switcher:** Puoi fare clic sull’icona Visualizza commutatore  ![](assets/viewlist.png) visualizzatore o  ![](assets/viewcard.png) visualizzatore per passare rapidamente dalla visualizzazione a elenco a quella a schede. Per ulteriori informazioni sui componenti comuni dell&#39;interfaccia utente, vedere [Authoring](/help/sites-authoring/author.md).
* **Ricerca:** L’opzione di ricerca  ![](assets/search.png) consente di trovare e passare rapidamente ai contenuti e agli strumenti necessari. Digitate il nome del contenuto o della funzionalità del prodotto e selezionate tra i suggerimenti, ad esempio &quot;Documenti&quot; per trovare e passare rapidamente alla console **[!UICONTROL Forms &amp; Documents]** o Frammenti documento. Per ulteriori informazioni sulla ricerca, consultate AEM 6.2 [search](/help/sites-authoring/search.md) article

* **Barra degli strumenti** Azioni: Quando si seleziona una risorsa, la barra degli strumenti Azioni è visualizzata sopra l’elenco delle risorse. Contiene tutti gli strumenti di gestione per la risorsa selezionata. Passate il puntatore del mouse sull&#39;icona di uno strumento per visualizzare la descrizione delle sue funzionalità

>[!NOTE]
>
>Quando un utente esegue una ricerca in una qualsiasi console di Forms e documenti, la barra laterale contiene solo **Filtri e opzioni**. È possibile utilizzare Filtri e opzioni per eseguire ricerche avanzate.

* **Barra degli strumenti** Azioni: Quando si seleziona una risorsa, la barra degli strumenti Azioni è visualizzata sopra l’elenco delle risorse. Contiene tutti gli strumenti di gestione per la risorsa selezionata. Passate il puntatore del mouse sull&#39;icona di uno strumento per visualizzare la descrizione delle sue funzionalità

   ![Barra degli strumenti delle azioni per un modulo adattivo](assets/action_toolbar_new.png)

   Barra degli strumenti delle azioni per un modulo adattivo
