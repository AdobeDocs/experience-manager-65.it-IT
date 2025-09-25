---
title: Configurazione dei provider di autenticazione
description: Aggiungi, modifica o elimina provider di autenticazione, modifica le impostazioni di autenticazione e leggi informazioni sul provisioning just-in-time degli utenti.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: d72a3977-1423-49e0-899b-234bb76be378
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '1592'
ht-degree: 100%

---

# Configurazione dei provider di autenticazione {#configuring-authentication-providers}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

I domini ibridi richiedono almeno un provider di autenticazione, mentre i domini Enterprise richiedono almeno un provider di autenticazione o un provider di directory.

Se abiliti SSO utilizzando SPNEGO, aggiungi un provider di autenticazione Kerberos con SPNEGO abilitato e un provider LDAP come backup. Questa configurazione consente l’autenticazione utente con un ID utente e una password se SPNEGO non funziona. Consulta [Abilitare SSO tramite SPNEGO](/help/forms/using/admin-help/enabling-single-sign-on-aem.md#enable-sso-using-spnego).

## Aggiungere un provider di autenticazione {#add-an-authentication-provider}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utenti > Gestione dominio.
1. Fai clic su un dominio esistente nell’elenco. Se stai aggiungendo l’autenticazione per un nuovo dominio, consulta [Aggiungere un dominio Enterprise](/help/forms/using/admin-help/adding-domains.md#add-an-enterprise-domain) o [Aggiungere un dominio ibrido](/help/forms/using/admin-help/adding-domains.md#add-a-hybrid-domain).
1. Fai clic su Aggiungi autenticazione e, nell’elenco Provider di autenticazione, seleziona un provider, a seconda del meccanismo di autenticazione utilizzato dall’organizzazione.
1. Fornisci eventuali informazioni aggiuntive richieste sulla pagina. Consulta [Impostazioni di autenticazione](configuring-authentication-providers.md#authentication-settings).
1. (Facoltativo) Fai clic su Test per verificare la configurazione.
1. Fai clic su OK e quindi di nuovo su OK.

## Modificare un provider di autenticazione esistente {#edit-an-existing-authentication-provider}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utenti > Gestione dominio.
1. Fai clic sul dominio appropriato nell’elenco.
1. Nella pagina visualizzata, seleziona il provider di autenticazione appropriato dall’elenco e apporta le modifiche necessarie. Consulta [Impostazioni di autenticazione](configuring-authentication-providers.md#authentication-settings).
1. Fai clic su OK.

## Eliminare un provider di autenticazione {#delete-an-authentication-provider}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utenti > Gestione dominio.
1. Fai clic sul dominio appropriato nell’elenco.
1. Seleziona le caselle di controllo relative ai provider di autenticazione da eliminare e fai clic su Elimina.
1. Fai clic su OK nella pagina di conferma visualizzata e fai di nuovo clic su OK.

## Impostazioni di autenticazione {#authentication-settings}

Sono disponibili le seguenti impostazioni, a seconda del tipo di dominio e del tipo di autenticazione che hai scelto.

### Impostazioni LDAP {#ldap-settings}

Se stai configurando l’autenticazione per un dominio Enterprise o ibrido e selezioni l’autenticazione LDAP, puoi scegliere di utilizzare il server LDAP specificato nella configurazione della directory oppure scegliere un server LDAP diverso da utilizzare per l’autenticazione. Se scegli un server diverso, gli utenti devono esistere in entrambi i server LDAP.

Per utilizzare il server LDAP specificato nella configurazione della directory, seleziona LDAP come provider di autenticazione e fai clic su OK.

Per utilizzare un server LDAP diverso per eseguire l’autenticazione, seleziona LDAP come provider di autenticazione e seleziona la casella di controllo Autenticazione LDAP personalizzata. Vengono visualizzate le seguenti impostazioni di configurazione.

**Server:** (obbligatorio) il nome dominio completo (FQDN) del server delle directory. Ad esempio, per un computer denominato x nella rete example.com, il nome di dominio completo (FQDN) è x.example.com. Puoi utilizzare un indirizzo IP al posto del nome del server FQDN.

**Porta:** (obbligatoria) la porta utilizzata dal server delle directory. In genere, 389 o 636 se il protocollo SSL (Secure Sockets Layer) viene utilizzato per l’invio di informazioni di autenticazione sulla rete.

**SSL:** (obbligatorio) specifica se il server della directory utilizza SSL per l’invio di dati in rete. L’impostazione predefinita è no. Se impostato su sì, il certificato del server LDAP corrispondente deve essere considerato attendibile dall’ambiente runtime Java™ (JRE) del server applicazioni.

**Binding** (obbligatorio) specifica come accedere alla directory.

**Anonimo:** non è richiesto alcun nome utente o password.

**Utente:** è richiesta l’autenticazione. Nella casella Nome, specifica il nome del record utente che può accedere alla directory. È consigliabile immettere il nome distinto completo (DN) dell’account utente, ad esempio cn=Jane Doe, ou=user, dc=can, dc=com. Nella casella Password, specifica la password associata. Queste impostazioni sono necessarie quando selezioni Utente come opzione di binding.

**Recupera DN di base:** (non obbligatorio) recupera i DN di base e li visualizza nell’elenco a discesa. Questa impostazione è utile quando disponi di più DN di base e devi selezionare un valore.

**DN di base:** (obbligatorio) utilizzato come punto iniziale per la sincronizzazione di utenti e gruppi dalla gerarchia LDAP. È consigliabile specificare un DN di base al livello più basso della gerarchia che includa tutti gli utenti e i gruppi che devono essere sincronizzati per i servizi. Non includere il DN dell’utente in questa impostazione. Per sincronizzare un utente specifico, utilizza l’impostazione filtro di ricerca.

**Popola pagina con:** (non obbligatorio) se selezionata, popola gli attributi nelle pagine delle impostazioni Utente e Gruppo con i corrispondenti valori LDAP predefiniti.

**Filtro di ricerca:** (obbligatorio) il filtro di ricerca da utilizzare per trovare il record associato all’utente. Consulta Sintassi del filtro di ricerca.

### Impostazioni Kerberos {#kerberos-settings}

Se stai configurando l’autenticazione per un dominio Enterprise o ibrido e selezioni Autenticazione Kerberos, sono disponibili le impostazioni seguenti.

**IP DNS:** l’indirizzo IP DNS del server in cui è in esecuzione AEM Forms. In Windows, puoi determinare questo indirizzo IP eseguendo ipconfig /all nella riga di comando.

**Host KDC:** il nome host completo o l’indirizzo IP del server Active Directory utilizzato per l’autenticazione.

**Utente servizio:** se utilizzi Active Directory 2003, questo valore è la mappatura creata per l’entità servizio nel formato `HTTP/<server name>`. Se utilizzi Active Directory 2008, questo valore è l’ID di accesso dell’entità servizio. Ad esempio, supponiamo che l’entità servizio sia denominata um spnego, che l’ID utente sia spnegodemo e che la mappatura sia HTTP/example.yourcompany.com. Con Active Directory 2003, imposta l’utente del servizio su HTTP/example.yourcompany.com. Con Active Directory 2008, imposta l’utente del servizio su spnegodemo. Consulta Abilitare SSO tramite SPNEGO.

**Area di autenticazione servizio:** il nome dominio per Active Directory

**Password servizio:** la password dell’utente servizio

**Abilita SPNEGO:** abilita l’utilizzo di SPNEGO per SSO (single sign-on). Consulta Abilitare SSO tramite SPNEGO.

### Impostazioni SAML {#saml-settings}

Se stai configurando l’autenticazione per un dominio Enterprise o ibrido e selezioni l’autenticazione SAML, sono disponibili le seguenti impostazioni. Per ulteriori informazioni sulle impostazioni SAML, consulta [Configurare le impostazioni del provider di servizi SAML](/help/forms/using/admin-help/configure-saml-service-provider-settings.md#configure-saml-service-provider-settings).

**Seleziona un file metadati provider di identità SAML
da importare:** fai clic su Sfoglia per selezionare un file metadati del provider di identità SAML generato dall’IDP, quindi fai clic su Importa. Vengono visualizzati i dettagli dall’IDP.

**Titolo:** alias dell’URL indicato da EntityID. Il titolo viene visualizzato anche nella pagina di accesso per gli utenti Enterprise e locali.

**Il provider di identità supporta l’autenticazione di base del client:** l’autenticazione di base del client viene utilizzata quando l’IDP utilizza un profilo di risoluzione degli artefatti SAML. In questo profilo, gestione utenti si connette a un servizio web in esecuzione nell’IDP per recuperare l’asserzione SAML effettiva. L&#39;IDP potrebbe richiedere l’autenticazione. Se l’IDP richiede l’autenticazione, seleziona questa opzione e specifica un nome utente e una password nelle caselle fornite.

**Proprietà personalizzate:** consente di specificare proprietà aggiuntive. Le proprietà aggiuntive sono coppie nome=valore separate da nuove righe.

Se utilizzi l’associazione degli artefatti, sono necessarie le seguenti proprietà personalizzate.

* Aggiungi la seguente proprietà personalizzata per specificare un nome utente che rappresenti il provider di servizi AEM Forms, utilizzato per l’autenticazione nel servizio di risoluzione degli artefatti IDP.
  `saml.idp.resolve.username=<username>`

* Aggiungi la seguente proprietà personalizzata per specificare la password per l’utente specificato in `saml.idp.resolve.username`.
  `saml.idp.resolve.password=<password>`

* Aggiungi la seguente proprietà personalizzata per consentire al provider di servizi di ignorare la convalida del certificato durante la creazione della connessione con il servizio di risoluzione degli artefatti tramite SSL.
  `saml.idp.resolve.ignorecert=true`

### Impostazioni personalizzate {#custom-settings}

Se stai configurando l’autenticazione per un dominio Enterprise o ibrido e selezioni l’autenticazione personalizzata, seleziona il nome del provider di autenticazione personalizzato.

## Provisioning just-in-time degli utenti {#just-in-time-provisioning-of-users}

Il provisioning just-in-time crea automaticamente un utente nel database di gestione utenti dopo che l’utente è stato autenticato correttamente tramite un provider di autenticazione. Anche i ruoli e i gruppi rilevanti vengono assegnati in modo dinamico al nuovo utente. Puoi abilitare il provisioning just-in-time per i domini Enterprise e ibridi.

Questa procedura descrive il funzionamento dell’autenticazione tradizionale in AEM Forms:

1. Quando un utente tenta di accedere ad AEM Forms, Gestione utenti trasmette le relative credenziali in sequenza a tutti i provider di autenticazione disponibili. Le credenziali di accesso includono la combinazione nome utente/password, il ticket Kerberos, la firma PKCS7 e così via.
1. Il provider di autenticazione convalida le credenziali.
1. Il provider di autenticazione verifica quindi se l’utente esiste nel database della Gestione utenti. Sono possibili i seguenti stati:

   **Esiste** Se l’utente è corrente e sbloccato, Gestione utenti restituirà l’autenticazione completata. Tuttavia, se l’utente non è attuale o è bloccato, Gestione utenti restituisce un errore di autenticazione.

   **Non esiste** Gestione utenti restituisce un errore di autenticazione.

   **Non valido** Gestione utenti restituisce un errore di autenticazione.

1. Viene valutato il risultato restituito dal provider di autenticazione. Se il provider di autenticazione ha restituito l’autenticazione, l’utente può accedere. In caso contrario, Gestione utente controlla con il provider di autenticazione successivo (passaggi 2-3).
1. Se nessun provider di autenticazione disponibile convalida le credenziali utente, viene restituito un errore di autenticazione.

Quando è abilitato il provisioning just-in-time, i nuovi utenti vengono creati in modo dinamico in Gestione utenti se uno dei provider di autenticazione convalida le credenziali. (Dopo il passaggio 3 della procedura precedente).

Senza il provisioning just-in-time, quando un utente viene autenticato correttamente ma non viene trovato nel database di gestione utenti, l’autenticazione non riesce. Il provisioning just-in-time aggiunge un passaggio nella procedura di autenticazione per creare l’utente e assegnargli ruoli e gruppi.

### Abilitare il provisioning just-in-time per un dominio {#enable-just-in-time-provisioning-for-a-domain}

1. Scrivi un contenitore di servizi che implementi le interfacce IdentityCreator e AssignmentProvider. Consulta [Programmazione con AEM Forms](https://www.adobe.com/go/learn_aemforms_programming_63_it).
1. Distribusci il contenitore del servizio nel server Forms.
1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utenti > Gestione dominio.

   Seleziona un dominio esistente o fai clic su Nuovo dominio enterprise.

1. Per creare un dominio, fai clic su Nuovo dominio enterprise o Nuovo dominio ibrido. Per modificare un dominio esistente, fai clic sul nome del dominio.
1. Seleziona Abilita provisioning Just In Time.

   ***nota **: se la casella di controllo Abilita provisioning Just In Time non è presente, fai clic su Home > Impostazioni > Gestione utente> Configurazione > Attributi di sistema avanzati, quindi fai clic su Ricarica.*

1. Aggiungi provider di autenticazione. Durante l’aggiunta dei provider di autenticazione, nella schermata Nuova autenticazione, seleziona un creatore di identità e un provider di assegnazione registrati. Consulta [Configurazione dei provider di autenticazione](configuring-authentication-providers.md#configuring-authentication-providers).
1. Salva il dominio.
