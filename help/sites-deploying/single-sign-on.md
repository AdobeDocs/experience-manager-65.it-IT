---
title: Single Sign-On
description: Scopri come configurare il Single Sign On (SSO) per un’istanza di Adobe Experience Manager (AEM).
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring, Security
content-type: reference
feature: Security
exl-id: 7d2e4620-c3a5-4f5a-9eb6-42a706479d41
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 0%

---

# Single Sign-On {#single-sign-on}

Single Sign-On (SSO) consente a un utente di accedere a più sistemi dopo aver fornito le credenziali di autenticazione, ad esempio un nome utente e una password. L&#39;autenticazione viene eseguita da un sistema separato, denominato autenticatore attendibile, che fornisce agli Experienci Manager le credenziali utente. Experience Manager verifica e applica le autorizzazioni di accesso per l’utente (ovvero, determina quali risorse l’utente può accedere).

Il servizio Gestore autenticazione SSO ( `com.adobe.granite.auth.sso.impl.SsoAuthenticationHandler`) elabora i risultati di autenticazione forniti dall&#39;autenticatore attendibile. Il gestore di autenticazione SSO cerca un identificatore SSO (SSID) come valore di un attributo speciale nelle posizioni seguenti in questo ordine:

1. Intestazioni richiesta
1. Cookie
1. Parametri di richiesta

Quando viene trovato un valore, la ricerca viene completata e questo valore viene utilizzato.

Configura i due servizi seguenti per riconoscere il nome dell&#39;attributo che memorizza l&#39;SSID:

* Il modulo di accesso.
* Il servizio di autenticazione SSO.

Specificare lo stesso nome di attributo per entrambi i servizi. L&#39;attributo è incluso in `SimpleCredentials` fornito a `Repository.login`. Il valore dell’attributo è irrilevante e ignorato, la sua mera presenza è importante e verificata.

## Configurazione dell’SSO {#configuring-sso}

Per configurare SSO per un&#39;istanza AEM, configurare il [Gestore autenticazione SSO](/help/sites-deploying/osgi-configuration-settings.md#adobegranitessoauthenticationhandler):

1. Quando si lavora con AEM, esistono diversi metodi per gestire le impostazioni di configurazione per tali servizi; vedere [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md) per ulteriori dettagli e le procedure consigliate.

   Ad esempio, per il set NTLM:

   * **Percorso:** come richiesto; ad esempio, `/`
   * **Nomi intestazione**: `LOGON_USER`
   * **Formato ID**: `^<DOMAIN>\\(.+)$`

     Dove `<*DOMAIN*>` è sostituito dal nome del tuo dominio.

   Per CoSign:

   * **Percorso:** come richiesto; ad esempio, `/`
   * **Nomi intestazioni**: remote_user
   * **Formato ID:** Così Com&#39;È

   Per SiteMinder:

   * **Percorso:** come richiesto; ad esempio, `/`
   * **Nomi intestazione:** SM_USER
   * **Formato ID**: così com&#39;è

1. Verificare che Single Sign-On funzioni come richiesto, inclusa l&#39;autorizzazione.

>[!CAUTION]
>
>Assicurati che gli utenti non possano accedere direttamente all&#39;AEM se SSO è configurato.
>
>Richiedendo agli utenti di passare attraverso un server web che esegue l&#39;agente del sistema SSO, si garantisce che nessun utente possa inviare direttamente un&#39;intestazione, un cookie o un parametro che porti l&#39;utente ad essere considerato attendibile dall&#39;AEM, in quanto l&#39;agente filtrerà tali informazioni se inviate dall&#39;esterno.
>
>Qualsiasi utente che può accedere direttamente all’istanza AEM senza passare per il server web sarà in grado di agire come qualsiasi altro utente inviando l’intestazione, il cookie o il parametro, se i nomi sono noti.
>
>Inoltre, accertati che tra intestazioni, cookie e nomi di parametri di richiesta sia configurato solo quello necessario per la configurazione SSO.
>

>[!NOTE]
>
>Single Sign-On viene spesso utilizzato con [LDAP](/help/sites-administering/ldap-config.md).

>[!NOTE]
>
>Se si utilizza anche [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=it) con Microsoft® Internet Information Server (IIS), è necessario configurare ulteriormente in:
>
>* `disp_iis.ini`
>* IIS
>
>In `disp_iis.ini` set:
>(per informazioni dettagliate, vedere [installazione di Dispatcher con Microsoft® Internet Information Server](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/dispatcher-install.html?lang=it#microsoft-internet-information-server))
>
>* `servervariables=1` (inoltra le variabili del server IIS come intestazioni di richiesta all&#39;istanza remota)
>* `replaceauthorization=1` (sostituisce qualsiasi intestazione denominata &quot;Authorization&quot; diversa da &quot;Basic&quot; con il suo equivalente &quot;Basic&quot;)
>
>In IIS:
>
>* disabilita **Accesso anonimo**
>
>* abilita **autenticazione integrata di Windows**
>

Puoi vedere quale gestore di autenticazione viene applicato a qualsiasi sezione della struttura del contenuto utilizzando l&#39;opzione **Autenticatore** della console Felix; ad esempio:

`http://localhost:4502/system/console/slingauth`

Viene eseguita prima una query sul gestore che corrisponde meglio al percorso. Ad esempio, se si configura il gestore A per il percorso `/` e il gestore B per il percorso `/content`, una richiesta a `/content/mypage.html` eseguirà prima la query del gestore B.

![schermata_shot_2012-02-15at21006pm](assets/screen_shot_2012-02-15at21006pm.png)

### Esempio {#example}

Per una richiesta di cookie (utilizzando l&#39;URL `http://localhost:4502/libs/wcm/content/siteadmin.html`):

```xml
GET /libs/cq/core/content/welcome.html HTTP/1.1
Host: localhost:4502
Cookie: TestCookie=admin
```

Utilizzando la seguente configurazione:

* **Percorso**: `/`

* **Nomi intestazione**: `TestHeader`

* **Nomi cookie**: `TestCookie`

* **Nomi Parametri**: `TestParameter`

* **Formato ID**: `AsIs`

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

Questo funziona anche se richiedi:
`http://localhost:4502/libs/cq/core/content/welcome.html?TestParameter=admin`

Oppure puoi usare il seguente comando curl per inviare l&#39;intestazione `TestHeader` a `admin:`
`curl -D - -H "TestHeader: admin" http://localhost:4502/libs/cq/core/content/welcome.html`

>[!NOTE]
>
>Quando utilizzi il parametro di richiesta in un browser, vengono visualizzati solo alcuni dei HTML, senza CSS. Questo perché tutte le richieste del HTML vengono effettuate senza il parametro di richiesta.

## Rimozione dei collegamenti di disconnessione AEM {#removing-aem-sign-out-links}

Quando si utilizza l’SSO, l’accesso e la disconnessione vengono gestiti esternamente, pertanto i collegamenti di disconnessione propri dell’AEM non sono più applicabili e devono essere rimossi.

Il collegamento di disconnessione nella schermata di benvenuto può essere rimosso seguendo la procedura riportata di seguito.

1. Sovrapponi `/libs/cq/core/components/welcome/welcome.jsp` a `/apps/cq/core/components/welcome/welcome.jsp`
1. rimuovi la parte seguente da jsp.

   `<a href="#" onclick="signout('<%= request.getContextPath() %>');" class="signout"><%= i18n.get("sign out", "welcome screen") %>`

Per rimuovere il collegamento di disconnessione disponibile nel menu personale dell&#39;utente nell&#39;angolo in alto a destra, eseguire la procedura seguente:

1. Sovrapponi `/libs/cq/ui/widgets/source/widgets/UserInfo.js` a `/apps/cq/ui/widgets/source/widgets/UserInfo.js`

1. Rimuovere la parte seguente dal file:

   ```
   menu.addMenuItem({
       "text":CQ.I18n.getMessage("Sign out"),
       "cls": "cq-userinfo-logout",
       "handler": this.logout
   });
   menu.addSeparator();
   ```
