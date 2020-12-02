---
title: Utilizzare la funzione Risorse collegate per condividere risorse DAM in [!DNL Sites]
description: 'Utilizzate le risorse disponibili in una distribuzione remota. [!DNL Adobe Experience Manager Assets] deployment when creating your web pages on another [!DNL Adobe Experience Manager Sites] '
contentOwner: AG
translation-type: tm+mt
source-git-commit: f0d91a32caa4d3b862d852028e3bc5547aeb8015
workflow-type: tm+mt
source-wordcount: '2263'
ht-degree: 41%

---


# Utilizzare la funzione Risorse collegate per condividere risorse DAM in [!DNL Experience Manager Sites] {#use-connected-assets-to-share-dam-assets-in-aem-sites}

Nelle grandi aziende l’infrastruttura necessaria per la creazione di siti web può essere dislocata in luoghi diversi. A volte, le funzionalità per la creazione di siti web e le risorse digitali utilizzate per creare i siti possono trovarsi in implementazioni diverse. Un motivo può essere rappresentato dalla distribuzione geografica delle implementazioni esistenti necessarie per lavorare in parallelo. Un altro motivo può essere costituito dalle acquisizioni che portano a un&#39;infrastruttura eterogenea che la società madre desidera utilizzare insieme.

Gli utenti possono creare pagine Web in [!DNL Experience Manager Sites]. [!DNL Experience Manager Assets] è il sistema Digital Asset Management (DAM) che fornisce le risorse necessarie per i siti Web. [!DNL Experience Manager] supporta ora il caso d&#39;uso di cui sopra integrando  [!DNL Sites] e  [!DNL Assets].

## Panoramica della funzione Risorse collegate {#overview-of-connected-assets}

Quando modificate le pagine in [!UICONTROL Editor pagina] come destinazione, gli autori possono cercare, sfogliare e incorporare facilmente le risorse da una diversa distribuzione [!DNL Assets] che funge da origine delle risorse. Gli amministratori creano un&#39;integrazione una tantum di una distribuzione di [!DNL Experience Manager] con funzionalità [!DNL Sites] con un&#39;altra implementazione di [!DNL Experience Manager] con funzionalità [!DNL Assets].

Per gli autori [!DNL Sites], le risorse remote sono disponibili come risorse locali di sola lettura. Questa funzionalità supporta la ricerca e l’utilizzo di un numero limitato di risorse remote alla volta. Per rendere disponibili molte risorse remote in una distribuzione [!DNL Sites] in una sola volta, è consigliabile migrare le risorse in massa. Vedere [ Guida alla migrazione delle risorse di Experience Manager](/help/assets/assets-migration-guide.md).

### Prerequisiti e implementazioni supportate {#prerequisites}

Prima di utilizzare o configurare questa funzionalità, verifica questi aspetti:

* Gli utenti fanno parte dei gruppi di utenti appropriati per ciascuna distribuzione.
* Per i tipi di distribuzione [!DNL Adobe Experience Manager], uno dei criteri supportati è soddisfatto. [!DNL Experience Manager] 6.5  [!DNL Assets] funziona  [!DNL Experience Manager] come Cloud Service. Per ulteriori informazioni sul funzionamento di questa funzionalità in [!DNL Experience Manager as a Cloud Service], vedi [Risorse collegate in  Experience Manager come Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/use-assets-across-connected-assets-instances.html).

   |  | [!DNL Sites] come Cloud Service | [!DNL Experience Manager] 6.5  [!DNL Sites] su AMS | [!DNL Experience Manager] 6.5  [!DNL Sites] in sede |
   |---|---|---|---|
   | **[!DNL Experience Manager Assets]come Cloud Service** | Supportato | Supportato | Supportato |
   | **[!DNL Experience Manager]6.5  [!DNL Assets] su AMS** | Supportato | Supportato | Supportato |
   | **[!DNL Experience Manager]6.5  [!DNL Assets] in sede** | Non supportato | Non supportato | Non supportato |

### Formati di file supportati {#mimetypes}

Gli autori ricercano le immagini e i seguenti tipi di documenti in Content Finder e utilizzano le risorse ricercate in Editor pagina. I documenti vengono aggiunti al componente `Download` e le immagini al componente `Image`. Gli autori possono inoltre aggiungere le risorse remote in qualsiasi componente [!DNL Experience Manager] personalizzato che estende i componenti predefiniti `Download` o `Image`. I formati supportati sono:

* **Formati** immagine: Formati supportati dal  [componente ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/image.html) Immagine. [!DNL Dynamic Media] le immagini non sono supportate.
* **Formati** del documento: Vedere i formati [ di documento ](assets-formats.md#supported-document-formats)supportati.

### Utenti e gruppi interessati {#users-and-groups-involved}

Di seguito sono descritti i diversi ruoli coinvolti nella configurazione e nell’utilizzo della funzionalità e i relativi gruppi di utenti. L&#39;ambito locale viene utilizzato per il caso di utilizzo in cui un autore crea una pagina Web. L’ambito remoto viene utilizzato per l’implementazione DAM in cui sono ospitate le risorse necessarie. Le risorse remote vengono recuperate dall&#39;autore [!DNL Sites].

| Ruolo | Ambito | Gruppo di utenti | Nome utente nella procedura dettagliata | Requisito |
|---|---|---|---|---|
| [!DNL Sites] administrator | Locale | [!DNL Experience Manager] `administrators` | `admin` | Configurare [!DNL Experience Manager] e configurare l&#39;integrazione con la distribuzione remota [!DNL Assets]. |
| Utente DAM | Locale | `Authors` | `ksaner` | Utilizzato per visualizzare e duplicare le risorse recuperate in `/content/DAM/connectedassets/`. |
| [!DNL Sites] author | Locale | `Authors` (con accesso in lettura sul DAM remoto e accesso dell&#39;autore sul locale  [!DNL Sites]) | `ksaner` | Gli utenti finali sono [!DNL Sites] autori che utilizzano questa integrazione per migliorare la velocità dei contenuti. Gli autori ricercano e sfogliano le risorse in DAM remoto utilizzando [!UICONTROL Content Finder] e utilizzando le immagini richieste nelle pagine Web locali. Vengono utilizzate le credenziali dell’utente `ksaner` di DAM. |
| [!DNL Assets] administrator | Remoto | [!DNL Experience Manager] `administrators` | `admin` su remoto  [!DNL Experience Manager] | Configurare la condivisione risorse tra le origini (CORS, Cross-Origin Resource Sharing). |
| Utente DAM | Remoto | `Authors` | `ksaner` su remoto  [!DNL Experience Manager] | Ruolo di authoring nella distribuzione remota [!DNL Experience Manager]. Cercate e sfogliate le risorse in Risorse collegate utilizzando il Content Finder][!UICONTROL  |
| Distributore DAM (utente tecnico) | Remoto | [!DNL Sites] `Authors` | `ksaner` su remoto  [!DNL Experience Manager] | Questo utente presente nella distribuzione remota viene utilizzato dal server locale [!DNL Experience Manager] (non dal ruolo di [!DNL Sites] autore) per recuperare le risorse remote, per conto dell&#39;autore [!DNL Sites]. Questo ruolo non è lo stesso dei due ruoli `ksaner` precedenti e appartiene a un gruppo di utenti diverso. |

## Configurare una connessione tra [!DNL Sites] e [!DNL Assets] distribuzioni {#configure-a-connection-between-sites-and-assets-deployments}

Un amministratore [!DNL Experience Manager] può creare questa integrazione. Una volta create, le autorizzazioni necessarie per utilizzarle vengono stabilite tramite i gruppi di utenti. I gruppi di utenti sono definiti nella distribuzione [!DNL Sites] e nella distribuzione DAM.

Per configurare le risorse connesse e la connettività [!DNL Sites] locale, effettua le seguenti operazioni:

1. Accedete a una distribuzione [!DNL Sites] esistente o create una distribuzione utilizzando il seguente comando:

   1. Nella cartella del file JAR, eseguire il comando seguente su un terminale per creare ogni [!DNL Experience Manager] server.
      `java -XX:MaxPermSize=768m -Xmx4096m -jar <quickstart jar filepath> -r samplecontent -p 4502 -nofork -gui -nointeractive &`

   1. Dopo alcuni minuti, il server [!DNL Experience Manager] viene avviato correttamente. Considerate questa distribuzione [!DNL Sites] come il computer locale per l&#39;authoring delle pagine Web, ad esempio in `https://[local_sites]:4502`.

1. Assicurarsi che gli utenti e i ruoli con ambito locale siano presenti nella distribuzione [!DNL Sites] e nella distribuzione [!DNL Assets] su AMS. Crea un utente tecnico nella [!DNL Assets] distribuzione e aggiungi al gruppo di utenti indicato in [utenti e gruppi coinvolti](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved).

1. Accedi alla distribuzione [!DNL Sites] locale in `https://[local_sites]:4502`. Fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Configurazione risorse collegate]** e fornisci i seguenti valori:

   1. [!DNL Assets] la posizione è  `https://[assets_servername_ams]:[port]`.
   1. Credenziali di un distributore DAM (utente tecnico).
   1. Nel campo **[!UICONTROL Punto di montaggio]**, immettete il percorso locale [!DNL Experience Manager] in cui [!DNL Experience Manager] recupera le risorse. Ad esempio, la cartella `remoteassets`.
   1. Regola i valori di **[!UICONTROL Soglia ottimizzazione trasferimento binario originale]** in base alla rete. Il rendering di una risorsa con dimensioni superiori alla soglia viene trasferito in modo asincrono.
   1. Seleziona **[!UICONTROL Archivio dati condiviso con risorse collegate]** se per memorizzare le risorse utilizzi un archivio dati in comune tra le due implementazioni di In questo caso, il limite di soglia non ha importanza in quanto i dati binari effettivi delle risorse risiedono nell’archivio dati e non vengono trasferiti.

   ![Configurazione tipica per Risorse collegate](assets/connected-assets-typical-config.png)

   *Figura: una configurazione tipica per Risorse collegate.*

1. Poiché le risorse sono già state elaborate e i rendering vengono recuperati, disattiva i moduli di avvio dei flussi di lavoro. Regolate le configurazioni del modulo di avvio nella distribuzione locale ([!DNL Sites]) per escludere la cartella `connectedassets`, in cui vengono recuperate le risorse remote.

   1. Durante la distribuzione di [!DNL Sites], fare clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Avviatori]**.

   1. Individua i moduli di avvio con flussi di lavoro come **[!UICONTROL Aggiorna risorsa DAM]** e **[!UICONTROL Writeback di metadati DAM]**.

   1. Seleziona il modulo di avvio del flusso di lavoro e fai clic su **[!UICONTROL Proprietà]** nella barra delle azioni.

   1. Nella procedura guidata [!UICONTROL Proprietà], modificare i campi **[!UICONTROL Path]** come le seguenti mappature per aggiornare le espressioni regolari per escludere il punto di montaggio **[!UICONTROL connection assets]**.

   | Prima | Dopo |
   |---|---|
   | `/content/dam(/((?!/subassets).)*/)renditions/original` | `/content/dam(/((?!/subassets)(?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*/)renditions/original` | `/content/dam(/((?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*)/jcr:content/metadata` | `/content/dam(/((?!connectedassets).)*/)jcr:content/metadata` |

   >[!NOTE]
   >
   >Quando gli autori recuperano una risorsa, vengono recuperati tutti i rendering disponibili nell’implementazione remota. Se desideri creare più rendering per una risorsa recuperata, ignora questo passaggio di configurazione. Il flusso di lavoro [!UICONTROL DAM Update Asset] viene attivato e crea più rappresentazioni. Queste rappresentazioni sono disponibili solo nella [!DNL Sites] distribuzione locale e non nella distribuzione DAM remota.

1. Aggiungere la [!DNL Sites] distribuzione come una delle **[!UICONTROL Origini consentite]** nella configurazione remota [!DNL Assets'] CORS.

   1. Effettuate l&#39;accesso utilizzando le credenziali dell&#39;amministratore. Cerca `Cross-Origin`. Accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > Console Web ****.

   1. Per creare una configurazione CORS per la distribuzione [!DNL Sites], fare clic su Aggiungi opzione ![Risorse aggiungere l&#39;icona](assets/do-not-localize/assets_add_icon.png) accanto a **[!UICONTROL Adobe Granite Cross-Origin Resource Sharing Policy]**.

   1. Nel campo **[!UICONTROL Origini consentite]**, inserire l&#39;URL del [!DNL Sites] locale, ovvero `https://[local_sites]:[port]`. Salva la configurazione.

## Utilizzare le risorse remote {#use-remote-assets}

Gli autori del sito Web utilizzano Content Finder per connettersi alla distribuzione DAM. Gli autori possono sfogliare, cercare e trascinare le risorse remote in un componente. Per eseguire l’autenticazione nel DAM remoto, tieni a portata di mano le credenziali dell’utente DAM fornite dal tuo amministratore.

Gli autori possono utilizzare le risorse disponibili nella DAM locale e nella distribuzione DAM remota, in una singola pagina Web. Utilizza Content Finder per passare dalla ricerca nel DAM locale alla ricerca nel DAM remoto.

Vengono recuperati solo i tag delle risorse remote con un tag corrispondente esatto insieme alla stessa gerarchia tassonomia, disponibile nella distribuzione locale [!DNL Sites]. Tutti gli altri tag vengono eliminati. Gli autori possono cercare risorse remote utilizzando tutti i tag presenti nella distribuzione remota [!DNL Experience Manager], in quanto offre una ricerca full-text.

### Procedura dettagliata per l’utilizzo {#walk-through-of-usage}

Utilizza la configurazione precedente per provare l’esperienza di authoring e comprendere il funzionamento di questa caratteristica. Utilizza documenti o immagini di tua scelta nell’implementazione remota di DAM.

1. Andate all&#39;interfaccia [!DNL Assets] nella distribuzione remota accedendo a **[!UICONTROL Risorse]** > **[!UICONTROL File]** dall&#39;area di lavoro [!DNL Experience Manager]. In alternativa, puoi accedere a `https://[assets_servername_ams]:[port]/assets.html/content/dam` in un browser. Carica le risorse che hai scelto.
1. Nella [!DNL Sites] distribuzione, nell&#39;attivatore del profilo in alto a destra, fare clic su **[!UICONTROL Impersona come]**. Specifica `ksaner` come nome utente, seleziona l’opzione fornita e fai clic su **[!UICONTROL OK]**.
1. Apri una pagina del sito web We.Retail in **[!UICONTROL Sites]** > **[!UICONTROL We.Retail]** > **[!UICONTROL us]** > **[!UICONTROL en]**. Modifica la pagina. In alternativa, accedi a `https://[aem_server]:[port]/editor.html/content/we-retail/us/en/men.html` tramite un browser per modificare una pagina.

   Fai clic su **[!UICONTROL Attiva/Disattiva pannello laterale]** nell’angolo in alto a sinistra della pagina.

1. Aprite la scheda [!UICONTROL Risorse] e fate clic su **[!UICONTROL Accedi a Risorse collegate]**.
1. Immetti le credenziali: `ksaner` come nome utente e `password` come password. Questo utente dispone di autorizzazioni di authoring sia per le [!DNL Experience Manager] distribuzioni.
1. Cerca la risorsa aggiunta a DAM. Le risorse remote vengono visualizzate nel pannello a sinistra. Filtra immagini o documenti e filtra ulteriormente i tipi di documenti supportati. Trascina le immagini su un componente `Image`, e i documenti su un componente `Download`.

   Le risorse recuperate sono di sola lettura nella distribuzione locale [!DNL Sites]. Potete comunque utilizzare le opzioni fornite dai componenti [!DNL Sites] per modificare la risorsa recuperata. La modifica per componenti non è distruttiva.

   ![Opzioni di filtro per tipi di documenti e immagini nella ricerca di risorse in DAM remoto](assets/filetypes_filter_connected_assets.png)

   *Figura: opzioni di filtro per tipi di documenti e immagini nella ricerca di risorse in DAM remoto.*

1. Un autore del sito riceve una notifica se una risorsa viene recuperata in modo asincrono e se un’attività di recupero ha esito negativo. Durante l’authoring, o anche successivamente, gli autori possono visualizzare informazioni dettagliate sulle attività di recupero e sugli errori nell’interfaccia utente [Processi asincroni](/help/sites-administering/asynchronous-jobs.md).

   ![Notifica relativa al recupero asincrono delle risorse in background.](assets/assets_async_transfer_fails.png)

   *Figura: notifica relativa al recupero asincrono delle risorse in background.*

1. Quando si pubblica una pagina, [!DNL Experience Manager] visualizza un elenco completo delle risorse utilizzate nella pagina. Assicurati che le risorse remote vengano recuperate correttamente al momento della pubblicazione. Per verificare lo stato di ciascuna risorsa recuperata, consulta l’interfaccia utente dei [processi asincroni](/help/sites-administering/asynchronous-jobs.md).

   >[!NOTE]
   >
   >La pagina viene pubblicata anche se una o più risorse remote non vengono recuperate. Il componente che utilizza la risorsa remota viene pubblicato come vuoto. L&#39;area di notifica [!DNL Experience Manager] visualizza una notifica per gli errori che vengono visualizzati nella pagina dei processi asincroni.

>[!CAUTION]
>
>Una volta utilizzate in una pagina Web, le risorse remote recuperate sono ricercabili e utilizzabili da chiunque disponga delle autorizzazioni per accedere alla cartella locale. Le risorse recuperate vengono memorizzate nella cartella locale (`connectedassets` nel passaggio precedente). Le risorse possono inoltre essere cercate e visualizzate nell’archivio locale tramite [!UICONTROL Content Finder].

Le risorse recuperate possono essere utilizzate come qualsiasi altra risorsa locale, ad eccezione del fatto che i metadati associati non possono essere modificati.

## Limitazioni  e best practice {#tips-and-limitations}

* Per informazioni dettagliate sull&#39;utilizzo delle risorse, configurate la funzionalità [Asset Insight](/help/assets/asset-insights.md) sull&#39;istanza [!DNL Sites].

### Gestione delle autorizzazioni e delle risorse {#permissions-and-managing-assets}

* Le risorse locali non vengono sincronizzate con le risorse originali nell’implementazione remota. Eventuali modifiche, eliminazioni o revoche delle autorizzazioni nell’implementazione DAM non vengono propagate downstream.
* Le risorse locali sono copie in sola lettura. [!DNL Experience Manager]I componenti apportano modifiche non distruttive alle risorse. Non sono consentite altre modifiche.
* Le risorse recuperate localmente sono disponibili solo a scopo di authoring. I flussi di lavoro di aggiornamento delle risorse non possono essere applicati e i metadati non possono essere modificati.
* Sono supportati solo le immagini e i formati di documento elencati. [!DNL Dynamic Media]Le risorse , i frammenti di contenuto e i frammenti di esperienza non sono supportati.
* [!DNL Experience Manager] non recupera gli schemi di metadati. Ciò significa che tutti i metadati recuperati potrebbero non essere visualizzati. Se lo schema viene aggiornato separatamente, vengono visualizzate tutte le proprietà.
* Tutti gli autori [!DNL Sites] dispongono di autorizzazioni di lettura sulle copie recuperate, anche se gli autori non possono accedere alla distribuzione DAM remota.
* Nessun supporto API per personalizzare l’integrazione.
* Questa funzionalità supporta la ricerca e l’utilizzo diretti delle risorse remote. Per rendere disponibili molte risorse remote nell’implementazione locale con un’unica operazione, è consigliabile eseguire la migrazione delle risorse. Consulta la [guida alla migrazione di Assets](assets-migration-guide.md).
* Non è possibile utilizzare una risorsa remota come miniatura di pagina nell&#39;interfaccia utente [!UICONTROL Proprietà pagina]. È possibile impostare una miniatura di una pagina Web nell&#39;interfaccia utente [!UICONTROL Proprietà pagina] dalla [!UICONTROL Miniatura] facendo clic su [!UICONTROL Seleziona immagine].

### Configurazione e licenze {#setup-licensing}

* [!DNL Assets] la distribuzione  [!DNL Adobe Managed Services] è supportata.
* [!DNL Sites] può connettersi a un singolo  [!DNL Assets] archivio alla volta.
* Una licenza di [!DNL Assets] funzionamento come repository remoto.
* Una o più licenze di [!DNL Sites] funzionamento come distribuzione di authoring locale.

### Utilizzo {#usage}

* Gli utenti possono cercare risorse remote e trascinarle sulla pagina locale durante l’authoring. Non sono supportate altre funzionalità.
* L’operazione di recupero si interrompe per timeout dopo 5 secondi. Gli autori possono rilevare dei problemi durante il recupero delle risorse, ad esempio in caso di problemi di rete. Gli autori possono riprovare trascinando la risorsa remota da [!UICONTROL Content Finder] a [!UICONTROL Editor pagina].
* Le risorse recuperate possono essere sottoposte a semplici modifiche non distruttive e alle modifiche supportate tramite il componente `Image` di Le risorse sono di sola lettura.
* L’unico metodo per recuperare nuovamente la risorsa consiste nel trascinarla su una pagina. Non esiste un supporto API o altri metodi per recuperare nuovamente una risorsa e aggiornarla.
* Se le risorse vengono disattivate da DAM, continueranno a essere utilizzate su [!DNL Sites] pagine.

## Risoluzione dei problemi {#troubleshoot}

Per risolvere eventuali problemi relativi allo scenario di errore comune, procedere come segue:

* Se non riuscite a cercare risorse remote da [!UICONTROL Content Finder], accertatevi che i ruoli e le autorizzazioni richiesti siano già presenti.
* Una risorsa recuperata dalla diga remota potrebbe non essere pubblicata su una pagina Web per uno o più motivi. Non esiste sul server remoto, mancano le autorizzazioni necessarie per recuperarlo o l&#39;errore di rete può essere dovuto a cause. Assicurarsi che la risorsa non venga rimossa dal DAM remoto. Verificate che siano disponibili le autorizzazioni appropriate e che i prerequisiti siano soddisfatti. Provate ad aggiungere la risorsa alla pagina e ripubblicatela. Controlla l’[elenco dei processi asincroni](/help/sites-administering/asynchronous-jobs.md) per verificare la presenza di errori nel recupero delle risorse.
* Se non riuscite ad accedere alla distribuzione DAM remota dalla distribuzione locale [!DNL Sites], accertatevi che i cookie intersito siano consentiti. Se i cookie cross-site sono bloccati, le due distribuzioni di [!DNL Experience Manager] potrebbero non essere autenticate. Ad esempio, [!DNL Google Chrome] in modalità Incognito può bloccare i cookie di terze parti. Per consentire i cookie nel browser [!DNL Chrome], fai clic sull&#39;icona a forma di occhio nella barra degli indirizzi, vai a Sito che non funziona > Bloccato, seleziona l&#39;URL DAM remoto e consenti il cookie del token di login. In alternativa, consultare la Guida relativa all&#39;attivazione dei cookie di terze parti [e](https://support.google.com/chrome/answer/95647).

   ![Errore del cookie in Chrome in modalità incognito](assets/chrome-cookies-incognito-dialog.png)
