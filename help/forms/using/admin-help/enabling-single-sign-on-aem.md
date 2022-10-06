---
title: Abilitazione del single sign-on nei moduli AEM
seo-title: Enabling single sign-on in AEM forms
description: Scopri come abilitare Single Sign-On (SSO) utilizzando intestazioni HTTP e SPNEGO.
seo-description: Learn how to enable single sign-on (SSO) using HTTP headers and SPNEGO.
uuid: 2bc08b4f-dcbe-4a16-9025-32fc14605e13
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ee54d9d4-190d-4665-925a-9740ac65fbd5
exl-id: 89561ed0-d094-4ef7-9bc1-bde11f3c5bc3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1520'
ht-degree: 0%

---

# Abilitazione del single sign-on nei moduli AEM{#enabling-single-sign-on-in-aem-forms}

AEM forms offre due modi per abilitare Single Sign-On (SSO): intestazioni HTTP e SPNEGO.

Quando l’SSO è implementato, le pagine di accesso utente dei moduli di AEM non sono necessarie e non vengono visualizzate se l’utente è già autenticato tramite il portale aziendale.

Se AEM moduli non sono in grado di autenticare un utente utilizzando uno di questi metodi, l’utente viene reindirizzato a una pagina di accesso.

## Abilita SSO utilizzando intestazioni HTTP {#enable-sso-using-http-headers}

Puoi utilizzare la pagina Configurazione portale per abilitare l’accesso single sign-on (SSO) tra le applicazioni e qualsiasi applicazione che supporta la trasmissione dell’identità tramite l’intestazione HTTP. Quando l’SSO è implementato, le pagine di accesso utente dei moduli di AEM non sono necessarie e non vengono visualizzate se l’utente è già autenticato tramite il portale aziendale.

È inoltre possibile abilitare SSO utilizzando SPNEGO. (Vedi [Abilitare SSO con SPNEGO](enabling-single-sign-on-aem.md#enable-sso-using-spnego).)

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Configurazione > Configura attributi del portale.
1. Selezionare Sì per abilitare SSO. Se si seleziona No, le impostazioni rimanenti nella pagina non saranno disponibili.
1. Imposta le opzioni rimanenti sulla pagina come richiesto e fai clic su OK:

   * **Tipo SSO:** (Obbligatorio) Seleziona Intestazione HTTP per abilitare SSO utilizzando le intestazioni HTTP.
   * **Intestazione HTTP per l’identificatore dell’utente:** (Obbligatorio) Nome dell&#39;intestazione il cui valore contiene l&#39;identificatore univoco dell&#39;utente connesso. User Management utilizza questo valore per trovare l&#39;utente nel database User Management. Il valore ottenuto da questa intestazione deve corrispondere all&#39;identificatore univoco dell&#39;utente sincronizzato dalla directory LDAP. (Vedi [Impostazioni utente](/help/forms/using/admin-help/adding-configuring-users.md#user-settings).)
   * **Il valore dell’identificatore è associato all’ID utente dell’utente al posto dell’identificatore univoco dell’utente:** Mappa il valore dell&#39;identificatore univoco dell&#39;utente sull&#39;ID utente. Selezionare questa opzione se l’identificatore univoco dell’utente è un valore binario che non può essere facilmente propagato tramite intestazioni HTTP (ad esempio, objectGUID se si sincronizzano gli utenti da Active Directory).
   * **Intestazione HTTP per il dominio:** (Non obbligatorio) Nome dell’intestazione il cui valore contiene il nome di dominio. Utilizza questa impostazione solo se nessuna singola intestazione HTTP identifica l’utente in modo univoco. Utilizza questa impostazione per i casi in cui esistono più domini e l’identificatore univoco è univoco solo all’interno di un dominio. In questo caso, specifica il nome dell’intestazione in questa casella di testo e specifica la mappatura del dominio per i più domini nella casella Mapping dominio. (Vedi [Modifica e conversione di domini esistenti](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains).)
   * **Mappatura del dominio:** (Obbligatorio) Specifica la mappatura per più domini nel formato *valore header=nome di dominio*.

      Ad esempio, considera una situazione in cui l’intestazione HTTP per un dominio è domainName e può avere valori di domain1, domain2 o domain3. In questo caso, utilizza la mappatura del dominio per mappare i valori domainName ai nomi di dominio User Management. Ogni mappatura deve trovarsi su una riga diversa:

      domain1=UMdomain1

      domain2=UMdomain2

      domain3=UMdomain3

### Configurare i referenti consentiti {#configure-allowed-referers}

Per i passaggi per configurare i referenti consentiti, vedi [Configurare i referenti consentiti](/help/forms/using/admin-help/preventing-csrf-attacks.md#configure-allowed-referers).

## Abilitare SSO con SPNEGO {#enable-sso-using-spnego}

È possibile utilizzare il meccanismo di negoziazione GSSAPI semplice e protetto (SPNEGO) per abilitare il single sign-on (SSO) quando si utilizza Active Directory come server LDAP in un ambiente Windows. Quando l’SSO è abilitato, le pagine di accesso utente ai moduli di AEM non sono richieste e non vengono visualizzate.

Puoi anche abilitare SSO utilizzando intestazioni HTTP. (Vedi [Abilita SSO utilizzando intestazioni HTTP](enabling-single-sign-on-aem.md#enable-sso-using-http-headers).)

>[!NOTE]
>
>AEM Forms su JEE non supporta la configurazione di SSO utilizzando Kerberos/SPNEGO in ambienti di dominio figlio multipli .

1. Decidi quale dominio utilizzare per abilitare SSO. Il server AEM forms e gli utenti devono far parte dello stesso dominio Windows o dello stesso dominio trusted.
1. In Active Directory, creare un utente che rappresenti il server moduli AEM. (Vedi [Creare un account utente](enabling-single-sign-on-aem.md#create-a-user-account).) Se stai configurando più di un dominio per utilizzare SPNEGO, assicurati che le password per ciascuno di questi utenti siano diverse. Se le password non sono diverse, SPNEGO SSO non funziona.
1. Mappa il nome dell&#39;entità del servizio. (Vedi [Mappare un nome entità servizio (SPN)](enabling-single-sign-on-aem.md#map-a-service-principal-name-spn).)
1. Configura il controller di dominio. (Vedi [Impedisci errori di controllo dell&#39;integrità Kerberos](enabling-single-sign-on-aem.md#prevent-kerberos-integrity-check-failures).)
1. Aggiungi o modifica un dominio enterprise come descritto in [Aggiunta di domini](/help/forms/using/admin-help/adding-domains.md#adding-domains) o [Modifica e conversione di domini esistenti](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains). Quando si crea o si modifica il dominio enterprise, eseguire le operazioni seguenti:

   * Aggiungere o modificare una directory contenente le informazioni di Active Directory.
   * Aggiungi LDAP come provider di autenticazione.
   * Aggiungi Kerberos come provider di autenticazione. Fornire le seguenti informazioni nella pagina Nuova o Modifica autenticazione per Kerberos:

      * **Provider di autenticazione:** Kerberos
      * **IP DNS:** Indirizzo IP DNS del server in cui sono in esecuzione i moduli AEM. Puoi determinare questo indirizzo IP eseguendo `ipconfig/all` sulla riga di comando.
      * **Host KDC:** Nome host completo o indirizzo IP del server Active Directory utilizzato per l&#39;autenticazione
      * **Utente del servizio:** Il nome dell&#39;entità servizio (SPN) passato allo strumento KtPass. Nell’esempio precedente, l’utente del servizio è `HTTP/lcserver.um.lc.com`.
      * **Realm di servizio:** Nome di dominio per Active Directory. Nell’esempio utilizzato in precedenza, il nome del dominio è `UM.LC.COM.`
      * **Password servizio:** Password dell’utente del servizio. Nell’esempio precedente, la password del servizio è `password`.
      * **Abilita SPNEGO:** Abilita l&#39;utilizzo di SPNEGO per il single sign-on (SSO). Seleziona questa opzione.

1. Configura le impostazioni del browser client SPNEGO. (Vedi [Configurazione delle impostazioni del browser client SPNEGO](enabling-single-sign-on-aem.md#configuring-spnego-client-browser-settings).)

### Creare un account utente {#create-a-user-account}

1. In SPNEGO, registrare un servizio come utente in Active Directory nel controller di dominio per rappresentare i moduli AEM. Nel controller di dominio, selezionare Menu Start > Strumenti di amministrazione > Utenti e computer di Active Directory. Se Strumenti di amministrazione non è presente nel menu Start, utilizzare il Pannello di controllo Campaign.
1. Fai clic sulla cartella Utenti per visualizzare un elenco di utenti.
1. Fare clic con il pulsante destro del mouse sulla cartella utente e selezionare Nuovo > Utente.
1. Digitare il nome/cognome e il nome di accesso utente e quindi fare clic su Avanti. Ad esempio, imposta i seguenti valori:

   * **Nome**: umspnego
   * **Nome accesso utente**: smermo

1. Digita una password. Ad esempio, impostalo su *password*. Assicurati che Password Never Expires sia selezionato e che non siano selezionate altre opzioni.
1. Fare clic su Avanti e quindi su Fine.

### Mappare un nome entità servizio (SPN) {#map-a-service-principal-name-spn}

1. Ottieni l&#39;utilità KtPass. Questa utility viene utilizzata per mappare un SPN su un REALM. È possibile ottenere l&#39;utility KtPass come parte del Tool pack o del Resource Kit di Windows Server. (Vedi [Strumenti di supporto per Windows Server 2003 Service Pack 1](https://support.microsoft.com/kb/892777).)
1. Al prompt dei comandi, eseguire `ktpass` utilizzando i seguenti argomenti:

   `ktpass -princ HTTP/`*host* `@`*REALM* `-mapuser`*user*

   Ad esempio, digitare il testo seguente:

   `ktpass -princ HTTP/lcserver.um.lc.com@UM.LC.COM -mapuser spnegodemo`

   I valori da specificare sono descritti come segue:

   **host:** Nome completo del server dei moduli o di qualsiasi URL univoco. In questo esempio, è impostato su lcserver.um.lc.com.

   **REALM:** Il realm di Active Directory per il controller di dominio. In questo esempio, è impostato su UM.LC.COM. Assicurati di inserire il realm in caratteri maiuscoli. Per determinare l&#39;area di autenticazione per Windows 2003, completare i seguenti passaggi:

   * Fare clic con il pulsante destro del mouse su Risorse del computer e selezionare Proprietà
   * Fare clic sulla scheda Nome computer. Il valore Nome di dominio è il nome del realm.

   **utente:** Nome di accesso dell&#39;account utente creato nell&#39;attività precedente. In questo esempio, è impostato su sptrading demo.

Se si verifica questo errore:

```shell
DsCrackNames returned 0x2 in the name entry for spnegodemo.
ktpass:failed getting target domain for specified user.
```

prova a specificare l’utente come spnegodemo@um.lc.com:

```shell
ktpass -princ HTTP/lcserver.um.lc.com@UM.LC.COM -mapuser spnegodemo
```

### Impedisci errori di controllo dell&#39;integrità Kerberos {#prevent-kerberos-integrity-check-failures}

1. Nel controller di dominio, selezionare Menu Start > Strumenti di amministrazione > Utenti e computer di Active Directory. Se Strumenti di amministrazione non è presente nel menu Start, utilizzare il Pannello di controllo Campaign.
1. Fai clic sulla cartella Utenti per visualizzare un elenco di utenti.
1. Fare clic con il pulsante destro del mouse sull&#39;account utente creato in un&#39;attività precedente. In questo esempio, l’account utente è `spnegodemo`.
1. Fare clic su Ripristina password.
1. Digitare e confermare la stessa password digitata in precedenza. In questo esempio, è impostato su `password`.
1. Deselezionare Cambia password al successivo accesso, quindi fare clic su OK.

### Configurazione delle impostazioni del browser client SPNEGO {#configuring-spnego-client-browser-settings}

Affinché l&#39;autenticazione basata su SPNEGO funzioni, il computer client deve far parte del dominio in cui viene creato l&#39;account utente. È inoltre necessario configurare il browser client per consentire l’autenticazione basata su SPNEGO. Inoltre, il sito che richiede l&#39;autenticazione basata su SPNEGO deve essere un sito attendibile.

Se l&#39;accesso al server viene effettuato utilizzando il nome del computer, ad esempio https://lcserver:8080, non sono necessarie impostazioni per Internet Explorer. Se si immette un URL che non contiene punti (&quot;.&quot;), Internet Explorer considera il sito come sito Intranet locale. Se utilizzi un nome completo per il sito, il sito deve essere aggiunto come sito attendibile.

**Configurare Internet Explorer 6.x**

1. Selezionare Strumenti > Opzioni Internet e fare clic sulla scheda Protezione.
1. Fare clic sull&#39;icona Intranet locale e quindi su Siti.
1. Fare clic su Avanzate e, nella casella Aggiungi sito Web alla zona, digitare l’URL del server dei moduli. Ad esempio, digitare `https://lcserver.um.lc.com`
1. Fare clic su OK finché tutte le finestre di dialogo non vengono chiuse.
1. Verifica la configurazione accedendo all’URL del server dei moduli AEM. Ad esempio, nella casella URL browser, digita `https://lcserver.um.lc.com:8080/um/login?um_no_redirect=true`

**Configurazione Mozilla Firefox**

1. Nella casella URL del browser, digita `about:config`

   Viene visualizzata la finestra di dialogo about:config - Mozilla Firefox.

1. Nella casella Filtro digitare `negotiate`
1. Nell&#39;elenco visualizzato, fare clic su network.Negoti-auth.trusted-uri e digitare uno dei seguenti comandi in base alle esigenze dell&#39;ambiente:

   `.um.lc.com`- Configura Firefox per consentire a SPNEGO di trovare qualsiasi URL che termina con um.lc.com. Accertati di includere il punto (&quot;.&quot;) all&#39;inizio.

   `lcserver.um.lc.com` - Configura Firefox per consentire SPNEGO solo per il server specifico. Non iniziare questo valore con un punto (&quot;.&quot;).

1. Verifica la configurazione accedendo all’applicazione. Viene visualizzata la pagina di benvenuto per l’applicazione di destinazione.
