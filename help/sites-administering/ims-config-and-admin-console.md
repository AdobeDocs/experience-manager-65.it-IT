---
title: ' Adobe IMS Authentication [!DNL Admin Console] and Support per AEM Managed Services'
seo-title: ' Adobe IMS Authentication [!DNL Admin Console] and Support per AEM Managed Services'
description: Scoprite come utilizzare il Admin Console di [!DNL] in AEM.
seo-description: Scoprite come utilizzare il Admin Console di [!DNL] in AEM.
uuid: 3f5b32c7-cf62-41a4-be34-3f71bbf224eb
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: f6112dea-a1eb-4fd6-84fb-f098476deab7
translation-type: tm+mt
source-git-commit: 5a421c66930d8c7a9eb633c707b4b51d4549b303
workflow-type: tm+mt
source-wordcount: '1730'
ht-degree: 11%

---


#  autenticazione IMS Adobe e [!DNL Admin Console] supporto per AEM Managed Services {#adobe-ims-authentication-and-admin-console-support-for-aem-managed-services}

>[!NOTE]
>
>Questa funzione è disponibile solo per i clienti di Adobe Managed Services.

## Introduzione {#introduction}

AEM 6.4.3.0 introduce [!DNL Admin Console] il supporto per le istanze AEM e  l&#39;autenticazione basata Adobe IMS( Identity Management System) per **AEM clienti Managed Services** .

AEM l&#39;accesso al [!DNL Admin Console] sistema consentirà AEM clienti Managed Services di gestire tutti gli utenti  Experience Cloud in un&#39;unica console. Gli utenti e i gruppi possono essere assegnati ai profili di prodotto associati alle istanze AEM, consentendo loro di accedere a un&#39;istanza specifica.

## Elementi di rilievo {#key-highlights}

* AEM supporto dell&#39;autenticazione IMS è solo per autori, amministratori o sviluppatori AEM, non per utenti finali esterni di siti cliente come i visitatori del sito
* I clienti Managed Services [!DNL Admin Console] saranno AEM come organizzazioni IMS e le relative istanze come contesti di prodotto. Gli amministratori di prodotto e di sistema dei clienti potranno gestire l&#39;accesso alle istanze
* AEM Managed Services sincronizzerà le topologie dei clienti con il [!DNL Admin Console]. Esiste un&#39;istanza di AEM contesto prodotto Managed Services per istanza nel [!DNL Admin Console].
* Product Profiles in [!DNL Admin Console] will determine which instances a user can access
* È supportata l&#39;autenticazione federativa tramite provider di identità conformi SAML 2
* Saranno supportati solo Enterprise ID o Federated ID (per il cliente Single Sign-On), non  ID Adobe personali.
* [!DNL User Management] (nel  Adobe [!DNL Admin Console]) continueranno a essere di proprietà degli amministratori cliente.

## Architettura {#architecture}

L&#39;autenticazione IMS funziona utilizzando il protocollo OAuth tra AEM e l&#39;endpoint IMS del Adobe . Dopo l’aggiunta a IMS, un utente con identità Adobe può accedere ad AEM Managed Services utilizzando le credenziali IMS.

Il flusso di accesso dell&#39;utente è riportato di seguito, l&#39;utente verrà reindirizzato a IMS e, facoltativamente, all&#39;IDP del cliente per la convalida SSO e quindi reindirizzato nuovamente a AEM.

![image2018-9-23_23-55-8](assets/image2018-9-23_23-55-8.png)

## How To Set Up {#how-to-set-up}

### Onboarding Organizations to [!DNL Admin Console] {#onboarding-organizations-to-admin-console}

The customer onboarding to [!DNL Admin Console] is a pre-requisite to using Adobe IMS for AEM authentication.

Come primo passo, i clienti devono avere un&#39;organizzazione predisposta in  Adobe IMS.  clienti Enterprise Adobe sono rappresentati come organizzazioni IMS nel Adobe [ [!DNL Admin Console]](https://helpx.adobe.com/it/enterprise/using/admin-console.html).

AEM Managed Services customers should already have an organization provisioned, and as part of the IMS provisioning, the customer instances will be made available in the [!DNL Admin Console] for managing user entitlements and access.

Il passaggio a IMS per l&#39;autenticazione degli utenti sarà uno sforzo congiunto tra AMS e i clienti, con ciascuno dei quali i flussi di lavoro saranno completati.

Una volta che un cliente esiste come organizzazione IMS e AMS ha effettuato il provisioning del cliente per IMS, questo è il riepilogo dei flussi di lavoro di configurazione richiesti:

![image2018-9-23_23-33-25](assets/image2018-9-23_23-33-25.png)

1. The designated System Admin receives an invite to log in to the [!DNL Admin Console]
1. L&#39;amministratore di sistema richiede il dominio per confermare la proprietà del dominio (in questo esempio acme.com)
1. L&#39;amministratore di sistema imposta le directory utente
1. L&#39;amministratore di sistema configura il provider di identità (IDP) nella configurazione [!DNL Admin Console] per SSO.
1. L&#39;amministratore AEM gestisce i gruppi locali, le autorizzazioni e i privilegi come al solito. Consultate Sincronizzazione di utenti e gruppi

>[!NOTE]
>
>Per ulteriori informazioni sul Adobe   Identity Management Basics, inclusa la configurazione IDP, consultate l&#39;articolo [in questa pagina.](https://helpx.adobe.com/it/enterprise/using/set-up-identity.html)
>
>Per ulteriori informazioni sull&#39;amministrazione Enterprise e [!DNL Admin Console] consultate l&#39;articolo [in questa pagina](https://helpx.adobe.com/it/enterprise/managing/user-guide.html).

### Onboarding Users to the [!DNL Admin Console] {#onboarding-users-to-the-admin-console}

Esistono tre modi per integrare gli utenti a seconda delle dimensioni del cliente e delle loro preferenze:

1. Creare manualmente utenti e gruppi in [!DNL Admin Console]
1. Caricare un file CSV con gli utenti
1. Sincronizzare utenti e gruppi dall&#39;Active Directory aziendale del cliente.

#### Manual Addition through [!DNL Admin Console] UI {#manual-addition-through-admin-console-ui}

Users and Groups can be manually created in the [!DNL Admin Console] UI. Questo metodo può essere utilizzato se non dispone di un numero elevato di utenti da gestire. Ad esempio, un numero inferiore a 50 utenti AEM.

Gli utenti possono anche essere creati manualmente se il cliente utilizza già questo metodo per amministrare altri prodotti  Adobe come Analytics, Target o applicazioni di Creative Cloud.

![image2018-9-23_20-39-9](assets/image2018-9-23_20-39-9.png)

#### Caricamento file nell’ [!DNL Admin Console] interfaccia utente {#file-upload-in-the-admin-console-ui}

Per semplificare la gestione della creazione di utenti, potete caricare un file CSV per aggiungere utenti in massa:

![image2018-9-23_18-59-57](assets/image2018-9-23_18-59-57.png)

#### Strumento User Sync {#user-sync-tool}

Lo strumento di sincronizzazione utenti (UST in breve) consente ai clienti aziendali di creare o gestire  utenti di Adobi che utilizzano Active Directory o altri servizi di directory OpenLDAP testati. Gli utenti di destinazione sono amministratori di identità IT (Enterprise Directory e System Admins) che saranno in grado di installare e configurare lo strumento. Lo strumento open source è personalizzabile in modo che i clienti possano modificarlo in base alle proprie esigenze specifiche.

When User Sync runs, it fetches a list of users from the organization’s Active Directory (or any other compatible data source) and compares it with the list of users within the [!DNL Admin Console]. It then calls the Adobe [!DNL User Management] API so that the [!DNL Admin Console] is synchronized with the organization’s directory. Il flusso di variazione è interamente unidirezionale; eventuali modifiche apportate nella directory [!DNL Admin Console] non vengono inviate alla directory.

Lo strumento consente all&#39;amministratore di sistema di mappare i gruppi di utenti nella directory del cliente con la configurazione del prodotto e i gruppi di utenti nella [!DNL Admin Console], la nuova versione UST consente anche la creazione dinamica dei gruppi di utenti nella [!DNL Admin Console].

Per configurare User Sync, l’organizzazione deve creare un set di credenziali in modo analogo a come userebbe l’[[!DNL User Management] API ](https://www.adobe.io/apis/cloudplatform/usermanagement/docs/setup.html).

![image2018-9-23_13-36-56](assets/image2018-9-23_13-36-56.png)

La sincronizzazione degli utenti è distribuita tramite l&#39;archivio di Github  Adobe, nel seguente percorso:

[https://github.com/adobe-apiplatform/user-sync.py/releases/latest](https://github.com/adobe-apiplatform/user-sync.py/releases/latest)

Una versione precedente alla release 2.4RC1 è disponibile con il supporto per la creazione di gruppi dinamici ed è disponibile qui: [https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1](https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1)

The major features for this release are the ability to dynamically map new LDAP groups for user membership in the [!DNL Admin Console], as well as dynamic user group creation.

Ulteriori informazioni sulle nuove funzioni del gruppo sono disponibili qui:

[https://github.com/adobe-apiplatform/user-sync.py/blob/v2/docs/en/user-manual/advanced_configuration](https://github.com/adobe-apiplatform/user-sync.py/blob/v2/docs/en/user-manual/advanced_configuration.md#additional-group-options)

>[!NOTE]
>
>Per ulteriori informazioni sullo strumento di sincronizzazione degli utenti, consulta la pagina [della](https://adobe-apiplatform.github.io/user-sync.py/en/)documentazione.
>
>
>The User Sync Tool needs to register as an Adobe I/O client UMAPI using the procedure described [here](https://adobe-apiplatform.github.io/umapi-documentation/en/UM_Authentication.html).
>
>The Adobe I/O Console Documentation can be found [here](https://www.adobe.io/apis/cloudplatform/console.html).
>
>
>L&#39; [!DNL User Management] API utilizzata dallo strumento di sincronizzazione degli utenti è trattata in questa [posizione](https://www.adobe.io/apis/cloudplatform/umapi-new.html).

>[!NOTE]
>
>La configurazione IMS AEM sarà gestita dal team Adobe Managed Services. Tuttavia, l&#39;amministratore del cliente può modificarlo in base alle proprie esigenze (ad esempio, Appartenenza automatica al gruppo o Mappatura del gruppo). Il client IMS verrà registrato anche dal team Managed Services.

## Guida all’uso {#how-to-use}

### Managing Products and User Access in [!DNL Admin Console] {#managing-products-and-user-access-in-admin-console}

When the customer Product Administrator logs in to [!DNL Admin Console], they will see multiple instances of the AEM Managed Services Product Context as shown below:

![screen_shot_2018-09-17at105804pm](assets/screen_shot_2018-09-17at105804pm.png)

In this example, the org *AEM-MS-Onboard* has 32 instances spanning different topologies and environments like Stage, Prod, etc.

![screen_shot_2018-09-17at105517pm](assets/screen_shot_2018-09-17at105517pm.png)

I dettagli dell’istanza possono essere verificati per identificare l’istanza:

![screen_shot_2018-09-17at105601pm](assets/screen_shot_2018-09-17at105601pm.png)

In ogni istanza Contesto prodotto, sarà associato un profilo di prodotto. Questo profilo di prodotto viene utilizzato per assegnare l&#39;accesso a utenti e gruppi.

![image2018-9-18_7-48-50](assets/image2018-9-18_7-48-50.png)

Tutti gli utenti e i gruppi aggiunti sotto questo profilo di prodotto potranno accedere a tale istanza come mostrato nell&#39;esempio seguente:

![screen_shot_2018-09-17at105623pm](assets/screen_shot_2018-09-17at105623pm.png)

### Accesso AEM {#logging-into-aem}

#### Login amministratore locale {#local-admin-login}

AEM continuare a supportare gli accessi locali per gli utenti Admin, poiché la schermata di accesso dispone di un&#39;opzione per accedere localmente:

![screen_shot_2018-09-18at121056am](assets/screen_shot_2018-09-18at121056am.png)

#### Accesso basato su IMS {#ims-based-login}

Per altri utenti, è possibile utilizzare l’accesso basato su IMS dopo che IMS è stato configurato per l’istanza. The user will first click on the **Sign in with Adobe** button as shown below:

![image2018-9-18_0-10-32](assets/image2018-9-18_0-10-32.png)

Vengono quindi reindirizzati alla schermata di accesso IMS e immettono le proprie credenziali:

![screen_shot_2018-09-17at115629pm](assets/screen_shot_2018-09-17at115629pm.png)

If a federated IDP is configured during initial [!DNL Admin Console] setup, then the user will be redirected to the customer IDP for SSO.

L&#39;IDP è Okta nell&#39;esempio seguente:

![screen_shot_2018-09-17at15734pm](assets/screen_shot_2018-09-17at115734pm.png)

Una volta completata l’autenticazione, l’utente verrà reindirizzato ad AEM per eseguire l’accesso:

![screen_shot_2018-09-18at120124am](assets/screen_shot_2018-09-18at120124am.png)

### Migrazione degli utenti esistenti {#migrating-existing-users}

Per le istanze di AEM esistenti che utilizzano un altro metodo di autenticazione e che ora vengono trasferite a IMS, è necessario effettuare una migrazione.

Gli utenti esistenti nell&#39;archivio AEM (originati localmente, tramite LDAP o SAML) possono essere migrati a IMS come IDP utilizzando l&#39;Utilità di migrazione degli utenti.

Questa utility verrà eseguita dal team AMS come parte del provisioning IMS.

### Gestione di autorizzazioni e ACL in AEM {#managing-permissions-and-acls-in-aem}

Il controllo degli accessi e le autorizzazioni continueranno a essere gestiti in AEM, ciò può essere ottenuto separando i gruppi di utenti provenienti da IMS (ad es. AEM-GRP-008 nell&#39;esempio seguente) e i gruppi locali in cui sono definite le autorizzazioni e il controllo degli accessi. I gruppi di utenti sincronizzati da IMS possono essere assegnati a gruppi locali e ereditare le autorizzazioni.

Nell’esempio seguente, ad esempio, i gruppi sincronizzati vengono aggiunti al gruppo *Dam_Users* locale.

In questo caso, un utente è stato assegnato anche a alcuni gruppi nella [!DNL Admin Console]. (Gli utenti e i gruppi possono essere sincronizzati da LDAP utilizzando lo strumento di sincronizzazione utenti o creati localmente. Consultate la sezione Utenti **onboarding[!DNL Admin Console]** qui sopra).

&amp;ast;Si noti che i gruppi di utenti vengono sincronizzati solo quando gli utenti accedono all&#39;istanza, per i clienti che hanno un numero elevato di utenti e gruppi, AMS può eseguire un&#39;utility di sincronizzazione di gruppo per preacquisire i gruppi per il controllo degli accessi e la gestione delle autorizzazioni descritte in precedenza.

![screen_shot_2018-09-17at94207pm](assets/screen_shot_2018-09-17at94207pm.png)

L’utente fa parte dei seguenti gruppi in IMS:

![screen_shot_2018-09-17at94237pm](assets/screen_shot_2018-09-17at94237pm.png)

Quando l’utente esegue l’accesso, le iscrizioni ai gruppi vengono sincronizzate, come illustrato di seguito:

![screen_shot_2018-09-17at94033pm](assets/screen_shot_2018-09-17at94033pm.png)

In AEM, i gruppi di utenti sincronizzati da IMS possono essere aggiunti come membri a gruppi locali esistenti, ad esempio Utenti DAM.

![screen_shot_2018-09-17at95804pm](assets/screen_shot_2018-09-17at95804pm.png)

Come mostrato di seguito, il gruppo *AEM-GRP_008* eredita i privilegi e le autorizzazioni degli utenti DAM. Questo è un modo efficace per gestire le autorizzazioni per i gruppi sincronizzati ed è comunemente utilizzato anche nei metodi di autenticazione basati su LDAP.

![screen_shot_2018-09-17at110505pm](assets/screen_shot_2018-09-17at110505pm.png)