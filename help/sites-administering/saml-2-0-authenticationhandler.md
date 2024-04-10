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

L’AEM viene fornito con un [SAML](https://saml.xml.org/saml-specifications) gestore di autenticazione. Questo gestore supporta [SAML](https://saml.xml.org/saml-specifications) 2.0 Authentication Request Protocol (profilo Web-SSO) utilizzando `HTTP POST` binding.

Supporta:

* firma e crittografia dei messaggi
* creazione automatica di utenti
* sincronizzazione dei gruppi con quelli esistenti nell’AEM
* Autenticazione avviata dal provider di servizi e dal provider di identità

Questo gestore memorizza il messaggio di risposta SAML crittografato nel nodo utente ( `usernode/samlResponse`) per facilitare la comunicazione con un fornitore di servizi di terze parti.

>[!NOTE]
>
>Consulta [una dimostrazione dell’integrazione di AEM e SAML](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17481.html).

## Configurazione del gestore di autenticazione SAML 2.0 {#configuring-the-saml-authentication-handler}

Il [Console web](/help/sites-deploying/configuring-osgi.md) fornisce accesso al [SAML](https://saml.xml.org/saml-specifications) Configurazione del gestore di autenticazione 2.0 chiamata **Gestore autenticazione SAML 2.0 Adobe Granite**. È possibile impostare le seguenti proprietà.

>[!NOTE]
>
>Il gestore di autenticazione SAML 2.0 è disabilitato per impostazione predefinita. Imposta almeno una delle seguenti proprietà per abilitare il gestore:
>
>* L’URL del POST del provider di identità o URL IDP.
>* ID dell&#39;entità del provider di servizi.
>

>[!NOTE]
>
>Le asserzioni SAML sono firmate e possono essere facoltativamente crittografate. Affinché ciò funzioni, devi fornire almeno il certificato pubblico del provider di identità nel TrustStore. Consulta [Aggiunta del certificato IdP al TrustStore](/help/sites-administering/saml-2-0-authenticationhandler.md#add-the-idp-certificate-to-the-aem-truststore) per ulteriori informazioni.

**Percorso** Percorso dell’archivio per il quale Sling deve utilizzare questo gestore di autenticazione. Se è vuoto, il gestore di autenticazione verrà disabilitato.

**Classifica dei servizi** Valore di classificazione del servizio del framework OSGi per indicare l’ordine in cui chiamare questo servizio. Si tratta di un valore intero in cui i valori più alti indicano una precedenza maggiore.

**Alias certificato IDP** Alias del certificato del provider di identità nel truststore globale. Se questa proprietà è vuota, il gestore di autenticazione è disabilitato. Consulta il capitolo &quot;Aggiungere il certificato IdP al TrustStore AEM&quot; di seguito per informazioni su come configurarlo.

**URL IDP** URL dell&#39;IDP a cui inviare la richiesta di autenticazione SAML. Se questa proprietà è vuota, il gestore di autenticazione è disabilitato.

>[!CAUTION]
>
>Il nome host del provider di identità deve essere aggiunto al **Filtro referrer Apache Sling** Configurazione OSGi. Consulta la [Console web](/help/sites-deploying/configuring-osgi.md) per ulteriori informazioni.

**ID entità provider di servizi** ID che identifica in modo univoco questo provider di servizi con il provider di identità. Se questa proprietà è vuota, il gestore di autenticazione è disabilitato.

**Reindirizzamento predefinito** Percorso predefinito a cui reindirizzare dopo l’autenticazione.

>[!NOTE]
>
>Questa posizione viene utilizzata solo se `request-path` cookie non impostato. Se richiedi una pagina sotto il percorso configurato senza un token di accesso valido, il percorso richiesto viene memorizzato in un cookie
>e il browser verrà reindirizzato nuovamente a questa posizione dopo la corretta autenticazione.

**Attributo User-ID** Nome dell’attributo contenente l’ID utente utilizzato per autenticare e creare l’utente nell’archivio CRX.

>[!NOTE]
>
>L&#39;ID utente non verrà ricavato da `saml:Subject` nodo dell&#39;asserzione SAML, ma da questo `saml:Attribute`.

**Usa crittografia** Indica se il gestore di autenticazione prevede o meno asserzioni SAML crittografate.

**Crea automaticamente utenti CRX** Specifica se creare automaticamente o meno utenti non esistenti nel repository dopo l&#39;autenticazione riuscita.

>[!CAUTION]
>
>Se la creazione automatica degli utenti CRX è disabilitata, gli utenti dovranno essere creati manualmente.

**Aggiungi a gruppi** Specifica se un utente deve essere aggiunto automaticamente ai gruppi CRX dopo la corretta autenticazione.

**Appartenenza al gruppo** Nome dell&#39;attributo saml:Attribute contenente un elenco di gruppi CRX a cui l&#39;utente deve essere aggiunto.

## Aggiungi il certificato IdP al TrustStore AEM {#add-the-idp-certificate-to-the-aem-truststore}

Le asserzioni SAML sono firmate e possono essere facoltativamente crittografate. Affinché questo funzioni, devi fornire almeno il certificato pubblico dell&#39;IdP nell&#39;archivio. A questo scopo, devi:

1. Vai a *http:/serveraddress:serverport/libs/granite/security/content/truststore.html*
1. Premere il tasto **[!UICONTROL Crea collegamento TrustStore]**
1. Immettere la password per il TrustStore e premere **[!UICONTROL Salva]**.
1. Fai clic su **[!UICONTROL Gestisci TrustStore]**.
1. Carica il certificato IdP.
1. Prendi nota dell’alias del certificato. L’alias è **[!UICONTROL admin#1436172864930]** nell’esempio seguente.

   ![chlimage_1-372](assets/chlimage_1-372.png)

## Aggiungere la chiave del provider di servizi e la catena di certificati al keystore AEM {#add-the-service-provider-key-and-certificate-chain-to-the-aem-keystore}

>[!NOTE]
>
>I passaggi seguenti sono obbligatori, altrimenti verrà generata la seguente eccezione: `com.adobe.granite.keystore.KeyStoreNotInitialisedException: Uninitialised system trust store`

1. Vai a: [http://localhost:4502/libs/granite/security/content/useradmin.html](http://localhost:4502/libs/granite/security/content/useradmin.html)
1. Modifica il `authentication-service` utente.
1. Creare un registro chiavi facendo clic su **Crea registro chiavi** in **Impostazioni account**.

>[!NOTE]
>
>I passaggi seguenti sono necessari solo se il gestore deve essere in grado di firmare o decrittografare i messaggi.

1. Crea il certificato/coppia di chiavi per AEM. Il comando per generarlo tramite openssl deve essere simile all&#39;esempio seguente:

   `openssl req -newkey rsa:2048 -new -x509 -days 3652 -nodes -out certificate.crt -keyout key.pem`

1. Converti la chiave nel formato PKCS#8 con codifica DER. Questo è il formato richiesto dal keystore AEM.

   `openssl pkcs8 -topk8 -inform PEM -outform DER -in key.pem -out key.der -nocrypt`

1. Carica il file della chiave privata facendo clic su **Seleziona file di chiave privata**.
1. Carica il file del certificato facendo clic su **Seleziona file di portachiavi certificati**.
1. Assegna un alias, come illustrato di seguito:

   ![chlimage_1-373](assets/chlimage_1-373.png)

## Configurare un logger per SAML {#configure-a-logger-for-saml}

È possibile impostare un logger per eseguire il debug di eventuali problemi derivanti da una configurazione non corretta di SAML. Per farlo, segui questi passaggi:

1. Vai alla console web, all’indirizzo *http://localhost:4502/system/console/configMgr*
1. Cerca e fai clic sulla voce denominata **Configurazione logger registrazione Sling Apache**
1. Crea un logger con la seguente configurazione:

   * **Livello registro:** Debug
   * **File di registro:** logs/saml.log
   * **Logger:** com.adobe.granite.auth.saml
