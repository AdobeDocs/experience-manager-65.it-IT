---
title: Configurare le impostazioni del provider di servizi SAML
description: Puoi configurare le impostazioni del provider di servizi SAML per consentire agli utenti di accedere e autenticarsi in AEM Forms tramite un provider di identità (IDP) di terze parti specificato.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: dd302cfb-eae1-4189-aa7b-9f2533ebd164
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '607'
ht-degree: 100%

---

# Configurare le impostazioni del provider di servizi SAML{#configure-saml-service-provider-settings}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Il linguaggio SAML (Security Assertion Markup Language) è una delle opzioni che puoi selezionare durante la configurazione dell’autorizzazione per un dominio enterprise o ibrido. SAML viene utilizzato principalmente per supportare SSO tra più domini. Quando SAML è configurato come provider di autenticazione, gli utenti accedono e si autenticano in AEM Forms tramite un provider di identità (IDP) di terze parti specificato.

Per una spiegazione di SAML, consulta [Panoramica tecnica di SAML (Security Assertion Markup Language) V2.0](https://docs.oasis-open.org/security/saml/Post2.0/sstc-saml-tech-overview-2.0.html).

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Configurazione > Impostazioni del provider di servizi SAML.
1. Nella casella ID entità del provider di servizi digitare un ID univoco da utilizzare come identificatore per l’implementazione del provider di servizi AEM forms. Puoi specificare questo ID univoco anche durante la configurazione dell’IDP (ad esempio, `um.lc.com`). Puoi inoltre utilizzare l’URL che viene usato per accedere a AEM Forms (ad esempio, `https://AEMformsserver`).
1. Nella casella URL di base provider di servizi digita l’URL di base per il server Forms, ad esempio `https://AEMformsserver:8080`.
1. (Facoltativo) Per consentire ad AEM Forms di inviare richieste di autenticazione firmate all’IDP, procedi come segue:

   * Utilizza Gestore affidabilità per importare una credenziale in formato PKCS #12 con l’opzione Credenziale per la firma di documenti selezionata per Tipo di archivio fonti attendibili. Consulta [Gestire le credenziali locali](/help/forms/using/admin-help/local-credentials.md#managing-local-credentials).
   * Nell’elenco Alias chiave della credenziale del provider di servizi seleziona l’alias assegnato alla credenziale nell’archivio fonti attendibili.
   * Fai clic su Esporta per salvare il contenuto dell’URL in un file e quindi importa il file nell’IDP.

1. (Facoltativo) Nell’elenco Criterio per l’ID del nome del provider di servizi seleziona il formato del nome utilizzato dall’IDP per identificare l’utente in un’asserzione SAML. Le opzioni disponibili sono Non specificato, E-mail e Nome qualificato del dominio Windows.

   >[!NOTE]
   >
   >I formati dei nomi non fanno distinzione tra maiuscole e minuscole.

1. (Facoltativo) Seleziona Abilita il prompt di autenticazione per gli utenti locali. Quando questa opzione è selezionata, gli utenti visualizzano due collegamenti:

   * un collegamento alla pagina di accesso del provider di identità SAML di terze parti, in cui gli utenti che appartengono a un dominio Enterprise possono eseguire l’autenticazione.
   * un collegamento alla pagina di accesso di AEM Forms, in cui gli utenti che appartengono a un dominio locale possono eseguire l’autenticazione.

   Se questa opzione non è selezionata, gli utenti vengono indirizzati direttamente alla pagina di accesso del provider di identità SAML di terze parti, in cui gli utenti che appartengono a un dominio Enterprise possono eseguire l’autenticazione.

1. (Facoltativo) Seleziona Abilita binding degli artefatti per abilitare il supporto del binding degli artefatti. Per impostazione predefinita, con SAML viene utilizzata l’associazione POST. Se tuttavia hai configurato l’associazione degli artefatti, seleziona questa opzione. Quando questa opzione è selezionata, l’asserzione utente effettiva non viene passata alla richiesta Browser. Viene invece passato un puntatore all’asserzione e l’asserzione viene recuperata utilizzando una chiamata di servizio web back-end.
1. (Facoltativo) Seleziona Abilita binding di reindirizzamento per supportare i binding SAML che utilizzano il reindirizzamento.
1. (Facoltativo) In Proprietà personalizzate, specifica le proprietà aggiuntive. Le proprietà aggiuntive sono coppie nome=valore separate da nuove righe.

   * Puoi configurare AEM Forms in modo che produca un’asserzione SAML per un periodo di validità corrispondente al periodo di validità di un’asserzione di terze parti. Per rispettare il timeout dell’asserzione SAML di terze parti, aggiungi la seguente riga in Proprietà personalizzate:

     `saml.sp.honour.idp.assertion.expiry=true`

   * Aggiungi la seguente proprietà personalizzata per l’utilizzo di RelayState per determinare l’URL a cui verrà reindirizzato l’utente dopo la riuscita dell’autenticazione.

     `saml.sp.use.relaystate=true`

   * Aggiungi la seguente proprietà personalizzata per poter configurare l’URL per le JSP (Java™ Server Pages) personalizzate, utilizzate per il rendering dell’elenco registrato di provider di identità. Se non è stata distribuita un’applicazione web personalizzata, per il rendering dell’elenco verrà utilizzata la pagina Gestione utente predefinita.

   `saml.sp.discovery.url=/custom/custom.jsp`

1. Fai clic su Salva.
