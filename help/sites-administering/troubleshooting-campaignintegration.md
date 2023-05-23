---
title: Risoluzione dei problemi di integrazione Adobe Campaign
seo-title: Troubleshooting your Adobe Campaign Integration
description: Scopri come risolvere i problemi relativi all’integrazione di Adobe Campaign.
seo-description: Learn how to troubleshoot issues with the Adobe Campaign Integration.
uuid: 835ac2c3-ef2f-4963-9047-aeda3647b114
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: b1d45f01-78de-423c-8f6b-5cb7067c3a2f
exl-id: 317bab41-3504-4e46-9ddc-72e291a34e06
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 0%

---

# Risoluzione dei problemi di integrazione Adobe Campaign{#troubleshooting-your-adobe-campaign-integration}

>[!NOTE]
>
>Questa pagina si applica a Campaign Classic.

I seguenti suggerimenti per la risoluzione dei problemi aiutano a risolvere i problemi più comuni che si possono incontrare durante l’integrazione dell’AEM con Adobe Campaign:

## Suggerimenti generali per la risoluzione dei problemi {#general-troubleshooting-tips}

Per entrambe le integrazioni, puoi verificare se vengono inviate le chiamate HTTP (AEM > Adobe Campaign, Adobe Campaign > AEM):

* Quando le integrazioni non riescono, assicurati che queste chiamate arrivino all’altro capo (per evitare problemi firewall/SSL).
* Per quanto riguarda la funzionalità AEM, vedrai che le chiamate JSON vengono richieste dall’interfaccia di authoring dell’AEM; non dovrebbero causare un errore HTTP-500. Se vengono visualizzati errori HTTP-500, controllare `error.log` per ulteriori informazioni.
* Anche l’aumento del livello di debug per le classi di campagna in AEM consente di risolvere i problemi.

## Se la connessione non riesce {#if-the-connection-fails}

Verifica di aver configurato **aemserver** in Adobe Campaign.

## Se le immagini non vengono visualizzate nella console Adobe Campaign {#if-images-do-not-appear-in-the-adobe-campaign-console}

Controlla l’origine HTML e verifica di poter aprire l’URL dal computer client. Se l’URL contiene localhost:4503, modifica la configurazione di Day CQ Link Externalizer nell’istanza di authoring in modo che punti a un’istanza di pubblicazione raggiungibile dal computer della console di Adobe Campaign.

Consulta [Configurazione di Externalizer.](/help/sites-administering/campaignstandard.md#configuring-the-externalizer)

## Se non riesci a connetterti da AEM ad Adobe Campaign {#if-you-cannot-connect-from-aem-to-adobe-campaign}

Cerca il seguente messaggio di errore in Adobe Campaign:

`No datasource defined in the instance 'default'.`

`Make sure the DNS alias used to access the server is correct (for example, avoid hard-coded IP addresses). (iRc=16384)`

Per risolvere il problema, modifica quanto segue in **$CAMPAIGN_HOME/conf/config-&lt;instance-name>.xml**:

`<dataStore hosts="*" lang="en_GB">`

## Se non vengono visualizzati dati nella finestra di dialogo di Adobe Campaign {#if-no-data-displays-in-the-adobe-campaign-dialog}

In Adobe Campaign, accertati di non avere alcuna barra finale (/) dopo il numero della porta.

![chlimage_1-149](assets/chlimage_1-149.png)

## Se ricevi un avviso relativo al tuo setlocale {#if-you-get-a-warning-about-your-setlocale}

Se stai avviando il servizio Apache HTTPD e visualizzi l’errore `"Warning: setlocale: LC_CTYPE cannot change locale"` assicurati di avere **en_CA.ISO-8859-15 locale** installato nel sistema.

È possibile verificare se è installato utilizzando `local -a`. Se non è installato, è possibile applicare la patch **/usr/local/neolane/nl6/env.sh** e modificare le impostazioni locali in una versione installata.

## Se si verifica un errore durante la compilazione dello script &#39;get_nms_amcGetSeedMetaData_jssp&#39; {#if-you-get-an-error-while-compiling-script-get-nms-amcgetseedmetadata-jssp}

Se nel file di registro AEM viene visualizzato il seguente messaggio di errore:

`com.day.cq.mcm.campaign.impl.CampaignConnectorImpl Internal Adobe Campaign error: response body is Error while compiling script 'get_nms_amcGetSeedMetaData_jssp' line 45: String.prototype.toJSON called on incompatible XML.`

Utilizza la seguente soluzione alternativa:

1. Apri file **$CAMPAIGN_HOME/datakit/nms/fra/js/amcIntegration.js**
1. Modificare la riga 467 del metodo &quot;amcGetSeedMetaData&quot;
1. Cambia `label : [inclView.@label](mailto:inclView.@label)` a `label : String([inclView.@label](mailto:inclView.@label))`

1. Salva.
1. Riavvia il server.

## Se Adobe Campaign visualizza un errore quando si fa clic sul pulsante Sincronizza {#if-adobe-campaign-displays-an-error-when-clicking-the-synchronize-button}

Se facendo clic su **Sincronizza** in Adobe Campaign Classic, viene visualizzato il seguente errore:

`Error while executing the method ‘aemListContent' of service [nms:delivery](https://nmsdelivery/)`

Per risolvere questo problema, accertati che l’URL di connessione AEM configurato negli account esterni sia raggiungibile dal computer.

Un interruttore da **localhost** a un indirizzo IP ha risolto questo problema.

## Se viene visualizzato l’errore &quot;Impossibile analizzare data+ora XTK &quot;non definita&quot;&quot; {#if-you-get-a-cannot-parse-xtk-date-time-undefined-error}

Dopo aver fatto clic su Sincronizza, viene visualizzato un errore che indica che si è verificato uno script nelle pagine: Impossibile analizzare Data e ora XTK &quot;non definite&quot;: valore XTK non valido.

Questo accade se sull’istanza dell’AEM sono ancora presenti informazioni obsolete di Adobe Campaign. Risolvi questo problema rimuovendo e ricostruendo tutte le configurazioni di integrazione delle campagne che sono in AEM. Quindi, crea un nuovo modello.

## Se una connessione a SSL mostra un errore durante la configurazione del servizio cloud {#if-a-connection-to-ssl-displays-an-error-when-setting-up-the-cloud-service}

Nel registro degli errori dell’AEM, se vedi quanto segue:

```xml
javax.net.ssl.SSLProtocolException: handshake alert:  unrecognized_name
at sun.security.ssl.ClientHandshaker.handshakeAlert(Unknown Source)
at sun.security.ssl.SSLSocketImpl.recvAlert(Unknown Source)
at sun.security.ssl.SSLSocketImpl.readRecord(Unknown Source)
at sun.security.ssl.SSLSocketImpl.performInitialHandshake(Unknown Source)
at sun.security.ssl.SSLSocketImpl.writeRecord(Unknown Source)
at sun.security.ssl.AppOutputStream.write(Unknown Source)
```

Crea un ticket con il team di supporto Adobe Campaign.

## Se trovi http invece di un collegamento https previsto nella finestra di dialogo di sincronizzazione {#if-you-see-http-instead-of-an-expected-https-links-in-the-synchronization-dialog}

Con la seguente configurazione:

* Adobe Campaign in hosting utilizzando https per la comunicazione con AEM Author
* Proxy inverso con terminazione SSL
* Istanza di authoring AEM on-premise

Quando tenti di sincronizzare il contenuto nella distribuzione di Adobe Campaign, l’AEM restituisce un elenco di newsletter. Tuttavia, gli URL delle newsletter nell’elenco sono indirizzi http. Quando si seleziona uno degli elementi dell’elenco, si verifica un errore.

Per risolvere questo problema:

* Il dispatcher o il reverse proxy deve essere configurato per trasmettere il protocollo originale come intestazione.
* Il *Filtro SSL di Apache Felix Http Service* nella configurazione OSGi ([https://&lt;host>:&lt;port>/system/console/configMgr](http://localhost:4502/system/console/configMgr)) deve essere configurato in base alle rispettive impostazioni di intestazione. Consulta [https://felix.apache.org/documentation/subprojects/apache-felix-http-service.html#using-the-ssl-filter](https://felix.apache.org/documentation/subprojects/apache-felix-http-service.html#using-the-ssl-filter)

## Se il modello personalizzato creato non può essere selezionato in Proprietà pagina {#if-the-custom-template-i-created-cannot-be-selected-in-page-properties}

Quando crei un modello di posta per Adobe Campaign, devi includere la proprietà **acMapping** con il valore **mapRecipient** nel **jcr:content** del modello, oppure non sarà possibile selezionare il modello Adobe Campaign in **Proprietà pagina** dell’AEM (campo disabilitato).

## Se nei registri viene visualizzato l’errore &quot;com.day.cq.mcm.campaign.servlets.util.ParameterMapper&quot; {#if-you-get-the-error-com-day-cq-mcm-campaign-servlets-util-parametermapper-in-your-logs}

Quando utilizzi il modello personalizzato, nei registri viene visualizzato l’errore &quot;com.day.cq.mcm.campaign.servlets.util.ParameterMapper&quot;. In questo caso, assicurati di installare Featurepack 6576 da [Condivisione pacchetti](/help/sites-administering/package-manager.md#package-share). Si tratta di un problema in cui se la proprietà acMapping è impostata su un valore diverso da recipient.firstName, viene creato un valore vuoto sul lato Adobe Campaign Manager.
