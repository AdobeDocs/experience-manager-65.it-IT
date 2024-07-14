---
title: Configurazione delle notifiche e-mail
description: Scopri come configurare le notifiche e-mail in Adobe Experience Manager.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: 918fcbbc-a78a-4fab-a933-f183ce6a907f
solution: Experience Manager, Experience Manager Sites
feature: Configuring
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '2037'
ht-degree: 9%

---


# Configurazione delle notifiche e-mail{#configuring-email-notification}

AEM invia notifiche e-mail agli utenti che:

* Si sono abbonati a eventi di pagina, ad esempio modifiche o repliche. La sezione [Casella in entrata notifiche](/help/sites-classic-ui-authoring/author-env-inbox.md#subscribing-to-notifications) descrive come sottoscrivere tali eventi.

* Ti sei iscritto agli eventi del forum.
* Devi eseguire un passaggio in un flusso di lavoro. La sezione [Passaggio partecipante](/help/sites-developing/workflows-step-ref.md#participant-step) descrive come attivare la notifica e-mail in un flusso di lavoro.

Prerequisiti:

* Gli utenti devono avere un indirizzo e-mail valido definito nel loro profilo.
* Il servizio di posta CQ **Day** deve essere configurato correttamente.

Quando un utente riceve una notifica, riceve un’e-mail nella lingua definita nel suo profilo. Ogni lingua ha un proprio modello che può essere personalizzato. È possibile aggiungere nuovi modelli e-mail per le nuove lingue.

>[!NOTE]
>
>Quando si lavora con AEM, esistono diversi metodi per gestire le impostazioni di configurazione per tali servizi; vedere [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md) per ulteriori dettagli e le procedure consigliate.

## Configurazione del servizio e-mail {#configuring-the-mail-service}

Affinché l&#39;AEM possa inviare e-mail, è necessario configurare correttamente il servizio di posta CQ **Day**. Puoi visualizzare la configurazione nella console Web. Quando si lavora con AEM, esistono diversi metodi per gestire le impostazioni di configurazione per tali servizi; vedere [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md) per ulteriori dettagli e le procedure consigliate.

Si applicano i seguenti vincoli:

* La **porta del server SMTP** deve essere 25 o superiore.

* Il nome host del server SMTP **** non può essere vuoto.
* L&#39;indirizzo **&quot;Da&quot;** non può essere vuoto.

Per aiutarti a eseguire il debug di un problema relativo al servizio di posta **Day CQ**, puoi visualizzare i registri del servizio:

`com.day.cq.mailer.DefaultMailService`

Nella console Web la configurazione si presenta come segue:

![Finestra di configurazione OSGi Day CQ Mail Service](assets/chlimage_1-276.png)

## Configurazione del canale di notifica e-mail {#configuring-the-email-notification-channel}

Quando ci si abbona alle notifiche degli eventi di pagina o forum, l&#39;indirizzo e-mail da è impostato su `no-reply@acme.com` per impostazione predefinita. È possibile modificare questo valore configurando il servizio **Canale e-mail di notifica** nella console Web.

Per configurare l&#39;indirizzo di posta elettronica da, aggiungere un nodo `sling:OsgiConfig` all&#39;archivio. Per aggiungere il nodo direttamente utilizzando CRXDE Lite, attenersi alla procedura descritta di seguito.

1. In CRXDE Lite, aggiungi una cartella denominata `config` sotto la cartella dell&#39;applicazione.
1. Nella cartella di configurazione, aggiungi un nodo denominato:

   `com.day.cq.wcm.notification.email.impl.EmailChannel` di tipo `sling:OsgiConfig`

1. Aggiungere una proprietà `String` al nodo denominato `email.from`. Per il valore, specifica l’indirizzo e-mail che desideri utilizzare.

1. Fare clic su **Salva tutto**.

Per definire il nodo nelle cartelle di origine dei pacchetti di contenuti, attenersi alla procedura descritta di seguito.

1. In `jcr_root/apps/*app_name*/config folder`, crea un file denominato `com.day.cq.wcm.notification.email.impl.EmailChannel.xml`

1. Aggiungi il seguente XML per rappresentare il nodo:

   `<?xml version="1.0" encoding="UTF-8"?> <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0" jcr:primaryType="sling:OsgiConfig" email.from="name@server.com"/>`
1. Sostituisci il valore dell&#39;attributo `email.from` ( `name@server.com`) con il tuo indirizzo e-mail.

1. Salva il file.

## Configurazione del servizio di notifica e-mail del flusso di lavoro {#configuring-the-workflow-email-notification-service}

Quando ricevi le notifiche e-mail del flusso di lavoro, sia l’indirizzo e-mail da che il prefisso dell’URL host vengono impostati sui valori predefiniti. È possibile modificare questi valori configurando il servizio di notifica e-mail del flusso di lavoro CQ **Day** nella console Web. In tal caso, si consiglia di mantenere la modifica nell’archivio.

Nella console Web la configurazione predefinita è la seguente:

![Finestra di configurazione del servizio di notifica e-mail del flusso di lavoro Day CQ](assets/chlimage_1-277.png)

### Modelli e-mail per notifica pagina {#email-templates-for-page-notification}

I modelli e-mail per le notifiche di pagina si trovano qui sotto:

`/libs/settings/notification-templates/com.day.cq.wcm.core.page`

Il modello inglese predefinito ( `en.txt`) è definito come segue:

```xml
subject=[CQ Page Event Notification]: Page Event

header=-------------------------------------------------------------------------------------\n \
Time: ${time}\n \
User: ${userFullName} (${userId})\n \
-------------------------------------------------------------------------------------\n\n

message=The following pages were affected by the event: \n \
 \n \
${modifications} \n \
 \n\n
footer=\n \
-------------------------------------------------------------------------------------\n \
This is an automatically generated message. Please do not reply.
```

#### Personalizzazione dei modelli e-mail per le notifiche di pagina {#customizing-email-templates-for-page-notification}

Per personalizzare il modello e-mail inglese per la notifica della pagina:

1. In CRXDE, apri il file:

   `/libs/settings/notification-templates/com.day.cq.wcm.core.page/en.txt`

1. Modifica il file in base alle tue esigenze.
1. Salva le modifiche.

Il modello deve avere il seguente formato:

```
 subject=<text_1>
 header=<text_2>
 message=<text_3>
 footer=<text_4>
```

Dove &lt;text_x> può essere una combinazione di testo statico e variabili di stringa dinamiche. Le seguenti variabili possono essere utilizzate all’interno del modello e-mail per le notifiche di pagina:

* `${time}`, data e ora dell&#39;evento.

* `${userFullName}`, nome completo dell&#39;utente che ha attivato l&#39;evento.

* `${userId}`, ID dell&#39;utente che ha attivato l&#39;evento.
* `${modifications}`, descrive il tipo di evento di pagina e il percorso della pagina nel formato:

  &lt;tipo evento pagina> => &lt;percorso pagina>

  Ad esempio:

  PageModified => /content/geometrixx/en/products

### Modelli e-mail per notifica flusso di lavoro {#email-templates-for-workflow-notification}

Il modello e-mail per le notifiche del flusso di lavoro (inglese) si trova in:

`/libs/settings/workflow/notification/email/default/en.txt`

È definito come segue:

```xml
subject=Workflow notification: ${event.EventType}

header=-------------------------------------------------------------------------------------\n \
Time: ${event.TimeStamp}\n \
Step: ${item.node.title}\n \
User: ${participant.name} (${participant.id})\n \
Workflow: ${model.title}\n \
-------------------------------------------------------------------------------------\n\n

message=Content: ${host.prefix}${payload.path.open}\n

footer=\n \
-------------------------------------------------------------------------------------\n \
View the overview in your ${host.prefix}/aem/inbox\n \
-------------------------------------------------------------------------------------\n \
This is an automatically generated message. Please do not reply.
```

#### Personalizzazione dei modelli e-mail per le notifiche del flusso di lavoro {#customizing-email-templates-for-workflow-notification}

Per personalizzare il modello e-mail inglese per la notifica degli eventi del flusso di lavoro:

1. In CRXDE, apri il file:

   `/libs/settings/workflow/notification/email/default/en.txt`

1. Modifica il file in base alle tue esigenze.
1. Salva le modifiche.

Il modello deve avere il seguente formato:

```
subject=<text_1>
 header=<text_2>
 message=<text_3>
 footer=<text_4>
```

>[!NOTE]
>
>Dove `<text_x>` può essere una combinazione di testo statico e variabili di stringa dinamiche. Ogni riga di un elemento `<text_x>` deve terminare con una barra rovesciata ( `\`), tranne per l&#39;ultima istanza, quando l&#39;assenza della barra rovesciata indica la fine della variabile stringa `<text_x>`.
>
>Ulteriori informazioni sul formato del modello sono disponibili nei [javadocs del metodo Properties.load()](https://docs.oracle.com/javase/8/docs/api/java/util/Properties.html#load-java.io.InputStream-).

Il metodo `${payload.path.open}` rivela il percorso del payload dell&#39;elemento di lavoro. Ad esempio, per una pagina in Sites, `payload.path.open` sarebbe simile a `/bin/wcmcommand?cmd=open&path=…`.; questo senza il nome del server, motivo per cui il modello lo precede con `${host.prefix}`.

Le seguenti variabili possono essere utilizzate all’interno del modello e-mail:

* `${event.EventType}`, tipo di evento
* `${event.TimeStamp}`, data e ora dell&#39;evento
* `${event.User}`, l&#39;utente che ha attivato l&#39;evento
* `${initiator.home}`, il percorso del nodo iniziatore

* `${initiator.name}`, nome iniziatore

* `${initiator.email}`, indirizzo e-mail dell&#39;iniziatore
* `${item.id}`, ID dell&#39;elemento di lavoro
* `${item.node.id}`, ID del nodo nel modello di flusso di lavoro associato a questo elemento di lavoro
* `${item.node.title}`, titolo dell&#39;elemento di lavoro
* `${participant.email}`, indirizzo e-mail del partecipante
* `${participant.name}`, nome del partecipante
* `${participant.familyName}`, cognome del partecipante
* `${participant.id}`, ID del partecipante
* `${participant.language}`, lingua del partecipante
* `${instance.id}`, ID del flusso di lavoro
* `${instance.state}`, lo stato del flusso di lavoro
* `${model.title}`, titolo del modello di flusso di lavoro
* `${model.id}`, ID del modello di flusso di lavoro

* `${model.version}`, versione del modello di flusso di lavoro
* `${payload.data}`, il payload

* `${payload.type}`, il tipo di payload
* `${payload.path}`, percorso del payload
* `${host.prefix}`, prefisso host, ad esempio: `http://localhost:4502`

### Aggiunta di un modello e-mail per una nuova lingua {#adding-an-email-template-for-a-new-language}

Per aggiungere un modello per una nuova lingua:

1. In CRXDE, aggiungere un file `<language-code>.txt` di seguito:

   * `/libs/settings/notification-templates/com.day.cq.wcm.core.page` : per le notifiche pagina
   * `/libs/settings/workflow/notification/email/default` : per le notifiche del flusso di lavoro

1. Adattare il file alla lingua.
1. Salva le modifiche.

>[!NOTE]
>
>`<language-code>` utilizzato come nome file per il modello e-mail deve essere un codice di lingua in minuscolo di due lettere riconosciuto dall&#39;AEM. Per i codici di lingua, l&#39;AEM si basa sullo standard ISO-639-1.

## Configurazione delle notifiche e-mail di AEM Assets {#assetsconfig}

Quando le raccolte in AEM Assets sono condivise o non condivise, gli utenti possono ricevere notifiche e-mail dall’AEM. Per configurare le notifiche e-mail, segui la procedura riportata di seguito.

1. Configurare il servizio di posta elettronica come descritto in precedenza in [Configurazione del servizio di posta](/help/sites-administering/notification.md#configuring-the-mail-service).
1. Accedi all’AEM come amministratore. Fai clic su **Strumenti** > **Operazioni** > **Console Web** per aprire Configurazione console Web.
1. Modifica **giorno CQ DAM Resource Collection Servlet**. Seleziona **invia e-mail**. Fai clic su **Salva**.

## Configurazione di OAuth {#setting-up-oauth}

AEM offre il supporto OAuth2 per il suo servizio Mailer integrato, per consentire alle organizzazioni di rispettare i requisiti e-mail sicuri.

Puoi configurare OAuth per più provider di posta elettronica, come descritto di seguito.

>[!NOTE]
>
>Questa procedura è un esempio per un’istanza di Publish. Se desideri abilitare le notifiche e-mail su un’istanza Autore, segui gli stessi passaggi anche sull’Autore.

### Gmail {#gmail}

1. Crea il progetto in `https://console.developers.google.com/projectcreate`
1. Seleziona il progetto, quindi vai a **API e servizi** - **Dashboard - Credenziali**
1. Configurare la schermata di consenso OAuth in base alle tue esigenze
1. Nella schermata di aggiornamento seguente, aggiungi questi due ambiti:
   * `https://mail.google.com/`
   * `https://www.googleapis.com//auth/gmail.send`
1. Dopo aver aggiunto gli ambiti, torna a **Credenziali** nel menu a sinistra, quindi vai a **Crea credenziali** - **ID client OAuth** - **App desktop**
1. Viene visualizzata una nuova finestra contenente l’ID client e il segreto client.
1. Salva queste credenziali.

**Configurazioni lato AEM**

>[!NOTE]
>
>I clienti Adobe Managed Service possono collaborare con il proprio tecnico dell’assistenza clienti per apportare queste modifiche agli ambienti di produzione.

Innanzitutto, configura il servizio di posta:

1. Aprire la console Web AEM accedendo a `http://serveraddress:serverport/system/console/configMgr`
1. Cerca, quindi fai clic su **Day CQ Mail Service**
1. Aggiungi le seguenti impostazioni:
   * Nome host server SMTP: `smtp.gmail.com`
   * Porta del server SMTP: `25` o `587`, a seconda dei requisiti
   * Seleziona le caselle di spunta per **SMPT usa StarTLS** e **SMTP richiede StarTLS**
   * Controlla **Flusso OAuth** e fai clic su **Salva**.

Quindi, configura il provider OAuth SMTP seguendo la procedura seguente:

1. Aprire la console Web AEM accedendo a `http://serveraddress:serverport/system/console/configMgr`
1. Cerca, quindi fai clic su **Provider SMTP OAuth2 CQ Mailer**
1. Compila le informazioni richieste come segue:
   * URL autorizzazione: `https://accounts.google.com/o/oauth2/auth`
   * URL token: `https://accounts.google.com/o/oauth2/token`
   * Ambiti: `https://www.googleapis.com/auth/gmail.send` e `https://mail.google.com/`. È possibile aggiungere più ambiti premendo il pulsante **+** sul lato destro di ogni ambito configurato.
   * ID client e Segreto client: configura questi campi con i valori recuperati come descritto nel paragrafo precedente.
   * Aggiorna URL token: `https://accounts.google.com/o/oauth2/token`
   * Scadenza token di aggiornamento: mai
1. Fai clic su **Salva**.

<!-- clarify refresh token expiry, currently not present in the UI -->

Una volta configurate, le impostazioni avranno un aspetto simile a questo:

![Finestra di configurazione del provider SMTP Oauth2 del Mailer CQ](assets/oauth-smtpprov2.png)

Ora, attiva i componenti OAuth. Per farlo, segui questi passaggi:

1. Passare alla console Componenti visitando questo URL: `http://serveraddress:serverport/system/console/components`
1. Cerca i seguenti componenti
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeGenerateServlet`
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeAccessTokenGenerator`
1. Premi l’icona Play a sinistra dei componenti

   ![Elenco di componenti che mostrano OAuthCodeGenerateServlet e OAuthCodeAccessTokenGenerator](assets/oauth-components-play.png)

Infine, conferma la configurazione:

1. Vai all’indirizzo dell’istanza di Publish e accedi come amministratore.
1. Apri una nuova scheda nel browser e passa a `http://serveraddress:serverport/services/mailer/oauth2/authorize`. Questo ti reindirizzerà alla pagina del tuo provider SMTP, in questo caso Gmail.
1. Accesso e consenso per l’assegnazione delle autorizzazioni richieste
1. Dopo il consenso, il token verrà archiviato nell’archivio. Puoi accedervi in `accessToken` accedendo direttamente a questo URL nella tua istanza di pubblicazione: `http://serveraddress:serverport/crx/de/index.jsp#/conf/global/settings/mailer/oauth`
1. Ripeti quanto sopra per ogni istanza di pubblicazione

<!-- clarify if the ip/server address in the last procedure is that of the publish instance -->

### Microsoft Outlook {#microsoft-outlook}

1. Vai a [https://portal.azure.com/](https://portal.azure.com/) e accedi.
1. Cerca **Azure Active Directory** nella barra di ricerca e fai clic sul risultato. In alternativa, è possibile passare direttamente a [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)
1. Fai clic su **Registrazione app** - **Nuova registrazione**

   ![Nuovo pulsante di registrazione durante la configurazione di Microsoft Outlook](assets/oauth-outlook1.png)

1. Inserisci le informazioni in base alle tue esigenze, quindi fai clic su **Registra**
1. Vai alla nuova app creata e seleziona **Autorizzazioni API**
1. Vai a **Aggiungi autorizzazione** - **Autorizzazione grafico** - **Autorizzazioni delegate**
1. Seleziona le seguenti autorizzazioni per la tua app, quindi fai clic su **Aggiungi autorizzazione**:
   * `SMTP.Send`
   * `Mail.Read`
   * `Mail.Send`
   * `openid`
   * `offline_access`
1. Vai a **Autenticazione** - **Aggiungi una piattaforma** - **Web** e nella sezione **Url di reindirizzamento** aggiungi il seguente URL per reindirizzare il codice OAuth, quindi premi **Configura**:
   * `http://localhost:4503/services/mailer/oauth2/token`
1. Ripeti quanto sopra per ogni istanza di pubblicazione
1. Configura le impostazioni in base alle tue esigenze
1. Quindi, vai a **Certificati e segreti**, fai clic su **Nuovo segreto client** e segui i passaggi sullo schermo per creare un segreto. Assicurati di prendere nota di questo segreto per un uso successivo
1. Premi **Panoramica** nel riquadro a sinistra e copia i valori per **ID applicazione (client)** e **ID directory (tenant)** per un uso successivo

Per ricapitolare, è necessario disporre delle seguenti informazioni per configurare OAuth2 per il servizio Mailer sul lato AEM:

* L’URL di autenticazione, che verrà costruito con l’ID tenant. Avrà il seguente modulo: `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/authorize`
* L’URL del token, che verrà costruito con l’ID tenant. Avrà il seguente modulo: `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* L’URL di aggiornamento, che verrà costruito con l’ID tenant. Avrà il seguente modulo: `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* ID client
* Segreto client

**Configurazioni lato AEM**

Quindi, integra le impostazioni OAuth2 con AEM:

1. Passa alla console Web dell&#39;istanza locale passando a `http://serveraddress:serverport/system/console/configMgr`
1. Cerca e fai clic su **Day CQ Mail Service**
1. Aggiungi le seguenti impostazioni:
   * Nome host server SMTP: `smtp.office365.com`
   * Utente SMTP: nome utente in formato e-mail
   * Indirizzo &quot;Da&quot;: indirizzo e-mail da utilizzare nel campo &quot;Da:&quot; dei messaggi inviati dal mailer
   * Porta del server SMTP: `25` o `587` a seconda dei requisiti
   * Seleziona le caselle di spunta per **SMPT usa StarTLS** e **SMTP richiede StarTLS**
   * Controlla **Flusso OAuth** e fai clic su **Salva**.
1. Cerca, quindi fai clic su **Provider SMTP OAuth2 CQ Mailer**
1. Compila le informazioni richieste come segue:
   * Compila l&#39;URL di autorizzazione, l&#39;URL del token e l&#39;URL del token di aggiornamento costruendoli come descritto in [fine della procedura](#microsoft-outlook)
   * ID client e Segreto client: configura questi campi con i valori recuperati come descritto in precedenza.
   * Aggiungi i seguenti ambiti alla configurazione:
      * openid
      * offline_access
      * `https://outlook.office365.com/Mail.Send`
      * `https://outlook.office365.com/Mail.Read`
      * `https://outlook.office365.com/SMTP.Send`
   * URL reindirizzamento codice di autenticazione: `http://localhost:4503/services/mailer/oauth2/token`
   * Aggiorna URL token: deve avere lo stesso valore dell’URL token indicato sopra
1. Fai clic su **Salva**.

Una volta configurate, le impostazioni avranno un aspetto simile a questo:

![Configurazione SMTP OAuth2 del Mailer CQ completata](assets/oauth-outlook-smptconfig.png)

Ora, attiva i componenti OAuth. Per farlo, segui questi passaggi:

1. Passare alla console Componenti visitando questo URL: `http://serveraddress:serverport/system/console/components`
1. Cerca i seguenti componenti
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeGenerateServlet`
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeAccessTokenGenerator`
1. Premi l’icona Play a sinistra dei componenti

![Frammento dell&#39;elenco dei componenti contenente OAuthCodeGenerateServlet e OAuthCodeAccessTokenGenerator](assets/oauth-components-play.png)

Infine, conferma la configurazione:

1. Vai all’indirizzo dell’istanza di Publish e accedi come amministratore.
1. Apri una nuova scheda nel browser e passa a `http://serveraddress:serverport/services/mailer/oauth2/authorize`. In questo caso verrà reindirizzato alla pagina del provider SMTP, in questo caso Outlook.
1. Accesso e consenso per l’assegnazione delle autorizzazioni richieste
1. Dopo il consenso, il token verrà archiviato nell’archivio. Puoi accedervi in `accessToken` accedendo direttamente a questo URL nella tua istanza di pubblicazione: `http://serveraddress:serverport/crx/de/index.jsp#/conf/global/settings/mailer/oauth`
