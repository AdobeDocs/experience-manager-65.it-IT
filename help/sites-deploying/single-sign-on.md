---
title: Single Sign On
seo-title: Single Sign On
description: Scopri come configurare Single Sign On (SSO) per un’istanza AEM.
seo-description: Scopri come configurare Single Sign On (SSO) per un’istanza AEM.
uuid: b8dcb28e-4604-4da5-b8dd-4e1e2cbdda18
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring, Security
content-type: reference
discoiquuid: 86e8dc12-608d-4aff-ba7a-5524f6b4eb0d
feature: Configuring
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 0%

---


# Single Sign On {#single-sign-on}

L&#39;accesso Single Sign On (SSO) consente a un utente di accedere a più sistemi dopo aver fornito le credenziali di autenticazione (ad esempio un nome utente e una password) una volta. Un sistema separato (noto come autenticatore affidabile) esegue l&#39;autenticazione e fornisce Experienci Manager con le credenziali utente. Experience Manager controlla e applica le autorizzazioni di accesso per l’utente (ovvero determina a quali risorse l’utente può accedere).

Il servizio SSO Authentication Handler ( `com.adobe.granite.auth.sso.impl.SsoAuthenticationHandler`) elabora i risultati di autenticazione forniti dall&#39;autenticatore affidabile. Il gestore di autenticazione SSO cerca un ssid (SSO Identifier) come valore di un attributo speciale nelle seguenti posizioni in questo ordine:

1. Intestazioni richieste
1. Cookie
1. Parametri di richiesta

Quando viene trovato un valore, la ricerca viene completata e viene utilizzato questo valore.

Configura i due servizi seguenti per riconoscere il nome dell&#39;attributo che memorizza il ssid:

* Modulo di accesso.
* Servizio autenticazione SSO.

È necessario specificare lo stesso nome di attributo per entrambi i servizi. L&#39;attributo è incluso nel `SimpleCredentials` fornito a `Repository.login`. Il valore dell&#39;attributo è irrilevante e ignorato, la sua mera presenza è importante e verificata.

## Configurazione dell&#39;SSO {#configuring-sso}

Per configurare SSO per un&#39;istanza AEM, è necessario configurare [SSO Authentication Handler](/help/sites-deploying/osgi-configuration-settings.md#adobegranitessoauthenticationhandler):

1. Quando si lavora con AEM esistono diversi metodi per gestire le impostazioni di configurazione di tali servizi; per ulteriori dettagli e pratiche consigliate, consulta [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md) .

   Ad esempio, per il set NTLM:

   * **Percorso:** come richiesto; ad esempio,  `/`
   * **Nomi** intestazione:  `LOGON_USER`
   * **Formato** ID:  `^<DOMAIN>\\(.+)$`

      Dove `<*DOMAIN*>` viene sostituito dal tuo nome di dominio.
   Per CoSign:

   * **Percorso:** come richiesto; ad esempio,  `/`
   * **Nomi** intestazione: remote_user
   * **Formato ID:** AsIs

   Per SiteMinder:

   * **Percorso:** come richiesto; ad esempio,  `/`
   * **Nomi delle intestazioni:** SM_USER
   * **Formato** ID: AsIs



1. Verificare che Single Sign On funzioni come necessario; compresa l&#39;autorizzazione.

>[!CAUTION]
>
>Assicurati che gli utenti non possano accedere AEM direttamente se è configurato l&#39;SSO.
>
>Richiedendo agli utenti di passare attraverso un server web che esegue l&#39;agente del sistema SSO, si garantisce che nessun utente possa inviare direttamente un&#39;intestazione, un cookie o un parametro che porterà l&#39;utente ad essere affidabile da AEM, in quanto l&#39;agente filtrerà tali informazioni se inviate dall&#39;esterno.
>
>Qualsiasi utente che può accedere direttamente all’istanza di AEM senza passare attraverso il server web potrà agire come qualsiasi utente inviando l’intestazione, il cookie o il parametro , se i nomi sono noti.
>
>Inoltre, assicurati che per le intestazioni, i cookie e i nomi dei parametri di richiesta, configuri solo quello richiesto per la configurazione SSO.


>[!NOTE]
>
>L&#39;accesso singolo viene spesso utilizzato insieme a [LDAP](/help/sites-administering/ldap-config.md).

>[!NOTE]
>
>Se utilizzi anche [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html) con Microsoft Internet Information Server (IIS), sarà necessaria una configurazione aggiuntiva in:
>
>* `disp_iis.ini`
>* IIS

>
>
In `disp_iis.ini` imposta:
>(consulta [installazione del Dispatcher con Microsoft Internet Information Server](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-install.html#microsoft-internet-information-server) per informazioni complete)
>
>* `servervariables=1` (inoltra le variabili del server IIS come intestazioni della richiesta all&#39;istanza remota)
>* `replaceauthorization=1` (sostituisce qualsiasi intestazione denominata &quot;Autorizzazione&quot; diversa da &quot;Base&quot; con il suo equivalente &quot;Base&quot;)

>
>
In IIS:
>
>* disattiva **Accesso anonimo**
   >
   >
* abilita **autenticazione Windows integrata**

>



Puoi vedere quale gestore di autenticazione viene applicato a qualsiasi sezione della struttura del contenuto utilizzando l&#39;opzione **Autenticatore** della console Felix; ad esempio:

`http://localhost:4502/system/console/slingauth`

Viene prima eseguita una query sul gestore che meglio corrisponde al percorso. Ad esempio, se configuri handler-A per il percorso `/` e handler-B per il percorso `/content`, una richiesta a `/content/mypage.html` eseguirà prima una query su handler-B.

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

* **Nomi** intestazione:  `TestHeader`

* **Nomi** dei cookie:  `TestCookie`

* **Nomi** dei parametri:  `TestParameter`

* **Formato** ID:  `AsIs`

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
>Quando utilizzi il parametro di richiesta in un browser, visualizzerai solo parte del codice HTML, senza CSS. Questo perché tutte le richieste dall’HTML vengono effettuate senza il parametro di richiesta.

## Rimozione dei collegamenti di disconnessione AEM {#removing-aem-sign-out-links}

Quando utilizzi SSO, l’accesso e la disconnessione vengono gestiti esternamente, in modo che AEM propri collegamenti di disconnessione non siano più applicabili e debbano essere rimossi.

Il collegamento di disconnessione nella schermata di benvenuto può essere rimosso utilizzando i seguenti passaggi.

1. Sovrapponi `/libs/cq/core/components/welcome/welcome.jsp` a `/apps/cq/core/components/welcome/welcome.jsp`
1. rimuovi la parte seguente dal jsp.

   `<a href="#" onclick="signout('<%= request.getContextPath() %>');" class="signout"><%= i18n.get("sign out", "welcome screen") %>`

Per rimuovere il collegamento di disconnessione disponibile nel menu personale dell’utente nell’angolo in alto a destra, effettua le seguenti operazioni:

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

