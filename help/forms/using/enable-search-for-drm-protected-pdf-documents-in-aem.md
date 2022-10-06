---
title: Abilita AEM per cercare documenti PDF protetti per la protezione dei documenti
seo-title: Enable AEM to search document security protected PDF documents
description: Scopri come abilitare la ricerca AEM nativa per eseguire la ricerca full-text sui documenti PDF protetti DRM.
seo-description: Learn how to enable native AEM search to perform full-text search on DRM protected PDF documents.
uuid: ec6e5d53-a74c-4958-a389-7937d073c083
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/working_with_document_security
discoiquuid: b79c147c-f846-4e48-bec0-8b658502bb6f
docset: aem65
feature: Document Security
exl-id: 7cf17fb6-021a-473e-bc3b-27c317953002
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 1%

---

# Abilita AEM per cercare documenti PDF protetti per la protezione dei documenti{#enable-aem-to-search-document-security-protected-pdf-documents}

AEM ricerca consente di cercare e individuare AEM risorse ed eseguire ricerche di testo in vari formati di documenti comunemente utilizzati, ad esempio file di testo normale, documenti Microsoft Office e documenti PDF. Puoi anche estendere la ricerca nativa per eseguire la ricerca full-text su [Documenti PDF protetti con protezione AEM documenti](../../forms/using/admin-help/document-security.md). Per abilitare AEM per eseguire la ricerca full-text su tali documenti, effettua le seguenti operazioni:

1. Stabilire una connessione sicura
1. Indice di un documento PDF protetto da policy di esempio

## Prerequisiti {#prerequisites}

* Se utilizzi AEM Forms su OSGi:

   * Installa [Pacchetto Document Security Indexer di AEM Forms](https://helpx.adobe.com/it/aem-forms/kb/aem-forms-releases.html) sul server AEM Forms.

   * Assicurati che un AEM Forms sul server JEE sia in esecuzione e che la sicurezza dei documenti sia installata sul corrispondente AEM Forms sul server JEE. Il modulo AEM sul server JEE è necessario per indicizzare il documento protetto.

* Se utilizzi solo AEM Forms sul server JEE, il pacchetto dell’indicizzatore è già installato.
* Assicurati che tutti i bundle siano in funzione. Se tutti i bundle non sono attivi, attendi che tutti i bundle siano in esecuzione.

   * Per AEM Forms su OSGi, i bundle sono elencati su https://&#39;[server]:[porta]&#39;/system/console/bundles.
   * Per AEM Forms su JEE, i bundle sono elencati in https://&#39;[server]:[porta]&#39;/[percorso contestuale]/system/console/bundles. Ad esempio https://localhost:8080/lc/system/console/bundles.

* Aggiungi il *sun.util.calendar* all&#39;inserire nell&#39;elenco Consentiti. Per aggiungere il pacchetto all&#39;inserire nell&#39;elenco Consentiti, esegui i seguenti passaggi:

   1. Apri AEM console Web. L’URL è https://&#39;[server]:[porta]&#39;/system/console/configMgr.
   1. Individua e apri **Configurazione del firewall di deserializzazione**.

   1. Aggiungi il pacchetto sun.util.calendar al campo delle classi o dei prefissi del pacchetto Inseriti nell&#39;elenco Consentiti e fai clic su **Salva**.

### Stabilire una connessione sicura tra gli stack AEM Forms JEE e OSGi {#establish-a-secure-connection-between-aem-forms-jee-and-osgi-stacks}

Per stabilire la connessione sicura, è possibile utilizzare uno dei metodi seguenti:

* Configurare Adobe LiveCycle Client SDK Bundle con le credenziali di amministratore AEM Forms su JEE
* Configurare Adobe LiveCycle Client SDK Bundle utilizzando l’autenticazione reciproca

#### Configurare Adobe LiveCycle Client SDK Bundle con le credenziali di amministratore AEM Forms su JEE {#configure-adobe-livecycle-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. Apri AEM console Web. L’URL è https://&#39;[server]:[porta]&#39;/system/console/configMgr.
1. Individua e apri la **Bundle SDK client di Adobe LiveCycle**. Specifica il valore per i campi seguenti:

   * **URL server:** Specifica l’URL HTTPS di AEM Forms sul server JEE. Per abilitare la comunicazione su https, riavvia il server con -Djavax.net.ssl.trustStore=&lt;path of=&quot;&quot; aem=&quot;&quot; forms=&quot;&quot; on=&quot;&quot; jee=&quot;&quot; keystore=&quot;&quot; file=&quot;&quot;> parametro .
   * **Nome servizio**: Aggiungi RightsManagementService all’elenco dei servizi specificati.
   * **Nome utente:** Specifica il nome utente dell’account AEM Forms su JEE da utilizzare per avviare chiamate da AEM server. L&#39;account specificato deve disporre delle autorizzazioni per avviare document services sul server AEM Forms su JEE.
   * **Password**: Specifica la password dell’account AEM Forms su JEE menzionato nel campo Nome utente .

   Fai clic su **Salva**. AEM è abilitato per la ricerca di documenti PDF protetti da protezione dei documenti.

#### Configurare Adobe LiveCycle Client SDK Bundle utilizzando l’autenticazione reciproca {#configure-adobe-livecycle-client-sdk-bundle-using-mutual-authentication}

1. Abilita l’autenticazione reciproca per AEM Forms su JEE. Per informazioni dettagliate, consulta [CAC e autenticazione reciproca](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html).
1. Apri AEM console Web. L’URL è https://&#39;[server]:[porta]&#39;/system/console/configMgr.
1. Individua e apri la **Adobe LiveCycle Client SDK** Bundle. Specifica il valore per le seguenti proprietà:

   * **URL server**: Specifica l’URL HTTPS di AEM Forms sul server JEE. Per abilitare la comunicazione su https, riavvia il server AEM con -Djavax.net.ssl.trustStore=&lt;path of=&quot;&quot; aem=&quot;&quot; forms=&quot;&quot; on=&quot;&quot; jee=&quot;&quot; keystore=&quot;&quot; file=&quot;&quot;> parametro .
   * **Abilita SSL a 2 vie**: Abilita l’opzione Abilita SSL a 2 vie.
   * **URL file KeyStore**: Specifica l&#39;URL del file dell&#39;archivio chiavi.
   * **URL del file TrustStore**: Specifica l’URL del file truststore.
   * **Password KeyStore**: Specifica la password per il file dell&#39;archivio chiavi.
   * **TrustStorePassword**: Specifica la password per il file truststore.
   * **Nome servizio**: Aggiungi RightsManagementService all’elenco dei servizi specificati.

   Fai clic su **Salva**. AEM abilitato per la ricerca di documenti PDF protetti per la protezione dei documenti

### Indice di un documento PDF protetto da policy di esempio {#index-a-sample-policy-protected-pdf-document}

1. Accedi ad AEM Assets come amministratore.
1. Crea una cartella in AEM Digital Asset Manager e carica i documenti PDF protetti da policy nella nuova cartella creata.

   Ora è possibile cercare i documenti protetti da policy utilizzando AEM ricerca.
