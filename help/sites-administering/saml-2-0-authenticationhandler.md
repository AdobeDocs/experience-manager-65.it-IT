---
title: Gestore di autenticazione SAML 2.0
description: Scopri il gestore di autenticazione SAML 2.0 in AEM.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: 8e54bccf-0ff1-448d-a237-ec42fd3bfa23
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 2%

---

# Gestore di autenticazione SAML 2.0{#saml-authentication-handler}

AEM viene fornito con un gestore di autenticazione [SAML](https://saml.xml.org/saml-specifications). Questo gestore supporta il protocollo di richiesta di autenticazione [SAML](https://saml.xml.org/saml-specifications) 2.0 (profilo Web-SSO) utilizzando l&#39;associazione `HTTP POST`.

Supporta:

* firma e crittografia dei messaggi
* creazione automatica di utenti
* sincronizzazione dei gruppi con quelli esistenti nell’AEM
* Autenticazione avviata dal provider di servizi e dal provider di identità

Questo gestore archivia il messaggio di risposta SAML crittografato nel nodo utente ( `usernode/samlResponse`) per facilitare la comunicazione con un provider di servizi di terze parti.

>[!NOTE]
>
>Vedere [una dimostrazione dell&#39;integrazione di AEM e SAML](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17481.html?lang=it).

## Configurazione del gestore di autenticazione SAML 2.0 {#configuring-the-saml-authentication-handler}

La [console Web](/help/sites-deploying/configuring-osgi.md) fornisce l&#39;accesso alla configurazione del gestore di autenticazione [SAML](https://saml.xml.org/saml-specifications) 2.0 denominata **Gestore di autenticazione SAML 2.0 Adobe Granite**. È possibile impostare le seguenti proprietà.

>[!NOTE]
>
>Il gestore di autenticazione SAML 2.0 è disabilitato per impostazione predefinita. Imposta almeno una delle seguenti proprietà per abilitare il gestore:
>
>* L’URL del POST del provider di identità o URL IDP.
>* ID dell&#39;entità del provider di servizi.
>

>[!NOTE]
>
>Le asserzioni SAML sono firmate e possono essere facoltativamente crittografate. Affinché ciò funzioni, devi fornire almeno il certificato pubblico del provider di identità nel TrustStore. Per ulteriori informazioni, vedere [Aggiunta del certificato IdP alla sezione TrustStore](/help/sites-administering/saml-2-0-authenticationhandler.md#add-the-idp-certificate-to-the-aem-truststore).

**Percorso** Percorso dell&#39;archivio per il quale Sling deve utilizzare questo gestore di autenticazione. Se è vuoto, il gestore di autenticazione verrà disabilitato.

**Classifica dei servizi** Valore della classificazione dei servizi del framework OSGi per indicare l&#39;ordine in cui chiamare il servizio. Si tratta di un valore intero in cui i valori più alti indicano una precedenza maggiore.

**Alias certificato IDP** Alias del certificato IdP nel truststore globale. Se questa proprietà è vuota, il gestore di autenticazione è disabilitato. Consulta il capitolo &quot;Aggiungere il certificato IdP al TrustStore AEM&quot; di seguito per informazioni su come configurarlo.

**URL IDP** dell&#39;IDP a cui deve essere inviata la richiesta di autenticazione SAML. Se questa proprietà è vuota, il gestore di autenticazione è disabilitato.

>[!CAUTION]
>
>È necessario aggiungere il nome host del provider di identità alla configurazione OSGi **Apache Sling Referrer Filter**. Per ulteriori informazioni, vedere la sezione [Console Web](/help/sites-deploying/configuring-osgi.md).

**ID entità provider di servizi** che identifica in modo univoco il provider di servizi con il provider di identità. Se questa proprietà è vuota, il gestore di autenticazione è disabilitato.

**Reindirizzamento predefinito** Percorso predefinito a cui reindirizzare dopo l&#39;autenticazione.

>[!NOTE]
>
>Questa posizione viene utilizzata solo se il cookie `request-path` non è impostato. Se richiedi una pagina sotto il percorso configurato senza un token di accesso valido, il percorso richiesto viene memorizzato in un cookie
>e il browser verrà reindirizzato nuovamente a questa posizione dopo la corretta autenticazione.

**Attributo ID utente** Il nome dell&#39;attributo contenente l&#39;ID utente utilizzato per autenticare e creare l&#39;utente nel repository di CRX.

>[!NOTE]
>
>L&#39;ID utente non verrà prelevato dal nodo `saml:Subject` dell&#39;asserzione SAML, ma da questo `saml:Attribute`.

**Usa crittografia** Indica se il gestore di autenticazione prevede o meno asserzioni SAML crittografate.

**Creazione automatica utenti CRX** Indica se creare automaticamente gli utenti non esistenti nel repository dopo l&#39;autenticazione riuscita.

>[!CAUTION]
>
>Se la creazione automatica degli utenti di CRX è disabilitata, gli utenti dovranno essere creati manualmente.

**Aggiungi ai gruppi** Indica se un utente deve essere aggiunto automaticamente ai gruppi di CRX dopo l&#39;autenticazione riuscita.

**Appartenenza al gruppo** Il nome dell&#39;attributo saml:Attribute contenente un elenco di gruppi CRX a cui deve essere aggiunto l&#39;utente.

## Aggiungi il certificato IdP al TrustStore AEM {#add-the-idp-certificate-to-the-aem-truststore}

Le asserzioni SAML sono firmate e possono essere facoltativamente crittografate. Affinché questo funzioni, devi fornire almeno il certificato pubblico dell&#39;IdP nell&#39;archivio. A questo scopo, devi:

1. Vai a *http:/serveraddress:serverport/libs/granite/security/content/truststore.html*
1. Premi il collegamento **[!UICONTROL Crea TrustStore]**
1. Immettere la password per TrustStore e premere **[!UICONTROL Salva]**.
1. Fai clic su **[!UICONTROL Gestisci TrustStore]**.
1. Carica il certificato IdP.
1. Prendi nota dell’alias del certificato. L&#39;alias è **[!UICONTROL admin#1436172864930]** nell&#39;esempio seguente.

   ![chlimage_1-372](assets/chlimage_1-372.png)

## Aggiungere la chiave del provider di servizi e la catena di certificati al keystore AEM {#add-the-service-provider-key-and-certificate-chain-to-the-aem-keystore}

>[!NOTE]
>
>I seguenti passaggi sono obbligatori, altrimenti verrà generata la seguente eccezione: `com.adobe.granite.keystore.KeyStoreNotInitialisedException: Uninitialised system trust store`

1. Vai a: [http://localhost:4502/libs/granite/security/content/useradmin.html](http://localhost:4502/libs/granite/security/content/useradmin.html)
1. Modifica l&#39;utente `authentication-service`.
1. Creare un registro chiavi facendo clic su **Crea registro chiavi** in **Impostazioni account**.

>[!NOTE]
>
>I passaggi seguenti sono necessari solo se il gestore deve essere in grado di firmare o decrittografare i messaggi.

1. Crea il certificato/coppia di chiavi per AEM. Il comando per generarlo tramite openssl deve essere simile all&#39;esempio seguente:

   `openssl req -newkey rsa:2048 -new -x509 -days 3652 -nodes -out certificate.crt -keyout key.pem`

1. Converti la chiave nel formato PKCS#8 con codifica DER. Questo è il formato richiesto dal keystore AEM.

   `openssl pkcs8 -topk8 -inform PEM -outform DER -in key.pem -out key.der -nocrypt`

1. Caricare il file della chiave privata facendo clic su **Seleziona file della chiave privata**.
1. Caricare il file del certificato facendo clic su **Seleziona file di portachiavi certificati**.
1. Assegna un alias, come illustrato di seguito:

   ![chlimage_1-373](assets/chlimage_1-373.png)

## Configurare un logger per SAML {#configure-a-logger-for-saml}

È possibile impostare un logger per eseguire il debug di eventuali problemi derivanti da una configurazione non corretta di SAML. Per farlo, segui questi passaggi:

1. Vai alla console Web all&#39;indirizzo *http://localhost:4502/system/console/configMgr*
1. Cerca e fai clic sulla voce denominata **Configurazione logger registrazione Sling Apache**
1. Crea un logger con la seguente configurazione:

   * **Livello registro:** debug
   * **File di registro:** logs/saml.log
   * **Logger:** com.adobe.granite.auth.saml
