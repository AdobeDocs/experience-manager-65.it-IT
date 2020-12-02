---
title: Gestore autenticazione SAML 2.0
seo-title: Gestore autenticazione SAML 2.0
description: Ulteriori informazioni sul gestore di autenticazione SAML 2.0 in AEM.
seo-description: Ulteriori informazioni sul gestore di autenticazione SAML 2.0 in AEM.
uuid: 51f97315-350a-42a4-af2c-2de87307c6ad
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 6ed09b5d-5089-43d2-b9d5-e7db57be5c02
translation-type: tm+mt
source-git-commit: d559a15e3c1c65c39e38935691835146f54a356e
workflow-type: tm+mt
source-wordcount: '853'
ht-degree: 0%

---


# Gestore autenticazione SAML 2.0{#saml-authentication-handler}

AEM viene fornito con un gestore di autenticazione [SAML](http://saml.xml.org/saml-specifications). Questo gestore fornisce il supporto per il protocollo di richiesta autenticazione [SAML](http://saml.xml.org/saml-specifications) 2.0 (profilo Web-SSO) mediante il binding `HTTP POST`.

Supporta:

* firma e cifratura dei messaggi
* creazione automatica degli utenti
* sincronizzazione di gruppi con quelli esistenti in AEM
* Autenticazione avviata dal provider di servizi e dal provider di identità

Questo gestore memorizza il messaggio di risposta SAML crittografato nel nodo utente ( `usernode/samlResponse`) per facilitare la comunicazione con un provider di servizi di terze parti.

>[!NOTE]
>
>Vedere [una dimostrazione dell&#39;integrazione AEM e SAML](https://helpx.adobe.com/experience-manager/kb/simple-saml-demo.html).
>
>Per leggere un articolo della community end to end, fate clic su: [Integrazione SAML con Adobe Experience Manager](https://helpx.adobe.com/experience-manager/using/aem63_saml.html).

## Configurazione del gestore di autenticazione SAML 2.0 {#configuring-the-saml-authentication-handler}

La [console Web](/help/sites-deploying/configuring-osgi.md) fornisce l&#39;accesso alla [configurazione del gestore di autenticazione SAML](http://saml.xml.org/saml-specifications) 2.0 denominata **Adobe Gestore di autenticazione Granite SAML 2.0**. È possibile impostare le seguenti proprietà.

>[!NOTE]
>
>Per impostazione predefinita, il gestore di autenticazione SAML 2.0 è disabilitato. Per attivare il gestore, è necessario impostare almeno una delle seguenti proprietà:
>
>* L&#39;URL del POST del provider di identità.
>* L&#39;ID entità provider di servizi.

>



>[!NOTE]
>
>Le asserzioni SAML sono firmate e facoltativamente possono essere crittografate. Affinché questo funzioni è necessario fornire almeno il certificato pubblico del provider di identità nel TrustStore. Per ulteriori informazioni, vedere [Aggiunta del certificato IdP alla sezione TrustStore](/help/sites-administering/saml-2-0-authenticationhandler.md#add-the-idp-certificate-to-the-aem-truststore).

**Percorso** PathRepository per il quale Sling deve utilizzare il gestore di autenticazione. Se questo campo è vuoto, il gestore di autenticazione verrà disabilitato.

**Servizio** RankingOSGi Framework Service Ranking valore per indicare l&#39;ordine in cui chiamare questo servizio. Si tratta di un valore intero in cui i valori più alti indicano una precedenza maggiore.

**Alias certificato IDP:** l&#39;alias del certificato dell&#39;IdP nell&#39;archivio attendibili globale. Se questa proprietà è vuota, il gestore di autenticazione è disabilitato. Consultate il capitolo &quot;Add the IdP Certificate to the AEM TrustStore&quot; (Aggiungi il certificato IdP a TrustStore) di seguito per informazioni sulla configurazione.

**URL del provider di identità** dell&#39;IDP a cui deve essere inviata la richiesta di autenticazione SAML. Se questa proprietà è vuota, il gestore di autenticazione è disabilitato.

>[!CAUTION]
>
>Il nome host del provider di identità deve essere aggiunto alla configurazione **Apache Sling Referrer Filter** OSGi. Per ulteriori informazioni, vedere la sezione [Console Web](/help/sites-deploying/configuring-osgi.md).

**Service Provider Entity** ID che identifica in modo univoco questo provider di servizi con il provider di identità. Se questa proprietà è vuota, il gestore di autenticazione è disabilitato.

**Reindirizza predefinito:** percorso predefinito a cui reindirizzare dopo l&#39;autenticazione.

>[!NOTE]
>
>Questa posizione viene utilizzata solo se il cookie `request-path` non è impostato. Se richiedete una pagina sotto il percorso configurato senza un token di login valido, il percorso richiesto viene memorizzato in un cookie
>e il browser verrà reindirizzato di nuovo a questa posizione dopo l&#39;autenticazione.

**Attributo ID utente:** il nome dell’attributo contenente l’ID utente utilizzato per autenticare e creare l’utente nell’archivio CRX.

>[!NOTE]
>
>L&#39;ID utente non verrà prelevato dal nodo `saml:Subject` dell&#39;asserzione SAML ma da questo `saml:Attribute`.

**Usa** crittografia: specifica se questo gestore di autenticazione prevede o meno asserzioni SAML crittografate.

**Creazione automatica di** utenti CRXConsente di creare automaticamente utenti non esistenti nella directory archivio dopo l&#39;autenticazione.

>[!CAUTION]
>
>Se la creazione automatica di utenti CRX è disattivata, gli utenti dovranno essere creati manualmente.

**Aggiungi a** gruppiIndica se un utente deve essere aggiunto automaticamente ai gruppi CRX dopo l’autenticazione.

**Appartenenza** al gruppoIl nome dell&#39;attributo saml:Attribute contenente un elenco di gruppi CRX a cui l&#39;utente deve essere aggiunto.

## Aggiungi il certificato IdP al AEM TrustStore {#add-the-idp-certificate-to-the-aem-truststore}

Le asserzioni SAML sono firmate e facoltativamente possono essere crittografate. Affinché questo funzioni, è necessario fornire almeno il certificato pubblico dell&#39;IdP nella directory archivio. A tal fine, è necessario:

1. Vai a *http:/serveraddress:serverport/libs/granite/security/content/truststore.html*
1. Premere il collegamento **[!UICONTROL Create TrustStore]**
1. Immettere la password per TrustStore e premere **[!UICONTROL Save]**.
1. Fare clic su **[!UICONTROL Gestisci TrustStore]**.
1. Caricate il certificato IdP.
1. Prendi nota del certificato Alias. L&#39;alias è **[!UICONTROL admin#1436172864930]** nell&#39;esempio seguente.

   ![chlimage_1-372](assets/chlimage_1-372.png)

## Aggiungere il codice del provider di servizi e la catena di certificati all&#39;archivio chiavi AEM {#add-the-service-provider-key-and-certificate-chain-to-the-aem-keystore}

>[!NOTE]
>
>I passaggi indicati di seguito sono obbligatori, in caso contrario verrà generata l&#39;eccezione seguente: `com.adobe.granite.keystore.KeyStoreNotInitialisedException: Uninitialised system trust store`

1. Vai a: [http://localhost:4502/libs/granite/security/content/useradmin.html](http://localhost:4502/libs/granite/security/content/useradmin.html)
1. Modificate l&#39;utente `authentication-service`.
1. Creare un archivio chiavi facendo clic su **Crea archivio chiavi** in **Impostazioni account**.

>[!NOTE]
>
>La procedura seguente è necessaria solo se il gestore deve essere in grado di firmare o decifrare i messaggi.

1. Caricate il file della chiave privata facendo clic su **Seleziona file di chiave privata**. I contenuti chiave devono essere in formato PKCS#8 con codifica DER.
1. Caricate il file del certificato facendo clic su **Seleziona file catena certificati**.
1. Assegna un alias, come illustrato di seguito:

   ![chlimage_1-373](assets/chlimage_1-373.png)

## Configurare un logger per SAML {#configure-a-logger-for-saml}

È possibile impostare un logger per eseguire il debug di eventuali problemi che potrebbero verificarsi durante la configurazione errata di SAML. È possibile eseguire questa operazione tramite:

1. Passando alla console Web, all&#39;indirizzo *http://localhost:4502/system/console/configMgr*
1. Cercare e fare clic sulla voce denominata **Apache Sling Logging Logging Configuration**
1. Create un logger con la configurazione seguente:

   * **Livello Registro:** Debug
   * **File Di Registro:** logs/saml.log
   * **Logger:** com.adobe.granite.auth.saml

