---
title: Configurare le impostazioni del provider di servizi SAML
seo-title: Configure SAML service provider settings
description: È possibile configurare le impostazioni del provider di servizi SAML per consentire agli utenti di effettuare l’accesso e l’autenticazione per AEM moduli tramite un provider di identità di terze parti (IDP) specifico.
seo-description: You can configure SAML service provider settings to allow users to login and authenticate to AEM forms via a specified third-party identity provider (IDP).
uuid: 14c706ad-8b1c-4c03-9cd4-97424f2162bc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 1169d0d1-cbfb-486b-acca-9b9de3d410dc
exl-id: dd302cfb-eae1-4189-aa7b-9f2533ebd164
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 0%

---

# Configurare le impostazioni del provider di servizi SAML{#configure-saml-service-provider-settings}

SAML (Security Assertion Markup Language) è una delle opzioni che è possibile selezionare durante la configurazione dell&#39;autorizzazione per un dominio enterprise o ibrido. SAML viene utilizzato principalmente per supportare SSO in più domini. Quando SAML è configurato come provider di autenticazione, gli utenti accedono e autenticano i moduli AEM tramite un provider di identità di terze parti (IDP) specifico.

Per una spiegazione di SAML, vedi [Panoramica tecnica di Security Assertion Markup Language (SAML) V2.0](https://www.oasis-open.org/committees/download.php/20645/sstc-saml-tech-overview-2%200-draft-10.pdf).

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Configurazione > Impostazioni provider di servizi SAML.
1. Nella casella ID entità fornitore di servizi, digitare un ID univoco da utilizzare come identificatore per l’implementazione del provider di servizi di AEM forms. Puoi anche specificare questo ID univoco durante la configurazione dell’IDP (ad esempio, `um.lc.com`.) È inoltre possibile utilizzare l’URL utilizzato per accedere AEM moduli (ad esempio, `https://AEMformsserver`).
1. Nella casella URL di base del provider di servizi, digitare l’URL di base per il server dei moduli (ad esempio, `https://AEMformsserver:8080`).
1. (Facoltativo) Per consentire AEM moduli di inviare richieste di autenticazione firmate all’IDP, eseguire le seguenti operazioni:

   * Utilizzare Trust Manager per importare una credenziale in formato PKCS #12 con la credenziale di firma documento selezionata come tipo di archivio attendibile. (Vedi [Gestione delle credenziali locali](/help/forms/using/admin-help/local-credentials.md#managing-local-credentials).)
   * Nell&#39;elenco Alias chiave credenziale del fornitore di servizi selezionare l&#39;alias assegnato alla credenziale in Archivio fonti attendibili.
   * Fai clic su Esporta per salvare il contenuto dell’URL in un file e quindi importarlo nell’IDP.

1. (Facoltativo) Nell&#39;elenco Criteri ID provider di servizi, selezionare il formato del nome utilizzato dall&#39;IDP per identificare l&#39;utente in un&#39;asserzione SAML. Le opzioni sono Non specificato, Email e Nome certificato del dominio Windows.

   >[!NOTE]
   >
   >I formati dei nomi non sono sensibili all’uso di maiuscole e minuscole.

1. (Facoltativo) Selezionare Abilita prompt di autenticazione per gli utenti locali. Quando questa opzione è selezionata, gli utenti visualizzano due collegamenti:

   * un collegamento alla pagina di accesso del provider di identità SAML di terze parti, in cui gli utenti che appartengono a un dominio Enterprise possono effettuare l’autenticazione.
   * un collegamento alla pagina di accesso ai moduli di AEM, in cui possono essere autenticati gli utenti che appartengono a un dominio locale.

   Quando questa opzione non è selezionata, gli utenti verranno indirizzati direttamente alla pagina di accesso del provider di identità SAML di terze parti, dove gli utenti che appartengono a un dominio Enterprise possono effettuare l’autenticazione.

1. (Facoltativo) Selezionare Abilita binding artefatti per abilitare il supporto del binding degli artefatti. Per impostazione predefinita, il binding di POST viene utilizzato con SAML. Se tuttavia è stato configurato Binding degli artefatti, selezionare questa opzione. Quando questa opzione è selezionata, l&#39;asserzione utente effettiva non viene passata attraverso la richiesta Browser. Viene invece passato un puntatore all’asserzione e l’asserzione viene recuperata utilizzando una chiamata al servizio Web di backend.
1. (Facoltativo) Selezionare Abilita binding di reindirizzamento per supportare i binding SAML che utilizzano i reindirizzamenti.
1. (Facoltativo) In Proprietà personalizzate, specifica ulteriori proprietà. Le proprietà aggiuntive sono coppie nome=valore separate da nuove righe.

   * È possibile configurare AEM moduli per emettere un’asserzione SAML per un periodo di validità corrispondente al periodo di validità di un’asserzione di terze parti. Per rispettare il timeout dell’asserzione SAML di terze parti, aggiungi la seguente riga in Proprietà personalizzate:

      `saml.sp.honour.idp.assertion.expiry=true`

   * Aggiungi la seguente proprietà personalizzata per l&#39;utilizzo di RelayState per determinare l&#39;URL in cui l&#39;utente verrà reindirizzato dopo l&#39;autenticazione.

      `saml.sp.use.relaystate=true`

   * Aggiungi la seguente proprietà personalizzata per configurare l&#39;URL per le pagine Java Server personalizzate (JSP), che verranno utilizzate per eseguire il rendering dell&#39;elenco registrato dei provider di identità. Se non hai implementato un&#39;applicazione Web personalizzata, utilizzerà la pagina Gestione utente predefinita per eseguire il rendering dell&#39;elenco.

   `saml.sp.discovery.url=/custom/custom.jsp`

1. Fai clic su Salva.
