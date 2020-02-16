---
title: Configurazione dei provider di autenticazione
seo-title: Configurazione dei provider di autenticazione
description: Aggiungete, modificate o eliminate i provider di autenticazione, modificate le impostazioni di autenticazione e leggete il provisioning "just-in-time" degli utenti.
seo-description: Aggiungete, modificate o eliminate i provider di autenticazione, modificate le impostazioni di autenticazione e leggete il provisioning "just-in-time" degli utenti.
uuid: 90e7690b-1ce0-4604-b58f-6dca4f2372cf
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 31dd8db3-ddac-429e-82f8-8c5dc4ffc186
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configurazione dei provider di autenticazione {#configuring-authentication-providers}

I domini ibridi richiedono almeno un provider di autenticazione e i domini enterprise richiedono almeno un provider di autenticazione o un provider di directory.

Se si abilita SSO utilizzando SPNEGO, aggiungere un provider di autenticazione Kerberos con SPNEGO abilitato e un provider LDAP come backup. Questa configurazione abilita l&#39;autenticazione utente con un ID utente e una password se SPNEGO non funziona. Consultate [Abilitare SSO con SPNEGO](/help/forms/using/admin-help/enabling-single-sign-on-aem.md#enable-sso-using-spnego).

## Aggiunta di un provider di autenticazione {#add-an-authentication-provider}

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Gestione dominio.
1. Fare clic su un dominio esistente nell&#39;elenco. Se state aggiungendo l&#39;autenticazione per un nuovo dominio, consultate [Aggiungere un dominio](/help/forms/using/admin-help/adding-domains.md#add-an-enterprise-domain) Enterprise o [Aggiungere un dominio](/help/forms/using/admin-help/adding-domains.md#add-a-hybrid-domain)ibrido.
1. Fate clic su Aggiungi autenticazione e, nell&#39;elenco Provider autenticazione, selezionate un provider, a seconda del meccanismo di autenticazione utilizzato dall&#39;organizzazione.
1. Fornite eventuali informazioni aggiuntive richieste sulla pagina. Consultate Impostazioni [](configuring-authentication-providers.md#authentication-settings)di autenticazione.
1. (Facoltativo) Fate clic su Test per verificare la configurazione.
1. Fate clic su OK, quindi di nuovo su OK.

## Modificare un provider di autenticazione esistente {#edit-an-existing-authentication-provider}

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Gestione dominio.
1. Fare clic sul dominio appropriato nell&#39;elenco.
1. Nella pagina visualizzata, selezionate il provider di autenticazione appropriato dall&#39;elenco e apportate le modifiche necessarie. Consultate Impostazioni [](configuring-authentication-providers.md#authentication-settings)di autenticazione.
1. Fate clic su OK.

## Eliminazione di un provider di autenticazione {#delete-an-authentication-provider}

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Gestione dominio.
1. Fare clic sul dominio appropriato nell&#39;elenco.
1. Selezionate le caselle di controllo per i provider di autenticazione da eliminare e fate clic su Elimina.
1. Fare clic su OK nella pagina di conferma visualizzata e fare di nuovo clic su OK.

## Authentication settings {#authentication-settings}

Sono disponibili le seguenti impostazioni, a seconda del tipo di dominio e del tipo di autenticazione scelto.

### Impostazioni LDAP {#ldap-settings}

Se state configurando l’autenticazione per un dominio Enterprise o ibrido e selezionate l’autenticazione LDAP, potete scegliere di utilizzare il server LDAP specificato nella configurazione di directory oppure potete scegliere un altro server LDAP da usare per l’autenticazione. Se scegliete un server diverso, gli utenti devono esistere su entrambi i server LDAP.

Per utilizzare il server LDAP specificato nella configurazione della directory, selezionate LDAP come provider di autenticazione e fate clic su OK.

Per utilizzare un altro server LDAP per eseguire l’autenticazione, selezionate LDAP come provider di autenticazione e selezionate la casella di controllo Autenticazione LDAP personalizzata. Vengono visualizzate le seguenti impostazioni di configurazione.

**** Server: (Obbligatorio) Nome di dominio completo (FQDN) del server di directory. Ad esempio, per un computer chiamato x sulla rete corp.example.com, l&#39;FQDN è x.corp.example.com. Un indirizzo IP può essere usato al posto del nome del server FQDN.

**** Porta: (Obbligatorio) La porta utilizzata dal server di directory. In genere 389 o 636 se il protocollo SSL (Secure Sockets Layer) è utilizzato per inviare informazioni di autenticazione attraverso la rete.

**** SSL: (Obbligatorio) Specifica se il server di directory utilizza SSL quando invia dati sulla rete. Il valore predefinito è No. Se si imposta su Sì, il certificato del server LDAP corrispondente deve essere considerato affidabile dall&#39;ambiente runtime Java™ (JRE) del server applicazione.

**Binding** (obbligatorio) Specifica come accedere alla directory.

**** Anonimo: Non è richiesto alcun nome utente o password.

**** Utente: L&#39;autenticazione è obbligatoria. Nella casella Nome, specificare il nome del record utente che può accedere alla directory. È consigliabile immettere il nome distinto completo (DN) dell&#39;account utente, ad esempio cn=Jane Doe, ou=user, dc=can, dc=com. Nella casella Password, specificare la password associata. Queste impostazioni sono necessarie quando si seleziona Utente come opzione di binding.

**** Recupera DN di base: (Non obbligatorio) Recupera i DN di base e li visualizza nell&#39;elenco a discesa. Questa impostazione è utile quando hai più DN base e devi selezionare un valore.

**** DN di base: (Obbligatorio) Utilizzato come punto di partenza per la sincronizzazione di utenti e gruppi dalla gerarchia LDAP. È consigliabile specificare un DN di base al livello più basso della gerarchia che includa tutti gli utenti e i gruppi che devono essere sincronizzati per i servizi. Non includete il DN dell&#39;utente in questa impostazione. Per sincronizzare un particolare utente, usate l’impostazione Filtro ricerca.

**** Compila la pagina con: (Non obbligatorio) Se questa opzione è selezionata, compila gli attributi nelle pagine delle impostazioni Utente e Gruppo con i corrispondenti valori LDAP predefiniti.

**** Filtro di ricerca: (Obbligatorio) Il filtro di ricerca da utilizzare per trovare il record associato all&#39;utente. Consulta Cerca sintassi filtro.

### Impostazioni Kerberos {#kerberos-settings}

Se si sta configurando l&#39;autenticazione per un dominio Enterprise o ibrido e si seleziona l&#39;autenticazione Kerberos, sono disponibili le seguenti impostazioni.

**** IP DNS: L&#39;indirizzo IP DNS del server in cui sono in esecuzione i moduli AEM. In Windows, potete determinare questo indirizzo IP eseguendo ipconfig /all alla riga di comando.

**** Host KDC: Nome host completo o indirizzo IP del server Active Directory utilizzato per l&#39;autenticazione.

**** Utente del servizio: Se si utilizza Active Directory 2003, questo valore corrisponde al mapping creato per l&#39;entità del servizio nel modulo `HTTP/<server name>`. Se si utilizza Active Directory 2008, questo valore è l&#39;ID di accesso dell&#39;entità del servizio. Ad esempio, si supponga che l&#39;entità del servizio sia denominata um spnego, che l&#39;ID utente sia spnegozidemo e che la mappatura sia HTTP/example.corp.yourcompany.com. Con Active Directory 2003, impostate Utente servizio su HTTP/example.corp.nomeazienda.com. Con Active Directory 2008, l&#39;utente del servizio è impostato su sptrading demo. Consultate Abilitare SSO con SPNEGO.

**** Service Realm: Nome di dominio per Active Directory

**** Password del servizio: Password utente del servizio

**** Abilita SPNEGO: Abilita l&#39;utilizzo di SPNEGO per Single Sign-On (SSO). Consultate Abilitare SSO con SPNEGO.

### Impostazioni SAML {#saml-settings}

Se state configurando l&#39;autenticazione per un dominio Enterprise o ibrido e selezionate l&#39;autenticazione SAML, sono disponibili le seguenti impostazioni. Per informazioni su ulteriori impostazioni SAML, consulta [Configurare le impostazioni](/help/forms/using/admin-help/configure-saml-service-provider-settings.md#configure-saml-service-provider-settings)del provider di servizi SAML.

**** Selezionare un file metadati provider di identità SAML da importare: Fate clic su Sfoglia per selezionare un file di metadati del provider di identità SAML generato dall&#39;IDP, quindi fate clic su Importa. Vengono visualizzati i dettagli dell&#39;IDP.

**** Titolo: Alias all’URL indicato da EntityID. Il titolo viene visualizzato anche nella pagina di accesso per gli utenti Enterprise e Locali.

**** Il Provider Di Identità Supporta L&#39;Autenticazione Client Basic: L&#39;autenticazione di base client viene utilizzata quando l&#39;IDP utilizza un profilo SAML per la risoluzione degli artefatti. In questo profilo, User Management si connette a un servizio Web in esecuzione nell&#39;IDP per recuperare l&#39;asserzione SAML effettiva. L&#39;IDP potrebbe richiedere l&#39;autenticazione. Se l&#39;IDP richiede l&#39;autenticazione, selezionare questa opzione e specificare un nome utente e una password nelle caselle fornite.

**** Proprietà personalizzate: Consente di specificare proprietà aggiuntive. Le proprietà aggiuntive sono coppie nome=valore separate da nuove righe.

Se si utilizza il binding degli artifact, sono necessarie le seguenti proprietà personalizzate.

* Aggiungete la seguente proprietà personalizzata per specificare un nome utente che rappresenta il provider di servizi AEM Form, che verrà utilizzato per l&#39;autenticazione al servizio di risoluzione degli artefatti IDP.
   `saml.idp.resolve.username=<username>`

* Aggiungete la seguente proprietà personalizzata per specificare la password per l&#39;utente specificato in `saml.idp.resolve.username`.
   `saml.idp.resolve.password=<password>`

* Aggiungete la seguente proprietà personalizzata per consentire al provider di servizi di ignorare la convalida del certificato durante la definizione della connessione con il servizio di risoluzione degli artefatti tramite SSL.
   `saml.idp.resolve.ignorecert=true`

### Custom settings {#custom-settings}

Se state configurando l&#39;autenticazione per un dominio Enterprise o ibrido e selezionate Autenticazione personalizzata, selezionate il nome del provider di autenticazione personalizzato.

## Provisioning in tempo reale degli utenti {#just-in-time-provisioning-of-users}

Il provisioning in tempo reale crea automaticamente un utente nel database Gestione utente dopo che l&#39;utente è stato autenticato tramite un provider di autenticazione. Anche i ruoli e i gruppi pertinenti vengono assegnati in modo dinamico al nuovo utente. Potete abilitare il provisioning &quot;just-in-time&quot; per i domini Enterprise e ibridi.

Questa procedura descrive il funzionamento dell&#39;autenticazione tradizionale nei moduli AEM:

1. Quando un utente tenta di accedere ai moduli AEM, Gestione utente passa le proprie credenziali in sequenza a tutti i provider di autenticazione disponibili. (Le credenziali di login includono la combinazione nome utente/password, il ticket Kerberos, la firma PKCS7 e così via).
1. Il provider di autenticazione convalida le credenziali.
1. Il provider di autenticazione verifica quindi se l&#39;utente esiste nel database Gestione utente. Sono possibili i seguenti stati:

   **Esiste** Se l&#39;utente è corrente e sbloccato, Gestione utente restituisce il successo dell&#39;autenticazione. Tuttavia, se l&#39;utente non è corrente o è bloccato, Gestione utente restituisce un errore di autenticazione.

   **Non esiste** Gestione utente restituisce un errore di autenticazione.

   **Gestione utente non valida** restituisce un errore di autenticazione.

1. Il risultato restituito dal provider di autenticazione viene valutato. Se il provider di autenticazione ha restituito un esito positivo, l&#39;utente può effettuare l&#39;accesso. In caso contrario, Gestione utente verifica con il provider di autenticazione successivo (passaggi da 2 a 3).
1. L&#39;errore di autenticazione viene restituito se nessun provider di autenticazione disponibile convalida le credenziali utente.

Quando il provisioning &quot;in-time&quot; è abilitato, i nuovi utenti vengono creati dinamicamente in Gestione utente se uno dei provider di autenticazione convalida le proprie credenziali. (Dopo la fase 3 della procedura precedente).

Senza il provisioning &quot;in-time&quot;, quando un utente viene autenticato correttamente ma non viene trovato nel database di Gestione utente, l&#39;autenticazione non riesce. Il provisioning in tempo reale aggiunge un passaggio alla procedura di autenticazione per creare l&#39;utente e assegnare ruoli e gruppi all&#39;utente.

### Abilitare il provisioning just-in-time per un dominio {#enable-just-in-time-provisioning-for-a-domain}

1. Scrivete un contenitore di servizi che implementa le interfacce IdentityCreator e AssignmentProvider. (Vedere [Programmazione con i moduli](https://www.adobe.com/go/learn_aemforms_programming_63)AEM.)
1. Distribuire il contenitore del servizio al server dei moduli.
1. Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Gestione dominio.

   Selezionate un dominio esistente o fate clic su Nuovo dominio Enterprise.

1. Per creare un dominio, fare clic su Nuovo dominio Enterprise o Nuovo dominio ibrido. Per modificare un dominio esistente, fate clic sul nome del dominio.
1. Selezionate Abilita solo in provisioning tempo.

   ***nota **: Se la casella di controllo Abilita solo in provisioning temporale non è presente, fate clic su Home > Impostazioni > Gestione utente > Configurazione > Attributi di sistema avanzati, quindi fate clic su Ricarica.*

1. Aggiunta di provider di autenticazione. Durante l&#39;aggiunta di provider di autenticazione, nella schermata Nuova autenticazione, selezionate un creatore di identità registrato e un provider di assegnazione. Consultate [Configurazione dei provider](configuring-authentication-providers.md#configuring-authentication-providers)di autenticazione.
1. Salva il dominio.

