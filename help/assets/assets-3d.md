---
title: Utilizzo di risorse 3D in Dynamic Media
seo-title: Working with 3D assets in Dynamic Media
description: Scopri come lavorare con le risorse 3D in Dynamic Media
seo-description: Learn how to work with 3D assets in Dynamic Media
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: introduction
content-type: reference
feature: 3D Assets,Asset Management
role: User, Admin
exl-id: 01c96f1e-c0e6-497d-bd7a-c0fd547a34da
source-git-commit: 9f08d529af0ec37d2bd2a4f479a172c6c950c47d
workflow-type: tm+mt
source-wordcount: '2309'
ht-degree: 4%

---

# Utilizzare le risorse 3D in Dynamic Media {#working-with-three-d-assets-dm}

Dynamic Media consente di caricare, gestire, visualizzare e distribuire risorse 3D come esperienze immersive.

* Pubblicazione con un solo clic (utilizzando **[!UICONTROL Pubblicazione rapida]** sulla barra degli strumenti) di risorse 3D per generare un URL.
* Supporto ottimizzato per la visualizzazione di risorse 3D con il visualizzatore Dimensionale interattivo di alta qualità basato su Adobe Dimension.
* Il componente 3D Media WCM consente di aggiungere facilmente risorse 3D alle pagine Adobe Experience Manager Sites.

Non è necessaria alcuna configurazione aggiuntiva per utilizzare le risorse 3D in Dynamic Media.

![Scarpa in 3d](/help/assets/assets-dm/3d-dimensional-viewer-quickpublish-url-embed2.png)

<!-- See also [Dynamic Media 3D Release Notes](/help/release-notes/aem3d-release-notes.md). -->

## Formati 3D supportati in Dynamic Media {#supported-three-d-file-formats-in-dm}

Dynamic Media supporta i seguenti formati 3D.

Vedi anche [Formati 3D supportati](/help/assets/assets-formats.md).

| Estensione file 3D | Formato file | Tipo MIME | Note |
|---|---|---|---|
| GLB | Trasmissione GL binaria | model/gltf binario | Include i materiali e le texture come un’unica risorsa. |
| OBJ | File oggetto 3D WaveFront | application/x-tgif |  |
| STL | Stereolitografia | application/vnd.ms-pki.stl |  |
| USDZ | Universal Scene Descrizione Archivio ZIP | model/vnd.usdz+zip | *Sostegno solo all&#39;acquisizione; non è disponibile alcuna visualizzazione o interazione.* USDZ è un formato 3D proprietario che può essere visualizzato in modo nativo dai dispositivi Safari e iOS. |

## Avvio rapido: Risorse 3D in Dynamic Media {#quick-start-three-d}

La seguente descrizione dettagliata del flusso di lavoro è stata progettata per aiutarti a iniziare rapidamente a usare le risorse 3D in modalità Dynamic Media - Scene7.

>[!IMPORTANT]
>
>Le risorse 3D non sono supportate in Dynamic Media - Modalità ibrida.

Prima di lavorare con le risorse 3D in Dynamic Media, accertati che il tuo amministratore di Experience Manager abbia già abilitato e configurato i Cloud Services Dynamic Media in modalità Dynamic Media - Scene7.

Vedi [Cloud Services ConfiguraE Dynamic Media](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services) in Configurazione di Dynamic Media - Modalità Scene7 e [Risoluzione dei problemi Dynamic Media - Modalità Scene7](/help/assets/troubleshoot-dms7.md).

1. **Caricare risorse 3D**

   * [Caricare le risorse 3D da utilizzare in Dynamic Media](/help/assets/manage-assets.md#uploading-assets).
   * [Formati di file 3D supportati per il caricamento in Dynamic Media](#supported-three-d-file-formats-in-dm).

1. **Gestione delle risorse 3D**

   * Organizzare e cercare risorse 3D

      * [Organizzare le risorse digitali](/help/assets/organize-assets.md#organize-digital-assets).
      * [Cercare risorse 3D](/help/assets/search-assets.md).
      * [Utilizzare predicati personalizzati per filtrare i risultati della ricerca](/help/assets/search-assets.md#custompredicates).
   * Visualizzare risorse 3D

      * [Visualizzare e interagire con le risorse 3D](#viewing-three-d-assets).
      * [Gestire il predefinito visualizzatore dimensionale](/help/assets/managing-viewer-presets.md).
   * Utilizzare i metadati delle risorse 3D

      * [Gestione dei metadati per le risorse digitali](/help/assets/metadata.md).
      * [Schemi metadati](/help/assets/metadata-schemas.md).



1. **Pubblicare risorse 3D**

   * [Pubblicare risorse statiche Dynamic Media 3D](#publishing-three-d-assets)
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
>Vedi [Gestire i predefiniti per visualizzatori](/help/assets/managing-viewer-presets.md).

## Visualizzare e interagire con una risorsa 3D dalla pagina dei dettagli della risorsa {#viewing-three-d-assets-from-asset-details-page}

Vedi anche [Anteprima delle risorse tramite l’interfaccia software](/help/assets/previewing-assets.md).

**Per visualizzare e interagire con una risorsa 3D dalla pagina dei dettagli della risorsa:**

1. Assicurati di aver caricato risorse 3D in Experience Manager.

   Vedi [Caricare le risorse 3D da utilizzare in Dynamic Media](/help/assets/manage-assets.md#uploading-assets).

1. Dall’Experience Manager, sul **[!UICONTROL Navigazione]** vai a **[!UICONTROL Risorse]** > **[!UICONTROL File]**.
1. Vicino all’angolo superiore destro della pagina, dal **[!UICONTROL Visualizza]** elenco a discesa, seleziona **[!UICONTROL Vista a schede]**.
1. Accedi alla risorsa 3D da visualizzare.
1. Seleziona la scheda della risorsa 3D.
1. Nella pagina di visualizzazione dei dettagli della risorsa 3D, effettua una delle seguenti operazioni:

   | Visualizzazione | Descrizione | Azione del mouse | Azione touch screen |
   | --- | --- | --- | --- |
   | **Girare la fotocamera** | Ruota la vista attorno agli oggetti e alla scena 3D. | Clic a sinistra + trascinamento. | Premere un dito singolo + trascinare. |
   | **Panning della fotocamera** | Consente di scorrere la visualizzazione a sinistra, a destra, in alto o in basso. | Fai clic con il pulsante destro del mouse e trascina. | Premere due dita + trascinare. |
   | **Zoom della fotocamera** | Spostarsi all&#39;interno e all&#39;esterno delle aree della scena 3D. | Ruota di scorrimento. | Pizzico a due dita. |
   | **Ricollegare la fotocamera** | Rientra la fotocamera in un punto di un oggetto nella scena 3D. | Fare doppio clic. | Tocca due volte. |
   | **Ripristina** | Nell’angolo in basso a destra della pagina, seleziona l’icona Ripristina per ripristinare il punto di destinazione della visualizzazione al centro della risorsa 3D. Inoltre, la funzione Reset sposta la telecamera più vicino o più lontano per mostrare la risorsa nella sua interezza e a una dimensione di visualizzazione ragionevole. |  |  |
   | **Modalità a tutto schermo** | Per passare alla modalità a tutto schermo, seleziona l’icona a schermo intero nell’angolo inferiore destro della pagina. |  |  |

1. Nell’angolo in alto a destra della pagina, seleziona **[!UICONTROL Chiudi]** per tornare alla pagina Risorse .

## Visualizzazione e interazione con una risorsa 3D all’interno di un componente Media 3D {#interacting-with-asset-inside-three-d-media-component}

Quando una pagina web si trova in **[!UICONTROL Modifica]** con una risorsa 3D non è possibile interagire. Per rendere la risorsa interattiva, puoi utilizzare la funzione **[!UICONTROL Anteprima]** per visualizzare la pagina web nell’editor di pagine con accesso completo alle funzionalità del componente Media 3D.

>[!IMPORTANT]
>
>Puoi eseguire questa operazione solo dopo aver aggiunto un componente Media 3D a una pagina web e assegnato una risorsa 3D al componente. Vedi [Aggiunta del componente Media 3D a una pagina web](#adding-the-three-d-media-component-to-a-web-page) e [Assegnazione di una risorsa 3D a un componente Media 3D](#assigning-a-three-d-asset-to-the-component).

Vedi anche [Anteprima delle risorse tramite l’interfaccia software](/help/assets/previewing-assets.md).

**Per visualizzare e interagire con una risorsa 3D all’interno di un componente File multimediali 3D:**

1. Mentre una pagina web si trova in **[!UICONTROL Modifica]** eseguire una delle operazioni seguenti:

   * In alto a destra nella pagina, seleziona **[!UICONTROL Anteprima]** per immettere **[!UICONTROL Anteprima]** modalità.
   * Elimina `/editor.html` dall’URL della pagina nel browser.

Una risorsa 3D completamente interattiva come visualizzata in    ![Risorsa 3D visualizzata all’interno del componente Media 3D](/help/assets/assets-dm/3d-asset-in-3d-media.png)
Una risorsa 3D completamente interattiva come visualizzata in **[!UICONTROL Anteprima]** modalità.

1. Quando **[!UICONTROL Anteprima]** eseguire una delle operazioni seguenti:

   | Visualizzazione | Descrizione | Azione del mouse | Azione touch screen |
   | --- | --- | --- | --- |
   | **Girare la fotocamera** | Ruota la vista attorno agli oggetti e alla scena 3D. | Clic a sinistra + trascinamento. | Premere un dito singolo + trascinare. |
   | **Panning della fotocamera** | Consente di scorrere la visualizzazione a sinistra, a destra, in alto o in basso. | Fai clic con il pulsante destro del mouse e trascina. | Premere due dita + trascinare. |
   | **Zoom della fotocamera** | Spostarsi all&#39;interno e all&#39;esterno delle aree della scena 3D. | Ruota di scorrimento. | Pizzico a due dita. |
   | **Ricollegare la fotocamera** | Rientra la fotocamera in un punto di un oggetto nella scena 3D. | Fare doppio clic. | Tocca due volte. |
   | **Ripristina** | Nell’angolo in basso a destra della pagina, seleziona l’icona Ripristina per ripristinare il punto di destinazione della visualizzazione al centro della risorsa 3D. Inoltre, la funzione Reset sposta la telecamera più vicino o più lontano per mostrare la risorsa nella sua interezza e a una dimensione di visualizzazione ragionevole. |  |  |
   | **Modalità a tutto schermo** | Per passare alla modalità a tutto schermo, seleziona l’icona a schermo intero nell’angolo inferiore destro della pagina. |  |  |

## Utilizzo del componente File multimediali 3D {#working-with-three-d-media-component}

Dynamic Media include un componente Media 3D di Dynamic Media che può essere utilizzato in Adobe Experience Manager Sites per abilitare la visualizzazione interattiva dei modelli 3D sulle pagine web.

* [Aggiungi il componente Media 3D al modello di pagina](#adding-three-d-media-component-to-page-template)
* [Aggiungere il componente Media 3D a una pagina web](#adding-the-three-d-media-component-to-a-web-page)
   * [Facoltativo - Configura il componente File multimediali 3D](#configuring-the-three-d-component)
* [Assegnare una risorsa 3D al componente File multimediali 3D](#assigning-a-three-d-asset-to-the-component)

## Aggiungi il componente Media 3D al modello di pagina {#adding-three-d-media-component-to-page-template}

1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Generale]** > **[!UICONTROL Modelli]**.
1. Passa al modello di pagina in cui desideri abilitare il componente 3D e seleziona il modello.
1. Seleziona **[!UICONTROL Modifica]** quindi potete aprire il modello.
1. Nel menu a discesa visualizzato in alto a destra della pagina, seleziona **[!UICONTROL Struttura]** se non è già attiva.

   ![3d-media-component-structure](/help/assets/assets-dm/3d-media-component-structure.png)

1. Selezionare un&#39;area vuota nel **[!UICONTROL Contenitore di layout]** selezionare e aprire la relativa barra degli strumenti associata.
1. Nella barra degli strumenti, seleziona la **[!UICONTROL Criterio]** per aprire **[!UICONTROL Editor criteri]**.
1. In **[!UICONTROL Proprietà]** nella sezione **[!UICONTROL Componenti consentiti]** scheda , scorri fino a **[!UICONTROL Dynamic Media]**, quindi espandi l’elenco e controlla **[!UICONTROL Supporti 3D]**.
1. Seleziona **[!UICONTROL Fine]** per salvare le modifiche e chiudere il **[!UICONTROL Editor criteri]**.

   Ora puoi posizionare il componente Media 3D di Dynamic Media su tutte le pagine che utilizzano questo modello.

## Aggiungere il componente Media 3D in una pagina web {#adding-the-three-d-media-component-to-a-web-page}

Se utilizzi Experience Manager come sistema di gestione dei contenuti web, puoi aggiungere risorse 3D alle pagine web tramite il componente Media 3D.

Vedi anche [Aggiungere risorse Dynamic Media nelle pagine](/help/assets/adding-dynamic-media-assets-to-pages.md).

**Per aggiungere il componente Media 3D in una pagina web:**

1. Apri Experience Manager Sites e seleziona la pagina web a cui desideri aggiungere il componente Media 3D di Dynamic Media.
1. Seleziona la **[!UICONTROL Modifica]** (matita) per aprire la pagina nell’editor di pagine. Assicurati che **[!UICONTROL Modifica]** viene selezionata vicino alla parte superiore destra della pagina.

   ![3d-media-component-add](/help/assets/assets-dm/3d-media-component-edit.png)

1. Nella barra degli strumenti, seleziona l’icona Pannello laterale per attivare o disattivare la visualizzazione del pannello.

1. Nel pannello laterale, seleziona l’icona del segno più per aprire il **[!UICONTROL Componenti]** elenco.

   ![3d-media-component-drag-drop](/help/assets/assets-dm/3d-assets-filter.png)

1. Trascina **[!UICONTROL Supporti 3D]** dal **[!UICONTROL Componenti]** nella posizione della pagina in cui si desidera visualizzare il visualizzatore 3D.

Ora puoi assegnare una risorsa 3D al componente.

Vedi [Assegnare una risorsa 3D al componente File multimediali 3D](#assigning-a-three-d-asset-to-the-component).

### Facoltativo - Configura il componente File multimediali 3D {#configuring-the-three-d-component}

1. Nell’editor pagina di Experience Manager Sites, seleziona il **[!UICONTROL Visualizzatore multimediale 3D]** componente precedentemente aggiunto alla pagina.
1. Seleziona la **[!UICONTROL Configurazione]** icona (chiave inglese) per aprire la finestra di dialogo di configurazione del componente.

   ![3d-media-component-config](/help/assets/assets-dm/3d-media-component-config.png)

1. Nell’elenco a discesa Predefinito visualizzatore della finestra di dialogo File multimediali 3D , seleziona **[!UICONTROL Dimensionale]** per assegnare il predefinito visualizzatore dimensionale al componente.

   ![3d-media-component-edit-config](/help/assets/assets-dm/3d-media-component-edit-config.png)

1. Nell’angolo in alto a destra, seleziona il segno di spunta per salvare le modifiche.

## Assegnare una risorsa 3D al componente File multimediali 3D {#assigning-a-three-d-asset-to-the-component}

Dopo aver aggiunto un componente Media 3D a una pagina web, puoi assegnargli una risorsa 3D.

Vedi [Aggiungere il componente Media 3D a una pagina web](#adding-the-three-d-media-component-to-a-web-page).

**Per assegnare una risorsa 3D al componente File multimediali 3D:**

1. Nell’editor pagina di Experience Manager Sites, seleziona il **[!UICONTROL Risorse]** icona per aprire **[!UICONTROL Risorse]** nel pannello laterale.
1. Nell’elenco a discesa , seleziona **[!UICONTROL 3D]** per mostrare solo i tipi di file di risorse 3D.
1. Nel pannello laterale, cerca o scorri fino alla risorsa 3D che desideri visualizzare sulla pagina da modificare.
1. Trascina la risorsa 3D dal pannello laterale Risorse e rilasciala sul pannello **[!UICONTROL Supporti 3D]** componente precedentemente aggiunto alla pagina.

   ![Assegnare risorse 3D al componente File multimediali 3D](/help/assets/assets-dm/3d-asset-add.png)

>[!NOTE]
>
>Mentre una pagina web si trova in Experience Manager Sites **[!UICONTROL Modifica]** In modalità 3D Media, il componente File multimediali 3D visualizza la risorsa 3D ma non è possibile interagire con essa. Per rendere la risorsa interattiva, puoi utilizzare la funzione **[!UICONTROL Anteprima]** per visualizzare la pagina web nell’editor di pagine con accesso completo alle funzionalità del componente Media 3D.

## Pubblicare risorse statiche Dynamic Media 3D {#publishing-three-d-assets}

Dynamic Media accetta vari formati di file 3D supportati come *contenuto statico* in Dynamic Media. Il contenuto statico consente di caricare e pubblicare risorse 3D, ma non è disponibile il supporto per *imaging a variabili* o la sostituzione dell’immagine associata alla risorsa 3D. Il motivo è che Dynamic Media Imaging Server non riconosce i formati 3D. Di conseguenza, dopo aver pubblicato una risorsa 3D in Dynamic Media, disponi di un URL istantaneo che puoi copiare. L’URL della risorsa 3D segue la consueta struttura URL di Dynamic Media. Tuttavia, non puoi modificare alcun parametro nell’URL della risorsa, a differenza delle risorse di immagini tradizionali in Dynamic Media.

Vedi anche [Ottenere un URL per una risorsa statica](/help/assets/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-a-static-asset).

In **[!UICONTROL Vista a schede]**, sotto il nome di una risorsa viene visualizzata una piccola icona a forma di globo, a sinistra della data e dell’ora per indicare che è stata pubblicata. Nella **[!UICONTROL Vista a elenco]**, la colonna **[!UICONTROL Pubblicato]** indica lo stato di pubblicazione delle risorse.

Se utilizzi Experience Manager come WCM, utilizza questo metodo di pubblicazione per aggiungere le risorse 3D di Dynamic Media direttamente sulla tua pagina web.

Vedi anche [Pubblicare risorse Dynamic Media](publishing-dynamicmedia-assets.md).

Vedi anche [Pubblicare pagine](/help/sites-authoring/publishing-pages.md).

**Per pubblicare risorse 3D statiche di Dynamic Media:**

1. Apri una risorsa 3D (formato di file GLB, OBJ o STL) per visualizzarla nella pagina dei dettagli della risorsa.
1. Sulla barra degli strumenti, seleziona **[!UICONTROL Pubblicazione rapida]**.

   ![3d-asset-quick-publish](/help/assets/assets-dm/3d-asset-quick-publish.png)

1. Seleziona **[!UICONTROL Chiudi]** per uscire dalla finestra di dialogo e tornare alla pagina dei dettagli della risorsa.
1. Dall’elenco a discesa a sinistra del nome del file della risorsa 3D, seleziona **[!UICONTROL Rendering]**.

   ![3d-asset-rendering](/help/assets/assets-dm/3d-asset-renditions.png)

1. Seleziona **[!UICONTROL originale]**. Quando una risorsa 3D viene pubblicata (o &quot;attivata&quot;), la **[!UICONTROL URL]** viene visualizzato vicino all’angolo in basso a sinistra della pagina se sono soddisfatte tutte le seguenti condizioni della risorsa 3D:
   * Il asset 3D è un formato supportato (GLB, OBJ, STL e USDZ).
   * La risorsa 3D è stata assimilata in Dynamic Media Image Production System (IPS).
   * La risorsa 3D viene pubblicata.

   ![3d-asset-url](/help/assets/assets-dm/3d-asset-url.png)

1. Seleziona **[!UICONTROL URL]** così puoi visualizzare l’URL di produzione diretta della risorsa 3D che puoi copiare e utilizzare sulle pagine web.

### Metodi alternativi per la pubblicazione di risorse 3D Dynamic Media utilizzando il visualizzatore dimensionale {#alternate-publish-methods}

Utilizza i due metodi seguenti per pubblicare le risorse 3D di Dynamic Media se lo fai *not* utilizza Experience Manager come WCM.

* **[!UICONTROL URL]** - Utilizzo **[!UICONTROL URL]** se utilizzi un sistema di gestione dei contenuti web di terze parti e desideri collegare risorse Dynamic Media 3D alle tue pagine web utilizzando il visualizzatore dimensionale.

   Vedi [Collegare gli URL all’applicazione web](/help/assets/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset).

* **[!UICONTROL Incorpora]** - Utilizzo **[!UICONTROL Incorpora]** per visualizzare una risorsa Dynamic Media 3D incorporata in una pagina web utilizzando il visualizzatore dimensionale. Puoi copiare il codice da incorporare negli Appunti, per poi incollarlo nelle pagine web. La modifica del codice non è consentita nel **[!UICONTROL Incorpora]** finestra di dialogo.

   Vedi [Incorporare un visualizzatore video, immagine o dimensionale di Dynamic Media in una pagina web](/help/assets/embed-code.md#embedding-the-video-or-image-viewer-on-a-web-page).
