---
title: Selettore risorse
description: Scopri come utilizzare il selettore risorse per cercare, filtrare, sfogliare e recuperare i metadati delle risorse in Adobe Experience Manager Assets. Scopri anche come personalizzare l’interfaccia del selettore delle risorse.
contentOwner: Adobe
feature: Asset Management,Metadata,Search
role: User
exl-id: 4b518ac0-5b8b-4d61-ac31-269aa1f5abe4
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 2%

---

# Selettore risorse {#asset-selector}

>[!NOTE]
>
>Il selettore delle risorse è stato chiamato [Selettore risorse](https://helpx.adobe.com/experience-manager/6-2/assets/using/asset-picker.html) nelle versioni precedenti di [!DNL Experience Manager].

Il selettore delle risorse consente di sfogliare, cercare e filtrare le risorse in [!DNL Adobe Experience Manager] Risorse. Puoi anche recuperare i metadati delle risorse selezionate utilizzando il selettore risorse. Per personalizzare l’interfaccia del selettore risorse, puoi avviarla con parametri di richiesta supportati. Questi parametri impostano il contesto del selettore risorse per uno scenario particolare.

Al momento, puoi trasmettere i parametri della richiesta `assettype` (*Immagine/Video/Testo*) e selezione `mode` (*Singolo/Multiplo*) come informazioni contestuali per il selettore risorse, che rimangono intatte per tutta la selezione.

Il selettore risorse utilizza HTML5 **Window.postMessage** messaggio per inviare al destinatario i dati per la risorsa selezionata.

Il selettore delle risorse si basa sul vocabolario del selettore delle fondamenta di Granite. Per impostazione predefinita, il selettore risorse funziona in modalità Sfoglia. Tuttavia, puoi applicare i filtri utilizzando l’esperienza Omnisearch per perfezionare la ricerca di determinate risorse.

Puoi integrare qualsiasi pagina web (indipendentemente dal fatto che faccia parte del contenitore CQ) con il selettore risorse (`https://[AEM_server]:[port]/aem/assetpicker.html`).

## Parametri contestuali {#contextual-parameters}

Per avviare il selettore risorse in un determinato contesto, puoi trasmettere i seguenti parametri di richiesta in un URL:

| Nome | Valori | Esempio | Scopo |
|---|---|---|---|
| suffisso risorsa (B) | Percorso della cartella come suffisso della risorsa nell’URL:`http://localhost:4502/aem/`<br>`assetpicker.html/<folder_path>` | Per avviare il selettore risorse con una particolare cartella selezionata, ad esempio con la cartella `/content/dam/we-retail/en/activities` selezionato, l’URL deve essere nel formato: `http://localhost:4502/aem/assetpicker.html`<br>`/content/dam/we-retail/en/activities?assettype=images` | Se devi selezionare una particolare cartella all&#39;avvio del selettore di risorse, trasmettila come suffisso di risorsa. |
| modalità | singolo, multiplo | `http://localhost:4502/aem/assetpicker.html`<br>`?mode=multiple` <br> `http://localhost:4502/aem/assetpicker.html`<br>`?mode=single` | In modalità multipla, puoi selezionare più risorse contemporaneamente utilizzando il selettore risorse. |
| finestra di dialogo | true, false | `http://localhost:4502/aem/assetpicker.html`<br>`?dialog=true` | Utilizza questi parametri per aprire il selettore risorse come finestra di dialogo Granite. Questa opzione è applicabile solo quando avvii il selettore risorse tramite il campo Percorso Granite e lo configuri come URL pickerSrc. |
| radice | `<folder_path>` | `http://localhost:4502/aem/`<br>`assetpicker.html?assettype=images`<br>`&root=/content/dam/we-retail/en/activities` | Utilizza questa opzione per specificare la cartella principale per il selettore risorse. In questo caso, il selettore delle risorse consente di selezionare solo le risorse figlie (dirette/indirette) sotto la cartella principale. |
| viewmode | ricerca |  | Per avviare il selettore risorse in modalità di ricerca, con i parametri assettype e mimetype. |
| assettipo (S) | immagini, documenti, elementi multimediali, archivi | <ul><li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=images`</li> <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=documents`</li> <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=multimedia`</li> <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=archives`</li> | Utilizza questa opzione per filtrare i tipi di risorse in base al valore passato. |
| mimetype | tipo/i mime (`/jcr:content/metadata/dc:format`) di una risorsa (è supportato anche un carattere jolly) | <ul><li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&mimetype=image/png`</li>  <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&?mimetype=*png`</li>  <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&mimetype=*presentation`</li>  <li>`http://localhost:4502/aem/assetpicker?viewmode=search&mimetype=*presentation&mimetype=*png`</li></ul> | Utilizzala per filtrare le risorse in base ai tipi MIME |

## Utilizzare il selettore risorse {#using-the-asset-selector}

1. Per accedere all’interfaccia del selettore delle risorse, vai a `https://[AEM_server]:[port]/aem/assetpicker`.
1. Passa alla cartella desiderata e seleziona una o più risorse.

   ![chlimage_1-441](assets/chlimage_1-441.png)

   In alternativa, puoi cercare la risorsa desiderata dalla casella OmniSearch e selezionarla.

   ![chlimage_1-442](assets/chlimage_1-442.png)

   Se si cercano risorse utilizzando la casella OmniSearch, è possibile selezionare vari filtri dalla casella **[!UICONTROL Filtri]** per perfezionare la ricerca.

   ![chlimage_1-443](assets/chlimage_1-443.png)

1. Clic **[!UICONTROL Seleziona]** dalla barra degli strumenti.
