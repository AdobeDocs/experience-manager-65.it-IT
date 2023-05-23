---
title: Consentire all'AEM di effettuare ricerche nei documenti PDF e Microsoft Office protetti da Document Security
seo-title: Enable AEM to search document security protected PDF and Microsoft Office documents
description: Scopri come abilitare la ricerca AEM nativa per eseguire ricerche full-text sui documenti di PDF protetti da DRM.
seo-description: Learn how to enable native AEM search to perform full-text search on DRM protected PDF documents.
uuid: dba882f8-bad4-4122-a0df-03cf087afb23
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7eebef08-83b9-4b56-90ec-35ab3b0c27e8
noindex: true
feature: Document Security
exl-id: 91cbd1f1-d53d-455b-8d2c-6918b521db81
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 1%

---

# Consentire all&#39;AEM di effettuare ricerche nei documenti PDF e Microsoft Office protetti da Document Security{#enable-aem-to-search-document-security-protected-pdf-and-microsoft-office-documents}

Adobe Experience Manager fornisce un’interfaccia utente per cercare e individuare varie risorse memorizzate nell’AEM. La ricerca nativa consente di cercare e individuare le risorse AEM ed eseguire ricerche di testo in vari formati di documenti di uso comune, ad esempio file di testo normale, documenti di Microsoft Office e documenti di PDF. È inoltre possibile estendere e abilitare la ricerca nativa per eseguire ricerche full-text su documenti PDF protetti da DRM e Microsoft Office.

Per consentire all’AEM di effettuare ricerche nei documenti PDF e Microsoft Office protetti da Document Security, effettua le seguenti operazioni:

## Prima di iniziare {#before-you-start}

* Installa e configura AEM Forms Document Security.
* Aggiungi package sun.util.calendar al inserisco nell&#39;elenco Consentiti di del **Configurazione firewall deserializzazione.** La configurazione è elencata in `https://'[server]:[port]'/system/console/configMgr`.
* Assicurati che tutti i bundle AEM siano funzionanti. I bundle sono elencati in `https://'[server]:[port]'/system/console/bundles`. Se non tutti i bundle sono attivi, attendi e controlla lo stato dei bundle dopo per alcuni minuti.

## Stabilire una connessione sicura all’interno del flusso di lavoro di AEM Forms (AEM Forms on JEE) {#establish-a-secure-connection-within-aem-forms-workflow-aem-forms-on-jee}

Una connessione sicura consente un flusso ininterrotto di informazioni tra AEM Forms su JEE e i servizi OSGi in esecuzione sullo stesso server. Per stabilire una connessione sicura, utilizzare uno dei metodi seguenti:

* Configurare il bundle AEM Forms Client SDK con le credenziali amministratore AEM Forms su JEE
* Configurare il bundle AEM Forms Client SDK utilizzando l’autenticazione reciproca

### Configurare il bundle AEM Forms Client SDK con le credenziali amministratore AEM Forms su JEE {#configure-aem-forms-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. Apri Gestione configurazione AEM e accedi come amministratore. L’URL predefinito è https://&lt;servername>:&lt;port>/lc/system/console/configMgr.
1. Cerca e apri il bundle AEM Forms Client SDK. Specifica il valore per le seguenti proprietà:

   * **URL server:** Specifica l’URL HTTP di AEM Forms sul server JEE. Per abilitare la comunicazione tramite https, riavvia il server AEM Forms su JEE con -Djavax.net.ssl.trustStore=&lt;path of=&quot;&quot; aem=&quot;&quot; forms=&quot;&quot; on=&quot;&quot; jee=&quot;&quot; keystore=&quot;&quot; file=&quot;&quot;> parametro.
   * **Nome servizio**: aggiungere RightsManagementService all&#39;elenco dei servizi specificati.
   * **Nome utente:** Specifica il nome utente dell’account AEM Forms su JEE da utilizzare per avviare chiamate da AEM Forms sul server JEE. L’account specificato deve disporre delle autorizzazioni per richiamare Document Services sul server AEM Forms su JEE.
   * **Password**: specifica la password dell’account AEM Forms su JEE indicato nel campo Nome utente.

   Fai clic su **Salva**. L’AEM è abilitato per la ricerca di documenti protetti da PDF e Microsoft Office.

### Configurare il bundle AEM Forms Client SDK utilizzando l’autenticazione reciproca {#configure-aem-forms-client-sdk-bundle-using-mutual-authentication}

1. Abilita l’autenticazione reciproca per AEM Forms su JEE. Per informazioni dettagliate, consulta [CAC e autenticazione reciproca](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html).
1. Apri Gestione configurazione AEM e accedi come amministratore. L’URL predefinito è https://&lt;servername>:&lt;port>/lc/system/console/configMgr.
1. Cerca e apri il bundle AEM Forms Client SDK. Specifica il valore per le seguenti proprietà:

   * **URL server:** Specifica l’URL HTTPS di AEM Forms sul server JEE. Per abilitare la comunicazione tramite https, riavvia il server AEM Forms su JEE con -Djavax.net.ssl.trustStore=&lt;path of=&quot;&quot; aem=&quot;&quot; forms=&quot;&quot; on=&quot;&quot; jee=&quot;&quot; keystore=&quot;&quot; file=&quot;&quot;> parametro.
   * **Abilita SSL bidirezionale**: abilita l’opzione Abilita SSL a 2 vie.
   * **URL file registro chiavi**: specifica l’URL del file keystore.
   * **URL file TrustStore**: specifica l’URL del file truststore.
   * **Password registro chiavi**: specifica la password per il file keystore.
   * **TrustStorePassword**: specifica la password per il file truststore.
   * **Nome servizio**: aggiungere RightsManagementService all&#39;elenco dei servizi specificati.

   Fai clic su **Salva**. L’AEM è abilitato per la ricerca di documenti protetti da PDF e Microsoft Office

## Indicizzare un esempio di documento PDF o Microsoft Office protetto tramite policy {#index-a-sample-policy-protected-pdf-or-microsoft-office-document}

1. Accedi ad AEM Assets come amministratore.
1. Crea una cartella in AEM Digital Asset Manager e carica un documento PDF o Microsoft Office protetto tramite policy nella cartella appena creata. Ora è possibile cercare il contenuto dei documenti protetti tramite policy utilizzando la funzione di ricerca AEM. Deve restituire il documento contenente il testo cercato.
