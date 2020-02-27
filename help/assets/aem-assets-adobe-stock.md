---
title: Gestione delle risorse Adobe Stock in Risorse AEM
description: Cercare, recuperare, ottenere licenze e gestire risorse Adobe Stock da AEM. Utilizzate le risorse con licenza come qualsiasi altra risorsa digitale.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 62e82b6da2a5f961acf8cbc30ad29b3c25b1ecef

---


# Use Adobe Stock assets in AEM Assets {#use-adobe-stock-assets-in-aem-assets}

Le organizzazioni possono integrare il piano aziendale Adobe Stock con Risorse AEM per garantire che le risorse su licenza siano ampiamente disponibili per i loro progetti creativi e di marketing, con le potenti funzionalità di gestione delle risorse di AEM.

Il servizio Adobe Stock offre a designer e aziende l’accesso a milioni di foto, immagini vettoriali, illustrazioni, video, modelli e risorse 3D di alta qualità, curate ed esenti da royalty, per qualsiasi progetto creativo. Gli utenti AEM possono trovare, visualizzare in anteprima e concedere in licenza rapidamente le risorse Adobe Stock salvate in AEM, senza uscire dall’area di lavoro di AEM.

## Prerequisiti {#prerequisites}

L’integrazione richiede un piano [Adobe Stock](https://stockenterprise.adobe.com/) aziendale e AEM 6.5 o versione successiva. Per informazioni dettagliate sul service pack di AEM 6.5, consultate queste note [sulla](/help/release-notes/sp-release-notes.md)versione.

## Integrazione di AEM e Adobe Stock {#integrate-aem-and-adobe-stock}

Per consentire la comunicazione tra AEM e Adobe Stock, crea una configurazione IMS e una configurazione Adobe Stock in AEM.

>[!NOTE]
>
>L’integrazione può essere eseguita solo dagli amministratori di AEM e di Admin Console per un’organizzazione, in quanto richiede privilegi di amministratore.

### Creare una configurazione IMS {#create-an-ims-configuration}

1. Fai clic sul logo AEM. Seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Protezione]** > **[!UICONTROL Configurazioni Adobe IMS]**. Fai clic su **[!UICONTROL Crea]** e seleziona **[!UICONTROL Soluzione cloud]** > **[!UICONTROL Adobe Stock]**.
1. Riutilizzate un certificato esistente o selezionate **[!UICONTROL Crea nuovo certificato]**.
1. Fate clic su **[!UICONTROL Crea certificato]**. Una volta creata, scaricate la chiave pubblica. Fai clic su **[!UICONTROL Avanti]**.
1. Inserisci i valori appropriati nei campi **[!UICONTROL Titolo]**, **[!UICONTROL Server autorizzazioni]**, **[!UICONTROL Chiave API]**, **[!UICONTROL Segreto client]** e **[!UICONTROL Payload]**. Per informazioni dettagliate su come recuperare questi valori dall’I/O di Adobe, consulta la sezione [JWT authentication quick start (Avvio rapido di authentication JWT)](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWT.md).
1. Aggiungi la chiave pubblica scaricata al tuo account del servizio Adobe I/O.

### Creare la configurazione di Adobe Stock in AEM {#create-adobe-stock-configuration-in-aem}

1. Nell’interfaccia utente di AEM, passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**.
1. Fate clic su **[!UICONTROL Crea]** per creare una configurazione e associarla alla configurazione IMS esistente. Selezionate `PROD` come parametro di ambiente.
1. Nel campo Percorso **[!UICONTROL risorse]** concesso in licenza, lasciare invariata la posizione. Non cambiare la posizione in cui memorizzare le risorse Adobe Stock.
1. Completate la creazione aggiungendo tutte le proprietà richieste. Fate clic su **[!UICONTROL Salva e chiudi]**.
1. Aggiungete utenti o gruppi AEM che possono ottenere la licenza per le risorse.

>[!NOTE]
>
>Se sono presenti più configurazioni Adobe Stock, seleziona la configurazione desiderata nel pannello Preferenze  utente facendo clic sul logo AEM nell’interfaccia utente di AEM.

## Utilizzo e gestione di risorse Adobe Stock in AEM {#usemanage}

Grazie a questa funzionalità, le organizzazioni possono consentire ai propri utenti di utilizzare le risorse Adobe Stock in Risorse AEM. Dall’interfaccia utente di AEM, gli utenti possono effettuare ricerche nelle risorse Adobe Stock e ottenere la licenza per le risorse richieste.

Una volta ottenuta la licenza di una risorsa Adobe Stock in AEM, questa può essere utilizzata e gestita come una risorsa tipica. In AEM, gli utenti possono cercare e visualizzare in anteprima le risorse; copiare e pubblicare le risorse; condividere le risorse su Brand Portal; accedere e utilizzare le risorse tramite l’app desktop AEM; e così via.

![Cercare risorse Adobe Stock e filtrare i risultati dall’area di lavoro AEM](assets/adobe-stock-search-results-workspace.png)

*Figura: Cercare risorse Adobe Stock e filtrare i risultati dall’area di lavoro AEM*

**A.** Cerca risorse simili a quelle di chi è fornito l’ID Adobe Stock. **B.** Cerca risorse corrispondenti alla tua selezione di forma o orientamento. **C.** Cerca uno o più dei tipi di risorse supportati **D.** Apri o comprimi il riquadro Filtri **E.** Procurati la licenza relativa e salva la risorsa selezionata in AEM **F.** Salva la risorsa in AEM applicando la filigrana **G.** Sul sito web di Adobe Stock, esplora le risorse simili a quella selezionata **H.** Visualizza le risorse selezionate sul sito web di Adobe Stock **I.** Numero di risorse selezionate proveniente dai risultati della ricerca **J.** Passaggio tra la vista a schede e la vista a elenco

### Trovare le risorse {#find-assets}

Gli utenti AEM possono cercare risorse sia in AEM che in Adobe Stock. Quando il percorso di ricerca non è limitato ad Adobe Stock, vengono visualizzati i risultati di ricerca di AEM e Adobe Stock.

* Per cercare risorse Adobe Stock, fai clic su **[!UICONTROL Navigazione]** > **[!UICONTROL Risorse]** > **[!UICONTROL Cerca in Adobe Stock]**.

* Per cercare risorse in Adobe Stock e AEM Assets, fai clic sull’icona di ricerca ![search_icon](assets/search_icon.png).

In alternativa, iniziate a digitare `Location: Adobe Stock` nella barra di ricerca per selezionare le risorse Adobe Stock.  AEM offre funzionalità di filtraggio avanzate sulle risorse ricercate, consentendo agli utenti di accedere rapidamente alle risorse necessarie tramite filtri, quali tipi di risorse supportate, orientamento delle immagini e stato della licenza.

>[!NOTE]
>
>Le risorse ricercate da Adobe Stock vengono solo visualizzate in AEM. Le risorse Adobe Stock vengono recuperate e memorizzate nell’archivio di AEM solo dopo che un utente [salva una risorsa](/help/assets/aem-assets-adobe-stock.md#saveassets) o ne [concede la licenza](/help/assets/aem-assets-adobe-stock.md#licenseassets). Le risorse già memorizzate in AEM vengono visualizzate ed evidenziate per semplificare la consultazione e l’accesso. Inoltre, tali risorse vengono salvate con alcuni metadati aggiuntivi per indicare l’origine come Adobe Stock.

![Filtri di ricerca in AEM e risorse Adobe Stock evidenziate nei risultati di ricerca](assets/aem-search-filters2.jpg)

*Figura: Filtri di ricerca in AEM e risorse Adobe Stock evidenziate nei risultati di ricerca*

### Salvate e visualizzate le risorse richieste {#saveassets}

Selezionate una risorsa da salvare in AEM. Fate clic su Salva nella barra degli strumenti nella parte superiore e fornite il nome e la posizione della risorsa. Le risorse senza licenza vengono salvate localmente con una filigrana.

La prossima volta che ricercate le risorse, queste vengono evidenziate con un contrassegno, per indicare che sono disponibili in Risorse AEM.

>[!NOTE]
>
>Le risorse aggiunte di recente visualizzano un nuovo contrassegno invece del contrassegno Con licenza.

### Risorse di licenza {#licenseassets}

Gli utenti possono concedere in licenza le risorse Adobe Stock utilizzando la quota del piano Adobe Stock Enterprise. Quando si concede la licenza per una risorsa, questa viene salvata senza filigrana ed è disponibile per la ricerca e l’utilizzo in AEM Assets.

![Finestra di dialogo per ottenere la licenza e salvare risorse Adobe Stock in Risorse AEM](assets/aem-stock_licenseandsave.jpg)

*Figura: Finestra di dialogo per ottenere la licenza e salvare risorse Adobe Stock in Risorse AEM*

### Accesso a metadati e proprietà delle risorse {#access-metadata-and-asset-properties}

Gli utenti possono accedere ai metadati e visualizzarne l’anteprima, comprese le proprietà dei metadati Adobe Stock per le risorse salvate in AEM, e aggiungere riferimenti **[!UICONTROL di]** licenza per una risorsa. Tuttavia, gli aggiornamenti al riferimento della licenza non vengono sincronizzati tra il sito Web AEM e Adobe Stock.

Gli utenti possono visualizzare le proprietà per risorse con licenza e senza licenza.

![Visualizzare e accedere ai metadati e ai riferimenti di licenza delle risorse salvate](assets/metadata_properties.jpg)

*Figura: Visualizzare e accedere ai metadati e ai riferimenti di licenza delle risorse salvate*

## Limitazioni note {#known-limitations}

### L&#39;avviso dell&#39;immagine editoriale non viene visualizzato

Quando si concede la licenza a un’immagine, gli utenti non possono verificare se un’immagine è solo di uso editoriale. Per evitare possibili abusi, gli amministratori possono disattivare l’accesso alle risorse editoriali dall’Admin Console.

### Tipo di licenza errato visualizzato

È possibile che in AEM venga visualizzato un tipo di licenza non corretto per una risorsa. Gli utenti possono accedere al sito Web di Adobe Stock per vedere il tipo di licenza.

### Campi e metadati di riferimento non sincronizzati

Quando un utente aggiorna un campo di riferimento della licenza, le informazioni di riferimento della licenza vengono aggiornate in AEM ma non nel sito Web di Adobe Stock. Analogamente, se l’utente aggiorna i campi di riferimento nel sito Web di Adobe Stock, gli aggiornamenti non vengono sincronizzati in AEM.

## Related resources {#related-resources}

[Esercitazione video sull’utilizzo delle risorse Adobe Stock con Risorse AEM](https://helpx.adobe.com/experience-manager/kt/assets/using/stock-assets-feature-video-use.html)

[Guida al piano aziendale Adobe Stock](https://helpx.adobe.com/enterprise/using/adobe-stock-enterprise.html)

[Domande frequenti su Adobe Stock](https://helpx.adobe.com/stock/faq.html)
