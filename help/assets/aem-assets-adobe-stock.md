---
title: 'Gestire le risorse [!DNL Adobe Stock] '
description: Cerca, recupera, rilascia la licenza e gestisci [!DNL Adobe Stock] risorse all’interno di [!DNL Adobe Experience Manager]. Utilizza le risorse con licenza come qualsiasi altra risorsa digitale.
contentOwner: Vishabh Gupta
feature: Search, Adobe Stock
role: User, Admin
exl-id: 8ec597df-bb64-4768-bf9c-e8cca4fea25b
source-git-commit: 6d1073003c1b78be848652be0b387889eedbc193
workflow-type: tm+mt
source-wordcount: '2443'
ht-degree: 8%

---

# Utilizzare le risorse [!DNL Adobe Stock] in [!DNL Adobe Experience Manager Assets] {#use-adobe-stock-assets-in-aem-assets}

<!-- old content

[!DNL Experience Manager Assets] provides users the ability to search, preview, save, and license [!DNL Adobe Stock] assets directly from [!DNL Experience Manager]. 

Organizations can integrate their [!DNL Adobe Stock] enterprise plan with [!DNL Experience Manager Assets] to ensure that licensed assets are broadly available for their creative and marketing projects, with the powerful asset management capabilities of [!DNL Experience Manager].

[!DNL Adobe Stock] service provides designers and businesses with access to millions of high-quality, curated, royalty-free photos, vectors, illustrations, videos, templates, and 3D assets for all their creative projects. [!DNL Experience Manager] users are able to quickly find, preview, and license [!DNL Adobe Stock] assets that are saved in [!DNL Experience Manager], without leaving the [!DNL Experience Manager] interface.
-->

<!-- New overview content
-->

[!DNL Adobe Stock]Il servizio offre a designer e aziende l’accesso a milioni di foto, immagini vettoriali, illustrazioni, video, modelli e risorse 3D di alta qualità, curate ed esenti da royalty, per qualsiasi progetto creativo.

[!DNL Adobe Stock] per l’offerta enterprise, per impostazione predefinita, include la condivisione di diritti in tutta l’organizzazione. Una volta concessa la licenza a una risorsa da parte di un utente dell’organizzazione, altri utenti dell’organizzazione possono identificare, scaricare e utilizzare questa risorsa senza dover concedere nuovamente la licenza. Una volta che una risorsa è stata concessa in licenza dalla tua organizzazione, il diritto di utilizzarla è permanente.

Le organizzazioni possono integrare il piano aziendale [!DNL Adobe Stock] con [!DNL Experience Manager Assets] per garantire che le risorse concesse in licenza siano ampiamente disponibili per i loro progetti creativi e di marketing, con le potenti funzionalità di gestione delle risorse di [!DNL Experience Manager]. [!DNL Experience Manager] Gli utenti possono trovare rapidamente, visualizzare in anteprima e concedere in licenza le risorse Adobe Stock salvate in  [!DNL Experience Manager] senza uscire dall’ [!DNL Experience Manager] interfaccia.

<!-- Old content
## Prerequisites {#prerequisites}

The integration requires an [enterprise [!DNL Adobe Stock] plan](https://stockenterprise.adobe.com/).
-->

## Integrare [!DNL Experience Manager] e [!DNL Adobe Stock] {#integrate-aem-and-adobe-stock}

[!DNL Experience Manager Assets] consente agli utenti di cercare, visualizzare in anteprima, salvare e concedere in licenza  [!DNL Adobe Stock] le risorse direttamente da  [!DNL Experience Manager].

**Prerequisiti**

L&#39;integrazione richiede:
* Un [enterprise [!DNL Adobe Stock] plan](https://stockenterprise.adobe.com/)
* Un utente con autorizzazioni in Admin Console al profilo di prodotto Stock predefinito
* Utente con autorizzazioni per il profilo Developer Access per la creazione di integrazioni in Adobe Developer Console

Un piano [!DNL Adobe Stock] aziendale,
* Fornisce l&#39;adesione al prodotto per [!DNL Adobe Stock] (Stock collegati all&#39;Experience Manager)
* Crediti acquistati in [!DNL Adobe Admin Console] per l&#39;adesione alle azioni
* Abilita l&#39;autenticazione dell&#39;account di servizio (JWT) all&#39;interno di [!DNL Adobe Developer Console] per l&#39;adesione alle azioni
* Consente di gestire i crediti e le licenze a livello globale da [!DNL Adobe Admin Console]

All&#39;interno dell&#39;adesione, esiste un profilo di prodotto predefinito per [!DNL Adobe Stock] in [!DNL Admin Console]. È possibile creare più profili e questi profili determinano chi può concedere la licenza per le risorse Stock. Un utente con accesso diretto al profilo di prodotto può accedere a [https://stock.adobe.com/](https://stock.adobe.com/) e concedere in licenza le risorse Stock. Esiste un altro metodo per utilizzare Developer Access per creare un’integrazione (API) per autenticare la comunicazione tra [!DNL Experience Manager] e [!DNL Adobe Stock].

>[!NOTE]
>
>L’autenticazione dell’account del servizio Stock (JWT) viene fornita con l’autorizzazione Enterprise Stock.
>
>L’integrazione non supporta l’autenticazione Oauth per l’adesione a Enterprise Stock.

<!-- old content
To allow communication between [!DNL Experience Manager] and [!DNL Adobe Stock], create an IMS configuration and an [!DNL Adobe Stock] configuration in [!DNL Experience Manager].

>[!NOTE]
>
>Only [!DNL Experience Manager] administrators and [!DNL Admin Console] administrators for an organization can perform the integration as it requires administrator privileges.
-->

## Passaggi per integrare [!DNL Experience Manager] e [!DNL Adobe Stock] {#integration-steps}

Per integrare [!DNL Experience Manager] e [!DNL Adobe Stock], esegui i seguenti passaggi nella sequenza elencata:

1. [Recuperare il certificato pubblico](#public-certificate)

   In [!DNL Experience Manager], crea un account IMS e genera un certificato pubblico (chiave pubblica).

1. [Crea connessione account di servizio (JWT)](#createnewintegration)

   In [!DNL Adobe Developer Console], crea un progetto per la tua organizzazione [!DNL Adobe Stock]. Nel progetto, configura un’API utilizzando la chiave pubblica per creare una connessione a un account di servizio (JWT). Ottieni le credenziali dell&#39;account del servizio e le informazioni sul payload JWT.

1. [Configurare l’account IMS](#create-ims-account-configuration)

   In [!DNL Experience Manager], configura l’account IMS utilizzando le credenziali dell’account del servizio e il payload JWT.

1. [Configurare il servizio cloud](#configure-the-cloud-service)

   In [!DNL Experience Manager], configura un servizio cloud [!DNL Adobe Stock] utilizzando l’account IMS.


### Creare una configurazione IMS {#create-an-ims-configuration}

La configurazione IMS autentica l’istanza di authoring [!DNL Experience Manager Assets] con l’adesione [!DNL Adobe Stock].

La configurazione IMS prevede due passaggi:

* [Recuperare il certificato pubblico](#public-certificate)
* [Configurare l’account IMS](#create-ims-account-configuration)

### Recuperare il certificato pubblico {#public-certificate}

La chiave pubblica (certificato) autentica il profilo di prodotto in Adobe Developer Console.

1. Accedi alla tua istanza di authoring [!DNL Experience Manager Assets]. L’URL predefinito è `http://localhost:4502/aem/start.html`.

1. Dal pannello **[!UICONTROL Strumenti]**, passa a **[!UICONTROL Sicurezza]** > **[!UICONTROL Configurazioni Adobe IMS]**.

1. Nella pagina Configurazioni Adobe IMS, fai clic su **[!UICONTROL Crea]**. Viene visualizzata la pagina **[!UICONTROL Configurazione account tecnico Adobe IMS]** .

1. Nella scheda **[!UICONTROL Certificato]** , seleziona **[!UICONTROL Adobe Stock]** dall’elenco a discesa **[!UICONTROL Soluzione cloud]** .

1. Puoi creare un certificato o riutilizzare un certificato esistente per la configurazione.

   Per creare un certificato, seleziona la casella di controllo **[!UICONTROL Crea nuovo certificato]** e specifica un **alias** per la chiave pubblica. L&#39;alias funge da nome della chiave pubblica.

1. Fai clic su **[!UICONTROL Crea certificato]**. Quindi, fai clic su **[!UICONTROL OK]** per generare la chiave pubblica.

1. Fai clic sull&#39;icona **[!UICONTROL Scarica chiave pubblica]** e salva il file della chiave pubblica (.crt) sul computer. La chiave pubblica viene utilizzata in seguito per configurare l’API per il tenant Brand Portal e generare le credenziali dell’account del servizio in Adobe Developer Console.

   Fai clic su **[!UICONTROL Avanti]**.

   ![genera certificato](assets/stock-integration-ims-account.png)

1. Nella scheda **Account** viene creato l’account Adobe IMS che richiede le credenziali dell’account del servizio.

   Apri una nuova scheda e [crea una connessione a un account di servizio (JWT) in Adobe Developer Console](#createnewintegration).

### Crea connessione account di servizio (JWT) {#createnewintegration}

In Adobe Developer Console, i progetti e le API sono configurati a livello di organizzazione. La configurazione di un’API crea una connessione a un account di servizio (JWT). Esistono due metodi per configurare l’API, generando una coppia di chiavi (chiavi private e pubbliche) o caricando una chiave pubblica. In questo esempio, le credenziali dell’account del servizio vengono generate caricando la chiave pubblica.

Per generare le credenziali dell’account del servizio e il payload JWT:

1. Accedi ad Adobe Developer Console con privilegi di amministratore di sistema. L&#39;URL predefinito è [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui).


   Accertati di aver selezionato l’organizzazione IMS corretta (adesione Stock) dall’elenco a discesa (organizzazione).

1. Fai clic su **[!UICONTROL Crea nuovo progetto]**. Per la tua organizzazione viene creato un progetto vuoto con un nome generato dal sistema.

   Fai clic su **[!UICONTROL Modifica progetto]**. Aggiorna i valori **[!UICONTROL Titolo progetto]** e **[!UICONTROL Descrizione]**, quindi fai clic su **[!UICONTROL Salva]**.

1. Nella scheda **[!UICONTROL Panoramica progetto]** , fai clic su **[!UICONTROL Aggiungi API]**.

1. In **[!UICONTROL Aggiungi una finestra API]**, seleziona **[!UICONTROL Adobe Stock]**. Fai clic su **[!UICONTROL Avanti]**.

1. Nella finestra **[!UICONTROL Configura API]**, seleziona l&#39;autenticazione **[!UICONTROL Account di servizio (JWT)]**. Fai clic su **[!UICONTROL Avanti]**.

   ![create-jwt-credentials](assets/aem-stock-jwt.png)

1. Fai clic su **[!UICONTROL Carica la chiave pubblica]**. Fai clic su **[!UICONTROL Seleziona un file]** e carica la chiave pubblica (.crt file) scaricata nella sezione [Ottieni certificato pubblico](#public-certificate) . Fai clic su **[!UICONTROL Avanti]**.

1. Verifica la chiave pubblica e fai clic su **[!UICONTROL Avanti]**.

1. Seleziona il profilo di prodotto predefinito **[!UICONTROL Adobe Stock]** e fai clic su **[!UICONTROL Salva API configurata]**.

1. Una volta configurata l’API, vieni reindirizzato alla pagina di panoramica dell’API. Nella navigazione a sinistra sotto **[!UICONTROL Credenziali]**, fai clic sull&#39;opzione **[!UICONTROL Account di servizio (JWT)]**. Qui puoi visualizzare le credenziali ed eseguire azioni quali generare token JWT, copiare i dettagli delle credenziali e recuperare il segreto client.

1. Dalla scheda **[!UICONTROL Credenziali client]**, copia l&#39; **[!UICONTROL ID client]**.

   Fai clic su **[!UICONTROL Recupera segreto client]** e copia il **[!UICONTROL segreto client]**.

   ![generate-jwt-credentials](assets/aem-stock-jwt-credential.png)

1. Passa alla scheda **[!UICONTROL Genera JWT]** e copia le informazioni **[!UICONTROL Payload JWT]** .

Ora puoi utilizzare l’ID client (chiave API), il segreto client e il payload JWT per [configurare l’account IMS](#create-ims-account-configuration) in [!DNL Experience Manager Assets].

### Configurare l’account IMS {#create-ims-account-configuration}

Per configurare l’account IMS è necessario disporre delle credenziali [certificate](#public-certificate) e [service account (JWT)](#createnewintegration).

Per configurare l’account IMS:

1. Apri la configurazione IMS e passa alla scheda **[!UICONTROL Account]** . Hai tenuto aperta la pagina durante [il recupero del certificato pubblico](#public-certificate).

1. Specifica un **[!UICONTROL titolo]** per l’account IMS.

   Nel campo **[!UICONTROL Server autorizzazioni]** , immetti l’URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/).

   Immetti l&#39;ID client nel campo **[!UICONTROL Chiave API]** , **[!UICONTROL Segreto client]** e **[!UICONTROL Payload]** (Payload JWT) che hai copiato durante la creazione della connessione dell&#39;account del servizio (JWT)](#createnewintegration).[

1. Fai clic su **[!UICONTROL Crea]**. Viene creata una configurazione dell’account IMS.

   ![configure-ims-account](assets/aem-stock-ims-config.png)

1. Seleziona la configurazione dell’account IMS e fai clic su **[!UICONTROL Verifica stato]**.

   Fare clic su **[!UICONTROL Controlla]** nella finestra di dialogo. Una volta completata la configurazione, viene visualizzato un messaggio che informa che il *Token viene recuperato correttamente*.

   ![valutazione dello stato di salute](assets/aem-stock-healthcheck.png)


### Configurare il servizio cloud {#configure-the-cloud-service}

Per configurare il servizio cloud [!DNL Adobe Stock]:

1. Nell&#39;interfaccia utente [!DNL Experience Manager] , passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**.

1. Nella pagina [!DNL Adobe Stock Configurations], fai clic su **[!UICONTROL Crea]**.

1. Specifica un **[!UICONTROL titolo]** per la configurazione del cloud.

   Seleziona la configurazione IMS creata durante la [configurazione dell’account IMS](#create-ims-account-configuration).

   Seleziona le impostazioni internazionali dall’elenco a discesa.

   ![aem-stock-cloud-config](assets/aem-stock-cloud-config.png)

1. Fai clic su **[!UICONTROL Salva e chiudi]**.

   L&#39;istanza dell&#39;autore [!DNL Experience Manager Assets] è ora integrata con [!DNL Adobe Stock]. Puoi creare più configurazioni [!DNL Adobe Stock] (ad esempio, configurazioni basate sulle impostazioni internazionali). È ora possibile accedere, cercare e concedere in licenza le risorse [!DNL Adobe Stock] dall&#39;interfaccia utente di [!DNL Experience Manager].

   ![search-stock-assets](assets/aem-stock-searchstocks.png)

   >[!NOTE]
   >
   >A questo punto dell’integrazione, solo gli amministratori possono accedere alle risorse [!DNL Adobe Stock], cercare le risorse Stock (utilizzando omnisearch) e concedere in licenza le risorse [!DNL Adobe Stock].
   >
   >Gli amministratori possono aggiungere ulteriormente utenti o gruppi al servizio cloud [!DNL Adobe Stock] e concedere le autorizzazioni a questi utenti non amministratori in [!DNL Experience Manager] per accedere alla configurazione Stock.

1. Per aggiungere utenti o gruppi, seleziona la configurazione cloud [!DNL Adobe Stock] e fai clic su **[!UICONTROL Proprietà]**.

1. Cerca di aggiungere gli utenti o i gruppi a cui hai assegnato le autorizzazioni per accedere alla configurazione di Adobe Stock. Consulta [assegnare le autorizzazioni al gruppo di utenti](#assign-permissions-to-group).


## Assegnare le autorizzazioni al gruppo di utenti {#assign-permissions-to-group}

Gli amministratori possono creare gruppi di utenti e concedere ad alcuni utenti o gruppi le autorizzazioni necessarie per accedere al servizio cloud [!DNL Adobe Stock].

Di seguito sono riportate le autorizzazioni necessarie per consentire a un utente di cercare e concedere in licenza le risorse Adobe Stock:

* Configura il percorso: `/conf/global/settings/stock`
* Privilegi: `jcr:read`
* Tipo di autorizzazione: `Allow`

È possibile creare un gruppo di utenti o assegnare le autorizzazioni a un gruppo di utenti esistente. Le autorizzazioni possono essere assegnate dall&#39;interfaccia [!DNL Experience Manager Assets] o dalla console [!DNL User Admin].

**Per fornire l’accesso a un gruppo di utenti da  [!DNL Experience Manager]:**

1. Nell&#39;interfaccia utente [!DNL Experience Manager], passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Sicurezza]** > **[!UICONTROL Gruppi]**. Crea un gruppo di utenti per [!DNL Adobe Stock].

1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Sicurezza]** > **[!UICONTROL Autorizzazioni]**.

1. Cerca il gruppo di utenti nel pannello a sinistra e aggiungi una nuova **[!UICONTROL Voce di controllo accessi (ACE)]** per Adobe Stock.

   * Configura il percorso: `/conf/global/settings/stock`
   * Privilegi: `jcr:read`
   * Tipo di autorizzazione: `Allow`

   Fate clic su **[!UICONTROL Aggiungi]**.

   ![autorizzazioni utente](assets/aem-stock-user-permissions.png)

1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**. Seleziona la configurazione cloud [!DNL Adobe Stock] e fai clic su **[!UICONTROL Proprietà]**.

1. Aggiungi il gruppo di utenti appena creato alla configurazione [!DNL Adobe Stock] . Fai clic su **[!UICONTROL Salva e chiudi]**.

   ![assegna utente](assets/aem-stock-adduser.png)

**Per fornire l’accesso a un utente da  [!DNL User Admin Console]:**

1. Apri l&#39;Admin Console utente [!DNL Experience Manager]. L’URL predefinito è `http://localhost:4502/userdamin`.

1. Nel pannello a sinistra, cerca l’utente immettendo il valore `user_id` o `name`. Fare doppio clic per aprire le proprietà utente.

1. Passa alla scheda **[!UICONTROL Autorizzazioni]** e consenti le autorizzazioni `read` per la configurazione cloud [!DNL Adobe Stock]: `/conf/global/settings/stock`.

   >[!CAUTION]
   >
   >Se la configurazione cloud non è consentita, l&#39;utente può accedere solo a **[!UICONTROL Risorse]** nell&#39;interfaccia [!DNL Experience Manager].
   >
   >Per consentire l’accesso alle risorse [!UICONTROL Risorse] e [!DNL Adobe Stock] , assicurati che la configurazione cloud sia consentita all’utente.

1. Fai clic su **[!UICONTROL Salva]** per aggiornare le autorizzazioni.

   ![assign-user-in-user-admin](assets/aem-stock-user-admin-console.png)

1. Aggiungi l&#39;utente o il gruppo alla configurazione cloud [!DNL Adobe Stock].


## Accedere alle risorse di Adobe Stock {#access-stock-assets}

Un utente non amministratore con autorizzazioni per la configurazione cloud [!DNL Adobe Stock] può cercare e concedere in licenza le risorse [!DNL Adobe Stock] dall&#39;interfaccia [!DNL Experience Manager].

L’utente deve eseguire un ulteriore passaggio per attivare la configurazione cloud [!DNL Adobe Stock] prima di accedere alle risorse [!DNL Adobe Stock] . È un’attività una tantum. Se all&#39;utente vengono assegnate autorizzazioni su più configurazioni cloud [!DNL Adobe Stock], l&#39;utente può selezionare la configurazione desiderata da **[!UICONTROL Preferenze utente]**.

Per attivare la configurazione cloud [!DNL Adobe Stock]:

1. Accedi a [!DNL Experience Manager].

1. Fai clic sull&#39;icona utente nell&#39;angolo in alto a destra, quindi fai clic su **[!UICONTROL Preferenze]**. Viene visualizzata la finestra **[!UICONTROL Preferenze utente]**.

1. Seleziona la **[!UICONTROL Configurazione stock]** desiderata dall&#39;elenco a discesa e fai clic su **[!UICONTROL Accetta]** per attivare la configurazione.

   ![preferenze utente](assets/aem-stock-preferences.png)

1. Passa a **[!UICONTROL Risorse]** > **[!UICONTROL Adobe Stock]**. Ora puoi visualizzare, cercare e concedere in licenza le risorse [!DNL Adobe Stock].

La tabella seguente spiega come funzionano le autorizzazioni utente quando si accede alle risorse [!DNL Adobe Stock] :

| User | Gruppo | Autorizzazioni | Accetta la configurazione Stock in Preferenze utente | Accedere alle risorse | Accedere ad Adobe Stock |
| --- | --- | --- | --- | --- | --- |
| admin | N/D | Tutti i bundle  | N/D | Sì | Sì |
| test-doc1 | Utente DAM | `/conf/global/settings/stock/cloud-config` | Sì | Sì | Sì |
| test-doc1 | Utente DAM | `/conf/global/settings/stock/cloud-config` | No | Errore: Impossibile caricare i dati | No |
| test-doc1 | Utente DAM | consentire: `/conf/global/settings/stock` nega: `/cloud-config` | La configurazione Stock non è visibile | Sì | No |


## Utilizzare e gestire le risorse [!DNL Adobe Stock] in [!DNL Experience Manager] {#usemanage}

Utilizzando questa funzionalità, le organizzazioni possono consentire agli utenti di utilizzare le risorse [!DNL Adobe Stock] in [!DNL Experience Manager Assets]. Dall’interno dell’interfaccia utente [!DNL Experience Manager], gli utenti possono cercare le risorse [!DNL Adobe Stock] e concedere in licenza le risorse richieste.

Una volta concessa la licenza a una risorsa [!DNL Adobe Stock] in [!DNL Experience Manager], questa può essere utilizzata e gestita come una tipica risorsa. In [!DNL Experience Manager], gli utenti possono cercare e visualizzare in anteprima le risorse; copiare e pubblicare le risorse; condividere le risorse su [!DNL Brand Portal]; accedere alle risorse e utilizzarle tramite l’app desktop [!DNL Experience Manager]; e così via.

![Cercare  [!DNL Adobe Stock] risorse e filtrare i risultati dall’ [!DNL Adobe Experience Manager] area di lavoro](assets/adobe-stock-search-results-workspace.png)

**A.**[!DNL Adobe Stock] Cerca risorse simili a quelle di chi è fornito l’ID **B.** Cerca risorse corrispondenti alla tua selezione di forma o orientamento. **C.** Cerca uno o più dei tipi di risorse supportati **D.** Apri o comprimi il riquadro Filtri **E.** Procurati la licenza relativa e salva la risorsa selezionata in [!DNL Experience Manager]**F.**[!DNL Experience Manager] Salva la risorsa in applicando la filigrana **G.**[!DNL Adobe Stock] Sul sito web di , esplora le risorse simili a quella selezionata **H.**[!DNL Adobe Stock] Visualizza le risorse selezionate sul sito web di **I.** Numero di risorse selezionate proveniente dai risultati della ricerca **J.** Passaggio tra la vista a schede e la vista a elenco

### Trovare risorse {#find-assets}

Gli utenti [!DNL Experience Manager] possono cercare le risorse in entrambi, [!DNL Experience Manager] e [!DNL Adobe Stock]. Quando il percorso di ricerca non è limitato a [!DNL Adobe Stock], vengono visualizzati i risultati di ricerca da [!DNL Experience Manager] e [!DNL Adobe Stock].

* Per cercare le risorse [!DNL Adobe Stock], fai clic su **[!UICONTROL Navigazione]** > **[!UICONTROL Risorse]** > **[!UICONTROL Ricerca in Adobe Stock]**.

* Per cercare le risorse tra [!DNL Adobe Stock] e [!DNL Experience Manager Assets], fai clic su Cerca ![cerca](assets/do-not-localize/search_icon.png).

In alternativa, inizia a digitare `Location: Adobe Stock` nella barra di ricerca per selezionare le risorse [!DNL Adobe Stock]. [!DNL Experience Manager] offre funzionalità di filtro avanzate per le risorse ricercate, che consentono agli utenti di accedere rapidamente da zero alle risorse richieste utilizzando i filtri, ad esempio i tipi di risorse supportate, l’orientamento dell’immagine e lo stato con licenza.

>[!NOTE]
>
>Le risorse ricercate da [!DNL Adobe Stock] vengono visualizzate in [!DNL Experience Manager]. [!DNL Adobe Stock] le risorse vengono recuperate e memorizzate nell’ [!DNL Experience Manager] archivio solo dopo che un utente  [salva una ](/help/assets/aem-assets-adobe-stock.md#saveassets) risorsa o  [ne salva una](/help/assets/aem-assets-adobe-stock.md#licenseassets). Le risorse già memorizzate in [!DNL Experience Manager] vengono visualizzate ed evidenziate per semplificare il riferimento e l’accesso. Inoltre, le risorse [!DNL Stock] vengono salvate con alcuni metadati aggiuntivi per indicare l’origine come [!DNL Stock].

![Ricerca di filtri  [!DNL Experience Manager] e  [!DNL Adobe Stock] risorse evidenziate nei risultati di ricerca](assets/aem-search-filters2.jpg)

### Salvare e visualizzare le risorse richieste {#saveassets}

Seleziona una risorsa da salvare in [!DNL Experience Manager]. Fai clic su [!UICONTROL Salva] nella barra degli strumenti nella parte superiore e fornisci il nome e la posizione della risorsa. Le risorse senza licenza vengono salvate localmente con una filigrana.

La prossima volta che cerchi le risorse, le risorse salvate vengono evidenziate con un contrassegno, per indicare che sono disponibili in [!DNL Experience Manager Assets].

>[!NOTE]
>
>Le risorse aggiunte di recente visualizzano un nuovo badge invece del badge License .

### Risorse di licenza {#licenseassets}

Gli utenti possono concedere in licenza le risorse [!DNL Adobe Stock] utilizzando la quota del proprio [!DNL Adobe Stock] piano aziendale. Quando si concede la licenza a una risorsa, questa viene salvata senza filigrana ed è disponibile per la ricerca e l’utilizzo in [!DNL Experience Manager Assets].

![Finestra di dialogo per concedere in licenza e salvare  [!DNL Adobe Stock] le risorse in  [!DNL Experience Manager Assets]](assets/aem-stock_licenseandsave.jpg)


### Accedere a metadati e proprietà delle risorse {#access-metadata-and-asset-properties}

Gli utenti possono accedere ai metadati e visualizzarli in anteprima, comprese le proprietà dei metadati [!DNL Adobe Stock] per le risorse salvate in [!DNL Experience Manager], e aggiungere **[!UICONTROL Riferimenti di licenza]** per una risorsa. Tuttavia, gli aggiornamenti al riferimento di licenza non vengono sincronizzati tra il sito web [!DNL Experience Manager] e [!DNL Adobe Stock].

Gli utenti possono visualizzare le proprietà sia delle risorse con licenza che di quelle senza licenza.

![Visualizzare e accedere ai metadati e ai riferimenti di licenza delle risorse salvate](assets/metadata_properties.jpg)


## Limitazioni note {#known-limitations}

* **Problemi in integrazione con  [!DNL Experience Manager] Service Pack 6.5.7.0 e versioni successive**: Un problema imprevisto viene identificato durante l&#39;integrazione con  [!DNL Experience Manager] 6.5.7.0 e versioni successive. Il problema è in fase di test e dovrebbe essere disponibile in [!DNL Experience Manager] 6.5.11.0. Contatta [!DNL Customer Support] per un hotfix immediato.

* **La funzionalità per limitare gli utenti dalle licenze non funziona correttamente**: Tutti gli utenti che dispongono di  `read` autorizzazioni per la configurazione delle risorse possono cercare e concedere la licenza per le  [!DNL Adobe Stock] risorse.

* **Gli utenti non amministratori devono attivare manualmente la configurazione  [!DNL Adobe Stock] cloud**: Nella finestra  **[!UICONTROL Preferenze]** utente, la  **[!UICONTROL configurazione]** Stock mostra la configurazione  [!DNL Adobe Stock] cloud come abilitata, ma non funziona per un utente non amministratore. L&#39;utente deve fare clic sul pulsante **[!UICONTROL Accetta]** per attivare la configurazione Stock. In assenza di questo passaggio, il sistema riflette un messaggio di errore sull&#39;accesso a **[!UICONTROL Risorse]**.

* **L&#39;avviso dell&#39;immagine editoriale non viene visualizzato**: Quando si concede in licenza un&#39;immagine, gli utenti non possono verificare se un&#39;immagine è di utilizzo solo editoriale. Per evitare possibili abusi, gli amministratori possono disattivare l’accesso alle risorse editoriali dall’Admin Console.

* **Viene visualizzato** un tipo di licenza errato: È possibile che venga visualizzato un tipo di licenza errato in  [!DNL Experience Manager] per una risorsa. Gli utenti possono accedere al sito web [!DNL Adobe Stock] per visualizzare il tipo di licenza.

* **I campi e i metadati di riferimento non sono sincronizzati**: Quando un utente aggiorna un campo di riferimento della licenza, le informazioni di riferimento della licenza vengono aggiornate in  [!DNL Experience Manager] ma non sul  [!DNL Adobe Stock] sito web. Analogamente, se l&#39;utente aggiorna i campi di riferimento sul sito web [!DNL Adobe Stock], gli aggiornamenti non vengono sincronizzati in [!DNL Experience Manager].

>[!MORELIKETHIS]
>
>* [Esercitazione video sull’ [!DNL Adobe Stock] utilizzo delle risorse con [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/creative-workflows/adobe-stock.html)
>* [[!DNL Adobe Stock] aiuto per il piano aziendale](https://helpx.adobe.com/enterprise/using/adobe-stock-enterprise.html)
>* [[!DNL Adobe Stock] Domande frequenti](https://helpx.adobe.com/stock/faq.html)



<!--old content

### Create an IMS configuration {#create-an-ims-configuration}

1. In the [!DNL Experience Manager] user interface, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**. Click **[!UICONTROL Create]** and select **[!UICONTROL Cloud Solution]** > **[!UICONTROL Adobe Stock]**.
1. Either reuse an existing certificate or select **[!UICONTROL Create new certificate]**.
1. Click **[!UICONTROL Create certificate]**. Once created, download the public key. Click **[!UICONTROL Next]**. Leave the [!UICONTROL Adobe IMS Technical Account Configuration] screen open to provide the required values shortly.
1. Access [Adobe Developer Console](https://console.adobe.io). Ensure that your account has administrator permissions for the organization for which the integration is required.
1. Click **[!UICONTROL Create new project]** and click **[!UICONTROL Add API]**. Select **[!UICONTROL Adobe Stock]** from the list of APIs that are available to you. Select [!UICONTROL OAUTH 2.0 Web].
1. Provide **[!UICONTROL Default redirect URI]** and **[!UICONTROL Redirect URI pattern]** values. Click **[!UICONTROL Save configured API]**. Copy the generated ID and secret.
1. In [!UICONTROL Adobe IMS Technical Account Configuration] screen, provide the values in the boxes titled **[!UICONTROL Title]**, **[!UICONTROL Authorization Server]**, **[!UICONTROL API Key]**, **[!UICONTROL Client Secret]**, and **[!UICONTROL Payload]**. For detailed information about these values, see [JWT authentication quick start](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWT.md).

-->

<!-- TBD: Update the URL to update the terminology when AIO team updates their documentation URL. Logged issue github.com/AdobeDocs/adobeio-auth/issues/63.
-->

<!--
### Create [!DNL Adobe Stock] configuration in [!DNL Experience Manager] {#create-adobe-stock-configuration-in-aem}

1. In the [!DNL Experience Manager], navigate to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**.
1. Click **[!UICONTROL Create]** to create a configuration and associate it with your existing IMS Configuration. Select `PROD` as the environment parameter.
1. In **[!UICONTROL Licensed Assets Path]** field, leave a location as is. Do not change the location where you want to store the [!DNL Adobe Stock] assets.
1. Complete creation by adding all the required properties. Click **[!UICONTROL Save & Close]**.
1. Add [!DNL Experience Manager] users or groups, who can license the assets.

>[!NOTE]
>
>If there are multiple [!DNL Adobe Stock] configurations, select the desired configuration in [!UICONTROL User Preferences] panel. To access the panel from [!DNL Experience Manager] home page, click the user icon and then click **[!UICONTROL User Preferences]** > **[!UICONTROL Stock Configuration]**.

-->