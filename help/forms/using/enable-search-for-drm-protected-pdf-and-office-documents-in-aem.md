---
title: Abilitare AEM per la ricerca di documenti PDF protetti per la protezione dei documenti e documenti Microsoft Office
seo-title: Abilitare AEM per la ricerca di documenti PDF protetti per la protezione dei documenti e documenti Microsoft Office
description: Scoprite come abilitare la ricerca AEM nativa per eseguire la ricerca full-text sui documenti PDF protetti da DRM.
seo-description: Scoprite come abilitare la ricerca AEM nativa per eseguire la ricerca full-text sui documenti PDF protetti da DRM.
uuid: dba882f8-bad4-4122-a0df-03cf087afb23
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7eebef08-83b9-4b56-90ec-35ab3b0c27e8
noindex: true
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Abilitare AEM per la ricerca di documenti PDF protetti per la protezione dei documenti e documenti Microsoft Office{#enable-aem-to-search-document-security-protected-pdf-and-microsoft-office-documents}

Adobe Experience Manager offre un’interfaccia utente per cercare e individuare diverse risorse memorizzate in AEM. La ricerca nativa è in grado di cercare e individuare le risorse AEM e di eseguire ricerche di testo in vari formati di documento comunemente utilizzati, quali file di testo normale, documenti di Microsoft Office e documenti PDF. È inoltre possibile estendere e abilitare la ricerca nativa per eseguire la ricerca full-text sui documenti PDF e Microsoft Office protetti da DRM.

Per abilitare AEM per la ricerca nei documenti PDF e Microsoft Office protetti per la protezione dei documenti, effettuate le seguenti operazioni:

## Prima di iniziare {#before-you-start}

* Installare e configurare la protezione dei documenti in AEM Forms.
* Aggiungete il pacchetto sun.util.calendar alla whitelist della configurazione del firewall di **deserializzazione.** La configurazione è elencata in `https://'[server]:[port]'/system/console/configMgr`.
* Verificate che tutti i bundle AEM siano pronti e in esecuzione. I bundle sono elencati in `https://'[server]:[port]'/system/console/bundles`. Se tutti i bundle non sono attivi, attendete e verificate lo stato dei bundle dopo alcuni minuti.

## Stabilire una connessione sicura nel flusso di lavoro AEM Forms (AEM Forms on JEE) {#establish-a-secure-connection-within-aem-forms-workflow-aem-forms-on-jee}

Una connessione protetta consente un flusso di informazioni continuo tra AEM Forms su JEE e i servizi OSGi in esecuzione sullo stesso server. Per stabilire una connessione protetta, utilizzare uno dei seguenti metodi:

* Configurare il pacchetto SDK per client AEM Forms con i moduli AEM sulle credenziali di amministratore JEE
* Configurare il pacchetto SDK per client AEM Forms mediante l&#39;autenticazione reciproca

### Configurare il pacchetto SDK per client AEM Forms con i moduli AEM sulle credenziali di amministratore JEE {#configure-aem-forms-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. Apri Gestione configurazione AEM e accedi come amministratore. L’URL predefinito è https://&lt;serverName>:&lt;port>/lc/system/console/configMgr.
1. Cercate e aprite il pacchetto SDK per client AEM Forms. Specificate il valore per le seguenti proprietà:

   * **URL server:** Specificate l&#39;URL HTTP di AEM Forms sul server JEE. Per abilitare la comunicazione mediante https, riavviate AEM Forms sul server JEE con il parametro -Djavax.net.ssl.trustStore=&lt;percorso di AEM Forms su JEE keystore file>.
   * **Nome** servizio: Aggiungete RightsManagementService all&#39;elenco dei servizi specificati.
   * **Nome utente:** Specificate il nome utente dell&#39;account AEM Forms su JEE da utilizzare per avviare chiamate da AEM Forms su un server JEE. L&#39;account specificato deve disporre delle autorizzazioni necessarie per richiamare Document Services sul server AEM Forms su JEE.
   * **Password**: Specifica la password dell&#39;account AEM Forms su JEE indicato nel campo Nome utente.
   Fai clic su **Salva**. AEM è abilitato per la ricerca di documenti PDF protetti per la protezione dei documenti e documenti Microsoft Office.

### Configurare il pacchetto SDK per client AEM Forms mediante l&#39;autenticazione reciproca {#configure-aem-forms-client-sdk-bundle-using-mutual-authentication}

1. Abilita autenticazione reciproca per AEM Forms su JEE. Per informazioni dettagliate, consultate [CAC e Autenticazione](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html)reciproca.
1. Apri Gestione configurazione AEM e accedi come amministratore. L’URL predefinito è https://&lt;serverName>:&lt;port>/lc/system/console/configMgr.
1. Cercate e aprite il pacchetto SDK per client AEM Forms. Specificate il valore per le seguenti proprietà:

   * **URL server:** Specificate l&#39;URL HTTPS di AEM Forms sul server JEE. Per abilitare la comunicazione mediante https, riavviate AEM Forms sul server JEE con il parametro -Djavax.net.ssl.trustStore=&lt;percorso di AEM Forms su JEE keystore file>.
   * **Abilita SSL** bidirezionale: Abilitate l’opzione Abilita SSL bidirezionale.
   * **URL** file KeyStore: Specificate l&#39;URL del file dell&#39;archivio di chiavi.
   * **URL** file TrustStore: Specificate l&#39;URL del file truststore.
   * **Password** archivio chiavi: Specificate la password per il file dell&#39;archivio di chiavi.
   * **TrustStorePassword**: Specificate la password per il file dell&#39;archivio attendibili.
   * **Nome** servizio: Aggiungete RightsManagementService all&#39;elenco dei servizi specificati.
   Fai clic su **Salva**. AEM è abilitato per la ricerca di documenti PDF protetti per la protezione dei documenti e documenti Microsoft Office

## Indicizzazione di un esempio di documento PDF o Microsoft Office protetto tramite criterio {#index-a-sample-policy-protected-pdf-or-microsoft-office-document}

1. Accedi a Risorse AEM come amministratore.
1. Create una cartella in AEM Digital Asset Manager e caricate un documento PDF o Microsoft Office protetto tramite criterio nella nuova cartella creata. A questo punto, cercate il contenuto dei documenti protetti tramite criterio tramite la ricerca AEM. Deve restituire il documento contenente testo ricercato.

