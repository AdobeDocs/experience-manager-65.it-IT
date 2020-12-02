---
title: Abilitare AEM per effettuare ricerche nei documenti PDF e Microsoft Office protetti per la protezione dei documenti
seo-title: Abilitare AEM per effettuare ricerche nei documenti PDF e Microsoft Office protetti per la protezione dei documenti
description: Scoprite come abilitare la ricerca AEM nativa per eseguire la ricerca full-text sui documenti PDF protetti da DRM.
seo-description: Scoprite come abilitare la ricerca AEM nativa per eseguire la ricerca full-text sui documenti PDF protetti da DRM.
uuid: dba882f8-bad4-4122-a0df-03cf087afb23
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7eebef08-83b9-4b56-90ec-35ab3b0c27e8
noindex: true
translation-type: tm+mt
source-git-commit: b703c59d7d913fc890c713c6e49e7d89211fd998
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 1%

---


# Abilitare AEM cercare documenti PDF protetti per la protezione dei documenti e documenti Microsoft Office{#enable-aem-to-search-document-security-protected-pdf-and-microsoft-office-documents}

Adobe Experience Manager offre un’interfaccia utente per cercare e individuare le varie risorse memorizzate in AEM. La ricerca nativa è in grado di cercare e individuare AEM risorse ed eseguire ricerche di testo in vari formati di documento comunemente utilizzati, quali file di testo normale, documenti di Microsoft Office e documenti PDF. È inoltre possibile estendere e abilitare la ricerca nativa per eseguire la ricerca full-text sui documenti PDF e Microsoft Office protetti da DRM.

Per attivare AEM per eseguire ricerche nei documenti PDF e Microsoft Office protetti da protezione dei documenti, procedere come segue:

## Prima di iniziare {#before-you-start}

* Installare e configurare  protezione dei documenti AEM Forms.
* Aggiungete il pacchetto sun.util.Calendar al inserire nell&#39;elenco Consentiti  della **configurazione del firewall di deserializzazione.** La configurazione è elencata in  `https://'[server]:[port]'/system/console/configMgr`.
* Verificate che tutti AEM bundle siano pronti e in esecuzione. I bundle sono elencati in `https://'[server]:[port]'/system/console/bundles`. Se tutti i bundle non sono attivi, attendete e verificate lo stato dei bundle dopo alcuni minuti.

## Stabilire una connessione protetta all&#39;interno  flusso di lavoro AEM Forms ( AEM Forms su JEE) {#establish-a-secure-connection-within-aem-forms-workflow-aem-forms-on-jee}

Una connessione sicura consente un flusso di informazioni senza soluzione di continuità tra  AEM Forms su JEE e i servizi OSGi in esecuzione sullo stesso server. Per stabilire una connessione protetta, utilizzare uno dei seguenti metodi:

* Configurare  AEM Forms Client SDK Bundle con  AEM Forms sulle credenziali di amministratore JEE
* Configurare  AEM Forms Client SDK Bundle mediante autenticazione reciproca

### Configurare  AEM Forms Client SDK Bundle con  AEM Forms sulle credenziali di amministrazione JEE {#configure-aem-forms-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. Aprite AEM gestione della configurazione e accedete come amministratore. L’URL predefinito è https://&lt;serverName>:&lt;port>/lc/system/console/configMgr.
1. Cercate e aprite  AEM Forms Client SDK Bundle. Specificate il valore per le seguenti proprietà:

   * **URL server:** specifica URL HTTP di  AEM Forms sul server JEE. Per abilitare la comunicazione tramite https, riavviate l&#39;AEM Forms  sul server JEE con il parametro -Djavax.net.ssl.trustStore=&lt;percorso di  AEM Forms su file di keystore JEE>.
   * **Nome** servizio: Aggiungete RightsManagementService all&#39;elenco dei servizi specificati.
   * **Nome utente:** specifica il nome utente dell&#39;AEM Forms  sull&#39;account JEE da utilizzare per avviare chiamate da  AEM Forms sul server JEE. L&#39;account specificato deve disporre delle autorizzazioni necessarie per richiamare Document Services sull&#39;AEM Forms  sul server JEE.
   * **Password**: Specificate la password dell&#39;AEM Forms  sull&#39;account JEE indicato nel campo Nome utente.

   Fai clic su **Salva**. AEM è abilitata per la ricerca di documenti PDF e Microsoft Office protetti per la protezione dei documenti.

### Configurare  AEM Forms Client SDK Bundle utilizzando l&#39;autenticazione reciproca {#configure-aem-forms-client-sdk-bundle-using-mutual-authentication}

1. Abilitare l&#39;autenticazione reciproca per  AEM Forms su JEE. Per informazioni dettagliate, vedere [CAC and Mutual Authentication](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html).
1. Aprite AEM gestione della configurazione e accedete come amministratore. L’URL predefinito è https://&lt;serverName>:&lt;port>/lc/system/console/configMgr.
1. Cercate e aprite  AEM Forms Client SDK Bundle. Specificate il valore per le seguenti proprietà:

   * **URL server:** specifica URL HTTPS di  AEM Forms sul server JEE. Per abilitare la comunicazione tramite https, riavviate l&#39;AEM Forms  sul server JEE con il parametro -Djavax.net.ssl.trustStore=&lt;percorso di  AEM Forms su file di keystore JEE>.
   * **Abilita SSL** bidirezionale: Abilitate l’opzione Abilita SSL bidirezionale.
   * **URL** file KeyStore: Specificate l&#39;URL del file dell&#39;archivio di chiavi.
   * **URL** file TrustStore: Specificate l&#39;URL del file truststore.
   * **Password** archivio chiavi: Specificate la password per il file dell&#39;archivio di chiavi.
   * **TrustStorePassword**: Specificate la password per il file dell&#39;archivio attendibili.
   * **Nome** servizio: Aggiungete RightsManagementService all&#39;elenco dei servizi specificati.

   Fai clic su **Salva**. AEM è abilitata per la ricerca di documenti PDF e Microsoft Office protetti per la protezione dei documenti

## Indicizzare un esempio di documento PDF o Microsoft Office protetto tramite criterio {#index-a-sample-policy-protected-pdf-or-microsoft-office-document}

1. Accedete a  AEM Assets come amministratore.
1. Create una cartella in AEM Digital Asset Manager e caricate un documento PDF o Microsoft Office protetto tramite criterio nella cartella appena creata. A questo punto, eseguite la ricerca nel contenuto dei documenti protetti tramite criterio tramite AEM. Deve restituire il documento contenente testo ricercato.

