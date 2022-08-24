---
title: Risoluzione dei problemi relativi all’integrazione di Adobe Campaign
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

# Risoluzione dei problemi relativi all’integrazione di Adobe Campaign{#troubleshooting-your-adobe-campaign-integration}

>[!NOTE]
>
>Questa pagina si applica a Campaign Classic.

I seguenti suggerimenti per la risoluzione dei problemi possono essere utili per risolvere i problemi più comuni che si possono incontrare durante l’integrazione di AEM con Adobe Campaign:

## Suggerimenti generali per la risoluzione dei problemi {#general-troubleshooting-tips}

Per entrambe le integrazioni, puoi verificare se le chiamate HTTP sono inviate (AEM > Adobe Campaign, Adobe Campaign > AEM):

* Quando le integrazioni non riescono, assicurati che queste chiamate arrivino dall’altra parte (per evitare problemi di firewall/SSL).
* Per AEM funzionalità, noterai che le chiamate json sono richieste dall’interfaccia AEM autore; questi non devono causare un errore HTTP-500. Se vengono visualizzati errori HTTP-500, controlla il `error.log` per ulteriori informazioni.
* Anche aumentare il livello di debug per le classi di campagna in AEM aiuta a risolvere i problemi.

## Se la connessione non riesce {#if-the-connection-fails}

Verifica di aver configurato il **aemserver** in Adobe Campaign.

## Se le immagini non vengono visualizzate nella console Adobe Campaign {#if-images-do-not-appear-in-the-adobe-campaign-console}

Controlla l’origine di HTML e verifica di poter aprire l’URL dal computer client. Se l’URL contiene localhost:4503, modifica la configurazione di Day CQ Link Externalizer sull’istanza dell’autore in modo che punti a un’istanza di pubblicazione raggiungibile dal computer della console Adobe Campaign.

Vedi [Configurazione dell’esternalizzatore.](/help/sites-administering/campaignstandard.md#configuring-the-externalizer)

## Se non è possibile connettersi da AEM ad Adobe Campaign {#if-you-cannot-connect-from-aem-to-adobe-campaign}

Cerca il seguente messaggio di errore in Adobe Campaign:

`No datasource defined in the instance 'default'.`

`Make sure the DNS alias used to access the server is correct (for example, avoid hard-coded IP addresses). (iRc=16384)`

Per risolvere questo problema, modifica quanto segue in **$CAMPAIGN_HOME/conf/config-&lt;instance-name>.xml**:

`<dataStore hosts="*" lang="en_GB">`

## Se non vengono visualizzati dati nella finestra di dialogo Adobe Campaign {#if-no-data-displays-in-the-adobe-campaign-dialog}

In Adobe Campaign, assicurati di non avere una barra finale (/) dopo il numero di porta.

![chlimage_1-149](assets/chlimage_1-149.png)

## Se ricevi un avviso sulle impostazioni locali {#if-you-get-a-warning-about-your-setlocale}

Se stai avviando il servizio HTTPD di Apache e vedi l&#39;errore `"Warning: setlocale: LC_CTYPE cannot change locale"` assicurati di avere **en_CA.ISO-8859-15 locale** installato nel sistema.

Puoi verificare se è installato utilizzando `local -a`. Se non è installato, è possibile eseguire la patch **/usr/local/neolane/nl6/env.sh** creare lo script e modificare le impostazioni internazionali in una lingua installata.

## Se ricevi un errore durante la compilazione dello script &#39;get_nms_amcGetSeedMetaData_jssp&#39; {#if-you-get-an-error-while-compiling-script-get-nms-amcgetseedmetadata-jssp}

Se vedi il seguente messaggio di errore nel file di log AEM:

`com.day.cq.mcm.campaign.impl.CampaignConnectorImpl Internal Adobe Campaign error: response body is Error while compiling script 'get_nms_amcGetSeedMetaData_jssp' line 45: String.prototype.toJSON called on incompatible XML.`

Utilizza la seguente soluzione alternativa:

1. Apri file **$CAMPAIGN_HOME/datakit/nms/fra/js/amcIntegration.js**
1. Modifica la riga 467 del metodo &quot;amcGetSeedMetaData&quot;
1. Modifica `label : [inclView.@label](mailto:inclView.@label)` a `label : String([inclView.@label](mailto:inclView.@label))`

1. Salva.
1. Riavvia il server.

## Se in Adobe Campaign viene visualizzato un errore quando si fa clic sul pulsante Sincronizza {#if-adobe-campaign-displays-an-error-when-clicking-the-synchronize-button}

Se fai clic sul pulsante **Sincronizza** In Adobe Campaign Classic, viene visualizzato il seguente errore:

`Error while executing the method ‘aemListContent' of service [nms:delivery](https://nmsdelivery/)`

Per risolvere questo problema, assicurati che l&#39;URL di connessione AEM configurato negli account esterni sia raggiungibile dal computer.

Interruttore da **localhost** a un indirizzo IP risolto questo problema.

## Se ottieni un errore &#39;Impossibile analizzare XTK Date+Time &#39;undefined&#39;&#39; {#if-you-get-a-cannot-parse-xtk-date-time-undefined-error}

Dopo aver fatto clic su Sincronizza, viene visualizzato un errore di script sulle pagine: Impossibile analizzare XTK Date+Time &#39;undefined&#39;: non è un valore XTK valido.

Ciò si verifica se sono ancora presenti informazioni Adobe Campaign obsolete sull’istanza AEM. Risolvi questo problema rimuovendo tutte le configurazioni di integrazione delle campagne in AEM e ricreandole. Quindi, crea un nuovo modello.

## Se una connessione a SSL visualizza un errore durante la configurazione del servizio cloud {#if-a-connection-to-ssl-displays-an-error-when-setting-up-the-cloud-service}

Nel file error.log di AEM, se vedi quanto segue:

```xml
javax.net.ssl.SSLProtocolException: handshake alert:  unrecognized_name
at sun.security.ssl.ClientHandshaker.handshakeAlert(Unknown Source)
at sun.security.ssl.SSLSocketImpl.recvAlert(Unknown Source)
at sun.security.ssl.SSLSocketImpl.readRecord(Unknown Source)
at sun.security.ssl.SSLSocketImpl.performInitialHandshake(Unknown Source)
at sun.security.ssl.SSLSocketImpl.writeRecord(Unknown Source)
at sun.security.ssl.AppOutputStream.write(Unknown Source)
```

Presenta un ticket al team di supporto Adobe Campaign.

## Se vedi i collegamenti http invece dei collegamenti https previsti nella finestra di dialogo di sincronizzazione {#if-you-see-http-instead-of-an-expected-https-links-in-the-synchronization-dialog}

Con la seguente configurazione:

* Adobe Campaign in hosting tramite https per la comunicazione con AEM Author
* Inverti proxy che termina SSL
* Istanza locale di AEM Author

Quando si tenta di sincronizzare il contenuto nella consegna Adobe Campaign, AEM restituisce un elenco di newsletter. Tuttavia, gli url delle newsletter nell’elenco sono indirizzi http. Quando si seleziona uno degli elementi dell’elenco si verifica un errore.

Per risolvere questo problema:

* Per passare il protocollo originale come intestazione, è necessario configurare il dispatcher o il proxy inverso.
* La *Filtro SSL del servizio Apache Felix Http* nella configurazione OSGi ([https://&lt;host>:&lt;port>/system/console/configMgr](http://localhost:4502/system/console/configMgr)) deve essere configurata per le rispettive impostazioni di intestazione. Vedi [https://felix.apache.org/documentation/subprojects/apache-felix-http-service.html#using-the-ssl-filter](https://felix.apache.org/documentation/subprojects/apache-felix-http-service.html#using-the-ssl-filter)

## Se il modello personalizzato che ho creato non può essere selezionato in Proprietà pagina {#if-the-custom-template-i-created-cannot-be-selected-in-page-properties}

Quando crei un modello di posta per Adobe Campaign, devi includere la proprietà **acMapping** con il valore **mapRecipient** in **jcr:content** nodo del modello, oppure non potrai selezionare il modello Adobe Campaign in **Proprietà pagina** di AEM (campo disabilitato).

## Se ottieni l&#39;errore &quot;com.day.cq.mcm.campaign.servlets.util.ParameterMapper&quot; nei tuoi log {#if-you-get-the-error-com-day-cq-mcm-campaign-servlets-util-parametermapper-in-your-logs}

Quando utilizzi il modello personalizzato, ottieni l’errore &quot;com.day.cq.mcm.campaign.servlets.util.ParameterMapper&quot; nei log. In questo caso, assicurati di installare Featurepack 6576 da [Condivisione pacchetti](/help/sites-administering/package-manager.md#package-share). Questo è un problema in cui se la proprietà acMapping è impostata su un valore diverso da recipient.firstName, viene creato un valore vuoto sul lato Adobe Campaign Manager.
