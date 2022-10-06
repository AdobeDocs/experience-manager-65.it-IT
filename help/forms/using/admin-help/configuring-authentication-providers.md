---
title: Configurazione dei provider di autenticazione
seo-title: Configuring authentication providers
description: Aggiungi, modifica o elimina fornitori di autenticazione, modifica le impostazioni di autenticazione e leggi sul provisioning in tempo reale degli utenti.
seo-description: Add, edit, or delete authentication providers, change authentication settings, and read about just-in-time provisioning of users.
uuid: 90e7690b-1ce0-4604-b58f-6dca4f2372cf
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 31dd8db3-ddac-429e-82f8-8c5dc4ffc186
exl-id: d72a3977-1423-49e0-899b-234bb76be378
source-git-commit: 1cdd15800548362ccdd9e70847d9df8ce93ee06e
workflow-type: tm+mt
source-wordcount: '1576'
ht-degree: 0%

---

# Configurazione dei provider di autenticazione {#configuring-authentication-providers}

I domini ibridi richiedono almeno un provider di autenticazione e i domini aziendali richiedono almeno un provider di autenticazione o di directory.

Se si abilita SSO utilizzando SPNEGO, aggiungere un provider di autenticazione Kerberos con SPNEGO abilitato e un provider LDAP come backup. Questa configurazione abilita l&#39;autenticazione utente con un ID utente e una password se SPNEGO non funziona. (Vedi [Abilitare SSO con SPNEGO](/help/forms/using/admin-help/enabling-single-sign-on-aem.md#enable-sso-using-spnego).)

## Aggiungi un provider di autenticazione {#add-an-authentication-provider}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione dominio.
1. Fai clic su un dominio esistente nell’elenco. Se stai aggiungendo l’autenticazione per un nuovo dominio, consulta [Aggiungi un dominio enterprise](/help/forms/using/admin-help/adding-domains.md#add-an-enterprise-domain) o [Aggiungi un dominio ibrido](/help/forms/using/admin-help/adding-domains.md#add-a-hybrid-domain).
1. Fare clic su Aggiungi autenticazione e, nell&#39;elenco Provider di autenticazione, selezionare un provider, a seconda del meccanismo di autenticazione utilizzato dall&#39;organizzazione.
1. Fornisci eventuali informazioni aggiuntive richieste sulla pagina. (Vedi [Impostazioni di autenticazione](configuring-authentication-providers.md#authentication-settings).)
1. (Facoltativo) Fai clic su Prova per testare la configurazione.
1. Fare clic su OK, quindi di nuovo su OK.

## Modificare un provider di autenticazione esistente {#edit-an-existing-authentication-provider}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione dominio.
1. Fai clic sul dominio appropriato nell’elenco.
1. Nella pagina visualizzata, seleziona il provider di autenticazione appropriato dall’elenco e apporta le modifiche necessarie. (Vedi [Impostazioni di autenticazione](configuring-authentication-providers.md#authentication-settings).)
1. Fai clic su OK.

## Eliminare un provider di autenticazione {#delete-an-authentication-provider}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione dominio.
1. Fai clic sul dominio appropriato nell’elenco.
1. Selezionare le caselle di controllo per i provider di autenticazione da eliminare e fare clic su Elimina.
1. Fare clic su OK nella pagina di conferma visualizzata e fare di nuovo clic su OK.

## Impostazioni di autenticazione {#authentication-settings}

Sono disponibili le seguenti impostazioni, a seconda del tipo di dominio e del tipo di autenticazione scelto.

### Impostazioni LDAP {#ldap-settings}

Se si configura l&#39;autenticazione per un dominio enterprise o ibrido e si seleziona l&#39;autenticazione LDAP, è possibile scegliere di utilizzare il server LDAP specificato nella configurazione della directory oppure scegliere un altro server LDAP da utilizzare per l&#39;autenticazione. Se scegli un server diverso, gli utenti devono esistere su entrambi i server LDAP.

Per utilizzare il server LDAP specificato nella configurazione della directory, selezionare LDAP come provider di autenticazione e fare clic su OK.

Per utilizzare un server LDAP diverso per eseguire l&#39;autenticazione, selezionare LDAP come provider di autenticazione e selezionare la casella di controllo Autenticazione LDAP personalizzata. Vengono visualizzate le seguenti impostazioni di configurazione.

**Server:** (Obbligatorio) Nome di dominio completo (FQDN) del server delle directory. Ad esempio, per un computer chiamato x sulla rete example.com, l&#39;FQDN è x.example.com. Un indirizzo IP può essere utilizzato al posto del nome del server FQDN.

**Porta:** (Obbligatorio) La porta utilizzata dal server delle directory. In genere 389 o 636 se il protocollo SSL (Secure Sockets Layer) viene utilizzato per l&#39;invio di informazioni di autenticazione sulla rete.

**SSL:** (Obbligatorio) Specifica se il server di directory utilizza SSL quando invia dati sulla rete. Il valore predefinito è No. Se è impostato su Sì, il certificato del server LDAP corrispondente deve essere considerato attendibile dall&#39;ambiente di runtime Java™ (JRE) del server dell&#39;applicazione.

**Binding** (Obbligatorio) Specifica come accedere alla directory.

**Anonimo:** Non è richiesto alcun nome utente o password.

**Utente:** L&#39;autenticazione è obbligatoria. Nella casella Nome specificare il nome del record utente che può accedere alla directory. È consigliabile inserire il nome distinto completo (DN) dell’account utente, ad esempio cn=Jane Doe, ou=user, dc=can, dc=com. Nella casella Password specificare la password associata. Queste impostazioni sono necessarie quando si seleziona Utente come opzione Binding.

**Recupera DN di base:** (Non obbligatorio) Recupera i DN di base e li visualizza nell’elenco a discesa. Questa impostazione è utile quando disponi di più DN di base e devi selezionare un valore.

**DN di base:** (Obbligatorio) Utilizzato come punto iniziale per la sincronizzazione di utenti e gruppi dalla gerarchia LDAP. È consigliabile specificare un DN di base al livello più basso della gerarchia che includa tutti gli utenti e i gruppi che devono essere sincronizzati per i servizi. Non includere il DN dell’utente in questa impostazione. Per sincronizzare un particolare utente, utilizza l’impostazione Filtro di ricerca .

**Popolare la pagina con:** (Non obbligatorio) Quando è selezionata, compila gli attributi nelle pagine delle impostazioni Utente e Gruppo con i corrispondenti valori LDAP predefiniti.

**Filtro di ricerca:** (Obbligatorio) Il filtro di ricerca da utilizzare per trovare il record associato all&#39;utente. Consulta la sezione sulla sintassi del filtro di ricerca.

### Impostazioni Kerberos {#kerberos-settings}

Se si configura l&#39;autenticazione per un dominio enterprise o ibrido e si seleziona l&#39;autenticazione Kerberos, sono disponibili le seguenti impostazioni.

**IP DNS:** Indirizzo IP DNS del server in cui sono in esecuzione i moduli AEM. In Windows, è possibile determinare questo indirizzo IP eseguendo ipconfig /all alla riga di comando.

**Host KDC:** Nome host completo o indirizzo IP del server Active Directory utilizzato per l&#39;autenticazione.

**Utente del servizio:** Se si utilizza Active Directory 2003, questo valore corrisponde al mapping creato per l&#39;entità servizio nel modulo `HTTP/<server name>`. Se si utilizza Active Directory 2008, questo valore corrisponde all&#39;ID di accesso dell&#39;entità del servizio. Ad esempio, si supponga che l’entità servizio sia denominata um spnego, che l’ID utente sia sptrading demo e che la mappatura sia HTTP/example.yourcompany.com. Con Active Directory 2003, è possibile impostare l&#39;utente del servizio su HTTP/example.yourcompany.com. Con Active Directory 2008, è possibile impostare l&#39;utente del servizio su sptrading demo. (Consultare Abilitare SSO utilizzando SPNEGO.)

**Realm di servizio:** Nome di dominio per Active Directory

**Password servizio:** Password utente del servizio

**Abilita SPNEGO:** Abilita l&#39;utilizzo di SPNEGO per il single sign-on (SSO). (Consultare Abilitare SSO utilizzando SPNEGO.)

### Impostazioni SAML {#saml-settings}

Se si configura l&#39;autenticazione per un dominio enterprise o ibrido e si seleziona l&#39;autenticazione SAML, sono disponibili le seguenti impostazioni. Per informazioni sulle impostazioni SAML aggiuntive, vedi [Configurare le impostazioni del provider di servizi SAML](/help/forms/using/admin-help/configure-saml-service-provider-settings.md#configure-saml-service-provider-settings).

**Selezionare un file metadati provider di identità SAML da importare:** Fai clic su Sfoglia per selezionare un file di metadati del provider di identità SAML generato dall&#39;IDP, quindi fai clic su Importa. Vengono visualizzati i dettagli dell’IDP.

**Titolo:** Alias dell&#39;URL indicato da EntityID. Il titolo viene inoltre visualizzato nella pagina di accesso per gli utenti aziendali e locali.

**Il Provider Di Identità Supporta L&#39;Autenticazione Di Base Del Client:** L&#39;autenticazione di base del client viene utilizzata quando l&#39;IDP utilizza un profilo di risoluzione dell&#39;artefatto SAML. In questo profilo, User Management si connette a un servizio Web in esecuzione all&#39;IDP per recuperare l&#39;asserzione SAML effettiva. L&#39;IDP potrebbe richiedere l&#39;autenticazione. Se l’IDP richiede l’autenticazione, seleziona questa opzione e specifica un nome utente e una password nelle caselle fornite.

**Proprietà personalizzate:** Consente di specificare proprietà aggiuntive. Le proprietà aggiuntive sono coppie nome=valore separate da nuove righe.

Se si utilizza il binding degli artefatti, sono necessarie le seguenti proprietà personalizzate.

* Aggiungi la seguente proprietà personalizzata per specificare un nome utente che rappresenta il provider di servizi AEM forms, che verrà utilizzato per l’autenticazione al servizio IDP di risoluzione degli artefatti.
   `saml.idp.resolve.username=<username>`

* Aggiungi la seguente proprietà personalizzata per specificare la password per l&#39;utente specificato in `saml.idp.resolve.username`.
   `saml.idp.resolve.password=<password>`

* Aggiungi la seguente proprietà personalizzata per consentire al provider di servizi di ignorare la convalida del certificato durante la determinazione della connessione con il servizio di risoluzione degli artefatti su SSL.
   `saml.idp.resolve.ignorecert=true`

### Impostazioni personalizzate {#custom-settings}

Se si configura l&#39;autenticazione per un dominio enterprise o ibrido e si seleziona Autenticazione personalizzata, selezionare il nome del provider di autenticazione personalizzato.

## Provisioning in tempo reale degli utenti {#just-in-time-provisioning-of-users}

Il provisioning in tempo reale crea automaticamente un utente nel database User Management dopo che l&#39;utente è stato autenticato correttamente tramite un provider di autenticazione. Anche i ruoli e i gruppi rilevanti vengono assegnati in modo dinamico al nuovo utente. Puoi abilitare il provisioning in tempo per i domini enterprise e ibridi.

Questa procedura descrive il funzionamento dell’autenticazione tradizionale nei moduli AEM:

1. Quando un utente tenta di accedere AEM moduli, Gestione utente trasmette le credenziali in sequenza a tutti i provider di autenticazione disponibili. (Le credenziali di accesso includono combinazione nome utente/password, ticket Kerberos, firma PKCS7 e così via.)
1. Il provider di autenticazione convalida le credenziali.
1. Il provider di autenticazione controlla quindi se l&#39;utente esiste nel database User Management. Sono possibili i seguenti stati:

   **Esiste** Se l&#39;utente è corrente e sbloccato, Gestione utente restituisce l&#39;autenticazione riuscita. Tuttavia, se l&#39;utente non è corrente o è bloccato, Gestione utente restituisce un errore di autenticazione.

   **Non esiste** Gestione utente restituisce un errore di autenticazione.

   **Non valido** Gestione utente restituisce un errore di autenticazione.

1. Viene valutato il risultato restituito dal provider di autenticazione. Se il provider di autenticazione ha restituito l&#39;autenticazione, l&#39;utente può effettuare l&#39;accesso. In caso contrario, User Management controlla con il provider di autenticazione successivo (passaggi 2-3).
1. Se le credenziali utente non vengono convalidate da alcun provider di autenticazione disponibile, viene restituito un errore di autenticazione.

Quando il provisioning in tempo reale è abilitato, i nuovi utenti vengono creati in modo dinamico in Gestione utente se uno dei provider di autenticazione convalida le proprie credenziali. (Dopo la fase 3 della procedura precedente.)

Senza il provisioning in tempo reale, quando un utente viene autenticato correttamente ma non viene trovato nel database di Gestione utente, l&#39;autenticazione non riesce. Il provisioning in tempo reale aggiunge un passaggio nella procedura di autenticazione per creare l’utente e assegnare ruoli e gruppi all’utente.

### Abilitare il provisioning just-in-time per un dominio {#enable-just-in-time-provisioning-for-a-domain}

1. Scrivere un contenitore di servizi che implementa le interfacce IdentityCreator e AssignmentProvider. (Vedi [Programmazione con moduli AEM](https://www.adobe.com/go/learn_aemforms_programming_63).)
1. Distribuire il contenitore di servizio al server dei moduli.
1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione dominio.

   Selezionare un dominio esistente o fare clic su Nuovo dominio organizzazione.

1. Per creare un dominio, fare clic su Nuovo dominio Enterprise o Nuovo dominio ibrido. Per modificare un dominio esistente, fai clic sul nome del dominio.
1. Selezionare Abilita solo in provisioning tempo.

   ***nota **: Se la casella di controllo Abilita provisioning in tempo è mancante, fare clic su Home > Impostazioni > Gestione utente > Configurazione > Attributi di sistema avanzati, quindi fare clic su Ricarica.*

1. Aggiungi provider di autenticazione. Durante l’aggiunta di provider di autenticazione, nella schermata Nuova autenticazione , seleziona un creatore di identità registrato e un fornitore di assegnazione. (Vedi [Configurazione dei provider di autenticazione](configuring-authentication-providers.md#configuring-authentication-providers).)
1. Salva il dominio.
