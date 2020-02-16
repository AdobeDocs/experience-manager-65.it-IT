---
title: Autenticazione Adobe IMS e supporto di Admin Console per i servizi gestiti AEM
seo-title: Autenticazione Adobe IMS e supporto di Admin Console per i servizi gestiti AEM
description: Scopri come utilizzare Admin Console in AEM.
seo-description: Scopri come utilizzare Admin Console in AEM.
uuid: 3f5b32c7-cf62-41a4-be34-3f71bbf224eb
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: f6112dea-a1eb-4fd6-84fb-f098476deab7
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d

---


# Autenticazione Adobe IMS e supporto di Admin Console per i servizi gestiti AEM {#adobe-ims-authentication-and-admin-console-support-for-aem-managed-services}

>[!NOTE]
>
>Questa funzione è disponibile solo per i clienti di Adobe Managed Services.

## Introduzione {#introduction}

AEM 6.4.3.0 introduce il supporto Admin Console per le istanze AEM e l&#39;autenticazione basata su Adobe IMS(Identity Management System) per i clienti dei servizi **gestiti** AEM.

L&#39;accesso ad Admin Console di AEM consentirà ai clienti dei servizi gestiti di AEM di gestire tutti gli utenti Experience Cloud in un&#39;unica console. Utenti e gruppi possono essere assegnati ai profili di prodotto associati alle istanze AEM, consentendo loro di accedere a un&#39;istanza specifica.

## Evidenziazioni chiave {#key-highlights}

* Il supporto per l&#39;autenticazione AEM IMS è solo per autori, amministratori o sviluppatori AEM, non per utenti finali esterni di siti cliente come i visitatori del sito
* Admin Console rappresenterà i clienti dei servizi gestiti AEM come organizzazioni IMS e le loro istanze come contesti di prodotto. Gli amministratori di sistema e prodotti dei clienti potranno gestire l&#39;accesso alle istanze
* I servizi gestiti AEM sincronizzeranno le topologie dei clienti con Admin Console. Nell’Admin Console sarà presente un’istanza del contesto prodotto dei servizi gestiti AEM per istanza.
* Profili di prodotto in Admin Console determineranno a quali istanze un utente può accedere
* È supportata l&#39;autenticazione federativa tramite provider di identità conformi SAML 2
* Saranno supportati solo Enterprise ID o Federated ID (per il cliente Single Sign-On), non gli Adobe ID personali.
* La gestione degli utenti (in Adobe Admin Console) continuerà a essere di proprietà degli amministratori dei clienti.

## Architettura {#architecture}

L&#39;autenticazione IMS funziona utilizzando il protocollo OAuth tra AEM e l&#39;endpoint Adobe IMS. Dopo aver aggiunto un utente a IMS e avere un’identità Adobe, può accedere alle istanze dei servizi gestiti AEM utilizzando le credenziali IMS.

Il flusso di accesso dell&#39;utente è riportato di seguito, l&#39;utente verrà reindirizzato a IMS ed eventualmente all&#39;IDP del cliente per la convalida SSO e quindi reindirizzato nuovamente ad AEM.

![image2018-9-23_23-55-8](assets/image2018-9-23_23-55-8.png)

## Come impostare {#how-to-set-up}

### Organizzazione in Admin Console {#onboarding-organizations-to-admin-console}

L&#39;accesso del cliente ad Admin Console è un prerequisito per utilizzare Adobe IMS per l&#39;autenticazione AEM.

Come primo passo, i clienti devono disporre di un&#39;organizzazione con provisioning in Adobe IMS. I clienti Adobe Enterprise sono rappresentati come organizzazioni IMS in [Adobe Admin Console](https://helpx.adobe.com/enterprise/using/admin-console.html).

I clienti dei servizi gestiti AEM devono già disporre di un&#39;organizzazione predisposta e, nell&#39;ambito del provisioning IMS, le istanze dei clienti saranno rese disponibili nell&#39;Admin Console per la gestione delle adesioni e dell&#39;accesso degli utenti.

Il passaggio a IMS per l&#39;autenticazione degli utenti sarà uno sforzo congiunto tra AMS e i clienti, con ciascuno dei quali i flussi di lavoro saranno completati.

Una volta che un cliente esiste come organizzazione IMS e AMS ha effettuato il provisioning del cliente per IMS, questo è il riepilogo dei flussi di lavoro di configurazione richiesti:

![image2018-9-23_23-33-25](assets/image2018-9-23_23-33-25.png)

1. L&#39;amministratore di sistema designato riceve un invito ad accedere ad Admin Console
1. L&#39;amministratore di sistema richiede il dominio per confermare la proprietà del dominio (in questo esempio acme.com)
1. L&#39;amministratore di sistema imposta le directory utente
1. L&#39;amministratore di sistema configura il provider di identità (IDP) nell&#39;Admin Console per l&#39;impostazione SSO.
1. L&#39;amministratore AEM gestisce i gruppi, le autorizzazioni e i privilegi locali come al solito. Consultate Sincronizzazione di utenti e gruppi

>[!NOTE]
>
>Per ulteriori informazioni su Adobe Identity Management Basics, compresa la configurazione IDP, consultate l&#39;articolo [in questa pagina.](https://helpx.adobe.com/enterprise/using/set-up-identity.html)
>
>Per ulteriori informazioni sull&#39;amministrazione Enterprise e l&#39;Admin Console, consulta l&#39;articolo [in questa pagina](https://helpx.adobe.com/enterprise/managing/user-guide.html).

### Accesso degli utenti ad Admin Console {#onboarding-users-to-the-admin-console}

Esistono tre modi per integrare gli utenti a seconda delle dimensioni del cliente e delle loro preferenze:

1. Creazione manuale di utenti e gruppi in Admin Console
1. Caricare un file CSV con gli utenti
1. Sincronizzare utenti e gruppi dall&#39;Active Directory aziendale del cliente.

#### Aggiunta manuale tramite l’interfaccia utente di Admin Console {#manual-addition-through-admin-console-ui}

Gli utenti e i gruppi possono essere creati manualmente nell’interfaccia utente di Admin Console. Questo metodo può essere utilizzato se non dispone di un numero elevato di utenti da gestire. Ad esempio, meno di 50 utenti AEM.

Gli utenti possono anche essere creati manualmente se il cliente utilizza già questo metodo per amministrare altri prodotti Adobe come Analytics, Target o le applicazioni Creative Cloud.

![image2018-9-23_20-39-9](assets/image2018-9-23_20-39-9.png)

#### Caricamento file nell’interfaccia utente di Admin Console {#file-upload-in-the-admin-console-ui}

Per semplificare la gestione della creazione di utenti, potete caricare un file CSV per aggiungere utenti in massa:

![image2018-9-23_18-59-57](assets/image2018-9-23_18-59-57.png)

#### Strumento di sincronizzazione utenti {#user-sync-tool}

Lo strumento di sincronizzazione utenti (UST in breve) consente ai clienti aziendali di creare o gestire utenti Adobe che utilizzano Active Directory o altri servizi di directory OpenLDAP testati. Gli utenti di destinazione sono amministratori di identità IT (Enterprise Directory e System Admins) che potranno installare e configurare lo strumento. Lo strumento open source è personalizzabile in modo che i clienti possano modificarlo in base alle proprie esigenze specifiche.

Durante l&#39;esecuzione della sincronizzazione utenti, recupera un elenco di utenti da Active Directory dell&#39;organizzazione (o da qualsiasi altra origine dati compatibile) e lo confronta con l&#39;elenco di utenti all&#39;interno di Admin Console. Quindi chiama l’API di gestione utenti Adobe in modo che Admin Console sia sincronizzato con la directory dell’organizzazione. Il flusso di variazione è interamente unidirezionale; le modifiche effettuate in Admin Console non vengono inviate alla directory.

Lo strumento consente all&#39;amministratore di sistema di mappare i gruppi di utenti nella directory del cliente con la configurazione di prodotto e i gruppi di utenti nell&#39;Admin Console; la nuova versione UST consente inoltre la creazione dinamica di gruppi di utenti nell&#39;Admin Console.

Per configurare la sincronizzazione utenti, l&#39;organizzazione deve creare un set di credenziali nello stesso modo in cui utilizzerebbero l&#39;API [di gestione](https://www.adobe.io/apis/cloudplatform/usermanagement/docs/setup.html)utente.

![image2018-9-23_13-36-56](assets/image2018-9-23_13-36-56.png)

La sincronizzazione utenti viene distribuita tramite l’archivio di Adobe Github nel seguente percorso:

[https://github.com/adobe-apiplatform/user-sync.py/releases/latest](https://github.com/adobe-apiplatform/user-sync.py/releases/latest)

Una versione precedente alla release 2.4RC1 è disponibile con il supporto per la creazione di gruppi dinamici ed è disponibile qui: [https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1](https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1)

Le funzioni principali di questa versione sono la possibilità di mappare dinamicamente i nuovi gruppi LDAP per l’iscrizione degli utenti nell’Admin Console, nonché la creazione di gruppi di utenti dinamici.

Ulteriori informazioni sulle nuove funzioni del gruppo sono disponibili qui:

[https://github.com/adobe-apiplatform/user-sync.py/blob/v2/docs/en/user-manual/advanced_configuration](https://github.com/adobe-apiplatform/user-sync.py/blob/v2/docs/en/user-manual/advanced_configuration.md#additional-group-options)

>[!NOTE]
>
>Per ulteriori informazioni sullo strumento di sincronizzazione utenti, consulta la pagina [della](https://adobe-apiplatform.github.io/user-sync.py/en/)documentazione.
>
>
>Lo strumento di sincronizzazione utenti deve registrarsi come UMAPI client di I/O Adobe utilizzando la procedura descritta [qui](https://adobe-apiplatform.github.io/umapi-documentation/en/UM_Authentication.html).
>
>La documentazione della console Adobe I/O è disponibile [qui](https://www.adobe.io/apis/cloudplatform/console.html).
>
>
>L&#39;API di gestione utente utilizzata dallo strumento di sincronizzazione degli utenti è trattata in questa [posizione](https://www.adobe.io/apis/cloudplatform/umapi-new.html).

>[!NOTE]
>
>La configurazione AEM IMS verrà gestita dal team Adobe Managed Services. Tuttavia, l&#39;amministratore del cliente può modificarlo in base alle proprie esigenze (ad esempio, Appartenenza automatica al gruppo o Mappatura gruppo). Il client IMS verrà registrato anche dal team dei servizi gestiti.

## Guida all’uso {#how-to-use}

### Gestione di prodotti e accesso utente in Admin Console {#managing-products-and-user-access-in-admin-console}

Quando l&#39;amministratore del prodotto del cliente accede ad Admin Console, visualizzeranno più istanze del contesto del prodotto dei servizi gestiti AEM, come illustrato di seguito:

![screen_shot_2018-09-17at105804pm](assets/screen_shot_2018-09-17at105804pm.png)

In questo esempio, l’organizzazione *AEM-MS-Onboard* dispone di 32 istanze che si estendono su topologie e ambienti diversi come Stage, Prod, ecc.

![screen_shot_2018-09-17at105517pm](assets/screen_shot_2018-09-17at105517pm.png)

I dettagli dell’istanza possono essere verificati per identificare l’istanza:

![screen_shot_2018-09-17at105601pm](assets/screen_shot_2018-09-17at105601pm.png)

In ciascuna istanza Contesto prodotto, sarà associato un profilo di prodotto. Questo profilo di prodotto viene utilizzato per assegnare l&#39;accesso a utenti e gruppi.

![image2018-9-18_7-48-50](assets/image2018-9-18_7-48-50.png)

Tutti gli utenti e i gruppi aggiunti sotto questo profilo di prodotto potranno accedere a tale istanza come mostrato nell&#39;esempio seguente:

![screen_shot_2018-09-17at105623pm](assets/screen_shot_2018-09-17at105623pm.png)

### Accesso ad AEM {#logging-into-aem}

#### Login amministratore locale {#local-admin-login}

AEM può continuare a supportare gli accessi locali per gli utenti Admin, poiché la schermata di accesso dispone di un’opzione per accedere localmente:

![screen_shot_2018-09-18at121056am](assets/screen_shot_2018-09-18at121056am.png)

#### Login basato su IMS {#ims-based-login}

Per altri utenti, l&#39;accesso basato su IMS può essere utilizzato una volta che IMS è configurato sull&#39;istanza. L&#39;utente farà clic sul pulsante **Accedi con Adobe** , come illustrato di seguito:

![image2018-9-18_0-10-32](assets/image2018-9-18_0-10-32.png)

Vengono quindi reindirizzati alla schermata di accesso IMS e immettono le proprie credenziali:

![screen_shot_2018-09-17at115629pm](assets/screen_shot_2018-09-17at115629pm.png)

Se durante la configurazione iniziale di Admin Console è configurato un IDP federato, l&#39;utente verrà reindirizzato all&#39;IDP del cliente per SSO.

L&#39;IDP è Okta nell&#39;esempio seguente:

![screen_shot_2018-09-17at15734pm](assets/screen_shot_2018-09-17at115734pm.png)

Al termine dell&#39;autenticazione, l&#39;utente verrà reindirizzato ad AEM e ha effettuato l&#39;accesso:

![screen_shot_2018-09-18at120124am](assets/screen_shot_2018-09-18at120124am.png)

### Migrazione degli utenti esistenti {#migrating-existing-users}

Per le istanze AEM esistenti che utilizzano un altro metodo di autenticazione e che ora vengono trasferite a IMS, è necessario effettuare una migrazione.

Gli utenti esistenti nell’archivio AEM (originati localmente, tramite LDAP o SAML) possono essere migrati a IMS come IDP utilizzando l’Utilità di migrazione degli utenti.

Questa utility verrà eseguita dal team AMS come parte del provisioning IMS.

### Gestione di autorizzazioni e ACL in AEM {#managing-permissions-and-acls-in-aem}

Il controllo degli accessi e le autorizzazioni continueranno a essere gestiti in AEM, questo può essere ottenuto separando i gruppi utenti da IMS (ad esempio AEM-GRP-008 nell’esempio di seguito) e i gruppi locali in cui sono definiti le autorizzazioni e il controllo degli accessi. I gruppi di utenti sincronizzati da IMS possono essere assegnati a gruppi locali e ereditare le autorizzazioni.

Nell&#39;esempio seguente, come esempio, vengono aggiunti gruppi sincronizzati al gruppo *Dam_Users* locale.

In questo caso, un utente è stato assegnato anche ad alcuni gruppi nell’Admin Console. (Gli utenti e i gruppi possono essere sincronizzati da LDAP tramite lo strumento di sincronizzazione utenti o creati localmente. Consultate la sezione **Utenti onboarding in Admin Console** sopra).

&amp;ast;Si noti che i gruppi di utenti vengono sincronizzati solo quando gli utenti accedono all&#39;istanza, per i clienti che hanno un numero elevato di utenti e gruppi, AMS può eseguire un&#39;utility di sincronizzazione di gruppo per preacquisire i gruppi per il controllo degli accessi e la gestione delle autorizzazioni descritte in precedenza.

![screen_shot_2018-09-17at94207pm](assets/screen_shot_2018-09-17at94207pm.png)

L’utente fa parte dei seguenti gruppi in IMS:

![screen_shot_2018-09-17at94237pm](assets/screen_shot_2018-09-17at94237pm.png)

Quando l’utente accede, le appartenenze al gruppo vengono sincronizzate, come illustrato di seguito:

![screen_shot_2018-09-17at94033pm](assets/screen_shot_2018-09-17at94033pm.png)

In AEM, i gruppi di utenti sincronizzati da IMS possono essere aggiunti come membri a gruppi locali esistenti, ad esempio Utenti DAM.

![screen_shot_2018-09-17at95804pm](assets/screen_shot_2018-09-17at95804pm.png)

Come mostrato di seguito, il gruppo *AEM-GRP_008* eredita i privilegi e le autorizzazioni degli utenti DAM. Questo è un modo efficace per gestire le autorizzazioni per i gruppi sincronizzati ed è comunemente utilizzato anche nei metodi di autenticazione basati su LDAP.

![screen_shot_2018-09-17at110505pm](assets/screen_shot_2018-09-17at110505pm.png)

