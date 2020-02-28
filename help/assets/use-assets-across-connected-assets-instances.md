---
title: Utilizzare le risorse collegate per condividere le risorse DAM nel flusso di lavoro di creazione di siti Adobe Experience Manager
description: Utilizza le risorse disponibili in una distribuzione remota di Risorse Adobe Experience Manager quando crei le pagine Web in un’altra distribuzione del sito Experience Manager.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 8a014887f395c5ade0affcb3c199e090af263bdc

---


# Utilizzo di risorse collegate per condividere risorse DAM in AEM Sites {#use-connected-assets-to-share-dam-assets-in-aem-sites}

Nelle grandi imprese l&#39;infrastruttura necessaria per creare siti web può essere distribuita. A volte le capacità di creazione del sito Web e le risorse digitali utilizzate per creare questi siti Web possono risiedere in implementazioni diverse. Per alcuni motivi è possibile distribuire geograficamente le installazioni necessarie per lavorare in parallelo; acquisizioni che portano a infrastrutture eterogenee che la società madre vuole consolidare; che porta a una scala tale da richiedere un’istanza dedicata per la gestione delle risorse.

AEM Sites offre la funzionalità di creazione di pagine web e AEM Assets è il sistema di gestione delle risorse digitali (DAM) che fornisce le risorse necessarie per i siti web. AEM supporta ora questo tipo di caso d’uso mediante l’integrazione di AEM Sites e AEM Assets.

## Panoramica delle risorse connesse {#overview-of-connected-assets}

Durante la modifica delle pagine in Editor pagina, gli autori possono cercare, sfogliare e incorporare facilmente le risorse da una diversa distribuzione di Risorse AEM. Un amministratore AEM può effettuare un’integrazione una tantum di una distribuzione locale di AEM Sites con una distribuzione diversa (remota) di AEM Assets.

Per gli autori dei siti, le risorse remote sono disponibili come risorse locali di sola lettura. Questa funzionalità supporta la ricerca e l&#39;utilizzo di poche risorse remote alla volta. Per rendere disponibili molte risorse remote nella distribuzione locale in una sola volta, è consigliabile migrare le risorse in massa. Consulta la guida [alla migrazione delle](/help/assets/assets-migration-guide.md)risorse.

### Prerequisiti e distribuzioni supportate {#prerequisites}

Prima di utilizzare o configurare questa funzionalità, accertati di:

* Gli utenti fanno parte dei gruppi di utenti appropriati per ciascuna distribuzione.
* Per i tipi di distribuzione di Adobe Experience Manager, uno dei criteri supportati è soddisfatto. Risorse AEM 6.5 funziona con AEM come servizio cloud. Per ulteriori informazioni, vedi [Funzionalità delle risorse connesse in AEM come servizio](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/assets/admin/use-assets-across-connected-assets-instances.html)cloud.

   |  | AEM Sites as a Cloud Service | Siti AEM 6.5 su AMS | AEM 6.5 Sites on-premise |
   |---|---|---|---|
   | **AEM Assets as a Cloud Service** | Supportato | Supportato | Supportato |
   | **Risorse AEM 6.5 su AMS** | Non supportato | Supportato | Supportato |
   | **Risorse AEM 6.5 in sede** | Non supportato | Non supportato | Non supportato |

### Formati di file supportati {#mimetypes}

Gli autori possono cercare immagini e i seguenti tipi di documenti in Content Finder e utilizzare le risorse ricercate in Editor pagina. È possibile aggiungere dei documenti al `Download` componente e aggiungere delle immagini al `Image` componente. Gli autori possono inoltre aggiungere le risorse remote a qualsiasi componente AEM personalizzato che estenda i componenti predefiniti `Download` o `Image` . Per un elenco dei formati supportati, consulta Formati [supportati per le risorse](assets-formats.md#supported-document-formats)connesse.

### Users and groups involved {#users-and-groups-involved}

Di seguito sono descritti i vari ruoli coinvolti nella configurazione e nell&#39;utilizzo della funzionalità e dei relativi gruppi di utenti. L&#39;ambito locale viene utilizzato per il caso di utilizzo in cui una pagina Web viene creata da un autore. L&#39;ambito remoto viene utilizzato per la distribuzione DAM in cui sono ospitate le risorse necessarie. Le risorse remote vengono recuperate dall’autore dei siti.

| Ruolo | Ambito | Gruppo utenti | Nome utente nella procedura dettagliata | Requisito |
|----------------------------------|--------|------------------------------------------------------------------------------|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Amministratore di AEM Sites | Locale | Amministratore AEM | `admin` | Configurare AEM, configurare l’integrazione con la distribuzione remota di Risorse. |
| Utente DAM | Locale | Authoring | `ksaner` | Utilizzato per visualizzare e duplicare le risorse recuperate in `/content/DAM/connectedassets/`. |
| Autore di AEM Sites | Locale | Autore (con accesso in lettura su DAM remoto e accesso all&#39;autore su Siti locali) | `ksaner` | Gli utenti finali sono autori di Siti che utilizzano questa integrazione per migliorare la velocità dei contenuti. Gli autori ricercano e sfogliano le risorse in DAM remoto utilizzando Content Finder e utilizzando le immagini richieste nelle pagine Web locali. Vengono utilizzate le credenziali dell&#39;utente `ksaner` DAM. |
| Amministratore di AEM Assets | Remoto | Amministratore AEM | `admin` su AEM remoto | Configurare CORS (Cross-Origin Resource Sharing). |
| Utente DAM | Remoto | Authoring | `ksaner` su AEM remoto | Ruolo di authoring nella distribuzione AEM remota. Cercate e sfogliate le risorse in Risorse collegate mediante Content Finder. |
| Distributore DAM (utente tecnico) | Remoto | creazione di pacchetti e autori di siti | `ksaner` su AEM remoto | Questo utente presente nella distribuzione remota viene utilizzato dal server locale AEM (non dal ruolo di autore del sito) per recuperare le risorse remote, per conto dell’autore di Siti. Questo ruolo non è lo stesso dei due `ksaner` ruoli precedenti e appartiene a un gruppo di utenti diverso. |

## Configurare una connessione tra le distribuzioni di Siti e Risorse {#configure-a-connection-between-sites-and-assets-deployments}

Un amministratore AEM può creare questa integrazione. Una volta create, le autorizzazioni necessarie per utilizzarle vengono stabilite tramite gruppi di utenti definiti nella distribuzione Siti e nella distribuzione DAM.

Per configurare le risorse connesse e la connettività ai siti locali, segui questi passaggi.

1. Accedi a una distribuzione AEM Sites esistente o crea una distribuzione tramite il seguente comando:

   1. Nella cartella del file JAR, eseguite il comando seguente su un terminale per creare ogni server AEM.
      `java -XX:MaxPermSize=768m -Xmx4096m -jar <quickstart jar filepath> -r samplecontent -p 4502 -nofork -gui -nointeractive &`

   1. Dopo alcuni minuti, il server AEM si avvia correttamente. Considerate questa implementazione di AEM Sites come computer locale per l&#39;authoring delle pagine Web, ad esempio in `https://[local_sites]:4502`.

1. Verifica che gli utenti e i ruoli con ambito locale siano presenti nella distribuzione di AEM Sites e nella distribuzione di AEM Assets su AMS. Crea un utente tecnico per la distribuzione delle risorse e aggiungi al gruppo di utenti menzionato in [utenti e gruppi coinvolti](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved).

1. Accedi alla distribuzione locale di AEM Sites in `https://[local_sites]:4502`. Fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > Configurazione **[!UICONTROL risorse]** connesse e specifica i seguenti valori:

   1. La posizione di Risorse AEM è `https://[assets_servername_ams]:[port]`.
   1. Credenziali di un distributore DAM (utente tecnico).
   1. Nel campo Punto **[!UICONTROL di]** montaggio, inserite il percorso AEM locale in cui AEM raccoglie le risorse. Ad esempio, `remoteassets` cartella.

   1. Regola i valori di Soglia **[!UICONTROL di ottimizzazione trasferimento binario]** originale in base alla rete. La rappresentazione di una risorsa con una dimensione maggiore di questa soglia viene trasferita in modo asincrono.
   1. Se utilizzi un archivio dati per archiviare le risorse, seleziona **[!UICONTROL archivio dati condiviso con risorse]** collegate e il datastore è lo storage comune tra le due distribuzioni AEM. In questo caso, il limite di soglia non ha importanza in quanto i binari di attività effettivi risiedono nel datastore e non vengono trasferiti.
   ![Configurazione tipica per le risorse connesse](assets/connected-assets-typical-config.png)

   *Figura:Configurazione tipica per le risorse connesse*

1. Poiché le risorse sono già state elaborate e le rappresentazioni vengono recuperate, disattivate gli avviatori dei flussi di lavoro. Regolate le configurazioni di avvio nella distribuzione locale (AEM Sites) per escludere la `connectedassets` cartella in cui vengono recuperate le risorse remote.

   1. Nella distribuzione AEM Sites, fate clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso]** di lavoro > **[!UICONTROL Lanci]**.

   1. Cerca avviatori con flussi di lavoro come **[!UICONTROL DAM Update Asset]** e **[!UICONTROL DAM Metadata Write]**.

   1. Selezionate il lancio del flusso di lavoro e fate clic su **[!UICONTROL Proprietà]** nella barra delle azioni.

   1. Nella procedura guidata Proprietà, modificare i campi **[!UICONTROL Percorso]** come le seguenti mappature per aggiornare le espressioni regolari al fine di escludere le risorse **** collegate ai punti di montaggio.
   | Prima | Dopo |
   |---|---|
   | /content/dam(/(?!/subassets).*/)rappresentazioni/originali | /content/dam(/(?!/subassets)(?!connectedassets).)*/)rappresentazioni/originali |
   | /content/dam(/.*/)rappresentazioni/originali | /content/dam(/(?!connectedassets).*/)rappresentazioni/originali |
   | /content/dam(/.*)/jcr:content/metadata | /content/dam(/(?!connectedassets).*/)jcr:content/metadata |

   >[!NOTE]
   >
   >Quando gli autori recuperano una risorsa, vengono recuperate tutte le rappresentazioni disponibili nella distribuzione AEM remota. Se desiderate creare più rappresentazioni di una risorsa recuperata, saltate questo passaggio di configurazione. Viene attivato il flusso di lavoro Aggiorna risorsa DAM e vengono create più rappresentazioni. Queste rappresentazioni sono disponibili solo nella distribuzione di Siti locali e non nella distribuzione remota di DAM.

1. Aggiungi l’istanza AEM Sites come una delle origini **[!UICONTROL consentite]** nella configurazione CORS di Risorse AEM remota.

   1. Effettuate l&#39;accesso utilizzando le credenziali dell&#39;amministratore. Cercate Cross-Origin. Accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > Console **** Web.

   1. Per creare una configurazione CORS per l’istanza di AEM Sites, fai clic sull’icona ![aem_assets_add_icon](assets/aem_assets_add_icon.png) accanto all’icona **[!UICONTROL Adobe Granite Cross-Origin Resource Sharing Policy]**(Condivisione risorse tra le origini di Adobe Granite).

   1. Nel campo **[!UICONTROL Origini]** consentite, inserite l&#39;URL dei Siti locali, ovvero `https://[local_sites]:[port]`. Salvate la configurazione.

## Utilizzare risorse remote {#use-remote-assets}

Gli autori del sito Web utilizzano Content Finder per connettersi all&#39;istanza DAM. Gli autori possono sfogliare, cercare e trascinare le risorse remote in un componente. Per eseguire l&#39;autenticazione nel DAM remoto, tieni a portata di mano le credenziali dell&#39;utente DAM fornite dal tuo amministratore.

Gli autori possono utilizzare le risorse disponibili in una singola pagina Web, sia nelle istanze DAM locali che in quelle DAM remote. Utilizzate Content Finder per passare dalla ricerca nel DAM locale alla ricerca nel DAM remoto.

Vengono recuperati solo i tag delle risorse remote con un tag corrispondente esatto, con la stessa gerarchia tassonomia, disponibile nell’istanza Siti locale. Tutti gli altri tag vengono eliminati. Gli autori possono cercare risorse remote utilizzando tutti i tag presenti nella distribuzione AEM remota, poiché AEM offre una ricerca full-text.

### Procedura dettagliata di utilizzo {#walk-through-of-usage}

Utilizzate la configurazione di cui sopra per provare l’esperienza di authoring per comprendere come funziona la funzionalità. Utilizza documenti o immagini di tua scelta nella distribuzione remota di DAM.

1. Passa all’interfaccia utente Risorse nella distribuzione remota accedendo a **[!UICONTROL Risorse]** > **[!UICONTROL File]** dall’area di lavoro di AEM. In alternativa, potete accedere `https://[assets_servername_ams]:[port]/assets.html/content/dam` in un browser. Caricate le risorse di vostra scelta.
1. Nell’istanza Siti, nell’attivatore del profilo nell’angolo in alto a destra, fate clic su **[!UICONTROL Impersona con nome]**. Specificate `ksaner` come nome utente, selezionate l’opzione fornita e fate clic su **[!UICONTROL OK]**.
1. Aprite una pagina Web We.Retail in **[!UICONTROL Sites]** > **[!UICONTROL We.Retail]** > **[!UICONTROL us]** > **[!UICONTROL it]**. Modificate la pagina. In alternativa, potete accedere `https://[aem_server]:[port]/editor.html/content/we-retail/us/en/men.html` a un browser per modificare una pagina.

   Fate clic su **[!UICONTROL Attiva/disattiva pannello]** laterale nell’angolo superiore sinistro della pagina.

1. Aprite la scheda Risorse e fate clic su **[!UICONTROL Accedi alle risorse]** connesse.
1. Immettete le credenziali, `ksaner` come nome utente e `password` come password. Questo utente dispone di autorizzazioni di authoring per entrambe le distribuzioni AEM.
1. Cercate la risorsa aggiunta a DAM. Le risorse remote vengono visualizzate nel pannello a sinistra. Filtrare immagini o documenti e filtrare ulteriormente i tipi di documenti supportati. Trascinate le immagini su un `Image` componente e i documenti su un `Download` componente.

   Le risorse recuperate sono di sola lettura nella distribuzione locale di AEM Sites. Puoi comunque utilizzare le opzioni fornite dai componenti di AEM Sites per modificare la risorsa recuperata. La modifica per componenti non è distruttiva.

   ![Opzioni per filtrare i tipi di documenti e le immagini durante la ricerca di risorse in DAM remoto](assets/filetypes_filter_connected_assets.png)

   *Figura: Opzioni per filtrare i tipi di documenti e le immagini durante la ricerca di risorse in DAM remoto*

1. Un autore del sito riceve una notifica se una risorsa viene recuperata in modo asincrono e se un’attività di recupero ha esito negativo. Durante l’authoring o anche dopo l’authoring, gli autori possono visualizzare informazioni dettagliate sulle attività di recupero e sugli errori nell’interfaccia utente dei processi [](/help/assets/asynchronous-jobs.md) asincroni.

   ![Notifica del recupero asincrono delle risorse che si verifica in background.](assets/assets_async_transfer_fails.png)

   *Figura: Notifica del recupero asincrono delle risorse che si verifica in background.*

1. Quando si pubblica una pagina, AEM visualizza un elenco completo delle risorse utilizzate nella pagina. Accertatevi che le risorse remote vengano recuperate correttamente al momento della pubblicazione. Per verificare lo stato di ciascuna risorsa recuperata, consultate Interfaccia utente dei processi [](/help/assets/asynchronous-jobs.md) asincroni.

   >[!NOTE]
   >
   >Anche se una o più risorse remote non vengono recuperate, la pagina viene pubblicata. Il componente che utilizza la risorsa remota viene pubblicato vuoto. L’area di notifica di AEM visualizza la notifica degli errori visualizzati nella pagina dei processi asincroni.

>[!CAUTION]
>
>Una volta utilizzate in una pagina Web, le risorse remote recuperate sono ricercabili e utilizzabili da chiunque disponga delle autorizzazioni per accedere alla cartella locale in cui sono memorizzate le risorse recuperate (`connectedassets` nel passaggio precedente). Le risorse sono inoltre ricercabili e visibili nell&#39;archivio locale tramite [!UICONTROL Content Finder].

Le risorse recuperate possono essere usate come qualsiasi altra risorsa locale, a eccezione del fatto che i metadati associati non possono essere modificati.

## Limiti {#limitations}

**Autorizzazioni e gestione delle risorse**

* Le risorse locali non vengono sincronizzate con le risorse originali nella distribuzione remota. Eventuali modifiche, eliminazioni o revoca delle autorizzazioni sulla distribuzione DAM non vengono propagate a valle.
* Le risorse locali sono copie in sola lettura. I componenti AEM apportano modifiche non distruttive alle risorse. Non sono consentite altre modifiche.
* Le risorse recuperate localmente sono disponibili solo a scopo di authoring. I flussi di lavoro di aggiornamento delle risorse non possono essere applicati e i metadati non possono essere modificati.
* Sono supportati solo le immagini e i formati di documento elencati. Le risorse multimediali dinamiche, i frammenti di contenuto e i frammenti esperienza non sono supportati.
* Gli schemi di metadati non vengono recuperati.
* Tutti gli autori dei siti dispongono di autorizzazioni di lettura sulle copie recuperate, anche se non dispongono dell&#39;accesso alla distribuzione remota di DAM.
* Nessun supporto API per personalizzare l&#39;integrazione.
* Questa funzionalità supporta la ricerca e l&#39;utilizzo senza soluzione di continuità delle risorse remote. Per rendere disponibili molte risorse remote nella distribuzione locale in un&#39;unica operazione, è consigliabile eseguire la migrazione delle risorse. Consulta la guida [alla migrazione delle](assets-migration-guide.md)risorse.
* Non è possibile utilizzare una risorsa remota come miniatura di pagina nell’interfaccia utente Proprietà  pagina. Per impostare una miniatura di una pagina Web nell’interfaccia utente Proprietà  pagina dalla [!UICONTROL miniatura] , fare clic su [!UICONTROL Seleziona immagine].

**Configurazione e licenze**

* È supportata la distribuzione di AEM Assets su AMS.
* AEM Sites può connettersi a un unico archivio di Risorse AEM alla volta.
* Una licenza di Risorse AEM che funziona come archivio remoto.
* Una o più licenze di AEM Sites che funzionano come distribuzione di authoring locale.

**Utilizzo**

* È supportata solo la ricerca di risorse remote e il trascinamento delle risorse remote sulla pagina locale per creare contenuti.
* Timeout dell&#39;operazione di recupero dopo 5 secondi. Gli autori possono rilevare dei problemi durante il recupero delle risorse, ad esempio in caso di problemi di rete. Gli autori possono riprovare trascinando la risorsa remota da [!UICONTROL Content Finder] all’editor [!UICONTROL di]pagina.
* Le risorse recuperate possono essere sottoposte a semplici modifiche non distruttive e alle modifiche supportate tramite il componente AEM `Image` . Le risorse sono di sola lettura.

## Risoluzione dei problemi {#troubleshoot}

Per risolvere eventuali situazioni di errore comuni, effettuate le seguenti operazioni:

* Se non riuscite a cercare risorse remote da Content Finder, verificate nuovamente e accertatevi che i ruoli e le autorizzazioni richiesti siano attivi.
* Una risorsa recuperata dalla diga remota potrebbe non essere pubblicata su una pagina Web per i seguenti motivi: non esiste sul telecomando; mancanza di autorizzazioni adeguate per recuperarla; errore di rete. Assicurati che la risorsa non venga rimossa dal DAM remoto o che le autorizzazioni non vengano modificate; garantire che siano soddisfatti i prerequisiti adeguati; provate ad aggiungere la risorsa alla pagina e ripubblicatela. Controllate l’ [elenco dei processi](/help/assets/asynchronous-jobs.md) asincroni per verificare la presenza di errori nel recupero delle risorse.
