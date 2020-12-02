---
title: ' autenticazione IMS Adobe e supporto per AEM Managed Services [!DNL Admin Console] '
seo-title: ' autenticazione IMS Adobe e supporto per AEM Managed Services [!DNL Admin Console] '
description: Scoprite come utilizzare il AEM  [!DNL Admin Console] in.
seo-description: Scoprite come utilizzare il AEM  [!DNL Admin Console] in.
uuid: 3f5b32c7-cf62-41a4-be34-3f71bbf224eb
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: f6112dea-a1eb-4fd6-84fb-f098476deab7
translation-type: tm+mt
source-git-commit: a71c1e87dd5f01ba2584282e0960ca27d419adb0
workflow-type: tm+mt
source-wordcount: '1726'
ht-degree: 11%

---


#  autenticazione IMS Adobe e [!DNL Admin Console] supporto per AEM Managed Services {#adobe-ims-authentication-and-admin-console-support-for-aem-managed-services}

>[!NOTE]
>
>Questa funzione è disponibile solo per i clienti di Adobe Managed Services.

## Introduzione {#introduction}

AEM 6.4.3.0 introduce il supporto [!DNL Admin Console] per le istanze AEM e  l&#39;autenticazione basata Adobe IMS( Identity Management System) per i clienti **AEM Managed Services**.

AEM l&#39;accesso a [!DNL Admin Console] consentirà AEM clienti Managed Services di gestire tutti gli utenti  Experience Cloud in un&#39;unica console. Gli utenti e i gruppi possono essere assegnati ai profili di prodotto associati alle istanze AEM, consentendo loro di accedere a un&#39;istanza specifica.

## Elementi di rilievo {#key-highlights}

* AEM supporto dell&#39;autenticazione IMS è solo per autori, amministratori o sviluppatori AEM, non per utenti finali esterni di siti cliente come i visitatori del sito
* [!DNL Admin Console] rappresenterà AEM clienti Managed Services come organizzazioni IMS e le loro istanze come contesti di prodotto. Gli amministratori di prodotto e di sistema dei clienti potranno gestire l&#39;accesso alle istanze
* AEM Managed Services sincronizzerà le topologie dei clienti con [!DNL Admin Console]. Nella [!DNL Admin Console] sarà presente un&#39;istanza AEM contesto prodotto Managed Services per istanza.
* Profili di prodotto in [!DNL Admin Console] determinerà le istanze a cui l&#39;utente può accedere
* È supportata l&#39;autenticazione federativa tramite provider di identità conformi SAML 2
* Saranno supportati solo Enterprise ID o Federated ID (per il cliente Single Sign-On), non  ID Adobe personali.
* [!DNL User Management] (nel  Adobe  [!DNL Admin Console]) continueranno a essere di proprietà degli amministratori cliente.

## Architettura {#architecture}

L&#39;autenticazione IMS funziona utilizzando il protocollo OAuth tra AEM e l&#39;endpoint IMS del Adobe . Dopo l’aggiunta a IMS, un utente con identità Adobe può accedere ad AEM Managed Services utilizzando le credenziali IMS.

Il flusso di accesso dell&#39;utente è riportato di seguito, l&#39;utente verrà reindirizzato a IMS e, facoltativamente, all&#39;IDP del cliente per la convalida SSO e quindi reindirizzato nuovamente a AEM.

![image2018-9-23_23-55-8](assets/image2018-9-23_23-55-8.png)

## Come impostare {#how-to-set-up}

### Organizzazione onboarding in [!DNL Admin Console] {#onboarding-organizations-to-admin-console}

L&#39;onboarding del cliente su [!DNL Admin Console] è un prerequisito per utilizzare  Adobe IMS per l&#39;autenticazione AEM.

Come primo passo, i clienti devono avere un&#39;organizzazione predisposta in  Adobe IMS.  clienti Enterprise Adobe sono rappresentati come organizzazioni IMS nel [Adobe  [!DNL Admin Console]](https://helpx.adobe.com/it/enterprise/using/admin-console.html).

AEM clienti Managed Services devono già disporre di un&#39;organizzazione predisposta e, come parte del provisioning IMS, le istanze cliente saranno rese disponibili in [!DNL Admin Console] per la gestione delle adesioni e dell&#39;accesso degli utenti.

Il passaggio a IMS per l&#39;autenticazione degli utenti sarà uno sforzo congiunto tra AMS e i clienti, con ciascuno dei quali i flussi di lavoro saranno completati.

Una volta che un cliente esiste come organizzazione IMS e AMS ha effettuato il provisioning del cliente per IMS, questo è il riepilogo dei flussi di lavoro di configurazione richiesti:

![image2018-9-23_23-33-25](assets/image2018-9-23_23-33-25.png)

1. L&#39;amministratore di sistema designato riceve un invito ad accedere a [!DNL Admin Console]
1. L&#39;amministratore di sistema richiede il dominio per confermare la proprietà del dominio (in questo esempio acme.com)
1. L&#39;amministratore di sistema imposta le directory utente
1. L&#39;amministratore di sistema configura il provider di identità (IDP) in [!DNL Admin Console] per l&#39;impostazione SSO.
1. L&#39;amministratore AEM gestisce i gruppi locali, le autorizzazioni e i privilegi come al solito. Consultate Sincronizzazione di utenti e gruppi

>[!NOTE]
>
>Per ulteriori informazioni sul Adobe   Identity Management Basics, inclusa la configurazione IDP, vedere l&#39;articolo [questa pagina.](https://helpx.adobe.com/it/enterprise/using/set-up-identity.html)
>
>Per ulteriori informazioni sull&#39;amministrazione Enterprise e [!DNL Admin Console] vedere l&#39;articolo [questa pagina](https://helpx.adobe.com/it/enterprise/managing/user-guide.html).

### Onboarding Users to [!DNL Admin Console] {#onboarding-users-to-the-admin-console}

Esistono tre modi per integrare gli utenti a seconda delle dimensioni del cliente e delle loro preferenze:

1. Creare manualmente utenti e gruppi in [!DNL Admin Console]
1. Caricare un file CSV con gli utenti
1. Sincronizzare utenti e gruppi dall&#39;Active Directory aziendale del cliente.

#### Aggiunta manuale tramite l&#39;interfaccia [!DNL Admin Console] {#manual-addition-through-admin-console-ui}

Utenti e gruppi possono essere creati manualmente nell&#39;interfaccia [!DNL Admin Console]. Questo metodo può essere utilizzato se non dispone di un numero elevato di utenti da gestire. Ad esempio, un numero inferiore a 50 utenti AEM.

Gli utenti possono anche essere creati manualmente se il cliente utilizza già questo metodo per amministrare altri prodotti  Adobe come Analytics, Target o applicazioni di Creative Cloud.

![image2018-9-23_20-39-9](assets/image2018-9-23_20-39-9.png)

#### Caricamento file nell&#39;interfaccia [!DNL Admin Console] {#file-upload-in-the-admin-console-ui}

Per semplificare la gestione della creazione di utenti, potete caricare un file CSV per aggiungere utenti in massa:

![image2018-9-23_18-59-57](assets/image2018-9-23_18-59-57.png)

#### Strumento User Sync {#user-sync-tool}

Lo strumento di sincronizzazione utenti (UST in breve) consente ai clienti aziendali di creare o gestire  utenti di Adobi che utilizzano Active Directory o altri servizi di directory OpenLDAP testati. Gli utenti di destinazione sono amministratori di identità IT (Enterprise Directory e System Admins) che saranno in grado di installare e configurare lo strumento. Lo strumento open source è personalizzabile in modo che i clienti possano modificarlo in base alle proprie esigenze specifiche.

Durante l&#39;esecuzione della sincronizzazione utenti, recupera un elenco di utenti da Active Directory dell&#39;organizzazione (o da qualsiasi altra origine dati compatibile) e lo confronta con l&#39;elenco di utenti all&#39;interno della [!DNL Admin Console]. Quindi chiama l&#39;API del Adobe  [!DNL User Management] in modo che la [!DNL Admin Console] sia sincronizzata con la directory dell&#39;organizzazione. Il flusso di variazione è interamente unidirezionale; eventuali modifiche apportate in [!DNL Admin Console] non vengono inviate alla directory.

Lo strumento consente all&#39;amministratore di sistema di mappare gruppi di utenti nella directory del cliente con configurazione di prodotto e gruppi di utenti in [!DNL Admin Console], la nuova versione UST consente anche la creazione dinamica di gruppi di utenti in [!DNL Admin Console].

Per configurare User Sync, l’organizzazione deve creare un set di credenziali in modo analogo a come userebbe l’[[!DNL User Management] API ](https://www.adobe.io/apis/cloudplatform/usermanagement/docs/setup.html).

![image2018-9-23_13-36-56](assets/image2018-9-23_13-36-56.png)

La sincronizzazione degli utenti è distribuita tramite l&#39;archivio di Github  Adobe, nel seguente percorso:

[https://github.com/adobe-apiplatform/user-sync.py/releases/latest](https://github.com/adobe-apiplatform/user-sync.py/releases/latest)

Una versione precedente alla release 2.4RC1 è disponibile con il supporto per la creazione di gruppi dinamici ed è disponibile qui: [https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1](https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1)

Le funzioni principali di questa versione sono la possibilità di mappare dinamicamente i nuovi gruppi LDAP per l&#39;iscrizione degli utenti in [!DNL Admin Console], nonché la creazione di gruppi di utenti dinamici.

Ulteriori informazioni sulle nuove funzioni del gruppo sono disponibili qui:

[https://github.com/adobe-apiplatform/user-sync.py/blob/v2/docs/en/user-manual/advanced_configuration](https://github.com/adobe-apiplatform/user-sync.py/blob/v2/docs/en/user-manual/advanced_configuration.md#additional-group-options)

>[!NOTE]
>
>Per ulteriori informazioni sullo strumento di sincronizzazione degli utenti, consultare la [pagina della documentazione](https://adobe-apiplatform.github.io/user-sync.py/en/).
>
>
>Lo strumento di sincronizzazione utenti deve registrarsi come  client Adobe I/O UMAPI utilizzando la procedura descritta [qui](https://adobe-apiplatform.github.io/umapi-documentation/en/UM_Authentication.html).
>
>La documentazione relativa  console Adobe I/O è disponibile [qui](https://www.adobe.io/apis/cloudplatform/console.html).
>
>
>L&#39;API [!DNL User Management] utilizzata dallo strumento di sincronizzazione degli utenti è coperta in questa [posizione](https://www.adobe.io/apis/cloudplatform/umapi-new.html).

>[!NOTE]
>
>La configurazione IMS AEM sarà gestita dal team Adobe Managed Services. Tuttavia, l&#39;amministratore del cliente può modificarlo in base alle proprie esigenze (ad esempio, Appartenenza automatica al gruppo o Mappatura del gruppo). Il client IMS verrà registrato anche dal team Managed Services.

## Guida all’uso {#how-to-use}

### Gestione di prodotti e accesso utente in [!DNL Admin Console] {#managing-products-and-user-access-in-admin-console}

Quando l&#39;amministratore del prodotto cliente accede a [!DNL Admin Console], visualizzeranno più istanze del contesto AEM prodotto Managed Services come illustrato di seguito:

![screen_shot_2018-09-17at105804pm](assets/screen_shot_2018-09-17at105804pm.png)

In questo esempio, l&#39;organizzazione *AEM-MS-Onboard* ha 32 istanze che si estendono su topologie e ambienti diversi come Stage, Prod, ecc.

![screen_shot_2018-09-17at105517pm](assets/screen_shot_2018-09-17at105517pm.png)

I dettagli dell’istanza possono essere verificati per identificare l’istanza:

![screen_shot_2018-09-17at105601pm](assets/screen_shot_2018-09-17at105601pm.png)

In ogni istanza Contesto prodotto, sarà associato un profilo di prodotto. Questo profilo di prodotto viene utilizzato per assegnare l&#39;accesso a utenti e gruppi.

![image2018-9-18_7-48-50](assets/image2018-9-18_7-48-50.png)

Tutti gli utenti e i gruppi aggiunti sotto questo profilo di prodotto potranno accedere a tale istanza come mostrato nell&#39;esempio seguente:

![screen_shot_2018-09-17at105623pm](assets/screen_shot_2018-09-17at105623pm.png)

### Accesso a AEM {#logging-into-aem}

#### Login amministratore locale {#local-admin-login}

AEM continuare a supportare gli accessi locali per gli utenti Admin, poiché la schermata di accesso dispone di un&#39;opzione per accedere localmente:

![screen_shot_2018-09-18at121056am](assets/screen_shot_2018-09-18at121056am.png)

#### Accesso basato su IMS {#ims-based-login}

Per altri utenti, è possibile utilizzare l’accesso basato su IMS dopo che IMS è stato configurato per l’istanza. L&#39;utente farà clic sul pulsante **Accedi con  Adobe** come mostrato di seguito:

![image2018-9-18_0-10-32](assets/image2018-9-18_0-10-32.png)

Vengono quindi reindirizzati alla schermata di accesso IMS e immettono le proprie credenziali:

![screen_shot_2018-09-17at115629pm](assets/screen_shot_2018-09-17at115629pm.png)

Se durante la configurazione iniziale di [!DNL Admin Console] è configurato un IDP federato, l&#39;utente verrà reindirizzato all&#39;IDP del cliente per SSO.

L&#39;IDP è Okta nell&#39;esempio seguente:

![screen_shot_2018-09-17at15734pm](assets/screen_shot_2018-09-17at115734pm.png)

Una volta completata l’autenticazione, l’utente verrà reindirizzato ad AEM per eseguire l’accesso:

![screen_shot_2018-09-18at120124am](assets/screen_shot_2018-09-18at120124am.png)

### Migrazione degli utenti esistenti {#migrating-existing-users}

Per le istanze di AEM esistenti che utilizzano un altro metodo di autenticazione e che ora vengono trasferite a IMS, è necessario effettuare una migrazione.

Gli utenti esistenti nell&#39;archivio AEM (originati localmente, tramite LDAP o SAML) possono essere migrati a IMS come IDP utilizzando l&#39;Utilità di migrazione degli utenti.

Questa utility verrà eseguita dal team AMS come parte del provisioning IMS.

### Gestione delle autorizzazioni e degli ACL in AEM {#managing-permissions-and-acls-in-aem}

Il controllo degli accessi e le autorizzazioni continueranno a essere gestiti in AEM, ciò può essere ottenuto separando i gruppi di utenti provenienti da IMS (ad es. AEM-GRP-008 nell&#39;esempio seguente) e i gruppi locali in cui sono definite le autorizzazioni e il controllo degli accessi. I gruppi di utenti sincronizzati da IMS possono essere assegnati a gruppi locali e ereditare le autorizzazioni.

Nell’esempio seguente, ad esempio, i gruppi sincronizzati vengono aggiunti al gruppo *Dam_Users* locale.

In questo caso, un utente è stato anche assegnato ad alcuni gruppi nella cartella [!DNL Admin Console]. ( Gli utenti e i gruppi possono essere sincronizzati da LDAP utilizzando lo strumento di sincronizzazione degli utenti o creati localmente. Consultate la sezione **Utenti onboarding sul[!DNL Admin Console]** precedente).

&amp;ast;Si noti che i gruppi di utenti vengono sincronizzati solo quando gli utenti accedono all&#39;istanza, per i clienti che hanno un numero elevato di utenti e gruppi, AMS può eseguire un&#39;utility di sincronizzazione di gruppo per preacquisire i gruppi per il controllo degli accessi e la gestione delle autorizzazioni descritte in precedenza.

![screen_shot_2018-09-17at94207pm](assets/screen_shot_2018-09-17at94207pm.png)

L’utente fa parte dei seguenti gruppi in IMS:

![screen_shot_2018-09-17at94237pm](assets/screen_shot_2018-09-17at94237pm.png)

Quando l’utente esegue l’accesso, le iscrizioni ai gruppi vengono sincronizzate, come illustrato di seguito:

![screen_shot_2018-09-17at94033pm](assets/screen_shot_2018-09-17at94033pm.png)

In AEM, i gruppi di utenti sincronizzati da IMS possono essere aggiunti come membri a gruppi locali esistenti, ad esempio Utenti DAM.

![screen_shot_2018-09-17at95804pm](assets/screen_shot_2018-09-17at95804pm.png)

Come mostrato di seguito, il gruppo *AEM-GRP_008* eredita le autorizzazioni e i privilegi degli utenti DAM. Questo è un modo efficace per gestire le autorizzazioni per i gruppi sincronizzati ed è comunemente utilizzato anche nei metodi di autenticazione basati su LDAP.

![screen_shot_2018-09-17at110505pm](assets/screen_shot_2018-09-17at110505pm.png)
