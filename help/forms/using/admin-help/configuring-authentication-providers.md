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
workflow-type: tm+mt
source-wordcount: '1595'
ht-degree: 0%

---


# Configurazione dei provider di autenticazione {#configuring-authentication-providers}

I domini ibridi richiedono almeno un provider di autenticazione e i domini enterprise richiedono almeno un provider di autenticazione o un provider di directory.

Se si abilita SSO utilizzando SPNEGO, aggiungere un provider di autenticazione Kerberos con SPNEGO abilitato e un provider LDAP come backup. Questa configurazione abilita l&#39;autenticazione utente con un ID utente e una password se SPNEGO non funziona. (vedere [Abilitare SSO utilizzando SPNEGO](/help/forms/using/admin-help/enabling-single-sign-on-aem.md#enable-sso-using-spnego)).

## Aggiunta di un provider di autenticazione {#add-an-authentication-provider}

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Gestione dominio.
1. Fare clic su un dominio esistente nell&#39;elenco. Se si sta aggiungendo l&#39;autenticazione per un nuovo dominio, vedere [Aggiungi un dominio Enterprise](/help/forms/using/admin-help/adding-domains.md#add-an-enterprise-domain) o [Aggiungi un dominio ibrido](/help/forms/using/admin-help/adding-domains.md#add-a-hybrid-domain).
1. Fate clic su Aggiungi autenticazione e, nell&#39;elenco Provider autenticazione, selezionate un provider, a seconda del meccanismo di autenticazione utilizzato dall&#39;organizzazione.
1. Fornite eventuali informazioni aggiuntive richieste sulla pagina. (Vedere [Impostazioni di autenticazione](configuring-authentication-providers.md#authentication-settings).)
1. (Facoltativo) Fate clic su Test per verificare la configurazione.
1. Fate clic su OK, quindi di nuovo su OK.

## Modifica provider di autenticazione esistente {#edit-an-existing-authentication-provider}

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Gestione dominio.
1. Fare clic sul dominio appropriato nell&#39;elenco.
1. Nella pagina visualizzata, selezionate il provider di autenticazione appropriato dall&#39;elenco e apportate le modifiche necessarie. (Vedere [Impostazioni di autenticazione](configuring-authentication-providers.md#authentication-settings).)
1. Fai clic su OK.

## Eliminare un provider di autenticazione {#delete-an-authentication-provider}

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Gestione dominio.
1. Fare clic sul dominio appropriato nell&#39;elenco.
1. Selezionate le caselle di controllo per i provider di autenticazione da eliminare e fate clic su Elimina.
1. Fare clic su OK nella pagina di conferma visualizzata e fare di nuovo clic su OK.

## Impostazioni di autenticazione {#authentication-settings}

Sono disponibili le seguenti impostazioni, a seconda del tipo di dominio e del tipo di autenticazione scelto.

### Impostazioni LDAP {#ldap-settings}

Se state configurando l’autenticazione per un dominio Enterprise o ibrido e selezionate l’autenticazione LDAP, potete scegliere di utilizzare il server LDAP specificato nella configurazione di directory oppure potete scegliere un altro server LDAP da usare per l’autenticazione. Se scegliete un server diverso, gli utenti devono esistere su entrambi i server LDAP.

Per utilizzare il server LDAP specificato nella configurazione della directory, selezionate LDAP come provider di autenticazione e fate clic su OK.

Per utilizzare un altro server LDAP per eseguire l’autenticazione, selezionate LDAP come provider di autenticazione e selezionate la casella di controllo Autenticazione LDAP personalizzata. Vengono visualizzate le seguenti impostazioni di configurazione.

**Server:** (obbligatorio) Nome di dominio completo (FQDN) del server di directory. Ad esempio, per un computer chiamato x sulla rete corp.example.com, l&#39;FQDN è x.corp.example.com. Un indirizzo IP può essere usato al posto del nome del server FQDN.

**Porta:** (obbligatoria) La porta utilizzata dal server di directory. In genere 389 o 636 se il protocollo SSL (Secure Sockets Layer) è utilizzato per inviare informazioni di autenticazione attraverso la rete.

**SSL:** (obbligatorio) Specifica se il server di directory utilizza SSL per l’invio di dati sulla rete. Il valore predefinito è No. Se si imposta su Sì, il certificato del server LDAP corrispondente deve essere considerato affidabile dall&#39;ambiente runtime Java™ (JRE) del server dell&#39;applicazione.

**Binding** (obbligatorio) Specifica come accedere alla directory.

**Anonimo:** non sono necessari nome utente o password.

**Utente:** Autenticazione obbligatoria. Nella casella Nome, specificare il nome del record utente che può accedere alla directory. È consigliabile immettere il nome distinto completo (DN) dell&#39;account utente, ad esempio cn=Jane Doe, ou=user, dc=can, dc=com. Nella casella Password, specificare la password associata. Queste impostazioni sono necessarie quando si seleziona Utente come opzione di binding.

**Recupera DN di base:** (non obbligatorio) Recupera i DN di base e li visualizza nell&#39;elenco a discesa. Questa impostazione è utile quando hai più DN base e devi selezionare un valore.

**DN di base:** (obbligatorio) Utilizzato come punto di partenza per la sincronizzazione di utenti e gruppi dalla gerarchia LDAP. È consigliabile specificare un DN di base al livello più basso della gerarchia che includa tutti gli utenti e i gruppi che devono essere sincronizzati per i servizi. Non includete il DN dell&#39;utente in questa impostazione. Per sincronizzare un particolare utente, usate l’impostazione Filtro ricerca.

**Compilare la pagina con:** (Non obbligatorio) Se questa opzione è selezionata, compila gli attributi nelle pagine delle impostazioni Utente e Gruppo con i corrispondenti valori LDAP predefiniti.

**Filtro di ricerca:** (obbligatorio) Il filtro di ricerca da utilizzare per trovare il record associato all&#39;utente. Consulta Cerca sintassi filtro.

### Impostazioni Kerberos {#kerberos-settings}

Se si sta configurando l&#39;autenticazione per un dominio Enterprise o ibrido e si seleziona l&#39;autenticazione Kerberos, sono disponibili le seguenti impostazioni.

**IP DNS:** l&#39;indirizzo IP DNS del server in cui sono in esecuzione AEM moduli. In Windows, potete determinare questo indirizzo IP eseguendo ipconfig /all alla riga di comando.

**Host KDC: nome host** completo o indirizzo IP del server Active Directory utilizzato per l&#39;autenticazione.

**Utente del servizio:** se si utilizza Active Directory 2003, questo valore è il mapping creato per l&#39;entità del servizio nel modulo  `HTTP/<server name>`. Se si utilizza Active Directory 2008, questo valore è l&#39;ID di accesso dell&#39;entità del servizio. Ad esempio, si supponga che l&#39;entità del servizio sia denominata um spnego, che l&#39;ID utente sia spnegozidemo e che la mappatura sia HTTP/example.corp.nomeazienda.com. Con Active Directory 2003, l&#39;utente del servizio è impostato su HTTP/example.corp.nomeazienda.com. Con Active Directory 2008, l&#39;utente del servizio è impostato su sptrading demo. Consultate Abilitare SSO con SPNEGO.

**Service Realm:nome** di dominio per Active Directory

**Password del servizio:password utente** del servizio

**Abilita SPNEGO:** abilita l&#39;utilizzo di SPNEGO per Single Sign-On (SSO). Consultate Abilitare SSO con SPNEGO.

### Impostazioni SAML {#saml-settings}

Se state configurando l&#39;autenticazione per un dominio Enterprise o ibrido e selezionate l&#39;autenticazione SAML, sono disponibili le seguenti impostazioni. Per informazioni su ulteriori impostazioni SAML, vedere [Configurare le impostazioni del provider di servizi SAML](/help/forms/using/admin-help/configure-saml-service-provider-settings.md#configure-saml-service-provider-settings).

**Selezionare un file metadati provider di identità SAML da importare:** fare clic su Sfoglia per selezionare un file di metadati provider di identità SAML generato dall&#39;IDP, quindi fare clic su Importa. Vengono visualizzati i dettagli dell&#39;IDP.

**Titolo:** alias all’URL indicato dall’EntityID. Il titolo viene visualizzato anche nella pagina di accesso per gli utenti Enterprise e Locali.

**Il provider di identità supporta l&#39;autenticazione di base del client: l&#39;autenticazione di base del** client viene utilizzata quando l&#39;IDP utilizza un profilo di risoluzione degli artefatti SAML. In questo profilo, User Management si connette a un servizio Web in esecuzione nell&#39;IDP per recuperare l&#39;asserzione SAML effettiva. L&#39;IDP potrebbe richiedere l&#39;autenticazione. Se l&#39;IDP richiede l&#39;autenticazione, selezionare questa opzione e specificare un nome utente e una password nelle caselle fornite.

**Proprietà personalizzate:** consente di specificare proprietà aggiuntive. Le proprietà aggiuntive sono coppie nome=valore separate da nuove righe.

Se si utilizza il binding degli artifact, sono necessarie le seguenti proprietà personalizzate.

* Aggiungete la seguente proprietà personalizzata per specificare un nome utente che rappresenta il provider di servizi AEM, che verrà utilizzato per l&#39;autenticazione al servizio di risoluzione degli artefatti IDP.
   `saml.idp.resolve.username=<username>`

* Aggiungete la seguente proprietà personalizzata per specificare la password per l&#39;utente specificata in `saml.idp.resolve.username`.
   `saml.idp.resolve.password=<password>`

* Aggiungete la seguente proprietà personalizzata per consentire al provider di servizi di ignorare la convalida del certificato durante la definizione della connessione con il servizio di risoluzione degli artefatti tramite SSL.
   `saml.idp.resolve.ignorecert=true`

### Impostazioni personalizzate {#custom-settings}

Se state configurando l&#39;autenticazione per un dominio Enterprise o ibrido e selezionate Autenticazione personalizzata, selezionate il nome del provider di autenticazione personalizzato.

## Provisioning in tempo reale degli utenti {#just-in-time-provisioning-of-users}

Il provisioning in tempo reale crea automaticamente un utente nel database Gestione utente dopo che l&#39;utente è stato autenticato tramite un provider di autenticazione. Anche i ruoli e i gruppi pertinenti vengono assegnati in modo dinamico al nuovo utente. Potete abilitare il provisioning &quot;just-in-time&quot; per i domini Enterprise e ibridi.

Questa procedura descrive il funzionamento dell&#39;autenticazione tradizionale nei moduli AEM:

1. Quando un utente tenta di accedere ai moduli AEM, Gestione utente passa le credenziali in sequenza a tutti i provider di autenticazione disponibili. (Le credenziali di login includono la combinazione nome utente/password, il ticket Kerberos, la firma PKCS7 e così via).
1. Il provider di autenticazione convalida le credenziali.
1. Il provider di autenticazione verifica quindi se l&#39;utente esiste nel database Gestione utente. Sono possibili i seguenti stati:

   **** EsisteSe l&#39;utente è corrente e sbloccato, Gestione utente restituisce il successo dell&#39;autenticazione. Tuttavia, se l&#39;utente non è corrente o è bloccato, Gestione utente restituisce un errore di autenticazione.

   **Non** esisteUser Management restituisce un errore di autenticazione.

   **Gestione** InvalidUser restituisce un errore di autenticazione.

1. Il risultato restituito dal provider di autenticazione viene valutato. Se il provider di autenticazione ha restituito un esito positivo, l&#39;utente può effettuare l&#39;accesso. In caso contrario, Gestione utente verifica con il provider di autenticazione successivo (passaggi da 2 a 3).
1. L&#39;errore di autenticazione viene restituito se nessun provider di autenticazione disponibile convalida le credenziali utente.

Quando il provisioning &quot;in-time&quot; è abilitato, i nuovi utenti vengono creati dinamicamente in Gestione utente se uno dei provider di autenticazione convalida le proprie credenziali. (Dopo la fase 3 della procedura precedente).

Senza il provisioning &quot;in-time&quot;, quando un utente viene autenticato correttamente ma non viene trovato nel database di Gestione utente, l&#39;autenticazione non riesce. Il provisioning in tempo reale aggiunge un passaggio alla procedura di autenticazione per creare l&#39;utente e assegnare ruoli e gruppi all&#39;utente.

### Abilitare il provisioning just-in-time per un dominio {#enable-just-in-time-provisioning-for-a-domain}

1. Scrivete un contenitore di servizi che implementa le interfacce IdentityCreator e AssignmentProvider. (Vedere [Programmazione con moduli AEM](https://www.adobe.com/go/learn_aemforms_programming_63).)
1. Distribuire il contenitore del servizio al server dei moduli.
1. Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Gestione dominio.

   Selezionate un dominio esistente o fate clic su Nuovo dominio Enterprise.

1. Per creare un dominio, fare clic su Nuovo dominio Enterprise o Nuovo dominio ibrido. Per modificare un dominio esistente, fate clic sul nome del dominio.
1. Selezionate Abilita solo in provisioning tempo.

   ***nota **: Se la casella di controllo Abilita solo in provisioning temporale non è presente, fate clic su Home > Impostazioni > Gestione utente > Configurazione > Attributi di sistema avanzati, quindi fate clic su Ricarica.*

1. Aggiunta di provider di autenticazione. Durante l&#39;aggiunta di provider di autenticazione, nella schermata Nuova autenticazione, selezionate un creatore di identità registrato e un provider di assegnazione. (Vedere [Configurazione di provider di autenticazione](configuring-authentication-providers.md#configuring-authentication-providers).)
1. Salva il dominio.

