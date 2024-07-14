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

Per ulteriori dettagli sulla registrazione, vedere le pagine [Registrazione](/help/sites-deploying/configure-logging.md) e [Utilizzo dei record di controllo e dei file di registro](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files).

## Problemi di integrazione di Analytics {#analytics-integration-issues}

### Importazione report causa un elevato utilizzo di CPU/memoria {#the-report-importer-causes-high-cpu-memory-usage}

Importazione report causa un elevato utilizzo di CPU/memoria o `OutOfMemoryError` eccezioni.

#### Soluzione {#solution}

Per risolvere il problema, provare a effettuare le seguenti operazioni:

* Assicurati che non vi sia una grande quantità di PollingImporters registrati (vedi la sezione &quot;L’arresto richiede molto tempo a causa di PollingImporter&quot; di seguito).
* Eseguire Report Importers a una certa ora del giorno utilizzando le espressioni CRON per le configurazioni `ManagedPollingImporter` nella [console OSGi](/help/sites-deploying/configuring-osgi.md).

Per ulteriori informazioni sulla creazione di servizi di importazione dati personalizzati in AEM, leggere l&#39;articolo seguente [https://helpx.adobe.com/experience-manager/using/polling.html](https://helpx.adobe.com/experience-manager/using/polling.html).

### L&#39;arresto richiede molto tempo a causa di Importazione polling {#shutdown-takes-a-long-time-due-to-the-pollingimporter}

Analytics è stato progettato pensando a un meccanismo di ereditarietà. In genere, per abilitare Analytics per un sito si aggiunge un riferimento a una configurazione Analytics nella scheda [Cloud Service](/help/sites-developing/extending-cloud-config.md) delle proprietà della pagina. La configurazione viene quindi ereditata automaticamente da tutte le sottopagine senza dover fare nuovamente riferimento ad essa, a meno che una pagina non richieda una configurazione diversa. L’aggiunta di un riferimento a un sito crea automaticamente anche diversi nodi (12 per AEM 6.3 e versioni precedenti o 6 per AEM 6.4   e versioni successive) del tipo `cq;PollConfig` che crea un&#39;istanza di PollingImporters utilizzata per importare dati di Analytics in AEM. Di conseguenza:

* Se un numero elevato di pagine fa riferimento ad Analytics, il numero di PollingImporters è elevato.
* Inoltre, copiare e incollare pagine con un riferimento a una configurazione Analytics comporta la duplicazione dei relativi PollingImporters.

#### Soluzione {#solution-1}

In primo luogo, l&#39;analisi di [error.log](/help/sites-deploying/configure-logging.md) potrebbe fornire informazioni approfondite sulla quantità di PollingImporters attivi o registrati. Ad esempio:

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

Per ulteriori informazioni sulla creazione di servizi di importazione dati personalizzati in AEM, leggere l&#39;articolo seguente [https://helpx.adobe.com/experience-manager/using/polling.html](https://helpx.adobe.com/experience-manager/using/polling.html).

## Problemi DTM(Legacy) {#dtm-legacy-issues}

### Il tag dello script DTM non viene renderizzato nell’origine della pagina {#the-dtm-script-tag-is-not-rendered-in-the-page-source}

Il tag di script [DTM](/help/sites-administering/dtm.md) non è incluso correttamente nella pagina anche se nella scheda delle proprietà della pagina [Cloud Service](/help/sites-developing/extending-cloud-config.md) è stato fatto riferimento alla configurazione.

#### Soluzione {#solution-2}

Per risolvere il problema, puoi provare a effettuare le seguenti operazioni:

* Assicurati che le proprietà crittografate possano essere decrittografate (tieni presente che la crittografia potrebbe utilizzare una chiave generata automaticamente diversa su ogni istanza AEM). Per ulteriori dettagli, leggere anche il documento [Supporto crittografia per le proprietà di configurazione](/help/sites-administering/encryption-support-for-configuration-properties.md).
* Ripubblica le configurazioni trovate in `/etc/cloudservices/dynamictagmanagement`
* Controllare gli ACL su `/etc/cloudservices`. Gli ACL devono essere:

   * consenti; jcr:read; webservice-support-servicelibfinder
   * consenti; jcr:read; tutti; `rep:glob:`&amp;ast;`/defaults/`&amp;ast;
   * consenti; jcr:read; tutti; `rep:glob:`&amp;ast;`/defaults`
   * consenti; jcr:read; tutti; `rep:glob:`&amp;ast;`/public/`&amp;ast;
   * consenti; jcr:read; tutti; `rep:glob:`&amp;ast;`/public`

Per ulteriori informazioni sulla gestione degli ACL, leggere la pagina [Amministrazione utenti e sicurezza](/help/sites-administering/security.md#permissions-in-aem).

## Problemi di integrazione di Target {#target-integration-issues}

### Contenuto mirato non visibile in modalità Anteprima quando si utilizzano componenti pagina personalizzati {#targeted-content-not-visible-in-preview-mode-when-using-custom-page-components}

Questo problema si verifica perché i componenti pagina personalizzati non includono le librerie JSP o client corrette che gestiscono le integrazioni Target DTM.

#### Soluzione {#solution-3}

Puoi provare le seguenti soluzioni:

* Assicurarsi che il `headlibs.jsp` personalizzato (se presente `/apps/<CUSTOM-COMPONENTS-PATH>/headlibs.jsp`) includa quanto segue:

```
<%@include file="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp" %>
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

* Assicurati che `head.html` personalizzato (se presente `/apps/<CUSTOM-COMPONENTS-PATH>/head.html`) **non** includa selettivamente le headlibs di integrazione specifiche, come nell&#39;esempio seguente:

```
<!-- DO NOT MANUALLY INCLUDE SPECIFIC CLOUD SERVICE HEADLIBS LIKE THIS -->
<meta data-sly-include="/libs/cq/dtm/components/dynamictagmanagement/headlibs.jsp" data-sly-unwrap/>
```

`servicelibs.jsp` aggiunge gli oggetti JavaScript di analisi richiesti e carica le librerie del servizio cloud associate al sito Web. Per il servizio Target, le librerie vengono caricate tramite `/libs/cq/analytics/components/testandtarget/headlibs.jsp`

Il set di librerie caricate dipende dal tipo di libreria client di destinazione ( `mbox.js` o `at.js`) utilizzata nella configurazione di destinazione.

Quando utilizzi DTM per distribuire `mbox.js` o `at.js`, accertati che le librerie siano caricate prima del rendering del contenuto. L’utilizzo di sistemi Tag Management per caricare queste librerie in modo asincrono potrebbe causare problemi nell’esecuzione del codice JavaScript specifico di destinazione.

Per ulteriori informazioni, leggere la pagina [Sviluppo per contenuti di destinazione](/help/sites-developing/target.md#understanding-the-target-component).

### Nella console del browser viene visualizzato l’errore &quot;Manca l’ID Report Suite nell’inizializzazione di AppMeasurement&quot; {#the-error-missing-report-suite-id-in-appmeasurement-initialization-is-displayed-in-the-browser-console}

Questo problema può verificarsi quando Adobe Analytics viene implementato sul sito web utilizzando DTM e utilizza un codice personalizzato. La causa sta utilizzando `s = new AppMeasurement()` per creare un&#39;istanza dell&#39;oggetto `s`.

#### Soluzione {#solution-4}

Utilizzare `s_gi` al posto del metodo di creazione istanza `new AppMeasurement`. Ad esempio:

```
var s_account="INSERT-RSID-HERE"
var s=s_gi(s_account)
```

### Un’offerta predefinita viene visualizzata in modo casuale al posto dell’offerta corretta {#a-default-offer-is-randomly-displayed-instead-of-the-correct-offer}

Questo problema può avere diverse cause:

* Il caricamento delle librerie client di Target ( `mbox.js` o `at.js`) in modo asincrono utilizzando sistemi Tag Management di terze parti può interrompere il targeting in modo casuale. Le librerie di Target devono essere caricate in modo sincrono nell’intestazione della pagina. Questo è sempre vero quando le librerie vengono distribuite dall’AEM.

* Caricamento simultaneo di due librerie client di Target ( `at.js`), ad esempio una che utilizza DTM e una che utilizza la configurazione di Target nell&#39;AEM. Ciò può causare conflitti per la definizione di `adobe.target` se le versioni di `at.js` sono diverse.

#### Soluzione {#solution-5}

Puoi provare le seguenti soluzioni:

* Assicurati che il codice del cliente che carica le librerie simili a DTM (che a sua volta caricano le librerie di Target) venga eseguito in modo sincrono nell&#39;[intestazione pagina](/help/sites-developing/target.md#enabling-targeting-with-adobe-target-on-your-pages).
* Se il sito è configurato per l&#39;utilizzo di DTM per la distribuzione delle librerie di Target, verificare che l&#39;opzione **Clientlib consegnata da DTM** sia selezionata nella [configurazione di Target](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/target-configuring.html) per il sito.

### Viene sempre visualizzata un’offerta predefinita invece dell’offerta corretta quando si utilizza AT.js 1.3+ {#a-default-offer-is-always-displayed-instead-of-correct-offer-when-using-at-js}

AEM 6.2 e 6.3 non sono compatibili con AT.js versione 1.3.0+. Con la versione 1.3.0 di AT.js che introduce la convalida dei parametri per le API, `adobe.target.applyOffer()` richiede un parametro &quot;mbox&quot; non fornito dal codice `atjs-itegration.js`.

#### Soluzione {#solution-6}

Per risolvere il problema, modificare `atjs-itegration.js` e aggiungere il campo `"mbox": mboxName` nell&#39;oggetto parametro per `adobe.target.applyOffer()` come segue:

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

Questo problema è probabilmente un problema di provisioning di [Configurazione A4T Analytics Cloud](/help/sites-administering/target-configuring.md).

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

Se la risposta contiene la riga `a4tEnabled:false`, contatta [l&#39;Assistenza clienti Adobe](https://helpx.adobe.com/contact.html) per il corretto provisioning dell&#39;account.

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
