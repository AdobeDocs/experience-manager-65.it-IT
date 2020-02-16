---
title: Risoluzione dei problemi dell'integrazione con Adobe Campaign
seo-title: Risoluzione dei problemi dell'integrazione con Adobe Campaign
description: Scopri come risolvere i problemi relativi all'integrazione con Adobe Campaign.
seo-description: Scopri come risolvere i problemi relativi all'integrazione con Adobe Campaign.
uuid: 835ac2c3-ef2f-4963-9047-aeda3647b114
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: b1d45f01-78de-423c-8f6b-5cb7067c3a2f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Risoluzione dei problemi dell&#39;integrazione con Adobe Campaign{#troubleshooting-your-adobe-campaign-integration}

>[!NOTE]
>
>Questa pagina è valida per Campaign Classic.

I seguenti suggerimenti per la risoluzione dei problemi aiutano a risolvere i problemi più comuni che si possono incontrare quando si integra AEM con Adobe Campaign:

## Suggerimenti generali per la risoluzione dei problemi {#general-troubleshooting-tips}

Per entrambe le integrazioni, potete verificare se le chiamate HTTP vengono inviate (AEM > Adobe Campaign, Adobe Campaign > AEM):

* Se le integrazioni non vanno a buon fine, accertatevi che queste chiamate arrivino dall&#39;altra parte (per evitare problemi firewall/SSL).
* Per la funzionalità AEM, noterete che le chiamate json sono richieste dall’interfaccia di authoring di AEM; questi non devono generare un errore HTTP-500. Se si verificano errori HTTP-500, controllate se `error.log` sono disponibili ulteriori informazioni.
* L’aumento del livello di debug per le classi di campagna in AEM aiuta anche a risolvere i problemi.

## Se la connessione ha esito negativo {#if-the-connection-fails}

Verifica di aver configurato l&#39;operatore **server** di posta elettronica in Adobe Campaign.

## Se le immagini non vengono visualizzate nella console di Adobe Campaign {#if-images-do-not-appear-in-the-adobe-campaign-console}

Controllare l&#39;origine HTML e verificare che sia possibile aprire l&#39;URL dal computer client. Se l’URL contiene localhost:4503, modifica la configurazione di Day CQ Link Externalizer nell’istanza di creazione per puntare a un’istanza di pubblicazione raggiungibile dal computer della console di Adobe Campaign.

Consultate [Configurazione dell’esternalizzatore.](/help/sites-administering/campaignstandard.md#configuring-the-externalizer)

## Se non è possibile connettersi da AEM ad Adobe Campaign {#if-you-cannot-connect-from-aem-to-adobe-campaign}

Cerca il seguente messaggio di errore in Adobe Campaign:

`No datasource defined in the instance 'default'.`

`Make sure the DNS alias used to access the server is correct (for example, avoid hard-coded IP addresses). (iRc=16384)`

Per risolvere il problema, modificare quanto segue in **$CAMPAIGN_HOME/conf/config-&lt;instance-name>.xml**:

`<dataStore hosts="*" lang="en_GB">`

## Se non vengono visualizzati dati nella finestra di dialogo Adobe Campaign {#if-no-data-displays-in-the-adobe-campaign-dialog}

In Adobe Campaign, accertatevi di non avere una barra finale (/) dopo il numero della porta.

![chlimage_1-149](assets/chlimage_1-149.png)

## Se viene visualizzato un avviso relativo alle impostazioni internazionali {#if-you-get-a-warning-about-your-setlocale}

Se state avviando il servizio Apache HTTPD e vedete l&#39;errore, `"Warning: setlocale: LC_CTYPE cannot change locale"` accertatevi che nel sistema sia installata la lingua **** en_CA.ISO-8859-15.

È possibile verificare se è installato utilizzando `local -a`. Se non è installato, è possibile eseguire la patch **/usr/local/neolane/nl6/env.sh** script e modificare le impostazioni internazionali in modo da impostarne una installata.

## Se viene visualizzato un errore durante la compilazione dello script &#39;get_nms_amcGetSeedMetaData_jssp&#39; {#if-you-get-an-error-while-compiling-script-get-nms-amcgetseedmetadata-jssp}

Se viene visualizzato il seguente messaggio di errore nel file di registro di AEM:

`com.day.cq.mcm.campaign.impl.CampaignConnectorImpl Internal Adobe Campaign error: response body is Error while compiling script 'get_nms_amcGetSeedMetaData_jssp' line 45: String.prototype.toJSON called on incompatible XML.`

Utilizzate la seguente soluzione alternativa:

1. Apri file **$CAMPAIGN_HOME/datakit/nms/fra/js/amcIntegration.js**
1. Modifica la riga 467 del metodo &quot;amcGetSeedMetaData&quot;
1. Change `label : [inclView.@label](mailto:inclView.@label)` to `label : String([inclView.@label](mailto:inclView.@label))`

1. Salva.
1. Riavviate il server.

## Se Adobe Campaign visualizza un errore quando fai clic sul pulsante Sincronizza {#if-adobe-campaign-displays-an-error-when-clicking-the-synchronize-button}

Se quando fai clic sul pulsante **Sincronizza** in Adobe Campaign Classic, viene visualizzato il seguente errore:

`Error while executing the method ‘aemListContent' of service [nms:delivery](https://nmsdelivery/)`

Per risolvere questo problema, accertatevi che l&#39;URL di connessione AEM configurato negli account esterni sia raggiungibile dal computer.

Il passaggio da **localhost** a indirizzo IP ha risolto il problema.

## Se viene visualizzato un errore &#39;Impossibile analizzare XTK Date+Time &#39;undefined&#39; {#if-you-get-a-cannot-parse-xtk-date-time-undefined-error}

Dopo aver fatto clic su Sincronizza, si verifica un errore di script sulle pagine: Impossibile analizzare XTK Date+Time &#39;undefined&#39;: non è un valore XTK valido.

Ciò si verifica se nell’istanza di AEM sono ancora presenti informazioni Adobe Campaign non aggiornate. Risolvete questo problema rimuovendo tutte le configurazioni di integrazione delle campagne presenti in AEM e ricreandole. Quindi, create un nuovo modello.

## Se una connessione a SSL visualizza un errore durante la configurazione del servizio cloud {#if-a-connection-to-ssl-displays-an-error-when-setting-up-the-cloud-service}

Nel registro error.log di AEM, se vengono visualizzati i seguenti elementi:

```xml
javax.net.ssl.SSLProtocolException: handshake alert:  unrecognized_name
at sun.security.ssl.ClientHandshaker.handshakeAlert(Unknown Source)
at sun.security.ssl.SSLSocketImpl.recvAlert(Unknown Source)
at sun.security.ssl.SSLSocketImpl.readRecord(Unknown Source)
at sun.security.ssl.SSLSocketImpl.performInitialHandshake(Unknown Source)
at sun.security.ssl.SSLSocketImpl.writeRecord(Unknown Source)
at sun.security.ssl.AppOutputStream.write(Unknown Source)
```

Richiedi un ticket al team di supporto di Adobe Campaign.

## Se nella finestra di dialogo di sincronizzazione visualizzate http invece dei collegamenti https previsti {#if-you-see-http-instead-of-an-expected-https-links-in-the-synchronization-dialog}

Con la seguente configurazione:

* Adobe Campaign in hosting tramite https per le comunicazioni con AEM Author
* Inverti proxy che termina SSL
* Istanza locale di AEM Author

Quando si tenta di sincronizzare il contenuto nella distribuzione di Adobe Campaign, AEM restituisce un elenco di newsletter. Tuttavia, gli URL delle newsletter presenti nell&#39;elenco sono indirizzi http. Quando si seleziona una delle voci nell&#39;elenco si verifica un errore.

Per risolvere il problema:

* Il dispatcher o il proxy inverso devono essere configurati per trasmettere il protocollo originale come intestazione.
* Il filtro *SSL del servizio* Apache Felix Http nella configurazione OSGi ([https://&lt;host>:&lt;porta>/system/console/configMgr](http://localhost:4502/system/console/configMgr)) deve essere configurato nelle rispettive impostazioni di intestazione. Consultate [https://felix.apache.org/documentation/subprojects/apache-felix-http-service.html#using-the-ssl-filter](https://felix.apache.org/documentation/subprojects/apache-felix-http-service.html#using-the-ssl-filter)

## Se il modello personalizzato che ho creato non può essere selezionato in Proprietà pagina {#if-the-custom-template-i-created-cannot-be-selected-in-page-properties}

Quando crei un modello di posta elettronica per Adobe Campaign, devi includere la proprietà **acMapping** con il valore **mapRecipient** nel nodo **jcr:content** del modello, oppure non sarai in grado di selezionare il modello Adobe Campaign in Proprietà **** pagina di AEM (campo disabilitato).

## Se viene visualizzato l’errore &quot;com.day.cq.mcm.campaign.servlets.util.ParameterMapper&quot; nei registri {#if-you-get-the-error-com-day-cq-mcm-campaign-servlets-util-parametermapper-in-your-logs}

Quando usate il modello personalizzato, nei registri viene visualizzato l’errore &quot;com.day.cq.mcm.campaign.servlets.util.ParameterMapper&quot;. In questo caso, accertatevi di installare Feature Pack 6576 da [Package Share](/help/sites-administering/package-manager.md#package-share). Si tratta di un problema per il quale se la proprietà acMapping è impostata su un valore diverso da Recipient.firstName, viene creato un valore vuoto sul lato Adobe Campaign Manager.
