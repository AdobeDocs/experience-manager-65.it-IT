---
title: Single Sign On
seo-title: Single Sign On
description: Scoprite come configurare Single Sign On (SSO) per un'istanza AEM.
seo-description: Scoprite come configurare Single Sign On (SSO) per un'istanza AEM.
uuid: b8dcb28e-4604-4da5-b8dd-4e1e2cbdda18
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring, Security
content-type: reference
discoiquuid: 86e8dc12-608d-4aff-ba7a-5524f6b4eb0d
translation-type: tm+mt
source-git-commit: 46f2ae565fe4a8cfea49572eb87a489cb5d9ebd7
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 0%

---


# Single Sign On {#single-sign-on}

Single Sign On (SSO) consente a un utente di accedere a più sistemi dopo aver fornito le credenziali di autenticazione (ad esempio un nome utente e una password) una volta. Un sistema separato (noto come autenticatore affidabile) esegue l&#39;autenticazione e fornisce  Experience Manager con le credenziali utente.  Experience Manager verifica e applica le autorizzazioni di accesso per l’utente (ossia determina a quali risorse l’utente può accedere).

Il servizio Gestore autenticazione SSO ( `com.adobe.granite.auth.sso.impl.SsoAuthenticationHandler`) elabora i risultati dell&#39;autenticazione forniti dall&#39;autenticatore affidabile. Il gestore autenticazione SSO cerca in questo ordine un valore ssid (SSO Identifier) come valore di un attributo speciale nelle seguenti posizioni:

1. Richiedi intestazioni
1. Cookie
1. Parametri di richiesta

Quando viene trovato un valore, la ricerca viene completata e viene utilizzato questo valore.

Configurate i due servizi seguenti per riconoscere il nome dell&#39;attributo che memorizza il ssid:

* Modulo di login.
* Servizio autenticazione SSO.

È necessario specificare lo stesso nome attributo per entrambi i servizi. L’attributo è incluso nel `SimpleCredentials` file a cui è stato fornito `Repository.login`. Il valore dell&#39;attributo è irrilevante e ignorato, la sua semplice presenza è importante e verificata.

## Configurazione di SSO {#configuring-sso}

Per configurare SSO per un&#39;istanza AEM, è necessario configurare il gestore [autenticazione](/help/sites-deploying/osgi-configuration-settings.md#adobegranitessoauthenticationhandler)SSO:

1. When working with AEM there are several methods of managing the configuration settings for such services; see [Configuring OSGi](/help/sites-deploying/configuring-osgi.md) for more details and the recommended practices.

   Ad esempio, per i set NTLM:

   * **Percorso:** se necessario; ad esempio, `/`
   * **Nomi** intestazione: `LOGON_USER`
   * **Formato** ID: `^<DOMAIN>\\(.+)$`

      Dove `<*DOMAIN*>` viene sostituito dal proprio nome di dominio.
   Per CoSign:

   * **Percorso:** se necessario; ad esempio, `/`
   * **Nomi** intestazione: remote_user
   * **Formato ID:** AsIs

   Per SiteMinder:

   * **Percorso:** se necessario; ad esempio, `/`
   * **Nomi intestazione:** SM_USER
   * **Formato** ID: AsIs



1. Verificare che Single Sign On funzioni come necessario. compresa l&#39;autorizzazione.

>[!CAUTION]
>
>Assicuratevi che gli utenti non possano accedere AEM direttamente se è configurato SSO.
>
>Richiedendo agli utenti di passare attraverso un server Web che esegue l&#39;agente del sistema SSO, si garantisce che nessun utente possa inviare direttamente un&#39;intestazione, un cookie o un parametro che induca l&#39;utente ad essere fidato da AEM, in quanto l&#39;agente filtrerà tali informazioni se inviate dall&#39;esterno.
>
>Ogni utente che può accedere direttamente all’istanza AEM senza passare attraverso il server Web sarà in grado di agire come qualsiasi utente inviando l’intestazione, il cookie o il parametro, se i nomi sono noti.
>
>Inoltre, accertatevi che per le intestazioni, i cookie e i nomi dei parametri di richiesta, sia configurato solo quello richiesto per la configurazione SSO.


>[!NOTE]
>
>Single Sign On è spesso utilizzato insieme a [LDAP](/help/sites-administering/ldap-config.md).

>[!NOTE]
>
>Se si utilizza anche il [dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html) con Microsoft Internet Information Server (IIS), sarà necessaria una configurazione aggiuntiva in:
>
>* `disp_iis.ini`
>* IIS

>
>
Nel `disp_iis.ini` set:
>(consultate [Installazione del dispatcher con Microsoft Internet Information Server](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-install.html#microsoft-internet-information-server) per ulteriori dettagli)
>
>* `servervariables=1` (inoltra le variabili del server IIS come intestazioni di richiesta all&#39;istanza remota)
>* `replaceauthorization=1` (sostituisce qualsiasi intestazione denominata &quot;Autorizzazione&quot; diversa da &quot;Base&quot; con il suo equivalente &quot;Base&quot;)

>
>
In IIS:
>
>* disattiva accesso **anonimo**
   >
   >
* abilita autenticazione **integrata di Windows**

>



Potete vedere quale gestore di autenticazione viene applicato a qualsiasi sezione della struttura del contenuto utilizzando l&#39;opzione **Autenticatore** della console Flash; ad esempio:

`http://localhost:4502/system/console/slingauth`

Viene eseguito innanzitutto un query sul gestore che meglio corrisponde al percorso. Ad esempio, se si configura handler-A per il percorso `/` e handler-B per il percorso `/content`, prima una richiesta a `/content/mypage.html` eseguirà query su handler-B.

![screen_shot_2012-02-15at21006pm](assets/screen_shot_2012-02-15at21006pm.png)

### Esempio {#example}

Per una richiesta di cookie (utilizzando l’URL `http://localhost:4502/libs/wcm/content/siteadmin.html`):

```xml
GET /libs/cq/core/content/welcome.html HTTP/1.1
Host: localhost:4502
Cookie: TestCookie=admin
```

Utilizzando la configurazione seguente:

* **Percorso**: `/`

* **Nomi** intestazione: `TestHeader`

* **Nomi** cookie: `TestCookie`

* **Nomi** dei parametri: `TestParameter`

* **Formato** ID: `AsIs`

La risposta sarebbe:

```xml
HTTP/1.1 200 OK
Connection: Keep-Alive
Server: Day-Servlet-Engine/4.1.24
Content-Type: text/html;charset=utf-8
Date: Thu, 23 Aug 2012 09:58:39 GMT
Transfer-Encoding: chunked

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "https://www.w3.org/TR/html4/strict.dtd">
<html>
<head>
    <meta http-equiv="content-type" content="text/html; charset=UTF-8">
    <title>Welcome to Adobe&reg; CQ5</title>
....
```

Questo funziona anche se richiedete:
`http://localhost:4502/libs/cq/core/content/welcome.html?TestParameter=admin`

Oppure potete usare il seguente comando curl per inviare l’ `TestHeader` intestazione a `admin:`
`curl -D - -H "TestHeader: admin" http://localhost:4502/libs/cq/core/content/welcome.html`

>[!NOTE]
>
>Quando si utilizza il parametro request in un browser, viene visualizzato solo parte del codice HTML, senza CSS. Questo perché tutte le richieste dall’HTML vengono effettuate senza il parametro request.

## Rimozione AEM collegamenti Disconnetti {#removing-aem-sign-out-links}

Quando si utilizza SSO, l&#39;accesso e la disconnessione vengono gestiti esternamente, in modo che AEM propri collegamenti di disconnessione non siano più applicabili e debbano essere rimossi.

Il collegamento di disconnessione nella schermata di benvenuto può essere rimosso tramite la procedura seguente.

1. Sovrapposizione `/libs/cq/core/components/welcome/welcome.jsp` a `/apps/cq/core/components/welcome/welcome.jsp`
1. rimuovere la parte seguente dal jsp.

   `<a href="#" onclick="signout('<%= request.getContextPath() %>');" class="signout"><%= i18n.get("sign out", "welcome screen") %>`

Per rimuovere il collegamento di disconnessione disponibile nel menu personale dell&#39;utente, nell&#39;angolo superiore destro, effettuate le seguenti operazioni:

1. Sovrapposizione `/libs/cq/ui/widgets/source/widgets/UserInfo.js` a `/apps/cq/ui/widgets/source/widgets/UserInfo.js`

1. Rimuovere la parte seguente dal file:

   ```
   menu.addMenuItem({
       "text":CQ.I18n.getMessage("Sign out"),
       "cls": "cq-userinfo-logout",
       "handler": this.logout
   });
   menu.addSeparator();
   ```

