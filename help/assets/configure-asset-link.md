---
title: Configurare Experience Manager Assets per Adobe Asset Link
description: Configura Experience Manager Assets per l’utilizzo con l’estensione Adobe Asset Link per le applicazioni Creative Cloud.
contentOwner: Vishabh Gupta
role: Admin
feature: Asset Management
exl-id: 3a9b44d4-1756-4ad5-91df-df8d53e82193
solution: Experience Manager, Experience Manager Assets
source-git-commit: 6ab943894398733d178f561430d3f391e8722195
workflow-type: tm+mt
source-wordcount: '3059'
ht-degree: 0%

---

# Configurare Experience Manager Assets per Adobe Asset Link {#adobe-asset-link}

[Adobe Asset Link (AAL)](https://www.adobe.com/it/creativecloud/business/enterprise/adobe-asset-link.html) semplifica la collaborazione tra creativi ed esperti di marketing nel processo di creazione dei contenuti. Collega Adobe Experience Manager Assets con le app desktop Creative Cloud Adobe InDesign, Adobe Photoshop e Adobe Illustrator. Il pannello Adobe Asset Link consente ai creativi di accedere e modificare i contenuti memorizzati in AEM Assets senza uscire dalle app creative che preferiscono.

Per configurare Experience Manager Assets per l’utilizzo con Asset Link, implementa le seguenti attività. Utilizza l’account amministratore di Experience Manager per eseguire la configurazione:

1. Installa i pacchetti come richiesto. I dettagli sono inclusi in [prerequisiti](#prerequisites).

1. Configura Experience Manager [manualmente](#manual-configuration) o utilizzando un [pacchetto](#configure-using-package).

1. Per mappare gli utenti con licenza Creative Cloud con gli utenti Experience Manager, gestisci [il controllo dell&#39;accesso utente](#user-access).

1. Crea [indice di query personalizzato](#create-custom-index), configura [rappresentazioni FPO](/help/assets/configure-fpo-renditions.md) per InDesign, configura [integrazione Adobe Stock](/help/assets/aem-assets-adobe-stock.md) e configura [ricerca visiva o per similarità](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/search-assets.html?lang=it#configvisualsearch).

## Prerequisiti e supporto per varie funzionalità {#prerequisites}

Assicurarsi di installare il service pack e il pacchetto appropriati in base alle esigenze. Per ogni versione di Experience Manager e per le funzionalità specifiche, vedi i seguenti requisiti.

| Funzionalità Assets | Versione di Experience Manager e requisiti per il supporto |
|--- |--- |
| Asset Link funziona per impostazione predefinita | Experience Manager 6.5 e 6.5.2 o versioni successive. </br> Experience Manager 6.4.4 e 6.4.6 o versioni successive. </br> Adobe consiglia di installare l&#39;ultimo [Service Pack (SP) di Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=it) prima di utilizzare AAL. |
| Asset Link funziona dopo l’installazione di un pacchetto | Per Experience Manager 6.4.0 - 6.4.3, installa il pacchetto [adobe-asset-link-support](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/featurepack/adobe-asset-link-support). |
| Integrazione con Adobe Stock | Experience Manager 6.4.2 o versione successiva |
| Ricerca visiva o per affinità | Experience Manager 6.5.0 o versione successiva |


## Configurare Experience Manager utilizzando il pacchetto di configurazione {#configure-using-package}

Adobe consiglia di installare il pacchetto di configurazione [adobe-asset-link-config](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/product/assets/adobe-asset-link-config) per automatizzare la maggior parte delle attività di configurazione, seguito da alcune attività manuali. In alternativa, è possibile [configurare manualmente](#manual-configuration).

>[!CAUTION]
>
>Se l’istanza di Experience Manager è configurata per l’accesso utente con account Adobe IMS, non utilizzare il pacchetto di configurazione. Invece, [configura](#manual-configuration) manualmente l&#39;istanza di Experience Manager.

1. Per aprire Gestione pacchetti, nell&#39;interfaccia Web di Experience Manager, accedere a **[!UICONTROL Strumenti]** > **[!UICONTROL Distribuzione]** > **[!UICONTROL Condivisione pacchetti]**. Installa il pacchetto `adobe-asset-link-config`.

1. Accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Console Web]**. Individua la configurazione **[!UICONTROL del provider IMS OAuth Adobe Granite]** e fai clic su per modificarla.

   Imposta le seguenti proprietà e salva le modifiche.

   * [!UICONTROL Mappature gruppo]: lascia vuoto a meno che non lo desideri. Per ulteriori dettagli, vedere [Mappatura gruppo](#group-mapping).
   * [!UICONTROL Organizzazione]: immetti l&#39;ID organizzazione in uso in Adobe Admin Console. Per ulteriori informazioni sugli ID organizzazione, vedere [Crea gruppo utenti](https://helpx.adobe.com/it/enterprise/using/create-aal-user-group.html).

1. Individuare la configurazione **[!UICONTROL Adobe Granite Bearer Authentication Handler]** e fare clic per modificarla.

   Aggiungi **[!UICONTROL ID client InDesignAem2]** alla proprietà di configurazione **[!UICONTROL ID client OAuth consentiti]**.


## Configurare manualmente Experience Manager {#manual-configuration}

Configura manualmente Experience Manager se scegli di non utilizzare un pacchetto di configurazione o se la tua implementazione di Experience Manager è configurata per supportare l’accesso degli utenti con gli account Adobe IMS.

Per configurare manualmente Experience Manager:

1. Per accedere alla gestione della configurazione, accedere a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Console Web]**. Seleziona **[!UICONTROL OSGi]** > **[!UICONTROL Configurazione]** dal menu nella parte superiore.

1. Individua la configurazione **[!UICONTROL Adobe Granite OAuth IMS Provider]** e fai clic per modificarla.

   Imposta la seguente configurazione e fai clic su **[!UICONTROL Salva]**.

   * [!UICONTROL Endpoint autorizzazione]: ` https://ims-na1.adobelogin.com/ims/authorize/v1`
   * [!UICONTROL Endpoint token]: ` https://ims-na1.adobelogin.com/ims/token/v1`
   * [!UICONTROL Endpoint profilo]: ` https://ims-na1.adobelogin.com/ims/profile/v1`
   * [!UICONTROL URL di convalida]: ` https://ims-na1.adobelogin.com/ims/validate_token/v1`
   * [!UICONTROL Organizzazione]: impostato sull&#39;ID organizzazione in [Adobe Admin Console](https://adminconsole.adobe.com/).
   * [!UICONTROL Mappature gruppo]: lascia vuoto a meno che tu non abbia un caso speciale. Per ulteriori dettagli, vedere [Mappatura gruppo](#group-mapping).

1. Individuare la configurazione **[!UICONTROL Adobe Granite Bearer Authentication Handler]** e fare clic per modificarla.

   Aggiungi i seguenti ID client alla proprietà di configurazione **[!UICONTROL ID client OAuth consentiti]**: `InDesignAem2, cc-europa-desktop_0_1, cc-europa-desktop_1_0, cc-europa-desktop_2_0, cc-europa-desktop_3_0, cc-europa-desktop_4_0, cc-europa-desktop_5_0, cc-europa-desktop_6_0, cc-europa-desktop_7_0, cc-europa-desktop_8_0, cc-europa-desktop_9_0, and cc-europa-desktop_10_0`.

   Per aggiungere ogni `Client ID`, fare clic su `+`. Fai clic su **[!UICONTROL Salva]** dopo aver aggiunto tutti gli ID.

1. Nella configurazione dell&#39;applicazione e del provider OAuth **[!UICONTROL Adobe Granite]**, esaminare le istanze esistenti dell&#39;**[!UICONTROL applicazione e del provider OAuth Adobe Granite]**. Se si individua un&#39;istanza con il valore `Config ID` di `ims`, utilizzarla per le istruzioni della procedura. In caso contrario, fare clic su `+` per creare un&#39;istanza di configurazione. Imposta i seguenti valori di proprietà e fai clic su **[!UICONTROL Salva]**.

   * [!UICONTROL ID client]: non modificare
   * [!UICONTROL Segreto client]: non modificare
   * [!UICONTROL ID configurazione]: ` ims`
   * [!UICONTROL Ambito]: `AdobeID, OpenID, read_organizations` (nella configurazione possono essere presenti anche altri valori)
   * [!UICONTROL ID provider]: ` ims`
   * [!UICONTROL Crea utenti]: ` Checked`
   * [!UICONTROL Proprietà ID utente]: `Email` per la configurazione appena creata. In caso contrario, non modificare.

1. Individua la configurazione del **[!UICONTROL gestore di sincronizzazione predefinito di Apache Jackrabbit Oak]** con il **[!UICONTROL nome gestore di sincronizzazione]** `ims` e fai clic per modificarla.

   Imposta le seguenti proprietà di configurazione e fai clic su **[!UICONTROL Salva]**.

   * [!UICONTROL Scadenza utente e scadenza appartenenza utente]: dopo &#39;m&#39; in minuti non è disponibile spazio. `15m` per 15 minuti. Per ulteriori dettagli, vedere [Mappatura gruppo](#group-mapping).
   * [!UICONTROL Iscrizione automatica utente]: non modificare
   * [!UICONTROL Appartenenza dinamica utente]: ` Deslect`

1. Individua la configurazione **[!UICONTROL Adobe Granite OAuth Authentication Handler]** e fai clic per modificarla. Senza apportare modifiche, fai clic su **[!UICONTROL Salva]**.

1. Per regolare la priorità relativa del gestore di autenticazione Bearer, in CRXDE, passare a `/apps/system/config`. Individuare `com.adobe.granite.auth.oauth.impl.BearerAuthenticationHandler.config` e aprirne la configurazione. Alla fine, aggiungi `service.ranking=I"-10"`. Salva le modifiche.

   >[!NOTE]
   >
   >Ogni richiesta autenticata con un token Bearer comporta il sovraccarico di tre chiamate ad Adobe IMS, la sincronizzazione degli utenti e la creazione di un token di accesso in Experience Manager. Per ovviare a questo sovraccarico, Adobe Asset Link acquisisce il token di accesso restituito nella risposta di Experience Manager e lo invia con le richieste successive. Affinché questo processo funzioni, è necessario regolare la priorità relativa del gestore di autenticazione Bearer.

1. (Facoltativo) Se gli utenti di Experience Manager hanno nomi di dominio con lettere maiuscole o minuscole nei loro ID e-mail, seleziona **[!UICONTROL Cambia l&#39;utente con il blocco in minuscole]** in **[!UICONTROL Configurazioni piattaforma ACP Adobe Granite]** nella console Web Experience Manager.

## Configurazione aggiuntiva dopo la migrazione ai profili aziendali {#configure-migration-activity}

Gli utenti di Adobe Asset Link possono connettersi ad Experience Manager per consentire l’accesso IMS dall’organizzazione principale Creative Cloud for Enterprise (CCE). Experience Manager utilizza gli ID client per identificare l’organizzazione IMS consentita. Dopo la migrazione ai profili aziendali, è necessario configurare l’ID client e la chiave segreta per l’organizzazione IMS in Experience Manager per il gestore di autenticazione Bearer. Per ulteriori informazioni sui profili aziendali, vedere [introduzione ai profili Adobe](https://helpx.adobe.com/it/enterprise/kb/introducing-adobe-profiles.html).

È necessaria una configurazione aggiuntiva solo se per Experience Manager e Creative Cloud for Enterprise (CCE) utilizzi diverse organizzazioni Adobe IMS e se viene stabilita una relazione di trust tra domini tra queste due organizzazioni.

>[!NOTE]
>
>* La correzione per i profili aziendali è fornita in Experience Manager 6.5.11.0.
>* La configurazione esistente continua a funzionare se utilizzi la stessa organizzazione Adobe IMS con Experience Manager e CCE.


**Prerequisiti**

1. Istanza Experience Manager in esecuzione con autenticazione Bearer configurata per AAL.
1. Installa il seguente pacchetto (Service Pack 11) nell’istanza di Experience Manager 6.5.

   [Scarica Experience Manager 6.5.11.0](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.11.zip)

1. Contatta l&#39;[!UICONTROL Assistenza clienti] per ottenere l&#39;ID client e la chiave segreta per l&#39;autenticazione Bearer dell&#39;organizzazione IMS.

Di seguito sono riportate le configurazioni aggiuntive necessarie dopo la migrazione a Profili aziendali:

1. In **[!UICONTROL Provider configurazione IMS OAuth Adobe Granite]** (`com.adobe.granite.auth.ims.impl.ImsConfigProviderImpl`), impostare:

   * ID configurazione OAuth (`oauth.configmanager.ims.configid`): `ims` (verificare una volta, è possibile che sia già configurato)

   * Entità proprietaria IMS (`ims.owningEntity`): ID organizzazione IMS

   ![ID configurazione IMS](assets/bearer-authentication1.png)

1. Apri la configurazione di **[!UICONTROL Bearer Authentication Handler]** e aggiungi l&#39;ID client ottenuto da [!UICONTROL Assistenza clienti] all&#39;elenco di **[!UICONTROL ID client OAuth consentiti]**.

   ![Aggiungi ID client](assets/add-clientid-bearer-auth.png)

1. Apri la configurazione dell&#39;applicazione e del provider OAuth **[!UICONTROL Adobe Granite]** e aggiungi **[!UICONTROL ID client]** e **[!UICONTROL Segreto client]** (chiave segreta) ottenuti dall&#39;Assistenza clienti.

   Assicurati che il campo **[!UICONTROL ID configurazione]** (`oauth.config.id`) contenga lo stesso valore fornito nel campo **[!UICONTROL ID configurazione OAuth]** (`oauth.configmanager.ims.configid`) sopra.

   ![Verifica ID client](assets/clientid-secretkey.png)

1. Apri la configurazione di **[!UICONTROL Adobe Granite IMS Cluster Exchange Token Preprocessor]** e impostala su `enable`.

## Gestire il controllo degli accessi utente {#user-access}

Questa sezione descrive come gestire gli utenti e il loro accesso all’archivio Experience Manager.

### Mappatura gruppo {#group-mapping}

La mappatura dei gruppi determina il modo in cui i gruppi in Experience Manager corrispondono ai gruppi in Adobe IMS. Svolge un ruolo importante nel modo in cui agli utenti di Adobe Asset Link viene concessa l’autorizzazione per accedere a Experience Manager Assets.

Se utilizzata con Adobe Asset Link, Experience Manager delega le funzioni di gestione degli utenti ad Adobe IMS. Crea automaticamente utenti e gruppi che corrispondono a utenti e gruppi in Adobe IMS. Inoltre, sincronizza utenti, gruppi e appartenenze a gruppi in Experience Manager in modo che corrispondano a quelli di Adobe IMS.

Consideriamo ad esempio uno scenario in cui gli utenti di Adobe Asset Link sono membri del gruppo Adobe IMS assetlink-users. In questo caso, viene creato in Experience Manager un gruppo sincronizzato denominato assetlink-users quando un utente del gruppo Adobe IMS si connette per la prima volta ad Adobe Asset Link. Ogni nuovo utente del gruppo Adobe IMS viene aggiunto al gruppo corrispondente in Experience Manager quando si connette ad Experience Manager tramite Adobe Asset Link per la prima volta.

I gruppi in Experience Manager che corrispondono a e sono sincronizzati con i gruppi in Adobe IMS possono essere autorizzati ad accedere direttamente o rendendoli membri di un altro gruppo. Di seguito è riportato un esempio di come è possibile gestire le autorizzazioni.

![esempi di gruppi](assets/group-examples.png)

Le seguenti regole si applicano alle mappature dei gruppi in Experience Manager:

* Verificare che la proprietà **[!UICONTROL Group Mappings]** nella configurazione **[!UICONTROL Adobe Granite OAuth IMS Provider]** sia vuota.
* L&#39;appartenenza al gruppo utenti di Adobe Asset Link viene valutata quando l&#39;utente si autentica e il periodo di tempo nella proprietà **[!UICONTROL Data di scadenza utente]** nella configurazione **[!UICONTROL Apache Jackrabbit Oak Default Sync Handler]** è trascorso. Al momento, gli utenti possono essere aggiunti e rimossi dai gruppi in Experience Manager per sincronizzarli con gli elementi presenti in Adobe IMS.
* Evitare conflitti di nomi di gruppo. Assicurati che i nomi utilizzati per i gruppi creati in Adobe IMS (per gestire gli utenti) siano diversi da tutti i nomi dei gruppi di sistemi di Experience Manager.

  Assicurarsi, ad esempio, che siano diversi dal gruppo `dam-users` e dai gruppi creati dall&#39;amministratore Experience Manager.

  Un gruppo Adobe IMS il cui nome è in conflitto con il nome di un gruppo di sistema Experience Manager o di un gruppo creato manualmente non viene utilizzato per controllare le autorizzazioni utente.
* Se un utente Adobe IMS si connette a un’istanza di Experience Manager sulla quale il nome dell’utente è in conflitto con quello di un utente Experience Manager creato in precedenza, all’utente viene assegnato un altro nome con l’aggiunta di numeri per renderlo univoco.

**Imposta il controllo del primo accesso**

Gli utenti che si connettono tramite Adobe Asset Link possono visualizzare e interagire con le risorse solo dopo aver ottenuto l’autorizzazione richiesta. La sezione [Mappatura gruppo](#group-mapping) precedente illustra come vengono creati i gruppi di utenti in Experience Manager, che corrispondono ai gruppi di utenti della tua organizzazione all&#39;interno di Adobe IMS e con essi vengono sincronizzati. Si consiglia agli amministratori di Experience Manager di utilizzare questi gruppi per gestire il controllo degli accessi per gli utenti di Adobe Asset Link.

Per ogni gruppo Experience Manager sincronizzato con un gruppo Adobe IMS (utilizzato per gestire il controllo degli accessi utente):

1. Assicurati che il gruppo disponga di un membro che possa essere utilizzato per una connessione iniziale da Adobe Asset Link.
1. Utilizza tale utente per accedere ad Adobe Asset Link e per connettersi ad Experience Manager. Connessione non riuscita.
1. In Experience Manager, individua il gruppo corrispondente in Adobe IMS e concedi al gruppo il controllo di accesso desiderato. Ad esempio, il nuovo gruppo diventa membro del gruppo dam-users.
1. Chiudi Adobe Asset Link e riavvia l’applicazione Creative Cloud.
1. Per verificare che l’utente disponga dell’accesso previsto, riapri Adobe Asset Link.

Una volta eseguiti questi passaggi, gli altri utenti dello stesso gruppo possono connettersi ad Experience Manager con Adobe Asset Link al primo tentativo. Dispone automaticamente delle stesse autorizzazioni degli altri utenti del gruppo.

## Gestire gli utenti di Experience Manager per Adobe Asset Link {#manage-users}

Gli utenti di Adobe Asset Link possono connettersi con Experience Manager quando hanno effettuato l’accesso alla propria applicazione Creative Cloud. Questa autenticazione utilizza la tecnologia Adobe IMS e, se non esiste, crea le informazioni utente in Experience Manager. I clienti aziendali di Experience Manager possono gestire i propri utenti tramite un provider di identità esterno integrato con Experience Manager. I provider di identità includono Adobe IMS e altri prodotti che utilizzano i protocolli SAML e LDAP. In alternativa, gli utenti possono essere creati e gestiti localmente in Experience Manager.

Gli utenti che si connettono ad Experience Manager da Adobe Asset Link non sono in conflitto con le informazioni utente esistenti memorizzate in Experience Manager dal precedente accesso diretto, se:

* Tutti i nomi utente utilizzati per l’accesso diretto ad Experience Manager sono diversi dai nomi utente utilizzati in Adobe IMS per l’accesso a Creative Cloud.
* Adobe IMS viene utilizzato come provider di identità per l’accesso diretto ad Experience Manager.
* Gli utenti si connettono ad Experience Manager da Adobe Asset Link prima di accedere direttamente ad Experience Manager con lo stesso account.


D’altra parte, le informazioni utente create in seguito all’accesso diretto ad Experience Manager devono essere aggiornate per funzionare con Adobe Asset Link, nei seguenti scenari:

* Lo stesso nome utente, ad esempio l’indirizzo e-mail dell’utente, viene utilizzato sia per l’account in Creative Cloud, che utilizza Adobe IMS, che per l’account in un provider di identità esterno diverso da Adobe IMS.
* Lo stesso nome utente viene utilizzato per entrambi: l’account in Creative Cloud e un account Experience Manager locale.
* Gli account Creative Cloud in Adobe IMS sono Federated ID, forniti dallo stesso provider di identità esterno integrato con Experience Manager per l’accesso diretto.

Gli utenti creati tramite questi scenari non dispongono di una proprietà necessaria per gli utenti, che sono sincronizzati con Adobe IMS.

Per aggiornare questi utenti in Experience Manager e lavorare con Adobe Asset Link:

1. Nella console Web Experience Manager, individua la configurazione **[!UICONTROL Apache Jackrabbit Oak External PrincipalConfiguration]** e fai clic per modificarla. Deselezionare la casella di controllo **[!UICONTROL Protezione identità esterna]** e fare clic su **[!UICONTROL Salva]**.
1. Per accedere all&#39;interfaccia di User Management in Experience Manager, passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Sicurezza]** > **[!UICONTROL Utenti]**. Selezionare l&#39;utente da aggiornare, quindi annotare la fine del percorso URL del browser per l&#39;utente, a partire da `/home/users`. In alternativa, è possibile cercare il nome utente in CRXDE. Percorso utente di esempio: `/home/users/x/xTac082TDh-guJzzG7WM`.
1. In CRXDE, passa al percorso utente, seleziona il nodo utente e visualizza le proprietà del nodo selezionando la scheda **[!UICONTROL Proprietà]** nell&#39;area centrale inferiore. Questo nodo ha un valore della proprietà `jcr:primaryType` di `rep:User`.
1. Nella parte inferiore della scheda **[!UICONTROL Proprietà]** immettere un valore `Name` di `rep:externalId`, un valore `Type` di `String` e un valore `Value` di `rep:authorizableId`;`ims`, dove `rep:authorizableId` è il valore della proprietà `rep:authorizableId` del nodo. (Viene utilizzato un punto e virgola senza spazi per separare il valore `rep:authorizableId` da `ims`.)
1. Fai clic sul pulsante **[!UICONTROL Aggiungi]** a destra della nuova voce, quindi fai clic su **[!UICONTROL Salva tutto]**.
1. Ripeti i passaggi da 2 a 5 per tutti gli altri utenti che desideri aggiornare per lavorare con Adobe Asset Link.
1. Nella console Web Experience Manager, individua la configurazione **[!UICONTROL Apache Jackrabbit Oak External PrincipalConfiguration]** e fai clic per modificarla. Deselezionare la casella di controllo **[!UICONTROL Protezione identità esterna]** e fare clic su **[!UICONTROL Salva]**.

>[!NOTE]
>
>Se i servizi non vengono ripristinati in pochi minuti, riavvia Experience Manager per consentire le autenticazioni riuscite.

Dopo questa modifica, un utente Experience Manager aggiornato può connettersi con Adobe Asset Link e continuare a utilizzare il metodo di accesso diretto ad Experience Manager utilizzato prima dell’aggiornamento. In caso di autenticazione con Adobe IMS, le informazioni del profilo utente di Experience Manager vengono sincronizzate con il profilo utente in Adobe IMS.

Esiste un metodo che consente di eseguire una migrazione in blocco di più utenti di Experience Manager per consentire loro di lavorare con Adobe Asset Link. Per ulteriori informazioni e assistenza sull’abilitazione di questa opzione, contatta l’Assistenza Adobe.

In alternativa alla procedura, in alcune circostanze a un utente di Adobe Asset Link può essere fornito un accesso rapido ad Experience Manager. In questi casi, le informazioni utente preesistenti vengono trovate ed eliminate con Experience Manager User Management o Experience Manager CRXDE prima della loro connessione ad Adobe Asset Link. In Experience Manager vengono create nuove informazioni utente dopo la connessione. Utilizza questo approccio solo se sei certo che non sono presenti dati importanti aggiunti come elemento secondario del nodo utente. Tali dati aggiuntivi sono qualsiasi nodo figlio del nodo utente diverso dai nodi `tokens`, `preferences`, `profile`, `profiles`, `profiles/public` e `rep:policy/*`.

## Avvia automaticamente il flusso di lavoro per elaborare le risorse in modo condizionale {#auto-start-workflow}

In Experience Manager 6.4 e Experience Manager 6.5, gli amministratori possono configurare i flussi di lavoro per eseguire ed elaborare automaticamente le risorse in base a condizioni predefinite.

La configurazione è utile, ad esempio, per gli utenti e gli addetti al marketing della linea di business per creare un flusso di lavoro personalizzato in poche cartelle specifiche. Dì che tutte le risorse del servizio fotografico di un&#39;agenzia possono essere filigranate oppure tutte le risorse caricate da un freelance possono essere elaborate per creare rappresentazioni specifiche.

Per ulteriori informazioni e per la configurazione di Experience Manager, consulta [flusso di lavoro di esecuzione automatica sulle risorse](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-workflow.html?lang=it#auto-execute-workflow-on-some-assets).


## Creare un indice personalizzato nelle versioni Experience Manager 6.4.x {#create-custom-index}

Experience Manager contiene indici utilizzati per l’esecuzione di query. Crea il seguente indice personalizzato per la versione specificata. Per impostazione predefinita, Experience Manager 6.5.0 contiene questo indice. Adobe Asset Link richiede questo indice per determinare quali risorse sono state estratte da un utente.

1. In CRXDE, individua il nodo `/oak:index`. Creare un nodo denominato `cqDrivelock` e impostarne `Type` su `oak:QueryIndexDefinition`.

1. Aggiungi le seguenti proprietà al nuovo nodo e salva le modifiche:

   * `Name: type; Type: string; Value: property`

   * `Name: propertyNames; Type: Name[] (click the "Multi" button); Value: cq:drivelock`


## Configurare la ricerca visiva o per somiglianza {#configure-visual-similarity-search}

La funzionalità di ricerca visiva consente di cercare risorse visivamente simili nell’archivio AEM Assets, utilizzando il pannello Adobe Asset Link. La funzionalità è disponibile nella versione 6.5.0 o successive e vengono cercate solo le risorse indicizzate. Per ulteriori informazioni, vedere [come configurare la ricerca visiva](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/search-assets.html?lang=it#configvisualsearch).

## Genera solo rappresentazioni per posizionamento per Adobe InDesign {#fpo-renditions}

Experience Manager fornisce rappresentazioni utilizzate solo per il posizionamento (FPO). Queste copie trasformate FPO hanno dimensioni di file ridotte ma hanno le stesse proporzioni. Se per una risorsa non è disponibile una rappresentazione FPO, Adobe InDesign utilizza la risorsa originale. Questo meccanismo di fallback assicura che il flusso di lavoro creativo proceda senza interruzioni. Per ulteriori informazioni, vedere [generare copie trasformate dell&#39;oggetto Criteri di gruppo](/help/assets/configure-fpo-renditions.md).


## Integrare con Adobe Stock {#adobe-stock-integration}

Le organizzazioni integrano i propri account Adobe Stock con Experience Manager Assets. Aiuta gli esperti di marketing a rendere disponibili foto, vettori, illustrazioni, video, modelli e risorse 3D di alta qualità e senza royalty per i loro progetti creativi e di marketing. I creativi possono utilizzare queste risorse mediante il pannello Asset Link.

Per l&#39;integrazione con Adobe Stock, vedi [Risorse Adobe Stock in Experience Manager Assets](/help/assets/aem-assets-adobe-stock.md). Per l’integrazione con Adobe Stock è richiesto Experience Manager 6.4.2 o versione successiva.


## Risolvere i problemi relativi ad Experience Manager {#troubleshoot}


In caso di problemi durante la configurazione o l’utilizzo di Adobe Asset Link, prova quanto segue:

* Assicurati che l’implementazione soddisfi i prerequisiti. In particolare, assicurati che siano installati i pacchetti o i Feature Pack appropriati.
* Contatta il partner o l’integratore di sistemi della tua organizzazione.
* Se gli utenti di Creative Cloud non sono in grado di verificare le risorse estratte, verifica la presenza di maiuscole/minuscole nei nomi di dominio negli ID e-mail. Per risolvere il problema, vedere [configurazione manuale](#manual-configuration).
* Per ulteriori informazioni, consulta [risolvere i problemi di Asset Link](https://helpx.adobe.com/it/enterprise/kb/asset-link-troubleshooting.html).


>[!MORELIKETHIS]
>
>* [Informazioni su Adobe Asset Link](https://helpx.adobe.com/it/enterprise/using/adobe-asset-link.html)
>* [Utilizzare Asset Link nell&#39;app desktop Creative Cloud e gestire le risorse](https://helpx.adobe.com/it/enterprise/using/manage-assets-using-adobe-asset-link.html)
>* [Configura Adobe Experience Manager Assets as a Cloud Service](https://helpx.adobe.com/it/enterprise/using/configure-aem-assets-for-asset-link.html).
