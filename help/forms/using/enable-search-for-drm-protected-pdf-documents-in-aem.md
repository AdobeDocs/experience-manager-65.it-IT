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
source-git-commit: 8e724af4d69cb859537dd088119aaca652ea3931

---


# Abilitare AEM per la ricerca di documenti PDF protetti per la protezione dei documenti{#enable-aem-to-search-document-security-protected-pdf-documents}

La ricerca AEM consente di cercare e individuare le risorse AEM e di eseguire ricerche di testo in vari formati di documento comunemente utilizzati, quali file di testo normale, documenti Microsoft Office e documenti PDF. Potete anche estendere la ricerca nativa per eseguire la ricerca full-text sui documenti [PDF protetti tramite AEM Document Security](../../forms/using/admin-help/document-security.md). Per consentire ad AEM di eseguire ricerche full-text su tali documenti, effettuate le seguenti operazioni:

1. Stabilire una connessione sicura
1. Indicizzare un esempio di documento PDF protetto tramite criterio

## Prerequisiti {#prerequisites}

* Se utilizzi AEM Forms su OSGi:

   * Installate il pacchetto [](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) AEM Forms Document Security Indexer nel server AEM Forms.

   * Verifica che AEM Forms su JEE Server sia attivato ed in esecuzione e che la protezione dei documenti sia installata sui corrispondenti AEM Forms su JEE Server. Per indicizzare il documento protetto è necessario il modulo AEM sul server JEE.

* Se si utilizza solo AEM Forms su un server JEE, il pacchetto dell&#39;indicizzatore è già installato.
* Verificate che tutti i bundle siano pronti e in esecuzione. Se tutti i bundle non sono attivi, attendete che tutti i bundle siano pronti e in esecuzione.

   * Per AEM Forms su OSGi, i bundle sono elencati in https://[server]:[port]/system/console/bundle.
   * Per AEM Forms su JEE, i bundle sono elencati in https://[server]:[port]/[context-path]/system/console/bundle. Ad esempio https://localhost:8080/lc/system/console/bundles.

* Inserite nella whitelist il pacchetto *sun.util.Calendar* . Per inserire in una whitelist il pacchetto, effettuate le seguenti operazioni:

   1. Aprite la console Web di AEM. L’URL è https://[server]:[port]/system/console/configMgr.
   1. Individua e apri la configurazione **del firewall di** deserializzazione.

   1. Aggiungete il pacchetto sun.util.calendar al campo Whitelist class o package prefix, quindi fate clic su **Salva**.

### Stabilire una connessione sicura tra gli stack AEM Forms JEE e OSGi {#establish-a-secure-connection-between-aem-forms-jee-and-osgi-stacks}

È possibile utilizzare uno dei seguenti metodi per stabilire la connessione protetta:

* Configurare Adobe LiveCycle Client SDK Bundle con AEM Forms sulle credenziali di amministratore JEE
* Configurare Adobe LiveCycle Client SDK Bundle tramite autenticazione reciproca

#### Configurare Adobe LiveCycle Client SDK Bundle con AEM Forms sulle credenziali di amministratore JEE {#configure-adobe-livecycle-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. Aprite la console Web di AEM. L’URL è https://[server]:[port]/system/console/configMgr.
1. Individua e apri il pacchetto SDK per client **Adobe LiveCycle**. Specificare il valore per i campi seguenti:

   * **** URL server: Specificate l&#39;URL HTTPS di AEM Forms sul server JEE. Per abilitare la comunicazione mediante https, riavviate il server con il parametro -Djavax.net.ssl.trustStore=&lt;percorso di AEM Forms su file dell&#39;archivio di chiavi JEE>.
   * **Nome** servizio: Aggiungete RightsManagementService all&#39;elenco dei servizi specificati.
   * **** Nome utente: Specifica il nome utente dell’account AEM Forms su JEE da utilizzare per avviare chiamate dal server AEM. L&#39;account specificato deve disporre delle autorizzazioni necessarie per avviare Document Services nel server AEM Forms su JEE.
   * **Password**: Specifica la password dell&#39;account AEM Forms su JEE indicato nel campo Nome utente.
   Fai clic su **Salva**. AEM è abilitato per la ricerca di documenti PDF protetti per la protezione dei documenti.

#### Configurare Adobe LiveCycle Client SDK Bundle tramite autenticazione reciproca {#configure-adobe-livecycle-client-sdk-bundle-using-mutual-authentication}

1. Abilita autenticazione reciproca per AEM Forms su JEE. Per informazioni dettagliate, consultate [CAC e Autenticazione](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html)reciproca.
1. Aprite la console Web di AEM. L’URL è https://[server]:[port]/system/console/configMgr.
1. Individua e apri il pacchetto SDK **client** Adobe LiveCycle. Specificate il valore per le seguenti proprietà:

   * **URL** server: Specificate l&#39;URL HTTPS di AEM Forms sul server JEE. Per abilitare la comunicazione mediante https, riavviate il server AEM con il parametro -Djavax.net.ssl.trustStore=&lt;percorso di AEM Forms su JEE keystore file>.
   * **Abilita SSL** bidirezionale: Abilitate l’opzione Abilita SSL bidirezionale.
   * **URL** file KeyStore: Specificate l’URL del file dell’archivio di chiavi.
   * **URL** file TrustStore: Specificate l&#39;URL del file truststore.
   * **Password** archivio chiavi: Specificate la password per il file dell&#39;archivio di chiavi.
   * **TrustStorePassword**: Specificate la password per il file dell&#39;archivio attendibili.
   * **Nome** servizio: Aggiungete RightsManagementService all&#39;elenco dei servizi specificati.
   Fai clic su **Salva**. AEM è abilitato per la ricerca di documenti PDF protetti per la protezione dei documenti

### Indicizzare un esempio di documento PDF protetto tramite criterio {#index-a-sample-policy-protected-pdf-document}

1. Accedi a Risorse AEM come amministratore.
1. Create una cartella in AEM Digital Asset Manager e caricate i documenti PDF protetti tramite criterio nella nuova cartella creata.

   Ora potete effettuare ricerche nei documenti protetti tramite criterio tramite AEM Search.

