---
title: Abilitazione del single sign-on nei moduli AEM
seo-title: Abilitazione del single sign-on nei moduli AEM
description: Scopri come abilitare Single Sign-On (SSO) utilizzando intestazioni HTTP e SPNEGO.
seo-description: Scopri come abilitare Single Sign-On (SSO) utilizzando intestazioni HTTP e SPNEGO.
uuid: 2bc08b4f-dcbe-4a16-9025-32fc14605e13
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ee54d9d4-190d-4665-925a-9740ac65fbd5
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1538'
ht-degree: 0%

---


# Abilitazione del single sign-on nei moduli AEM{#enabling-single-sign-on-in-aem-forms}

I moduli AEM forniscono due modi per abilitare Single Sign-On (SSO) - Intestazioni HTTP e SPNEGO.

Quando SSO è implementato, le pagine di accesso utente dei moduli AEM non sono obbligatorie e non vengono visualizzate se l&#39;utente è già autenticato tramite il portale aziendale.

Se i moduli AEM non sono in grado di autenticare un utente utilizzando uno di questi metodi, l&#39;utente viene reindirizzato a una pagina di accesso.

## Abilita SSO mediante intestazioni HTTP {#enable-sso-using-http-headers}

Potete utilizzare la pagina Configurazione portale per abilitare SSO (Single Sign-On) tra le applicazioni e qualsiasi applicazione che supporti la trasmissione dell&#39;identità tramite l&#39;intestazione HTTP. Quando SSO è implementato, le pagine di accesso utente dei moduli AEM non sono obbligatorie e non vengono visualizzate se l&#39;utente è già autenticato tramite il portale aziendale.

È inoltre possibile abilitare SSO utilizzando SPNEGO. Consultate [Abilitare SSO con SPNEGO](enabling-single-sign-on-aem.md#enable-sso-using-spnego).

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Configurazione > Configura attributi del portale.
1. Selezionare Sì per abilitare SSO. Se si seleziona No, le impostazioni rimanenti sulla pagina non sono disponibili.
1. Impostate le altre opzioni sulla pagina come desiderate e fate clic su OK:

   * **Tipo SSO:** (Obbligatorio) Selezionate Intestazione HTTP per abilitare SSO utilizzando le intestazioni HTTP.
   * **Intestazione HTTP per l’identificatore dell’utente:** (Obbligatorio) Nome dell’intestazione il cui valore contiene l’identificatore univoco dell’utente connesso. Gestione utente utilizza questo valore per trovare l&#39;utente nel database Gestione utente. Il valore ottenuto da questa intestazione deve corrispondere all’identificatore univoco dell’utente sincronizzato dalla directory LDAP. Consultate Impostazioni [](/help/forms/using/admin-help/adding-configuring-users.md#user-settings)utente.
   * **Il valore dell’identificatore viene mappato sull’ID utente dell’utente invece dell’identificatore univoco dell’utente:** Mappa il valore dell&#39;identificatore univoco dell&#39;utente all&#39;ID utente. Selezionare questa opzione se l&#39;identificatore univoco dell&#39;utente è un valore binario che non può essere facilmente propagato attraverso le intestazioni HTTP (ad esempio, objectGUID se si sincronizzano gli utenti da Active Directory).
   * **Intestazione HTTP per il dominio:** (Non obbligatorio) Nome dell’intestazione il cui valore contiene il nome del dominio. Utilizzate questa impostazione solo se nessuna singola intestazione HTTP identifica in modo univoco l&#39;utente. Utilizzare questa impostazione per i casi in cui esistono più domini e l&#39;identificatore univoco è univoco solo all&#39;interno di un dominio. In questo caso, specificate il nome dell&#39;intestazione in questa casella di testo e specificate la mappatura del dominio per i più domini nella casella Mappatura dominio. (Vedere [Modifica e conversione di domini](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains)esistenti.)
   * **Mappatura del dominio:** (Obbligatorio) Specifica la mappatura per più domini nel formato *header value=domain name*.

      Ad esempio, si consideri una situazione in cui l’intestazione HTTP di un dominio è domainName e può avere valori di domain1, domain2 o domain3. In questo caso, utilizzate la mappatura del dominio per mappare i valori domainName ai nomi del dominio Gestione utente. Ogni mappatura deve essere su una riga diversa:

      domain1=UMdomain1

      domain2=UMdomain2

      domain3=UMdomain3

### Configurare i referenti consentiti {#configure-allowed-referers}

Per i passaggi per configurare i referenti consentiti, consulta [Configurare i referenti](/help/forms/using/admin-help/preventing-csrf-attacks.md#configure-allowed-referers)consentiti.

## Abilita SSO con SPNEGO {#enable-sso-using-spnego}

È possibile utilizzare il meccanismo di negoziazione GSSAPI semplice e protetto (SPNEGO) per abilitare SSO (Single Sign-On) quando si utilizza Active Directory come server LDAP in un ambiente Windows. Quando SSO è abilitato, le pagine di accesso utente dei moduli AEM non sono obbligatorie e non vengono visualizzate.

È inoltre possibile abilitare SSO utilizzando intestazioni HTTP. Consultate [Abilitare SSO utilizzando intestazioni](enabling-single-sign-on-aem.md#enable-sso-using-http-headers)HTTP.

>[!NOTE]
>
>I AEM Forms su JEE non supportano la configurazione di SSO tramite Kerberos/SPNEGO in ambienti con più domini figlio.

1. Decidete quale dominio utilizzare per abilitare SSO. Il server moduli AEM e gli utenti devono appartenere allo stesso dominio Windows o allo stesso dominio trusted.
1. In Active Directory, creare un utente che rappresenti il server moduli AEM. Consultate [Creare un account](enabling-single-sign-on-aem.md#create-a-user-account)utente. Se state configurando più di un dominio per utilizzare SPNEGO, accertatevi che le password per ciascuno di questi utenti siano diverse. Se le password non sono diverse, SPNEGO SSO non funziona.
1. Mappare il nome dell&#39;entità del servizio. (vedere [Mappare un nome entità servizio (SPN)](enabling-single-sign-on-aem.md#map-a-service-principal-name-spn).)
1. Configurare il controller di dominio. (vedere [Impedire gli errori](enabling-single-sign-on-aem.md#prevent-kerberos-integrity-check-failures)di controllo dell&#39;integrità Kerberos).
1. Aggiungi o modifica un dominio enterprise come descritto in [Aggiunta di domini](/help/forms/using/admin-help/adding-domains.md#adding-domains) o [Modifica e conversione di domini](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains)esistenti. Quando create o modificate il dominio Enterprise, eseguite le seguenti operazioni:

   * Aggiungere o modificare una directory che contiene le informazioni di Active Directory.
   * Aggiungete LDAP come provider di autenticazione.
   * Aggiungi Kerberos come provider di autenticazione. Fornire le seguenti informazioni nella pagina Nuova autenticazione o Modifica autenticazione per Kerberos:

      * **Provider autenticazione:** Kerberos
      * **IP DNS:** L&#39;indirizzo IP DNS del server in cui sono in esecuzione i moduli AEM. È possibile determinare questo indirizzo IP eseguendo `ipconfig/all` la riga di comando.
      * **Host KDC:** Nome host completo o indirizzo IP del server Active Directory utilizzato per l&#39;autenticazione
      * **Utente del servizio:** Il nome dell&#39;entità del servizio (SPN) passato allo strumento KtPass. Nell’esempio precedente, l’utente del servizio è `HTTP/lcserver.um.lc.com`.
      * **Service Realm:** Nome di dominio per Active Directory. Nell&#39;esempio precedente, il nome del dominio è `UM.LC.COM.`
      * **Password del servizio:** Password dell’utente del servizio. Nell’esempio precedente, la password del servizio è `password`.
      * **Abilita SPNEGO:** Abilita l&#39;utilizzo di SPNEGO per Single Sign-On (SSO). Selezionate questa opzione.

1. Configurare le impostazioni del browser del client SPNEGO. Consultate [Configurazione delle impostazioni](enabling-single-sign-on-aem.md#configuring-spnego-client-browser-settings)del browser client SPNEGO.

### Creazione di un account utente {#create-a-user-account}

1. In SPNEGO, registrare un servizio come utente in Active Directory nel controller di dominio per rappresentare i moduli AEM. Nel controller di dominio, scegliere Start Menu > Strumenti di amministrazione > Utenti e computer di Active Directory. Se Strumenti di amministrazione non si trova nel menu Start, usate l’Pannello di controllo Campaign.
1. Fate clic sulla cartella Utenti per visualizzare un elenco di utenti.
1. Fate clic con il pulsante destro del mouse sulla cartella utente e selezionate Nuovo > Utente.
1. Digitate il nome/cognome e il nome di accesso dell’utente, quindi fate clic su Avanti. Ad esempio, impostare i seguenti valori:

   * **Nome**: umspnego
   * **Nome** di accesso utente: spnegozidemo

1. Digitate una password. Ad esempio, impostarlo su *password*. Assicurarsi che la password non scada mai e che non siano selezionate altre opzioni.
1. Fare clic su Avanti, quindi su Fine.

### Mappare un nome entità servizio (SPN) {#map-a-service-principal-name-spn}

1. Ottenete l&#39;utility KtPass. Questa utilità viene utilizzata per mappare un SPN su un REALM. È possibile ottenere l&#39;utility KtPass come parte di Windows Server Tool Pack o Resource Kit. (vedere Strumenti [di supporto di](https://support.microsoft.com/kb/892777)Windows Server 2003 Service Pack 1.)
1. In un prompt dei comandi, eseguire `ktpass` utilizzando gli argomenti seguenti:

   `ktpass -princ HTTP/`*host *`@`*REALM* `-mapuser`*user *

   Ad esempio, digitare il testo seguente:

   `ktpass -princ HTTP/lcserver.um.lc.com@UM.LC.COM -mapuser spnegodemo`

   I valori che dovete fornire sono descritti di seguito:

   **host:** Nome completo del server dei moduli o qualsiasi URL univoco. In questo esempio, è impostata su lcserver.um.lc.com.

   **REALM:** Area di autenticazione di Active Directory per il controller di dominio. In questo esempio, è impostata su UM.LC.COM. Assicurarsi di immettere l&#39;area di autenticazione in caratteri maiuscoli. Per determinare l&#39;area di autenticazione per Windows 2003, completare i seguenti passaggi:

   * Fate clic con il pulsante destro del mouse su Risorse del computer e selezionate Proprietà
   * Fare clic sulla scheda Nome computer. Il valore Nome dominio è il nome dell&#39;area di autenticazione.

   **utente:** Nome di accesso dell’account utente creato nell’attività precedente. In questo esempio, è impostato su spnegozidemo.

Se si verifica questo errore:

```java
DsCrackNames returned 0x2 in the name entry for spnegodemo.
ktpass:failed getting target domain for specified user.
```

provate a specificare l’utente come spnegodemo@um.lc.com:

```java
ktpass -princ HTTP/lcserver.um.lc.com@UM.LC.COM -mapuser spnegodemo
```

### Impedisci errori di controllo dell&#39;integrità Kerberos {#prevent-kerberos-integrity-check-failures}

1. Nel controller di dominio, scegliere Start Menu > Strumenti di amministrazione > Utenti e computer di Active Directory. Se Strumenti di amministrazione non si trova nel menu Start, usate l’Pannello di controllo Campaign.
1. Fate clic sulla cartella Utenti per visualizzare un elenco di utenti.
1. Fare clic con il pulsante destro del mouse sull&#39;account utente creato in un&#39;attività precedente. In questo esempio, l&#39;account utente è `spnegodemo`.
1. Fate clic su Reimposta password.
1. Digitare e confermare la stessa password digitata in precedenza. In questo esempio, è impostato su `password`.
1. Deselezionate Modifica password al successivo accesso, quindi fate clic su OK.

### Configurazione delle impostazioni del browser del client SPNEGO {#configuring-spnego-client-browser-settings}

Affinché l&#39;autenticazione basata su SPNEGO funzioni, il computer client deve far parte del dominio in cui è stato creato l&#39;account utente. Dovete inoltre configurare il browser client per consentire l&#39;autenticazione basata su SPNEGO. Inoltre, il sito che richiede l&#39;autenticazione basata su SPNEGO deve essere un sito affidabile.

Se l&#39;accesso al server avviene utilizzando il nome del computer, ad esempio https://lcserver:8080, non sono necessarie impostazioni per Internet Explorer. Se immettete un URL che non contiene punti (&quot;.&quot;), Internet Explorer considera il sito come sito Intranet locale. Se utilizzate un nome completo per il sito, il sito deve essere aggiunto come sito attendibile.

**Configurare Internet Explorer 6.x**

1. Scegliere Strumenti > Opzioni Internet e fare clic sulla scheda Protezione.
1. Fate clic sull&#39;icona Intranet locale, quindi fate clic su Siti.
1. Fare clic su Avanzate e, nella casella Aggiungi questo sito Web alla zona, digitare l&#39;URL del server moduli. For example, type `https://lcserver.um.lc.com`
1. Fare clic su OK fino a chiudere tutte le finestre di dialogo.
1. Verificare la configurazione accedendo all&#39;URL del server moduli AEM. Ad esempio, nella casella URL del browser, digitare `https://lcserver.um.lc.com:8080/um/login?um_no_redirect=true`

**Configurare Mozilla Firefox**

1. Nella casella URL del browser, digitate `about:config`

   Viene visualizzata la finestra di dialogo about:config - Mozilla Firefox.

1. Nella casella Filtro, digitare `negotiate`
1. Nell&#39;elenco visualizzato, fare clic su network.deal-auth.trusted-uri e digitare uno dei seguenti comandi in base alle esigenze dell&#39;ambiente:

   `.um.lc.com`- Configura Firefox per consentire a SPNEGO qualsiasi URL che termina con um.lc.com. Assicurarsi di includere il punto (&quot;.&quot;) all&#39;inizio.

   `lcserver.um.lc.com` - Configura Firefox per consentire SPNEGO solo per il server specifico. Non iniziare questo valore con un punto (&quot;.&quot;).

1. Verificate la configurazione accedendo all’applicazione. Viene visualizzata la pagina di benvenuto per l’applicazione di destinazione.

