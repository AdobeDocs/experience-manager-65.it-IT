---
title: Risorse [!DNL Adobe Stock] di gestione
description: Cercare, recuperare, ottenere licenze e [!DNL Adobe Stock] gestire risorse dall'interno [!DNL Adobe Experience Manager]. Utilizzate le risorse con licenza come qualsiasi altra risorsa digitale.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 12c56c27c7f97f1029c757ec6d28f482516149d0
workflow-type: tm+mt
source-wordcount: '1080'
ht-degree: 13%

---


# Usa [!DNL Adobe Stock] risorse in [!DNL Adobe Experience Manager Assets] {#use-adobe-stock-assets-in-aem-assets}

Le organizzazioni possono integrare il piano [!DNL Adobe Stock] aziendale con [!DNL Experience Manager Assets] l&#39;obiettivo di garantire che le risorse concesse in licenza siano ampiamente disponibili per i loro progetti creativi e di marketing, con le potenti funzionalità di gestione delle risorse di [!DNL Experience Manager].

[!DNL Adobe Stock]Il servizio offre a designer e aziende l’accesso a milioni di foto, immagini vettoriali, illustrazioni, video, modelli e risorse 3D di alta qualità, curate ed esenti da royalty, per qualsiasi progetto creativo. [!DNL Experience Manager] gli utenti possono trovare, visualizzare in anteprima e concedere in licenza [!DNL Adobe Stock] le risorse salvate in [!DNL Experience Manager], senza uscire dall&#39; [!DNL Experience Manager] interfaccia.

## Prerequisiti {#prerequisites}

L&#39;integrazione richiede un [ [!DNL Adobe Stock] piano aziendale](https://stockenterprise.adobe.com/).

## Integrare [!DNL Experience Manager] e [!DNL Adobe Stock] {#integrate-aem-and-adobe-stock}

Per consentire la comunicazione tra [!DNL Experience Manager] e [!DNL Adobe Stock], create una configurazione IMS e una [!DNL Adobe Stock] configurazione in [!DNL Experience Manager].

>[!NOTE]
>
>Solo [!DNL Experience Manager] gli amministratori e [!DNL Admin Console] gli amministratori di un&#39;organizzazione possono eseguire l&#39;integrazione in quanto richiede privilegi di amministratore.

### Create an IMS configuration {#create-an-ims-configuration}

1. In the [!DNL Experience Manager] user interface, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**. Fai clic su **[!UICONTROL Crea]** e seleziona **[!UICONTROL Soluzione cloud]** > **[!UICONTROL Adobe Stock]**.
1. Riutilizzate un certificato esistente o selezionate **[!UICONTROL Crea nuovo certificato]**.
1. Fai clic su **[!UICONTROL Crea certificato]**. Una volta creata, scaricate la chiave pubblica. Fai clic su **[!UICONTROL Avanti]**.
1. Aggiungete la chiave pubblica scaricata al vostro account di [!DNL Adobe Developer Console] servizio. Fai clic su **[!UICONTROL Avanti]**. Lasciate aperta la schermata Configurazione [!UICONTROL account tecnico IMS del Adobe] per fornire i valori a breve.
1. Accedere [console](https://console.adobe.io)Sviluppatore di Adobe. Assicuratevi che l&#39;account disponga delle autorizzazioni di amministratore per l&#39;organizzazione per la quale è richiesta l&#39;integrazione.
1. Fate clic su **[!UICONTROL Crea nuovo progetto]** e fate clic su **[!UICONTROL Aggiungi API]**. Selezionate **[!UICONTROL Adobe Stock]** dall&#39;elenco delle API disponibili. Selezionare [!UICONTROL OAUTH 2.0 Web]. Configurare e copiare i vari valori presentati.
1. In [!DNL Experience Manager] provide the values in the fields titled **[!UICONTROL Title]**, **[!UICONTROL Authorization Server]**, **[!UICONTROL API Key]**, **[!UICONTROL Client Secret]**, and **[!UICONTROL Payload]**. Per informazioni dettagliate su questi valori, consultate Avvio [rapido dell&#39;autenticazione](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWT.md)JWT.

<!-- TBD: Update the URL to update the terminology when AIO team updates their documentation URL. Logged issue github.com/AdobeDocs/adobeio-auth/issues/63.
-->

### Crea [!DNL Adobe Stock] configurazione in [!DNL Experience Manager] {#create-adobe-stock-configuration-in-aem}

1. In the [!DNL Experience Manager], navigate to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**.
1. Fate clic su **[!UICONTROL Crea]** per creare una configurazione e associarla alla configurazione IMS esistente. Selezionate `PROD` come parametro di ambiente.
1. Nel campo Percorso **[!UICONTROL risorse]** concesso in licenza, lasciare invariata la posizione. Non modificate il percorso in cui desiderate memorizzare le [!DNL Adobe Stock] risorse.
1. Completate la creazione aggiungendo tutte le proprietà richieste. Fai clic su **[!UICONTROL Salva e chiudi]**.
1. Aggiungete [!DNL Experience Manager] utenti o gruppi che possono ottenere la licenza per le risorse.

>[!NOTE]
>
>Se sono presenti più [!DNL Adobe Stock] configurazioni, selezionate la configurazione desiderata nel pannello Preferenze  utente. Per accedere al pannello dalla [!DNL Experience Manager] home page, fai clic sull’icona utente, quindi fai clic su Preferenze **** utente > Configurazione **** Stock.

## Utilizzare e gestire [!DNL Adobe Stock] le risorse in [!DNL Experience Manager] {#usemanage}

Grazie a questa funzione, le organizzazioni possono consentire agli utenti di utilizzare [!DNL Adobe Stock] le risorse in [!DNL Experience Manager Assets]. Dall’interfaccia [!DNL Experience Manager] utente, gli utenti possono cercare [!DNL Adobe Stock] le risorse e ottenere la licenza per le risorse necessarie.

Una volta ottenuta la licenza di una [!DNL Adobe Stock] risorsa in [!DNL Experience Manager], questa può essere utilizzata e gestita come una risorsa tipica. In [!DNL Experience Manager]potete cercare e visualizzare in anteprima le risorse; copiare e pubblicare le risorse; condividere le attività su [!DNL Brand Portal]; accedere e utilizzare le risorse tramite l’app [!DNL Experience Manager] desktop; e così via.

![Cercare [!DNL Adobe Stock] risorse e filtrare i risultati dall’ [!DNL Adobe Experience Manager] area di lavoro](assets/adobe-stock-search-results-workspace.png)

*Figura: Cercate [!DNL Adobe Stock] le risorse e i risultati del filtro dall’ [!DNL Experience Manager] interfaccia.*

**A.**[!DNL Adobe Stock] Cerca risorse simili a quelle di chi è fornito l’ID **B.** Cerca risorse corrispondenti alla tua selezione di forma o orientamento. **C.** Cerca uno o più dei tipi di risorse supportati **D.** Apri o comprimi il riquadro Filtri **E.** Procurati la licenza relativa e salva la risorsa selezionata in [!DNL Experience Manager]**F.**[!DNL Experience Manager] Salva la risorsa in applicando la filigrana **G.**[!DNL Adobe Stock] Sul sito web di , esplora le risorse simili a quella selezionata **H.**[!DNL Adobe Stock] Visualizza le risorse selezionate sul sito web di **I.** Numero di risorse selezionate proveniente dai risultati della ricerca **J.** Passaggio tra la vista a schede e la vista a elenco

### Trovare le risorse {#find-assets}

Gli [!DNL Experience Manager] utenti possono cercare le risorse sia in [!DNL Experience Manager] che [!DNL Adobe Stock]. Quando il percorso di ricerca non è limitato a [!DNL Adobe Stock], i risultati della ricerca da [!DNL Experience Manager] e [!DNL Adobe Stock] vengono visualizzati.

* Per cercare [!DNL Adobe Stock] le risorse, fate clic su **[!UICONTROL Navigazione]** > **[!UICONTROL Risorse]** > **[!UICONTROL Cerca  Adobe Stock]**.

* Per cercare le risorse [!DNL Adobe Stock] e [!DNL Experience Manager Assets], fate clic su Cerca ![nella ricerca](assets/do-not-localize/search_icon.png).

In alternativa, iniziate a digitare `Location: Adobe Stock` nella barra di ricerca per selezionare [!DNL Adobe Stock] le risorse. [!DNL Experience Manager] offre funzionalità di filtro avanzate sulle risorse ricercate, che consentono agli utenti di accedere rapidamente alle risorse necessarie tramite filtri, quali tipi di risorse supportate, orientamento delle immagini e stato della licenza.

>[!NOTE]
>
>Assets searched from [!DNL Adobe Stock] are just displayed in [!DNL Experience Manager]. [!DNL Adobe Stock] le risorse vengono recuperate e memorizzate nell’ [!DNL Experience Manager] archivio solo dopo che un utente [salva una risorsa](/help/assets/aem-assets-adobe-stock.md#saveassets) o [le licenze e salva una risorsa](/help/assets/aem-assets-adobe-stock.md#licenseassets). Assets that are already stored in [!DNL Experience Manager] are displayed and highlighted for ease of reference and access. Also, the [!DNL Stock] assets are saved with some additional metadata to indicate the source as [!DNL Stock].

![Ricerca di filtri nelle risorse [!DNL Experience Manager] e evidenziate [!DNL Adobe Stock] nei risultati di ricerca](assets/aem-search-filters2.jpg)

*Figura: Consente di cercare i filtri nelle risorse [!DNL Experience Manager] evidenziate [!DNL Adobe Stock] nei risultati della ricerca.*

### Salvate e visualizzate le risorse richieste {#saveassets}

Selezionate una risorsa da salvare in [!DNL Experience Manager]. Fate clic su [!UICONTROL Salva] nella barra degli strumenti nella parte superiore e fornite il nome e la posizione della risorsa. Le risorse senza licenza vengono salvate localmente con una filigrana.

La prossima volta che ricercate le risorse, queste vengono evidenziate con un contrassegno, per indicare che sono disponibili in [!DNL Experience Manager Assets].

>[!NOTE]
>
>Le risorse aggiunte di recente visualizzano un nuovo contrassegno invece del contrassegno Con licenza.

### Risorse di licenza {#licenseassets}

Gli utenti possono concedere in licenza [!DNL Adobe Stock] le risorse utilizzando la quota del proprio piano [!DNL Adobe Stock] enterprise. Quando acquistate una licenza, la risorsa viene salvata senza filigrana ed è disponibile per la ricerca e l’utilizzo in [!DNL Experience Manager Assets].

![Finestra di dialogo per ottenere la licenza e salvare [!DNL Adobe Stock] le risorse in [!DNL Experience Manager Assets]](assets/aem-stock_licenseandsave.jpg)

*Figura: Finestra di dialogo per ottenere la licenza e salvare [!DNL Adobe Stock] le risorse in [!DNL Experience Manager Assets].*

### Accesso a metadati e proprietà delle risorse {#access-metadata-and-asset-properties}

Gli utenti possono accedere ai metadati e visualizzarne l’anteprima, comprese le proprietà dei [!DNL Adobe Stock] metadati per le risorse salvate in [!DNL Experience Manager], e aggiungere riferimenti **[!UICONTROL di]** licenza per una risorsa. Tuttavia, gli aggiornamenti al riferimento della licenza non vengono sincronizzati tra [!DNL Experience Manager] e il [!DNL Adobe Stock] sito Web.

Gli utenti possono visualizzare le proprietà per risorse con licenza e senza licenza.

![Visualizzare e accedere ai metadati e ai riferimenti di licenza delle risorse salvate](assets/metadata_properties.jpg)

*Figura: Visualizzare e accedere ai metadati e ai riferimenti di licenza delle risorse salvate.*

## Limitazioni note {#known-limitations}

* **L&#39;avviso dell&#39;immagine editoriale non viene visualizzato**: Quando si concede la licenza a un’immagine, gli utenti non possono verificare se un’immagine è solo di uso editoriale. Per evitare possibili abusi, gli amministratori possono disattivare l’accesso alle risorse editoriali dal Admin Console .

* **Viene visualizzato** un tipo di licenza errato: È possibile che per una risorsa venga visualizzato un tipo di licenza errato [!DNL Experience Manager] . Gli utenti possono accedere al [!DNL Adobe Stock] sito Web per visualizzare il tipo di licenza.

* **I campi e i metadati di riferimento non sono sincronizzati**: Quando un utente aggiorna un campo di riferimento della licenza, le informazioni di riferimento della licenza vengono aggiornate nel [!DNL Experience Manager] sito Web, ma non nel [!DNL Adobe Stock] sito Web. Analogamente, se l’utente aggiorna i campi di riferimento sul [!DNL Adobe Stock] sito Web, gli aggiornamenti non vengono sincronizzati in [!DNL Experience Manager].

>[!MORELIKETHIS]
>
>* [Esercitazione video sull’ [!DNL Adobe Stock] utilizzo delle risorse [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/creative-workflows/adobe-stock.html)
>* [[!DNL Adobe Stock] guida del piano aziendale](https://helpx.adobe.com/enterprise/using/adobe-stock-enterprise.html)
>* [[!DNL Adobe Stock] Domande frequenti](https://helpx.adobe.com/stock/faq.html)

