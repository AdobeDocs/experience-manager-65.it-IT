---
title: Configurare Experience Manager Assets per Adobe Asset Link
description: Configura Experience Manager Assets da utilizzare con l’estensione Adobe Asset Link per le applicazioni Creative Cloud.
contentOwner: Vishabh Gupta
role: Admin
feature: Asset Management
exl-id: 3a9b44d4-1756-4ad5-91df-df8d53e82193
source-git-commit: 84b16dd1a60f731b568dd87ef89699875cb86596
workflow-type: tm+mt
source-wordcount: '3149'
ht-degree: 1%

---

# Configurare Experience Manager Assets per Adobe Asset Link {#adobe-asset-link}

[Adobe Asset Link (AAL)](https://www.adobe.com/it/creativecloud/business/enterprise/adobe-asset-link.html) semplifica la collaborazione tra creativi e addetti al marketing nel processo di creazione dei contenuti. Collega Adobe Experience Manager Assets alle app desktop Creative Cloud Adobe InDesign, Adobe Photoshop e Adobe Illustrator. Il pannello Adobe Asset Link consente ai creativi di accedere e modificare i contenuti archiviati in AEM Assets senza lasciare le app creative con cui hanno più familiarità.

Per configurare Experience Manager Assets da utilizzare con Asset Link, implementa le seguenti attività. Utilizza l’account amministratore di Experience Manager per eseguire la configurazione:

1. Installa i pacchetti come necessario. Dettagli in [prerequisiti](#prerequisites).

1. Configura Experience Manager [manuale](#manual-configuration) o utilizzando [pacchetto](#configure-using-package).

1. Per mappare gli utenti con licenza di Creative Cloud con gli utenti di Experience Manager, gestisci [controllo accesso utente](#user-access).

1. Crea [indice di query personalizzato](#create-custom-index), configura [Rendering FPO](/help/assets/configure-fpo-renditions.md) per InDesign, configura [Integrazione Adobe Stock](/help/assets/aem-assets-adobe-stock.md)e configura [ricerca visiva o per similarità](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/search-assets.html#configvisualsearch).

## Prerequisiti e supporto per varie funzionalità {#prerequisites}

Se necessario, assicurati di installare il service pack e il pacchetto appropriati. Per ogni versione di Experience Manager e per funzionalità specifiche, consulta i seguenti requisiti.

| Funzionalità Assets | Versione di Experience Manager e requisiti per il supporto |
|--- |--- |
| Asset Link funziona per impostazione predefinita | Experience Manager 6.5 e 6.5.2 o successivo. </br> Experience Manager 6.4.4 e 6.4.6 o successivo. </br> Adobe consiglia di installare l&#39;ultima [Service Pack di Experience Manager (SP)](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=it) prima di utilizzare AAL. |
| Asset Link funziona dopo l’installazione di un pacchetto | Per Experience Manager 6.4.0 - 6.4.3, installa [supporto adobe-asset-link](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/featurepack/adobe-asset-link-support) pacchetto. |
| Integrazione di Adobe Stock | Experience Manager 6.4.2 o successivo |
| Ricerca visiva o per similarità | Experience Manager 6.5.0 o successivo |


## Configurare l’Experience Manager utilizzando il pacchetto di configurazione {#configure-using-package}

Adobe consiglia di installare [adobe-asset-link-config](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/product/assets/adobe-asset-link-config) pacchetto di configurazione per automatizzare la maggior parte delle attività di configurazione, seguito da alcune attività manuali. In alternativa, è possibile [configurare manualmente](#manual-configuration).

>[!CAUTION]
>
>Se l’istanza di Experience Manager è configurata per l’accesso dell’utente con gli account Adobe IMS, non utilizzare il pacchetto di configurazione. Invece, [configurare manualmente](#manual-configuration) l’istanza di Experience Manager.

1. Per aprire Gestione pacchetti, nell’interfaccia Web di Experience Manager, accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Distribuzione]** > **[!UICONTROL Condivisione pacchetti]**. Installa `adobe-asset-link-config` pacchetto.

1. Accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > Console Web. **** Individua **[!UICONTROL Provider IMS OAuth di Adobe Granite]** e fai clic su per modificarlo.

   Imposta le seguenti proprietà e salva le modifiche.

   * [!UICONTROL Mappature dei gruppi]: Lascia vuoto a meno che non desideri. Per maggiori dettagli, vedi [Mappatura del gruppo](#group-mapping).
   * [!UICONTROL Organizzazione]: Immetti l&#39;ID organizzazione che utilizzi in Adobe Admin Console. Per ulteriori informazioni sugli ID organizzazione, vedi [Crea gruppo di utenti](https://helpx.adobe.com/enterprise/using/create-aal-user-group.html).

1. Individua **[!UICONTROL Gestore autenticazione portatore di Adobe Granite]** e fai clic su per modificarlo.

   Aggiungi **[!UICONTROL InDesignAem2]** ID client per **[!UICONTROL ID client OAuth consentiti]** proprietà di configurazione.


## Configurare manualmente Experience Manager {#manual-configuration}

Configura manualmente Experience Manager se scegli di non utilizzare un pacchetto di configurazione o se la distribuzione di Experience Manager è configurata per supportare l’accesso degli utenti con gli account Adobe IMS.

Per configurare manualmente l’Experience Manager:

1. Per accedere alla gestione della configurazione, accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Console web]**. Seleziona **[!UICONTROL OSGi]** > **[!UICONTROL Configurazione]** dal menu in alto.

1. Individua il **[!UICONTROL Provider IMS OAuth di Adobe Granite]** e fai clic su per modificarlo.

   Imposta la configurazione seguente e fai clic su **[!UICONTROL Salva]**.

   * [!UICONTROL Endpoint autorizzazione]: ` https://ims-na1.adobelogin.com/ims/authorize/v1`
   * [!UICONTROL Endpoint token]: ` https://ims-na1.adobelogin.com/ims/token/v1`
   * [!UICONTROL Endpoint profilo]: ` https://ims-na1.adobelogin.com/ims/profile/v1`
   * [!UICONTROL URL convalida]: ` https://ims-na1.adobelogin.com/ims/validate_token/v1`
   * [!UICONTROL Organizzazione]: Imposta l&#39;ID organizzazione in [Adobe Admin Console](https://adminconsole.adobe.com/).
   * [!UICONTROL Mappature dei gruppi]: Lasciare vuoto a meno che non si disponga di un caso speciale. Per maggiori dettagli, vedi [Mappatura del gruppo](#group-mapping).

1. Individua **[!UICONTROL Gestore autenticazione portatore di Adobe Granite]** e fai clic su per modificarlo.

   Aggiungi i seguenti ID client a **[!UICONTROL ID client OAuth consentiti]** proprietà di configurazione: `InDesignAem2, cc-europa-desktop_0_1, cc-europa-desktop_1_0, cc-europa-desktop_2_0, cc-europa-desktop_3_0, cc-europa-desktop_4_0, cc-europa-desktop_5_0, cc-europa-desktop_6_0, cc-europa-desktop_7_0, cc-europa-desktop_8_0, cc-europa-desktop_9_0, and cc-europa-desktop_10_0`.

   Per aggiungere `Client ID`, fai clic su `+`. Fai clic su **[!UICONTROL Salva]** dopo aver aggiunto tutti gli ID.

1. In **[!UICONTROL Applicazione e provider OAuth di Adobe Granite]** configurazione, ispezionare l&#39;esistente **[!UICONTROL Gestore autenticazione OAuth di Adobe Granite]** istanze. Se individua un&#39;istanza con il `Config ID` valore `ims`, utilizzalo per le istruzioni contenute in questa procedura. In caso contrario, fai clic su `+` per creare un&#39;istanza di configurazione. Imposta i seguenti valori di proprietà e fai clic su **[!UICONTROL Salva]**.

   * [!UICONTROL ID client]: Non modificare
   * [!UICONTROL Segreto client]: Non modificare
   * [!UICONTROL ID configurazione]: ` ims`
   * [!UICONTROL Ambito]: `AdobeID, OpenID, read_organizations` (nella configurazione possono essere presenti anche altri valori)
   * [!UICONTROL ID fornitore]: ` ims`
   * [!UICONTROL Creare utenti]: ` Checked`
   * [!UICONTROL Proprietà ID utente]: `Email` per la configurazione appena creata. In caso contrario, non modificare.

1. Individua il **[!UICONTROL Apache Jackrabbit Oak Default Sync Handler]** con la **[!UICONTROL Nome del gestore di sincronizzazione]** `ims` e fai clic su per modificarlo.

   Imposta le seguenti proprietà di configurazione e fai clic su **[!UICONTROL Salva]**.

   * [!UICONTROL Scadenza utente e scadenza iscrizione utente]: Tempo in minuti dopo &quot;m&quot; senza spazio. Ad esempio: `15m` per 15 minuti. Per maggiori dettagli, vedi [Mappatura del gruppo](#group-mapping).
   * [!UICONTROL Iscrizione automatica utente]: Non modificare
   * [!UICONTROL Iscrizione dinamica utente]: ` Deslect`

1. Individua il **[!UICONTROL Gestore autenticazione OAuth di Adobe Granite]** e fai clic su per modificarlo. Senza apportare modifiche, fai clic su **[!UICONTROL Salva]**.

1. Per regolare la priorità relativa del gestore di autenticazione portatore, in CRXDE, passa a `/apps/system/config`. Individua `com.adobe.granite.auth.oauth.impl.BearerAuthenticationHandler.config` e apri la relativa configurazione. Alla fine, aggiungi `service.ranking=I"-10"`. Salva le modifiche.

   >[!NOTE]
   >
   >Ogni richiesta autenticata con un token portatore gestisce il sovraccarico di tre chiamate ad Adobe IMS, la sincronizzazione degli utenti e la creazione di un token di accesso in Experience Manager. Per superare questo sovraccarico, Adobe Asset Link acquisisce il token di accesso restituito nella risposta da Experience Manager e lo invia con le richieste successive. Affinché questo processo funzioni, è necessario regolare la priorità relativa del gestore di autenticazione portatore.

1. (Facoltativo) Se gli utenti di Experience Manager hanno nomi di dominio maiuscoli o con maiuscole/minuscole nei loro ID e-mail, seleziona **[!UICONTROL Cambia il blocco utente in minuscolo]** in **[!UICONTROL Configurazioni della piattaforma Adobe Granite ACP]** in Experience Manager Web Console.

## Configurazione aggiuntiva dopo la migrazione a profili aziendali {#configure-migration-activity}

Gli utenti di Adobe Asset Link possono connettersi ad Experience Manager per consentire l’accesso IMS dalla Creative Cloud principale per l’organizzazione Enterprise (CCE). Experience Manager utilizza gli ID client per identificare l’organizzazione IMS consentita. Dopo la migrazione a profili aziendali, è necessario configurare l’ID client e la chiave segreta per l’organizzazione IMS nell’Experience Manager per il gestore di autenticazione al portatore. Per ulteriori informazioni sui profili aziendali, consulta [introduzione di profili di Adobe](https://helpx.adobe.com/enterprise/kb/introducing-adobe-profiles.html).

È necessaria un’ulteriore configurazione solo se utilizzi diverse organizzazioni Adobe IMS per Experience Manager e Creative Cloud per Enterprise (CCE) e tra queste due organizzazioni viene stabilita una relazione di trust tra domini.

>[!NOTE]
>
>* La correzione per i profili aziendali viene fornita in Experience Manager 6.5.11.0.
>* La configurazione esistente continua a funzionare se utilizzi la stessa organizzazione Adobe IMS con Experience Manager e CCE.



**Prerequisiti**

1. Un’istanza di Experience Manager funzionante con autenticazione portatore configurata per AAL.
1. Installa il seguente pacchetto (Service Pack 11) sull&#39;istanza Experience Manager 6.5.

   [Scarica Experience Manager 6.5.11.0](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.11.zip)

1. Contatto [!UICONTROL Assistenza clienti] per ottenere l’ID client e la chiave segreta per l’autenticazione al portatore della tua organizzazione IMS.

Di seguito sono riportate le configurazioni aggiuntive necessarie dopo la migrazione a profili aziendali:

1. In **[!UICONTROL Provider di configurazione IMS OAuth di Adobe Granite]** (`com.adobe.granite.auth.ims.impl.ImsConfigProviderImpl`), imposta:

   * ID configurazione OAuth (`oauth.configmanager.ims.configid`): `ims` (Verifica una volta, potrebbe essere già configurato)

   * Entità proprietaria IMS (`ims.owningEntity`): ID organizzazione IMS

   ![ID configurazione IMS](assets/bearer-authentication1.png)

1. Apri **[!UICONTROL Gestore autenticazione portatore]** configurazione e aggiunta dell’ID client ottenuto da [!UICONTROL Assistenza clienti] all&#39;elenco **[!UICONTROL ID client OAuth consentiti]**.

   ![Aggiungi ID client](assets/add-clientid-bearer-auth.png)

1. Apri **[!UICONTROL Applicazione e provider OAuth di Adobe Granite]** e aggiungi la **[!UICONTROL ID client]** e **[!UICONTROL Segreto client]** (Chiave segreta) ottenuta dall’Assistenza clienti.

   Assicurati che **[!UICONTROL ID configurazione]** campo (`oauth.config.id`) contiene lo stesso valore fornito in **[!UICONTROL ID configurazione OAuth]** campo (`oauth.configmanager.ims.configid`).

   ![Verifica ID client](assets/clientid-secretkey.png)

1. Apri **[!UICONTROL Adobe Granite IMS Cluster Exchange Token Preprocessor]** e impostalo su `enable`.

## Gestione del controllo degli accessi utente {#user-access}

Questa sezione descrive come gestire gli utenti e il loro accesso all’archivio Experience Manager.

### Mappatura del gruppo {#group-mapping}

La mappatura dei gruppi determina il modo in cui i gruppi in Experience Manager corrispondono ai gruppi in Adobe IMS. Questa funzione svolge un ruolo importante nel modo in cui gli utenti di Adobe Asset Link ricevono l’autorizzazione per accedere a Experience Manager Assets.

Se utilizzato con Adobe Asset Link, Experience Manager delega le funzioni di gestione degli utenti ad Adobe IMS. Crea automaticamente utenti e gruppi corrispondenti a utenti e gruppi in Adobe IMS. Inoltre, sincronizza utenti, gruppi e appartenenza al gruppo in Experience Manager in modo che corrispondano a quelli in Adobe IMS.

Ad esempio, considera uno scenario in cui gli utenti di Adobe Asset Link sono membri del gruppo Adobe IMS asset-link-users. In questo caso, un gruppo sincronizzato denominato utenti di risorse viene creato in Experience Manager quando un utente di quel gruppo Adobe IMS si connette ad Adobe Asset Link per la prima volta. Ogni nuovo utente del gruppo Adobe IMS viene aggiunto al gruppo corrispondente in Experience Manager quando si connette ad Experience Manager per la prima volta tramite Adobe Asset Link.

I gruppi in Experience Manager che corrispondono e sono sincronizzati con i gruppi in Adobe IMS possono avere accesso direttamente o facendo di loro un membro di un altro gruppo. Ecco un esempio di come è possibile gestire le autorizzazioni.

![esempi di gruppi](assets/group-examples.png)

Le seguenti regole si applicano alle mappature dei gruppi nell&#39;Experience Manager:

* Assicurati che **[!UICONTROL Mappature dei gruppi]** proprietà in **[!UICONTROL Provider IMS OAuth di Adobe Granite]** la configurazione è vuota.
* L’appartenenza al gruppo di utenti di Adobe Asset Link viene valutata al momento dell’autenticazione dell’utente e del periodo di tempo in **[!UICONTROL Ora di scadenza utente]** proprietà in **[!UICONTROL Apache Jackrabbit Oak Default Sync Handler]** la configurazione è scaduta. Attualmente, gli utenti possono essere aggiunti e rimossi dai gruppi in Experience Manager per eseguire la sincronizzazione con ciò che si trova in Adobe IMS.
* Evitare conflitti tra nomi di gruppo. Assicurati che i nomi utilizzati per i gruppi creati in Adobe IMS (per gestire gli utenti) siano diversi da tutti i nomi dei gruppi di sistema di Experience Manager.

   Ad esempio, assicurati che siano diversi dal `dam-users` e i gruppi creati dall&#39;amministratore di Experience Manager.

   Un gruppo Adobe IMS il cui nome è in conflitto con il nome di un gruppo di sistema di Experience Manager o di un gruppo creato manualmente non viene utilizzato per controllare le autorizzazioni utente.
* Se un utente Adobe IMS si connette a un’istanza di Experience Manager in cui il nome dell’utente è in conflitto con un utente di Experience Manager creato in precedenza, all’utente Adobe IMS viene assegnato un altro nome con dei numeri aggiunti per renderlo univoco.

**Impostazione del controllo di accesso per la prima volta**

Gli utenti che si connettono tramite Adobe Asset Link possono visualizzare e interagire solo con le risorse dopo aver ottenuto l’autorizzazione richiesta. La [Mappatura del gruppo](#group-mapping) la sezione precedente illustra come vengono creati in Experience Manager i gruppi di utenti che corrispondono e sono sincronizzati con i gruppi di utenti della tua organizzazione all’interno di Adobe IMS. È consigliabile che gli amministratori di Experience Manager utilizzino questi gruppi per gestire il controllo degli accessi per gli utenti di Adobe Asset Link.

Per ogni gruppo di Experienci Manager sincronizzato con un gruppo Adobe IMS (utilizzato per gestire il controllo degli accessi utente):

1. Assicurati che il gruppo disponga di un membro che possa essere utilizzato per una connessione iniziale da Adobe Asset Link.
1. Utilizza quell’utente per accedere ad Adobe Asset Link e connetterti ad Experience Manager. Si prevede che la connessione non riesca.
1. Ad Experience Manager, individua il gruppo corrispondente al gruppo in Adobe IMS e assegnagli il controllo di accesso desiderato. Ad esempio, il nuovo gruppo viene creato come membro del gruppo dam-users.
1. Chiudi Adobe Asset Link e riavvia l’applicazione Creative Cloud.
1. Per verificare che l’utente disponga dell’accesso previsto, riapri Adobe Asset Link.

Una volta eseguiti questi passaggi, gli altri utenti dello stesso gruppo possono connettersi ad Experience Manager con Adobe Asset Link al primo tentativo. Hanno automaticamente le stesse autorizzazioni degli altri utenti del gruppo.

## Gestione degli utenti di Experience Manager per Adobe Asset Link {#manage-users}

Gli utenti di Adobe Asset Link possono connettersi ad Experience Manager quando effettuano l’accesso alla propria applicazione Creative Cloud. Questa autenticazione utilizza la tecnologia Adobe IMS e crea informazioni utente in Experience Manager, se non esiste. È comune per i clienti aziendali di Experience Manager gestire i propri utenti con un provider di identità esterno integrato con Experience Manager. I provider di identità includono Adobe IMS e altri prodotti che utilizzano i protocolli SAML e LDAP. In alternativa, gli utenti possono essere creati e gestiti localmente in Experience Manager.

Gli utenti che si collegano ad Experience Manager da Adobe Asset Link non hanno alcun conflitto con le informazioni utente esistenti memorizzate in Experience Manager dal precedente accesso diretto, se:

* Tutti i nomi utente utilizzati per l’accesso diretto all’Experience Manager sono diversi dai nomi utente utilizzati in Adobe IMS per l’accesso Creative Cloud.
* Adobe IMS viene utilizzato come provider di identità per l’accesso diretto all’Experience Manager.
* Gli utenti si collegano ad Experience Manager da Adobe Asset Link prima di effettuare l’accesso diretto ad Experience Manager con lo stesso account.


D’altro canto, le informazioni utente create a seguito dell’accesso diretto ad Experience Manager devono essere aggiornate per funzionare con Adobe Asset Link, nei seguenti scenari:

* Lo stesso nome utente, ad esempio l’indirizzo e-mail dell’utente, viene utilizzato sia per l’account in Creative Cloud, che utilizza Adobe IMS, sia per l’account in un provider di identità esterno diverso da Adobe IMS.
* Lo stesso nome utente viene utilizzato per entrambi, l’account in Creative Cloud e un account di Experience Manager locale.
* Gli account Creative Cloud in Adobe IMS sono Federated ID, forniti dallo stesso provider di identità esterno integrato con Experience Manager per l’accesso diretto.

Gli utenti creati in questi scenari non dispongono di una proprietà necessaria per gli utenti, sincronizzata con Adobe IMS.

Per aggiornare tali utenti in Experience Manager in modo che funzionino con Adobe Asset Link:

1. Nella console Web di Experience Manager, individua **[!UICONTROL Configurazione principale esterna Apache Jackrabbit Oak]** e fai clic su per modificarlo. Deseleziona la **[!UICONTROL Protezione dell’identità esterna]** e fai clic su **[!UICONTROL Salva]**.
1. Per accedere all’interfaccia di gestione utente in Experience Manager, passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Sicurezza]** > **[!UICONTROL Utenti]**. Seleziona l’utente da aggiornare, quindi prendi nota della fine del percorso URL del browser per quell’utente, a partire da `/home/users`. In alternativa, puoi cercare il nome utente in CRXDE. Un percorso utente di esempio: `/home/users/x/xTac082TDh-guJzzG7WM`.
1. In CRXDE, accedi al percorso utente, seleziona il nodo utente e visualizza le proprietà del nodo selezionando il **[!UICONTROL Proprietà]** nell&#39;area in basso a metà. Questo nodo ha un `jcr:primaryType` valore di proprietà di `rep:User`.
1. Nella parte inferiore del **[!UICONTROL Proprietà]** area tabulazione, immettere un `Name` valore `rep:externalId`, `Type` valore `String`e `Value` valore `rep:authorizableId`;`ims`, dove `rep:authorizableId` è il valore del `rep:authorizableId` proprietà del nodo. (Viene utilizzato un punto e virgola senza spazi per separare la `rep:authorizableId` valore da `ims`.)
1. Fai clic sul pulsante **[!UICONTROL Aggiungi]** a destra della nuova voce, quindi fare clic su **[!UICONTROL Salva tutto]**.
1. Ripeti i passaggi da 2 a 5 per tutti gli altri utenti che desideri aggiornare per lavorare con Adobe Asset Link.
1. Nella console Web di Experience Manager, individua **[!UICONTROL Configurazione principale esterna Apache Jackrabbit Oak]** e fai clic su per modificarlo. Deseleziona la **[!UICONTROL Protezione dell’identità esterna]** e fai clic su **[!UICONTROL Salva]**.

>[!NOTE]
>
>Se i servizi non vengono ripristinati in pochi minuti, riavviare l&#39;Experience Manager per consentire l&#39;autenticazione corretta.

Dopo questa modifica, un utente Experience Manager aggiornato può connettersi ad Adobe Asset Link e continuare a utilizzare il metodo di accesso diretto all’Experience Manager utilizzato prima dell’aggiornamento. Dopo l’autenticazione con Adobe IMS, le informazioni del profilo utente Experience Manager vengono sincronizzate con il profilo utente in Adobe IMS.

È disponibile un metodo con cui è possibile eseguire una migrazione in massa di più utenti di Experience Manager per consentire loro di lavorare con Adobe Asset Link. Contatta l’Assistenza Adobe per ulteriori informazioni e assistenza sull’abilitazione di questa opzione.

In alternativa ai passaggi, in determinate circostanze, è possibile fornire a un utente Adobe Asset Link l’accesso rapido ad Experience Manager. In questi casi, le informazioni utente preesistenti vengono trovate ed eliminate con Experience Manager User Management o Experience Manager CRXDE prima della loro connessione con Adobe Asset Link. Dopo la connessione vengono create nuove informazioni utente in Experience Manager. Utilizza questo approccio solo se sei sicuro che non ci siano dati importanti aggiunti come elementi secondari del nodo utente. Tali dati aggiuntivi sono qualsiasi nodo figlio del nodo utente diverso da `tokens`, `preferences`, `profile`, `profiles`, `profiles/public`e `rep:policy/*` nodi.

## Flusso di lavoro con avvio automatico per elaborare le risorse in modo condizionale {#auto-start-workflow}

Negli Experienci Manager 6.4 e 6.5, gli amministratori possono configurare flussi di lavoro per eseguire ed elaborare automaticamente le risorse in base a condizioni predefinite.

La configurazione è utile per gli utenti della linea di business e per gli addetti al marketing, ad esempio, per creare un flusso di lavoro personalizzato su alcune cartelle specifiche. Supponiamo che tutte le risorse del servizio fotografico di un’agenzia possano essere filigranate o che tutte le risorse caricate da un freelancer possano essere elaborate per creare rappresentazioni specifiche.

Per ulteriori informazioni e per Experience Manager di configurazione, consulta [esecuzione automatica del flusso di lavoro sulle risorse](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-workflow.html#auto-execute-workflow-on-some-assets).


## Creare un indice personalizzato nelle versioni Experience Manager 6.4.x {#create-custom-index}

L&#39;Experience Manager contiene gli indici utilizzati per le query. Crea il seguente indice personalizzato per la versione specificata. Experience Manager 6.5.0 contiene questo indice per impostazione predefinita. Adobe Asset Link richiede questo indice per determinare quali risorse ha estratto un utente.

1. In CRXDE, individua `/oak:index` nodo. Crea un nodo denominato `cqDrivelock` e imposta le `Type` a `oak:QueryIndexDefinition`.

1. Aggiungi le seguenti proprietà al nuovo nodo e salva le modifiche:

   * `Name: type; Type: string; Value: property`

   * `Name: propertyNames; Type: Name[] (click the "Multi" button); Value: cq:drivelock`


## Configurare la ricerca visiva o per similarità {#configure-visual-similarity-search}

La funzionalità di ricerca visiva consente di cercare risorse visivamente simili nell’archivio AEM Assets, utilizzando il pannello Asset Link di Adobe. La funzionalità è disponibile nelle versioni 6.5.0 o successive e la ricerca viene eseguita solo sulle risorse indicizzate. Per ulteriori informazioni, consulta [come configurare la ricerca visiva](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/search-assets.html#configvisualsearch).

## Genera solo rappresentazioni per posizionamento per Adobe InDesign {#fpo-renditions}

Experience Manager fornisce rappresentazioni utilizzate solo per il posizionamento (FPO). Queste rappresentazioni FPO hanno dimensioni file ridotte ma hanno le stesse proporzioni. Se per una risorsa non è disponibile un rendering FPO, Adobe InDesign utilizza invece la risorsa originale. Questo meccanismo di fallback assicura che il flusso di lavoro creativo proceda senza interruzioni. Per ulteriori informazioni, consulta [generare rappresentazioni FPO](/help/assets/configure-fpo-renditions.md).


## Integrare con Adobe Stock {#adobe-stock-integration}

Le organizzazioni integrano i loro account Adobe Stock con Experience Manager Assets. Consente agli esperti di marketing di rendere disponibili foto, vettori, illustrazioni, video, modelli e risorse 3D di alta qualità e prive di royalty per i loro progetti creativi e di marketing. I creativi professionisti possono utilizzare queste risorse utilizzando il pannello Asset Link.

Per l’integrazione con Adobe Stock, consulta [Risorse Adobe Stock in Experience Manager Assets](/help/assets/aem-assets-adobe-stock.md). Per l’integrazione con Adobe Stock è necessario Experience Manager 6.4.2 o versioni successive.


## Risolvere i problemi relativi all’Experience Manager {#troubleshoot}


In caso di problemi durante la configurazione o l’utilizzo di Adobe Asset Link, prova quanto segue:

* Assicurati che la distribuzione soddisfi i prerequisiti. In particolare, assicurati che siano installati i pacchetti o i pacchetti di funzioni appropriati.
* Contatta il partner o l’integratore di sistema della tua organizzazione.
* Se gli utenti Creative Cloud non sono in grado di verificare nelle risorse sottoposte a Check-Out, controlla la presenza di eventuali nomi di dominio negli ID e-mail. Per risolvere il problema, vedi [configurazione manuale](#manual-configuration).
* Per ulteriori informazioni, consulta [risolvere i problemi relativi a Asset Link](https://helpx.adobe.com/enterprise/kb/asset-link-troubleshooting.html).


>[!MORELIKETHIS]
>
>* [Informazioni su Adobe Asset Link](https://helpx.adobe.com/it/enterprise/using/adobe-asset-link.html)
>* [Utilizzare Asset Link nell’app desktop Creative Cloud e gestire le risorse](https://helpx.adobe.com/it/enterprise/using/manage-assets-using-adobe-asset-link.html)
>* [Configurare Adobe Experience Manager Assets as a Cloud Service](https://helpx.adobe.com/it/enterprise/using/configure-aem-assets-for-asset-link.html).

