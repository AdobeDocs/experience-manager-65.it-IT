---
title: Configurazione dei provider di autenticazione
description: Aggiungere, modificare o eliminare provider di autenticazione, modificare le impostazioni di autenticazione e leggere informazioni sul provisioning just-in-time degli utenti.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: d72a3977-1423-49e0-899b-234bb76be378
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '1592'
ht-degree: 0%

---

# Configurazione dei provider di autenticazione {#configuring-authentication-providers}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

I domini ibridi richiedono almeno un provider di autenticazione, mentre i domini enterprise richiedono almeno un provider di autenticazione o un provider di directory.

Se si abilita SSO utilizzando SPNEGO, aggiungere un provider di autenticazione Kerberos con SPNEGO abilitato e un provider LDAP come backup. Questa configurazione abilita l&#39;autenticazione utente con un ID utente e una password se SPNEGO non funziona. (Vedi [Abilitare l&#39;SSO tramite SPNEGO](/help/forms/using/admin-help/enabling-single-sign-on-aem.md#enable-sso-using-spnego).)

## Aggiungere un provider di autenticazione {#add-an-authentication-provider}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione dominio.
1. Selezionare un dominio esistente nell&#39;elenco. Se stai aggiungendo l&#39;autenticazione per un nuovo dominio, vedi [Aggiungere un dominio enterprise](/help/forms/using/admin-help/adding-domains.md#add-an-enterprise-domain) o [Aggiungere un dominio ibrido](/help/forms/using/admin-help/adding-domains.md#add-a-hybrid-domain).
1. Fare clic su Aggiungi autenticazione e, nell&#39;elenco Provider di autenticazione, selezionare un provider, a seconda del meccanismo di autenticazione utilizzato dall&#39;organizzazione.
1. Fornisci eventuali informazioni aggiuntive richieste sulla pagina. (Vedi [Impostazioni di autenticazione](configuring-authentication-providers.md#authentication-settings).)
1. (Facoltativo) Fai clic su Prova per verificare la configurazione.
1. Fare clic su OK e quindi di nuovo su OK.

## Modifica un provider di autenticazione esistente {#edit-an-existing-authentication-provider}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione dominio.
1. Fare clic sul dominio appropriato nell&#39;elenco.
1. Nella pagina visualizzata, seleziona il provider di autenticazione appropriato dall’elenco e apporta le modifiche necessarie. (Vedi [Impostazioni di autenticazione](configuring-authentication-providers.md#authentication-settings).)
1. Fare clic su OK.

## Eliminare un provider di autenticazione {#delete-an-authentication-provider}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione dominio.
1. Fare clic sul dominio appropriato nell&#39;elenco.
1. Selezionare le caselle di controllo relative ai provider di autenticazione da eliminare e fare clic su Elimina.
1. Fare clic su OK nella pagina di conferma visualizzata e fare di nuovo clic su OK.

## Impostazioni di autenticazione {#authentication-settings}

Sono disponibili le seguenti impostazioni, a seconda del tipo di dominio e del tipo di autenticazione scelti.

### Impostazioni LDAP {#ldap-settings}

Se si sta configurando l&#39;autenticazione per un dominio enterprise o ibrido e si seleziona l&#39;autenticazione LDAP, è possibile scegliere di utilizzare il server LDAP specificato nella configurazione della directory oppure scegliere un server LDAP diverso da utilizzare per l&#39;autenticazione. Se si sceglie un server diverso, gli utenti devono esistere in entrambi i server LDAP.

Per utilizzare il server LDAP specificato nella configurazione della directory, selezionare LDAP come provider di autenticazione e fare clic su OK.

Per utilizzare un server LDAP diverso per eseguire l&#39;autenticazione, selezionare LDAP come provider di autenticazione e selezionare la casella di controllo Autenticazione LDAP personalizzata. Vengono visualizzate le seguenti impostazioni di configurazione.

**Server:** (obbligatorio) Nome di dominio completo (FQDN) del server delle directory. Ad esempio, per un computer denominato x nella rete example.com, il nome di dominio completo è x.example.com. È possibile utilizzare un indirizzo IP al posto del nome del server FQDN.

**Porta:** (obbligatoria) Porta utilizzata dal server delle directory. In genere, 389 o 636 se il protocollo SSL (Secure Sockets Layer) viene utilizzato per l&#39;invio di informazioni di autenticazione sulla rete.

**SSL:** (obbligatorio) Specifica se il server delle directory utilizza SSL per l&#39;invio di dati in rete. Il valore predefinito è No. Se impostato su Sì, il certificato del server LDAP corrispondente deve essere considerato attendibile dall&#39;ambiente runtime Java™ (JRE) del server applicazioni.

**Binding** (obbligatorio) Specifica come accedere alla directory.

**Anonimo:** Non è richiesto alcun nome utente o password.

**Utente:** autenticazione richiesta. Nella casella Nome specificare il nome del record utente che può accedere alla directory. È consigliabile immettere il nome distinto completo (DN) dell&#39;account utente, ad esempio cn=Jane Doe, ou=user, dc=can, dc=com. Nella casella Password specificare la password associata. Queste impostazioni sono necessarie quando si seleziona Utente come opzione di binding.

**Recupera DN di base:** (non obbligatorio) Recupera i DN di base e li visualizza nell&#39;elenco a discesa. Questa impostazione è utile quando si dispone di più DN di base e si deve selezionare un valore.

**DN di base:** (obbligatorio) Utilizzato come punto iniziale per la sincronizzazione di utenti e gruppi dalla gerarchia LDAP. È consigliabile specificare un DN di base al livello più basso della gerarchia che includa tutti gli utenti e i gruppi che devono essere sincronizzati per i servizi. Non includere il DN dell’utente in questa impostazione. Per sincronizzare un utente specifico, utilizzare l&#39;impostazione Filtro di ricerca.

**Popola pagina con:** (non obbligatorio) Se selezionata, compila gli attributi nelle pagine delle impostazioni Utente e Gruppo con i corrispondenti valori LDAP predefiniti.

**Filtro di ricerca:** (obbligatorio) Filtro di ricerca da utilizzare per trovare il record associato all&#39;utente. Consulta Sintassi del filtro di ricerca.

### Impostazioni Kerberos {#kerberos-settings}

Se si configura l&#39;autenticazione per un dominio enterprise o ibrido e si seleziona Autenticazione Kerberos, sono disponibili le impostazioni seguenti.

**IP DNS:** indirizzo IP DNS del server in cui sono in esecuzione i moduli AEM. In Windows, è possibile determinare questo indirizzo IP eseguendo ipconfig /all nella riga di comando.

**Host KDC:** Nome host completo o indirizzo IP del server Active Directory utilizzato per l&#39;autenticazione.

**Utente servizio:** Se si utilizza Active Directory 2003, questo valore è il mapping creato per l&#39;entità servizio nel formato `HTTP/<server name>`. Se si utilizza Active Directory 2008, questo valore è l&#39;ID di accesso dell&#39;entità servizio. Ad esempio, si supponga che l&#39;entità servizio sia denominata um spnego, che l&#39;ID utente sia spnegodemo e che la mappatura sia HTTP/example.yourcompany.com. Con Active Directory 2003, l&#39;utente del servizio viene impostato su HTTP/example.yourcompany.com. Con Active Directory 2008, l&#39;utente del servizio viene impostato su spnegodemo. Consultate Abilitare l&#39;SSO tramite SPNEGO.

**Area di autenticazione servizio:** Nome dominio per Active Directory

**Password servizio:** Password utente servizio

**Abilita SPNEGO:** Abilita l&#39;utilizzo di SPNEGO per Single Sign-On (SSO). Consultate Abilitare l&#39;SSO tramite SPNEGO.

### Impostazioni SAML {#saml-settings}

Se stai configurando l’autenticazione per un dominio enterprise o ibrido e selezioni l’autenticazione SAML, sono disponibili le seguenti impostazioni. Per ulteriori informazioni sulle impostazioni SAML, vedere [Configurare le impostazioni del provider di servizi SAML](/help/forms/using/admin-help/configure-saml-service-provider-settings.md#configure-saml-service-provider-settings).

**Selezionare un metadati provider di identità SAML
file da importare:** Fare clic su Sfoglia per selezionare un file di metadati del provider di identità SAML generato dall&#39;IDP, quindi fare clic su Importa. Vengono visualizzati i dettagli dell&#39;IDP.

**Titolo:** Alias dell&#39;URL indicato da EntityID. Il titolo viene visualizzato anche nella pagina di accesso per gli utenti aziendali e locali.

**Il provider di identità supporta l&#39;autenticazione di base del client:** l&#39;autenticazione di base del client viene utilizzata quando l&#39;IDP utilizza un profilo di risoluzione degli artefatti SAML. In questo profilo, User Management si connette a un servizio Web in esecuzione nell&#39;IDP per recuperare l&#39;asserzione SAML effettiva. L&#39;IDP potrebbe richiedere l&#39;autenticazione. Se l&#39;IDP richiede l&#39;autenticazione, selezionare questa opzione e specificare un nome utente e una password nelle caselle fornite.

**Proprietà personalizzate:** Consente di specificare proprietà aggiuntive. Le proprietà aggiuntive sono coppie nome=valore separate da nuove righe.

Se si utilizza l&#39;associazione degli artefatti, sono necessarie le seguenti proprietà personalizzate.

* Aggiungi la seguente proprietà personalizzata per specificare un nome utente che rappresenti il provider di servizi AEM forms, utilizzato per l’autenticazione nel servizio IDP Artifact Resolution.
  `saml.idp.resolve.username=<username>`

* Aggiungere la seguente proprietà personalizzata per specificare la password per l&#39;utente specificato in `saml.idp.resolve.username`.
  `saml.idp.resolve.password=<password>`

* Aggiungi la seguente proprietà personalizzata per consentire al provider di servizi di ignorare la convalida del certificato durante la creazione della connessione con il servizio di risoluzione degli artefatti tramite SSL.
  `saml.idp.resolve.ignorecert=true`

### Impostazioni personalizzate {#custom-settings}

Se si sta configurando l&#39;autenticazione per un dominio enterprise o ibrido e si seleziona Autenticazione personalizzata, selezionare il nome del provider di autenticazione personalizzato.

## Provisioning degli utenti &quot;just-in-time&quot; {#just-in-time-provisioning-of-users}

Il provisioning just-in-time crea automaticamente un utente nel database di User Management dopo che l’utente è stato autenticato correttamente tramite un provider di autenticazione. Anche i ruoli e i gruppi rilevanti vengono assegnati in modo dinamico al nuovo utente. È possibile abilitare il provisioning just-in-time per i domini aziendali e ibridi.

Questa procedura descrive il funzionamento dell’autenticazione tradizionale nelle forme AEM:

1. Quando un utente tenta di accedere ai moduli AEM, Gestione utenti trasmette le proprie credenziali in sequenza a tutti i provider di autenticazione disponibili. Le credenziali di accesso includono la combinazione nome utente/password, il ticket Kerberos, la firma PKCS7 e così via.
1. Il provider di autenticazione convalida le credenziali.
1. Il provider di autenticazione verifica quindi se l&#39;utente esiste nel database User Management. Sono possibili i seguenti stati:

   **Esiste** Se l&#39;utente è corrente e sbloccato, Gestione utenti restituirà l&#39;autenticazione completata. Tuttavia, se l’utente non è attuale o è bloccato, Gestione utenti restituisce un errore di autenticazione.

   **Non esiste** Gestione utenti restituisce un errore di autenticazione.

   **Non valido** Gestione utenti ha restituito un errore di autenticazione.

1. Viene valutato il risultato restituito dal provider di autenticazione. Se il provider di autenticazione ha restituito l&#39;autenticazione, l&#39;utente può accedere. In caso contrario, User Management controlla con il provider di autenticazione successivo (passaggi 2-3).
1. Se nessun provider di autenticazione disponibile convalida le credenziali utente, viene restituito un errore di autenticazione.

Quando è abilitato il provisioning just-in-time, i nuovi utenti vengono creati in modo dinamico in Gestione utenti se uno dei provider di autenticazione convalida le credenziali. (Dopo il punto 3 della procedura precedente).

Senza il provisioning just-in-time, quando un utente viene autenticato correttamente ma non viene trovato nel database di gestione utenti, l’autenticazione non riesce. Il provisioning just-in-time aggiunge un passaggio nella procedura di autenticazione per creare l’utente e assegnare ruoli e gruppi all’utente.

### Abilitare il provisioning just-in-time per un dominio {#enable-just-in-time-provisioning-for-a-domain}

1. Scrivere un contenitore di servizi che implementi le interfacce IdentityCreator e AssignmentProvider. (Vedi [Programmazione con moduli AEM](https://www.adobe.com/go/learn_aemforms_programming_63).)
1. Distribuire il contenitore del servizio nel server Forms.
1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione dominio.

   Selezionare un dominio esistente o fare clic su Nuovo dominio enterprise.

1. Per creare un dominio, fai clic su Nuovo dominio enterprise o Nuovo dominio ibrido. Per modificare un dominio esistente, fai clic sul nome del dominio.
1. Selezionare Abilita provisioning Just In Time.

   ***nota **: se la casella di controllo Abilita provisioning Just In Time non è presente, fare clic su Home > Impostazioni > Gestione utente> Configurazione > Attributi di sistema avanzati, quindi fare clic su Ricarica.*

1. Aggiungi provider di autenticazione. Durante l&#39;aggiunta dei provider di autenticazione, nella schermata Nuova autenticazione selezionare un creatore di identità e un provider di assegnazione registrati. (Vedere [Configurazione dei provider di autenticazione](configuring-authentication-providers.md#configuring-authentication-providers).)
1. Salva il dominio.
