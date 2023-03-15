---
title: Risoluzione dei problemi di integrazione
seo-title: Troubleshooting Integration Issues
description: Scopri come risolvere i problemi di integrazione.
seo-description: Learn how to troubleshoot integration issues.
uuid: fe080e58-a855-4308-a611-f72eb47ba82d
contentOwner: raiman
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 422ee332-23ae-46bd-8394-a4e0915beaa2
exl-id: 11b0023e-34bd-4dfe-8173-5466db9fbe34
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1096'
ht-degree: 2%

---

# Risoluzione dei problemi di integrazione{#troubleshooting-integration-issues}

## Suggerimenti generali per la risoluzione dei problemi {#general-troubleshooting-tips}

### Assicurati che non ci siano errori JavaScript {#ensure-there-are-no-javascript-errors}

Controlla se nella console JavaScript del browser vengono visualizzati degli errori. Errori non gestiti potrebbero impedire la corretta esecuzione del codice successivo. In caso di errori, controlla quale script sta causando l’errore e in quale area. Il percorso dello script potrebbe fornire un&#39;indicazione delle funzionalità a cui appartiene lo script.

### Accesso a livello di componente {#logging-on-component-level}

In alcuni casi, potrebbe essere utile aggiungere istruzioni aggiuntive a livello di componente. Poiché il componente è sottoposto a rendering, puoi aggiungere un markup temporaneo per mostrare valori variabili che potrebbero aiutarti a identificare potenziali problemi. Esempio:

```
<%
log.info("myVariable={}", myVariable);
%>

<!--
<%= myJspVariable %>
-->

<!--
${ myHtlVariable }
-->
```

Per ulteriori dettagli sulla registrazione, consulta la sezione [Registrazione](/help/sites-deploying/configure-logging.md) e [Utilizzo dei record di controllo e dei file di registro](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files) pagine.

## Problemi di integrazione di Analytics {#analytics-integration-issues}

### L’importazione dei report causa un elevato utilizzo di CPU/memoria {#the-report-importer-causes-high-cpu-memory-usage}

L’importazione dei report causa un elevato utilizzo della CPU/memoria o causa `OutOfMemoryError` eccezioni.

#### Soluzione {#solution}

Per risolvere questo problema è possibile provare quanto segue:

* Assicurati che non ci sia una grande quantità di PollingImporter registrati (vedi la sezione &quot;Lo spegnimento richiede molto tempo a causa di PollingImporter&quot; qui sotto).
* Esegui gli importatori di report in un determinato momento della giornata utilizzando le espressioni CRON per `ManagedPollingImporter` configurazioni [Console OSGi](/help/sites-deploying/configuring-osgi.md).

Per ulteriori dettagli sulla creazione di servizi di importazione dati personalizzati in AEM, leggi il seguente articolo [https://helpx.adobe.com/experience-manager/using/polling.html](https://helpx.adobe.com/experience-manager/using/polling.html).

### Lo spegnimento richiede molto tempo a causa di PollingImporter {#shutdown-takes-a-long-time-due-to-the-pollingimporter}

Analytics è stato progettato pensando a un meccanismo di ereditarietà. Di solito, per abilitare Analytics per un sito, aggiungi un riferimento a una configurazione di Analytics all’interno delle proprietà della pagina [Cloud Services](/help/sites-developing/extending-cloud-config.md) scheda . La configurazione viene quindi ereditata automaticamente da tutte le sottopagine senza la necessità di farvi nuovamente riferimento, a meno che una pagina non richieda una configurazione diversa. Aggiungendo un riferimento a un sito vengono automaticamente creati diversi nodi (12 per AEM 6.3 e versioni precedenti o 6 per AEM 6.4 e versioni successive) del tipo `cq;PollConfig` che crea un&#39;istanza di PollingImporter utilizzata per importare i dati di Analytics in AEM. Di conseguenza:

* Avere molte pagine che fanno riferimento ad Analytics porta a un&#39;elevata quantità di PollingImporter.
* Inoltre, copiare e incollare le pagine con un riferimento a una configurazione di Analytics porta a una duplicazione dei relativi PollingImporter.

#### Soluzione {#solution-1}

In primo luogo, l&#39;analisi della [error.log](/help/sites-deploying/configure-logging.md) potrebbe darti qualche idea sulla quantità di PollingImporter attivi o registrati. Esempio:

```
# Count PollingImporter entries
$ sed -n "s/.*(aem-analytics-integration-.*).*target=\(.*\),interval.*/\1/p" error.log | wc -l
86415
# Count PollingImporter entries for last30days
$ sed -n "s/.*(aem-analytics-integration-last30Days).*target=\(.*\),interval.*/\1/p" error.log | wc -l
14531
# Count unique paths of PollingImporter registrations
sed -n "s/.*(aem-analytics-integration-.*).*target=\(.*\)\/jcr:content.*/\1/p" error.log | sort | uniq -c
28115
```

In secondo luogo, assicurati che solo le pagine principali (alte nella gerarchia) abbiano una configurazione di Analytics a cui fare riferimento.

Per ulteriori dettagli sulla creazione di servizi di importazione dati personalizzati in AEM, leggi il seguente articolo [https://helpx.adobe.com/experience-manager/using/polling.html](https://helpx.adobe.com/experience-manager/using/polling.html).

## Problemi DTM (legacy) {#dtm-legacy-issues}

### Il tag script DTM non viene riprodotto nell’origine della pagina {#the-dtm-script-tag-is-not-rendered-in-the-page-source}

La [DTM](/help/sites-administering/dtm.md) il tag script non è incluso correttamente nella pagina anche se è stato fatto riferimento alla configurazione nelle proprietà della pagina [Cloud Services](/help/sites-developing/extending-cloud-config.md) scheda .

#### Soluzione {#solution-2}

Per risolvere il problema, prova quanto segue:

* Assicurati che le proprietà crittografate possano essere decrittografate (nota che la crittografia potrebbe utilizzare una chiave generata automaticamente diversa in ogni istanza di AEM). Per ulteriori dettagli, leggere anche [Supporto crittografia per le proprietà di configurazione](/help/sites-administering/encryption-support-for-configuration-properties.md).
* Ripubblica le configurazioni trovate in `/etc/cloudservices/dynamictagmanagement`
* Controlla ACL su `/etc/cloudservices`. Le ACL devono essere:

   * consentire; jcr:read; webservice-support-servicelibfinder
   * consentire; jcr:read; tutti; rep:glob:&amp;ast;/default/&amp;ast;
   * consentire; jcr:read; tutti; rep:glob:&amp;ast;/default
   * consentire; jcr:read; tutti; rep:glob:&amp;ast;/public/&amp;ast;
   * consentire; jcr:read; tutti; rep:glob:&amp;ast;/public

Per ulteriori informazioni sulla gestione degli ACL, consulta la sezione [Amministrazione degli utenti e sicurezza](/help/sites-administering/security.md#permissions-in-aem) pagina.

## Problemi di integrazione di Target {#target-integration-issues}

### Contenuto di destinazione non visibile in modalità Anteprima quando si utilizzano componenti di pagina personalizzati {#targeted-content-not-visible-in-preview-mode-when-using-custom-page-components}

Questo problema si verifica perché i componenti di pagina personalizzati non includono le librerie client o JSP corrette che gestiscono le integrazioni DTM di Target.

#### Soluzione {#solution-3}

Puoi provare le seguenti soluzioni:

* Assicurati di personalizzare `headlibs.jsp` se del caso `/apps/<CUSTOM-COMPONENTS-PATH>/headlibs.jsp`) include quanto segue:

```
<%@include file="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp" %>
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

* Assicurati di personalizzare `head.html` se del caso `/apps/<CUSTOM-COMPONENTS-PATH>/head.html`) **non** includi in modo selettivo gli headlibs di integrazione specifici, come nell’esempio seguente:

```
<!-- DO NOT MANUALLY INCLUDE SPECIFIC CLOUD SERVICE HEADLIBS LIKE THIS -->
<meta data-sly-include="/libs/cq/dtm/components/dynamictagmanagement/headlibs.jsp" data-sly-unwrap/>
```

La `servicelibs.jsp` aggiunge gli oggetti JavaScript di analytics richiesti e carica le librerie dei servizi cloud associate al sito web. Per il servizio Target, le librerie vengono caricate tramite il `/libs/cq/analytics/components/testandtarget/headlibs.jsp`

Il set di librerie caricate dipende dal tipo di libreria client di destinazione ( `mbox.js` o `at.js`) utilizzata nella configurazione di Target.

Quando si utilizza DTM per distribuire `mbox.js` o `at.js` assicurati che le librerie siano caricate prima del rendering del contenuto. L’utilizzo di Tag Management Systems che carica queste librerie in modo asincrono potrebbe causare problemi nell’esecuzione del codice JavaScript specifico di destinazione.

Per ulteriori informazioni, consulta la sezione [Sviluppo per contenuti mirati](/help/sites-developing/target.md#understanding-the-target-component) pagina.

### L’errore &quot;ID suite di rapporti mancante nell’inizializzazione AppMeasurement&quot; viene visualizzato nella console del browser {#the-error-missing-report-suite-id-in-appmeasurement-initialization-is-displayed-in-the-browser-console}

Questo problema può comparire quando Adobe Analytics viene implementato sul sito web utilizzando DTM e utilizza codice personalizzato. La causa sta utilizzando il `s = new AppMeasurement()` per creare un&#39;istanza del `s` oggetto.

#### Soluzione {#solution-4}

Utilizzo `s_gi` anziché `new AppMeasurement` metodo di creazione istanze. Esempio:

```
var s_account="INSERT-RSID-HERE"
var s=s_gi(s_account)
```

### Invece dell’offerta corretta viene visualizzata in modo casuale un’offerta predefinita {#a-default-offer-is-randomly-displayed-instead-of-the-correct-offer}

Questo problema può avere molteplici cause:

* Caricamento delle librerie client di Target ( `mbox.js` o `at.js`) in modo asincrono utilizzando Tag Management Systems di terze parti potrebbe interrompere il targeting in modo casuale. Le librerie di Target devono essere caricate in modo sincrono nell’intestazione di pagina. Questo è sempre vero quando le librerie vengono distribuite da AEM.

* Caricamento di due librerie client Target ( `at.js`) simultaneamente, ad esempio, uno che utilizza DTM e uno che utilizza la configurazione di Target in AEM. Questo può causare scontri per `adobe.target` se `at.js` le versioni sono diverse.

#### Soluzione {#solution-5}

Puoi provare le seguenti soluzioni:

* Assicurati che il codice del cliente che carica le librerie simili a DTM (che a loro volta caricano le librerie di Target) venga eseguito in modo sincrono nel [intestazione pagina](/help/sites-developing/target.md#enabling-targeting-with-adobe-target-on-your-pages).
* se il sito è configurato per utilizzare DTM per distribuire le librerie di Target, assicurati che **Clientlib consegnata da DTM** è selezionata l’opzione [Configurazione di Target](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/target-configuring.html) per il sito.

### Quando si utilizza AT.js 1.3+, viene sempre visualizzata un’offerta predefinita al posto dell’offerta corretta {#a-default-offer-is-always-displayed-instead-of-correct-offer-when-using-at-js}

Le versioni standard AEM 6.2 e 6.3 non sono compatibili con AT.js 1.3.0+. Con AT.js versione 1.3.0 che introduce la convalida dei parametri per le sue API, `adobe.target.applyOffer()` richiede un parametro &quot;mbox&quot; che non è fornito dal `atjs-itegration.js` codice.

#### Soluzione {#solution-6}

Per risolvere questo problema modificare `atjs-itegration.js` e aggiungi la `"mbox": mboxName` nell&#39;oggetto parametro per `adobe.target.applyOffer()` come segue:

```
adobe.target.getOffer({
    "mbox": mboxName,
    "params": params,
    "success": function (response) {
        adobe.target.applyOffer({
            "mbox": mboxName, //<--- ADDED PARAM
            "selector": "#" + mboxName,
            "offer": response
        })
    },
```

### La pagina Obiettivi e impostazioni non mostra la sezione Origini di reporting {#the-goals-settings-page-does-not-show-the-reporting-sources-section}

Questo problema è probabilmente un [Configurazione di A4T Analytics Cloud](/help/sites-administering/target-configuring.md) problema di provisioning.

#### Soluzione {#solution-7}

È necessario verificare che A4T sia abilitato correttamente per il tuo account Target effettuando la seguente richiesta di verifica a AEM:

```
http://localhost:4502/etc/cloudservices/testandtarget/<YOUR-CONFIG>/jcr:content.a4t.json

{
    "a4tEnabled": true,
    "sharedsecret": "SECRET",
    "proxyUrl": "/libs/cq/contentinsight/content/proxy.reportingservices.json",
    "active": "true",
    "pageName": "",
    "url": "https://api5.omniture.com/rs/0.5/",
    "username": "USER@DOMAIN"
}
```

Se la risposta contiene la riga `a4tEnabled:false`, contancato [Adobe Customer Care](https://helpx.adobe.com/contact.html) per ottenere il provisioning corretto del tuo account.

### API di Target utili {#helpful-target-apis}

Di seguito sono riportate due API di Target che potrebbero essere utili per la risoluzione dei problemi di Target:

* Recupera l&#39;endpoint Target per un dato codice client

```
https://admin.testandtarget.omniture.com/rest/v1/endpoint/<CLIENTCODE>.json

{"api":"https://admin<N>.testandtarget.omniture.com/admin/rest/v1"}
```

* Recuperare il profilo di un client

```
https://admin<N>.testandtarget.omniture.com/admin/rest/v1/clients/<CLIENT>?email=<EMAIL>&password=<PASSWORD>

Response for N=4, CLIENT-dayintegrationintern
{
    "clientCode": "dayintegrationintern",
    "companyName": "Day Integration - Internal",
    "omnitureCompanyId": "Day Integration Internal",
    "softTraxId": -1,
    "address1": "XYZ",
    "city": "San Francisco",
    "state": "ca",
    "zip": "94107",
    "country": "UNITED STATES",
    "locale": "de_DE",
    "timeZone": "Europe/Berlin",
    "phone": "XX-XX-XXXX",
    "serviceLevel": "Up to 100,000",
    "privileges": [
        "a4t",
        "hosts",
        "TnT-SC-integration",
        "mvt",
        "steps",
        "testing-campaigns",
        "view-snapshot",
        "on-site-editor",
        "optimizing-campaign",
        "third-party-id-support",
        "landing-page-campaigns",
        "segment",
        "rest-create-user",
        "advanced-targeting",
        "mobile-device-targeting",
        "beta",
        "geolocation"
    ]
}
```
