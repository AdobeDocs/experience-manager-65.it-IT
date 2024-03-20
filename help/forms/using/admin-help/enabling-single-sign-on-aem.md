---
title: Abilitazione del single sign-on nei moduli AEM
description: Scopri come abilitare il single sign-on (SSO) utilizzando le intestazioni HTTP e SPNEGO.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 89561ed0-d094-4ef7-9bc1-bde11f3c5bc3
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1520'
ht-degree: 0%

---

# Abilitazione del single sign-on nei moduli AEM{#enabling-single-sign-on-in-aem-forms}

I moduli AEM offrono due modi per abilitare il Single Sign-On (SSO): intestazioni HTTP e SPNEGO.

Quando l’SSO viene implementato, le pagine di accesso degli utenti dei moduli AEM non sono obbligatorie e non vengono visualizzate se l’utente è già autenticato tramite il portale aziendale.

Se i moduli AEM non sono in grado di autenticare un utente utilizzando uno di questi metodi, l’utente viene reindirizzato a una pagina di accesso.

## Abilita SSO tramite intestazioni HTTP {#enable-sso-using-http-headers}

È possibile utilizzare la pagina Configurazione portale per abilitare il Single Sign-On (SSO) tra le applicazioni e qualsiasi applicazione che supporti la trasmissione dell&#39;identità tramite l&#39;intestazione HTTP. Quando l’SSO viene implementato, le pagine di accesso degli utenti dei moduli AEM non sono obbligatorie e non vengono visualizzate se l’utente è già autenticato tramite il portale aziendale.

È inoltre possibile abilitare SSO utilizzando SPNEGO. (vedere [Abilita SSO tramite SPNEGO](enabling-single-sign-on-aem.md#enable-sso-using-spnego).)

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Configurazione > Configura attributi del portale.
1. Selezionare Sì per abilitare l&#39;SSO. Se si seleziona No, le altre impostazioni della pagina non sono disponibili.
1. Impostare le opzioni rimanenti sulla pagina come desiderato e fare clic su OK:

   * **Tipo SSO:** (Obbligatorio) Seleziona Intestazione HTTP per abilitare SSO utilizzando le intestazioni HTTP.
   * **Intestazione HTTP per l’identificatore dell’utente:** (Obbligatorio) Nome dell’intestazione il cui valore contiene l’identificatore univoco dell’utente connesso. User Management utilizza questo valore per trovare l&#39;utente nel database User Management. Il valore ottenuto da questa intestazione deve corrispondere all&#39;identificatore univoco dell&#39;utente sincronizzato dalla directory LDAP. (vedere [Impostazioni utente](/help/forms/using/admin-help/adding-configuring-users.md#user-settings).)
   * **Il valore dell’identificatore corrisponde all’ID utente dell’utente invece dell’identificatore univoco dell’utente:** Associa il valore dell’identificatore univoco dell’utente all’ID utente. Selezionare questa opzione se l&#39;identificatore univoco dell&#39;utente è un valore binario che non può essere facilmente propagato tramite intestazioni HTTP (ad esempio, objectGUID se si sincronizzano gli utenti da Active Directory).
   * **Intestazione HTTP per il dominio:** (Non obbligatorio) Nome dell’intestazione il cui valore contiene il nome di dominio. Usa questa impostazione solo se nessuna singola intestazione HTTP identifica l’utente in modo univoco. Utilizza questa impostazione per i casi in cui esistono più domini e l’identificatore univoco è univoco solo all’interno di un dominio. In questo caso, specificare il nome dell&#39;intestazione in questa casella di testo e specificare il mapping dei domini per i domini multipli nella casella Mapping domini. (vedere [Modifica e conversione di domini esistenti](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains).)
   * **Mappatura dominio:** (Obbligatorio) Specifica la mappatura per più domini nel formato *header value=domain name*.

     Consideriamo ad esempio una situazione in cui l’intestazione HTTP per un dominio è domainName e può avere valori di domain1, domain2 o domain3. In questo caso, utilizza la mappatura del dominio per mappare i valori domainName ai nomi di dominio User Management. Ogni mappatura deve essere su una riga diversa:

     domain1=dominioUM1

     domain2=dominioUM2

     domain3=dominioUM3

### Configurare i referenti consentiti {#configure-allowed-referers}

Per i passaggi per configurare i referenti consentiti, consulta [Configurare i referenti consentiti](/help/forms/using/admin-help/preventing-csrf-attacks.md#configure-allowed-referers).

## Abilita SSO tramite SPNEGO {#enable-sso-using-spnego}

È possibile utilizzare il meccanismo di negoziazione GSSAPI (SPNEGO) semplice e protetto per abilitare il Single Sign-On (SSO) quando si utilizza Active Directory come server LDAP in un ambiente Windows. Quando l’SSO è abilitato, le pagine di accesso degli utenti dei moduli AEM non sono obbligatorie e non vengono visualizzate.

Puoi anche abilitare il SSO utilizzando le intestazioni HTTP. (vedere [Abilita SSO tramite intestazioni HTTP](enabling-single-sign-on-aem.md#enable-sso-using-http-headers).)

>[!NOTE]
>
>AEM Forms su JEE non supporta la configurazione del SSO utilizzando Kerberos/SPNEGO in più ambienti di dominio figlio.

1. Decidi quale dominio utilizzare per abilitare l&#39;SSO. Il server AEM Forms e gli utenti devono far parte dello stesso dominio Windows o dominio trusted.
1. In Active Directory, creare un utente che rappresenti il server AEM Forms. (vedere [Creare un account utente](enabling-single-sign-on-aem.md#create-a-user-account).) Se configuri più domini per l&#39;utilizzo di SPNEGO, assicurati che le password di ciascuno di questi utenti siano diverse. Se le password non sono diverse, SPNEGO SSO non funziona.
1. Mappare il nome dell&#39;entità servizio. (vedere [Mappare un nome principale di servizio (SPN)](enabling-single-sign-on-aem.md#map-a-service-principal-name-spn).)
1. Configurare il controller di dominio. (vedere [Impedisci errori di verifica integrità Kerberos](enabling-single-sign-on-aem.md#prevent-kerberos-integrity-check-failures).)
1. Aggiungere o modificare un dominio enterprise come descritto in [Aggiunta di domini](/help/forms/using/admin-help/adding-domains.md#adding-domains) o [Modifica e conversione di domini esistenti](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains). Quando si crea o si modifica il dominio enterprise, eseguire le operazioni seguenti:

   * Aggiungere o modificare una directory contenente le informazioni di Active Directory.
   * Aggiungere LDAP come provider di autenticazione.
   * Aggiungere Kerberos come provider di autenticazione. Nella pagina Nuova o Modifica autenticazione per Kerberos specificare le informazioni seguenti:

      * **Provider di autenticazione:** Kerberos
      * **IP DNS:** Indirizzo IP DNS del server in cui è in esecuzione il modulo AEM. È possibile determinare questo indirizzo IP eseguendo `ipconfig/all` sulla riga di comando.
      * **Host KDC:** Nome host o indirizzo IP completo del server Active Directory utilizzato per l&#39;autenticazione
      * **Utente servizio:** Il nome dell&#39;entità servizio (SPN) passato allo strumento KtPass. Nell’esempio precedente, l’utente del servizio è `HTTP/lcserver.um.lc.com`.
      * **Area di autenticazione servizio:** Nome di dominio per Active Directory. Nell’esempio utilizzato in precedenza, il nome del dominio è `UM.LC.COM.`
      * **Password servizio:** Password dell’utente del servizio. Nell’esempio precedente, la password del servizio è `password`.
      * **Attiva SPNEGO:** Consente l&#39;utilizzo di SPNEGO per il Single Sign-On (SSO). Seleziona questa opzione.

1. Configurare le impostazioni del browser client SPNEGO. (vedere [Configurazione delle impostazioni del browser client SPNEGO](enabling-single-sign-on-aem.md#configuring-spnego-client-browser-settings).)

### Creare un account utente {#create-a-user-account}

1. In SPNEGO, registrare un servizio come utente in Active Directory sul controller di dominio per rappresentare i moduli AEM. Nel controller di dominio passare a Menu Start > Strumenti di amministrazione > Utenti e computer di Active Directory. Se Strumenti di amministrazione non è disponibile nel menu Start, utilizzare il Pannello di controllo Campaign.
1. Fare clic sulla cartella Utenti per visualizzare un elenco di utenti.
1. Fare clic con il pulsante destro del mouse sulla cartella utente e selezionare Nuovo > Utente.
1. Digitare Nome/Cognome e Nome di accesso utente, quindi fare clic su Avanti. Ad esempio, imposta i seguenti valori:

   * **Nome**: umspnego
   * **Nome di accesso utente**: spnegozidemo

1. Digitare una password. Ad esempio, impostalo su *password*. Assicurati che l’opzione Password Never Expires (Password senza scadenza) sia selezionata e che non siano selezionate altre opzioni.
1. Fare clic su Avanti e quindi su Fine.

### Mappare un nome principale di servizio (SPN) {#map-a-service-principal-name-spn}

1. Ottenere l&#39;utilità KtPass. Questa utility viene utilizzata per mappare un SPN a un realm. È possibile ottenere l&#39;utilità KtPass come parte di Windows Server Tool Pack o Resource Kit. (vedere [Strumenti di supporto per Windows Server 2003 Service Pack 1](https://support.microsoft.com/kb/892777).)
1. Al prompt dei comandi eseguire `ktpass` utilizzando i seguenti argomenti:

   `ktpass -princ HTTP/`*host* `@`*AREA DI AUTENTICAZIONE* `-mapuser`*utente*

   Digitare ad esempio il testo seguente:

   `ktpass -princ HTTP/lcserver.um.lc.com@UM.LC.COM -mapuser spnegodemo`

   I valori da fornire sono descritti come segue:

   **host:** Nome completo del server Forms o qualsiasi URL univoco. In questo esempio, è impostato su lcserver.um.lc.com.

   **REALM:** Reame di Active Directory per il controller di dominio. In questo esempio, è impostato su UM.LC.COM. Assicurati di immettere il realm in caratteri maiuscoli. La procedura seguente illustra come determinare il realm per Windows 2003:

   * Fare clic con il pulsante destro del mouse su Risorse del computer e selezionare Proprietà
   * Fare clic sulla scheda Nome computer. Il valore Nome dominio è il nome del realm.

   **utente:** Nome di accesso dell&#39;account utente creato nell&#39;attività precedente. In questo esempio, è impostato su spnegodemo.

Se riscontri questo errore:

```shell
DsCrackNames returned 0x2 in the name entry for spnegodemo.
ktpass:failed getting target domain for specified user.
```

prova a specificare l’utente come spnegodemo@um.lc.com:

```shell
ktpass -princ HTTP/lcserver.um.lc.com@UM.LC.COM -mapuser spnegodemo
```

### Impedisci errori di verifica integrità Kerberos {#prevent-kerberos-integrity-check-failures}

1. Nel controller di dominio passare a Menu Start > Strumenti di amministrazione > Utenti e computer di Active Directory. Se Strumenti di amministrazione non è disponibile nel menu Start, utilizzare il Pannello di controllo Campaign.
1. Fare clic sulla cartella Utenti per visualizzare un elenco di utenti.
1. Fare clic con il pulsante destro del mouse sull&#39;account utente creato in un&#39;attività precedente. In questo esempio, l’account utente è `spnegodemo`.
1. Fare clic su Reimposta password.
1. Digitare e confermare la stessa password digitata in precedenza. In questo esempio, è impostato su `password`.
1. Deselezionare Cambia password all&#39;accesso successivo e quindi fare clic su OK.

### Configurazione delle impostazioni del browser client SPNEGO {#configuring-spnego-client-browser-settings}

Affinché l&#39;autenticazione basata su SPNEGO funzioni, il computer client deve far parte del dominio in cui viene creato l&#39;account utente. È inoltre necessario configurare il browser client per consentire l&#39;autenticazione basata su SPNEGO. Inoltre, il sito che richiede l&#39;autenticazione basata su SPNEGO deve essere attendibile.

Se si accede al server utilizzando il nome del computer, ad esempio https://lcserver:8080, non sono necessarie impostazioni per Internet Explorer. Se si immette un URL che non contiene punti (&quot;.&quot;), Internet Explorer considera il sito come sito Intranet locale. Se si utilizza un nome completo per il sito, è necessario aggiungerlo come sito attendibile.

**Configurare Internet Explorer 6.x**

1. Vai a Strumenti > Opzioni Internet e fai clic sulla scheda Sicurezza.
1. Fare clic sull&#39;icona Intranet locale e quindi su Sites.
1. Fare clic su Avanzate e nella casella Aggiungi il sito Web all&#39;area digitare l&#39;URL del server Forms. Ad esempio, digitare `https://lcserver.um.lc.com`
1. Fare clic su OK fino a quando tutte le finestre di dialogo non vengono chiuse.
1. Verifica la configurazione accedendo all’URL del server AEM Forms. Ad esempio, nella casella URL browser, digita `https://lcserver.um.lc.com:8080/um/login?um_no_redirect=true`

**Configurare Mozilla Firefox**

1. Nella casella URL browser digitare `about:config`

   Viene visualizzata la finestra di dialogo about:config - Mozilla Firefox.

1. Nella casella Filtro digitare `negotiate`
1. Nell&#39;elenco visualizzato fare clic su network.NEGOTIate-auth.trusted-uri e digitare uno dei comandi seguenti in base alle esigenze dell&#39;ambiente:

   `.um.lc.com`: configura Firefox per consentire SPNEGO per qualsiasi URL che termina con um.lc.com. Assicurati di includere il punto (&quot;.&quot;) all&#39;inizio.

   `lcserver.um.lc.com` - Configura Firefox per consentire SPNEGO solo per il tuo server specifico. Non iniziare questo valore con un punto (&quot;.&quot;).

1. Verifica la configurazione accedendo all’applicazione. Viene visualizzata la pagina di benvenuto per l’applicazione di destinazione.
