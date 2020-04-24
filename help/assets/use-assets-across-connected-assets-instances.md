---
title: Utilizza le risorse collegate per condividere le risorse DAM nel flusso di lavoro di authoring di [!DNL Adobe Experience Manager Sites].
description: Utilizzate le risorse disponibili in una distribuzione remota di [!DNL Risorse Adobe Experience Manager] quando create le pagine Web in un'altra distribuzione del sito Experience Manager.
contentOwner: AG
translation-type: tm+mt
source-git-commit: abc4821ec3720969bf1c2fb068744c07477aca46

---


# Utilizzare la funzione Risorse collegate per condividere risorse DAM in [!DNL Experience Manager Sites] {#use-connected-assets-to-share-dam-assets-in-aem-sites}

Nelle grandi aziende l’infrastruttura necessaria per la creazione di siti web può essere dislocata in luoghi diversi. A volte, le funzionalità per la creazione di siti web e le risorse digitali utilizzate per creare i siti possono trovarsi in implementazioni diverse. Tale dislocazione può essere dovuta a implementazioni esistenti distribuite geograficamente che devono operare in parallelo oppure infrastrutture eterogenee in seguito ad acquisizioni e che la società madre desidera mantenere.

[!DNL Adobe Experience Manager Sites] offre la funzionalità di creazione di pagine web e è il sistema di gestione delle risorse digitali (DAM) che fornisce le risorse necessarie per i siti web. [!DNL Adobe Experience Manager Assets] [!DNL Experience Manager] supporta ora il caso d&#39;uso di cui sopra integrando [!DNL Experience Manager Sites] e [!DNL Experience Manager Assets].

## Panoramica della funzione Risorse collegate {#overview-of-connected-assets}

When editing pages in Page Editor, the authors can seamlessly search, browse, and embed assets from a different [!DNL Experience Manager Assets] deployment. To do an [!DNL Experience Manager] administrator do a one-time integration of a local deployment of [!DNL Experience Manager Sites] with a different (remote) deployment of [!DNL Experience Manager Assets].

For the [!DNL Sites] authors, the remote assets are available as read-only local assets. Questa funzionalità supporta la ricerca e l’utilizzo di un numero limitato di risorse remote alla volta. Per rendere disponibili contemporaneamente numerose risorse remote in un’implementazione locale, è consigliabile effettuare una migrazione in massa delle risorse. Consulta la guida [alla migrazione delle risorse di](/help/assets/assets-migration-guide.md)Experience Manager.

### Prerequisiti e implementazioni supportate {#prerequisites}

Prima di utilizzare o configurare questa funzionalità, verifica questi aspetti:

* Gli utenti fanno parte dei gruppi di utenti appropriati per ciascuna implementazione.
* Per i tipi di implementazione di Adobe Experience Manager, deve essere soddisfatto uno dei criteri supportati. [!DNL Experience Manager] 6.5 [!DNL Assets] funziona con [!DNL Experience Manager] un servizio cloud. Per ulteriori informazioni, consulta la sezione relativa alla funzionalità delle risorse [connesse in Experience Manager come servizio](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/assets/admin/use-assets-across-connected-assets-instances.html)cloud.

   |  | [!DNL Experience Manager Sites] come servizio Cloud | Experience Manager 6.5 [!DNL Sites] su AMS | Experience Manager 6.5 [!DNL Sites] locale |
   |---|---|---|---|
   | **[!DNL Experience Manager Assets]come servizio Cloud ** | Supportato | Supportato | Supportato |
   | **Experience Manager 6.5[!DNL Assets]su AMS** | Supportato | Supportato | Supportato |
   | **Experience Manager 6.5[!DNL Assets]locale** | Non supportato | Non supportato | Non supportato |

### Formati di file supportati {#mimetypes}

Gli autori possono cercare in Content Finder le immagini e i tipi di documenti indicati di seguito, quindi utilizzare nell’Editor pagina le risorse che hanno cercato. È possibile aggiungere i documenti al componente `Download`, e le immagini al componente `Image`. Authors can also add the remote assets in any custom Experience Manager component that extends the default `Download` or `Image` components. L&#39;elenco dei formati supportati è:

* **Formati** immagine: I formati immagine supportati dal componente [](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/components/image.html) Immagine sono supportati da Risorse collegate. [!DNL Dynamic Media] le immagini non sono supportate.
* **Formati di documenti**: vedi [Formati di documenti supportati da Risorse collegate](assets-formats.md#supported-document-formats).

### Utenti e gruppi interessati {#users-and-groups-involved}

Di seguito sono descritti i diversi ruoli coinvolti nella configurazione e nell’utilizzo della funzionalità e i relativi gruppi di utenti. L’ambito locale viene utilizzato per il caso d’uso in cui una pagina web viene creata da un autore. L’ambito remoto viene utilizzato per l’implementazione DAM in cui sono ospitate le risorse necessarie. The [!DNL Sites] author fetches these remote assets.

| Ruolo | Ambito | Gruppo di utenti | Nome utente nella procedura dettagliata | Requisito |
|---|---|---|---|---|
| [!DNL Sites] administrator | Locale | Amministratore Experience Manager | `admin` | Set up Experience Manager, configure integration with the remote [!DNL Assets] deployment. |
| Utente DAM | Locale | Autore | `ksaner` | Utilizzato per visualizzare e duplicare le risorse recuperate in `/content/DAM/connectedassets/`. |
| [!DNL Sites] author | Locale | Author (with read access on the remote DAM and author access on local [!DNL Sites]) | `ksaner` | End user are [!DNL Sites] authors who use this integration to improve their content velocity. Gli autori ricercano e sfogliano le risorse in DAM remoto utilizzando Content Finder e utilizzando le immagini richieste nelle pagine web locali. Vengono utilizzate le credenziali dell’utente `ksaner` di DAM. |
| [!DNL Assets] administrator | Remoto | Amministratore Experience Manager | `admin` su Remote Experience Manager | Configurare la condivisione risorse tra le origini (CORS, Cross-Origin Resource Sharing). |
| Utente DAM | Remoto | Autore | `ksaner` su Remote Experience Manager | Ruolo di authoring nella distribuzione remota di Experience Manager. Cercare e sfogliare le risorse in Risorse collegate mediante Content Finder. |
| Distributore DAM (utente tecnico) | Remoto | Creatori di pacchetti e autori di siti | `ksaner` su Remote Experience Manager | This user present on the remote deployment is used by Experience Manager local server (not the Site author role) to fetch the remote assets, on behalf of [!DNL Sites] author. Questo ruolo non è lo stesso dei due ruoli `ksaner` precedenti e appartiene a un gruppo di utenti diverso. |

## Configure a connection between [!DNL Sites] and [!DNL Assets] deployments {#configure-a-connection-between-sites-and-assets-deployments}

Un amministratore di Experience Manager può creare questa integrazione. Once created, the permissions required to use it are established via user groups that are defined on the [!DNL Sites] deployment and on the DAM deployment.

To configure Connected Assets and local [!DNL Sites] connectivity, follow these steps.

1. Access an existing [!DNL Experience Manager Sites] deployment or create a deployment using the following command:

   1. Nella cartella del file JAR, esegui il comando seguente su un terminale per creare ogni server Experience Manager.
      `java -XX:MaxPermSize=768m -Xmx4096m -jar <quickstart jar filepath> -r samplecontent -p 4502 -nofork -gui -nointeractive &`

   1. Dopo alcuni minuti, il server Experience Manager si avvia correttamente. Consider this [!DNL Experience Manager Sites] deployment as the local machine for web page authoring, say at `https://[local_sites]:4502`.

1. Ensure that the users and roles with local scope exist on the Experience Manager Sites deployment and on the [!DNL Experience Manager Assets] deployment on AMS. Create a technical user on [!DNL Assets] deployment and add to the user group mentioned in [users and groups involved](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved).

1. Access the local [!DNL Experience Manager Sites] deployment at `https://[local_sites]:4502`. Fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Configurazione risorse collegate]** e fornisci i seguenti valori:

   1. [!DNL Experience Manager Assets] la posizione è `https://[assets_servername_ams]:[port]`.
   1. Credenziali di un distributore DAM (utente tecnico).
   1. In **[!UICONTROL Mount Point]** field, enter the local Experience Manager path where Experience Manager fetches the assets. Ad esempio, la cartella `remoteassets`.
   1. Regola i valori di **[!UICONTROL Soglia ottimizzazione trasferimento binario originale]** in base alla rete. Il rendering di una risorsa con dimensioni superiori alla soglia viene trasferito in modo asincrono.
   1. Select **[!UICONTROL Datastore Shared with Connected Assets]**, if you use a datastore to store your assets and the Datastore is the common storage between both Experience Manager deployments. In questo caso, il limite di soglia non ha importanza in quanto i dati binari effettivi delle risorse risiedono nell’archivio dati e non vengono trasferiti.
      ![Configurazione tipica per Risorse collegate](assets/connected-assets-typical-config.png)
   *Figura: una configurazione tipica per Risorse collegate.*

1. Poiché le risorse sono già state elaborate e i rendering vengono recuperati, disattiva i moduli di avvio dei flussi di lavoro. Adjust the launcher configurations on the local ([!DNL Experience Manager Sites]) deployment to exclude the `connectedassets` folder, in which the remote assets are fetched.

   1. On [!DNL Experience Manager Sites] deployment, click **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Launchers]**.

   1. Individua i moduli di avvio con flussi di lavoro come **[!UICONTROL Aggiorna risorsa DAM]** e **[!UICONTROL Writeback di metadati DAM]**.

   1. Seleziona il modulo di avvio del flusso di lavoro e fai clic su **[!UICONTROL Proprietà]** nella barra delle azioni.

   1. Nella procedura guidata Proprietà, modifica i campi **[!UICONTROL Percorso]** in base alle mappature seguenti per aggiornare le espressioni regolari al fine di escludere il punto di montaggio **[!UICONTROL connectedassets]**.
   | Prima | Dopo |
   |---|---|
   | `/content/dam(/((?!/subassets).)*/)renditions/original` | `/content/dam(/((?!/subassets)(?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/*/)renditions/original` | `/content/dam(/((?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/*)/jcr:content/metadata` | `/content/dam(/((?!connectedassets).)*/)jcr:content/metadata` |

   >[!NOTE]
   >
   >Quando gli autori recuperano una risorsa, vengono recuperate tutte le rappresentazioni disponibili nella distribuzione remota di Experience Manager. Se desideri creare più rendering per una risorsa recuperata, ignora questo passaggio di configurazione. The [!UICONTROL DAM Update Asset] workflow gets triggered and creates more renditions. These renditions are available only on the local [!DNL Sites] deployment and not on the remote DAM deployment.

1. Add the [!DNL Experience Manager Sites] instance as one of the **[!UICONTROL Allowed Origins]** on the remote [!DNL Experience Manager Assets] CORS configuration.

   1. Accedi con le credenziali di amministratore. Cerca `Cross-Origin`. Accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > Console Web ****.

   1. To create a CORS configuration for [!DNL Experience Manager Sites] instance, click ![aem_assets_add_icon](assets/aem_assets_add_icon.png) icon next to **[!UICONTROL Adobe Granite Cross-Origin Resource Sharing Policy]**.

   1. In the field **[!UICONTROL Allowed Origins]**, input the URL of the local [!DNL Sites], that is, `https://[local_sites]:[port]`. Salva la configurazione.

## Utilizzare le risorse remote {#use-remote-assets}

Gli autori del sito web utilizzano Content Finder per connettersi all’istanza DAM. Gli autori possono sfogliare, cercare e trascinare le risorse remote in un componente. Per eseguire l’autenticazione nel DAM remoto, tieni a portata di mano le credenziali dell’utente DAM fornite dal tuo amministratore.

Gli autori possono utilizzare le risorse disponibili in una singola pagina web, sia nelle istanze DAM locali che in quelle DAM remote. Utilizza Content Finder per passare dalla ricerca nel DAM locale alla ricerca nel DAM remoto.

Only those tags of remote assets are fetched that have an exact corresponding tag along with the same taxonomy hierarchy, available on the local [!DNL Sites] instance. Tutti gli altri tag vengono eliminati. Gli autori possono cercare risorse remote utilizzando tutti i tag presenti nella distribuzione remota di Experience Manager, in quanto Experience Manager offre una ricerca full-text.

### Procedura dettagliata per l’utilizzo {#walk-through-of-usage}

Utilizza la configurazione precedente per provare l’esperienza di authoring e comprendere il funzionamento di questa caratteristica. Utilizza documenti o immagini di tua scelta nell’implementazione remota di DAM.

1. Navigate to the [!DNL Assets] user interface on the remote deployment by accessing **[!UICONTROL Assets]** > **[!UICONTROL Files]** from [!DNL Experience Manager] workspace. In alternativa, puoi accedere a `https://[assets_servername_ams]:[port]/assets.html/content/dam` in un browser. Carica le risorse che hai scelto.
1. On the [!DNL Sites] instance, in the profile activator in the upper-right corner, click **[!UICONTROL Impersonate as]**. Specifica `ksaner` come nome utente, seleziona l’opzione fornita e fai clic su **[!UICONTROL OK]**.
1. Apri una pagina del sito web We.Retail in **[!UICONTROL Sites]** > **[!UICONTROL We.Retail]** > **[!UICONTROL us]** > **[!UICONTROL en]**. Modifica la pagina. In alternativa, accedi a `https://[aem_server]:[port]/editor.html/content/we-retail/us/en/men.html` tramite un browser per modificare una pagina.

   Fai clic su **[!UICONTROL Attiva/Disattiva pannello laterale]** nell’angolo in alto a sinistra della pagina.

1. Open the [!UICONTROL Assets] tab and click **[!UICONTROL Log in to Connected Assets]**.
1. Immetti le credenziali: `ksaner` come nome utente e `password` come password. This user has authoring permissions on both the [!DNL Experience Manager] deployments.
1. Cerca la risorsa aggiunta a DAM. Le risorse remote vengono visualizzate nel pannello a sinistra. Filtra immagini o documenti e filtra ulteriormente i tipi di documenti supportati. Trascina le immagini su un componente `Image`, e i documenti su un componente `Download`.

   The fetched assets are read-only on the local [!DNL Experience Manager Sites] deployment. You can still use the options provided by your [!DNL Experience Manager Sites] components to edit the fetched asset. La modifica per componenti non è distruttiva.

   ![Opzioni di filtro per tipi di documenti e immagini nella ricerca di risorse in DAM remoto](assets/filetypes_filter_connected_assets.png)

   *Figura: opzioni di filtro per tipi di documenti e immagini nella ricerca di risorse in DAM remoto.*

1. Un autore del sito riceve una notifica se una risorsa viene recuperata in modo asincrono e se un’attività di recupero ha esito negativo. Durante l’authoring, o anche successivamente, gli autori possono visualizzare informazioni dettagliate sulle attività di recupero e sugli errori nell’interfaccia utente [Processi asincroni](/help/assets/asynchronous-jobs.md).

   ![Notifica relativa al recupero asincrono delle risorse in background.](assets/assets_async_transfer_fails.png)

   *Figura: notifica relativa al recupero asincrono delle risorse in background.*

1. When publishing a page, [!DNL Experience Manager] displays a complete list of assets that are used in the page. Assicurati che le risorse remote vengano recuperate correttamente al momento della pubblicazione. Per verificare lo stato di ciascuna risorsa recuperata, consulta l’interfaccia utente dei [processi asincroni](/help/assets/asynchronous-jobs.md).

   >[!NOTE]
   >
   >La pagina viene pubblicata anche se una o più risorse remote non vengono recuperate. Il componente che utilizza la risorsa remota viene pubblicato come vuoto. The [!DNL Experience Manager] notification area displays notification for errors that show in async jobs page.

>[!CAUTION]
>
>Una volta utilizzate in una pagina web, le risorse remote recuperate possono essere cercate e utilizzate da qualsiasi utente con autorizzazioni di accesso alla cartella locale in cui sono memorizzate (nel passaggio precedente: `connectedassets`). Le risorse possono inoltre essere cercate e visualizzate nell’archivio locale tramite [!UICONTROL Content Finder].

Le risorse recuperate possono essere utilizzate come qualsiasi altra risorsa locale, ad eccezione del fatto che i metadati associati non possono essere modificati.

## Limitazioni    {#limitations}

**Autorizzazioni e gestione delle risorse**

* Le risorse locali non vengono sincronizzate con le risorse originali nell’implementazione remota. Eventuali modifiche, eliminazioni o revoche delle autorizzazioni nell’implementazione DAM non vengono propagate downstream.
* Le risorse locali sono copie in sola lettura. I componenti di Experience Manager apportano modifiche non distruttive alle risorse. Non sono consentite altre modifiche.
* Le risorse recuperate localmente sono disponibili solo a scopo di authoring. I flussi di lavoro di aggiornamento delle risorse non possono essere applicati e i metadati non possono essere modificati.
* Sono supportati solo le immagini e i formati di documento elencati. [!DNL Dynamic Media]Le risorse , i frammenti di contenuto e i frammenti di esperienza non sono supportati.
* Gli schemi di metadati non vengono recuperati.
* All [!DNL Sites] authors have read permissions on the fetched copies, even if they do not have access to the remote DAM deployment.
* Nessun supporto API per personalizzare l’integrazione.
* Questa funzionalità supporta la ricerca e l’utilizzo diretti delle risorse remote. Per rendere disponibili molte risorse remote nell’implementazione locale con un’unica operazione, è consigliabile eseguire la migrazione delle risorse. Consulta la [guida alla migrazione di Assets](assets-migration-guide.md).
* Non è possibile utilizzare una risorsa remota come miniatura di pagina nell’interfaccia utente Proprietà  pagina. Per impostare una miniatura di una pagina Web nell’interfaccia utente Proprietà  pagina dalla [!UICONTROL miniatura] , fare clic su [!UICONTROL Seleziona immagine].

**Configurazione e licenze**

* [!DNL Experience Manager Assets] la distribuzione su AMS è supportata.
* [!DNL Experience Manager Sites] può connettersi a un singolo [!DNL Experience Manager Assets] archivio alla volta.
* A license of [!DNL Experience Manager Assets] working as remote repository.
* One or more licenses of [!DNL Experience Manager Sites] working as local authoring deployment.

**Utilizzo**

* È supportata solo la ricerca di risorse remote e il trascinamento delle risorse remote sulla pagina locale per creare contenuti.
* L’operazione di recupero si interrompe per timeout dopo 5 secondi. Gli autori possono rilevare dei problemi durante il recupero delle risorse, ad esempio in caso di problemi di rete. Gli autori possono riprovare trascinando la risorsa remota da [!UICONTROL Content Finder] all’[!UICONTROL Editor pagina].
* Le risorse recuperate possono essere sottoposte a semplici modifiche non distruttive e alle modifiche supportate tramite il componente [!DNL Experience Manager] di `Image` Le risorse sono di sola lettura.

## Risoluzione dei problemi {#troubleshoot}

Per risolvere eventuali errori comuni, segui i passaggi indicati di seguito.

* Se non riesci a cercare le risorse remote tramite Content Finder, verifica di nuovo e assicurati che siano presenti i ruoli e le autorizzazioni richiesti.
* Una risorsa recuperata da DAM remoto potrebbe non essere pubblicata su una pagina web per i seguenti motivi: non esiste in remoto, l’utente non dispone delle autorizzazioni necessarie per recuperarla o per un errore di rete. Assicurati che la risorsa non venga rimossa da DAM remoto o che le autorizzazioni non vengano modificate; assicurati che siano soddisfatti i prerequisiti appropriati e prova di nuovo ad aggiungere la risorsa alla pagina e ripubblicarla. Controlla l’[elenco dei processi asincroni](/help/assets/asynchronous-jobs.md) per verificare la presenza di errori nel recupero delle risorse.
