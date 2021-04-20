---
title: Abilitare AEM per la ricerca di documenti PDF protetti da protezione dei documenti e documenti di Microsoft Office
seo-title: Abilitare AEM per la ricerca di documenti PDF protetti da protezione dei documenti e documenti di Microsoft Office
description: Scopri come abilitare la ricerca AEM nativa per eseguire la ricerca full-text sui documenti PDF protetti da DRM.
seo-description: Scopri come abilitare la ricerca AEM nativa per eseguire la ricerca full-text sui documenti PDF protetti da DRM.
uuid: dba882f8-bad4-4122-a0df-03cf087afb23
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7eebef08-83b9-4b56-90ec-35ab3b0c27e8
noindex: true
feature: Document Security
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 1%

---


# Abilita AEM per cercare documenti PDF protetti da protezione dei documenti e documenti Microsoft Office{#enable-aem-to-search-document-security-protected-pdf-and-microsoft-office-documents}

Adobe Experience Manager fornisce un’interfaccia utente per cercare e individuare varie risorse memorizzate in AEM. La ricerca nativa è in grado di cercare e individuare AEM risorse ed eseguire ricerche di testo in vari formati di documenti comunemente utilizzati, ad esempio file di testo normale, documenti di Microsoft Office e documenti PDF. È inoltre possibile estendere e abilitare la ricerca nativa per eseguire la ricerca full-text sui documenti PDF e Microsoft Office protetti da DRM.

Per abilitare AEM per la ricerca di documenti PDF e Microsoft Office protetti da protezione dei documenti, eseguire le operazioni seguenti:

## Prima di iniziare {#before-you-start}

* Installa e configura la protezione dei documenti AEM Forms.
* Aggiungi il pacchetto sun.util.calendar all&#39;inserire nell&#39;elenco Consentiti della **configurazione del firewall di deserializzazione.** La configurazione è elencata in  `https://'[server]:[port]'/system/console/configMgr`.
* Assicurati che tutti i bundle AEM siano in esecuzione. I bundle sono elencati in `https://'[server]:[port]'/system/console/bundles`. Se tutti i bundle non sono attivi, attendi e controlla lo stato dei bundle dopo qualche minuto.

## Stabilire una connessione sicura all’interno del flusso di lavoro di AEM Forms (AEM Forms su JEE) {#establish-a-secure-connection-within-aem-forms-workflow-aem-forms-on-jee}

Una connessione sicura consente un flusso continuo di informazioni tra AEM Forms su JEE e i servizi OSGi in esecuzione sullo stesso server. Utilizzare uno dei seguenti metodi per stabilire una connessione sicura:

* Configurare il bundle AEM Forms Client SDK con le credenziali di amministratore AEM Forms su JEE
* Configurare AEM Forms Client SDK Bundle utilizzando l’autenticazione reciproca

### Configurare il bundle AEM Forms Client SDK con AEM Forms sulle credenziali di amministratore JEE {#configure-aem-forms-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. Apri AEM gestione della configurazione e accedi come amministratore. L&#39;URL predefinito è https://&lt;serverName>:&lt;port>/lc/system/console/configMgr.
1. Cerca e apri il bundle AEM Forms Client SDK. Specifica il valore per le seguenti proprietà:

   * **URL server:** specifica l’URL HTTP di AEM Forms sul server JEE. Per abilitare la comunicazione su https, riavvia AEM Forms sul server JEE con il parametro -Djavax.net.ssl.trustStore=&lt;path of AEM Forms on JEE keystore file> .
   * **Nome** servizio: Aggiungi RightsManagementService all’elenco dei servizi specificati.
   * **Nome utente:** specifica il nome utente dell’account AEM Forms su JEE da utilizzare per avviare chiamate da AEM Forms sul server JEE. L&#39;account specificato deve disporre delle autorizzazioni per richiamare Document Services su AEM Forms sul server JEE.
   * **Password**: Specifica la password dell’account AEM Forms su JEE menzionato nel campo Nome utente .

   Fai clic su **Salva**. AEM è abilitato per la ricerca di documenti PDF e Microsoft Office protetti da protezione dei documenti.

### Configurare AEM Forms Client SDK Bundle utilizzando l&#39;autenticazione reciproca {#configure-aem-forms-client-sdk-bundle-using-mutual-authentication}

1. Abilita l’autenticazione reciproca per AEM Forms su JEE. Per informazioni dettagliate, consulta [CAC e Autenticazione reciproca](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html).
1. Apri AEM gestione della configurazione e accedi come amministratore. L&#39;URL predefinito è https://&lt;serverName>:&lt;port>/lc/system/console/configMgr.
1. Cerca e apri il bundle AEM Forms Client SDK. Specifica il valore per le seguenti proprietà:

   * **URL server:** specifica l’URL HTTPS di AEM Forms sul server JEE. Per abilitare la comunicazione su https, riavvia AEM Forms sul server JEE con il parametro -Djavax.net.ssl.trustStore=&lt;path of AEM Forms on JEE keystore file> .
   * **Abilita SSL** a 2 vie: Abilita l’opzione Abilita SSL a 2 vie.
   * **URL** del file KeyStore: Specifica l&#39;URL del file dell&#39;archivio chiavi.
   * **URL** del file TrustStore: Specifica l’URL del file truststore.
   * **Password** archivio chiavi: Specifica la password per il file dell&#39;archivio chiavi.
   * **TrustStorePassword**: Specifica la password per il file truststore.
   * **Nome** servizio: Aggiungi RightsManagementService all’elenco dei servizi specificati.

   Fai clic su **Salva**. AEM abilitato per la ricerca di documenti PDF e Microsoft Office protetti da protezione dei documenti

## Indice di un documento PDF o Microsoft Office protetto da policy di esempio {#index-a-sample-policy-protected-pdf-or-microsoft-office-document}

1. Accedi ad AEM Assets come amministratore.
1. Crea una cartella in AEM Digital Asset Manager e carica un documento PDF o Microsoft Office protetto da policy nella cartella appena creata. Ora, cerca il contenuto dei documenti protetti da policy utilizzando AEM ricerca. Deve restituire il documento contenente testo ricercato.

