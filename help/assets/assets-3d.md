---
title: Utilizzo di risorse 3D in Dynamic Media
seo-title: Utilizzo di risorse 3D in Dynamic Media
description: Scopri come lavorare con le risorse 3D in Dynamic Media
seo-description: Scopri come lavorare con le risorse 3D in Dynamic Media
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: introduction
content-type: reference
feature: 3D Assets,Asset Management
role: Business Practitioner, Administrator
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '2319'
ht-degree: 5%

---


# Utilizzo di risorse 3D in Dynamic Media {#working-with-three-d-assets-dm}

Dynamic Media consente di caricare, gestire, visualizzare e distribuire risorse 3D come esperienze immersive.

* Pubblicazione con un solo clic (utilizzando **[!UICONTROL Pubblicazione rapida]** sulla barra degli strumenti) di risorse 3D per generare un URL.
* Supporto ottimizzato per la visualizzazione di risorse 3D con il visualizzatore Dimensionale interattivo di alta qualità basato su Adobe Dimension.
* Il componente 3D Media WCM consente di aggiungere facilmente risorse 3D alle pagine AEM Sites.

Non è necessaria alcuna configurazione aggiuntiva per utilizzare le risorse 3D in Dynamic Media.

![scarpa in 3d](/help/assets/assets-dm/3d-dimensional-viewer-quickpublish-url-embed2.png)

<!-- See also [Dynamic Media 3D Release Notes](/help/release-notes/aem3d-release-notes.md). -->

## Formati 3D supportati in Dynamic Media {#supported-three-d-file-formats-in-dm}

Dynamic Media supporta i seguenti formati 3D.

Vedere anche [Formati 3D supportati.](/help/assets/assets-formats.md)

| Estensione file 3D | Formato file | Tipo MIME | Note |
|---|---|---|---|
| GLB | Trasmissione GL binaria | model/gltf binario | Include i materiali e le texture come un’unica risorsa. |
| OBJ | File oggetto 3D WaveFront | application/x-tgif |  |
| STL | Stereolitografia | application/vnd.ms-pki.stl |  |
| USDZ | Universal Scene Descrizione Archivio ZIP | model/vnd.usdz+zip | *Sostegno solo all&#39;acquisizione; non è disponibile alcuna visualizzazione o interazione.* USDZ è un formato 3D proprietario che può essere visualizzato in modo nativo dai dispositivi Safari e iOS. |

## Avvio rapido: Risorse 3D in Dynamic Media {#quick-start-three-d}

La seguente descrizione dettagliata del flusso di lavoro è stata progettata per aiutarti a iniziare rapidamente a usare le risorse 3D in modalità Dynamic Media - Scene7.

>[!NOTE]
>
>Le risorse 3D non sono supportate in Dynamic Media - Modalità ibrida.

Prima di lavorare con le risorse 3D in Dynamic Media, accertati che il tuo amministratore AEM abbia già abilitato e configurato i Cloud Services Dynamic Media in modalità Dynamic Media - Scene7.

Consulta [Configurazione di Cloud Services Dynamic Media](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services) in Configurazione di Dynamic Media - Modalità Scene7 e [Risoluzione dei problemi relativi a Dynamic Media - Modalità Scene7.](/help/assets/troubleshoot-dms7.md)

1. **Caricare risorse 3D**

   * [Caricamento delle risorse 3D da utilizzare in Dynamic Media](/help/assets/manage-assets.md#uploading-assets).
   * [Formati di file 3D supportati per il caricamento in Dynamic Media](#supported-three-d-file-formats-in-dm).

1. **Gestione delle risorse 3D**

   * Organizzare e cercare risorse 3D

      * [Organizzazione delle risorse](/help/assets/organize-assets.md#organize-digital-assets) digitali.
      * [Ricerca di risorse](/help/assets/search-assets.md) 3D.
      * [Utilizzo di predicati personalizzati per filtrare i risultati](/help/assets/search-assets.md#custompredicates) della ricerca.
   * Visualizzare risorse 3D

      * [Visualizzazione e interazione con risorse](#viewing-three-d-assets) 3D.
      * [Gestione del predefinito](/help/assets/managing-viewer-presets.md) visualizzatore dimensionale.
   * Utilizzare i metadati delle risorse 3D

      * [Gestione dei metadati per le risorse](/help/assets/metadata.md) digitali.
      * [Schemi metadati](/help/assets/metadata-schemas.md).



1. **Pubblicare risorse 3D**

   * [Pubblicazione di risorse statiche Dynamic Media 3D](#publishing-three-d-assets)
   * [Metodi alternativi per la pubblicazione di risorse 3D Dynamic Media utilizzando il visualizzatore dimensionale](#alternate-publish-methods)

## Informazioni sulla visualizzazione e sull’interazione con risorse 3D {#viewing-three-d-assets}

Questa sezione descrive come visualizzare e interagire con le risorse 3D in due modi diversi: dalla pagina dei dettagli della risorsa e dal componente Media 3D in Sites.

Il visualizzatore 3D interattivo include, tra le altre cose, una raccolta di controlli interattivi per le telecamere che consentono di orbitare, ingrandire e scorrere la risorsa 3D.

Il tempo necessario per aprire una risorsa 3D nella visualizzazione pagina Dettagli risorsa dipende da diversi fattori. quali:

* Larghezza di banda per il server.
* Latenze al server
* Complessità dell&#39;immagine.

Inoltre, le funzionalità del computer client, come una workstation, un notebook o un dispositivo touch mobile, sono importanti anche quando si manipola la fotocamera in modo interattivo. Un sistema ragionevolmente potente con buone capacità grafiche può rendere l’esperienza di visualizzazione 3D interattiva più fluida e favorevole.

>[!TIP]
>
>Puoi aprire il predefinito visualizzatore dimensionale nell’Editor predefiniti per visualizzatori per esercitarti a navigare su una risorsa 3D senza dover prima caricare alcun file 3D. Il predefinito visualizzatore dimensionale dispone di una risorsa 3D incorporata con cui è possibile interagire.
>
>Consulta [Gestione dei predefiniti per visualizzatori.](/help/assets/managing-viewer-presets.md)

## Visualizzazione e interazione con una risorsa 3D dalla pagina dei dettagli della risorsa {#viewing-three-d-assets-from-asset-details-page}

Consulta anche [Anteprima delle risorse tramite l&#39;interfaccia software](/help/assets/previewing-assets.md).

**Per visualizzare e interagire con una risorsa 3D dalla pagina dei dettagli della risorsa**

1. Assicurati di aver caricato le risorse 3D in AEM.

   Consulta [Caricamento delle risorse 3D per l&#39;utilizzo in Dynamic Media.](/help/assets/manage-assets.md#uploading-assets)

1. Da AEM, nella pagina **[!UICONTROL Navigazione]**, tocca **[!UICONTROL Risorse > File.]**
1. Dall’elenco a discesa **[!UICONTROL Visualizza]** nell’angolo in alto a destra della pagina, tocca **[!UICONTROL Vista a schede.]**
1. Accedi alla risorsa 3D da visualizzare.
1. Tocca la scheda della risorsa 3D per aprirla nella pagina dei dettagli della risorsa.
1. Nella pagina di visualizzazione dei dettagli della risorsa 3D, effettua una delle seguenti operazioni:

   * **Girare la fotocamera**  - Rotazione la visualizzazione intorno alla scena e agli oggetti 3D.
      * _Mouse_: Clic a sinistra + trascinamento.
      * _Schermata_ touch: Premere un dito singolo + trascinare.
   * **Panning della fotocamera** : effettua il panning della vista a sinistra, a destra, su o giù.
      * _Mouse_: Fai clic con il pulsante destro del mouse e trascina.
      * _Schermata_ touch: Premere due dita + trascinare.
   * **Zoom della fotocamera**  - Zoom della fotocamera per spostarsi in e fuori da aree della scena 3D.
      * _Mouse_: Ruota di scorrimento.
      * _Schermata_ touch: Pizzico a due dita.
   * **Ricentrate la fotocamera**  - Ricentate la fotocamera in un punto su un oggetto nella scena 3D.
      * _Mouse_: Fare doppio clic.
      * _Schermata_ touch: Tocca due volte.
   * **Ripristina** : vicino all’angolo inferiore destro della pagina, tocca l’icona Ripristina per ripristinare il punto di destinazione della visualizzazione al centro della risorsa 3D. Inoltre, la funzione Reset sposta la telecamera più vicino o più lontano per mostrare la risorsa nella sua interezza e a una dimensione di visualizzazione ragionevole.
   * **Modalità a tutto schermo**  - Per passare alla modalità a tutto schermo, tocca l’icona a schermo intero nell’angolo in basso a destra della pagina.

1. Nell’angolo in alto a destra della pagina, tocca **[!UICONTROL Chiudi]** per tornare alla schermata Risorse.

## Visualizzazione e interazione con una risorsa 3D all’interno di un componente Media 3D {#interacting-with-asset-inside-three-d-media-component}

Quando una pagina web è in modalità **[!UICONTROL Modifica]**, non è possibile interagire con una risorsa 3D. Per rendere la risorsa interattiva, puoi utilizzare la funzione **[!UICONTROL Anteprima]** per visualizzare la pagina web nell’editor di pagine con accesso completo alle funzionalità del componente File multimediali 3D.

>[!IMPORTANT]
>
>Puoi eseguire questa operazione solo dopo aver aggiunto un componente Media 3D a una pagina web e assegnato una risorsa 3D al componente. Consulta [Aggiunta di un componente Media 3D a una pagina web](#adding-the-three-d-media-component-to-a-web-page) e [Assegnazione di una risorsa 3D a un componente Media 3D.](#assigning-a-three-d-asset-to-the-component)

Consulta anche [Anteprima delle risorse tramite l&#39;interfaccia software.](/help/assets/previewing-assets.md)

**Per visualizzare e interagire con una risorsa 3D all’interno di un componente Media 3D**

1. Quando una pagina web è in modalità **[!UICONTROL Modifica]**, effettuare una delle seguenti operazioni:

   * Vicino all&#39;angolo superiore destro della pagina, fai clic su **[!UICONTROL Anteprima]** per accedere alla modalità **[!UICONTROL Anteprima]**.
   * Elimina `/editor.html` dall’URL della pagina nel browser.

Una risorsa 3D completamente interattiva come visualizzata in    ![Risorsa 3D visualizzata all’interno del ](/help/assets/assets-dm/3d-asset-in-3d-media.png)
componente File multimediali 3Duna risorsa 3D completamente interattiva come visualizzata in modalità  **** Anteprima.

1. In modalità **[!UICONTROL Anteprima]**, effettuare una delle seguenti operazioni:

   * **Girare la fotocamera**  - Rotazione la visualizzazione intorno alla scena e agli oggetti 3D.
      * _Mouse_: Clic a sinistra + trascinamento.
      * _Schermata_ touch: Premere un dito singolo + trascinare.
   * **Panning della fotocamera** : effettua il panning della vista a sinistra, a destra, su o giù.
      * _Mouse_: Fai clic con il pulsante destro del mouse e trascina.
      * _Schermata_ touch: Premere due dita + trascinare.
   * **Zoom della fotocamera**  - Zoom della fotocamera per spostarsi in e fuori da aree della scena 3D.
      * _Mouse_: Ruota di scorrimento.
      * _Schermata_ touch: Pizzico a due dita.
   * **Ricentrate la fotocamera**  - Ricentate la fotocamera in un punto su un oggetto nella scena 3D.
      * _Mouse_: Fare doppio clic.
      * _Schermata_ touch: Tocca due volte.
   * **Ripristina** : vicino all’angolo inferiore destro della pagina, tocca l’icona Ripristina per ripristinare il punto di destinazione della visualizzazione al centro della risorsa 3D. Inoltre, la funzione Reset sposta la telecamera più vicino o più lontano per mostrare la risorsa nella sua interezza e a una dimensione di visualizzazione ragionevole.
   * **Modalità a tutto schermo**  - Per passare alla modalità a tutto schermo, tocca l’icona a schermo intero nell’angolo in basso a destra della pagina.

## Utilizzo del componente Media 3D {#working-with-three-d-media-component}

Dynamic Media include un componente Media 3D di Dynamic Media che può essere utilizzato in AEM Sites per abilitare la visualizzazione interattiva dei modelli 3D sulle pagine web.

* [Aggiunta del componente Media 3D al modello di pagina](#adding-three-d-media-component-to-page-template)
* [Aggiunta del componente Media 3D a una pagina web](#adding-the-three-d-media-component-to-a-web-page)
   * [Facoltativo - Configurazione del componente File multimediali 3D](#configuring-the-three-d-component)
* [Assegnazione di una risorsa 3D al componente File multimediali 3D](#assigning-a-three-d-asset-to-the-component)


## Aggiunta del componente Media 3D al modello di pagina {#adding-three-d-media-component-to-page-template}

1. Passa a **[!UICONTROL Strumenti > Generale > Modelli.]**
1. Passa al modello di pagina in cui desideri abilitare il componente 3D e seleziona il modello.
1. Tocca **[!UICONTROL Modifica]** per aprire il modello.
1. Vicino all’angolo superiore destro della pagina, nel menu a discesa selezionare la modalità **[!UICONTROL Struttura]** , se non è già attiva.

   ![3d-media-component-structure](/help/assets/assets-dm/3d-media-component-structure.png)

1. Toccare un’area vuota nell’area **[!UICONTROL Contenitore di layout]** per selezionarla e aprire la relativa barra degli strumenti associata.
1. Sulla barra degli strumenti, tocca l&#39;icona **[!UICONTROL Policy]** per aprire l&#39; **[!UICONTROL Editor criteri.]**
1. Nella sezione **[!UICONTROL Proprietà]**, nella scheda **[!UICONTROL Componenti consentiti]** , scorri fino a **[!UICONTROL Dynamic Media]**, espandi l’elenco e seleziona **[!UICONTROL File multimediali 3D.]**
1. Tocca **[!UICONTROL Fine]** per salvare le modifiche e chiudere l&#39; **[!UICONTROL Editor criteri.]**

   Ora puoi posizionare il componente Media 3D di Dynamic Media su tutte le pagine che utilizzano questo modello.

## Aggiunta del componente Media 3D a una pagina web {#adding-the-three-d-media-component-to-a-web-page}

Se utilizzi Adobe Experience Manager come sistema di gestione dei contenuti web, puoi aggiungere risorse 3D alle pagine web tramite il componente Media 3D.

Consulta anche [Aggiunta di risorse Dynamic Media alle pagine.](/help/assets/adding-dynamic-media-assets-to-pages.md)

1. Apri AEM Sites e seleziona la pagina web a cui desideri aggiungere il componente Media 3D di Dynamic Media.
1. Tocca l’icona **[!UICONTROL Modifica]** (matita) per aprire la pagina nell’editor di pagine. Assicurati che la modalità **[!UICONTROL Modifica]** sia selezionata in alto a destra nella pagina.

   ![3d-media-component-add](/help/assets/assets-dm/3d-media-component-edit.png)

1. Nella barra degli strumenti, tocca l’icona Pannello laterale per attivare o disattivare la visualizzazione del pannello.

1. Nel pannello laterale, tocca l’icona del segno più per aprire l’elenco **[!UICONTROL Componenti]** .

   ![3d-media-component-drag-drop](/help/assets/assets-dm/3d-assets-filter.png)

1. Trascina il componente **[!UICONTROL File multimediali 3D]** dall’elenco **[!UICONTROL Componenti]** nella posizione nella pagina in cui vuoi visualizzare il visualizzatore 3D.

Ora puoi assegnare una risorsa 3D al componente.

Consulta [Assegnazione di una risorsa 3D a un componente Media 3D.](#assigning-a-three-d-asset-to-the-component)

### Facoltativo - Configurazione del componente Media 3D {#configuring-the-three-d-component}

1. Nell’editor pagina di AEM Sites, seleziona il componente **[!UICONTROL 3D Media Viewer]** che hai aggiunto in precedenza alla pagina.
1. Toccare l&#39;icona **[!UICONTROL Configurazione]** (chiave inglese) per aprire la finestra di dialogo di configurazione del componente.

   ![3d-media-component-config](/help/assets/assets-dm/3d-media-component-config.png)

1. Nell’elenco a discesa Predefinito visualizzatore della finestra di dialogo File multimediali 3D , seleziona **[!UICONTROL Dimensionale]** per assegnare il predefinito visualizzatore dimensionale al componente.

   ![3d-media-component-edit-config](/help/assets/assets-dm/3d-media-component-edit-config.png)

1. Nell’angolo in alto a destra, tocca il segno di spunta per salvare le modifiche.

## Assegnazione di una risorsa 3D al componente File multimediali 3D {#assigning-a-three-d-asset-to-the-component}

Dopo aver aggiunto un componente Media 3D a una pagina web, puoi assegnargli una risorsa 3D.

Consulta [Aggiunta del componente Media 3D a una pagina web.](#adding-the-three-d-media-component-to-a-web-page)

1. Nell’editor pagina di AEM Sites, fai clic sull’icona **[!UICONTROL Risorse]** per aprire **[!UICONTROL Risorse]** nel pannello laterale.
1. Nell’elenco a discesa, seleziona **[!UICONTROL 3D]** per visualizzare solo i tipi di file di risorse 3D.
1. Nel pannello laterale, cerca o scorri fino alla risorsa 3D che desideri visualizzare sulla pagina da modificare.
1. Trascina la risorsa 3D dal pannello laterale Risorse e rilasciala sul componente **[!UICONTROL 3D Media]** che hai aggiunto in precedenza alla pagina.

   ![Assegnare risorse 3d al componente Media 3d](/help/assets/assets-dm/3d-asset-add.png)

>[!NOTE]
>
>Mentre una pagina web è in modalità AEM Sites **[!UICONTROL Modifica]**, il componente File multimediali 3D visualizza la risorsa 3D ma non è possibile interagire con essa. Per rendere la risorsa interattiva, puoi utilizzare la funzione **[!UICONTROL Anteprima]** per visualizzare la pagina web nell’editor di pagine con accesso completo alle funzionalità del componente File multimediali 3D.

## Pubblicazione di risorse 3D Dynamic Media statiche {#publishing-three-d-assets}

Dynamic Media accetta diversi formati di file 3D supportati come *contenuto statico* in Dynamic Media. Il contenuto statico consente di caricare e pubblicare risorse 3D, ma non è disponibile il supporto per l’ *imaging dinamico* o per il caricamento di immagini associato alla risorsa 3D. Il motivo è che Dynamic Media Imaging Server non riconosce i formati 3D. Di conseguenza, dopo aver pubblicato una risorsa 3D in Dynamic Media, disponi di un URL istantaneo che puoi copiare. L’URL della risorsa 3D segue la consueta struttura URL di Dynamic Media. Tuttavia, non puoi modificare alcun parametro nell’URL della risorsa, a differenza delle risorse di immagini tradizionali in Dynamic Media.

Consulta anche [Ottenimento di un URL per una risorsa statica.](/help/assets/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-a-static-asset)

Nella **[!UICONTROL Vista a schede]**, sotto il nome di una risorsa viene visualizzata una piccola icona a forma di globo, a sinistra della data e dell’ora per indicare che è stata pubblicata. Nella **[!UICONTROL Vista a elenco]**, la colonna **[!UICONTROL Pubblicato]** indica lo stato di pubblicazione delle risorse.

Se utilizzi AEM come WCM, utilizza questo metodo di pubblicazione per aggiungere le risorse 3D di Dynamic Media direttamente sulla tua pagina web.

Consulta anche [Pubblicazione di risorse Dynamic Media.](publishing-dynamicmedia-assets.md)

Vedere anche [Pubblicazione di pagine.](/help/sites-authoring/publishing-pages.md)

**Per pubblicare risorse 3D statiche di Dynamic Media**

1. Apri una risorsa 3D (formato di file GLB, OBJ o STL) per visualizzarla nella pagina dei dettagli della risorsa.
1. Sulla barra degli strumenti, tocca **[!UICONTROL Pubblicazione rapida.]**

   ![3d-asset-quick-publish](/help/assets/assets-dm/3d-asset-quick-publish.png)

1. Tocca **[!UICONTROL Chiudi]** per uscire dalla finestra di dialogo e tornare alla pagina dei dettagli della risorsa.
1. Dall’elenco a discesa a sinistra del nome del file della risorsa 3D, tocca **[!UICONTROL Rappresentazioni.]**

   ![3d-asset-rendering](/help/assets/assets-dm/3d-asset-renditions.png)

1. Tocca **[!UICONTROL originale.]** Quando una risorsa 3D viene pubblicata (o &quot;attivata&quot;), il pulsante  **** URL viene visualizzato nell’angolo in basso a sinistra della pagina se sono soddisfatte tutte le seguenti condizioni per la risorsa 3D:
   * Il asset 3D è un formato supportato (GLB, OBJ, STL e USDZ).
   * La risorsa 3D è stata assimilata in Dynamic Media Image Production System (IPS).
   * La risorsa 3D viene pubblicata.

   ![3d-asset-url](/help/assets/assets-dm/3d-asset-url.png)

1. Tocca **[!UICONTROL URL]** per visualizzare l’URL di produzione diretta della risorsa 3D che puoi copiare e utilizzare nelle pagine web.

### Metodi alternativi per la pubblicazione di risorse 3D Dynamic Media utilizzando il visualizzatore dimensionale {#alternate-publish-methods}

Utilizza i due metodi seguenti per pubblicare le risorse Dynamic Media 3D se *non* utilizzi AEM come WCM.

* **[!UICONTROL URL]**  - Utilizza l’ **** URL se utilizzi un sistema di gestione dei contenuti web di terze parti e desideri collegare risorse Dynamic Media 3D alle tue pagine web utilizzando il visualizzatore dimensionale.

   Consulta [Collegamento di URL all&#39;applicazione Web.](/help/assets/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset)

* **[!UICONTROL Incorpora]**  - Utilizza  **** Incorpora per visualizzare una risorsa Dynamic Media 3D incorporata in una pagina web utilizzando il visualizzatore Dimensionale. Puoi copiare il codice da incorporare negli Appunti, per poi incollarlo nelle pagine web. La modifica del codice non è consentita nella finestra di dialogo **[!UICONTROL Incorpora]**.

   Consulta [Incorporare un visualizzatore video, immagine o dimensionale di Dynamic Media in una pagina web.](/help/assets/embed-code.md#embedding-the-video-or-image-viewer-on-a-web-page)