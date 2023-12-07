---
title: Consenti a AEM di effettuare ricerche nei documenti di PDF protetti da Document Security
description: Scopri come abilitare la ricerca AEM nativa per eseguire ricerche full-text sui documenti di PDF protetti da DRM.
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/working_with_document_security
docset: aem65
feature: Document Security
exl-id: 7cf17fb6-021a-473e-bc3b-27c317953002
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 0%

---

# Consenti a AEM di effettuare ricerche nei documenti di PDF protetti da Document Security{#enable-aem-to-search-document-security-protected-pdf-documents}

La funzione di ricerca AEM è in grado di cercare e individuare le risorse AEM e di eseguire ricerche testuali in vari formati di documenti comunemente utilizzati, come file di testo normale, documenti di Microsoft Office e documenti di PDF. È inoltre possibile estendere la ricerca nativa per eseguire ricerche full-text su [Documenti PDF protetti con AEM Document Security](../../forms/using/admin-help/document-security.md). Per consentire all’AEM di eseguire ricerche full-text su tali documenti, effettua le seguenti operazioni:

1. Stabilire una connessione sicura
1. Indicizzare un esempio di documento PDF protetto tramite policy

## Prerequisiti {#prerequisites}

* Se utilizzi AEM Forms su OSGi:

   * Installa [Pacchetto dell’indicizzatore di AEM Forms Document Security](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) sul server AEM Forms.

   * Assicurati che un AEM Forms sul server JEE sia in esecuzione e che la sicurezza dei documenti sia installata nel corrispondente AEM Forms sul server JEE. Per indicizzare il documento protetto è necessario il modulo AEM sul server JEE.

* Se utilizzi solo AEM Forms sul server JEE, il pacchetto di indicizzazione è già installato.
* Assicurati che tutti i bundle siano attivi e funzionanti. Se non tutti i bundle sono attivi, attendi che tutti i bundle siano attivi.

   * Per AEM Forms su OSGi, i bundle sono elencati in https://&#39;[server]:[porta]&#39;/system/console/bundle.
   * Per AEM Forms su JEE, i bundle sono elencati in https://&#39;[server]:[porta]&#39;/[context-path]/system/console/bundle. Ad esempio, https://localhost:8080/lc/system/console/bundles.

* Aggiungi il *sun.util.calendar* al elenco Consentiti di. Per aggiungere il pacchetto al inserisco nell&#39;elenco Consentiti di, effettuare le seguenti operazioni:

   1. Apri la console web AEM. L’URL è https://&#39;[server]:[porta]&#39;/system/console/configMgr.
   1. Individua e apri **Configurazione firewall deserializzazione**.

   1. Aggiungere il pacchetto sun.util.calendar al campo delle classi o dei prefissi di pacchetto Inseriti nell&#39;elenco Consentiti e fare clic su **Salva**.

### Stabilire una connessione sicura tra gli stack AEM Forms JEE e OSGi {#establish-a-secure-connection-between-aem-forms-jee-and-osgi-stacks}

Per stabilire la connessione sicura, è possibile utilizzare uno dei metodi seguenti:

* Configurare il bundle Adobe LiveCycle Client SDK con le credenziali amministratore AEM Forms su JEE
* Configurare il bundle Adobe LiveCycle Client SDK utilizzando l’autenticazione reciproca

#### Configurare il bundle Adobe LiveCycle Client SDK con le credenziali amministratore AEM Forms su JEE {#configure-adobe-livecycle-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. Apri la console web AEM. L’URL è https://&#39;[server]:[porta]&#39;/system/console/configMgr.
1. Individuare e aprire **Bundle SDK client Adobe LiveCycle**. Specifica il valore per i campi seguenti:

   * **URL server:** Specifica l’URL HTTPS di AEM Forms sul server JEE. Per abilitare la comunicazione tramite https, riavviare il server con -Djavax.net.ssl.trustStore=&lt;path of=&quot;&quot; aem=&quot;&quot; forms=&quot;&quot; on=&quot;&quot; jee=&quot;&quot; keystore=&quot;&quot; file=&quot;&quot;> parametro.
   * **Nome servizio**: aggiungere RightsManagementService all&#39;elenco dei servizi specificati.
   * **Nome utente:** Specifica il nome utente dell’account AEM Forms su JEE da utilizzare per avviare chiamate dal server AEM. L’account specificato deve disporre delle autorizzazioni necessarie per avviare i servizi documentali sul server AEM Forms su JEE.
   * **Password**: specifica la password dell’account AEM Forms su JEE indicato nel campo Nome utente.

   Clic **Salva**. AEM è abilitato per la ricerca di documenti PDF protetti da Document Security.

#### Configurare il bundle Adobe LiveCycle Client SDK utilizzando l’autenticazione reciproca {#configure-adobe-livecycle-client-sdk-bundle-using-mutual-authentication}

1. Abilita l’autenticazione reciproca per AEM Forms su JEE. Per informazioni dettagliate, consulta [CAC e autenticazione reciproca](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html).
1. Apri la console web AEM. L’URL è https://&#39;[server]:[porta]&#39;/system/console/configMgr.
1. Individuare e aprire **Adobe LiveCycle Client SDK** Pacchetto. Specifica il valore per le seguenti proprietà:

   * **URL server**: specifica l’URL HTTPS di AEM Forms sul server JEE. Per abilitare la comunicazione tramite https, riavviare il server AEM con -Djavax.net.ssl.trustStore=&lt;path of=&quot;&quot; aem=&quot;&quot; forms=&quot;&quot; on=&quot;&quot; jee=&quot;&quot; keystore=&quot;&quot; file=&quot;&quot;> parametro.
   * **Abilita SSL bidirezionale**: abilita l’opzione Abilita SSL a 2 vie.
   * **URL file registro chiavi**: specifica l’URL del file keystore.
   * **URL file TrustStore**: specifica l’URL del file truststore.
   * **Password registro chiavi**: specifica la password per il file keystore.
   * **TrustStorePassword**: specifica la password per il file truststore.
   * **Nome servizio**: aggiungere RightsManagementService all&#39;elenco dei servizi specificati.

   Clic **Salva**. L’AEM è abilitato alla ricerca di documenti PDF protetti da Document Security

### Indicizzare un esempio di documento PDF protetto tramite policy {#index-a-sample-policy-protected-pdf-document}

1. Accedi ad AEM Assets come amministratore.
1. Crea una cartella in AEM Digital Asset Manager e carica i documenti di PDF protetti tramite policy nella cartella appena creata.

   Ora è possibile eseguire ricerche nei documenti protetti tramite policy utilizzando la funzione di ricerca AEM.
