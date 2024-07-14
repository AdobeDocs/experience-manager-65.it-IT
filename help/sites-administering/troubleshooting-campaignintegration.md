---
title: Risoluzione dei problemi relativi all’integrazione di Adobe Campaign Classic
description: Scopri come risolvere i problemi relativi all’integrazione con Adobe Campaign Classic.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: 317bab41-3504-4e46-9ddc-72e291a34e06
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 0%

---


# Risoluzione dei problemi relativi all’integrazione di Adobe Campaign Classic{#troubleshooting-your-adobe-campaign-classic-integration}

Scopri come risolvere i problemi relativi all’integrazione con Adobe Campaign Classic (ACC).

I seguenti suggerimenti per la risoluzione dei problemi consentono di risolvere i problemi più comuni che possono verificarsi quando si integra AEM con ACC.

## Suggerimenti generali per la risoluzione dei problemi {#general-troubleshooting-tips}

Controlla se le chiamate HTTP vengono inviate e ricevute da entrambe le soluzioni (AEM > Adobe Campaign Classic, Adobe Campaign Classic > AEM). Questo suggerimento consente di evitare problemi firewall/SSL.

* Per la funzionalità AEM, puoi vedere che le chiamate JSON sono richieste dall’interfaccia di authoring AEM
   * Queste chiamate non devono causare un errore HTTP-500.
   * Se vengono visualizzati errori HTTP-500, controllare `error.log` per ulteriori informazioni.
* Anche l’aumento del livello di debug per le classi di campagna nell’AEM può aiutare a risolvere i problemi.

## Se la connessione non riesce {#when-the-connection-fails}

Verificare di aver configurato l&#39;operatore **`aemserver`** in Adobe Campaign Classic.

## Se le immagini non vengono visualizzate nella console Adobe Campaign Classic {#if-images-do-not-appear-in-the-adobe-campaign-console}

Controlla l’origine HTML e verifica di poter aprire l’URL dal computer client. Se l&#39;URL contiene `localhost:4503`, modifica la configurazione di Day CQ Link Externalizer nell&#39;istanza di authoring AEM. Farlo puntare a un’istanza Publish raggiungibile dal computer della console Adobe Campaign Classic.

Vedere [Configurazione di Externalizer.](/help/sites-administering/campaignstandard.md#configuring-the-externalizer)

## Se non riesci a connetterti da AEM a Adobe Campaign Classic  {#if-you-cannot-connect-from-aem-to-adobe-campaign}

Cerca il seguente messaggio di errore in Adobe Campaign Classic.

* `No datasource defined in the instance 'default'.`

* `Make sure the DNS alias used to access the server is correct (for example, avoid hard-coded IP addresses). (iRc=16384)`

Per risolvere il problema, modificare quanto segue in `$CAMPAIGN_HOME/conf/config-<instance-name>.xml`:

* `<dataStore hosts="*" lang="en_GB">`

## Se non vengono visualizzati dati nella finestra di dialogo Adobe Campaign Classic {#if-no-data-displays-in-the-adobe-campaign-dialog}

In Adobe Campaign Classic, verificare di non disporre di una barra finale (`/`) dopo il numero di porta.

![Adobe Campaign Classic - verificare che non sia presente una barra finale dopo il numero di porta](assets/chlimage_1-149.png)

## Se si riceve un avviso relativo a setlocale {#if-you-get-a-warning-about-your-setlocale}

Quando si avvia il servizio Apache HTTPD per Adobe Campaign Classic, è possibile che venga visualizzato l&#39;errore `Warning: setlocale: LC_CTYPE cannot change locale`

Verifica che `en_CA.ISO-8859-15 locale` sia installato nel server Adobe Campaign Classic.

* È possibile verificare se è installato utilizzando `local -a`.
* Se non è installato, è possibile applicare la patch allo script `/usr/local/neolane/nl6/env.sh` e modificare le impostazioni locali in quelle installate.

## Se si verifica un errore durante la compilazione dello script &#39;get_nms_amcGetSeedMetaData_jssp&#39; {#if-you-get-an-error-while-compiling-script-get-nms-amcgetseedmetadata-jssp}

Se nel file di registro AEM viene visualizzato il seguente messaggio di errore:

`com.day.cq.mcm.campaign.impl.CampaignConnectorImpl Internal Adobe Campaign error: response body is Error while compiling script 'get_nms_amcGetSeedMetaData_jssp' line 45: String.prototype.toJSON called on incompatible XML.`

Utilizza la seguente soluzione alternativa sul server Adobe Campaign Classic.

1. Apri file `$CAMPAIGN_HOME/datakit/nms/fra/js/amcIntegration.js`
1. Modificare la riga 467 del metodo `amcGetSeedMetaData`
1. Cambia `label : [inclView.@label](mailto:inclView.@label)` in `label : String([inclView.@label](mailto:inclView.@label))`
1. Salva.
1. Riavvia il server.

## Se Adobe Campaign Classic visualizza un errore quando si fa clic sul pulsante Sincronizza {#if-adobe-campaign-displays-an-error-when-clicking-the-synchronize-button}

Quando si fa clic sul pulsante **Sincronizza** in Adobe Campaign Classic, è possibile che venga visualizzato il seguente errore.

* `Error while executing the method 'aemListContent' of service [nms:delivery](https://nmsdelivery/)`

Per risolvere il problema, assicurarsi che l&#39;URL di connessione AEM configurato in **Account esterni** in Adobe Campaign Classic sia raggiungibile dal computer.

Spesso questo problema può essere risolto passando da `localhost` a un indirizzo IP per l&#39;URL.

## Se viene visualizzato l’errore &quot;Impossibile analizzare data e ora XTK &quot;non definito&quot;&quot; {#if-you-get-a-cannot-parse-xtk-date-time-undefined-error}

Dopo aver fatto clic su **Sincronizza** in AEM, è possibile che venga visualizzato un messaggio di errore che indica che si è verificato uno script nelle pagine.

* `Cannot parse XTK Date+Time 'undefined': not a valid XTK value.`

Questo errore si verifica se nell’istanza dell’AEM sono presenti informazioni obsolete di Adobe Campaign Classic. Per risolvere il problema, eseguire le operazioni seguenti:

1. Rimuovi tutte le configurazioni di integrazione di Adobe Campaign Classic che si trovano nell’AEM.
1. Rigenera l’integrazione.
1. Crea un modello.

## Se una connessione a SSL visualizza un errore durante la configurazione del Cloud Service {#if-a-connection-to-ssl-displays-an-error-when-setting-up-the-cloud-service}

Invia un ticket al team di supporto di Adobe Campaign se visualizzi quanto segue in `error.log` dell&#39;AEM.

```text
javax.net.ssl.SSLProtocolException: handshake alert:  unrecognized_name
at sun.security.ssl.ClientHandshaker.handshakeAlert(Unknown Source)
at sun.security.ssl.SSLSocketImpl.recvAlert(Unknown Source)
at sun.security.ssl.SSLSocketImpl.readRecord(Unknown Source)
at sun.security.ssl.SSLSocketImpl.performInitialHandshake(Unknown Source)
at sun.security.ssl.SSLSocketImpl.writeRecord(Unknown Source)
at sun.security.ssl.AppOutputStream.write(Unknown Source)
```

## Se trovi HTTP invece dei collegamenti HTTPS previsti nella finestra di dialogo Sincronizzazione {#if-you-see-http-instead-of-an-expected-https-links-in-the-synchronization-dialog}

Quando tenti di sincronizzare il contenuto nella consegna Adobe Campaign Classic, l’AEM restituisce un elenco di newsletter. Tuttavia, gli URL delle newsletter nell’elenco possono essere indirizzi HTTP invece di HTTPS. Quando si seleziona uno degli elementi dell’elenco, si verifica un errore. Questo errore può verificarsi con la seguente configurazione.

* Adobe Campaign in hosting utilizzando https per la comunicazione con l’Autore dell’AEM
* Proxy inverso con terminazione SSL
* Istanza di authoring AEM on-premise

Per risolvere questo problema, eseguire le operazioni seguenti:

* Il Dispatcher AEM o reverse proxy deve essere configurato per trasmettere il protocollo originale come intestazione.
* Il filtro SSL **di** Apache Felix Http Service nella configurazione OSGi dell&#39;AEM deve essere configurato con le impostazioni di intestazione richieste.
   * `https://<host>:<port>/system/console/configMgr`
   * Vedi [https://github.com/apache/felix-dev/tree/master/http#using-the-ssl-filter](https://github.com/apache/felix-dev/tree/master/http#using-the-ssl-filter)

## Impossibile selezionare un modello personalizzato nelle proprietà della pagina {#if-the-custom-template-i-created-cannot-be-selected-in-page-properties}

Durante la creazione di un modello di posta elettronica in AEM per Adobe Campaign Classic, è necessario includere la proprietà `acMapping` con il valore `mapRecipient` nel nodo `jcr:content` del modello. In caso contrario, non è possibile selezionare il modello Adobe Campaign Classic in **Proprietà pagina** dell&#39;AEM. Il campo è disattivato.

## Se trovi l’errore &quot;com.day.cq.mcm.campaign.servlets.util.ParameterMapper&quot; nei registri AEM {#if-you-get-the-error-com-day-cq-mcm-campaign-servlets-util-parametermapper-in-your-logs}

È possibile che venga visualizzato l&#39;errore `com.day.cq.mcm.campaign.servlets.util.ParameterMapper` nei registri AEM quando si utilizza un modello personalizzato.

Questo errore si verifica se la proprietà `acMapping` è impostata su un valore diverso da `recipient.firstName`, in Adobe Campaign Manager viene creato un valore vuoto.

Se si verifica questo errore, installare feature pack 6576 per AEM da [Package Share](/help/sites-administering/package-manager.md#package-share).
