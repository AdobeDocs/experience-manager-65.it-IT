---
title: Utilizzo di risorse 3D in elementi multimediali dinamici
seo-title: Utilizzo di risorse 3D in elementi multimediali dinamici
description: Scopri come lavorare con risorse 3D in Dynamic Media
seo-description: Scopri come lavorare con risorse 3D in Dynamic Media
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: introduction
content-type: reference
translation-type: tm+mt
source-git-commit: cec6c4f9a1a75eb049dd4b8461c36c8d58d46f79
workflow-type: tm+mt
source-wordcount: '2312'
ht-degree: 5%

---


# Utilizzo di risorse 3D in contenuti multimediali dinamici {#working-with-three-d-assets-dm}

Dynamic Media consente di caricare, gestire, visualizzare e distribuire risorse 3D come esperienze coinvolgenti.

* Pubblicazione con un solo clic (tramite **[!UICONTROL Pubblicazione rapida]** sulla barra degli strumenti) di risorse 3D per generare un URL.
* Supporto ottimizzato per la visualizzazione di risorse 3D con il predefinito per visualizzatori dimensionali interattivi di alta qualità fornito da  Adobe Dimension.
* Il componente 3D Media WCM consente di aggiungere facilmente risorse 3D alle pagine AEM Sites .

Non è richiesta alcuna configurazione aggiuntiva per utilizzare risorse 3D in Contenuti multimediali dinamici.

![scarpa in 3d](/help/assets/assets-dm/3d-dimensional-viewer-quickpublish-url-embed2.png)

<!-- See also [Dynamic Media 3D Release Notes](/help/release-notes/aem3d-release-notes.md). -->

## Formati 3D supportati in Dynamic Media {#supported-three-d-file-formats-in-dm}

Dynamic Media supporta i seguenti formati 3D.

Vedere anche formati [3D supportati.](/help/assets/assets-formats.md)

| Estensione dei file 3D | Formato file | Tipo MIME | Note |
|---|---|---|---|
| GLB | Trasmissione GL binario | model/gltf-binary | Include i materiali e le texture come un’unica risorsa. |
| OBJ | File oggetto WaveFront 3D | application/x-tgif |  |
| STL | Stereolitografia | application/vnd.ms-pki.stl |  |
| USDZ | Archivio ZIP con descrizione universale di Scene7 | model/vnd.usdz+zip | *Sostegno solo all&#39;ingestione; non è disponibile alcuna visualizzazione o interazione.* USDZ è un formato 3D proprietario che può essere visualizzato in modo nativo dai dispositivi Safari e iOS. |

## Avvio rapido: Risorse 3D in elementi multimediali dinamici {#quick-start-three-d}

La seguente descrizione dettagliata del flusso di lavoro è stata creata per consentirvi di imparare a usare rapidamente le risorse 3D in modalità Dynamic Media - Scene7.

>[!NOTE]
>
>Le risorse 3D non sono supportate nella modalità Dynamic Media - Hybrid.

Prima di usare risorse 3D in Contenuti multimediali dinamici, accertatevi che l’amministratore di AEM abbia già attivato e configurato Cloud Services di contenuti multimediali dinamici in modalità Scene7.

Consultate [Configuring Dynamic Media Cloud Services](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services) in Configuring Dynamic Media - Scene7 mode and [Troubleshooting Dynamic Media - Scene7 mode.](/help/assets/troubleshoot-dms7.md)

1. **Caricare risorse 3D**

   * [Caricamento delle risorse 3D per l’utilizzo in Contenuti multimediali](/help/assets/manage-assets.md#uploading-assets) dinamici.
   * [Formati di file 3D supportati per il caricamento in elementi multimediali](#supported-three-d-file-formats-in-dm) dinamici.

1. **Gestione delle risorse 3D**

   * Organizzare ed effettuare ricerche in risorse 3D

      * [Organizzazione delle risorse](/help/assets/organize-assets.md#organize-digital-assets) digitali.
      * [Ricerca di risorse](/help/assets/search-assets.md) 3D.
      * [Utilizzo di predicati personalizzati per filtrare i risultati](/help/assets/search-assets.md#custompredicates) di ricerca.
   * Visualizzare risorse 3D

      * [Visualizzazione e interazione con risorse](#viewing-three-d-assets) 3D.
      * [Gestione del predefinito](/help/assets/managing-viewer-presets.md) per visualizzatori dimensionali.
   * Operazioni con i metadati delle risorse 3D

      * [Gestione dei metadati per le risorse](/help/assets/metadata.md) digitali.
      * [Schemi metadati](/help/assets/metadata-schemas.md).



1. **Pubblicare risorse 3D**

   * [Pubblicazione di risorse 3D Dynamic Media statiche](#publishing-three-d-assets)
   * [Metodi alternativi per la pubblicazione di risorse 3D per file multimediali dinamici mediante il visualizzatore dimensionale](#alternate-publish-methods)

## Informazioni sulla visualizzazione e l&#39;interazione con risorse 3D {#viewing-three-d-assets}

Questa sezione descrive come visualizzare e interagire con le risorse 3D in due modi diversi: dalla pagina dei dettagli della risorsa e dal componente File multimediali 3D in Sites.

Il visualizzatore 3D interattivo include, tra le altre cose, una raccolta di controlli per telecamere interattive che consentono di orbitare, ingrandire e scorrere la risorsa 3D.

Il tempo necessario per aprire una risorsa 3D nella visualizzazione pagina Dettagli risorsa dipende da diversi fattori. quali:

* Larghezza di banda al server.
* Latenze al server
* Complessità dell’immagine.

Inoltre, le funzionalità del computer client, come una workstation, un notebook o un dispositivo mobile touch, sono importanti anche quando si modifica la telecamera in modo interattivo. Un sistema ragionevolmente potente con buone capacità grafiche può rendere l’esperienza di visualizzazione 3D interattiva più fluida e favorevole.

>[!TIP]
>
>Potete aprire il predefinito per visualizzatori dimensionali nell’Editor predefinito per visualizzatori per esercitarvi a navigare in una risorsa 3D senza dover prima caricare i file 3D. Il predefinito per visualizzatori dimensionali dispone di una risorsa 3D integrata con cui potete interagire.
>
>Consultate [Gestione dei predefiniti per visualizzatori.](/help/assets/managing-viewer-presets.md)

## Visualizzazione e interazione con una risorsa 3D dalla pagina dei dettagli della risorsa {#viewing-three-d-assets-from-asset-details-page}

Consultate anche [Anteprima delle risorse mediante l&#39;interfaccia software](/help/assets/previewing-assets.md).

**Per visualizzare e interagire con una risorsa 3D dalla pagina dei dettagli della risorsa**

1. Assicurati di aver caricato le risorse 3D in AEM.

   Consultate [Caricamento delle risorse 3D per l&#39;utilizzo in contenuti multimediali dinamici.](/help/assets/manage-assets.md#uploading-assets)

1. Da AEM, nella pagina **[!UICONTROL Navigazione]**, toccare **[!UICONTROL Risorse > File.]**
1. Nell&#39;angolo superiore destro della pagina, dall&#39;elenco a discesa **[!UICONTROL View]**, toccare **[!UICONTROL Card View.]**
1. Accedi alla risorsa 3D da visualizzare.
1. Tocca la scheda della risorsa 3D per aprirla nella pagina dei dettagli della risorsa.
1. Nella pagina di visualizzazione Dettagli della risorsa 3D, effettuate una delle seguenti operazioni:

   * **Girare la fotocamera**  - Orbire la vista intorno alla scena e agli oggetti 3D.
      * _Mouse_: Fare clic con il pulsante sinistro del mouse e trascinare.
      * _Touch screen_: Premere un dito singolo e trascinare.
   * **Scorrimento della telecamera**  - Scorrimento della vista verso sinistra, destra, verso l&#39;alto o verso il basso.
      * _Mouse_: Fare clic con il pulsante destro del mouse e trascinare.
      * _Touch screen_: Premere due dita e trascinare.
   * **Zoom della fotocamera**  - Zoom della fotocamera per spostarsi all&#39;interno e all&#39;esterno delle aree della scena 3D.
      * _Mouse_: Ruota di scorrimento.
      * _Touch screen_: Pizzicotto a due dita.
   * **Rientra la fotocamera**  - Ricentra la fotocamera in un punto della scena 3D.
      * _Mouse_: Fate doppio clic.
      * _Touch screen_: Doppio tocco.
   * **Reimposta** : accanto all’angolo inferiore destro della pagina, toccate l’icona Ripristina per ripristinare il punto di destinazione della vista al centro della risorsa 3D. La funzione Reset (Reimposta) consente di spostare la telecamera più vicino o più lontano per mostrare la risorsa nella sua interezza e a una dimensione di visualizzazione ragionevole.
   * **Modalità**  Schermo intero: per passare alla modalità Schermo intero, nell’angolo inferiore destro della pagina toccate l’icona Schermo intero.

1. Nell’angolo in alto a destra della pagina, tocca **[!UICONTROL Chiudi]** per tornare alla schermata Risorse.

## Visualizzazione e interazione con una risorsa 3D all&#39;interno di un componente Media 3D {#interacting-with-asset-inside-three-d-media-component}

Quando una pagina Web è in modalità **[!UICONTROL Modifica]**, non è possibile interagire con una risorsa 3D. Per rendere la risorsa interattiva, potete utilizzare la funzione **[!UICONTROL Anteprima]** per visualizzare la pagina Web nell’editor pagina e accedere pienamente alle funzionalità del componente File multimediali 3D.

>[!IMPORTANT]
>
>Potete eseguire questa operazione solo dopo aver aggiunto un componente File multimediali 3D a una pagina Web e assegnato una risorsa 3D al componente. Consultate [Aggiunta del componente File multimediali 3D a una pagina Web](#adding-the-three-d-media-component-to-a-web-page) e [Assegnazione di una risorsa 3D a un componente File multimediali 3D.](#assigning-a-three-d-asset-to-the-component)

Vedere anche [Anteprima delle risorse mediante l&#39;interfaccia software.](/help/assets/previewing-assets.md)

**Per visualizzare e interagire con una risorsa 3D all’interno di un componente Media 3D**

1. Mentre una pagina Web è in modalità **[!UICONTROL Modifica]**, effettuate una delle seguenti operazioni:

   * Vicino alla parte superiore destra della pagina, fare clic su **[!UICONTROL Anteprima]** per passare alla modalità **[!UICONTROL Anteprima]**.
   * Elimina `/editor.html` dall&#39;URL della pagina nel browser.

Una risorsa 3D completamente interattiva come visualizzata in    ![Risorsa 3D visualizzata all’interno del ](/help/assets/assets-dm/3d-asset-in-3d-media.png)
componente File multimediali 3Da risorsa 3D completamente interattiva visualizzata in modalità  **** Anteprima.

1. In modalità **[!UICONTROL Anteprima]**, effettuate una delle seguenti operazioni:

   * **Girare la fotocamera**  - Orbire la vista intorno alla scena e agli oggetti 3D.
      * _Mouse_: Fare clic con il pulsante sinistro del mouse e trascinare.
      * _Touch screen_: Premere un dito singolo e trascinare.
   * **Scorrimento della telecamera**  - Scorrimento della vista verso sinistra, destra, verso l&#39;alto o verso il basso.
      * _Mouse_: Fare clic con il pulsante destro del mouse e trascinare.
      * _Touch screen_: Premere due dita e trascinare.
   * **Zoom della fotocamera**  - Zoom della fotocamera per spostarsi all&#39;interno e all&#39;esterno delle aree della scena 3D.
      * _Mouse_: Ruota di scorrimento.
      * _Touch screen_: Pizzicotto a due dita.
   * **Rientra la fotocamera**  - Ricentra la fotocamera in un punto della scena 3D.
      * _Mouse_: Fate doppio clic.
      * _Touch screen_: Doppio tocco.
   * **Reimposta** : accanto all’angolo inferiore destro della pagina, toccate l’icona Ripristina per ripristinare il punto di destinazione della vista al centro della risorsa 3D. La funzione Reset (Reimposta) consente di spostare la telecamera più vicino o più lontano per mostrare la risorsa nella sua interezza e a una dimensione di visualizzazione ragionevole.
   * **Modalità**  Schermo intero: per passare alla modalità Schermo intero, nell’angolo inferiore destro della pagina toccate l’icona Schermo intero.

## Informazioni sull&#39;utilizzo del componente File multimediali 3D {#working-with-three-d-media-component}

Contenuti multimediali dinamici include un componente Contenuti multimediali 3D per elementi multimediali dinamici che potete usare in  AEM Sites per attivare la visualizzazione interattiva dei modelli 3D sulle pagine Web.

* [Aggiunta del componente File multimediali 3D al modello di pagina](#adding-three-d-media-component-to-page-template)
* [Aggiunta del componente File multimediali 3D a una pagina Web](#adding-the-three-d-media-component-to-a-web-page)
   * [Facoltativo - Configurazione del componente File multimediali 3D](#configuring-the-three-d-component)
* [Assegnazione di una risorsa 3D al componente File multimediali 3D](#assigning-a-three-d-asset-to-the-component)


## Aggiunta del componente File multimediali 3D al modello di pagina {#adding-three-d-media-component-to-page-template}

1. Passa a **[!UICONTROL Strumenti > Generale > Modelli.]**
1. Individuate il modello di pagina in cui desiderate abilitare il componente 3D e selezionatelo.
1. Toccate **[!UICONTROL Modifica]** per aprire il modello.
1. Vicino alla parte superiore destra della pagina, nel menu a discesa, selezionare la modalità **[!UICONTROL Struttura]**, se non è già attiva.

   ![3d-media-component-structure](/help/assets/assets-dm/3d-media-component-structure.png)

1. Toccate un&#39;area vuota nell&#39;area **[!UICONTROL Contenitore di layout]** per selezionarla e aprire la barra degli strumenti associata.
1. Sulla barra degli strumenti, toccare l&#39;icona **[!UICONTROL Policy]** per aprire l&#39; **[!UICONTROL Editor criteri.]**
1. Nella sezione **[!UICONTROL Proprietà]**, nella scheda **[!UICONTROL Componenti consentiti]**, scorrere fino a **[!UICONTROL Contenuti multimediali dinamici]**, espandere l&#39;elenco e selezionare **[!UICONTROL File multimediali 3D.]**
1. Toccate **[!UICONTROL Fine]** per salvare le modifiche e chiudere l&#39; **[!UICONTROL Editor criteri.]**

   Ora puoi posizionare il componente Contenuti multimediali 3D dinamici su tutte le pagine che utilizzano questo modello.

## Aggiunta del componente File multimediali 3D a una pagina Web {#adding-the-three-d-media-component-to-a-web-page}

Se utilizzate Adobe Experience Manager come sistema di gestione dei contenuti Web, potete aggiungere risorse 3D alle pagine Web mediante il componente File multimediali 3D.

Vedere anche [Aggiunta di risorse per file multimediali dinamici alle pagine.](/help/assets/adding-dynamic-media-assets-to-pages.md)

1. Aprite  AEM Sites e selezionate la pagina Web alla quale desiderate aggiungere il componente Contenuti multimediali 3D dinamici.
1. Toccate l&#39;icona **[!UICONTROL Modifica]** (matita) per aprire la pagina nell&#39;editor pagina. Assicurarsi che la modalità **[!UICONTROL Modifica]** sia selezionata in alto a destra della pagina.

   ![3d-media-component-add](/help/assets/assets-dm/3d-media-component-edit.png)

1. Sulla barra degli strumenti, toccate l’icona Pannello laterale per attivare o disattivare la visualizzazione del pannello.

1. Nel pannello laterale, toccate l&#39;icona del segno più per aprire l&#39;elenco **[!UICONTROL Componenti]**.

   ![3d-media-component-drag-drop](/help/assets/assets-dm/3d-assets-filter.png)

1. Trascinate il componente **[!UICONTROL File multimediali 3D]** dall&#39;elenco **[!UICONTROL Componenti]** nella posizione nella pagina in cui desiderate visualizzare il visualizzatore 3D.

È ora possibile assegnare una risorsa 3D al componente.

Consultate [Assegnazione di una risorsa 3D a un componente File multimediali 3D.](#assigning-a-three-d-asset-to-the-component)

### Facoltativo - Configurazione del componente File multimediali 3D {#configuring-the-three-d-component}

1. Nell&#39;editor  pagina AEM Sites, selezionate il componente **[!UICONTROL 3D Media Viewer]** precedentemente aggiunto alla pagina.
1. Toccate l&#39;icona **[!UICONTROL Configuration]** (chiave inglese) per aprire la finestra di dialogo di configurazione del componente.

   ![3d-media-component-config](/help/assets/assets-dm/3d-media-component-config.png)

1. Nella finestra di dialogo File multimediali 3D, dall’elenco a discesa Predefinito visualizzatore, selezionate **[!UICONTROL Dimensionale]** per assegnare il predefinito per visualizzatori dimensionali al componente.

   ![3d-media-component-edit-config](/help/assets/assets-dm/3d-media-component-edit-config.png)

1. Nell&#39;angolo superiore destro, toccate il segno di spunta per salvare le modifiche.

## Assegnazione di una risorsa 3D al componente File multimediali 3D {#assigning-a-three-d-asset-to-the-component}

Dopo aver aggiunto un componente File multimediali 3D a una pagina Web, potete assegnarvi una risorsa 3D.

Vedere [Aggiunta del componente File multimediali 3D a una pagina Web.](#adding-the-three-d-media-component-to-a-web-page)

1. Nell&#39;editor  pagina AEM Sites, fai clic sull&#39;icona **[!UICONTROL Risorse]** per aprire **[!UICONTROL Risorse]** nel pannello laterale.
1. Nell&#39;elenco a discesa, selezionate **[!UICONTROL 3D]** per visualizzare solo i tipi di file di risorse 3D.
1. Nel pannello laterale, cercate o scorrete fino alla risorsa 3D che desiderate visualizzare sulla pagina da modificare.
1. Trascina la risorsa 3D dal pannello laterale Risorse e rilasciala sul componente **[!UICONTROL 3D Media]** precedentemente aggiunto alla pagina.

   ![Assegnare risorse 3d al componente File multimediali 3d](/help/assets/assets-dm/3d-asset-add.png)

>[!NOTE]
>
>Mentre una pagina Web si trova nella  modalità AEM Sites **[!UICONTROL Modifica]**, il componente File multimediali 3D visualizza la risorsa 3D ma non è possibile interagire con essa. Per rendere la risorsa interattiva, potete utilizzare la funzione **[!UICONTROL Anteprima]** per visualizzare la pagina Web nell’editor pagina e accedere pienamente alle funzionalità del componente File multimediali 3D.

## Pubblicazione di risorse 3D Dynamic Media statiche {#publishing-three-d-assets}

Dynamic Media accetta una serie di formati di file 3D supportati come *contenuto statico* in Dynamic Media. I contenuti statici consentono di caricare e pubblicare risorse 3D, ma non è supportato per la riproduzione di immagini o immagini *dinamiche* associate alla risorsa 3D. Il motivo è che Dynamic Media Imaging Server non riconosce i formati 3D. Di conseguenza, dopo aver pubblicato una risorsa 3D in Contenuti multimediali dinamici, potete copiare un URL immediato. L’URL per la risorsa 3D segue la consueta struttura URL per file multimediali dinamici. Tuttavia, non potete modificare alcun parametro nell’URL della risorsa, a differenza delle risorse di immagine tradizionali negli elementi multimediali dinamici.

Consultate anche [Ottenimento di un URL per una risorsa statica.](/help/assets/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-a-static-asset)

Nella **[!UICONTROL vista a schede]**, un&#39;icona a forma di globo viene visualizzata direttamente sotto il nome di una risorsa e a sinistra della data e dell&#39;ora in cui è pubblicata per indicare che è stata pubblicata. Nella **[!UICONTROL Vista a elenco]**, la colonna **[!UICONTROL Pubblicato]** indica lo stato di pubblicazione delle risorse.

Se usate AEM come WCM, usate questo metodo di pubblicazione per aggiungere le risorse 3D per elementi multimediali dinamici direttamente sulla pagina Web.

Vedere anche [Pubblicazione di risorse per file multimediali dinamici.](publishing-dynamicmedia-assets.md)

Vedere anche [Pubblicazione di pagine.](/help/sites-authoring/publishing-pages.md)

**Per pubblicare risorse 3D per elementi multimediali dinamici statici**

1. Aprite una risorsa 3D (formato di file GLB, OBJ o STL) per visualizzarla nella pagina dei dettagli della risorsa.
1. Sulla barra degli strumenti, toccare **[!UICONTROL Pubblicazione rapida.]**

   ![3d-asset-quick-publish](/help/assets/assets-dm/3d-asset-quick-publish.png)

1. Toccate **[!UICONTROL Chiudi]** per uscire dalla finestra di dialogo e tornare alla pagina dei dettagli della risorsa.
1. Dall&#39;elenco a discesa a sinistra del nome del file della risorsa 3D, tocca **[!UICONTROL Rappresentazioni.]**

   ![3d-asset-renditions](/help/assets/assets-dm/3d-asset-renditions.png)

1. Toccate **[!UICONTROL originale.]** Quando una risorsa 3D viene pubblicata (o &quot;attivata&quot;), l’ **** URLbutton viene visualizzato accanto all’angolo in basso a sinistra della pagina se sono soddisfatte tutte le seguenti condizioni per la risorsa 3D:
   * La risorsa 3D è un formato supportato (GLB, OBJ, STL e USDZ).
   * La risorsa 3D è stata assimilata in Dynamic Media Image Production System (IPS).
   * La risorsa 3D viene pubblicata.

   ![3d-asset-url](/help/assets/assets-dm/3d-asset-url.png)

1. Toccate **[!UICONTROL URL]** per visualizzare l&#39;URL di produzione diretto della risorsa 3D, che potete copiare e utilizzare sulle pagine Web.

### Metodi alternativi per la pubblicazione di risorse Dynamic Media 3D mediante il visualizzatore dimensionale {#alternate-publish-methods}

Utilizzate i due metodi seguenti per pubblicare le risorse 3D per elementi multimediali dinamici se *non* utilizzate AEM come WCM.

* **[!UICONTROL URL]**  - Utilizzate  **** URL se utilizzate un sistema di gestione dei contenuti Web di terze parti e desiderate collegare le risorse 3D per elementi multimediali dinamici alle pagine Web mediante il visualizzatore dimensionale.

   Vedere [Collegamento di URL all&#39;applicazione Web.](/help/assets/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset)

* **[!UICONTROL Incorpora]**  - Utilizzate  **** Incorpora per visualizzare una risorsa 3D per file multimediali dinamici incorporata in una pagina Web mediante il visualizzatore Dimensionale. Puoi copiare il codice da incorporare negli Appunti, per poi incollarlo nelle pagine web. La modifica del codice non è consentita nella finestra di dialogo **[!UICONTROL Incorpora]**.

   Consultate [Incorporazione di video per file multimediali dinamici, visualizzatore immagini o visualizzatore dimensionale in una pagina Web.](/help/assets/embed-code.md#embedding-the-video-or-image-viewer-on-a-web-page)