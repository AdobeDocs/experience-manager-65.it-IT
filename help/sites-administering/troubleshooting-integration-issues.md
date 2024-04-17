---
title: Risoluzione dei problemi di integrazione
description: Scopri come risolvere i problemi durante l’integrazione con Adobe Experience Manager.
contentOwner: raiman
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: 11b0023e-34bd-4dfe-8173-5466db9fbe34
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1078'
ht-degree: 2%

---

# Risoluzione dei problemi di integrazione{#troubleshooting-integration-issues}

## Suggerimenti generali per la risoluzione dei problemi {#general-troubleshooting-tips}

### Verifica che non siano presenti errori JavaScript {#ensure-there-are-no-javascript-errors}

Controlla se nella console JavaScript del browser sono visualizzati errori. Errori non gestiti potrebbero impedire la corretta esecuzione del codice successivo. In caso di errori, controlla lo script che causa l’errore e in quale area. Il percorso dello script potrebbe fornire un’indicazione della funzionalità a cui appartiene lo script.

### Accesso a livello di componente {#logging-on-component-level}

In alcuni casi, potrebbe essere utile aggiungere istruzioni aggiuntive a livello di componente. Poiché è stato eseguito il rendering del componente, è possibile aggiungere un markup temporaneo per visualizzare i valori delle variabili che potrebbero aiutare a identificare potenziali problemi. Ad esempio:

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

Per ulteriori dettagli sulla registrazione, vedi [Registrazione](/help/sites-deploying/configure-logging.md) e [Utilizzo dei record di controllo e dei file di registro](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files) pagine.

## Problemi di integrazione di Analytics {#analytics-integration-issues}

### Importazione report causa un elevato utilizzo di CPU/memoria {#the-report-importer-causes-high-cpu-memory-usage}

La funzione di importazione report causa un elevato utilizzo di CPU/memoria o causa `OutOfMemoryError` eccezioni.

#### Soluzione {#solution}

Per risolvere il problema, provare a effettuare le seguenti operazioni:

* Assicurati che non vi sia una grande quantità di PollingImporters registrati (vedi la sezione &quot;L’arresto richiede molto tempo a causa di PollingImporter&quot; di seguito).
* Eseguire Importatori report a una determinata ora del giorno utilizzando le espressioni CRON per `ManagedPollingImporter` configurazioni in [Console OSGi](/help/sites-deploying/configuring-osgi.md).

Per ulteriori informazioni sulla creazione di servizi di importazione dati personalizzati in AEM, leggi l’articolo seguente [https://helpx.adobe.com/experience-manager/using/polling.html](https://helpx.adobe.com/experience-manager/using/polling.html).

### L&#39;arresto richiede molto tempo a causa di Importazione polling {#shutdown-takes-a-long-time-due-to-the-pollingimporter}

Analytics è stato progettato pensando a un meccanismo di ereditarietà. In genere, per abilitare Analytics per un sito si aggiunge un riferimento a una configurazione Analytics all’interno delle proprietà della pagina [Cloud Service](/help/sites-developing/extending-cloud-config.md) scheda. La configurazione viene quindi ereditata automaticamente da tutte le sottopagine senza dover fare nuovamente riferimento ad essa, a meno che una pagina non richieda una configurazione diversa. L’aggiunta di un riferimento a un sito crea automaticamente anche diversi nodi (12 per AEM 6.3 e versioni precedenti o 6 per AEM 6.4 e versioni successive) del tipo `cq;PollConfig` che crea un’istanza di PollingImporters utilizzata per importare dati Analytics in AEM. Di conseguenza:

* Se un numero elevato di pagine fa riferimento ad Analytics, il numero di PollingImporters è elevato.
* Inoltre, copiare e incollare pagine con un riferimento a una configurazione Analytics comporta la duplicazione dei relativi PollingImporters.

#### Soluzione {#solution-1}

In primo luogo, l&#39;analisi [error.log](/help/sites-deploying/configure-logging.md) potrebbe fornire informazioni sulla quantità di PollingImporters attivi o registrati. Ad esempio:

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

In secondo luogo, assicurati che solo le pagine superiori (in alto nella gerarchia) contengano un riferimento alla configurazione di Analytics.

Per ulteriori informazioni sulla creazione di servizi di importazione dati personalizzati in AEM, leggi l’articolo seguente [https://helpx.adobe.com/experience-manager/using/polling.html](https://helpx.adobe.com/experience-manager/using/polling.html).

## Problemi DTM(Legacy) {#dtm-legacy-issues}

### Il tag dello script DTM non viene renderizzato nell’origine della pagina {#the-dtm-script-tag-is-not-rendered-in-the-page-source}

Il [DTM](/help/sites-administering/dtm.md) il tag script non viene incluso correttamente nella pagina anche se si è fatto riferimento alla configurazione nelle proprietà della pagina [Cloud Service](/help/sites-developing/extending-cloud-config.md) scheda.

#### Soluzione {#solution-2}

Per risolvere il problema, puoi provare a effettuare le seguenti operazioni:

* Assicurati che le proprietà crittografate possano essere decrittografate (tieni presente che la crittografia potrebbe utilizzare una chiave generata automaticamente diversa su ogni istanza AEM). Per ulteriori informazioni, consulta anche [Supporto della crittografia per le proprietà di configurazione](/help/sites-administering/encryption-support-for-configuration-properties.md).
* Ripubblica le configurazioni trovate in `/etc/cloudservices/dynamictagmanagement`
* Controlla ACL su `/etc/cloudservices`. Gli ACL devono essere:

   * consenti; jcr:read; webservice-support-servicelibfinder
   * consenti; jcr:read; tutti; `rep:glob:`&amp;ast;`/defaults/`&amp;ast;
   * consenti; jcr:read; tutti; `rep:glob:`&amp;ast;`/defaults`
   * consenti; jcr:read; tutti; `rep:glob:`&amp;ast;`/public/`&amp;ast;
   * consenti; jcr:read; tutti; `rep:glob:`&amp;ast;`/public`

Per ulteriori informazioni sulla gestione delle ACL, vedere [Amministrazione utenti e sicurezza](/help/sites-administering/security.md#permissions-in-aem) pagina.

## Problemi di integrazione di Target {#target-integration-issues}

### Contenuto mirato non visibile in modalità Anteprima quando si utilizzano componenti pagina personalizzati {#targeted-content-not-visible-in-preview-mode-when-using-custom-page-components}

Questo problema si verifica perché i componenti pagina personalizzati non includono le librerie JSP o client corrette che gestiscono le integrazioni Target DTM.

#### Soluzione {#solution-3}

Puoi provare le seguenti soluzioni:

* Assicurati che le `headlibs.jsp` (se presente) `/apps/<CUSTOM-COMPONENTS-PATH>/headlibs.jsp`) include quanto segue:

```
<%@include file="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp" %>
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

* Assicurati che le `head.html` (se presente) `/apps/<CUSTOM-COMPONENTS-PATH>/head.html`) **non** includi selettivamente le headlibs di integrazione specifiche, come nell’esempio seguente:

```
<!-- DO NOT MANUALLY INCLUDE SPECIFIC CLOUD SERVICE HEADLIBS LIKE THIS -->
<meta data-sly-include="/libs/cq/dtm/components/dynamictagmanagement/headlibs.jsp" data-sly-unwrap/>
```

Il `servicelibs.jsp` aggiunge gli oggetti JavaScript di analisi richiesti e carica le librerie del servizio cloud associate al sito web. Per il servizio Target, le librerie vengono caricate tramite `/libs/cq/analytics/components/testandtarget/headlibs.jsp`

Il set di librerie caricate dipende dal tipo di libreria client di destinazione ( `mbox.js` o `at.js`) utilizzato nella configurazione di Target.

Quando si utilizza DTM per distribuire `mbox.js` o `at.js` assicurati che le librerie siano caricate prima che venga eseguito il rendering del contenuto. L’utilizzo di sistemi Tag Management che caricano queste librerie in modo asincrono potrebbe causare problemi nell’esecuzione del codice JavaScript specifico di destinazione.

Per ulteriori informazioni, leggere [Sviluppo per contenuti di destinazione](/help/sites-developing/target.md#understanding-the-target-component) pagina.

### Nella console del browser viene visualizzato l’errore &quot;Manca l’ID Report Suite nell’inizializzazione di AppMeasurement&quot; {#the-error-missing-report-suite-id-in-appmeasurement-initialization-is-displayed-in-the-browser-console}

Questo problema può verificarsi quando Adobe Analytics viene implementato sul sito web utilizzando DTM e utilizza un codice personalizzato. La causa è l’utilizzo di `s = new AppMeasurement()` per creare un&#39;istanza di `s` oggetto.

#### Soluzione {#solution-4}

Utilizzare `s_gi` invece del `new AppMeasurement` metodo di creazione istanza. Ad esempio:

```
var s_account="INSERT-RSID-HERE"
var s=s_gi(s_account)
```

### Un’offerta predefinita viene visualizzata in modo casuale al posto dell’offerta corretta {#a-default-offer-is-randomly-displayed-instead-of-the-correct-offer}

Questo problema può avere diverse cause:

* Caricamento librerie client di Target ( `mbox.js` o `at.js`) in modo asincrono, utilizzando sistemi Tag Management di terze parti, il targeting può essere interrotto in modo casuale. Le librerie di Target devono essere caricate in modo sincrono nell’intestazione della pagina. Questo è sempre vero quando le librerie vengono distribuite dall’AEM.

* Caricamento di due librerie client di Target ( `at.js`) simultaneamente, ad esempio, uno che utilizza DTM e uno che utilizza la configurazione di Target nell’AEM. Questo può causare conflitti per `adobe.target` definizione se `at.js` le versioni sono diverse.

#### Soluzione {#solution-5}

Puoi provare le seguenti soluzioni:

* Assicurati che il codice del cliente che carica le librerie simili a DTM (che a sua volta caricano le librerie di Target) venga eseguito in modo sincrono in [intestazione pagina](/help/sites-developing/target.md#enabling-targeting-with-adobe-target-on-your-pages).
* se il sito è configurato per l’utilizzo di DTM per la distribuzione di librerie Target, assicurati che il **Clientlib fornita da DTM** l&#39;opzione è selezionata in [Configurazione di Target](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/target-configuring.html) per il sito.

### Viene sempre visualizzata un’offerta predefinita invece dell’offerta corretta quando si utilizza AT.js 1.3+ {#a-default-offer-is-always-displayed-instead-of-correct-offer-when-using-at-js}

AEM 6.2 e 6.3 non sono compatibili con AT.js versione 1.3.0+. Con la versione 1.3.0 di AT.js che introduce la convalida dei parametri per le sue API, `adobe.target.applyOffer()` richiede un parametro &quot;mbox&quot; che non viene fornito da `atjs-itegration.js` codice.

#### Soluzione {#solution-6}

Per risolvere questo problema, modifica `atjs-itegration.js` e aggiungi `"mbox": mboxName` campo nell&#39;oggetto parametro per `adobe.target.applyOffer()` come segue:

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

Questo problema è molto probabilmente un [Configurazione di A4T Analytics Cloud](/help/sites-administering/target-configuring.md) problema di provisioning.

#### Soluzione {#solution-7}

Verifica che A4T sia abilitato correttamente per il tuo account Target emettendo la seguente richiesta di verifica all’AEM:

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

Se la risposta contiene la riga `a4tEnabled:false`, contenuto [Assistenza clienti Adobe](https://helpx.adobe.com/contact.html) per effettuare correttamente il provisioning del tuo account.

### API di Target utili {#helpful-target-apis}

Di seguito sono presentate due API di Target che potrebbero essere utili per la risoluzione dei problemi di Target:

* Recuperare l’endpoint Target per un determinato codice client

```
https://admin.testandtarget.omniture.com/rest/v1/endpoint/<CLIENTCODE>.json

{"api":"https://admin<N>.testandtarget.omniture.com/admin/rest/v1"}
```

* Recuperare il profilo di un cliente

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
