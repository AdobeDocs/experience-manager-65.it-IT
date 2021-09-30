---
title: Gestore di autenticazione SAML 2.0
seo-title: SAML 2.0 Authentication Handler
description: Scopri il Gestore autenticazione SAML 2.0 in AEM.
seo-description: Learn about the SAML 2.0 Authentication Handler in AEM.
uuid: 51f97315-350a-42a4-af2c-2de87307c6ad
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 6ed09b5d-5089-43d2-b9d5-e7db57be5c02
exl-id: 8e54bccf-0ff1-448d-a237-ec42fd3bfa23
source-git-commit: 6bc60122d2512a6f58c0204cd240a1b99a37ed93
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 1%

---

# Gestore di autenticazione SAML 2.0{#saml-authentication-handler}

AEM viene fornito con un gestore di autenticazione [SAML](http://saml.xml.org/saml-specifications). Questo gestore fornisce il supporto per il protocollo di richiesta dell&#39;autenticazione [SAML](http://saml.xml.org/saml-specifications) 2.0 (profilo Web-SSO) utilizzando il binding `HTTP POST`.

Supporta:

* firma e crittografia dei messaggi
* creazione automatica degli utenti
* sincronizzazione di gruppi con quelli esistenti in AEM
* Autenticazione avviata dal provider di servizi e dal provider di identità

Questo gestore memorizza il messaggio di risposta SAML crittografato nel nodo utente ( `usernode/samlResponse`) per facilitare la comunicazione con un provider di servizi di terze parti.

>[!NOTE]
>
>Vedi [una dimostrazione dell&#39;integrazione di AEM e SAML](https://helpx.adobe.com/experience-manager/kb/simple-saml-demo.html).
>
>Per leggere un articolo della community end to end, fai clic su: [Integrazione di SAML con Adobe Experience Manager](https://helpx.adobe.com/experience-manager/using/aem63_saml.html).

## Configurazione Del Gestore Di Autenticazione SAML 2.0 {#configuring-the-saml-authentication-handler}

La [console Web](/help/sites-deploying/configuring-osgi.md) fornisce l&#39;accesso alla configurazione [SAML](http://saml.xml.org/saml-specifications) 2.0 Authentication Handler denominata **Adobe Granite SAML 2.0 Authentication Handler**. È possibile impostare le seguenti proprietà.

>[!NOTE]
>
>Il gestore di autenticazione SAML 2.0 è disabilitato per impostazione predefinita. Per abilitare il gestore, è necessario impostare almeno una delle seguenti proprietà:
>
>* URL del POST del provider di identità.
>* ID entità fornitore di servizi.

>


>[!NOTE]
>
>Le asserzioni SAML sono firmate e possono essere facoltativamente crittografate. Affinché questo funzioni, è necessario fornire almeno il certificato pubblico del provider di identità nel TrustStore. Per ulteriori informazioni, consulta [Aggiunta del certificato IdP alla sezione TrustStore](/help/sites-administering/saml-2-0-authenticationhandler.md#add-the-idp-certificate-to-the-aem-truststore) .

**** PercorsoRepository per il quale questo gestore di autenticazione deve essere utilizzato da Sling. Se questo campo è vuoto, il gestore di autenticazione verrà disabilitato.

**Valore di classificazione del servizio** RankingOSGi Framework Service per indicare l&#39;ordine in cui chiamare questo servizio. Si tratta di un valore intero in cui i valori superiori indicano una precedenza superiore.

**Alias** del certificato IDPalias del certificato dell&#39;IdP nel truststore globale. Se questa proprietà è vuota, il gestore di autenticazione viene disabilitato. Consulta il capitolo &quot;Aggiungi il certificato IdP al TrustStore AEM&quot; per informazioni su come configurarlo.

**URL del provider di identità** dell’IDP a cui deve essere inviata la richiesta di autenticazione SAML. Se questa proprietà è vuota, il gestore di autenticazione viene disabilitato.

>[!CAUTION]
>
>Il nome host del provider di identità deve essere aggiunto alla configurazione **Apache Sling Referrer Filter** OSGi . Per ulteriori informazioni, consulta la sezione [Console web](/help/sites-deploying/configuring-osgi.md) .

**Service Provider Entity** ID che identifica in modo univoco questo provider di servizi con il provider di identità. Se questa proprietà è vuota, il gestore di autenticazione viene disabilitato.

**Reindirizzamento predefinitoIl percorso predefinito a cui reindirizzare dopo l&#39;autenticazione riuscita.** 

>[!NOTE]
>
>Questa posizione viene utilizzata solo se il cookie `request-path` non è impostato. Se richiedi una pagina sotto il percorso configurato senza un token di accesso valido, il percorso richiesto viene memorizzato in un cookie
>e il browser verrà reindirizzato nuovamente a questa posizione dopo l&#39;autenticazione.

**Attributo ID utente** Il nome dell&#39;attributo contenente l&#39;ID utente utilizzato per autenticare e creare l&#39;utente nell&#39;archivio CRX.

>[!NOTE]
>
>L&#39;ID utente non verrà prelevato dal nodo `saml:Subject` dell&#39;asserzione SAML, ma da questo `saml:Attribute`.

**Usa** crittografiaIndica se questo gestore di autenticazione richiede o meno asserzioni SAML crittografate.

**Crea automaticamente** utenti CRXindipendentemente dal fatto che crei automaticamente utenti non esistenti nell&#39;archivio dopo l&#39;autenticazione riuscita.

>[!CAUTION]
>
>Se la creazione automatica degli utenti CRX è disabilitata, gli utenti dovranno essere creati manualmente.

**Aggiungi ai** gruppiIndica se un utente deve essere aggiunto automaticamente ai gruppi CRX dopo l&#39;autenticazione riuscita.

**Group** MembershipIl nome del saml:Attribute contenente un elenco di gruppi CRX a cui deve essere aggiunto questo utente.

## Aggiungi il certificato IdP al TrustStore AEM {#add-the-idp-certificate-to-the-aem-truststore}

Le asserzioni SAML sono firmate e possono essere facoltativamente crittografate. Affinché ciò funzioni, devi fornire almeno il certificato pubblico dell’IdP nell’archivio. Per fare questo è necessario:

1. Vai a *http:/serveraddress:serverport/libs/granite/security/content/truststore.html*
1. Premere il **[!UICONTROL Crea collegamento TrustStore]**
1. Immettere la password per TrustStore e premere **[!UICONTROL Save]**.
1. Fai clic su **[!UICONTROL Gestisci TrustStore]**.
1. Carica il certificato IdP.
1. Prendi nota dell&#39;alias del certificato. L&#39;alias è **[!UICONTROL admin#1436172864930]** nell&#39;esempio seguente.

   ![chlimage_1-372](assets/chlimage_1-372.png)

## Aggiungi il codice del fornitore di servizi e la catena di certificati al AEM keystore {#add-the-service-provider-key-and-certificate-chain-to-the-aem-keystore}

>[!NOTE]
>
>I passaggi seguenti sono obbligatori, altrimenti verrà lanciata la seguente eccezione: `com.adobe.granite.keystore.KeyStoreNotInitialisedException: Uninitialised system trust store`

1. Vai a: [http://localhost:4502/libs/granite/security/content/useradmin.html](http://localhost:4502/libs/granite/security/content/useradmin.html)
1. Modifica l&#39;utente `authentication-service` .
1. Crea un KeyStore facendo clic su **Crea KeyStore** in **Impostazioni account**.

>[!NOTE]
>
>I passaggi seguenti sono necessari solo se il gestore deve essere in grado di firmare o decrittografare i messaggi.

1. Carica il file della chiave privata facendo clic su **Seleziona file di chiave privata**. La chiave deve essere in formato PKCS#8 con codifica DER.
1. Carica il file del certificato facendo clic su **Seleziona file della catena di certificati**.
1. Assegna un alias, come illustrato di seguito:

   ![chlimage_1-373](assets/chlimage_1-373.png)

## Configurare un logger per SAML {#configure-a-logger-for-saml}

È possibile impostare un logger per eseguire il debug di eventuali problemi derivanti dalla configurazione errata di SAML. Per farlo, segui questi passaggi:

1. Andando alla console Web all&#39;indirizzo *http://localhost:4502/system/console/configMgr*
1. Cerca e fai clic sulla voce denominata **Configurazione logger di registrazione Sling Apache**
1. Crea un logger con la seguente configurazione:

   * **Livello di log:** Debug
   * **File di registro:** logs/saml.log
   * **Logger:** com.adobe.granite.auth.saml
