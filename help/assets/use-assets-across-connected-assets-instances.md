---
title: Utilizzare la funzione Risorse collegate per condividere risorse DAM in [!DNL Sites]
description: Utilizzate le risorse disponibili in una distribuzione [!DNL Adobe Experience Manager Assets] deployment when creating your web pages on another [!DNL Adobe Experience Manager Sites] remota.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 12c56c27c7f97f1029c757ec6d28f482516149d0
workflow-type: tm+mt
source-wordcount: '2246'
ht-degree: 41%

---


# Utilizzare la funzione Risorse collegate per condividere risorse DAM in [!DNL Experience Manager Sites] {#use-connected-assets-to-share-dam-assets-in-aem-sites}

Nelle grandi aziende l’infrastruttura necessaria per la creazione di siti web può essere dislocata in luoghi diversi. A volte, le funzionalità per la creazione di siti web e le risorse digitali utilizzate per creare i siti possono trovarsi in implementazioni diverse. Un motivo può essere rappresentato dalla distribuzione geografica delle implementazioni esistenti necessarie per lavorare in parallelo. Un altro motivo può essere costituito dalle acquisizioni che portano a un&#39;infrastruttura eterogenea che la società madre desidera utilizzare insieme.

Gli utenti possono creare pagine Web in [!DNL Experience Manager Sites]. [!DNL Experience Manager Assets] è il sistema Digital Asset Management (DAM) che fornisce le risorse necessarie per i siti Web. [!DNL Experience Manager] supporta ora il caso d&#39;uso di cui sopra integrando [!DNL Sites] e [!DNL Assets].

## Panoramica della funzione Risorse collegate {#overview-of-connected-assets}

When editing pages in [!UICONTROL Page Editor], the authors can seamlessly search, browse, and embed assets from a different [!DNL Assets] deployment. Gli amministratori creano un&#39;integrazione una tantum di una distribuzione [!DNL Sites] con una distribuzione diversa (remota) di [!DNL Assets].

For the [!DNL Sites] authors, the remote assets are available as read-only local assets. Questa funzionalità supporta la ricerca e l’utilizzo di un numero limitato di risorse remote alla volta. To make many remote assets available on a [!DNL Sites] deployment in one-go, consider migrating the assets in bulk. Consulta [guida](/help/assets/assets-migration-guide.md)alla migrazione delle risorse di Experience Manager.

### Prerequisiti e implementazioni supportate {#prerequisites}

Prima di utilizzare o configurare questa funzionalità, verifica questi aspetti:

* Gli utenti fanno parte dei gruppi di utenti appropriati per ciascuna distribuzione.
* For [!DNL Adobe Experience Manager] deployment types, one of the supported criteria is met. [!DNL Experience Manager] 6.5 [!DNL Assets] funziona [!DNL Experience Manager] come Cloud Service. Per ulteriori informazioni, consulta la sezione relativa alla funzionalità delle risorse [collegate in  Experience Manager come Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/use-assets-across-connected-assets-instances.html).

   |  | [!DNL Sites] come Cloud Service | [!DNL Experience Manager] 6.5 [!DNL Sites] su AMS | [!DNL Experience Manager] 6.5 [!DNL Sites] locale |
   |---|---|---|---|
   | **[!DNL Experience Manager Assets]come Cloud Service** | Supportato | Supportato | Supportato |
   | **[!DNL Experience Manager]6.5 [!DNL Assets] su AMS** | Supportato | Supportato | Supportato |
   | **[!DNL Experience Manager]6.5 [!DNL Assets] locale** | Non supportato | Non supportato | Non supportato |

### Formati di file supportati {#mimetypes}

Gli autori ricercano le immagini e i seguenti tipi di documenti in Content Finder e utilizzano le risorse ricercate in Editor pagina. I documenti vengono aggiunti al `Download` componente e le immagini al `Image` componente. Authors also add the remote assets in any custom [!DNL Experience Manager] component that extends the default `Download` or `Image` components. I formati supportati sono:

* **Formati** immagine: Formati supportati dal componente [](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/image.html) Immagine. [!DNL Dynamic Media] le immagini non sono supportate.
* **Formati** del documento: Vedere i formati [di documento](assets-formats.md#supported-document-formats)supportati.

### Utenti e gruppi interessati {#users-and-groups-involved}

Di seguito sono descritti i diversi ruoli coinvolti nella configurazione e nell’utilizzo della funzionalità e i relativi gruppi di utenti. L&#39;ambito locale viene utilizzato per il caso di utilizzo in cui un autore crea una pagina Web. L’ambito remoto viene utilizzato per l’implementazione DAM in cui sono ospitate le risorse necessarie. The [!DNL Sites] author fetches these remote assets.

| Ruolo | Ambito | Gruppo di utenti | Nome utente nella procedura dettagliata | Requisito |
|---|---|---|---|---|
| [!DNL Sites] administrator | Locale | [!DNL Experience Manager] `administrators` | `admin` | Set up [!DNL Experience Manager] and configure integration with the remote [!DNL Assets] deployment. |
| Utente DAM | Locale | `Authors` | `ksaner` | Utilizzato per visualizzare e duplicare le risorse recuperate in `/content/DAM/connectedassets/`. |
| [!DNL Sites] author | Locale | `Authors` (con accesso in lettura sul DAM remoto e accesso dell&#39;autore sul locale [!DNL Sites]) | `ksaner` | End user are [!DNL Sites] authors who use this integration to improve their content velocity. The authors search and browse assets in remote DAM using [!UICONTROL Content Finder] and using the required images in local web pages. Vengono utilizzate le credenziali dell’utente `ksaner` di DAM. |
| [!DNL Assets] administrator | Remoto | [!DNL Experience Manager] `administrators` | `admin` su remoto [!DNL Experience Manager] | Configurare la condivisione risorse tra le origini (CORS, Cross-Origin Resource Sharing). |
| Utente DAM | Remoto | `Authors` | `ksaner` su remoto [!DNL Experience Manager] | Author role on the remote [!DNL Experience Manager] deployment. Search and browse assets in Connected Assets using the [!UICONTROL Content Finder]. |
| Distributore DAM (utente tecnico) | Remoto | [!DNL Sites] `Authors` | `ksaner` su remoto [!DNL Experience Manager] | This user present on the remote deployment is used by [!DNL Experience Manager] local server (not the [!DNL Sites] author role) to fetch the remote assets, on behalf of [!DNL Sites] author. Questo ruolo non è lo stesso dei due ruoli `ksaner` precedenti e appartiene a un gruppo di utenti diverso. |

## Configure a connection between [!DNL Sites] and [!DNL Assets] deployments {#configure-a-connection-between-sites-and-assets-deployments}

An [!DNL Experience Manager] administrator can create this integration. Una volta create, le autorizzazioni necessarie per utilizzarle vengono stabilite tramite i gruppi di utenti. I gruppi di utenti sono definiti nella [!DNL Sites] distribuzione e nella distribuzione DAM.

To configure Connected Assets and local [!DNL Sites] connectivity, follow these steps:

1. Access an existing [!DNL Sites] deployment or create a deployment using the following command:

   1. In the folder of the JAR file, execute the following command on a terminal to create each [!DNL Experience Manager] server.
      `java -XX:MaxPermSize=768m -Xmx4096m -jar <quickstart jar filepath> -r samplecontent -p 4502 -nofork -gui -nointeractive &`

   1. After a few minutes, the [!DNL Experience Manager] server starts successfully. Consider this [!DNL Sites] deployment as the local machine for web page authoring, say at `https://[local_sites]:4502`.

1. Ensure that the users and roles with local scope exist on the [!DNL Sites] deployment and on the [!DNL Assets] deployment on AMS. Create a technical user on [!DNL Assets] deployment and add to the user group mentioned in [users and groups involved](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved).

1. Access the local [!DNL Sites] deployment at `https://[local_sites]:4502`. Fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Configurazione risorse collegate]** e fornisci i seguenti valori:

   1. [!DNL Assets] la posizione è `https://[assets_servername_ams]:[port]`.
   1. Credenziali di un distributore DAM (utente tecnico).
   1. In the **[!UICONTROL Mount Point]** field, enter the local [!DNL Experience Manager] path where [!DNL Experience Manager] fetches the assets. Ad esempio, la cartella `remoteassets`.
   1. Regola i valori di **[!UICONTROL Soglia ottimizzazione trasferimento binario originale]** in base alla rete. Il rendering di una risorsa con dimensioni superiori alla soglia viene trasferito in modo asincrono.
   1. Seleziona **[!UICONTROL Archivio dati condiviso con risorse collegate]** se per memorizzare le risorse utilizzi un archivio dati in comune tra le due implementazioni di In questo caso, il limite di soglia non ha importanza in quanto i dati binari effettivi delle risorse risiedono nell’archivio dati e non vengono trasferiti.

   ![Configurazione tipica per Risorse collegate](assets/connected-assets-typical-config.png)

   *Figura: una configurazione tipica per Risorse collegate.*

1. Poiché le risorse sono già state elaborate e i rendering vengono recuperati, disattiva i moduli di avvio dei flussi di lavoro. Adjust the launcher configurations on the local ([!DNL Sites]) deployment to exclude the `connectedassets` folder, in which the remote assets are fetched.

   1. On [!DNL Sites] deployment, click **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Launchers]**.

   1. Individua i moduli di avvio con flussi di lavoro come **[!UICONTROL Aggiorna risorsa DAM]** e **[!UICONTROL Writeback di metadati DAM]**.

   1. Seleziona il modulo di avvio del flusso di lavoro e fai clic su **[!UICONTROL Proprietà]** nella barra delle azioni.

   1. In the [!UICONTROL Properties] wizard, change the **[!UICONTROL Path]** fields as the following mappings to update their regular expressions to exclude the mount point **[!UICONTROL connectedassets]**.

   | Prima | Dopo |
   |---|---|
   | `/content/dam(/((?!/subassets).)*/)renditions/original` | `/content/dam(/((?!/subassets)(?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*/)renditions/original` | `/content/dam(/((?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*)/jcr:content/metadata` | `/content/dam(/((?!connectedassets).)*/)jcr:content/metadata` |

   >[!NOTE]
   >
   >Quando gli autori recuperano una risorsa, vengono recuperati tutti i rendering disponibili nell’implementazione remota. Se desideri creare più rendering per una risorsa recuperata, ignora questo passaggio di configurazione. The [!UICONTROL DAM Update Asset] workflow gets triggered and creates more renditions. These renditions are available only on the local [!DNL Sites] deployment and not on the remote DAM deployment.

1. Add the [!DNL Sites] deployment as one of the **[!UICONTROL Allowed Origins]** on the remote [!DNL Assets'] CORS configuration.

   1. Effettuate l&#39;accesso utilizzando le credenziali dell&#39;amministratore. Cerca `Cross-Origin`. Accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > Console Web ****.

   1. To create a CORS configuration for [!DNL Sites] deployment, click add option ![Assets add icon](assets/do-not-localize/assets_add_icon.png) next to **[!UICONTROL Adobe Granite Cross-Origin Resource Sharing Policy]**.

   1. In the field **[!UICONTROL Allowed Origins]**, input the URL of the local [!DNL Sites], that is, `https://[local_sites]:[port]`. Salva la configurazione.

## Utilizzare le risorse remote {#use-remote-assets}

Gli autori del sito Web utilizzano Content Finder per connettersi alla distribuzione DAM. Gli autori possono sfogliare, cercare e trascinare le risorse remote in un componente. Per eseguire l’autenticazione nel DAM remoto, tieni a portata di mano le credenziali dell’utente DAM fornite dal tuo amministratore.

Gli autori possono utilizzare le risorse disponibili nella DAM locale e nella distribuzione DAM remota, in una singola pagina Web. Utilizza Content Finder per passare dalla ricerca nel DAM locale alla ricerca nel DAM remoto.

Vengono recuperati solo i tag delle risorse remote con un tag corrispondente esatto insieme alla stessa gerarchia di tassonomia, disponibile nella [!DNL Sites] distribuzione locale. Tutti gli altri tag vengono eliminati. Authors can search for remote assets using all the tags present on the remote [!DNL Experience Manager] deployment, as it offers a full-text search.

### Procedura dettagliata per l’utilizzo {#walk-through-of-usage}

Utilizza la configurazione precedente per provare l’esperienza di authoring e comprendere il funzionamento di questa caratteristica. Utilizza documenti o immagini di tua scelta nell’implementazione remota di DAM.

1. Navigate to the [!DNL Assets] interface on the remote deployment by accessing **[!UICONTROL Assets]** > **[!UICONTROL Files]** from [!DNL Experience Manager] workspace. In alternativa, puoi accedere a `https://[assets_servername_ams]:[port]/assets.html/content/dam` in un browser. Carica le risorse che hai scelto.
1. On the [!DNL Sites] deployment, in the profile activator in the upper-right corner, click **[!UICONTROL Impersonate as]**. Specifica `ksaner` come nome utente, seleziona l’opzione fornita e fai clic su **[!UICONTROL OK]**.
1. Apri una pagina del sito web We.Retail in **[!UICONTROL Sites]** > **[!UICONTROL We.Retail]** > **[!UICONTROL us]** > **[!UICONTROL en]**. Modifica la pagina. In alternativa, accedi a `https://[aem_server]:[port]/editor.html/content/we-retail/us/en/men.html` tramite un browser per modificare una pagina.

   Fai clic su **[!UICONTROL Attiva/Disattiva pannello laterale]** nell’angolo in alto a sinistra della pagina.

1. Open the [!UICONTROL Assets] tab and click **[!UICONTROL Log in to Connected Assets]**.
1. Immetti le credenziali: `ksaner` come nome utente e `password` come password. This user has authoring permissions on both the [!DNL Experience Manager] deployments.
1. Cerca la risorsa aggiunta a DAM. Le risorse remote vengono visualizzate nel pannello a sinistra. Filtra immagini o documenti e filtra ulteriormente i tipi di documenti supportati. Trascina le immagini su un componente `Image`, e i documenti su un componente `Download`.

   The fetched assets are read-only on the local [!DNL Sites] deployment. You can still use the options provided by your [!DNL Sites] components to edit the fetched asset. La modifica per componenti non è distruttiva.

   ![Opzioni di filtro per tipi di documenti e immagini nella ricerca di risorse in DAM remoto](assets/filetypes_filter_connected_assets.png)

   *Figura: opzioni di filtro per tipi di documenti e immagini nella ricerca di risorse in DAM remoto.*

1. Un autore del sito riceve una notifica se una risorsa viene recuperata in modo asincrono e se un’attività di recupero ha esito negativo. Durante l’authoring, o anche successivamente, gli autori possono visualizzare informazioni dettagliate sulle attività di recupero e sugli errori nell’interfaccia utente [Processi asincroni](/help/sites-administering/asynchronous-jobs.md).

   ![Notifica relativa al recupero asincrono delle risorse in background.](assets/assets_async_transfer_fails.png)

   *Figura: notifica relativa al recupero asincrono delle risorse in background.*

1. When publishing a page, [!DNL Experience Manager] displays a complete list of assets that are used on the page. Assicurati che le risorse remote vengano recuperate correttamente al momento della pubblicazione. Per verificare lo stato di ciascuna risorsa recuperata, consulta l’interfaccia utente dei [processi asincroni](/help/sites-administering/asynchronous-jobs.md).

   >[!NOTE]
   >
   >La pagina viene pubblicata anche se una o più risorse remote non vengono recuperate. Il componente che utilizza la risorsa remota viene pubblicato come vuoto. The [!DNL Experience Manager] notification area displays a notification for errors that show in async jobs page.

>[!CAUTION]
>
>Una volta utilizzate in una pagina Web, le risorse remote recuperate sono ricercabili e utilizzabili da chiunque disponga delle autorizzazioni per accedere alla cartella locale. Le risorse recuperate vengono memorizzate nella cartella locale (`connectedassets` nel passaggio precedente). Le risorse possono inoltre essere cercate e visualizzate nell’archivio locale tramite [!UICONTROL Content Finder].

Le risorse recuperate possono essere utilizzate come qualsiasi altra risorsa locale, ad eccezione del fatto che i metadati associati non possono essere modificati.

## Limitazioni  and best practices {#tips-and-limitations}

* Per informazioni dettagliate sull’utilizzo delle risorse, configurate la funzionalità [Asset Insight](/help/assets/asset-insights.md) nell’ [!DNL Sites] istanza.

### Gestione delle autorizzazioni e delle risorse {#permissions-and-managing-assets}

* Le risorse locali non vengono sincronizzate con le risorse originali nell’implementazione remota. Eventuali modifiche, eliminazioni o revoche delle autorizzazioni nell’implementazione DAM non vengono propagate downstream.
* Le risorse locali sono copie in sola lettura. [!DNL Experience Manager]I componenti apportano modifiche non distruttive alle risorse. Non sono consentite altre modifiche.
* Le risorse recuperate localmente sono disponibili solo a scopo di authoring. I flussi di lavoro di aggiornamento delle risorse non possono essere applicati e i metadati non possono essere modificati.
* Sono supportati solo le immagini e i formati di documento elencati. [!DNL Dynamic Media]Le risorse , i frammenti di contenuto e i frammenti di esperienza non sono supportati.
* [!DNL Experience Manager] non recupera gli schemi di metadati. Ciò significa che tutti i metadati recuperati potrebbero non essere visualizzati. Se lo schema viene aggiornato separatamente, vengono visualizzate tutte le proprietà.
* Tutti [!DNL Sites] gli autori dispongono delle autorizzazioni di lettura sulle copie recuperate, anche se gli autori non possono accedere alla distribuzione DAM remota.
* Nessun supporto API per personalizzare l’integrazione.
* Questa funzionalità supporta la ricerca e l’utilizzo diretti delle risorse remote. Per rendere disponibili molte risorse remote nell’implementazione locale con un’unica operazione, è consigliabile eseguire la migrazione delle risorse. Consulta la [guida alla migrazione di Assets](assets-migration-guide.md).
* Non è possibile utilizzare una risorsa remota come miniatura di pagina nell’interfaccia utente Proprietà  pagina. Per impostare una miniatura di una pagina Web nell’interfaccia utente Proprietà  pagina dalla [!UICONTROL miniatura] , fare clic su [!UICONTROL Seleziona immagine].

### Configurazione e licenze {#setup-licensing}

* [!DNL Assets] la distribuzione [!DNL Adobe Managed Services] è supportata.
* [!DNL Sites] può connettersi a un singolo [!DNL Assets] archivio alla volta.
* A license of [!DNL Assets] working as remote repository.
* One or more licenses of [!DNL Sites] working as local authoring deployment.

### Utilizzo {#usage}

* Gli utenti possono cercare risorse remote e trascinarle sulla pagina locale durante l’authoring. Non sono supportate altre funzionalità.
* L’operazione di recupero si interrompe per timeout dopo 5 secondi. Gli autori possono rilevare dei problemi durante il recupero delle risorse, ad esempio in caso di problemi di rete. Authors can reattempt by dragging the remote asset from [!UICONTROL Content Finder] to [!UICONTROL Page Editor].
* Le risorse recuperate possono essere sottoposte a semplici modifiche non distruttive e alle modifiche supportate tramite il componente `Image` di Le risorse sono di sola lettura.
* L’unico metodo per recuperare nuovamente la risorsa consiste nel trascinarla su una pagina. Non esiste un supporto API o altri metodi per recuperare nuovamente una risorsa e aggiornarla.
* Se le risorse vengono disattivate dal DAM, continueranno a essere utilizzate sulle [!DNL Sites] pagine.

## Risoluzione dei problemi {#troubleshoot}

Per risolvere eventuali problemi relativi allo scenario di errore comune, procedere come segue:

* If you are unable to search for remote assets from the [!UICONTROL Content Finder], then ensure that the required roles and permissions are in place.
* Una risorsa recuperata dalla diga remota potrebbe non essere pubblicata su una pagina Web per uno o più motivi. Non esiste sul server remoto, mancano le autorizzazioni necessarie per recuperarlo o l&#39;errore di rete può essere dovuto a cause. Assicurarsi che la risorsa non venga rimossa dal DAM remoto. Verificate che siano disponibili le autorizzazioni appropriate e che i prerequisiti siano soddisfatti. Provate ad aggiungere la risorsa alla pagina e ripubblicatela. Controlla l’[elenco dei processi asincroni](/help/sites-administering/asynchronous-jobs.md) per verificare la presenza di errori nel recupero delle risorse.
* Se non riuscite ad accedere alla distribuzione DAM remota dalla [!DNL Sites] distribuzione locale, accertatevi che i cookie intersito siano consentiti. Se i cookie cross-site sono bloccati, le due distribuzioni di [!DNL Experience Manager] potrebbero non essere autenticate. Ad esempio, [!DNL Google Chrome] in modalità Incognito i cookie di terze parti possono essere bloccati. Per consentire i cookie nel [!DNL Chrome] browser, fai clic sull&#39;icona a forma di occhio nella barra degli indirizzi, vai a Sito che non funziona > Bloccato, seleziona l&#39;URL DAM remoto e consenti il cookie del token di login. In alternativa, consulta la guida su [come abilitare i cookie](https://support.google.com/chrome/answer/95647)di terze parti.

   ![Errore del cookie in Chrome in modalità incognito](assets/chrome-cookies-incognito-dialog.png)
