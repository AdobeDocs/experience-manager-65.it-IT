---
title: Abilitare AEM per effettuare ricerche nei documenti PDF protetti per la protezione dei documenti
seo-title: Abilitare AEM per effettuare ricerche nei documenti PDF protetti per la protezione dei documenti
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


# Abilitare AEM cercare documenti PDF protetti per la protezione dei documenti{#enable-aem-to-search-document-security-protected-pdf-documents}

AEM ricerca è in grado di cercare e individuare AEM risorse ed eseguire ricerche di testo in vari formati di documento comunemente utilizzati, quali file di testo normale, documenti di Microsoft Office e documenti PDF. È inoltre possibile estendere la ricerca nativa per eseguire la ricerca full-text su [documenti PDF protetti con AEM Document Security](../../forms/using/admin-help/document-security.md). Per abilitare AEM eseguire la ricerca full-text su tali documenti, effettuare le seguenti operazioni:

1. Stabilire una connessione sicura
1. Indicizzazione di un documento PDF protetto tramite criterio di esempio

## Prerequisiti {#prerequisites}

* Se utilizzate  AEM Forms su OSGi:

   * Installate [ pacchetto AEM Forms Document Security Indexer](https://helpx.adobe.com/it/aem-forms/kb/aem-forms-releases.html) sul server AEM Forms .

   * Verificare che un AEM Forms  sul server JEE sia attivato e in esecuzione e che la protezione dei documenti sia installata  AEM Forms corrispondente sul server JEE. Il modulo AEM sul server JEE è necessario per indicizzare il documento protetto.

* Se utilizzate solo  AEM Forms sul server JEE, il pacchetto dell&#39;indicizzatore è già installato.
* Verificate che tutti i bundle siano pronti e in esecuzione. Se tutti i bundle non sono attivi, attendete che tutti i bundle siano pronti e in esecuzione.

   * Per  AEM Forms su OSGi, i bundle sono elencati in https://&#39;[server]:[port]&#39;/system/console/bundle.
   * Per  AEM Forms su JEE, i bundle sono elencati in https://&#39;[server]:[port]&#39;/[context-path]/system/console/bundle. Ad esempio https://localhost:8080/lc/system/console/bundles.

* Aggiungete il pacchetto *sun.util.Calendar* al inserire nell&#39;elenco Consentiti . Per aggiungere il pacchetto al inserire nell&#39;elenco Consentiti di , effettuate le seguenti operazioni:

   1. Apri AEM console Web. L&#39;URL è https://&#39;[server]:[porta]&#39;/system/console/configMgr.
   1. Individuare e aprire **Configurazione firewall di deserializzazione**.

   1. Aggiungete il pacchetto sun.util.calendar al campo delle classi o dei prefissi del pacchetto Inseriti nell&#39;elenco Consentiti e fate clic su **Save**.

### Stabilire una connessione sicura tra  stack AEM Forms JEE e OSGi {#establish-a-secure-connection-between-aem-forms-jee-and-osgi-stacks}

È possibile utilizzare uno dei seguenti metodi per stabilire la connessione protetta:

* Configurare  Adobe LiveCycle pacchetto SDK client con  AEM Forms sulle credenziali di amministratore JEE
* Configurare  Adobe LiveCycle SDK Bundle client utilizzando l&#39;autenticazione reciproca

#### Configurare  Adobe LiveCycle pacchetto SDK client con  AEM Forms sulle credenziali di amministrazione JEE {#configure-adobe-livecycle-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. Apri AEM console Web. L&#39;URL è https://&#39;[server]:[porta]&#39;/system/console/configMgr.
1. Individua e apri il **LiveCycle di Adobe Client SDK Bundle**. Specificare il valore per i campi seguenti:

   * **URL server:** specifica URL HTTPS di  AEM Forms sul server JEE. Per abilitare la comunicazione tramite https, riavviate il server con il parametro -Djavax.net.ssl.trustStore=&lt;percorso di  AEM Forms sul file dell&#39;archivio di chiavi JEE>.
   * **Nome** servizio: Aggiungete RightsManagementService all&#39;elenco dei servizi specificati.
   * **Nome utente:** specifica il nome utente dell&#39;AEM Forms  sull&#39;account JEE da utilizzare per avviare chiamate da AEM server. L&#39;account specificato deve disporre delle autorizzazioni per avviare Document Services sull&#39;AEM Forms  sul server JEE.
   * **Password**: Specificate la password dell&#39;AEM Forms  sull&#39;account JEE indicato nel campo Nome utente.

   Fai clic su **Salva**. AEM è abilitata per la ricerca di documenti PDF protetti per la protezione dei documenti.

#### Configurare  Adobe LiveCycle SDK Bundle client utilizzando l&#39;autenticazione reciproca {#configure-adobe-livecycle-client-sdk-bundle-using-mutual-authentication}

1. Abilitare l&#39;autenticazione reciproca per  AEM Forms su JEE. Per informazioni dettagliate, vedere [CAC and Mutual Authentication](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html).
1. Apri AEM console Web. L&#39;URL è https://&#39;[server]:[porta]&#39;/system/console/configMgr.
1. Individuate e aprite il pacchetto **LiveCycle Client SDK**. Specificate il valore per le seguenti proprietà:

   * **URL** server: Specificate l&#39;URL HTTPS di  AEM Forms sul server JEE. Per abilitare la comunicazione tramite https, riavviate il server AEM con il parametro -Djavax.net.ssl.trustStore=&lt;percorso di  AEM Forms su file di keystore JEE>.
   * **Abilita SSL** bidirezionale: Abilitate l’opzione Abilita SSL bidirezionale.
   * **URL** file KeyStore: Specificate l&#39;URL del file dell&#39;archivio di chiavi.
   * **URL** file TrustStore: Specificate l&#39;URL del file truststore.
   * **Password** archivio chiavi: Specificate la password per il file dell&#39;archivio di chiavi.
   * **TrustStorePassword**: Specificate la password per il file dell&#39;archivio attendibili.
   * **Nome** servizio: Aggiungete RightsManagementService all&#39;elenco dei servizi specificati.

   Fai clic su **Salva**. AEM è abilitata per la ricerca in documenti PDF protetti per la protezione dei documenti

### Indicizzazione di un documento PDF protetto tramite criterio di esempio {#index-a-sample-policy-protected-pdf-document}

1. Accedete a  AEM Assets come amministratore.
1. Create una cartella in AEM Digital Asset Manager e caricate i documenti PDF protetti tramite criterio nella nuova cartella creata.

   Ora è possibile effettuare ricerche nei documenti protetti tramite criterio tramite AEM ricerca.

