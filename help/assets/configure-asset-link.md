---
title: Configurare Experience Manager Assets, ad Adobe Asset Link
description: Configura Experience Manager Assets per l’utilizzo con l’estensione Adobe Asset Link per le applicazioni Creative Cloud.
contentOwner: Vishabh Gupta
role: Admin
feature: Asset Management
exl-id: 3a9b44d4-1756-4ad5-91df-df8d53e82193
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '3060'
ht-degree: 0%

---

# Configurare Experience Manager Assets, ad Adobe Asset Link {#adobe-asset-link}

[Adobe Asset Link (AAL)](https://www.adobe.com/it/creativecloud/business/enterprise/adobe-asset-link.html) semplifica la collaborazione tra creativi e professionisti del marketing nel processo di creazione dei contenuti. Collega Adobe Experience Manager Assets con le app desktop Creative Cloud Adobe InDesign, Adobe Photoshop e Adobe Illustrator. Il pannello Adobe Asset Link consente ai creativi di accedere e modificare i contenuti archiviati in AEM Assets senza uscire dalle app creative che preferiscono.

Per configurare Experience Manager Assets per l’utilizzo con Asset Link, implementa le seguenti attività. Utilizza l’account amministratore Experience Manager per eseguire la configurazione:

1. Installa i pacchetti come richiesto. I dettagli sono in [prerequisiti](#prerequisites).

1. Configura Experience Manager [manualmente](#manual-configuration) o utilizzando un [pacchetto](#configure-using-package).

1. Per associare utenti con licenza Creative Cloud a utenti Experienci Manager, gestisci [controllo dell’accesso utente](#user-access).

1. Crea [indice query personalizzato](#create-custom-index), configura [Copie trasformate FPO](/help/assets/configure-fpo-renditions.md) per InDesign, configura [Integrazione con Adobe Stock](/help/assets/aem-assets-adobe-stock.md), e configurare [ricerca visiva o per somiglianza](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/search-assets.html#configvisualsearch).

## Prerequisiti e supporto per varie funzionalità {#prerequisites}

Assicurarsi di installare il service pack e il pacchetto appropriati in base alle esigenze. Per ogni versione di Experience Manager e per le funzionalità specifiche, vedi i seguenti requisiti.

| Funzionalità risorse | Versione Experience Manager e requisiti per il supporto |
|--- |--- |
| Asset Link funziona per impostazione predefinita | Experienci Manager 6.5 e 6.5.2 o successivi. </br> Experienci Manager 6.4.4 e 6.4.6 o successivi. </br> L’Adobe consiglia di installare la versione più recente [Service Pack di Experience Manager (SP)](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=it) prima di utilizzare AAL. |
| Asset Link funziona dopo l’installazione di un pacchetto | Ad Experience Manager 6.4.0 - 6.4.3, installare [adobe-asset-link-support](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/featurepack/adobe-asset-link-support) pacchetto. |
| Integrazione con Adobe Stock | Experience Manager 6.4.2 o successivo |
| Ricerca visiva o per affinità | Experience Manager 6.5.0 o successivo |


## Configurare l’Experience Manager utilizzando il pacchetto di configurazione {#configure-using-package}

L’Adobe consiglia di installare [adobe-asset-link-config](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/product/assets/adobe-asset-link-config) pacchetto di configurazione per automatizzare la maggior parte delle attività di configurazione, seguito da alcune attività manuali. In alternativa, è possibile: [configurare manualmente](#manual-configuration).

>[!CAUTION]
>
>Se l’istanza di Experience Manager è configurata per l’accesso utente con account Adobe IMS, non utilizzare il pacchetto di configurazione. Invece, [configurare manualmente](#manual-configuration) l’istanza Experience Manager.

1. Per aprire Gestione pacchetti, ad Experience Manager nell’interfaccia web, accedi **[!UICONTROL Strumenti]** > **[!UICONTROL Distribuzione]** > **[!UICONTROL Condivisione pacchetti]**. Installa `adobe-asset-link-config` pacchetto.

1. Accesso **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Console web]**. Individua **[!UICONTROL Provider IMS OAuth Adobe Granite]** e fai clic su per modificarla.

   Imposta le seguenti proprietà e salva le modifiche.

   * [!UICONTROL Mappature gruppo]: lascia vuoto a meno che non lo desideri. Per ulteriori informazioni, consulta [Mappatura gruppo](#group-mapping).
   * [!UICONTROL Organizzazione]: immetti l’ID organizzazione utilizzato in Adobe Admin Console. Per ulteriori informazioni sugli ID organizzazione, consulta [Crea gruppo utenti](https://helpx.adobe.com/enterprise/using/create-aal-user-group.html).

1. Individua **[!UICONTROL Gestore autenticazione Bearer Granite Adobe]** e fai clic su per modificarla.

   Aggiungi **[!UICONTROL InDesignAem2]** ID client per **[!UICONTROL ID client OAuth consentiti]** proprietà di configurazione.


## Configura manualmente Experience Manager {#manual-configuration}

Configura manualmente Experience Manager se scegli di non utilizzare un pacchetto di configurazione o se la tua implementazione di Experience Manager è configurata per supportare l’accesso degli utenti con gli account Adobe IMS.

Per configurare manualmente Experience Manager:

1. Per accedere alla gestione della configurazione, accedere a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Console web]**. Seleziona **[!UICONTROL OSGi]** > **[!UICONTROL Configurazione]** dal menu nella parte superiore.

1. Individua il **[!UICONTROL Provider IMS OAuth Adobe Granite]** e fai clic su per modificarla.

   Imposta la seguente configurazione e fai clic su **[!UICONTROL Salva]**.

   * [!UICONTROL Endpoint di autorizzazione]: ` https://ims-na1.adobelogin.com/ims/authorize/v1`
   * [!UICONTROL Endpoint token]: ` https://ims-na1.adobelogin.com/ims/token/v1`
   * [!UICONTROL Endpoint profilo]: ` https://ims-na1.adobelogin.com/ims/profile/v1`
   * [!UICONTROL URL di convalida]: ` https://ims-na1.adobelogin.com/ims/validate_token/v1`
   * [!UICONTROL Organizzazione]: impostato sull’ID organizzazione in [Adobe Admin Console](https://adminconsole.adobe.com/).
   * [!UICONTROL Mappature gruppo]: lascia vuoto a meno che non abbia un caso speciale. Per ulteriori informazioni, consulta [Mappatura gruppo](#group-mapping).

1. Individua **[!UICONTROL Gestore autenticazione Bearer Granite Adobe]** e fai clic su per modificarla.

   Aggiungi i seguenti ID client a **[!UICONTROL ID client OAuth consentiti]** proprietà di configurazione: `InDesignAem2, cc-europa-desktop_0_1, cc-europa-desktop_1_0, cc-europa-desktop_2_0, cc-europa-desktop_3_0, cc-europa-desktop_4_0, cc-europa-desktop_5_0, cc-europa-desktop_6_0, cc-europa-desktop_7_0, cc-europa-desktop_8_0, cc-europa-desktop_9_0, and cc-europa-desktop_10_0`.

   Per aggiungere ciascuno `Client ID`, fai clic su `+`. Clic **[!UICONTROL Salva]** dopo l’aggiunta di tutti gli ID.

1. In entrata **[!UICONTROL Applicazione e provider OAuth Adobe Granite]** configurazione, verifica la configurazione **[!UICONTROL Gestore autenticazione OAuth Adobe Granite]** istanze. Se si individua un&#39;istanza con `Config ID` valore di `ims`, utilizzarlo per le istruzioni di questa procedura. In caso contrario, fare clic su `+` per creare un&#39;istanza di configurazione. Imposta i seguenti valori di proprietà e fai clic su **[!UICONTROL Salva]**.

   * [!UICONTROL ID client]: non modificare
   * [!UICONTROL Segreto client]: non modificare
   * [!UICONTROL ID configurazione]: ` ims`
   * [!UICONTROL Ambito]: `AdobeID, OpenID, read_organizations` (nella configurazione possono essere presenti anche altri valori)
   * [!UICONTROL ID provider]: ` ims`
   * [!UICONTROL Crea utenti]: ` Checked`
   * [!UICONTROL Proprietà ID utente]: `Email` per la configurazione appena creata. In caso contrario, non modificare.

1. Individua il **[!UICONTROL Gestore di sincronizzazione predefinito Apache Jackrabbit Oak]** configurazione con **[!UICONTROL Nome gestore di sincronizzazione]** `ims` e fai clic su per modificarlo.

   Imposta le seguenti proprietà di configurazione e fai clic su **[!UICONTROL Salva]**.

   * [!UICONTROL Scadenza utente e scadenza appartenenza utente]: tempo in minuti seguito da &#39;m&#39; senza spazio. Ad esempio: `15m` per 15 minuti. Per ulteriori informazioni, consulta [Mappatura gruppo](#group-mapping).
   * [!UICONTROL Iscrizione automatica utente]: non modificare
   * [!UICONTROL Appartenenza dinamica utente]: ` Deslect`

1. Individua il **[!UICONTROL Gestore autenticazione OAuth Adobe Granite]** e fai clic su per modificarla. Senza apportare alcuna modifica, fai clic su **[!UICONTROL Salva]**.

1. Per regolare la priorità relativa del gestore di autenticazione Bearer, in CRXDE, passa a `/apps/system/config`. Individua `com.adobe.granite.auth.oauth.impl.BearerAuthenticationHandler.config` e apri la relativa configurazione. Alla fine, aggiungere `service.ranking=I"-10"`. Salva le modifiche.

   >[!NOTE]
   >
   >Ogni richiesta autenticata con un token Bearer sostiene il sovraccarico di tre chiamate ad Adobe IMS, la sincronizzazione degli utenti e la creazione di un token di accesso in Experience Manager. Per ovviare a questo sovraccarico, Adobe Asset Link acquisisce il token di accesso restituito nella risposta di Experience Manager e lo invia con le richieste successive. Affinché questo processo funzioni, è necessario regolare la priorità relativa del gestore di autenticazione Bearer.

1. (Facoltativo) Se gli utenti dell’Experience Manager hanno nomi di dominio con lettere maiuscole o minuscole diverse nei loro ID e-mail, seleziona **[!UICONTROL Usa lettere minuscole per l&#39;utente di blocco]** in **[!UICONTROL Adobe di configurazioni della piattaforma ACP Granite]** in Experience Manager Web Console.

## Configurazione aggiuntiva dopo la migrazione ai profili aziendali {#configure-migration-activity}

Gli utenti di Adobe Asset Link possono connettersi a Experience Manager per consentire l’accesso IMS dall’organizzazione principale Creative Cloud for Enterprise (CCE). Experience Manager utilizza gli ID client per identificare l’organizzazione IMS consentita. Dopo la migrazione ai profili aziendali, è necessario configurare l’ID client e la chiave segreta per l’organizzazione IMS, ad Experience Manager per il gestore di autenticazione Bearer. Per ulteriori informazioni sui profili aziendali, consulta [introduzione ai profili di Adobe](https://helpx.adobe.com/enterprise/kb/introducing-adobe-profiles.html).

È necessaria una configurazione aggiuntiva solo se utilizzi diverse organizzazioni Adobe IMS, ad Experience Manager e Creative Cloud for Enterprise (CCE), e tra queste due organizzazioni viene stabilita una relazione di trust tra domini.

>[!NOTE]
>
>* La correzione per i profili aziendali è fornita nell&#39;Experience Manager 6.5.11.0.
>* La configurazione esistente continua a funzionare se utilizzi la stessa organizzazione Adobe IMS con Experience Manager e CCE.


**Prerequisiti**

1. Un’istanza Experience Manager in esecuzione con autenticazione Bearer configurata per AAL.
1. Installa il seguente pacchetto (Service Pack 11) nell’istanza Experience Manager 6.5.

   [Scarica l’Experience Manager 6.5.11.0](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.11.zip)

1. Contatto [!UICONTROL Assistenza clienti] per ottenere l’ID client e la chiave segreta per l’autenticazione Bearer dell’organizzazione IMS.

Di seguito sono riportate le configurazioni aggiuntive necessarie dopo la migrazione a Profili aziendali:

1. In entrata **[!UICONTROL Provider di configurazione IMS OAuth Adobe Granite]** (`com.adobe.granite.auth.ims.impl.ImsConfigProviderImpl`), imposta:

   * ID configurazione OAuth (`oauth.configmanager.ims.configid`): `ims` (Verifica una volta; è possibile che sia già configurato)

   * Entità proprietaria IMS (`ims.owningEntity`): ID organizzazione IMS

   ![ID configurazione IMS](assets/bearer-authentication1.png)

1. Apri **[!UICONTROL Gestore autenticazione Bearer]** e aggiungere l&#39;ID client ottenuto da [!UICONTROL Assistenza clienti] all&#39;elenco di **[!UICONTROL ID client OAuth consentiti]**.

   ![Aggiungi ID client](assets/add-clientid-bearer-auth.png)

1. Apri **[!UICONTROL Applicazione e provider OAuth Adobe Granite]** e aggiungere la **[!UICONTROL ID client]** e **[!UICONTROL Segreto client]** (Chiave segreta) ottenuta dall’Assistenza clienti.

   Assicurati che **[!UICONTROL ID configurazione]** campo (`oauth.config.id`) contiene lo stesso valore fornito in **[!UICONTROL ID configurazione OAuth]** campo (`oauth.configmanager.ims.configid`).

   ![Verifica ID client](assets/clientid-secretkey.png)

1. Apri **[!UICONTROL Adobe di preprocessore token di Exchange per cluster Granite IMS]** e impostarla su `enable`.

## Gestire il controllo degli accessi utente {#user-access}

Questa sezione descrive come gestire gli utenti e il loro accesso all’archivio Experience Manager.

### Mappatura gruppo {#group-mapping}

La mappatura dei gruppi determina il modo in cui i gruppi in Experience Manager corrispondono ai gruppi in Adobe IMS. Svolge un ruolo importante nel modo in cui agli utenti Adobe Asset Link viene concessa l’autorizzazione per accedere a Experience Manager Assets.

Se utilizzato con Adobe Asset Link, Experience Manager delega le funzioni di gestione degli utenti ad Adobe IMS. Crea automaticamente utenti e gruppi che corrispondono a utenti e gruppi in Adobe IMS. Inoltre, sincronizza gli utenti, i gruppi e l’appartenenza ai gruppi in Experience Manager in modo che corrispondano a quelli in Adobe IMS.

Consideriamo ad esempio uno scenario in cui gli utenti Adobe Asset Link sono membri del gruppo Adobe IMS assetlink-users. In questo caso, viene creato un gruppo sincronizzato denominato assetlink-users nell’Experience Manager di quando un utente del gruppo Adobe IMS si connette a Adobe Asset Link per la prima volta. Ogni nuovo utente del gruppo Adobe IMS viene aggiunto al gruppo corrispondente nell’Experience Manager quando si connette a Experience Manager tramite Adobe Asset Link per la prima volta.

I gruppi in Experience Manager che corrispondono a e sono sincronizzati con i gruppi in Adobe IMS possono essere autorizzati ad accedere direttamente o rendendoli membri di un altro gruppo. Di seguito è riportato un esempio di come è possibile gestire le autorizzazioni.

![esempi di gruppi](assets/group-examples.png)

Le seguenti regole si applicano alle mappature dei gruppi in Experience Manager:

* Assicurati che **[!UICONTROL Mappature gruppo]** proprietà in **[!UICONTROL Provider IMS OAuth Adobe Granite]** La configurazione è vuota.
* Adobe L’iscrizione al gruppo di utenti di Asset Link viene valutata quando l’utente si autentica e il periodo di tempo in **[!UICONTROL Tempo di scadenza utente]** proprietà in **[!UICONTROL Gestore di sincronizzazione predefinito Apache Jackrabbit Oak]** la configurazione è trascorsa. Attualmente, gli utenti possono essere aggiunti e rimossi dai gruppi in Experience Manager per sincronizzarli con gli elementi presenti in Adobe IMS.
* Evitare conflitti di nomi di gruppo. Assicurati che i nomi utilizzati per i gruppi creati in Adobe IMS (per gestire gli utenti) siano diversi da tutti i nomi dei gruppi di Experienci Manager.

  Ad esempio, accertati che siano diversi da `dam-users` e i gruppi creati dall&#39;amministratore Experience Manager.

  Un gruppo Adobe IMS il cui nome è in conflitto con il nome di un gruppo Experience Manager o di un gruppo creato manualmente non viene utilizzato per controllare le autorizzazioni utente.
* Se un utente Adobe IMS si connette a un’istanza Experience Manager sulla quale il nome dell’utente è in conflitto con quello di un utente Experience Manager creato in precedenza, all’utente Adobe IMS viene assegnato un altro nome con l’aggiunta di numeri per renderlo univoco.

**Imposta controllo accesso per la prima volta**

Gli utenti che si connettono tramite Adobe Asset Link possono visualizzare e interagire con le risorse solo dopo aver ottenuto l’autorizzazione richiesta. Il [Mappatura gruppo](#group-mapping) La sezione precedente illustra come vengono creati i gruppi di utenti in Experience Manager, che corrispondono ai gruppi di utenti della tua organizzazione all’interno di Adobe IMS e con essi vengono sincronizzati. Si consiglia agli amministratori di Experience Manager di utilizzare questi gruppi per gestire il controllo degli accessi per gli utenti di Adobe Asset Link.

Per ogni gruppo di Experienci Manager sincronizzato con un gruppo Adobe IMS (utilizzato per gestire il controllo degli accessi utente):

1. Assicurati che il gruppo abbia un membro che possa essere utilizzato per una connessione iniziale da Adobe Asset Link.
1. Utilizza l’utente per accedere ad Adobe Asset Link e per connetterti ad Experience Manager. Connessione non riuscita.
1. Ad Experience Manager, individua il gruppo corrispondente in Adobe IMS e concedi al gruppo il controllo di accesso desiderato. Ad esempio, il nuovo gruppo diventa membro del gruppo dam-users.
1. Chiudi Adobe Asset Link e riavvia l’applicazione Creative Cloud.
1. Per verificare che l’utente disponga dell’accesso previsto, riapri Adobe Asset Link.

Una volta eseguiti questi passaggi, gli altri utenti dello stesso gruppo possono connettersi ad Experience Manager con Adobe Asset Link al primo tentativo. Dispone automaticamente delle stesse autorizzazioni degli altri utenti del gruppo.

## Gestisci gli utenti Experience Manager per Asset Link di Adobe {#manage-users}

Gli utenti Adobe Asset Link possono connettersi con Experience Manager quando hanno effettuato l’accesso alla propria applicazione Creative Cloud. Questa autenticazione utilizza la tecnologia Adobe IMS e, se non esiste, crea informazioni utente in Experience Manager. Ad Experience Manager, è comune per i clienti aziendali gestire i propri utenti con un provider di identità esterno integrato con Experience Manager. I provider di identità includono Adobe IMS e altri prodotti che utilizzano i protocolli SAML e LDAP. In alternativa, in Experience Manager è possibile creare e gestire localmente gli utenti.

Gli utenti che si connettono a Experience Manager da Adobe Asset Link non sono in conflitto con le informazioni utente esistenti memorizzate in Experience Manager dal precedente accesso diretto, se:

* Tutti i nomi utente utilizzati per l’accesso diretto a Experience Manager sono diversi dai nomi utente utilizzati in Adobe IMS per l’accesso Creative Cloud.
* Adobe IMS viene utilizzato come provider di identità per l’accesso diretto degli Experienci Manager.
* Gli utenti si connettono all’Experience Manager da Adobe Asset Link prima di accedere direttamente all’Experience Manager con lo stesso account.


D’altra parte, le informazioni utente create in seguito all’accesso diretto di Experience Manager devono essere aggiornate per funzionare con Adobe Asset Link, nei seguenti scenari:

* Lo stesso nome utente, ad esempio l’indirizzo e-mail dell’utente, viene utilizzato per entrambi: per l’account in Creative Cloud, che utilizza Adobe IMS, e per l’account in un provider di identità esterno diverso da Adobe IMS.
* Lo stesso nome utente viene utilizzato per entrambi, l’account in Creative Cloud e un account di Experience Manager locale.
* Gli account di Creative Cloud in Adobe IMS sono Federated ID, gestiti dallo stesso provider di identità esterno integrato con Experience Manager per l’accesso diretto.

Gli utenti creati tramite questi scenari non dispongono di una proprietà necessaria per gli utenti, che sono sincronizzati con Adobe IMS.

Per aggiornare tali utenti in Experience Manager e utilizzarli con Adobe Asset Link:

1. Nella console web di Experience Manager, individua **[!UICONTROL Configurazione entità esterna Apache Jackrabbit Oak]** e fai clic su per modificarla. Deseleziona il **[!UICONTROL Protezione identità esterna]** e fare clic su **[!UICONTROL Salva]**.
1. Per accedere all’interfaccia di User Management in Experience Manager, passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Sicurezza]** > **[!UICONTROL Utenti]**. Seleziona l’utente da aggiornare, quindi annota la fine del percorso URL del browser per tale utente, a partire da `/home/users`. In alternativa, è possibile cercare il nome utente in CRXDE. Esempio di percorso utente: `/home/users/x/xTac082TDh-guJzzG7WM`.
1. In CRXDE, accedi al percorso utente, seleziona il nodo utente e visualizza le proprietà del nodo selezionando la **[!UICONTROL Proprietà]** nell&#39;area centrale inferiore. Questo nodo ha `jcr:primaryType` valore proprietà di `rep:User`.
1. Nella parte inferiore della sezione **[!UICONTROL Proprietà]** , immettere un valore `Name` valore di `rep:externalId`, `Type` valore di `String`, e un `Value` valore di `rep:authorizableId`;`ims`, dove `rep:authorizableId` è il valore del `rep:authorizableId` del nodo. (Viene utilizzato un punto e virgola senza spazi per separare `rep:authorizableId` valore da `ims`.)
1. Fai clic su **[!UICONTROL Aggiungi]** a destra della nuova voce, quindi fare clic su **[!UICONTROL Salva tutto]**.
1. Ripeti i passaggi da 2 a 5 per tutti gli altri utenti che desideri aggiornare per lavorare con Adobe Asset Link.
1. Nella console web di Experience Manager, individua **[!UICONTROL Configurazione entità esterna Apache Jackrabbit Oak]** e fai clic su per modificarla. Deseleziona il **[!UICONTROL Protezione identità esterna]** e fare clic su **[!UICONTROL Salva]**.

>[!NOTE]
>
>Se i servizi non vengono ripristinati in pochi minuti, riavviare Experience Manager per consentire autenticazioni riuscite.

Dopo questa modifica, un utente Experience Manager aggiornato può connettersi con Adobe Asset Link e continuare a utilizzare il metodo di accesso diretto a Experience Manager utilizzato prima dell’aggiornamento. In caso di autenticazione con Adobe IMS, le informazioni sul profilo utente di Experience Manager vengono sincronizzate con il profilo utente in Adobe IMS.

Esiste un metodo che consente di eseguire una migrazione in blocco di più utenti Experienci Manager per consentire loro di lavorare con Adobe Asset Link. Per ulteriori informazioni e assistenza sull’abilitazione di questa opzione, contatta l’Assistenza Adobe.

In alternativa ai passaggi, in alcune circostanze a un utente di Adobe Asset Link può essere fornito un accesso rapido a Experience Manager. In questi casi, le informazioni utente preesistenti vengono trovate ed eliminate con Experience Manager User Management o Experience Manager CRXDE prima della loro connessione con Adobe Asset Link. Le nuove informazioni utente vengono create nell’Experience Manager successivo alla connessione. Utilizza questo approccio solo se sei certo che non sono presenti dati importanti aggiunti come elemento secondario del nodo utente. Tali dati aggiuntivi sono qualsiasi nodo figlio del nodo utente diverso da `tokens`, `preferences`, `profile`, `profiles`, `profiles/public`, e `rep:policy/*` nodi.

## Avvia automaticamente il flusso di lavoro per elaborare le risorse in modo condizionale {#auto-start-workflow}

Nell&#39;Experience Manager 6.4 e nell&#39;Experience Manager 6.5, gli amministratori possono configurare i flussi di lavoro per eseguire ed elaborare automaticamente le risorse in base a condizioni predefinite.

La configurazione è utile, ad esempio, per gli utenti e gli addetti al marketing della linea di business per creare un flusso di lavoro personalizzato in poche cartelle specifiche. Dì che tutte le risorse del servizio fotografico di un&#39;agenzia possono essere filigranate oppure tutte le risorse caricate da un freelance possono essere elaborate per creare rappresentazioni specifiche.

Per ulteriori informazioni e, ad Experience Manager, per la configurazione, vedi [esecuzione automatica del flusso di lavoro sulle risorse](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-workflow.html#auto-execute-workflow-on-some-assets).


## Creazione di un indice personalizzato nelle versioni Experience Manager 6.4.x {#create-custom-index}

L&#39;Experience Manager contiene gli indici utilizzati per l&#39;esecuzione di query. Crea il seguente indice personalizzato per la versione specificata. L&#39;Experience Manager 6.5.0 contiene questo indice per impostazione predefinita. Adobe Asset Link richiede questo indice per determinare quali risorse sono state estratte da un utente.

1. In CRXDE, individua `/oak:index` nodo. Crea un nodo denominato `cqDrivelock` e impostarne `Type` a `oak:QueryIndexDefinition`.

1. Aggiungi le seguenti proprietà al nuovo nodo e salva le modifiche:

   * `Name: type; Type: string; Value: property`

   * `Name: propertyNames; Type: Name[] (click the "Multi" button); Value: cq:drivelock`


## Configurare la ricerca visiva o per somiglianza {#configure-visual-similarity-search}

La funzionalità di ricerca visiva consente di cercare risorse visivamente simili nell’archivio AEM Assets, utilizzando il pannello Adobe Asset Link. La funzionalità è disponibile nella versione 6.5.0 o successive e vengono cercate solo le risorse indicizzate. Per ulteriori informazioni, consulta [come configurare la ricerca visiva](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/search-assets.html#configvisualsearch).

## Genera solo rappresentazioni per posizionamento per Adobe InDesign {#fpo-renditions}

In questo Experience Manager vengono fornite le rappresentazioni utilizzate solo per il posizionamento (FPO). Queste copie trasformate FPO hanno dimensioni di file ridotte ma hanno le stesse proporzioni. Se per una risorsa non è disponibile una rappresentazione FPO, Adobe InDesign utilizza la risorsa originale. Questo meccanismo di fallback assicura che il flusso di lavoro creativo proceda senza interruzioni. Per ulteriori informazioni, consulta [genera rappresentazioni FPO](/help/assets/configure-fpo-renditions.md).


## Integrare con Adobe Stock {#adobe-stock-integration}

Le organizzazioni integrano i propri account Adobe Stock con Experience Manager Assets. Aiuta gli esperti di marketing a rendere disponibili foto, vettori, illustrazioni, video, modelli e risorse 3D di alta qualità e senza royalty per i loro progetti creativi e di marketing. I creativi possono utilizzare queste risorse mediante il pannello Asset Link.

Per l’integrazione con Adobe Stock, consulta [Risorse Adobe Stock in Experience Manager Assets](/help/assets/aem-assets-adobe-stock.md). Per l’integrazione con Adobe Stock è richiesto l’Experience Manager 6.4.2 o successivo.


## Risolvere i problemi relativi agli Experienci Manager {#troubleshoot}


In caso di problemi durante la configurazione o l’utilizzo di Adobe Asset Link, prova quanto segue:

* Assicurati che l’implementazione soddisfi i prerequisiti. In particolare, assicurati che siano installati i pacchetti o i Feature Pack appropriati.
* Contatta il partner o l’integratore di sistemi della tua organizzazione.
* Se gli utenti Creative Cloud non sono in grado di verificare le risorse estratte, verifica la presenza di maiuscole/minuscole nei nomi di dominio negli ID e-mail. Per risolvere il problema, consulta [configurazione manuale](#manual-configuration).
* Per ulteriori informazioni, consulta [risolvere i problemi di Asset Link](https://helpx.adobe.com/enterprise/kb/asset-link-troubleshooting.html).


>[!MORELIKETHIS]
>
>* [Informazioni su Adobe Asset Link](https://helpx.adobe.com/it/enterprise/using/adobe-asset-link.html)
>* [Utilizzare Asset Link nell’app desktop Creative Cloud e gestire le risorse](https://helpx.adobe.com/it/enterprise/using/manage-assets-using-adobe-asset-link.html)
>* [Configurare Adobe Experience Manager Assets as a Cloud Service](https://helpx.adobe.com/it/enterprise/using/configure-aem-assets-for-asset-link.html).
