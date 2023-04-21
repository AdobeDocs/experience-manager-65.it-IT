---
title: Configurazione della notifica e-mail
seo-title: Configuring Email Notification
description: Scopri come configurare le notifiche e-mail in AEM.
seo-description: Learn how to configure Email Notification in AEM.
uuid: 6cbdc312-860b-4a69-8bbe-2feb32204a27
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 6466d7b8-e308-43c5-acdc-dec15f796f64
exl-id: 918fcbbc-a78a-4fab-a933-f183ce6a907f
source-git-commit: e803fde42cfb7b7c9d3fb6483ca661ce386d6464
workflow-type: tm+mt
source-wordcount: '2116'
ht-degree: 12%

---

# Configurazione della notifica e-mail{#configuring-email-notification}

AEM invia notifiche e-mail agli utenti che:

* Si è iscritto a eventi di pagina, ad esempio modifiche o replica. La [Casella in entrata notifica](/help/sites-classic-ui-authoring/author-env-inbox.md#subscribing-to-notifications) la sezione descrive come effettuare la sottoscrizione a tali eventi.

* Si sono abbonati agli eventi del forum.
* Eseguire un passaggio in un flusso di lavoro. La [Passaggio partecipante](/help/sites-developing/workflows-step-ref.md#participant-step) in questa sezione viene descritto come attivare la notifica tramite e-mail in un flusso di lavoro.

Prerequisiti:

* Gli utenti devono avere un indirizzo e-mail valido definito nel suo profilo.
* La **Servizio e-mail Day CQ** deve essere configurato correttamente.

Quando un utente viene informato, riceve un’e-mail nella lingua definita nel suo profilo. Ogni lingua ha un proprio modello che può essere personalizzato. È possibile aggiungere nuovi modelli e-mail per le nuove lingue.

>[!NOTE]
>
>Quando si lavora con AEM esistono diversi metodi per gestire le impostazioni di configurazione di tali servizi; vedere [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md) per ulteriori dettagli e procedure consigliate.

## Configurazione del servizio e-mail {#configuring-the-mail-service}

Per AEM poter inviare e-mail, la **Servizio e-mail Day CQ** deve essere configurato correttamente. Puoi visualizzare la configurazione nella console Web. Quando si lavora con AEM esistono diversi metodi per gestire le impostazioni di configurazione di tali servizi; vedere [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md) per ulteriori dettagli e procedure consigliate.

Si applicano i seguenti vincoli:

* La **Porta server SMTP** deve essere uguale o superiore a 25.

* La **Nome host server SMTP** non deve essere vuoto.
* La **Indirizzo &quot;Da&quot;** non deve essere vuoto.

Per facilitare il debug di un problema con **Servizio e-mail Day CQ**, puoi guardare i registri del servizio:

`com.day.cq.mailer.DefaultMailService`

La configurazione si presenta come segue nella console Web:

![chlimage_1-276](assets/chlimage_1-276.png)

## Configurazione del canale di notifica e-mail {#configuring-the-email-notification-channel}

Quando vi abbonate a notifiche di eventi di pagina o forum, l’indirizzo e-mail del mittente è impostato su `no-reply@acme.com` per impostazione predefinita. Puoi modificare questo valore configurando la variabile **Canale e-mail notifica** nella console Web.

Per configurare l’indirizzo e-mail del mittente, aggiungi un `sling:OsgiConfig` al repository. Segui la procedura seguente per aggiungere il nodo direttamente utilizzando CRXDE Lite:

1. In CRXDE Lite, aggiungi una cartella denominata `config` nella cartella dell&#39;applicazione.
1. Nella cartella di configurazione, aggiungi un nodo denominato:

   `com.day.cq.wcm.notification.email.impl.EmailChannel` di tipo `sling:OsgiConfig`

1. Aggiungi un `String` al nodo denominato `email.from`. Per il valore , specifica l’indirizzo e-mail che desideri utilizzare.

1. Fai clic su **Salva tutto**.

Utilizza la seguente procedura per definire il nodo nelle cartelle di origine del pacchetto di contenuti:

1. Nel tuo `jcr_root/apps/*app_name*/config folder`, crea un file denominato `com.day.cq.wcm.notification.email.impl.EmailChannel.xml`

1. Aggiungi il seguente XML per rappresentare il nodo:

   `<?xml version="1.0" encoding="UTF-8"?> <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0" jcr:primaryType="sling:OsgiConfig" email.from="name@server.com"/>`
1. Sostituisci il valore del `email.from` attributo ( `name@server.com`) con il tuo indirizzo e-mail.

1. Salva il file.

## Configurazione del servizio di notifica e-mail del flusso di lavoro {#configuring-the-workflow-email-notification-service}

Quando ricevi notifiche e-mail del flusso di lavoro, sia l’indirizzo e-mail del flusso di lavoro che il prefisso dell’URL dell’host sono impostati sui valori predefiniti. Puoi modificare questi valori configurando la variabile **Servizio notifiche e-mail flusso di lavoro del giorno CQ** nella console Web. In questo caso, si consiglia di mantenere la modifica nell’archivio.

Nella console Web la configurazione predefinita è la seguente:

![chlimage_1-277](assets/chlimage_1-277.png)

### Modelli e-mail per notifica pagina {#email-templates-for-page-notification}

I modelli e-mail per le notifiche di pagina si trovano di seguito:

`/libs/settings/notification-templates/com.day.cq.wcm.core.page`

Il modello inglese predefinito ( `en.txt`) è definita come segue:

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

#### Personalizzazione dei modelli e-mail per la notifica della pagina {#customizing-email-templates-for-page-notification}

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

Dove &lt;text_x> può essere un insieme di variabili di testo statiche e di stringhe dinamiche. Le seguenti variabili possono essere utilizzate all’interno del modello e-mail per le notifiche di pagina:

* `${time}`, la data e l’ora dell’evento.

* `${userFullName}`, il nome completo dell’utente che ha attivato l’evento.

* `${userId}`, l&#39;ID dell&#39;utente che ha attivato l&#39;evento.
* `${modifications}`, descrive il tipo di evento pagina e il percorso della pagina nel formato :

   &lt;page event=&quot;&quot; type=&quot;&quot;> => &lt;page path=&quot;&quot;>

   Ad esempio:

   PageModified => /content/geometrixx/en/products

### Modelli e-mail per notifiche forum {#email-templates-for-forum-notification}

I modelli e-mail per le notifiche dei forum si trovano in:

`/etc/notification/email/default/com.day.cq.collab.forum`

Il modello inglese predefinito ( `en.txt`) è definita come segue:

```xml
subject=[CQ Forum Notification]

header=-------------------------------------------------------------------------------------\n \
Time: Time: ${time}\n \
Forum Page Path: ${forum.path}\n \
-------------------------------------------------------------------------------------\n\n

message=Page: ${host.prefix}${forum.path}.html\n

footer=\n \
-------------------------------------------------------------------------------------\n \
This is an automatically generated message. Please do not reply.
```

#### Personalizzazione dei modelli e-mail per la notifica del forum {#customizing-email-templates-for-forum-notification}

Per personalizzare il modello e-mail inglese per la notifica del forum:

1. In CRXDE, apri il file:

   `/etc/notification/email/default/com.day.cq.collab.forum/en.txt`

1. Modifica il file in base alle tue esigenze.
1. Salva le modifiche.

Il modello deve avere il seguente formato:

```
 subject=<text_1>
 header=<text_2>
 message=<text_3>
 footer=<text_4>
```

Dove `<text_x>` può essere un insieme di variabili di testo statiche e di stringhe dinamiche.

Le seguenti variabili possono essere utilizzate all&#39;interno del modello e-mail per le notifiche del forum:

* `${time}`, la data e l’ora dell’evento.

* `${forum.path}`, il percorso della pagina del forum.

### Modelli e-mail per notifiche flusso di lavoro {#email-templates-for-workflow-notification}

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

#### Personalizzazione dei modelli e-mail per le notifiche dei flussi di lavoro {#customizing-email-templates-for-workflow-notification}

Per personalizzare il modello e-mail inglese per la notifica dell’evento del flusso di lavoro:

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
>Dove `<text_x>` può essere un insieme di variabili di testo statiche e di stringhe dinamiche. Ogni riga di un `<text_x>` l’elemento deve essere terminato con una barra rovesciata ( `\`), ad eccezione dell’ultima istanza, quando l’assenza della barra inversa indica la fine della `<text_x>` variabile stringa.
>
>Ulteriori informazioni sul formato del modello sono disponibili nella sezione [javadocs di Properties.load()](https://docs.oracle.com/javase/8/docs/api/java/util/Properties.html#load-java.io.InputStream-) metodo .

Il metodo `${payload.path.open}` mostra il percorso del payload dell’elemento di lavoro. Ad esempio, per una pagina in Sites, quindi `payload.path.open` è simile a `/bin/wcmcommand?cmd=open&path=…`.; questo è senza il nome del server, ed è per questo che il modello ne fa una preclusione con `${host.prefix}`.

Le seguenti variabili possono essere utilizzate all’interno del modello e-mail:

* `${event.EventType}`, tipo dell’evento
* `${event.TimeStamp}`, data e ora dell&#39;evento
* `${event.User}`, l’utente che ha attivato l’evento
* `${initiator.home}`, il percorso del nodo iniziatore

* `${initiator.name}`, il nome dell&#39;iniziatore

* `${initiator.email}`, indirizzo e-mail dell&#39;iniziatore
* `${item.id}`, l&#39;id dell&#39;elemento di lavoro
* `${item.node.id}`, id del nodo nel modello di flusso di lavoro associato a questo elemento di lavoro
* `${item.node.title}`, titolo dell&#39;elemento di lavoro
* `${participant.email}`, indirizzo e-mail del partecipante
* `${participant.name}`, nome del partecipante
* `${participant.familyName}`, cognome del partecipante
* `${participant.id}`id del partecipante
* `${participant.language}`, la lingua del partecipante
* `${instance.id}`, l&#39;id del flusso di lavoro
* `${instance.state}`, lo stato del flusso di lavoro
* `${model.title}`, titolo del modello di flusso di lavoro
* `${model.id}`, l’id del modello di flusso di lavoro

* `${model.version}`, la versione del modello di flusso di lavoro
* `${payload.data}`, il payload

* `${payload.type}`, il tipo di payload
* `${payload.path}`, percorso del payload
* `${host.prefix}`, prefisso host, ad esempio: http://localhost:4502

### Aggiunta di un modello e-mail per una nuova lingua {#adding-an-email-template-for-a-new-language}

Per aggiungere un modello per una nuova lingua:

1. In CRXDE, aggiungi un file `<language-code>.txt` di seguito:

   * `/libs/settings/notification-templates/com.day.cq.wcm.core.page` : per le notifiche di pagina
   * `/etc/notification/email/default/com.day.cq.collab.forum` : per le notifiche sul forum
   * `/libs/settings/workflow/notification/email/default` : per le notifiche del flusso di lavoro

1. Adatta il file alla lingua.
1. Salva le modifiche.

>[!NOTE]
>
>La `<language-code>` utilizzato come nome del file per il modello e-mail deve essere un codice della lingua minuscolo a due lettere riconosciuto da AEM. Per i codici di lingua, AEM si basa su ISO-639-1.

## Configurazione delle notifiche e-mail di AEM Assets {#assetsconfig}

Quando le raccolte in AEM Assets vengono condivise o non condivise, gli utenti possono ricevere notifiche e-mail da AEM. Per configurare le notifiche e-mail, segui questi passaggi.

1. Configura il servizio e-mail come descritto sopra in [Configurazione del servizio e-mail](/help/sites-administering/notification.md#configuring-the-mail-service).
1. Accedi ad AEM come amministratore. Fai clic su **Strumenti** >  **Operazioni** >  **Console web** per aprire la configurazione della console Web.
1. Modifica **Servizio di raccolta risorse DAM Day CQ**. Seleziona **invia e-mail**. Fai clic su **Salva**.

## Configurazione di OAuth {#setting-up-oauth}

AEM offre il supporto OAuth2 per il suo servizio Mailer integrato, al fine di consentire alle organizzazioni di rispettare i requisiti di sicurezza delle e-mail.

Puoi configurare OAuth per più provider di posta elettronica, come descritto di seguito.

>[!NOTE]
>
>Questa procedura è un esempio per un&#39;istanza Publish. Se desideri abilitare le notifiche e-mail in un’istanza di authoring, devi seguire gli stessi passaggi sull’autore.

### Gmail {#gmail}

1. Crea il progetto in `https://console.developers.google.com/projectcreate`
1. Seleziona il progetto, quindi vai a **API e servizi** - **Dashboard - Credenziali**
1. Configura la schermata di consenso OAuth in base alle tue esigenze
1. Nella schermata Aggiorna che segue, aggiungi questi due ambiti:
   * `https://mail.google.com/`
   * `https://www.googleapis.com//auth/gmail.send`
1. Dopo aver aggiunto gli ambiti, torna a **Credenziali** nel menu a sinistra, vai a **Crea credenziali** - **ID client OAuth** - **App desktop**
1. Viene aperta una nuova finestra contenente l’ID client e il segreto client.
1. Salva queste credenziali.

**Configurazioni lato AEM**

>[!NOTE]
>
>I clienti di Adobe Managed Service possono collaborare con il tecnico del servizio clienti per apportare queste modifiche agli ambienti di produzione.

Per prima cosa, configura il servizio di posta:

1. Apri la Console Web AEM andando in `http://serveraddress:serverport/system/console/configMgr`
1. Cerca, quindi fai clic su **Servizio e-mail Day CQ**
1. Aggiungi le seguenti impostazioni:
   * Nome host del server SMTP: `smtp.gmail.com`
   * Porta server SMTP: `25` o `587`, a seconda dei requisiti
   * Seleziona le caselle di controllo per **SMPT utilizza StarTLS** e **SMTP richiede StarTLS**
   * Controlla **Flusso OAuth** e fai clic su **Salva**.

Quindi, configura il provider OAuth SMTP seguendo la procedura seguente:

1. Apri la Console Web AEM andando in `http://serveraddress:serverport/system/console/configMgr`
1. Cerca, quindi fai clic su **Provider OAuth2 SMTP del mittente CQ**
1. Compila le informazioni richieste come segue:
   * URL autorizzazione: `https://accounts.google.com/o/oauth2/auth`
   * URL token: `https://accounts.google.com/o/oauth2/token`
   * Ambiti: `https://www.googleapis.com/auth/gmail.send` e `https://mail.google.com/`. È possibile aggiungere più di un ambito premendo il pulsante **+** pulsante a destra di ogni ambito configurato.
   * ID client e segreto client: configura questi campi con i valori recuperati come descritto nel paragrafo precedente.
   * Aggiorna URL token: `https://accounts.google.com/o/oauth2/token`
   * Aggiorna scadenza token: mai
1. Fai clic su **Salva**.

<!-- clarify refresh token expiry, currrently not present in the UI -->

Una volta configurate, le impostazioni saranno simili al seguente:

![oauth smtp provider](assets/oauth-smtpprov2.png)

Ora attiva i componenti OAuth. Per farlo, segui questi passaggi:

1. Vai alla console Componenti visitando questo URL: `http://serveraddress:serverport/system/console/components`
1. Cerca i seguenti componenti
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeGenerateServlet`
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeAccessTokenGenerator`
1. Premere l’icona Riproduci a sinistra dei componenti

   ![componenti](assets/oauth-components-play.png)

Infine, conferma la configurazione:

1. Andando all&#39;indirizzo dell&#39;istanza Publish e accedendo come amministratore.
1. Apri una nuova scheda nel browser e vai a `http://serveraddress:serverport/services/mailer/oauth2/authorize`. Questo ti reindirizzerà alla pagina del tuo provider SMTP, in questo caso Gmail.
1. Accedi e acconsenti a concedere le autorizzazioni richieste
1. Dopo il consenso, il token verrà memorizzato nell’archivio. Puoi accedervi in `accessToken` accedendo direttamente a questo URL nella tua istanza di pubblicazione: `http://serveraddress:serverport/crx/de/index.jsp#/conf/global/settings/mailer/oauth`
1. Ripeti quanto sopra per ogni istanza di pubblicazione

<!-- clarify if the ip/server address in the last procedure is that of the publish instance -->

### Microsoft Outlook {#microsoft-outlook}

1. Vai a [https://portal.azure.com/](https://portal.azure.com/) e accedi.
1. Cerca **Azure Active Directory** nella barra di ricerca e fai clic sul risultato. In alternativa, è possibile navigare direttamente in [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)
1. Fai clic su **Registrazione app** - **Nuova registrazione**

   ![](assets/oauth-outlook1.png)

1. Compila le informazioni in base alle tue esigenze, quindi fai clic su **Registra**
1. Vai alla nuova app creata e seleziona **Autorizzazioni API**
1. Vai a **Aggiungi autorizzazione** - **Autorizzazione grafico** - **Autorizzazioni delegate**
1. Seleziona le seguenti autorizzazioni per la tua app, quindi fai clic su **Aggiungi autorizzazione**:
   * `SMTP.Send`
   * `Mail.Read`
   * `Mail.Send`
   * `openid`
   * `offline_access`
1. Vai a **Autenticazione** - **Aggiungere una piattaforma** - **Web** e nella **URL di reindirizzamento** aggiungi il seguente URL per reindirizzare il codice OAuth, quindi premi **Configura**:
   * `http://localhost:4503/services/mailer/oauth2/token`
1. Ripeti quanto sopra per ogni istanza di pubblicazione
1. Configura le impostazioni in base alle tue esigenze
1. Quindi, vai a **Certificati e segreti**, fai clic su **Nuovo segreto client** e segui i passaggi sullo schermo per creare un segreto. Assicurati di prendere nota di questo segreto per un uso successivo
1. Premi **Panoramica** nel riquadro a sinistra e copia i valori per **ID applicazione (client)** e **ID directory (tenant)** per un uso successivo

Per ricapitolare, dovrai disporre delle seguenti informazioni per configurare OAuth2 per il servizio Mailer sul lato AEM:

* L’URL di autenticazione, che verrà costruito con l’ID tenant. Avrà il seguente modulo: `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/authorize`
* L’URL del token, che verrà costruito con l’ID tenant. Avrà il seguente modulo: `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* L’URL di aggiornamento, che verrà costruito con l’ID tenant. Avrà il seguente modulo: `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* ID client
* Segreto client

**Configurazioni lato AEM**

Quindi, integra le impostazioni OAuth2 con AEM:

1. Passa alla console Web dell’istanza locale sfogliando `http://serveraddress:serverport/system/console/configMgr`
1. Cerca e fai clic su **Servizio e-mail Day CQ**
1. Aggiungi le seguenti impostazioni:
   * Nome host del server SMTP: `smtp.office365.com`
   * Utente SMTP: il tuo nome utente in formato e-mail
   * Indirizzo &quot;Da&quot;: Indirizzo e-mail da utilizzare nel campo &quot;Da:&quot; dei messaggi inviati dal mittente
   * Porta server SMTP: `25` o `587` a seconda dei requisiti
   * Seleziona le caselle di controllo per **SMPT utilizza StarTLS** e **SMTP richiede StarTLS**
   * Controlla **Flusso OAuth** e fai clic su **Salva**.
1. Cerca, quindi fai clic su **Provider OAuth2 SMTP del mittente CQ**
1. Compila le informazioni richieste come segue:
   * Compila l’URL di autorizzazione, l’URL del token e l’URL del token di aggiornamento costruendoli come descritto in [fine della procedura](#microsoft-outlook)
   * ID client e segreto client: configura questi campi con i valori recuperati come descritto in precedenza.
   * Aggiungi i seguenti ambiti alla configurazione:
      * openid
      * offline_access
      * `https://outlook.office365.com/Mail.Send`
      * `https://outlook.office365.com/Mail.Read`
      * `https://outlook.office365.com/SMTP.Send`
   * Url di reindirizzamento di AuthCode: `http://localhost:4503/services/mailer/oauth2/token`
   * Aggiorna URL token: dovrebbe avere lo stesso valore dell’URL del token sopra
1. Fai clic su **Salva**.

Una volta configurate, le impostazioni saranno simili al seguente:

![](assets/oauth-outlook-smptconfig.png)

Ora attiva i componenti OAuth. Per farlo, segui questi passaggi:

1. Vai alla console Componenti visitando questo URL: `http://serveraddress:serverport/system/console/components`
1. Cerca i seguenti componenti
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeGenerateServlet`
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeAccessTokenGenerator`
1. Premere l’icona Riproduci a sinistra dei componenti

![components2](assets/oauth-components-play.png)

Infine, conferma la configurazione:

1. Andando all&#39;indirizzo dell&#39;istanza Publish e accedendo come amministratore.
1. Apri una nuova scheda nel browser e vai a `http://serveraddress:serverport/services/mailer/oauth2/authorize`. In questo caso verrà reindirizzato alla pagina del provider SMTP, in Outlook.
1. Accedi e acconsenti a concedere le autorizzazioni richieste
1. Dopo il consenso, il token verrà memorizzato nell’archivio. Puoi accedervi in `accessToken` accedendo direttamente a questo URL nella tua istanza di pubblicazione: `http://serveraddress:serverport/crx/de/index.jsp#/conf/global/settings/mailer/oauth`