---
title: Selettore risorse
description: Scopri come utilizzare il selettore risorse per cercare, filtrare, sfogliare e recuperare i metadati delle risorse in Adobe Experience Manager Assets. Scopri anche come personalizzare l’interfaccia del selettore delle risorse.
contentOwner: Adobe
feature: Asset Management,Metadata,Search
role: User
hide: true
exl-id: c84ce84a-1e52-48fd-a16c-38c7769df9af
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 2%

---

# Selettore risorse {#asset-selector}

>[!NOTE]
>
>Il [selettore risorse](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/asset-selector.html?lang=it) è stato chiamato [Selettore risorse](https://helpx.adobe.com/it/experience-manager/6-2/assets/using/asset-picker.html) nelle versioni precedenti di [!DNL Experience Manager].

Il selettore risorse consente di sfogliare, cercare e filtrare le risorse in [!DNL Adobe Experience Manager] Assets. Puoi anche recuperare i metadati delle risorse selezionate utilizzando il selettore risorse. Per personalizzare l’interfaccia del selettore risorse, puoi avviarla con parametri di richiesta supportati. Questi parametri impostano il contesto del selettore risorse per uno scenario particolare.

Al momento, è possibile passare i parametri di richiesta `assettype` (*Immagine/Video/Testo*) e la selezione `mode` (*Singolo/Multiplo*) come informazioni contestuali per il selettore risorse, che rimangono intatte in tutta la selezione.

Il selettore risorse utilizza il messaggio HTML5 **Window.postMessage** per inviare i dati della risorsa selezionata al destinatario.

Il selettore delle risorse si basa sul vocabolario del selettore delle fondamenta di Granite. Per impostazione predefinita, il selettore risorse funziona in modalità Sfoglia. Tuttavia, puoi applicare i filtri utilizzando l’esperienza Omnisearch per perfezionare la ricerca di determinate risorse.

È possibile integrare qualsiasi pagina Web (indipendentemente dal fatto che faccia parte del contenitore CQ) con il selettore risorse (`https://[AEM_server]:[port]/aem/assetpicker.html`).

## Parametri contestuali {#contextual-parameters}

Per avviare il selettore risorse in un determinato contesto, puoi trasmettere i seguenti parametri di richiesta in un URL:

| Nome | Valori | Esempio | Scopo |
|---|---|---|---|
| suffisso risorsa (B) | Percorso della cartella come suffisso di risorsa nell&#39;URL:`http://localhost:4502/aem/`<br>`assetpicker.html/<folder_path>` | Per avviare il selettore risorse con una particolare cartella selezionata, ad esempio con la cartella `/content/dam/we-retail/en/activities` selezionata, l&#39;URL deve essere nel formato: `http://localhost:4502/aem/assetpicker.html`<br>`/content/dam/we-retail/en/activities?assettype=images` | Se devi selezionare una particolare cartella all&#39;avvio del selettore di risorse, trasmettila come suffisso di risorsa. |
| modalità | singolo, multiplo | `http://localhost:4502/aem/assetpicker.html`<br>`?mode=multiple` <br> `http://localhost:4502/aem/assetpicker.html`<br>`?mode=single` | In modalità multipla, puoi selezionare più risorse contemporaneamente utilizzando il selettore risorse. |
| finestra di dialogo | true, false | `http://localhost:4502/aem/assetpicker.html`<br>`?dialog=true` | Utilizza questi parametri per aprire il selettore risorse come finestra di dialogo Granite. Questa opzione è applicabile solo quando avvii il selettore risorse tramite il campo Percorso Granite e lo configuri come URL pickerSrc. |
| radice | `<folder_path>` | `http://localhost:4502/aem/`<br>`assetpicker.html?assettype=images`<br>`&root=/content/dam/we-retail/en/activities` | Utilizza questa opzione per specificare la cartella principale per il selettore risorse. In questo caso, il selettore delle risorse consente di selezionare solo le risorse figlie (dirette/indirette) sotto la cartella principale. |
| viewmode | ricerca |  | Per avviare il selettore risorse in modalità di ricerca, con i parametri assettype e mimetype. |
| assettipo (S) | immagini, documenti, elementi multimediali, archivi | <ul><li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=images`</li> <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=documents`</li> <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=multimedia`</li> <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=archives`</li> | Utilizza questa opzione per filtrare i tipi di risorse in base al valore passato. |
| mimetype | mimetype (`/jcr:content/metadata/dc:format`) di una risorsa (supporto di caratteri jolly incluso) | <ul><li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&mimetype=image/png`</li>  <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&?mimetype=*png`</li>  <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&mimetype=*presentation`</li>  <li>`http://localhost:4502/aem/assetpicker?viewmode=search&mimetype=*presentation&mimetype=*png`</li></ul> | Utilizzala per filtrare le risorse in base ai tipi MIME |

## Utilizzare il selettore risorse {#using-the-asset-selector}

1. Per accedere all&#39;interfaccia del selettore risorse, passa a `https://[AEM_server]:[port]/aem/assetpicker`.
1. Passa alla cartella desiderata e seleziona una o più risorse.

   ![chlimage_1-441](assets/chlimage_1-441.png)

   In alternativa, puoi cercare la risorsa desiderata dalla casella OmniSearch e selezionarla.

   ![chlimage_1-442](assets/chlimage_1-442.png)

   Se cerchi risorse utilizzando la casella OmniSearch, puoi selezionare vari filtri dal riquadro **[!UICONTROL Filtri]** per perfezionare la ricerca.

   ![chlimage_1-443](assets/chlimage_1-443.png)

1. Fai clic su **[!UICONTROL Seleziona]** nella barra degli strumenti.

>[!MORELIKETHIS]
>
>* [Selettore risorse micro-front-end in AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/asset-selector.html?lang=it)
