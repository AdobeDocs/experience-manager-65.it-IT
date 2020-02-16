---
title: Configurare le impostazioni del provider di servizi SAML
seo-title: Configurare le impostazioni del provider di servizi SAML
description: Puoi configurare le impostazioni del provider di servizi SAML per consentire agli utenti di accedere e autenticare i moduli AEM tramite un provider di identità (IDP) di terze parti specificato.
seo-description: Puoi configurare le impostazioni del provider di servizi SAML per consentire agli utenti di accedere e autenticare i moduli AEM tramite un provider di identità (IDP) di terze parti specificato.
uuid: 14c706ad-8b1c-4c03-9cd4-97424f2162bc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 1169d0d1-cbfb-486b-acca-9b9de3d410dc
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configurare le impostazioni del provider di servizi SAML{#configure-saml-service-provider-settings}

SAML (Security Assertion Markup Language) è una delle opzioni che è possibile selezionare al momento della configurazione dell&#39;autorizzazione per un dominio Enterprise o ibrido. SAML viene utilizzato principalmente per supportare SSO tra più domini. Quando SAML è configurato come provider di autenticazione, gli utenti accedono e autenticano i moduli AEM tramite un provider di identità (IDP) di terze parti specificato.

Per una spiegazione di SAML, vedere [Security Assertion Markup Language (SAML) V2.0 Technical Overview (Panoramica](https://www.oasis-open.org/committees/download.php/20645/sstc-saml-tech-overview-2%200-draft-10.pdf)tecnica di SAML).

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Configurazione > Impostazioni provider di servizi SAML.
1. Nella casella ID entità fornitore di servizi, digitare un ID univoco da utilizzare come identificatore per l&#39;implementazione del provider di servizi di moduli AEM. Potete inoltre specificare questo ID univoco al momento della configurazione dell’IDP (ad esempio, `um.lc.com`). Potete anche utilizzare l&#39;URL utilizzato per accedere ai moduli AEM (ad esempio, `https://AEMformsserver`).
1. Nella casella URL base provider di servizi, digitare l&#39;URL di base per il server moduli (ad esempio, `https://AEMformsserver:8080`).
1. (Facoltativo) Per consentire ai moduli AEM di inviare richieste di autenticazione firmate all’IDP, effettuare le seguenti operazioni:

   * Utilizzare Trust Manager per importare una credenziale in formato PKCS #12 con le credenziali per la firma dei documenti selezionate come tipo di archivio attendibili. (vedere [Gestione delle credenziali](/help/forms/using/admin-help/local-credentials.md#managing-local-credentials)locali.)
   * Nell&#39;elenco Alias chiave credenziali provider di servizi, selezionare l&#39;alias assegnato alla credenziale in Trust Store.
   * Fate clic su Esporta per salvare il contenuto dell’URL in un file e quindi importare il file nell’IDP.

1. (Facoltativo) Nell&#39;elenco Criteri ID nome provider di servizi, selezionare il formato del nome utilizzato dall&#39;IDP per identificare l&#39;utente in un&#39;asserzione SAML. Le opzioni sono Non specificato, E-mail e Nome qualificato del dominio Windows.

   >[!NOTE]
   >
   >I formati dei nomi non fanno distinzione tra maiuscole e minuscole.

1. (Facoltativo) Selezionate Abilita prompt di autenticazione per gli utenti locali. Quando questa opzione è selezionata, gli utenti visualizzeranno due collegamenti:

   * un collegamento alla pagina di accesso del provider di identità SAML di terze parti, in cui gli utenti appartenenti a un dominio Enterprise possono effettuare l&#39;autenticazione.
   * un collegamento alla pagina di accesso ai moduli AEM, in cui gli utenti appartenenti a un dominio locale possono effettuare l&#39;autenticazione.
   Se questa opzione non è selezionata, gli utenti verranno indirizzati direttamente alla pagina di accesso del provider di identità SAML di terze parti, dove gli utenti appartenenti a un dominio Enterprise possono effettuare l&#39;autenticazione.

1. (Facoltativo) Selezionare Abilita binding artefatti per abilitare il supporto per il binding degli artefatti. Per impostazione predefinita, il binding POST è utilizzato con SAML. Tuttavia, se è stato configurato Binding degli artefatti, selezionare questa opzione. Quando questa opzione è selezionata, l&#39;affermazione utente effettiva non viene passata attraverso la richiesta Browser. Al contrario, viene passato un puntatore all&#39;asserzione e l&#39;asserzione viene recuperata utilizzando una chiamata al servizio Web di back-end.
1. (Facoltativo) Selezionare Abilita binding di reindirizzamento per supportare i binding SAML che utilizzano i reindirizzamenti.
1. (Facoltativo) In Proprietà personalizzate, specificate ulteriori proprietà. Le proprietà aggiuntive sono coppie nome=valore separate da nuove righe.

   * Puoi configurare i moduli AEM per emettere un&#39;asserzione SAML per un periodo di validità che corrisponde al periodo di validità di un&#39;asserzione di terze parti. Per rispettare il timeout di asserzione SAML di terze parti, aggiungi la seguente riga in Proprietà personalizzate:

      `saml.sp.honour.idp.assertion.expiry=true`

   * Aggiungete la seguente proprietà personalizzata per l’utilizzo di RelayState per determinare l’URL a cui verrà reindirizzato l’utente dopo l’autenticazione.

      `saml.sp.use.relaystate=true`

   * Aggiungete la seguente proprietà personalizzata per configurare l&#39;URL per le pagine Java Server (JSP) personalizzate, che verranno utilizzate per eseguire il rendering dell&#39;elenco registrato di provider di identità. Se non è stata implementata un&#39;applicazione Web personalizzata, verrà utilizzata la pagina Gestione utente predefinita per eseguire il rendering dell&#39;elenco.
   `saml.sp.discovery.url=/custom/custom.jsp`

1. Fate clic su Salva.

