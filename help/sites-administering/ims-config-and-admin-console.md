---
title: Autenticazione Adobe IMS e supporto [!DNL Admin Console] AEM Managed Services
seo-title: Adobe IMS Authentication and [!DNL Admin Console] Support for AEM Managed Services
description: Scopri come utilizzare  [!DNL Admin Console] in AEM.
seo-description: Learn how to use the [!DNL Admin Console] in AEM.
uuid: 3f5b32c7-cf62-41a4-be34-3f71bbf224eb
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: f6112dea-a1eb-4fd6-84fb-f098476deab7
exl-id: 95eae97c-01c2-4f5c-8068-f504eab7c49e
feature: Security
source-git-commit: 1651fadeda0f2b37c90af2e1b2f84d74c118ccd9
workflow-type: tm+mt
source-wordcount: '1690'
ht-degree: 11%

---

# Autenticazione Adobe IMS e supporto [!DNL Admin Console] per AEM Managed Services {#adobe-ims-authentication-and-admin-console-support-for-aem-managed-services}

>[!NOTE]
>
>Questa funzione è disponibile solo per i clienti di Adobe Managed Services.

>[!NOTE]
>
>AEM attualmente non supporta l’assegnazione di gruppi ai profili.  Gli utenti devono essere aggiunti singolarmente.

## Introduzione {#introduction}

AEM 6.4.3.0 introduce il supporto [!DNL Admin Console] per le istanze AEM e l’autenticazione basata su Adobe IMS(Identity Management System) per i clienti **AEM Managed Services**.

AEM l’onboarding in [!DNL Admin Console] consentirà AEM clienti Managed Services di gestire tutti gli utenti di Experience Cloud in un’unica console. Gli utenti e i gruppi possono essere assegnati ai profili di prodotto associati alle istanze AEM, consentendo loro di accedere a un’istanza specifica.

## Elementi di rilievo {#key-highlights}

* Il supporto per l’autenticazione IMS di AEM è riservato solo agli autori, agli amministratori o agli sviluppatori di AEM, non agli utenti finali esterni di siti di clienti come i visitatori del sito
* I [!DNL Admin Console] rappresentano AEM clienti Managed Services come organizzazioni IMS e le loro istanze come contesti di prodotto. Gli amministratori di prodotto e di sistema dei clienti potranno gestire l’accesso alle istanze
* AEM Managed Services sincronizzerà le topologie dei clienti con [!DNL Admin Console]. Ci sarà un&#39;istanza di AEM contesto di prodotto Managed Services per istanza in [!DNL Admin Console].
* I profili di prodotto in [!DNL Admin Console] determinano a quali istanze può accedere un utente
* È supportata l’autenticazione federata tramite provider di identità conformi a SAML 2 dei clienti
* Saranno supportati solo Enterprise ID o Federated ID (per il servizio Single Sign-On del cliente), non gli ID Adobe personali.
* [!DNL User Management] (ad Adobe  [!DNL Admin Console]) continuerà a essere di proprietà degli amministratori dei clienti.

## Architettura {#architecture}

L’autenticazione IMS funziona utilizzando il protocollo OAuth tra AEM e l’endpoint Adobe IMS. Dopo l’aggiunta a IMS, un utente con identità Adobe può accedere ad AEM Managed Services utilizzando le credenziali IMS.

Il flusso di accesso dell&#39;utente è mostrato di seguito, l&#39;utente verrà reindirizzato a IMS ed eventualmente all&#39;IDP del cliente per la convalida SSO e quindi reindirizzato nuovamente a AEM.

![image2018-9-23_23-55-8](assets/image2018-9-23_23-55-8.png)

## Come impostare {#how-to-set-up}

### Onboarding di organizzazioni in [!DNL Admin Console] {#onboarding-organizations-to-admin-console}

L’onboarding del cliente in [!DNL Admin Console] è un prerequisito per l’utilizzo di Adobe IMS per l’autenticazione AEM.

Come primo passo, i clienti devono disporre di un&#39;organizzazione in Adobe IMS. I clienti Adobe Enterprise sono rappresentati come organizzazioni IMS nell’ [Adobe [!DNL Admin Console]](https://helpx.adobe.com/it/enterprise/using/admin-console.html).

AEM i clienti Managed Services devono già disporre del provisioning di un’organizzazione e, nell’ambito del provisioning IMS, le istanze dei clienti saranno rese disponibili in [!DNL Admin Console] per la gestione delle adesioni e dell’accesso degli utenti.

Il passaggio a IMS per l’autenticazione degli utenti sarà uno sforzo congiunto tra AMS e i clienti, ciascuno dei quali avrà i propri flussi di lavoro da completare.

Quando un cliente esiste come organizzazione IMS e AMS esegue il provisioning del cliente per IMS, questo è il riepilogo dei flussi di lavoro di configurazione richiesti:

![image2018-9-23_23-33-25](assets/image2018-9-23_23-33-25.png)

1. L&#39;amministratore di sistema designato riceve un invito ad accedere a [!DNL Admin Console]
1. L’amministratore di sistema richiede il dominio per confermare la proprietà del dominio (in questo esempio acme.com)
1. L’amministratore di sistema imposta le directory utente
1. L’amministratore di sistema configura il provider di identità (IDP) in [!DNL Admin Console] per la configurazione SSO.
1. L’amministratore AEM gestisce i gruppi, le autorizzazioni e i privilegi locali come di consueto. Consulta Sincronizzazione utenti e gruppi

>[!NOTE]
>
>Per ulteriori informazioni sull&#39;Adobe Nozioni di base di Identity Management, inclusa la configurazione IDP, consulta l&#39;articolo [questa pagina.](https://helpx.adobe.com/it/enterprise/using/set-up-identity.html)
>
>Per ulteriori informazioni sull&#39;amministrazione Enterprise e [!DNL Admin Console] consulta l&#39;articolo [questa pagina](https://helpx.adobe.com/it/enterprise/managing/user-guide.html).

### Onboarding degli utenti in [!DNL Admin Console] {#onboarding-users-to-the-admin-console}

Sono disponibili tre modi per integrare gli utenti a seconda delle dimensioni del cliente e delle loro preferenze:

1. Creare manualmente utenti e gruppi in [!DNL Admin Console]
1. Caricare un file CSV con gli utenti
1. Sincronizza utenti e gruppi dall&#39;organizzazione Active Directory del cliente.

#### Aggiunta manuale tramite l’interfaccia utente di [!DNL Admin Console] {#manual-addition-through-admin-console-ui}

Gli utenti e i gruppi possono essere creati manualmente nell&#39;interfaccia utente [!DNL Admin Console]. Questo metodo può essere utilizzato se non dispongono di un numero elevato di utenti da gestire. Ad esempio, un numero di utenti meno di 50 AEM.

Gli utenti possono anche essere creati manualmente se il cliente utilizza già questo metodo per amministrare altri prodotti di Adobe come le applicazioni di Analytics, Target o Creative Cloud.

![image2018-9-23_20-39-9](assets/image2018-9-23_20-39-9.png)

#### Caricamento di file nell’ interfaccia utente [!DNL Admin Console] {#file-upload-in-the-admin-console-ui}

Per facilitare la creazione di utenti, è possibile caricare un file CSV per aggiungere utenti in blocco:

![image2018-9-23_18-59-57](assets/image2018-9-23_18-59-57.png)

#### Strumento User Sync {#user-sync-tool}

Lo strumento User Sync (UST) consente ai clienti aziendali di creare o gestire gli utenti Adobe che utilizzano Active Directory o altri servizi di directory OpenLDAP testati. Gli utenti di destinazione sono amministratori di identità IT (directory Enterprise e amministratori di sistema) che saranno in grado di installare e configurare lo strumento. Lo strumento open source è personalizzabile in modo che i clienti possano modificarlo in base a specifiche esigenze.

Durante l’esecuzione di User Sync, recupera un elenco di utenti da Active Directory dell’organizzazione (o da qualsiasi altra origine dati compatibile) e lo confronta con l’elenco di utenti all’interno di [!DNL Admin Console]. Chiama quindi l&#39;API Adobe [!DNL User Management] in modo che il [!DNL Admin Console] sia sincronizzato con la directory dell&#39;organizzazione. Il flusso di variazione è interamente unidirezionale; eventuali modifiche apportate in [!DNL Admin Console] non vengono inviate alla directory.

Lo strumento consente all’amministratore di sistema di mappare i gruppi di utenti nella directory del cliente con la configurazione del prodotto e i gruppi di utenti nel [!DNL Admin Console], la nuova versione di UST consente anche la creazione dinamica di gruppi di utenti nel [!DNL Admin Console].

Per configurare User Sync, l’organizzazione deve creare un set di credenziali in modo analogo a come userebbe l’[[!DNL User Management] API ](https://www.adobe.io/apis/cloudplatform/usermanagement/docs/setup.html).

![image2018-9-23_13-36-56](assets/image2018-9-23_13-36-56.png)

User Sync viene distribuito tramite l’archivio Adobe Github nel seguente percorso:

[https://github.com/adobe-apiplatform/user-sync.py/releases/latest](https://github.com/adobe-apiplatform/user-sync.py/releases/latest)

Una versione pre-release 2.4RC1 è disponibile con supporto per la creazione di gruppi dinamici ed è disponibile qui: [https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1](https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1)

Le funzionalità principali di questa versione sono la possibilità di mappare in modo dinamico nuovi gruppi LDAP per l&#39;iscrizione dell&#39;utente in [!DNL Admin Console], così come la creazione di gruppi di utenti dinamici.

Ulteriori informazioni sulle nuove funzioni per i gruppi sono disponibili qui:

[https://github.com/adobe-apiplatform/user-sync.py/blob/v2/docs/en/user-manual/advanced_configuration](https://github.com/adobe-apiplatform/user-sync.py/blob/v2/docs/en/user-manual/advanced_configuration.md#additional-group-options)

>[!NOTE]
>
>Per ulteriori informazioni sullo strumento User Sync, consulta la [pagina di documentazione](https://adobe-apiplatform.github.io/user-sync.py/en/) .
>
>
>Lo strumento User Sync deve essere registrato come client UMAPI di Adobe I/O utilizzando la procedura descritta [qui](https://adobe-apiplatform.github.io/umapi-documentation/en/UM_Authentication.html).
>
>La documentazione della console Adobe I/O si trova [qui](https://www.adobe.io/apis/cloudplatform/console.html).
>
>
>L&#39;API [!DNL User Management] utilizzata dallo strumento User Sync viene descritta in questa [posizione](https://www.adobe.io/apis/cloudplatform/umapi-new.html).

>[!NOTE]
>
>La configurazione IMS AEM sarà gestita dal team di Adobe Managed Services. Tuttavia, l’amministratore del cliente può modificarlo in base alle proprie esigenze (ad esempio, Appartenenza al gruppo automatico o Mappatura gruppo). Il client IMS verrà registrato anche dal team Managed Services.

## Guida all’uso {#how-to-use}

### Gestione dei prodotti e dell’accesso utente in [!DNL Admin Console] {#managing-products-and-user-access-in-admin-console}

Quando l’amministratore del prodotto del cliente accede a [!DNL Admin Console], visualizza più istanze del contesto di prodotto Managed Services AEM come mostrato di seguito:

![screen_shot_2018-09-17at105804pm](assets/screen_shot_2018-09-17at105804pm.png)

In questo esempio, l&#39;organizzazione *AEM-MS-Onboard* dispone di 32 istanze che si estendono su topologie e ambienti diversi come Stage, Prod, ecc.

![screen_shot_2018-09-17at105517pm](assets/screen_shot_2018-09-17at105517pm.png)

Puoi controllare i dettagli dell’istanza per identificare l’istanza:

![screen_shot_2018-09-17at105601pm](assets/screen_shot_2018-09-17at105601pm.png)

In ogni istanza del contesto di prodotto, sarà presente un profilo di prodotto associato. Questo profilo di prodotto viene utilizzato per assegnare l’accesso a utenti e gruppi.

![image2018-9-18_7-48-50](assets/image2018-9-18_7-48-50.png)

Tutti gli utenti e i gruppi aggiunti sotto questo profilo di prodotto potranno accedere a tale istanza come mostrato nell’esempio seguente:

![screen_shot_2018-09-17at105623pm](assets/screen_shot_2018-09-17at105623pm.png)

### Accesso a AEM {#logging-into-aem}

#### Accesso amministratore locale {#local-admin-login}

AEM continuare a supportare gli accessi locali per gli utenti amministratori, in quanto la schermata di accesso dispone di un’opzione per accedere localmente:

![screen_shot_2018-09-18at121056am](assets/screen_shot_2018-09-18at121056am.png)

#### Accesso basato su IMS {#ims-based-login}

Per altri utenti, è possibile utilizzare l’accesso basato su IMS dopo che IMS è stato configurato per l’istanza. L&#39;utente farà prima clic sul pulsante **Accedi con Adobe** come mostrato di seguito:

![image2018-9-18_0-10-32](assets/image2018-9-18_0-10-32.png)

Vengono quindi reindirizzati alla schermata di accesso di IMS e immettono le proprie credenziali:

![screen_shot_2018-09-17at115629pm](assets/screen_shot_2018-09-17at115629pm.png)

Se durante la configurazione iniziale di [!DNL Admin Console] viene configurato un IDP federato, l&#39;utente verrà reindirizzato all&#39;IDP del cliente per l&#39;accesso SSO.

L&#39;IDP è Okta nell&#39;esempio seguente:

![screen_shot_2018-09-17at115734pm](assets/screen_shot_2018-09-17at115734pm.png)

Una volta completata l’autenticazione, l’utente verrà reindirizzato ad AEM per eseguire l’accesso:

![screen_shot_2018-09-18at120124am](assets/screen_shot_2018-09-18at120124am.png)

### Migrazione di utenti esistenti {#migrating-existing-users}

Per le istanze AEM esistenti che utilizzano un altro metodo di autenticazione e che vengono ora migrate a IMS, è necessario eseguire un passaggio di migrazione.

Gli utenti esistenti nell&#39;archivio AEM (originati localmente, tramite LDAP o SAML) possono essere migrati per puntare a IMS come IDP utilizzando l&#39;Utilità di migrazione utenti.

Questa utility verrà eseguita dal team AMS come parte del provisioning IMS.

### Gestione di autorizzazioni e ACL in AEM {#managing-permissions-and-acls-in-aem}

Il controllo degli accessi e le autorizzazioni continueranno a essere gestiti in AEM, ciò può essere ottenuto separando i gruppi di utenti provenienti da IMS (ad esempio, AEM-GRP-008 nell’esempio seguente) e i gruppi locali in cui sono definite le autorizzazioni e il controllo degli accessi. I gruppi di utenti sincronizzati da IMS possono essere assegnati a gruppi locali e ereditare le autorizzazioni.

Nell’esempio seguente, ad esempio, i gruppi sincronizzati vengono aggiunti al gruppo *Dam_Users* locale.

In questo caso, un utente è stato assegnato anche ad alcuni gruppi nel [!DNL Admin Console]. ( Tieni presente che gli utenti e i gruppi possono essere sincronizzati da LDAP utilizzando lo strumento di sincronizzazione degli utenti o creati localmente, consulta la sezione **Utenti di onboarding al[!DNL Admin Console]** precedente).

>[!NOTE]
>
>I gruppi di utenti vengono sincronizzati solo quando gli utenti accedono all&#39;istanza.

![screen_shot_2018-09-17at94207pm](assets/screen_shot_2018-09-17at94207pm.png)

L’utente fa parte dei seguenti gruppi in IMS:

![screen_shot_2018-09-17at94237pm](assets/screen_shot_2018-09-17at94237pm.png)

Quando l’utente esegue l’accesso, le iscrizioni ai gruppi vengono sincronizzate, come illustrato di seguito:

![screen_shot_2018-09-17at94033pm](assets/screen_shot_2018-09-17at94033pm.png)

In AEM, i gruppi di utenti sincronizzati da IMS possono essere aggiunti come membri a gruppi locali esistenti, ad esempio Utenti DAM.

![screen_shot_2018-09-17at95804pm](assets/screen_shot_2018-09-17at95804pm.png)

Come mostrato di seguito, il gruppo *AEM-GRP_008* eredita le autorizzazioni e i privilegi degli utenti DAM. Questo è un modo efficace di gestire le autorizzazioni per i gruppi sincronizzati ed è comunemente utilizzato anche nei metodi di autenticazione basati su LDAP.

![screen_shot_2018-09-17at110505pm](assets/screen_shot_2018-09-17at110505pm.png)
