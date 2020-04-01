---
title: Utilizzare le risorse collegate per la condivisione di risorse DAM nel flusso di lavoro di authoring di Adobe Experience Manager Sites
description: Utilizzare le risorse disponibili in un’implementazione remota di Adobe Experience Manager Assets durante la creazione di pagine web in un’altra implementazione di Experience Manager Sites.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 3c2c47b5d660fefd31470ce8d555c7bb949fa036

---


# Utilizzare la funzione Risorse collegate per condividere risorse DAM in AEM Sites {#use-connected-assets-to-share-dam-assets-in-aem-sites}

Nelle grandi aziende l’infrastruttura necessaria per la creazione di siti web può essere dislocata in luoghi diversi. A volte, le funzionalità per la creazione di siti web e le risorse digitali utilizzate per creare i siti possono trovarsi in implementazioni diverse. Alcuni motivi possono essere la distribuzione geografica delle installazioni esistenti necessarie per lavorare in parallelo o acquisizioni che determinano un&#39;infrastruttura eterogenea che la società madre desidera utilizzare insieme.

AEM Sites offre la funzionalità di creazione di pagine web e AEM Assets è il sistema di gestione delle risorse digitali (DAM) che fornisce le risorse necessarie per i siti web. AEM supporta ora questo tipo di caso d’uso mediante l’integrazione di AEM Sites e AEM Assets.

## Panoramica della funzione Risorse collegate {#overview-of-connected-assets}

Durante la modifica delle pagine nell’Editor pagina, gli autori possono cercare, sfogliare e incorporare facilmente le risorse di una diversa implementazione di AEM Assets. Un amministratore AEM può effettuare un’integrazione una tantum tra un’implementazione locale di AEM Sites e un’altra implementazione (remota) di AEM Assets.

Per gli autori di Sites, le risorse remote sono disponibili come risorse locali di sola lettura. Questa funzionalità supporta la ricerca e l’utilizzo di un numero limitato di risorse remote alla volta. Per rendere disponibili contemporaneamente numerose risorse remote in un’implementazione locale, è consigliabile effettuare una migrazione in massa delle risorse. Consulta la [guida alla migrazione di Assets](/help/assets/assets-migration-guide.md).

### Prerequisiti e implementazioni supportate {#prerequisites}

Prima di utilizzare o configurare questa funzionalità, verifica questi aspetti:

* Gli utenti fanno parte dei gruppi di utenti appropriati per ciascuna implementazione.
* Per i tipi di implementazione di Adobe Experience Manager, deve essere soddisfatto uno dei criteri supportati. Risorse AEM 6.5 funziona con AEM come servizio cloud. Per ulteriori informazioni, vedi [Funzionalità delle risorse connesse in AEM come servizio](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/assets/admin/use-assets-across-connected-assets-instances.html)cloud.

   |  | AEM Sites as a Cloud Service | AEM 6.5 Sites in AMS | AEM 6.5 Sites on-premise |
   |---|---|---|---|
   | **AEM Assets as a Cloud Service** | Supportato | Supportato | Supportato |
   | **AEM 6.5 Assets in AMS** | Supportato | Supportato | Supportato |
   | **AEM 6.5 Assets on-premise** | Non supportato | Non supportato | Non supportato |

### Formati di file supportati {#mimetypes}

Gli autori possono cercare in Content Finder le immagini e i tipi di documenti indicati di seguito, quindi utilizzare nell’Editor pagina le risorse che hanno cercato. È possibile aggiungere i documenti al componente `Download`, e le immagini al componente `Image`. Gli autori possono inoltre aggiungere le risorse remote a qualsiasi componente AEM personalizzato che estenda i componenti predefiniti `Download` o `Image`. L&#39;elenco dei formati supportati è:

* **Formati** immagine: I formati immagine supportati dal componente [](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/image.html) Immagine sono supportati da Risorse collegate. Le immagini Dynamic Media non sono supportate.
* **Formati di documenti**: vedi [Formati di documenti supportati da Risorse collegate](assets-formats.md#supported-document-formats).

### Utenti e gruppi interessati {#users-and-groups-involved}

Di seguito sono descritti i diversi ruoli coinvolti nella configurazione e nell’utilizzo della funzionalità e i relativi gruppi di utenti. L’ambito locale viene utilizzato per il caso d’uso in cui una pagina web viene creata da un autore. L’ambito remoto viene utilizzato per l’implementazione DAM in cui sono ospitate le risorse necessarie. Le risorse remote vengono recuperate dall’autore di Sites.

| Ruolo | Ambito | Gruppo di utenti | Nome utente nella procedura dettagliata | Requisito |
|----------------------------------|--------|------------------------------------------------------------------------------|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Amministratore AEM Sites | Locale | Amministratore AEM | `admin` | Configurare AEM, configurare l’integrazione con l’implementazione remota di Assets. |
| Utente DAM | Locale | Autore | `ksaner` | Utilizzato per visualizzare e duplicare le risorse recuperate in `/content/DAM/connectedassets/`. |
| Autore di AEM Sites | Locale | Autore (con accesso di sola lettura in DAM remoto e accesso di authoring in Sites locale) | `ksaner` | Gli utenti finali sono autori di Sites che utilizzano questa integrazione per velocizzare i contenuti. Gli autori ricercano e sfogliano le risorse in DAM remoto utilizzando Content Finder e utilizzando le immagini richieste nelle pagine web locali. Vengono utilizzate le credenziali dell’utente `ksaner` di DAM. |
| Amministratore AEM Assets | Remoto | Amministratore AEM | `admin` in AEM remoto | Configurare la condivisione risorse tra le origini (CORS, Cross-Origin Resource Sharing). |
| Utente DAM | Remoto | Autore | `ksaner` in AEM remoto | Ruolo Autore nell’implementazione AEM remota. Cercare e sfogliare le risorse in Risorse collegate mediante Content Finder. |
| Distributore DAM (utente tecnico) | Remoto | Creatori di pacchetti e autori di siti | `ksaner` in AEM remoto | Questo utente presente nell’implementazione remota viene utilizzato dal server AEM locale (non il ruolo di autore Sites) per recuperare le risorse remote, per conto dell’autore di Sites. Questo ruolo non è lo stesso dei due ruoli `ksaner` precedenti e appartiene a un gruppo di utenti diverso. |

## Configurare una connessione tra le implementazioni di Sites e Assets {#configure-a-connection-between-sites-and-assets-deployments}

Un amministratore AEM può creare l’integrazione. Dopo la creazione, le autorizzazioni necessarie per utilizzare l’integrazione vengono stabilite tramite gruppi di utenti definiti nelle implementazioni Sites e DAM.

Per configurare le risorse collegate e la connettività alla versione locale di Sites, segui i passaggi indicati di seguito.

1. Accedi a un’implementazione AEM Sites esistente o creane una tramite il seguente comando:

   1. Nella cartella del file JAR, esegui il comando seguente su un terminale per creare ciascun server AEM.
      `java -XX:MaxPermSize=768m -Xmx4096m -jar <quickstart jar filepath> -r samplecontent -p 4502 -nofork -gui -nointeractive &`

   1. Dopo alcuni minuti il server AEM viene avviato. Considera questa implementazione di AEM Sites come computer locale per l’authoring delle pagine web, ad esempio all’indirizzo `https://[local_sites]:4502`.

1. Assicurati che gli utenti e i ruoli con ambito locale siano presenti nell’implementazione di AEM Sites e in quella di AEM Assets in AMS. Crea un utente tecnico per l’implementazione di Assets e aggiungi al gruppo di utenti menzionato in [Utenti e gruppi interessati](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved).

1. Accedi all’implementazione locale di AEM Sites all’indirizzo `https://[local_sites]:4502`. Fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Configurazione risorse collegate]** e fornisci i seguenti valori:

   1. Posizione di AEM Assets: `https://[assets_servername_ams]:[port]`.
   1. Credenziali di un distributore DAM (utente tecnico).
   1. Nel campo **[!UICONTROL Punto di montaggio]** immetti il percorso AEM locale da cui AEM recupera le risorse. Ad esempio, la cartella `remoteassets`.

   1. Regola i valori di **[!UICONTROL Soglia ottimizzazione trasferimento binario originale]** in base alla rete. Il rendering di una risorsa con dimensioni superiori alla soglia viene trasferito in modo asincrono.
   1. Seleziona **[!UICONTROL Archivio dati condiviso con risorse collegate]** se per memorizzare le risorse utilizzi un archivio dati in comune tra le due implementazioni di AEM. In questo caso, il limite di soglia non ha importanza in quanto i dati binari effettivi delle risorse risiedono nell’archivio dati e non vengono trasferiti.
   ![Configurazione tipica per Risorse collegate](assets/connected-assets-typical-config.png)

   *Figura: una configurazione tipica per Risorse collegate*

1. Poiché le risorse sono già state elaborate e i rendering vengono recuperati, disattiva i moduli di avvio dei flussi di lavoro. Regola le configurazioni del modulo di avvio nell’implementazione locale (AEM Sites) per escludere la cartella `connectedassets` da cui vengono recuperate le risorse remote.

   1. Nell’implementazione di AEM Sites, fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Moduli di avvio]**.

   1. Individua i moduli di avvio con flussi di lavoro come **[!UICONTROL Aggiorna risorsa DAM]** e **[!UICONTROL Writeback di metadati DAM]**.

   1. Seleziona il modulo di avvio del flusso di lavoro e fai clic su **[!UICONTROL Proprietà]** nella barra delle azioni.

   1. Nella procedura guidata Proprietà, modifica i campi **[!UICONTROL Percorso]** in base alle mappature seguenti per aggiornare le espressioni regolari al fine di escludere il punto di montaggio **[!UICONTROL connectedassets]**.
   | Prima | Dopo |
   |---|---|
   | /content/dam(/((?!/subassets).)*/)renditions/original | /content/dam(/((?!/subassets)(?!connectedassets).)*/)renditions/original |
   | /content/dam(/.*/)renditions/original | /content/dam(/((?!connectedassets).)*/)renditions/original |
   | /content/dam(/.*)/jcr:content/metadata | /content/dam(/((?!connectedassets).)*/)jcr:content/metadata |

   >[!NOTE]
   >
   >Quando gli autori recuperano una risorsa, vengono recuperati tutti i rendering disponibili nell’implementazione AEM remota. Se desideri creare più rendering per una risorsa recuperata, ignora questo passaggio di configurazione. Viene attivato il flusso di lavoro Aggiorna risorsa DAM e vengono creati ulteriori rendering. I rendering sono disponibili solo nell’implementazione Sites locale e non nell’implementazione remota di DAM.

1. Aggiungi l’istanza AEM Sites come una delle **[!UICONTROL origini consentite]** nella configurazione CORS di AEM Assets remota.

   1. Accedi con le credenziali di amministratore. Cerca CORS. Accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > Console Web ****.

   1. Per creare una configurazione CORS per l’istanza di AEM Sites, fai clic sull’icona di ![aggiunta risorse AEM](assets/aem_assets_add_icon.png) accanto all’icona dei **[!UICONTROL criteri CORS di Adobe Granite]**.

   1. Nel campo delle **[!UICONTROL origini consentite]** inserisci l’URL dell’implementazione Sites locale, ovvero `https://[local_sites]:[port]`. Salva la configurazione.

## Utilizzare le risorse remote {#use-remote-assets}

Gli autori del sito web utilizzano Content Finder per connettersi all’istanza DAM. Gli autori possono sfogliare, cercare e trascinare le risorse remote in un componente. Per eseguire l’autenticazione nel DAM remoto, tieni a portata di mano le credenziali dell’utente DAM fornite dal tuo amministratore.

Gli autori possono utilizzare le risorse disponibili in una singola pagina web, sia nelle istanze DAM locali che in quelle DAM remote. Utilizza Content Finder per passare dalla ricerca nel DAM locale alla ricerca nel DAM remoto.

Vengono recuperati solo i tag delle risorse remote con un tag corrispondente esatto, con la stessa gerarchia di tassonomia, disponibile nell’istanza Sites locale. Tutti gli altri tag vengono eliminati. Gli autori possono cercare risorse remote utilizzando tutti i tag presenti nell’implementazione AEM remota, poiché AEM offre funzionalità di ricerca testuale.

### Procedura dettagliata per l’utilizzo {#walk-through-of-usage}

Utilizza la configurazione precedente per provare l’esperienza di authoring e comprendere il funzionamento di questa caratteristica. Utilizza documenti o immagini di tua scelta nell’implementazione remota di DAM.

1. Passa all’interfaccia utente di Assets nell’implementazione remota accedendo ad **[!UICONTROL Assets]** > **[!UICONTROL File]** dall’area di lavoro di AEM. In alternativa, puoi accedere a `https://[assets_servername_ams]:[port]/assets.html/content/dam` in un browser. Carica le risorse che hai scelto.
1. Nell’istanza di Sites, nell’attivatore del profilo in alto a destra, fai clic su **[!UICONTROL Impersona]**. Specifica `ksaner` come nome utente, seleziona l’opzione fornita e fai clic su **[!UICONTROL OK]**.
1. Apri una pagina del sito web We.Retail in **[!UICONTROL Sites]** > **[!UICONTROL We.Retail]** > **[!UICONTROL us]** > **[!UICONTROL en]**. Modifica la pagina. In alternativa, accedi a `https://[aem_server]:[port]/editor.html/content/we-retail/us/en/men.html` tramite un browser per modificare una pagina.

   Fai clic su **[!UICONTROL Attiva/Disattiva pannello laterale]** nell’angolo in alto a sinistra della pagina.

1. Apri la scheda Risorse e fai clic su **[!UICONTROL Accedi alle risorse collegate]**.
1. Immetti le credenziali: `ksaner` come nome utente e `password` come password. Questo utente dispone di autorizzazioni di authoring per entrambe le implementazioni di AEM.
1. Cerca la risorsa aggiunta a DAM. Le risorse remote vengono visualizzate nel pannello a sinistra. Filtra immagini o documenti e filtra ulteriormente i tipi di documenti supportati. Trascina le immagini su un componente `Image`, e i documenti su un componente `Download`.

   Le risorse recuperate sono di sola lettura nell’implementazione locale di AEM Sites. Puoi comunque utilizzare le opzioni fornite dai componenti di AEM Sites per modificare la risorsa recuperata. La modifica per componenti non è distruttiva.

   ![Opzioni di filtro per tipi di documenti e immagini nella ricerca di risorse in DAM remoto](assets/filetypes_filter_connected_assets.png)

   *Figura: opzioni di filtro per tipi di documenti e immagini nella ricerca di risorse in DAM remoto*

1. Un autore del sito riceve una notifica se una risorsa viene recuperata in modo asincrono e se un’attività di recupero ha esito negativo. Durante l’authoring, o anche successivamente, gli autori possono visualizzare informazioni dettagliate sulle attività di recupero e sugli errori nell’interfaccia utente [Processi asincroni](/help/assets/asynchronous-jobs.md).

   ![Notifica relativa al recupero asincrono delle risorse in background.](assets/assets_async_transfer_fails.png)

   *Figura: notifica relativa al recupero asincrono delle risorse in background*

1. Quando pubblichi una pagina, AEM visualizza un elenco completo delle risorse utilizzate nella pagina. Assicurati che le risorse remote vengano recuperate correttamente al momento della pubblicazione. Per verificare lo stato di ciascuna risorsa recuperata, consulta l’interfaccia utente dei [processi asincroni](/help/assets/asynchronous-jobs.md).

   >[!NOTE]
   >
   >La pagina viene pubblicata anche se una o più risorse remote non vengono recuperate. Il componente che utilizza la risorsa remota viene pubblicato come vuoto. L’area di notifica di AEM mostra la notifica degli errori visualizzati nella pagina dei processi asincroni.

>[!CAUTION]
>
>Una volta utilizzate in una pagina web, le risorse remote recuperate possono essere cercate e utilizzate da qualsiasi utente con autorizzazioni di accesso alla cartella locale in cui sono memorizzate (nel passaggio precedente: `connectedassets`). Le risorse possono inoltre essere cercate e visualizzate nell’archivio locale tramite [!UICONTROL Content Finder].

Le risorse recuperate possono essere utilizzate come qualsiasi altra risorsa locale, ad eccezione del fatto che i metadati associati non possono essere modificati.

## Limitazioni   {#limitations}

**Autorizzazioni e gestione delle risorse**

* Le risorse locali non vengono sincronizzate con le risorse originali nell’implementazione remota. Eventuali modifiche, eliminazioni o revoche delle autorizzazioni nell’implementazione DAM non vengono propagate downstream.
* Le risorse locali sono copie in sola lettura. I componenti AEM apportano modifiche non distruttive alle risorse. Non sono consentite altre modifiche.
* Le risorse recuperate localmente sono disponibili solo a scopo di authoring. I flussi di lavoro di aggiornamento delle risorse non possono essere applicati e i metadati non possono essere modificati.
* Sono supportati solo le immagini e i formati di documento elencati. Le risorse Dynamic Media, i frammenti di contenuto e i frammenti di esperienza non sono supportati.
* Gli schemi di metadati non vengono recuperati.
* Tutti gli autori di Sites dispongono di autorizzazioni di lettura per le copie recuperate, anche se non dispongono di accesso all’implementazione remota di DAM.
* Nessun supporto API per personalizzare l’integrazione.
* Questa funzionalità supporta la ricerca e l’utilizzo diretti delle risorse remote. Per rendere disponibili molte risorse remote nell’implementazione locale con un’unica operazione, è consigliabile eseguire la migrazione delle risorse. Consulta la [guida alla migrazione di Assets](assets-migration-guide.md).
* Non è possibile utilizzare una risorsa remota come miniatura di pagina nell’interfaccia utente Proprietà  pagina. Per impostare una miniatura di una pagina Web nell’interfaccia utente Proprietà  pagina dalla [!UICONTROL miniatura] , fare clic su [!UICONTROL Seleziona immagine].

**Configurazione e licenze**

* È supportata l’implementazione di AEM Assets in AMS.
* AEM Sites può connettersi a un solo archivio di AEM Assets alla volta.
* Una licenza di AEM Assets che funziona come archivio remoto.
* Una o più licenze di AEM Sites che funzionano come implementazione di authoring locale.

**Utilizzo**

* È supportata solo la ricerca di risorse remote e il trascinamento delle risorse remote sulla pagina locale per creare contenuti.
* L’operazione di recupero si interrompe per timeout dopo 5 secondi. Gli autori possono rilevare dei problemi durante il recupero delle risorse, ad esempio in caso di problemi di rete. Gli autori possono riprovare trascinando la risorsa remota da [!UICONTROL Content Finder] all’[!UICONTROL Editor pagina].
* Le risorse recuperate possono essere sottoposte a semplici modifiche non distruttive e alle modifiche supportate tramite il componente `Image` di AEM. Le risorse sono di sola lettura.

## Risoluzione dei problemi {#troubleshoot}

Per risolvere eventuali errori comuni, segui i passaggi indicati di seguito.

* Se non riesci a cercare le risorse remote tramite Content Finder, verifica di nuovo e assicurati che siano presenti i ruoli e le autorizzazioni richiesti.
* Una risorsa recuperata da DAM remoto potrebbe non essere pubblicata su una pagina web per i seguenti motivi: non esiste in remoto, l’utente non dispone delle autorizzazioni necessarie per recuperarla o per un errore di rete. Assicurati che la risorsa non venga rimossa da DAM remoto o che le autorizzazioni non vengano modificate; assicurati che siano soddisfatti i prerequisiti appropriati e prova di nuovo ad aggiungere la risorsa alla pagina e ripubblicarla. Controlla l’[elenco dei processi asincroni](/help/assets/asynchronous-jobs.md) per verificare la presenza di errori nel recupero delle risorse.
