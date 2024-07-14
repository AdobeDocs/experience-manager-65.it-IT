---
title: Gestisci [!DNL Adobe Stock] risorse
description: Cerca, recupera, concedi licenze e gestisci [!DNL Adobe Stock] risorse da [!DNL Adobe Experience Manager]. Utilizza le risorse concesse in licenza come qualsiasi altra risorsa digitale.
contentOwner: Vishabh Gupta
feature: Search, Adobe Stock
role: User, Admin
exl-id: 8ec597df-bb64-4768-bf9c-e8cca4fea25b
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2446'
ht-degree: 3%

---

# Usa [!DNL Adobe Stock] risorse in [!DNL Adobe Experience Manager Assets] {#use-adobe-stock-assets-in-aem-assets}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/aem-assets-adobe-stock.html?lang=en) |
| AEM 6.5 | Questo articolo |

<!-- old content

[!DNL Experience Manager Assets] provides users the ability to search, preview, save, and license [!DNL Adobe Stock] assets directly from [!DNL Experience Manager]. 

Organizations can integrate their [!DNL Adobe Stock] enterprise plan with [!DNL Experience Manager Assets] to ensure that licensed assets are broadly available for their creative and marketing projects, with the powerful asset management capabilities of [!DNL Experience Manager].

[!DNL Adobe Stock] service provides designers and businesses with access to millions of high-quality, curated, royalty-free photos, vectors, illustrations, videos, templates, and 3D assets for all their creative projects. [!DNL Experience Manager] users are able to quickly find, preview, and license [!DNL Adobe Stock] assets that are saved in [!DNL Experience Manager], without leaving the [!DNL Experience Manager] interface.
-->

<!-- New overview content
-->

Il servizio [!DNL Adobe Stock] consente ai designer e alle aziende di accedere a milioni di foto, vettori, illustrazioni, video, modelli e risorse 3D di alta qualità e curate, senza royalty, per tutti i progetti creativi.

[!DNL Adobe Stock] per l&#39;offerta Enterprise, per impostazione predefinita, include i diritti di condivisione in tutta l&#39;organizzazione. Una volta che una risorsa è stata concessa in licenza da un utente dell’organizzazione, altri utenti dell’organizzazione possono identificarla, scaricarla e utilizzarla senza doverla concedere nuovamente in licenza. Una volta che una risorsa è stata concessa in licenza dalla tua organizzazione, il diritto di utilizzarla è permanente.

Le organizzazioni possono integrare il piano [!DNL Adobe Stock] aziendale con [!DNL Experience Manager Assets] per garantire che le risorse concesse in licenza siano ampiamente disponibili per i progetti creativi e di marketing, con le potenti funzionalità di gestione delle risorse di [!DNL Experience Manager]. [!DNL Experience Manager] utenti possono trovare, visualizzare in anteprima e concedere in licenza le risorse Adobe Stock salvate in [!DNL Experience Manager] senza uscire dall&#39;interfaccia [!DNL Experience Manager].

<!-- Old content
## Prerequisites {#prerequisites}

The integration requires an [enterprise [!DNL Adobe Stock] plan](https://stockenterprise.adobe.com/).
-->

## Integrare [!DNL Experience Manager] e [!DNL Adobe Stock] {#integrate-aem-and-adobe-stock}

[!DNL Experience Manager Assets] consente agli utenti di cercare, visualizzare in anteprima, salvare e concedere in licenza [!DNL Adobe Stock] risorse direttamente da [!DNL Experience Manager].

**Prerequisiti**

L&#39;integrazione richiede:

* Un [piano [!DNL Adobe Stock] aziendale](https://stockenterprise.adobe.com/)
* Un utente con autorizzazioni in Admin Console al profilo di prodotto Stock predefinito
* Utente con autorizzazioni per il profilo Accesso sviluppatore per la creazione di un’integrazione in Adobe Developer Console

Un piano [!DNL Adobe Stock] dell&#39;organizzazione

* Fornisce prodotti autorizzati per [!DNL Adobe Stock] (scorte collegate all&#39;Experience Manager)
* Crediti acquistati in [!DNL Adobe Admin Console] per il tuo diritto sulle azioni
* Abilita l&#39;autenticazione dell&#39;account di servizio (JWT) entro [!DNL Adobe Developer Console] per il tuo diritto alle azioni
* Consente di gestire i crediti e le licenze a livello globale da [!DNL Adobe Admin Console]

All&#39;interno del diritto, esiste un profilo di prodotto predefinito per [!DNL Adobe Stock] in [!DNL Admin Console]. È possibile creare più profili, che determinano chi può concedere in licenza le risorse Stock. Un utente con accesso diretto al profilo di prodotto può accedere a [https://stock.adobe.com/](https://stock.adobe.com/) e alle risorse Stock della licenza. Esiste invece un altro metodo per utilizzare l&#39;API Developer Access per creare l&#39;integrazione per autenticare le comunicazioni tra [!DNL Experience Manager] e [!DNL Adobe Stock].

>[!NOTE]
>
>L’autenticazione dell’account del servizio Stock (JWT) viene fornita con il diritto Enterprise Stock.
>
>L’integrazione non supporta l’autenticazione Oauth per l’adesione a Enterprise Stock.

<!-- old content
To allow communication between [!DNL Experience Manager] and [!DNL Adobe Stock], create an IMS configuration and an [!DNL Adobe Stock] configuration in [!DNL Experience Manager].

>[!NOTE]
>
>Only [!DNL Experience Manager] administrators and [!DNL Admin Console] administrators for an organization can perform the integration as it requires administrator privileges.
-->

## Passaggi per integrare [!DNL Experience Manager] e [!DNL Adobe Stock] {#integration-steps}

Per integrare [!DNL Experience Manager] e [!DNL Adobe Stock], effettuare le seguenti operazioni nella sequenza elencata:

1. [Ottieni certificato pubblico](#public-certificate)

   In [!DNL Experience Manager], crea un account IMS e genera un certificato pubblico (chiave pubblica).

1. [Crea connessione account del servizio (JWT)](#createnewintegration)

   In [!DNL Adobe Developer Console], crea un progetto per l&#39;organizzazione [!DNL Adobe Stock]. Nel progetto, configura un’API utilizzando la chiave pubblica per creare una connessione a un account di servizio (JWT). Ottieni le credenziali dell’account di servizio e le informazioni sul payload JWT.

1. [Configurare l’account IMS](#create-ims-account-configuration)

   In [!DNL Experience Manager], configura l&#39;account IMS utilizzando le credenziali dell&#39;account del servizio e il payload JWT.

1. [Configurare il servizio cloud](#configure-the-cloud-service)

   In [!DNL Experience Manager] configurare un servizio cloud [!DNL Adobe Stock] utilizzando l&#39;account IMS.


### Creare una configurazione IMS {#create-an-ims-configuration}

La configurazione IMS autentica l&#39;istanza dell&#39;autore [!DNL Experience Manager Assets] con l&#39;adesione [!DNL Adobe Stock].

La configurazione IMS prevede due passaggi:

* [Recuperare il certificato pubblico](#public-certificate)
* [Configurare l’account IMS](#create-ims-account-configuration)

### Ottieni certificato pubblico {#public-certificate}

La chiave pubblica (certificato) autentica il profilo di prodotto in Adobe Developer Console.

1. Accedi all&#39;istanza dell&#39;autore [!DNL Experience Manager Assets]. URL predefinito: `http://localhost:4502/aem/start.html`.

1. Dal pannello **[!UICONTROL Strumenti]**, passa a **[!UICONTROL Sicurezza]** > **[!UICONTROL Configurazioni Adobe IMS]**.

1. Nella pagina Configurazioni Adobe IMS, fai clic su **[!UICONTROL Crea]**. Viene visualizzata la pagina **[!UICONTROL Configurazione account tecnico Adobe IMS]**.

1. Nella scheda **[!UICONTROL Certificato]**, seleziona **[!UICONTROL Adobe Stock]** dall&#39;elenco a discesa **[!UICONTROL Soluzione cloud]**.

1. Puoi creare un certificato o riutilizzare un certificato esistente per la configurazione.

   Per creare un certificato, selezionare la casella di controllo **[!UICONTROL Crea nuovo certificato]** e specificare un **alias** per la chiave pubblica. L&#39;alias funge da nome della chiave pubblica.

1. Fai clic su **[!UICONTROL Crea certificato]**. Quindi fare clic su **[!UICONTROL OK]** per generare la chiave pubblica.

1. Fai clic sull&#39;icona **[!UICONTROL Scarica chiave pubblica]** e salva il file della chiave pubblica (crt) nel computer. La chiave pubblica viene utilizzata in seguito per configurare l’API per il tenant Brand Portal e generare le credenziali dell’account del servizio in Adobe Developer Console.

   Fai clic su **[!UICONTROL Avanti]**.

   ![genera-certificato](assets/stock-integration-ims-account.png)

1. Nella scheda **Account**, viene creato l&#39;account Adobe IMS che richiede le credenziali dell&#39;account del servizio.

   Apri una nuova scheda e [crea una connessione a un account di servizio (JWT) in Adobe Developer Console](#createnewintegration).

### Creare la connessione dell’account di servizio (JWT) {#createnewintegration}

In Adobe Developer Console, i progetti e le API sono configurati a livello di organizzazione. La configurazione di un’API crea una connessione dell’account di servizio (JWT). Esistono due metodi per configurare l’API: generando una coppia di chiavi (chiavi privata e pubblica) o caricando una chiave pubblica. In questo esempio, le credenziali dell’account del servizio vengono generate caricando la chiave pubblica.

Per generare le credenziali dell’account di servizio e il payload JWT:

1. Accedi a Adobe Developer Console con i privilegi di amministratore di sistema. URL predefinito: [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui).


   Accertati di aver selezionato l’organizzazione IMS (Stock entitlement) corretta dall’elenco a discesa (organizzazione).

1. Fare clic su **[!UICONTROL Crea nuovo progetto]**. Per l’organizzazione viene creato un progetto vuoto con un nome generato dal sistema.

   Fare clic su **[!UICONTROL Modifica progetto]**. Aggiorna il **[!UICONTROL Titolo progetto]** e la **[!UICONTROL Descrizione]**, quindi fai clic su **[!UICONTROL Salva]**.

1. Nella scheda **[!UICONTROL Panoramica progetto]**, fai clic su **[!UICONTROL Aggiungi API]**.

1. In **[!UICONTROL Aggiungi una finestra API]**, seleziona **[!UICONTROL Adobe Stock]**. Fai clic su **[!UICONTROL Avanti]**.

1. Nella finestra **[!UICONTROL Configura API]**, seleziona l&#39;autenticazione **[!UICONTROL Account di servizio (JWT)]**. Fai clic su **[!UICONTROL Avanti]**.

   ![create-jwt-credentials](assets/aem-stock-jwt.png)

1. Fai clic su **[!UICONTROL Carica la chiave pubblica]**. Fai clic su **[!UICONTROL Seleziona un file]** e carica la chiave pubblica (file .crt) scaricata nella sezione [Ottieni certificato pubblico](#public-certificate). Fai clic su **[!UICONTROL Avanti]**.

1. Verificare la chiave pubblica e fare clic su **[!UICONTROL Avanti]**.

1. Seleziona il profilo di prodotto predefinito **[!UICONTROL Adobe Stock]** e fai clic su **[!UICONTROL Salva API configurata]**.

1. Una volta configurata l’API, vieni reindirizzato alla pagina di panoramica API. Dalla barra di navigazione a sinistra in **[!UICONTROL Credenziali]**, fai clic sull&#39;opzione **[!UICONTROL Account di servizio (JWT)]**. Qui puoi visualizzare le credenziali ed eseguire azioni quali generare token JWT, copiare i dettagli delle credenziali e recuperare il segreto client.

1. Dalla scheda **[!UICONTROL Credenziali client]**, copia il **[!UICONTROL ID client]**.

   Fai clic su **[!UICONTROL Recupera segreto client]** e copia il **[!UICONTROL segreto client]**.

   ![generate-jwt-credentials](assets/aem-stock-jwt-credential.png)

1. Passa alla scheda **[!UICONTROL Genera JWT]** e copia le informazioni del **[!UICONTROL Payload JWT]**.

È ora possibile utilizzare l&#39;ID client (chiave API), il segreto client e il payload JWT per [configurare l&#39;account IMS](#create-ims-account-configuration) in [!DNL Experience Manager Assets].

### Configurare l’account IMS {#create-ims-account-configuration}

Per configurare l&#39;account IMS è necessario disporre delle credenziali [certificate](#public-certificate) e [account di servizio (JWT)](#createnewintegration).

Per configurare l’account IMS:

1. Apri la configurazione IMS e passa alla scheda **[!UICONTROL Account]**. Hai tenuto aperta la pagina durante il [ottenimento del certificato pubblico](#public-certificate).

1. Specifica un **[!UICONTROL titolo]** per l’account IMS.

   Nel campo **[!UICONTROL Server autorizzazioni]** immettere l&#39;URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/).

   Immetti l&#39;ID client nel campo **[!UICONTROL Chiave API]**, **[!UICONTROL Segreto client]** e **[!UICONTROL Payload]** (payload JWT) copiati durante la [creazione della connessione dell&#39;account del servizio (JWT)](#createnewintegration).

1. Fai clic su **[!UICONTROL Crea]**. Viene creata una configurazione dell’account IMS.

   ![configure-ims-acount](assets/aem-stock-ims-config.png)

1. Seleziona la configurazione dell&#39;account IMS e fai clic su **[!UICONTROL Verifica stato]**.

   Fare clic su **[!UICONTROL Controlla]** nella finestra di dialogo. Una volta completata la configurazione, viene visualizzato un messaggio che informa che il token *è stato recuperato correttamente*.

   ![verifica stato](assets/aem-stock-healthcheck.png)


### Configurare il servizio cloud {#configure-the-cloud-service}

Per configurare il servizio cloud [!DNL Adobe Stock]:

1. Nell&#39;interfaccia utente [!DNL Experience Manager], passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Adobe Stock]**.

1. Nella pagina [!DNL Adobe Stock Configurations], fai clic su **[!UICONTROL Crea]**.

1. Specifica un **[!UICONTROL Titolo]** per la configurazione cloud.

   Seleziona la configurazione IMS creata durante [la configurazione dell&#39;account IMS](#create-ims-account-configuration).

   Seleziona la lingua dall’elenco a discesa.

   ![aem-stock-cloud-config](assets/aem-stock-cloud-config.png)

1. Fai clic su **[!UICONTROL Salva e chiudi]**.

   L&#39;istanza dell&#39;autore [!DNL Experience Manager Assets] è ora integrata con [!DNL Adobe Stock]. È possibile creare più configurazioni di [!DNL Adobe Stock] (ad esempio, configurazioni basate sulle impostazioni locali). È ora possibile accedere, cercare e concedere in licenza le risorse [!DNL Adobe Stock] dall&#39;interfaccia utente di [!DNL Experience Manager].

   ![risorse-magazzino-ricerca](assets/aem-stock-searchstocks.png)

   >[!NOTE]
   >
   >In questa fase dell&#39;integrazione, solo gli amministratori possono accedere alle risorse [!DNL Adobe Stock], cercare le risorse Stock (utilizzando omnisearch) e concedere in licenza le risorse [!DNL Adobe Stock].
   >
   >Gli amministratori possono aggiungere altri utenti o gruppi al servizio cloud [!DNL Adobe Stock] e concedere autorizzazioni a questi utenti non amministratori in [!DNL Experience Manager] per accedere alla configurazione Stock.

1. Per aggiungere utenti o gruppi, selezionare la configurazione cloud [!DNL Adobe Stock] e fare clic su **[!UICONTROL Proprietà]**.

1. Cerca per aggiungere gli utenti o i gruppi ai quali hai assegnato le autorizzazioni per accedere alla configurazione di Adobe Stock. Vedi [assegnare le autorizzazioni al gruppo di utenti](#assign-permissions-to-group).


## Assegna autorizzazioni a gruppo di utenti {#assign-permissions-to-group}

Gli amministratori possono creare gruppi di utenti e concedere autorizzazioni ad alcuni utenti o gruppi per accedere al servizio cloud [!DNL Adobe Stock].

Di seguito sono riportate le autorizzazioni necessarie affinché un utente possa cercare e concedere in licenza le risorse Adobe Stock:

* Configura il percorso: `/conf/global/settings/stock`
* Privilegi: `jcr:read`
* Tipo di autorizzazione: `Allow`

Puoi creare un gruppo di utenti o assegnare le autorizzazioni a un gruppo di utenti esistente. Le autorizzazioni possono essere assegnate dall&#39;interfaccia [!DNL Experience Manager Assets] o dalla console [!DNL User Admin].

**Per fornire l&#39;accesso a un gruppo di utenti da [!DNL Experience Manager]:**

1. Nell&#39;interfaccia utente di [!DNL Experience Manager], passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Sicurezza]** > **[!UICONTROL Gruppi]**. Crea un gruppo utenti per [!DNL Adobe Stock].

1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Sicurezza]** > **[!UICONTROL Autorizzazioni]**.

1. Cerca il gruppo di utenti nel pannello a sinistra e aggiungi la nuova **[!UICONTROL voce di controllo di accesso]** per Adobe Stock.

   * Configura il percorso: `/conf/global/settings/stock`
   * Privilegi: `jcr:read`
   * Tipo di autorizzazione: `Allow`

   Fare clic su **[!UICONTROL Aggiungi]**.

   ![autorizzazioni-utente](assets/aem-stock-user-permissions.png)

1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Adobe Stock]**. Selezionare la configurazione cloud [!DNL Adobe Stock] e fare clic su **[!UICONTROL Proprietà]**.

1. Aggiungere il gruppo utenti appena creato alla configurazione [!DNL Adobe Stock]. Fai clic su **[!UICONTROL Salva e chiudi]**.

   ![assegna-utente](assets/aem-stock-adduser.png)

**Per fornire l&#39;accesso a un utente da [!DNL User Admin Console]:**

1. Aprire l&#39;Admin Console utente [!DNL Experience Manager]. URL predefinito: `http://localhost:4502/userdamin`.

1. Nel pannello a sinistra, cerca l&#39;utente immettendo `user_id` o `name`. Fare doppio clic per aprire le proprietà utente.

1. Passare alla scheda **[!UICONTROL Autorizzazioni]** e consentire le autorizzazioni `read` per la configurazione cloud [!DNL Adobe Stock]: `/conf/global/settings/stock`.

   >[!CAUTION]
   >
   >Se la configurazione cloud non è consentita, l&#39;utente può accedere solo a **[!UICONTROL Assets]** nell&#39;interfaccia [!DNL Experience Manager].
   >
   >Per consentire l&#39;accesso a [!UICONTROL risorse Assets] e [!DNL Adobe Stock], assicurati che la configurazione cloud sia consentita per l&#39;utente.

1. Fai clic su **[!UICONTROL Salva]** per aggiornare le autorizzazioni.

   ![assegna-utente-in-utente-amministratore](assets/aem-stock-user-admin-console.png)

1. Aggiungere l&#39;utente o il gruppo alla configurazione cloud [!DNL Adobe Stock].


## Accedere alle risorse di Adobe Stock {#access-stock-assets}

Un utente non amministratore con autorizzazioni per la configurazione cloud [!DNL Adobe Stock] può cercare e concedere in licenza le risorse [!DNL Adobe Stock] dall&#39;interfaccia [!DNL Experience Manager].

L&#39;utente deve eseguire un passaggio aggiuntivo per attivare la configurazione cloud [!DNL Adobe Stock] prima di accedere alle risorse [!DNL Adobe Stock]. Si tratta di un’attività una tantum. Se all&#39;utente vengono assegnate autorizzazioni su più configurazioni cloud [!DNL Adobe Stock], l&#39;utente può selezionare la configurazione desiderata tra le **[!UICONTROL Preferenze utente]**.

Per attivare la configurazione cloud [!DNL Adobe Stock]:

1. Accedi a [!DNL Experience Manager].

1. Fai clic sull&#39;icona utente in alto a destra, quindi fai clic su **[!UICONTROL Preferenze]**. Viene visualizzata la finestra **[!UICONTROL Preferenze utente]**.

1. Seleziona la **[!UICONTROL Configurazione Stock]** desiderata dall&#39;elenco a discesa e fai clic su **[!UICONTROL Accetta]** per attivare la configurazione.

   ![preferenze utente](assets/aem-stock-preferences.png)

1. Passa a **[!UICONTROL Assets]** > **[!UICONTROL Adobe Stock]**. È ora possibile visualizzare, cercare e concedere in licenza [!DNL Adobe Stock] risorse.

Nella tabella seguente viene illustrato il funzionamento delle autorizzazioni utente durante l&#39;accesso alle risorse [!DNL Adobe Stock]:

| User | Gruppo | Autorizzazioni | Accetta configurazione Stock nelle preferenze utente | Accedere ad Assets | Accedere ad Adobe Stock |
| --- | --- | --- | --- | --- | --- |
| admin | N/D | Tutti | N/D | Sì | Sì |
| test-doc1 | Utente DAM | /conf/global /settings/stock/cloud-config | Sì | Sì | Sì |
| test-doc1 | Utente DAM | /conf/global /settings/stock/cloud-config | No | Errore: impossibile caricare i dati | No |
| test-doc1 | Utente DAM | **consenti**: /conf/global /settings/stock     **nega**: /cloud-config | La configurazione Stock non è visibile | Sì | No |


## Usa e gestisci [!DNL Adobe Stock] risorse in [!DNL Experience Manager] {#usemanage}

Utilizzando questa funzionalità, le organizzazioni possono consentire ai propri utenti di lavorare utilizzando [!DNL Adobe Stock] risorse in [!DNL Experience Manager Assets]. Dall&#39;interfaccia utente di [!DNL Experience Manager], gli utenti possono cercare [!DNL Adobe Stock] risorse e concedere in licenza le risorse richieste.

Una volta ottenuta la licenza per una risorsa [!DNL Adobe Stock] in [!DNL Experience Manager], è possibile utilizzarla e gestirla come una risorsa tipica. In [!DNL Experience Manager], gli utenti possono cercare e visualizzare in anteprima le risorse; copiare e pubblicare le risorse; condividere le risorse in [!DNL Brand Portal]; accedere alle risorse e utilizzarle tramite l&#39;app desktop [!DNL Experience Manager] e così via.

![Cerca [!DNL Adobe Stock] risorse e filtra i risultati dall&#39;area di lavoro [!DNL Adobe Experience Manager]](assets/adobe-stock-search-results-workspace.png)

**A.** Cerca risorse simili a quelle di cui è stato fornito l&#39;ID [!DNL Adobe Stock]. **B.** Cerca risorse corrispondenti alla tua selezione di forma o orientamento. **C.** Cerca uno o più tipi di risorse supportati **D.** Apri o comprimi il riquadro dei filtri **E.** Concedi la licenza e salva la risorsa selezionata in [!DNL Experience Manager] **F.** Salva la risorsa in [!DNL Experience Manager] con filigrana **G.** Esplora le risorse nel sito Web [!DNL Adobe Stock] simili a quelle selezionate **H.** Visualizza le risorse selezionate nel sito Web [!DNL Adobe Stock] **I.** Numero di risorse selezionate dai risultati della ricerca **J.** 9} Passare dalla vista a schede alla vista a elenco

### Trovare le risorse {#find-assets}

Gli utenti di [!DNL Experience Manager] possono cercare risorse in [!DNL Experience Manager] e [!DNL Adobe Stock]. Quando il percorso di ricerca non è limitato a [!DNL Adobe Stock], vengono visualizzati i risultati di ricerca di [!DNL Experience Manager] e [!DNL Adobe Stock].

* Per cercare [!DNL Adobe Stock] risorse, fai clic su **[!UICONTROL Navigazione]** > **[!UICONTROL Assets]** > **[!UICONTROL Cerca in Adobe Stock]**.

* Per cercare le risorse tra [!DNL Adobe Stock] e [!DNL Experience Manager Assets], fai clic su Cerca ![cerca](assets/do-not-localize/search_icon.png).

In alternativa, inizia a digitare `Location: Adobe Stock` nella barra di ricerca per selezionare [!DNL Adobe Stock] risorse. [!DNL Experience Manager] offre funzionalità di filtro avanzate sulle risorse trovate, consentendo agli utenti di inserire rapidamente le risorse richieste utilizzando filtri, ad esempio tipi di risorse supportate, orientamento dell&#39;immagine e stato della licenza.

>[!NOTE]
>
>Assets ricercati da [!DNL Adobe Stock] sono visualizzati in [!DNL Experience Manager]. [!DNL Adobe Stock] risorse vengono recuperate e archiviate nell&#39;archivio [!DNL Experience Manager] solo dopo che un utente [salva una risorsa](/help/assets/aem-assets-adobe-stock.md#saveassets) o [licenze e salva una risorsa](/help/assets/aem-assets-adobe-stock.md#licenseassets). Le Assets già archiviate in [!DNL Experience Manager] vengono visualizzate ed evidenziate per semplificare l&#39;accesso e la consultazione. Inoltre, le risorse [!DNL Stock] vengono salvate con alcuni metadati aggiuntivi per indicare l&#39;origine come [!DNL Stock].

![Filtri di ricerca in [!DNL Experience Manager] ed evidenziate [!DNL Adobe Stock] risorse nei risultati di ricerca](assets/aem-search-filters2.jpg)

### Salva e visualizza le risorse richieste {#saveassets}

Selezionare una risorsa da salvare in [!DNL Experience Manager]. Fai clic su [!UICONTROL Salva] nella barra degli strumenti nella parte superiore e specifica il nome e il percorso della risorsa. Le risorse senza licenza vengono salvate localmente con una filigrana.

La prossima volta che cerchi risorse, le risorse salvate vengono evidenziate con un contrassegno, per indicare che tali risorse sono disponibili in [!DNL Experience Manager Assets].

>[!NOTE]
>
>Le risorse aggiunte di recente presentano un badge Nuovo invece di Un badge Concesso in licenza.

### Ottieni licenza per risorse {#licenseassets}

Gli utenti possono concedere in licenza [!DNL Adobe Stock] risorse utilizzando la quota del proprio piano aziendale [!DNL Adobe Stock]. Quando si concede in licenza una risorsa, questa viene salvata senza filigrana ed è disponibile per la ricerca e l&#39;utilizzo in [!DNL Experience Manager Assets].

![Finestra di dialogo per concedere in licenza e salvare [!DNL Adobe Stock] risorse in [!DNL Experience Manager Assets]](assets/aem-stock_licenseandsave.jpg)


### Accedere ai metadati e alle proprietà delle risorse {#access-metadata-and-asset-properties}

Gli utenti possono accedere e visualizzare in anteprima i metadati, incluse le proprietà dei metadati [!DNL Adobe Stock] per le risorse salvate in [!DNL Experience Manager], e aggiungere **[!UICONTROL Riferimenti licenza]** per una risorsa. Tuttavia, gli aggiornamenti al riferimento della licenza non sono sincronizzati tra il sito Web [!DNL Experience Manager] e [!DNL Adobe Stock].

Gli utenti possono visualizzare le proprietà sia per le risorse con licenza che per quelle senza licenza.

![Visualizzare e accedere ai metadati e ai riferimenti di licenza delle risorse salvate](assets/metadata_properties.jpg)


## Limitazioni note {#known-limitations}

* **Problemi di integrazione con [!DNL Experience Manager] Service Pack 6.5.7.0 e versioni successive**: è stato identificato un problema imprevisto durante l&#39;integrazione con [!DNL Experience Manager] 6.5.7.0 e versioni successive. Il problema è in fase di test e dovrebbe essere disponibile in [!DNL Experience Manager] 6.5.11.0. Contattare [!DNL Customer Support] per un hotfix immediato.

* **La funzionalità per impedire agli utenti di concedere licenze non funziona correttamente**: tutti gli utenti con autorizzazioni `read` per la configurazione Stock possono cercare e concedere licenze alle risorse [!DNL Adobe Stock].

* **Gli utenti non amministratori devono attivare manualmente la configurazione cloud [!DNL Adobe Stock]**: nella finestra **[!UICONTROL Preferenze utente]**, la **[!UICONTROL Configurazione Stock]** mostra la configurazione cloud [!DNL Adobe Stock] come abilitata, ma non funziona per un utente non amministratore. L&#39;utente deve fare clic sul pulsante **[!UICONTROL Accetta]** per attivare la configurazione Stock. In assenza di questo passaggio, verrà visualizzato un messaggio di errore durante l&#39;accesso a **[!UICONTROL Assets]**.

* **Avviso immagine editoriale non visualizzato**: quando si concede la licenza a un&#39;immagine, gli utenti non possono verificare se un&#39;immagine è Solo per uso editoriale. Per evitare possibili abusi, gli amministratori possono disattivare dall’Admin Console l’accesso alle risorse editoriali.

* **È stato visualizzato un tipo di licenza errato**: è possibile che in [!DNL Experience Manager] venga visualizzato un tipo di licenza errato per una risorsa. Gli utenti possono accedere al sito Web [!DNL Adobe Stock] per visualizzare il tipo di licenza.

* **I campi di riferimento e i metadati non sono sincronizzati**: quando un utente aggiorna un campo di riferimento licenza, le informazioni di riferimento licenza vengono aggiornate in [!DNL Experience Manager] ma non nel sito Web [!DNL Adobe Stock]. Analogamente, se l&#39;utente aggiorna i campi di riferimento nel sito Web [!DNL Adobe Stock], gli aggiornamenti non vengono sincronizzati in [!DNL Experience Manager].

>[!MORELIKETHIS]
>
>* [Esercitazione video sull&#39;utilizzo di [!DNL Adobe Stock] risorse con [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/creative-workflows/adobe-stock.html)
>* [[!DNL Adobe Stock] guida del piano Enterprise](https://helpx.adobe.com/enterprise/using/adobe-stock-enterprise.html)
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

