---
title: Abilitare AEM per la ricerca di documenti PDF protetti per la protezione dei documenti
seo-title: Abilitare AEM per la ricerca di documenti PDF protetti per la protezione dei documenti
description: 'Scoprite come abilitare la ricerca AEM nativa per eseguire la ricerca full-text sui documenti PDF protetti da DRM.  '
seo-description: 'Scoprite come abilitare la ricerca AEM nativa per eseguire la ricerca full-text sui documenti PDF protetti da DRM.  '
uuid: ec6e5d53-a74c-4958-a389-7937d073c083
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/working_with_document_security
discoiquuid: b79c147c-f846-4e48-bec0-8b658502bb6f
docset: aem65
translation-type: tm+mt
source-git-commit: b703c59d7d913fc890c713c6e49e7d89211fd998
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 1%

---


# Abilitare AEM per la ricerca di documenti PDF protetti per la protezione dei documenti{#enable-aem-to-search-document-security-protected-pdf-documents}

La ricerca AEM consente di cercare e individuare le risorse AEM e di eseguire ricerche di testo in vari formati di documenti comunemente utilizzati, quali file di testo normale, documenti Microsoft Office e documenti PDF. Potete anche estendere la ricerca nativa per eseguire la ricerca full-text sui documenti [PDF protetti tramite AEM Document Security](../../forms/using/admin-help/document-security.md). Per consentire ad AEM di eseguire ricerche full-text su tali documenti, effettuate le seguenti operazioni:

1. Stabilire una connessione sicura
1. Indicizzazione di un documento PDF protetto tramite criterio di esempio

## Prerequisiti {#prerequisites}

* Se utilizzate AEM Forms in OSGi:

   * Installate il pacchetto [](https://helpx.adobe.com/it/aem-forms/kb/aem-forms-releases.html) AEM Forms Document Security Indexer nel server AEM Forms.

   * Verificare che un AEM Forms nel server JEE sia attivato e in esecuzione e che la protezione del documento sia installata sui AEM Forms corrispondenti nel server JEE. Per indicizzare il documento protetto è necessario il modulo AEM sul server JEE.

* Se utilizzate solo AEM Forms sul server JEE, il pacchetto dell&#39;indicizzatore è già installato.
* Verificate che tutti i bundle siano pronti e in esecuzione. Se tutti i bundle non sono attivi, attendete che tutti i bundle siano pronti e in esecuzione.

   * Per i AEM Forms su OSGi, i bundle sono elencati in https://&#39;[server]:[port]&#39;/system/console/bundle.
   * Per i AEM Forms su JEE, i bundle sono elencati in https://&#39;[server]:[port]&#39;/[context-path]/system/console/bundle. Ad esempio https://localhost:8080/lc/system/console/bundles.

* Aggiungete il pacchetto *sun.util.Calendar* all&#39;elenco consentito. Per aggiungere il pacchetto all&#39;elenco dei pacchetti consentiti, effettuate le seguenti operazioni:

   1. Aprite la console Web di AEM. L’URL è https://&#39;[server]:[port]&#39;/system/console/configMgr.
   1. Individua e apri la configurazione **del firewall di** deserializzazione.

   1. Aggiungete il pacchetto sun.util.Calendar al campo relativo alle classi o ai prefissi del pacchetto Allowlist e fate clic su **Salva**.

### Stabilire una connessione sicura tra gli stack JEE e OSGi degli AEM Forms {#establish-a-secure-connection-between-aem-forms-jee-and-osgi-stacks}

È possibile utilizzare uno dei seguenti metodi per stabilire la connessione protetta:

* Configurare Adobe LiveCycle Client SDK Bundle con AEM Forms sulle credenziali di amministratore JEE
* Configurare Adobe LiveCycle Client SDK Bundle utilizzando l&#39;autenticazione reciproca

#### Configurare Adobe LiveCycle Client SDK Bundle con AEM Forms sulle credenziali di amministratore JEE {#configure-adobe-livecycle-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. Aprite la console Web di AEM. L’URL è https://&#39;[server]:[port]&#39;/system/console/configMgr.
1. Individua e apri il pacchetto SDK per client **Adobe LiveCycle**. Specificare il valore per i campi seguenti:

   * **URL server:** Specificate l&#39;URL HTTPS dei AEM Forms sul server JEE. Per abilitare la comunicazione tramite https, riavviate il server con il parametro -Djavax.net.ssl.trustStore=&lt;percorso di AEM Forms nel file dell&#39;archivio di chiavi JEE>.
   * **Nome** servizio: Aggiungete RightsManagementService all&#39;elenco dei servizi specificati.
   * **Nome utente:** Specifica il nome utente dei AEM Forms sull’account JEE da utilizzare per avviare chiamate dal server AEM. L&#39;account specificato deve disporre delle autorizzazioni per avviare Document Services sui AEM Forms del server JEE.
   * **Password**: Specificate la password dei AEM Forms sull&#39;account JEE indicato nel campo Nome utente.

   Fai clic su **Salva**. AEM è abilitato per la ricerca di documenti PDF protetti per la protezione dei documenti.

#### Configurare Adobe LiveCycle Client SDK Bundle utilizzando l&#39;autenticazione reciproca {#configure-adobe-livecycle-client-sdk-bundle-using-mutual-authentication}

1. Abilitare l&#39;autenticazione reciproca per i AEM Forms su JEE. Per informazioni dettagliate, consultate [CAC e Autenticazione](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html)reciproca.
1. Aprite la console Web di AEM. L’URL è https://&#39;[server]:[port]&#39;/system/console/configMgr.
1. Individua e apri il pacchetto SDK **client** Adobe LiveCycle. Specificate il valore per le seguenti proprietà:

   * **URL** server: Specificate l&#39;URL HTTPS dei AEM Forms sul server JEE. Per abilitare la comunicazione tramite https, riavviate il server AEM con il parametro -Djavax.net.ssl.trustStore=&lt;percorso di AEM Forms nel file dell&#39;archivio di chiavi JEE>.
   * **Abilita SSL** bidirezionale: Abilitate l’opzione Abilita SSL bidirezionale.
   * **URL** file KeyStore: Specificate l&#39;URL del file dell&#39;archivio di chiavi.
   * **URL** file TrustStore: Specificate l&#39;URL del file truststore.
   * **Password** archivio chiavi: Specificate la password per il file dell&#39;archivio di chiavi.
   * **TrustStorePassword**: Specificate la password per il file dell&#39;archivio attendibili.
   * **Nome** servizio: Aggiungete RightsManagementService all&#39;elenco dei servizi specificati.

   Fai clic su **Salva**. AEM è abilitato per la ricerca di documenti PDF protetti per la protezione dei documenti

### Indicizzazione di un documento PDF protetto tramite criterio di esempio {#index-a-sample-policy-protected-pdf-document}

1. Accedete ai AEM Assets come amministratore.
1. Create una cartella in AEM Digital Asset Manager e caricate i documenti PDF protetti tramite criterio nella nuova cartella creata.

   Ora è possibile effettuare ricerche nei documenti protetti tramite criterio tramite AEM Search.

