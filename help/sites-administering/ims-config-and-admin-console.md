---
title: Autenticazione Adobe IMS e  [!DNL Admin Console] supporto per Adobe Experience Manager Managed Services
description: Scopri come utilizzare  [!DNL Admin Console]  in Adobe Experience Manager.
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: 95eae97c-01c2-4f5c-8068-f504eab7c49e
feature: Security
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 55bf7104dbd9b9fadf6cb37efa28084fe43393c3
workflow-type: tm+mt
source-wordcount: '1603'
ht-degree: 6%

---

# Autenticazione Adobe IMS e supporto [!DNL Admin Console] per AEM Managed Services {#adobe-ims-authentication-and-admin-console-support-for-aem-managed-services}

>[!NOTE]
>
>Questa funzione è disponibile solo per i clienti Adobe Managed Services.

## Introduzione {#introduction}

AEM 6.4.3.0 introduce il supporto [!DNL Admin Console] per le istanze AEM e l&#39;autenticazione basata su Adobe IMS (Identity Management System) per i clienti **AEM Managed Services**.

L&#39;onboarding AEM in [!DNL Admin Console] consentirà ai clienti AEM Managed Services di gestire tutti gli utenti Experience Cloud in un&#39;unica console. Gli utenti possono essere assegnati a profili di prodotto associati a istanze AEM, consentendo loro di accedere a un’istanza specifica.

## Elementi di rilievo {#key-highlights}

* Il supporto per l’autenticazione AEM IMS è riservato solo agli autori, agli amministratori o agli sviluppatori AEM e non agli utenti finali esterni del sito del cliente, come i visitatori del sito
* [!DNL Admin Console] rappresenterà i clienti Managed Services dell&#39;AEM come organizzazioni IMS e le relative istanze come contesti di prodotto. Gli amministratori di prodotto e sistema del cliente potranno gestire l’accesso alle istanze
* Managed Services per AEM sincronizzerà le topologie del cliente con [!DNL Admin Console]. AEM In [!DNL Admin Console] sarà presente un&#39;istanza di Contesto del prodotto Managed Services per istanza.
* I profili di prodotto in [!DNL Admin Console] determineranno le istanze a cui un utente può accedere
* È supportata l’autenticazione federata tramite i provider di identità conformi a SAML 2 dei clienti
* Saranno supportati solo Enterprise ID e Federated ID (per il Single Sign-On del cliente), non gli ID Adobe personali.
* [!DNL User Management] (nell&#39;Adobe [!DNL Admin Console]) continuerà a essere di proprietà degli amministratori dei clienti.

## Architettura {#architecture}

L’autenticazione IMS funziona utilizzando il protocollo OAuth tra l’AEM e l’endpoint Adobe IMS. Dopo l’aggiunta a IMS, un utente con identità Adobe può accedere ad AEM Managed Services utilizzando le credenziali IMS.

Il flusso di accesso dell’utente è mostrato di seguito, l’utente verrà reindirizzato a IMS e facoltativamente all’IDP del cliente per la convalida SSO e quindi reindirizzato nuovamente a AEM.

![immagine2018-9-23_23-55-8](assets/image2018-9-23_23-55-8.png)

## Come Impostare {#how-to-set-up}

### Onboarding di organizzazioni in [!DNL Admin Console] {#onboarding-organizations-to-admin-console}

L&#39;onboarding del cliente in [!DNL Admin Console] è un prerequisito per l&#39;utilizzo di Adobe IMS per l&#39;autenticazione AEM.

Come primo passaggio, per i clienti deve essere stato eseguito il provisioning di un’organizzazione in Adobe IMS. I clienti Adobe Enterprise sono rappresentati come organizzazioni IMS in [Adobe [!DNL Admin Console]](https://helpx.adobe.com/it/enterprise/using/admin-console.html).

Per i clienti Managed Services AEM è già necessario eseguire il provisioning di un&#39;organizzazione e, come parte del provisioning IMS, le istanze dei clienti saranno rese disponibili in [!DNL Admin Console] per la gestione delle adesioni utente e dell&#39;accesso.

Il passaggio a IMS per l’autenticazione degli utenti sarà uno sforzo congiunto tra AMS e i clienti, ciascuno con i propri flussi di lavoro da completare.

Una volta che un cliente esiste come organizzazione IMS e AMS ha completato il provisioning per IMS, si tratta del riepilogo dei flussi di lavoro di configurazione richiesti:

![immagine2018-9-23_23-33-25](assets/image2018-9-23_23-33-25.png)

1. L&#39;amministratore di sistema designato riceve un invito ad accedere a [!DNL Admin Console]
1. L’amministratore di sistema richiede il dominio per confermare la proprietà del dominio (in questo esempio acme.com)
1. L’amministratore di sistema configura le directory utente
1. L&#39;amministratore di sistema configura il provider di identità (IDP) in [!DNL Admin Console] per la configurazione SSO.
1. L’amministratore AEM gestisce i gruppi locali, le autorizzazioni e i privilegi come di consueto. Consulta User and Group Sync

>[!NOTE]
>
>Per ulteriori informazioni sull&#39;Adobe Nozioni di base di Identity Management, inclusa la configurazione IDP, vedere l&#39;articolo [questa pagina.](https://helpx.adobe.com/it/enterprise/using/set-up-identity.html)
>
>Per ulteriori informazioni sull&#39;amministrazione Enterprise e [!DNL Admin Console], vedere l&#39;articolo [questa pagina](https://helpx.adobe.com/it/enterprise/managing/user-guide.html).

### Onboarding degli utenti in [!DNL Admin Console] {#onboarding-users-to-the-admin-console}

Sono disponibili tre modi per integrare gli utenti a seconda delle dimensioni del cliente e delle sue preferenze:

1. Crea manualmente utenti e gruppi in [!DNL Admin Console]
1. Carica un file CSV con gli utenti
1. Sincronizza utenti e gruppi con Active Directory aziendale del cliente.

#### Aggiunta manuale tramite interfaccia utente [!DNL Admin Console] {#manual-addition-through-admin-console-ui}

È possibile creare manualmente utenti e gruppi nell&#39;interfaccia utente [!DNL Admin Console]. Questo metodo può essere utilizzato se non hanno molti utenti da gestire. Ad esempio, meno di 50 persone affette da AEM.

Gli utenti possono anche essere creati manualmente se il cliente sta già utilizzando questo metodo per amministrare altri prodotti di Adobe come le applicazioni Adobe Analytics, Adobe Target o Adobe Creative Cloud.

![immagine2018-9-23_20-39-9](assets/image2018-9-23_20-39-9.png)

#### Caricamento di file nell&#39;interfaccia utente [!DNL Admin Console] {#file-upload-in-the-admin-console-ui}

Per facilitare la creazione di utenti, è possibile caricare un file CSV per aggiungere utenti in blocco:

![immagine2018-9-23_18-59-57](assets/image2018-9-23_18-59-57.png)

#### Strumento User Sync {#user-sync-tool}

Lo strumento User Sync consente ai clienti aziendali di creare o gestire utenti Adobi che utilizzano Active Directory o altri servizi di directory OpenLDAP testati. Gli utenti target sono amministratori di identità IT (Enterprise Directory e amministratori di sistema) che saranno in grado di installare e configurare lo strumento. Lo strumento open-source è personalizzabile in modo che i clienti possano chiedere a uno sviluppatore di modificarlo in base alle proprie esigenze.

Durante l&#39;esecuzione di User Sync, viene recuperato un elenco di utenti da Active Directory dell&#39;organizzazione (o da qualsiasi altra origine dati compatibile) e viene confrontato con l&#39;elenco di utenti all&#39;interno di [!DNL Admin Console]. Chiama quindi l&#39;API Adobe [!DNL User Management] in modo che [!DNL Admin Console] sia sincronizzato con la directory dell&#39;organizzazione. Il flusso di modifica è completamente unidirezionale. Eventuali modifiche apportate in [!DNL Admin Console] non vengono inviate alla directory.

Lo strumento consente all&#39;amministratore di sistema di mappare i gruppi di utenti nella directory del cliente con la configurazione del prodotto e i gruppi di utenti in [!DNL Admin Console]. La nuova versione di User Sync consente inoltre la creazione dinamica di gruppi di utenti in [!DNL Admin Console].

Per impostare User Sync, l&#39;organizzazione deve creare un set di credenziali nello stesso modo in cui utilizzerebbe l&#39;[[!DNL User Management] API](https://www.adobe.io/apis/cloudplatform/usermanagement/docs/setup.html).

![immagine2018-9-23_13-36-56](assets/image2018-9-23_13-36-56.png)

La sincronizzazione degli utenti viene distribuita tramite l’archivio Github di Adobe nella posizione seguente:

[https://github.com/adobe-apiplatform/user-sync.py/releases/latest](https://github.com/adobe-apiplatform/user-sync.py/releases/latest)

È disponibile una versione non definitiva 2.4RC1 con supporto per la creazione di gruppi dinamici, disponibile qui: [https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1](https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1)

Le funzionalità principali di questa versione sono la possibilità di mappare dinamicamente nuovi gruppi LDAP per l&#39;iscrizione degli utenti in [!DNL Admin Console] e la creazione dinamica di gruppi di utenti.

Ulteriori informazioni sulle nuove funzioni per i gruppi sono disponibili qui:

[https://adobe-apiplatform.github.io/user-sync.py/en/user-manual/advanced_configuration.html#additional-group-options](https://adobe-apiplatform.github.io/user-sync.py/fr/user-manual/advanced_configuration.html#additional-group-options)

>[!NOTE]
>
>Per ulteriori informazioni sullo strumento User Sync, consulta la [pagina della documentazione](https://adobe-apiplatform.github.io/user-sync.py/it/).
>
>
>Lo strumento User Sync deve essere registrato come client UMAPI di Adobe I/O utilizzando la procedura descritta [qui](https://adobe-apiplatform.github.io/umapi-documentation/en/UM_Authentication.html).
>
>La documentazione di Adobe Developer Console è disponibile [qui](https://developer.adobe.com/developer-console/docs/guides/).
>
>
>L&#39;API [!DNL User Management] utilizzata dallo strumento User Sync è coperta in questa [posizione](https://adobe-apiplatform.github.io/umapi-documentation/en/).

>[!NOTE]
>
>La configurazione AEM IMS sarà gestita dal team Adobe Managed Services. Tuttavia, l’amministratore del cliente può modificarla in base alle proprie esigenze (ad esempio, Iscrizione automatica al gruppo o Mappatura del gruppo). Anche il client IMS verrà registrato dal team Managed Services.

## Guida all’uso {#how-to-use}

### Gestione di prodotti e accesso utente in [!DNL Admin Console] {#managing-products-and-user-access-in-admin-console}

Quando l&#39;amministratore di prodotto del cliente accede a [!DNL Admin Console], vedrà più istanze del contesto di prodotto Managed Services dell&#39;AEM come mostrato di seguito:

![schermata_shot_2018-09-17alle105804pm](assets/screen_shot_2018-09-17at105804pm.png)

In questo esempio, l&#39;organizzazione *AEM-MS-Onboard* dispone di 32 istanze distribuite in topologie e ambienti diversi come Stage, Prod e così via.

![schermata_shot_2018-09-17alle105517pm](assets/screen_shot_2018-09-17at105517pm.png)

I dettagli dell’istanza possono essere controllati per identificarla:

![schermata_shot_2018-09-17alle105601pm](assets/screen_shot_2018-09-17at105601pm.png)

In ogni istanza del contesto di prodotto sarà presente un profilo di prodotto associato. Questo profilo di prodotto viene utilizzato per assegnare l’accesso agli utenti.

![immagine2018-9-18_7-48-50](assets/image2018-9-18_7-48-50.png)

Tutti gli utenti aggiunti in questo profilo di prodotto potranno accedere a tale istanza come mostrato nell’esempio seguente:

![schermata_shot_2018-09-17alle105623pm](assets/screen_shot_2018-09-17at105623pm.png)

### Accesso all’AEM {#logging-into-aem}

#### Accesso amministratore locale {#local-admin-login}

AEM può continuare a supportare gli accessi locali per gli utenti Admin, in quanto la schermata di accesso dispone di un’opzione per accedere localmente:

![schermata_shot_2018-09-18at121056am](assets/screen_shot_2018-09-18at121056am.png)

#### Accesso basato su IMS {#ims-based-login}

Per altri utenti, è possibile utilizzare l’accesso basato su IMS dopo che IMS è stato configurato per l’istanza. L&#39;utente fa prima clic su **Accedi con l&#39;Adobe** come mostrato di seguito:

![immagine2018-9-18_0-10-32](assets/image2018-9-18_0-10-32.png)

Vengono quindi reindirizzati alla schermata di accesso di IMS e immettono le relative credenziali:

![schermata_shot_2018-09-17alle115629pm](assets/screen_shot_2018-09-17at115629pm.png)

Se durante la configurazione iniziale di [!DNL Admin Console] viene configurato un IDP federato, l&#39;utente verrà reindirizzato all&#39;IDP del cliente per l&#39;accesso SSO.

L’IDP è Okta nell’esempio seguente:

![schermata_shot_2018-09-17alle115734pm](assets/screen_shot_2018-09-17at115734pm.png)

Una volta completata l’autenticazione, l’utente verrà reindirizzato ad AEM per eseguire l’accesso:

![schermata_shot_2018-09-18at120124am](assets/screen_shot_2018-09-18at120124am.png)

### Migrazione degli utenti esistenti {#migrating-existing-users}

Per le istanze AEM esistenti che utilizzano un altro metodo di autenticazione e ora stanno eseguendo la migrazione a IMS, è necessario un passaggio di migrazione.

Gli utenti esistenti nell’archivio AEM (originato localmente, tramite LDAP o SAML) possono essere migrati per indicare IMS come IDP utilizzando l’utility di migrazione utenti.

Questa utility verrà eseguita dal team AMS come parte del provisioning IMS.

### Gestione di autorizzazioni e ACL in AEM {#managing-permissions-and-acls-in-aem}

Il controllo degli accessi e le autorizzazioni continueranno a essere gestiti in AEM; a questo scopo è possibile separare i gruppi di utenti provenienti da IMS (ad esempio AEM-GRP-008 nell’esempio seguente) e dai gruppi locali in cui sono definite le autorizzazioni e il controllo degli accessi. I gruppi di utenti sincronizzati da IMS possono essere assegnati a gruppi locali ed ereditare le autorizzazioni.

Nell’esempio seguente, ad esempio, i gruppi sincronizzati vengono aggiunti al gruppo *Dam_Users* locale.

In questo caso, un utente è stato anche assegnato ad alcuni gruppi in [!DNL Admin Console]. Gli utenti e i gruppi possono essere sincronizzati da LDAP utilizzando lo strumento User Sync o creati localmente. Consulta **Onboarding degli utenti in[!DNL Admin Console]** in precedenza).

>[!NOTE]
>
>I gruppi di utenti vengono sincronizzati solo quando gli utenti accedono all’istanza.

![schermata_shot_2018-09-17alle94207pm](assets/screen_shot_2018-09-17at94207pm.png)

L’utente fa parte dei seguenti gruppi in IMS:

![schermata_shot_2018-09-17alle94237pm](assets/screen_shot_2018-09-17at94237pm.png)

Quando l’utente esegue l’accesso, le iscrizioni ai gruppi vengono sincronizzate, come illustrato di seguito:

![schermata_shot_2018-09-17alle94033pm](assets/screen_shot_2018-09-17at94033pm.png)

In AEM, i gruppi di utenti sincronizzati da IMS possono essere aggiunti come membri a gruppi locali esistenti, ad esempio DAM Users.

![schermata_shot_2018-09-17alle95804pm](assets/screen_shot_2018-09-17at95804pm.png)

Come mostrato di seguito, il gruppo *AEM-GRP_008* eredita le autorizzazioni e i privilegi degli utenti DAM. Si tratta di un modo efficace per gestire le autorizzazioni per i gruppi sincronizzati ed è comunemente utilizzato anche nei metodi di autenticazione basati su LDAP.

![schermata_shot_2018-09-17alle110505pm](assets/screen_shot_2018-09-17at110505pm.png)
