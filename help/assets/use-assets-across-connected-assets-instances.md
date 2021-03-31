---
title: Utilizzare la funzione Risorse collegate per condividere risorse DAM in [!DNL Sites]
description: Utilizzare le risorse disponibili in una distribuzione remota [!DNL Adobe Experience Manager Assets] deployment when creating your web pages on another [!DNL Adobe Experience Manager Sites] remota.
contentOwner: AG
role: Professionista, Amministratore, Leader
feature: Risorse, utenti e gruppi collegati
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '2726'
ht-degree: 29%

---


# Utilizzare la funzione Risorse collegate per condividere risorse DAM in [!DNL Experience Manager Sites] {#use-connected-assets-to-share-dam-assets-in-aem-sites}

Nelle grandi aziende l’infrastruttura necessaria per la creazione di siti web può essere dislocata in luoghi diversi. A volte, le funzionalità per la creazione di siti web e le risorse digitali utilizzate per creare i siti possono trovarsi in implementazioni diverse. Un motivo può essere rappresentato dalla distribuzione geografica delle implementazioni esistenti necessarie per lavorare in parallelo. Un altro motivo può essere rappresentato dalle acquisizioni che portano a un&#39;infrastruttura eterogenea che la società madre desidera utilizzare insieme.

Gli utenti possono creare pagine web in [!DNL Experience Manager Sites]. [!DNL Experience Manager Assets] è il sistema Digital Asset Management (DAM) che fornisce le risorse necessarie per i siti web. [!DNL Experience Manager] ora supporta il caso d’uso precedente integrando  [!DNL Sites] e  [!DNL Assets].

## Panoramica della funzione Risorse collegate {#overview-of-connected-assets}

Durante la modifica delle pagine in [!UICONTROL Editor pagina] come destinazione di destinazione, gli autori possono cercare, sfogliare e incorporare facilmente le risorse di una diversa distribuzione [!DNL Assets] che funge da origine delle risorse. Gli amministratori creano un’integrazione una tantum di una distribuzione di [!DNL Experience Manager] con funzionalità [!DNL Sites] con un’altra distribuzione di [!DNL Experience Manager] con funzionalità [!DNL Assets].

Per gli autori [!DNL Sites] , le risorse remote sono disponibili come risorse locali di sola lettura. Questa funzionalità supporta la ricerca e l’utilizzo di un numero limitato di risorse remote alla volta. Per rendere disponibili molte risorse remote in una distribuzione [!DNL Sites] con una sola operazione, è consigliabile eseguire la migrazione delle risorse in massa. Consulta [Guida alla migrazione di Experience Manager Assets](/help/assets/assets-migration-guide.md).

### Prerequisiti e implementazioni supportate {#prerequisites}

Prima di utilizzare o configurare questa funzionalità, verifica questi aspetti:

* Gli utenti fanno parte dei gruppi di utenti appropriati per ciascuna distribuzione.
* Per i tipi di distribuzione [!DNL Adobe Experience Manager], viene soddisfatto uno dei criteri supportati. [!DNL Experience Manager] 6.5  [!DNL Assets] funziona con  [!DNL Experience Manager] come Cloud Service. Per ulteriori informazioni su come funziona questa funzionalità in [!DNL Experience Manager] come [!DNL Cloud Service], consulta [Risorse collegate in [!DNL Experience Manager] come a [!DNL Cloud Service]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/use-assets-across-connected-assets-instances.html).

   |  | [!DNL Sites] as a [!DNL Cloud Service] | [!DNL Experience Manager] 6.5  [!DNL Sites] in AMS | [!DNL Experience Manager] 6.5  [!DNL Sites] on-premise |
   |---|---|---|---|
   | **[!DNL Experience Manager Assets]come[!DNL Cloud Service]** | Supportato | Supportato | Supportato |
   | **[!DNL Experience Manager]6.5  [!DNL Assets] in AMS** | Supportato | Supportato | Supportato |
   | **[!DNL Experience Manager]6.5  [!DNL Assets] on-premise** | Non supportato | Non supportato | Non supportato |

### Formati di file supportati {#mimetypes}

Gli autori ricercano le immagini e i seguenti tipi di documenti in Content Finder e utilizzano le risorse cercate nell’Editor pagina. I documenti vengono aggiunti al componente `Download` e le immagini al componente `Image` . Gli autori possono inoltre aggiungere le risorse remote a qualsiasi componente [!DNL Experience Manager] personalizzato che estenda i componenti predefiniti `Download` o `Image` . I formati supportati sono:

* **Formati** immagine: Formati supportati dal componente  [Immagine ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/image.html) . [!DNL Dynamic Media] le immagini non sono supportate.
* **Formati** documento: Vedere i formati di documento  [supportati](assets-formats.md#supported-document-formats).

### Utenti e gruppi interessati {#users-and-groups-involved}

Di seguito sono descritti i diversi ruoli coinvolti nella configurazione e nell’utilizzo della funzionalità e i relativi gruppi di utenti. L’ambito locale viene utilizzato per il caso d’uso in cui un autore crea una pagina web. L’ambito remoto viene utilizzato per l’implementazione DAM in cui sono ospitate le risorse necessarie. Le risorse remote vengono recuperate dall’autore [!DNL Sites].

| Ruolo | Ambito | Gruppo di utenti | Nome utente nella procedura dettagliata | Requisito |
|---|---|---|---|---|
| [!DNL Sites] administrator | Locale | [!DNL Experience Manager] `administrators` | `admin` | Imposta [!DNL Experience Manager] e configura l&#39;integrazione con la distribuzione remota [!DNL Assets]. |
| Utente DAM | Locale | `Authors` | `ksaner` | Utilizzato per visualizzare e duplicare le risorse recuperate in `/content/DAM/connectedassets/`. |
| [!DNL Sites] author | Locale | <ul><li>`Authors` (con accesso in lettura sul DAM remoto e accesso dell’autore sul locale  [!DNL Sites]) </li> <li>`dam-users` locale  [!DNL Sites]</li></ul> | `ksaner` | Gli utenti finali sono [!DNL Sites] autori che utilizzano questa integrazione per velocizzare i contenuti. Gli autori ricercano e sfogliano le risorse in DAM remoto utilizzando [!UICONTROL Content Finder] e utilizzando le immagini richieste nelle pagine web locali. Vengono utilizzate le credenziali dell’utente `ksaner` di DAM. |
| [!DNL Assets] amministratore | Remoto | [!DNL Experience Manager] `administrators` | `admin` in remoto  [!DNL Experience Manager] | Configurare la condivisione risorse tra le origini (CORS, Cross-Origin Resource Sharing). |
| Utente DAM | Remoto | `Authors` | `ksaner` in remoto  [!DNL Experience Manager] | Ruolo di authoring nella distribuzione [!DNL Experience Manager] remota. Cerca e sfoglia le risorse in Risorse collegate utilizzando il [!UICONTROL Content Finder]. |
| Distributore DAM (utente tecnico) | Remoto | [!DNL Sites] `Authors` | `ksaner` in remoto  [!DNL Experience Manager] | Questo utente presente nell’implementazione remota viene utilizzato dal server locale [!DNL Experience Manager] (non il ruolo di autore [!DNL Sites]) per recuperare le risorse remote, per conto dell’ [!DNL Sites] autore. Questo ruolo non è lo stesso dei due ruoli `ksaner` precedenti e appartiene a un gruppo di utenti diverso. |

## Configura una connessione tra le distribuzioni [!DNL Sites] e [!DNL Assets] {#configure-a-connection-between-sites-and-assets-deployments}

Un amministratore [!DNL Experience Manager] può creare questa integrazione. Una volta create, le autorizzazioni necessarie per utilizzarle vengono stabilite tramite gruppi di utenti. I gruppi di utenti sono definiti nella distribuzione [!DNL Sites] e nella distribuzione DAM.

Per configurare le risorse collegate e la connettività locale [!DNL Sites], effettua le seguenti operazioni:

1. Accedi a una distribuzione [!DNL Sites] esistente o creane una utilizzando il seguente comando:

   1. Nella cartella del file JAR, esegui il seguente comando su un terminale per creare ogni [!DNL Experience Manager] server.
      `java -XX:MaxPermSize=768m -Xmx4096m -jar <quickstart jar filepath> -r samplecontent -p 4502 -nofork -gui -nointeractive &`

   1. Dopo alcuni minuti, il server [!DNL Experience Manager] viene avviato correttamente. Considera questa distribuzione [!DNL Sites] come computer locale per l’authoring delle pagine web, ad esempio all’indirizzo `https://[local_sites]:4502`.

1. Assicurati che gli utenti e i ruoli con l’ambito appropriato esistano nella distribuzione [!DNL Sites] e nella distribuzione [!DNL Assets] in AMS. Crea un utente tecnico per la distribuzione [!DNL Assets] e aggiungi al gruppo di utenti menzionato in [utenti e gruppi interessati](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved).

1. Accedi alla distribuzione [!DNL Sites] locale in `https://[local_sites]:4502`. Fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Configurazione risorse collegate]** e fornisci i seguenti valori:

   1. A **[!UICONTROL Titolo]** della configurazione.
   1. **[!UICONTROL L’]** URL DAM remoto è l’URL della  [!DNL Assets] posizione nel formato  `https://[assets_servername]:[port]`.
   1. Credenziali di un distributore DAM (utente tecnico).
   1. Nel campo **[!UICONTROL Punto di montaggio]** , immetti il percorso locale [!DNL Experience Manager] in cui [!DNL Experience Manager] recupera le risorse. Ad esempio, la cartella `remoteassets`. Le risorse recuperate da DAM sono memorizzate in questa cartella nella distribuzione [!DNL Sites] .
   1. **[!UICONTROL L’]** URL di Sites locale è il percorso della  [!DNL Sites] distribuzione. [!DNL Assets] Questo valore viene utilizzato per mantenere i riferimenti alle risorse digitali recuperate da questa  [!DNL Sites] distribuzione.
   1. Credenziali dell&#39;utente tecnico [!DNL Sites].
   1. Il valore del campo **[!UICONTROL Soglia ottimizzazione trasferimento binario originale]** specifica se le risorse originali (incluse le rappresentazioni) vengono trasferite in modo sincrono o meno. Le risorse con file di dimensioni minori possono essere recuperate rapidamente, mentre le risorse con file di dimensioni relativamente maggiori sono sincronizzate in modo asincrono. Il valore dipende dalle funzionalità di rete.
   1. Seleziona **[!UICONTROL Archivio dati condiviso con risorse collegate]** se per memorizzare le risorse utilizzi un archivio dati in comune tra le due implementazioni di In questo caso, il limite di soglia non ha importanza in quanto i binari effettivi delle attività sono disponibili nell’archivio dati e non vengono trasferiti.

   ![Configurazione tipica per la funzionalità Risorse collegate](assets/connected-assets-typical-config.png)

   *Figura: Configurazione tipica per la funzionalità Risorse collegate.*

1. Le risorse digitali esistenti nella distribuzione [!DNL Assets] sono già elaborate e le rappresentazioni vengono generate. Queste rappresentazioni vengono recuperate utilizzando questa funzionalità per cui non è necessario rigenerare le rappresentazioni. Disattiva i moduli di avvio del flusso di lavoro per impedire la rigenerazione dei rendering. Regola le configurazioni del modulo di avvio nella distribuzione ([!DNL Sites]) per escludere la cartella `connectedassets` (le risorse vengono recuperate in questa cartella).

   1. Nella distribuzione [!DNL Sites], fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Moduli di avvio]**.

   1. Individua i moduli di avvio con flussi di lavoro come **[!UICONTROL Aggiorna risorsa DAM]** e **[!UICONTROL Writeback di metadati DAM]**.

   1. Seleziona il modulo di avvio del flusso di lavoro e fai clic su **[!UICONTROL Proprietà]** nella barra delle azioni.

   1. Nella procedura guidata [!UICONTROL Proprietà], modifica i campi **[!UICONTROL Percorso]** come le mappature seguenti per aggiornare le espressioni regolari al fine di escludere il punto di montaggio **[!UICONTROL connectedassets]**.

   | Prima | Dopo |
   |---|---|
   | `/content/dam(/((?!/subassets).)*/)renditions/original` | `/content/dam(/((?!/subassets)(?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*/)renditions/original` | `/content/dam(/((?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*)/jcr:content/metadata` | `/content/dam(/((?!connectedassets).)*/)jcr:content/metadata` |

   >[!NOTE]
   >
   >Quando gli autori recuperano una risorsa, vengono recuperati tutti i rendering disponibili nell’implementazione remota. Se desideri creare più rendering per una risorsa recuperata, ignora questo passaggio di configurazione. Viene attivato il flusso di lavoro [!UICONTROL Aggiorna risorsa DAM] e vengono creati ulteriori rendering. Queste rappresentazioni sono disponibili solo nella distribuzione locale [!DNL Sites] e non nella distribuzione remota di DAM.

1. Aggiungi la distribuzione [!DNL Sites] come origine consentita nella configurazione CORS nella distribuzione [!DNL Assets] . Per ulteriori informazioni, consulta [comprendere CORS](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html).

<!-- TBD: See if these steps are not required.
    1. Log in using the administrator credentials. Search for `Cross-Origin`. Access **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.

    1. To create a CORS configuration for [!DNL Sites] deployment, click add option ![Assets add icon](assets/do-not-localize/assets_add_icon.png) next to **[!UICONTROL Adobe Granite Cross-Origin Resource Sharing Policy]**.

    1. In the field **[!UICONTROL Allowed Origins]**, input the URL of the local [!DNL Sites], that is, `https://[local_sites]:[port]`. Save the configuration.
-->

Puoi controllare la connettività tra le distribuzioni [!DNL Sites] configurate e la distribuzione [!DNL Assets].

![Test di connessione delle risorse collegate configurate  [!DNL Sites]](assets/connected-assets-multiple-config.png)

## Utilizzare le risorse remote {#use-remote-assets}

Gli autori del sito web utilizzano Content Finder per connettersi alla distribuzione DAM. Gli autori possono sfogliare, cercare e trascinare le risorse remote in un componente. Per eseguire l’autenticazione nel DAM remoto, tieni a portata di mano le credenziali dell’utente DAM fornite dal tuo amministratore.

Gli autori possono utilizzare le risorse disponibili nell’implementazione DAM locale e DAM remota, in un’unica pagina web. Utilizza Content Finder per passare dalla ricerca nel DAM locale alla ricerca nel DAM remoto.

Solo i tag delle risorse remote vengono recuperati con un tag corrispondente esatto insieme alla stessa gerarchia di tassonomia, disponibile nella distribuzione locale [!DNL Sites]. Tutti gli altri tag vengono eliminati. Gli autori possono cercare risorse remote utilizzando tutti i tag presenti nella distribuzione remota [!DNL Experience Manager], in quanto offre una ricerca full-text.

### Procedura dettagliata per l’utilizzo {#walk-through-of-usage}

Utilizza la configurazione precedente per provare l’esperienza di authoring e comprendere il funzionamento di questa caratteristica. Utilizza documenti o immagini di tua scelta nell’implementazione remota di DAM.

1. Passa all&#39;interfaccia [!DNL Assets] nell&#39;implementazione remota accedendo a **[!UICONTROL Risorse]** > **[!UICONTROL File]** dall&#39;area di lavoro [!DNL Experience Manager]. In alternativa, puoi accedere a `https://[assets_servername_ams]:[port]/assets.html/content/dam` in un browser. Carica le risorse che hai scelto.
1. Nella distribuzione [!DNL Sites], nell&#39;attivatore del profilo in alto a destra, fai clic su **[!UICONTROL Impersona come]**. Specifica `ksaner` come nome utente, seleziona l’opzione fornita e fai clic su **[!UICONTROL OK]**.
1. Apri una pagina del sito web We.Retail in **[!UICONTROL Sites]** > **[!UICONTROL We.Retail]** > **[!UICONTROL us]** > **[!UICONTROL en]**. Modifica la pagina. In alternativa, accedi a `https://[aem_server]:[port]/editor.html/content/we-retail/us/en/men.html` tramite un browser per modificare una pagina.

   Fai clic su **[!UICONTROL Attiva/Disattiva pannello laterale]** nell’angolo in alto a sinistra della pagina.

1. Apri la scheda [!UICONTROL Risorse] e fai clic su **[!UICONTROL Accedi a Risorse collegate]**.
1. Immetti le credenziali: `ksaner` come nome utente e `password` come password. Questo utente dispone delle autorizzazioni di authoring per entrambe le distribuzioni [!DNL Experience Manager].
1. Cerca la risorsa aggiunta a DAM. Le risorse remote vengono visualizzate nel pannello a sinistra. Filtra immagini o documenti e filtra ulteriormente i tipi di documenti supportati. Trascina le immagini su un componente `Image`, e i documenti su un componente `Download`.

   Le risorse recuperate sono di sola lettura nella distribuzione locale [!DNL Sites]. Puoi comunque utilizzare le opzioni fornite dai componenti [!DNL Sites] per modificare la risorsa recuperata. La modifica per componenti non è distruttiva.

   ![Opzioni di filtro per tipi di documenti e immagini nella ricerca di risorse in DAM remoto](assets/filetypes_filter_connected_assets.png)

   *Figura: opzioni di filtro per tipi di documenti e immagini nella ricerca di risorse in DAM remoto.*

1. Un autore del sito riceve una notifica se una risorsa viene recuperata in modo asincrono e se un’attività di recupero ha esito negativo. Durante l’authoring o anche dopo l’authoring, gli autori possono visualizzare informazioni dettagliate sulle attività di recupero e sugli errori nell’ interfaccia utente [processi asincroni](/help/sites-administering/asynchronous-jobs.md) .

   ![Notifica relativa al recupero asincrono delle risorse in background.](assets/assets_async_transfer_fails.png)

   *Figura: notifica relativa al recupero asincrono delle risorse in background.*

1. Quando pubblichi una pagina, [!DNL Experience Manager] visualizza un elenco completo delle risorse utilizzate nella pagina. Assicurati che le risorse remote vengano recuperate correttamente al momento della pubblicazione. Per controllare lo stato di ciascuna risorsa recuperata, consulta l’interfaccia utente [processi asincroni](/help/sites-administering/asynchronous-jobs.md) .

   >[!NOTE]
   >
   >La pagina viene pubblicata anche se una o più risorse remote non vengono recuperate. Il componente che utilizza la risorsa remota viene pubblicato come vuoto. L&#39;area di notifica [!DNL Experience Manager] visualizza una notifica per gli errori visualizzati nella pagina dei processi asincroni.

>[!CAUTION]
>
>Una volta utilizzate in una pagina web, le risorse remote recuperate possono essere cercate e utilizzate da chiunque disponga delle autorizzazioni per accedere alla cartella locale. Le risorse recuperate vengono memorizzate nella cartella locale (`connectedassets` nel passaggio precedente). Le risorse possono inoltre essere cercate e visualizzate nell’archivio locale tramite [!UICONTROL Content Finder].

Le risorse recuperate possono essere utilizzate come qualsiasi altra risorsa locale, ad eccezione del fatto che i metadati associati non possono essere modificati.

### Controlla l&#39;utilizzo di una risorsa tra le pagine web {#asset-usage-references}

[!DNL Experience Manager] consente agli utenti DAM di controllare tutti i riferimenti a una risorsa. Consente di comprendere e gestire l’utilizzo di una risorsa in risorse remote [!DNL Sites] e in risorse composte. Molti autori di pagine web nella distribuzione [!DNL Experience Manager Sites] possono utilizzare una risorsa in un [!DNL Assets] remoto in pagine web diverse. Per semplificare la gestione delle risorse e non portare a riferimenti interrotti, è importante che gli utenti DAM verifichino l’utilizzo di una risorsa nelle pagine web locali e remote. La scheda [!UICONTROL Riferimenti] nella pagina [!UICONTROL Proprietà] di una risorsa elenca i riferimenti locali e remoti della risorsa.

Per visualizzare e gestire i riferimenti nella distribuzione [!DNL Assets], effettua le seguenti operazioni:

1. Seleziona una risorsa nella console [!DNL Assets] e fai clic su **[!UICONTROL Proprietà]** nella barra degli strumenti.
1. Fare clic sulla scheda **[!UICONTROL Riferimenti]**. Consulta **[!UICONTROL Riferimenti locali]** per l’utilizzo della risorsa nella distribuzione [!DNL Assets] . Consulta **[!UICONTROL Riferimenti remoti] per l’utilizzo della risorsa nella distribuzione [!DNL Sites] in cui la risorsa è stata recuperata utilizzando la funzionalità Risorse collegate.

   ![riferimenti remoti nella pagina Proprietà risorsa](assets/connected-assets-remote-reference.png)

1. I riferimenti per le pagine [!DNL Sites] visualizzano il conteggio totale dei riferimenti per ciascun [!DNL Sites] locale. Potrebbe essere necessario un po&#39; di tempo per trovare tutti i riferimenti e visualizzare il numero totale di riferimenti.
1. L’elenco dei riferimenti è interattivo e gli utenti DAM possono fare clic su un riferimento per aprire la pagina di riferimento. Se non è possibile recuperare i riferimenti remoti per qualche motivo, viene visualizzata una notifica che informa l’utente dell’errore.
1. Gli utenti possono spostare o eliminare la risorsa. Quando si sposta o si elimina una risorsa, il numero totale di riferimenti a tutte le risorse o cartelle selezionate viene visualizzato in una finestra di avviso. Quando si elimina una risorsa per la quale i riferimenti non sono ancora stati visualizzati, viene visualizzata una finestra di dialogo di avviso.

   ![avviso di eliminazione forzata](assets/delete-referenced-asset.png)

## Limitazioni e best practice {#tip-and-limitations}

* Per ottenere informazioni sull’utilizzo delle risorse, configura la funzionalità [Asset Insight](/help/assets/asset-insights.md) sull’istanza [!DNL Sites] .

### Gestione di autorizzazioni e risorse {#permissions-and-managing-assets}

* Le risorse locali non vengono sincronizzate con le risorse originali nell’implementazione remota. Eventuali modifiche, eliminazioni o revoche delle autorizzazioni nell’implementazione DAM non vengono propagate downstream.
* Le risorse locali sono copie in sola lettura. [!DNL Experience Manager]I componenti apportano modifiche non distruttive alle risorse. Non sono consentite altre modifiche.
* Le risorse recuperate localmente sono disponibili solo a scopo di authoring. I flussi di lavoro di aggiornamento delle risorse non possono essere applicati e i metadati non possono essere modificati.
* Sono supportati solo le immagini e i formati di documento elencati. [!DNL Dynamic Media]Le risorse , i frammenti di contenuto e i frammenti di esperienza non sono supportati.
* [!DNL Experience Manager] non recupera gli schemi di metadati. Ciò significa che potrebbero non essere visualizzati tutti i metadati recuperati. Se lo schema viene aggiornato separatamente, vengono visualizzate tutte le proprietà.
* Tutti gli autori [!DNL Sites] dispongono delle autorizzazioni di lettura sulle copie recuperate, anche se gli autori non possono accedere alla distribuzione remota di DAM.
* Nessun supporto API per personalizzare l’integrazione.
* Questa funzionalità supporta la ricerca e l’utilizzo diretti delle risorse remote. Per rendere disponibili molte risorse remote nell’implementazione locale con un’unica operazione, è consigliabile eseguire la migrazione delle risorse. Consulta la [guida alla migrazione di Assets](assets-migration-guide.md).
* Non è possibile utilizzare una risorsa remota come miniatura di pagina nell’ interfaccia utente [!UICONTROL Proprietà pagina]. Puoi impostare una miniatura di una pagina web nell’ interfaccia utente [!UICONTROL Proprietà pagina] dalla [!UICONTROL Miniatura] facendo clic su [!UICONTROL Seleziona immagine].

### Configurazione e licenze {#setup-licensing}

* [!DNL Assets] la distribuzione su  [!DNL Adobe Managed Services] è supportata.
* [!DNL Sites] può connettersi a un singolo  [!DNL Assets] archivio alla volta.
* Una licenza di [!DNL Assets] che funziona come archivio remoto.
* Una o più licenze di [!DNL Sites] che funzionano come distribuzione di authoring locale.

### Utilizzo {#usage}

* Gli utenti possono cercare le risorse remote e trascinarle sulla pagina locale durante l’authoring. Non sono supportate altre funzionalità.
* L’operazione di recupero si interrompe per timeout dopo 5 secondi. Gli autori possono rilevare dei problemi durante il recupero delle risorse, ad esempio in caso di problemi di rete. Gli autori possono riprovare trascinando la risorsa remota da [!UICONTROL Content Finder] a [!UICONTROL Editor pagina].
* Le risorse recuperate possono essere sottoposte a semplici modifiche non distruttive e alle modifiche supportate tramite il componente `Image` di Le risorse sono di sola lettura.
* L’unico metodo per recuperare nuovamente la risorsa è trascinarla su una pagina. Non esiste alcun supporto API o altri metodi per recuperare nuovamente una risorsa per aggiornarla.
* Se le risorse vengono disattivate dal DAM, continuano a essere utilizzate nelle pagine [!DNL Sites] .
* Le voci di riferimento remote di una risorsa vengono recuperate in modo asincrono. I riferimenti e il conteggio totale non sono in tempo reale e potrebbe esserci qualche differenza se un autore di Sites utilizza la risorsa mentre un utente DAM visualizza il riferimento. Gli utenti DAM possono aggiornare la pagina e riprovare tra qualche minuto per ottenere il conteggio totale.

## Risoluzione dei problemi {#troubleshoot}

Per risolvere eventuali errori comuni, procedi come segue:

* Se non riesci a cercare risorse remote da [!UICONTROL Content Finder], assicurati che siano presenti i ruoli e le autorizzazioni richiesti.
* Una risorsa recuperata dalla dam remota potrebbe non essere pubblicata su una pagina web per uno o più motivi. Non esiste sul server remoto, mancano le autorizzazioni appropriate per recuperarlo o può essere causata da un errore di rete. Assicurati che la risorsa non venga rimossa dal DAM remoto. Assicurati che siano presenti le autorizzazioni appropriate e che siano soddisfatti i prerequisiti. Riprova ad aggiungere la risorsa alla pagina e ripubblica. Controlla l’[elenco dei processi asincroni](/help/sites-administering/asynchronous-jobs.md) per verificare la presenza di errori nel recupero delle risorse.
* Se non riesci ad accedere alla distribuzione DAM remota dalla distribuzione locale [!DNL Sites], assicurati che siano consentiti i cookie intersito. Se i cookie intersito sono bloccati, le due distribuzioni di [!DNL Experience Manager] potrebbero non essere autenticate. Ad esempio, [!DNL Google Chrome] in modalità in incognito può bloccare i cookie di terze parti. Per consentire i cookie nel browser [!DNL Chrome], fai clic sull’icona &quot;occhio&quot; nella barra degli indirizzi, vai a Sito non funzionante > Bloccato, seleziona l’URL DAM remoto e consenti il cookie login-token. In alternativa, consulta la guida su [come abilitare i cookie di terze parti](https://support.google.com/chrome/answer/95647).

   ![Errore cookie in Chrome in modalità in incognito](assets/chrome-cookies-incognito-dialog.png)

* Se i riferimenti remoti non vengono recuperati e si verifica un messaggio di errore, verifica se la distribuzione [!DNL Sites] è disponibile e verifica la presenza di problemi di connettività di rete. Riprova più tardi per controllare. [!DNL Assets] l&#39;implementazione tenta due volte di stabilire la connessione con  [!DNL Sites] l&#39;implementazione e quindi segnala un errore.

   ![impossibile ritentare i riferimenti remoti delle risorse](assets/reference-report-failure.png)
