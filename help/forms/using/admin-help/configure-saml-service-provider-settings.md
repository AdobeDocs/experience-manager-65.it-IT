---
title: Configura impostazioni provider di servizi SAML
description: È possibile configurare le impostazioni del provider di servizi SAML per consentire agli utenti di accedere e autenticarsi ai moduli AEM tramite un provider di identità di terze parti (IDP) specificato.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: dd302cfb-eae1-4189-aa7b-9f2533ebd164
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 0%

---

# Configura impostazioni provider di servizi SAML{#configure-saml-service-provider-settings}

Il linguaggio SAML (Security Assertion Markup Language) è una delle opzioni che è possibile selezionare durante la configurazione dell&#39;autorizzazione per un dominio enterprise o ibrido. SAML viene utilizzato principalmente per supportare SSO tra più domini. Quando SAML è configurato come provider di autenticazione, gli utenti accedono e si autenticano nei moduli AEM tramite un provider di identità (IDP) di terze parti specificato.

Per una spiegazione di SAML, vedere [Panoramica tecnica SAML (Security Assertion Markup Language) V2.0](https://www.oasis-open.org/committees/download.php/20645/sstc-saml-tech-overview-2%200-draft-10.pdf).

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Configurazione > Impostazioni provider di servizi SAML.
1. Nella casella ID entità fornitore di servizi digitare un ID univoco da utilizzare come identificatore per l&#39;implementazione del provider di servizi AEM forms. Puoi anche specificare questo ID univoco durante la configurazione dell’IDP (ad esempio, `um.lc.com`.) Puoi anche utilizzare l’URL utilizzato per accedere ai moduli AEM (ad esempio, `https://AEMformsserver`).
1. Nella casella URL di base provider di servizi digitare l&#39;URL di base per il server Forms, ad esempio `https://AEMformsserver:8080`).
1. (Facoltativo) Per consentire ai moduli AEM di inviare richieste di autenticazione firmate all&#39;IDP, eseguire le operazioni seguenti:

   * Utilizzare Gestione fonti attendibili per importare una credenziale in formato PKCS #12 con le credenziali di firma del documento selezionate come tipo di archivio fonti attendibili. (vedere [Gestione delle credenziali locali](/help/forms/using/admin-help/local-credentials.md#managing-local-credentials).)
   * Nell&#39;elenco Alias chiave credenziale provider di servizi selezionare l&#39;alias assegnato alle credenziali nell&#39;archivio fonti attendibili.
   * Fare clic su Esporta per salvare il contenuto dell&#39;URL in un file e quindi importare il file nell&#39;IDP.

1. (Facoltativo) Nell&#39;elenco Criterio ID nome provider di servizi selezionare il formato del nome utilizzato dall&#39;IDP per identificare l&#39;utente in un&#39;asserzione SAML. Le opzioni disponibili sono Non specificato, E-mail e Nome qualificato dominio Windows.

   >[!NOTE]
   >
   >I formati dei nomi non fanno distinzione tra maiuscole e minuscole.

1. (Facoltativo) Seleziona Abilita Richiesta Di Autenticazione Per Utenti Locali. Quando questa opzione è selezionata, gli utenti visualizzeranno due collegamenti:

   * un collegamento alla pagina di accesso del provider di identità SAML di terze parti, in cui gli utenti che appartengono a un dominio Enterprise possono eseguire l’autenticazione.
   * un collegamento alla pagina di accesso ai moduli AEM, in cui gli utenti che appartengono a un dominio locale possono eseguire l’autenticazione.

   Se questa opzione non è selezionata, gli utenti verranno indirizzati direttamente alla pagina di accesso del provider di identità SAML di terze parti, in cui gli utenti che appartengono a un dominio Enterprise possono eseguire l’autenticazione.

1. (Facoltativo) Seleziona Abilita associazione artefatto per abilitare il supporto dell’associazione artefatto. Per impostazione predefinita, l&#39;associazione POST viene utilizzata con SAML. Tuttavia, se hai configurato l’associazione degli artefatti, seleziona questa opzione. Quando questa opzione è selezionata, l’asserzione utente effettiva non viene trasmessa attraverso la richiesta Browser. Viene invece passato un puntatore all’asserzione e l’asserzione viene recuperata utilizzando una chiamata di servizio web back-end.
1. (Facoltativo) Seleziona Abilita binding di reindirizzamento per supportare binding SAML che utilizzano reindirizzamenti.
1. (Facoltativo) In Proprietà personalizzate, specifica proprietà aggiuntive. Le proprietà aggiuntive sono coppie nome=valore separate da nuove righe.

   * È possibile configurare i moduli AEM per rilasciare un’asserzione SAML per un periodo di validità corrispondente al periodo di validità di un’asserzione di terze parti. Per rispettare il timeout dell’asserzione SAML di terze parti, aggiungi la seguente riga in Proprietà personalizzate:

     `saml.sp.honour.idp.assertion.expiry=true`

   * Aggiungi la seguente proprietà personalizzata per l’utilizzo di RelayState per determinare l’URL a cui verrà reindirizzato l’utente dopo la corretta autenticazione.

     `saml.sp.use.relaystate=true`

   * Aggiungi la seguente proprietà personalizzata per configurare l’URL per le JSP (Java Server Pages) personalizzate, utilizzate per il rendering dell’elenco registrato dei provider di identità. Se non hai distribuito un’applicazione web personalizzata, per eseguire il rendering dell’elenco verrà utilizzata la pagina Gestione utente predefinita.

   `saml.sp.discovery.url=/custom/custom.jsp`

1. Fai clic su Salva.
