---
title: Risoluzione dei problemi di integrazione
seo-title: Risoluzione dei problemi di integrazione
description: Scoprite come risolvere i problemi di integrazione.
seo-description: Scoprite come risolvere i problemi di integrazione.
uuid: fe080e58-a855-4308-a611-f72eb47ba82d
contentOwner: raiman
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 422ee332-23ae-46bd-8394-a4e0915beaa2
translation-type: tm+mt
source-git-commit: 2fc35bfd93585a586cb1d4e3299261611db49ba6

---


# Risoluzione dei problemi di integrazione{#troubleshooting-integration-issues}

## Suggerimenti generali per la risoluzione dei problemi {#general-troubleshooting-tips}

### Verificare che non siano presenti errori JavaScript {#ensure-there-are-no-javascript-errors}

Verificate se la console JavaScript del browser presenta errori. Errori non gestiti potrebbero impedire che il codice successivo venga eseguito correttamente. In caso di errori, verificare lo script che causa l&#39;errore e in quale area. Il percorso dello script potrebbe fornire un&#39;indicazione delle funzionalità a cui appartiene lo script.

### Accesso a livello di componente {#logging-on-component-level}

In alcuni casi, potrebbe essere utile aggiungere istruzioni aggiuntive a livello di componente. Dal momento che è stato eseguito il rendering del componente, è possibile aggiungere una marcatura temporanea per visualizzare i valori variabili che possono facilitare l&#39;identificazione di potenziali problemi. Esempio:

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

Per ulteriori dettagli sulla registrazione, vedere le pagine [Registrazione](/help/sites-deploying/configure-logging.md) e [Utilizzo dei record di controllo e dei file](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files) di registro.

## Problemi di integrazione di Analytics {#analytics-integration-issues}

### Importazione report causa un utilizzo elevato di CPU/memoria {#the-report-importer-causes-high-cpu-memory-usage}

Importazione report causa un utilizzo elevato di CPU/memoria o causa `OutOfMemoryError` eccezioni.

#### Soluzione {#solution}

Per risolvere questo problema, potete provare quanto segue:

* Verificare che non ci sia una grande quantità di PollingImporter registrati (vedere la sezione &quot;Shutdown impiega molto tempo a causa di PollingImporter&quot; sotto).
* Eseguite gli importatori di report in un determinato momento della giornata utilizzando le espressioni CRON per le `ManagedPollingImporter` configurazioni nella console [](/help/sites-deploying/configuring-osgi.md)OSGi.

Per ulteriori dettagli sulla creazione di servizi di importazione dati personalizzati in AEM, consultate il seguente articolo [https://helpx.adobe.com/experience-manager/using/polling.html](https://helpx.adobe.com/experience-manager/using/polling.html).

### L&#39;arresto richiede molto tempo a causa di PollingImporter {#shutdown-takes-a-long-time-due-to-the-pollingimporter}

Analytics è stato progettato pensando a un meccanismo di ereditarietà. Solitamente, puoi abilitare Analytics per un sito aggiungendo un riferimento a una configurazione Analytics nella scheda delle proprietà della pagina [Servizi](/help/sites-developing/extending-cloud-config.md) cloud. La configurazione viene quindi ereditata automaticamente a tutte le sottopagine senza la necessità di farvi nuovamente riferimento, a meno che una pagina non richieda una configurazione diversa. L’aggiunta di un riferimento a un sito crea automaticamente diversi nodi (12 per AEM 6.3 e versioni precedenti o 6 per AEM 6.4 e versioni successive) del tipo `cq;PollConfig` che crea un’istanza di PollingImporter utilizzata per importare dati di Analytics in AEM. Di conseguenza:

* La presenza di molte pagine che fanno riferimento ad Analytics porta a un elevato numero di Importazione polling.
* Inoltre, copiando e incollando pagine con un riferimento a una configurazione di Analytics si crea una duplicazione dei relativi PollingImporter.

#### Soluzione {#solution-1}

In primo luogo, l’analisi di [error.log](/help/sites-deploying/configure-logging.md) potrebbe fornire alcune informazioni sulla quantità di PollingImporter attivi o registrati. Esempio:

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

In secondo luogo, accertatevi che solo le pagine principali (in alto nella gerarchia) abbiano un riferimento alla configurazione di Analytics.

Per ulteriori dettagli sulla creazione di servizi di importazione dati personalizzati in AEM, consultate il seguente articolo [https://helpx.adobe.com/experience-manager/using/polling.html](https://helpx.adobe.com/experience-manager/using/polling.html).

## Problemi DTM (legacy) {#dtm-legacy-issues}

### Il tag script DTM non viene rappresentato nell&#39;origine della pagina {#the-dtm-script-tag-is-not-rendered-in-the-page-source}

Il tag script [DTM](/help/sites-administering/dtm.md) non è incluso correttamente nella pagina anche se alla configurazione è stato fatto riferimento nella scheda delle proprietà della pagina [Cloud Services](/help/sites-developing/extending-cloud-config.md) .

#### Soluzione {#solution-2}

Per risolvere il problema, potete provare quanto segue:

* Assicuratevi che le proprietà crittografate possano essere decrittografate (tenete presente che la crittografia potrebbe utilizzare una chiave generata automaticamente diversa per ogni istanza di AEM). Per ulteriori dettagli, consultate anche Supporto [crittografia per le proprietà](/help/sites-administering/encryption-support-for-configuration-properties.md)di configurazione.
* Ripubblica le configurazioni trovate in `/etc/cloudservices/dynamictagmanagement`
* Selezionare ACL in `/etc/cloudservices`. Gli ACL devono essere:

   * allow; jcr:read; webservice-support-servicelibfinder
   * allow; jcr:read; tutti; rep:idspn:&amp;ast;/default/&amp;ast;
   * allow; jcr:read; tutti; rep:idspn:&amp;ast;/defas
   * allow; jcr:read; tutti; rep:idspn:&amp;ast;/public/&amp;ast;
   * allow; jcr:read; tutti; rep:idspn:&amp;ast;/public

Per ulteriori informazioni sulla gestione degli ACL, vedere la pagina Amministrazione [utente e sicurezza](/help/sites-administering/security.md#permissions-in-aem) .

## Problemi di integrazione di Target {#target-integration-issues}

### Contenuto di destinazione non visibile in modalità Anteprima quando si utilizzano componenti di pagina personalizzati {#targeted-content-not-visible-in-preview-mode-when-using-custom-page-components}

Questo problema si verifica perché i componenti della pagina personalizzata non includono le librerie JSP o client corrette per la gestione delle integrazioni DTM di Target.

#### Soluzione {#solution-3}

Potete provare le soluzioni seguenti:

* Accertatevi che l&#39; `headlibs.jsp` (se presente) personalizzato `/apps/<CUSTOM-COMPONENTS-PATH>/headlibs.jsp`includa quanto segue:

```
<%@include file="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp" %>
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

* Accertatevi che l&#39; `head.html` (se presente) personalizzato `/apps/<CUSTOM-COMPONENTS-PATH>/head.html`) **non** includa selettivamente delle cuffie di integrazione specifiche, come nell&#39;esempio seguente:

```
<!-- DO NOT MANUALLY INCLUDE SPECIFIC CLOUD SERVICE HEADLIBS LIKE THIS -->
<meta data-sly-include="/libs/cq/dtm/components/dynamictagmanagement/headlibs.jsp" data-sly-unwrap/>
```

L&#39; `servicelibs.jsp` utente aggiunge gli oggetti JavaScript di analisi richiesti e carica le librerie dei servizi cloud associate al sito Web. Per il servizio Target, le librerie vengono caricate tramite il `/libs/cq/analytics/components/testandtarget/headlibs.jsp`

Il set di librerie che vengono caricate dipende dal tipo di libreria client di destinazione ( `mbox.js` o `at.js`) utilizzata nella configurazione di Target.

Quando utilizzate Gestione dinamica dei tag per distribuire `mbox.js` o `at.js` verificare che le librerie siano caricate prima del rendering del contenuto. L&#39;utilizzo di sistemi di gestione dei tag che caricano queste librerie in modo asincrono potrebbe causare problemi durante l&#39;esecuzione del codice JavaScript specifico di destinazione.

Per ulteriori informazioni, consultate la pagina [Sviluppo per contenuti](/help/sites-developing/target.md#understanding-the-target-component) mirati.

### Nella console del browser viene visualizzato l’errore &quot;ID suite di rapporti mancante nell’inizializzazione AppMeasurement&quot; {#the-error-missing-report-suite-id-in-appmeasurement-initialization-is-displayed-in-the-browser-console}

Questo problema potrebbe verificarsi quando Adobe Analytics viene implementato sul sito Web utilizzando DTM e utilizza il codice personalizzato. La causa è l&#39;utilizzo dell&#39;oggetto `s = new AppMeasurement()` per creare un&#39;istanza dell&#39; `s` oggetto.

#### Soluzione {#solution-4}

Utilizzare `s_gi` invece del metodo di `new AppMeasurement` creazione dell&#39;istanza. Esempio:

```
var s_account="INSERT-RSID-HERE"
var s=s_gi(s_account)
```

### Un&#39;offerta predefinita viene visualizzata in modo casuale al posto dell&#39;offerta corretta {#a-default-offer-is-randomly-displayed-instead-of-the-correct-offer}

Questo problema può essere dovuto a più cause:

* Il caricamento delle librerie client Target ( `mbox.js` o `at.js`) in modo asincrono tramite sistemi di gestione tag di terze parti potrebbe interrompere il targeting in modo casuale. Le librerie Target devono essere caricate in modo sincrono nell&#39;intestazione della pagina. Questo è sempre vero quando le librerie vengono distribuite da AEM.

* Caricamento simultaneo di due librerie client Target ( `at.js`), ad esempio una con Gestione dinamica dei tag e una con la configurazione di Target in AEM. Ciò può causare gli arresti anomali per la `adobe.target` definizione se le `at.js` versioni sono diverse.

#### Soluzione {#solution-5}

Potete provare le soluzioni seguenti:

* Assicurati che il codice cliente che carica le librerie simili a Gestione dinamica dei tag (che a loro volta caricano le librerie Target) sia eseguito in modo sincrono nell&#39;intestazione [della](/help/sites-developing/target.md#enabling-targeting-with-adobe-target-on-your-pages)pagina.
* se il sito è configurato per utilizzare DTM per distribuire le librerie Target, assicurati che l&#39;opzione **Clientlib consegnata da DTM** sia selezionata nella configurazione [](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/target-configuring.html) Target del sito.

### Quando si utilizza AT.js 1.3+, viene sempre visualizzata un&#39;offerta predefinita al posto dell&#39;offerta corretta {#a-default-offer-is-always-displayed-instead-of-correct-offer-when-using-at-js}

AEM 6.2 e 6.3 non è compatibile con AT.js versione 1.3.0+. Con AT.js versione 1.3.0 che introduce la convalida dei parametri per le sue API, `adobe.target.applyOffer()` richiede un parametro &quot;mbox&quot; che non è fornito dal `atjs-itegration.js` codice.

#### Soluzione {#solution-6}

Per risolvere questo problema, modificate `atjs-itegration.js` e aggiungete il `"mbox": mboxName` campo nell&#39;oggetto del parametro per `adobe.target.applyOffer()` :

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

### La pagina Goals &amp; Settings (Obiettivi e impostazioni) non mostra la sezione Reporting Sources (Origini di rapporti) {#the-goals-settings-page-does-not-show-the-reporting-sources-section}

Questo problema è probabilmente un problema di provisioning di configurazione [cloud di Analytics](/help/sites-administering/target-configuring.md) A4T.

#### Soluzione {#solution-7}

È necessario verificare che A4T sia abilitato correttamente per l&#39;account Target emettendo la seguente richiesta di verifica ad AEM:

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

Se la risposta contiene la riga, contatta l’Assistenza `a4tEnabled:false`clienti [](https://helpx.adobe.com/contact.html) Adobe per ottenere il provisioning corretto dell’account.

### API Target utili {#helpful-target-apis}

Di seguito sono riportate due API Target che potrebbero essere utili per risolvere i problemi di Target:

* Recuperare l&#39;endpoint Target per un codice cliente specificato

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

