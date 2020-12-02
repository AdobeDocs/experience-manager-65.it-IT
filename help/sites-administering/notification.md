---
title: Configurazione delle notifiche e-mail
seo-title: Configurazione delle notifiche e-mail
description: Scoprite come configurare le notifiche e-mail in AEM.
seo-description: Scoprite come configurare le notifiche e-mail in AEM.
uuid: 6cbdc312-860b-4a69-8bbe-2feb32204a27
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 6466d7b8-e308-43c5-acdc-dec15f796f64
translation-type: tm+mt
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '1145'
ht-degree: 1%

---


# Configurazione di Email Notification{#configuring-email-notification}

AEM invia notifiche e-mail agli utenti che:

* Hanno effettuato la sottoscrizione a eventi di pagina, ad esempio modifiche o replica. La sezione [Inbox notifica](/help/sites-classic-ui-authoring/author-env-inbox.md#subscribing-to-notifications) descrive come effettuare la sottoscrizione a tali eventi.

* Hanno effettuato la sottoscrizione agli eventi forum.
* Eseguire un passaggio in un flusso di lavoro. La sezione [Passo partecipante](/help/sites-developing/workflows-step-ref.md#participant-step) descrive come attivare la notifica e-mail in un flusso di lavoro.

Prerequisiti:

* Gli utenti devono avere un indirizzo e-mail valido definito nel suo profilo.
* Il **Day CQ Mail Service** deve essere configurato correttamente.

Quando un utente riceve una notifica, riceve un messaggio e-mail nella lingua definita nel suo profilo. Ogni lingua ha un proprio modello che può essere personalizzato. È possibile aggiungere nuovi modelli di e-mail per le nuove lingue.

>[!NOTE]
>
>Quando lavorate con AEM esistono diversi metodi per gestire le impostazioni di configurazione di tali servizi; per ulteriori informazioni e procedure consigliate, vedere [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md).

## Configurazione di Mail Service {#configuring-the-mail-service}

Per AEM poter inviare e-mail, è necessario configurare correttamente il **Day CQ Mail Service**. Potete visualizzare la configurazione nella console Web. Quando lavorate con AEM esistono diversi metodi per gestire le impostazioni di configurazione di tali servizi; per ulteriori informazioni e procedure consigliate, vedere [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md).

Si applicano i seguenti vincoli:

* La **porta del server SMTP** deve essere uguale o superiore a 25.

* Il nome host del server **SMTP** non deve essere vuoto.
* L&#39;indirizzo **&quot;From&quot;** non deve essere vuoto.

Per risolvere un problema con il servizio **Day CQ Mail Service**, è possibile controllare i registri del servizio:

`com.day.cq.mailer.DefaultMailService`

Nella console Web, la configurazione è la seguente:

![chlimage_1-276](assets/chlimage_1-276.png)

## Configurazione del canale di notifica e-mail {#configuring-the-email-notification-channel}

Quando vi iscrivete alle notifiche degli eventi di pagina o forum, l’indirizzo e-mail è impostato su `no-reply@acme.com` per impostazione predefinita. Puoi modificare questo valore configurando il servizio **Canale e-mail di notifica** nella console Web.

Per configurare l&#39;indirizzo e-mail, aggiungere un nodo `sling:OsgiConfig` alla directory archivio. Utilizzare la procedura seguente per aggiungere il nodo direttamente utilizzando CRXDE Lite:

1. In CRXDE Lite, aggiungete una cartella denominata `config` sotto la cartella dell’applicazione.
1. Nella cartella di configurazione, aggiungete un nodo denominato:

   `com.day.cq.wcm.notification.email.impl.EmailChannel` di tipo  `sling:OsgiConfig`

1. Aggiungete una proprietà `String` al nodo denominato `email.from`. Per il valore, specificate l&#39;indirizzo e-mail che desiderate utilizzare.

1. Fare clic su **Salva tutto**.

Utilizzate la procedura seguente per definire il nodo nelle cartelle di origine del pacchetto di contenuto:

1. In `jcr_root/apps/*app_name*/config folder`, create un file denominato `com.day.cq.wcm.notification.email.impl.EmailChannel.xml`

1. Aggiungete il seguente codice XML per rappresentare il nodo:

   `<?xml version="1.0" encoding="UTF-8"?> <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0" jcr:primaryType="sling:OsgiConfig" email.from="name@server.com"/>`
1. Sostituite il valore dell&#39;attributo `email.from` ( `name@server.com`) con l&#39;indirizzo e-mail.

1. Salvate il file.

## Configurazione del servizio di notifica e-mail flusso di lavoro {#configuring-the-workflow-email-notification-service}

Quando ricevete notifiche e-mail dal flusso di lavoro, sia l’indirizzo e-mail che il prefisso dell’URL dell’host vengono impostati sui valori predefiniti. Potete modificare questi valori configurando il **Day CQ Workflow Notification Service** nella console Web. In questo caso, si consiglia di mantenere la modifica nella directory archivio.

Nella console Web la configurazione predefinita è la seguente:

![chlimage_1-277](assets/chlimage_1-277.png)

### Modelli e-mail per notifica pagina {#email-templates-for-page-notification}

Di seguito sono riportati i modelli e-mail per le notifiche della pagina:

`/etc/notification/email/default/com.day.cq.wcm.core.page`

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

#### Personalizzazione dei modelli e-mail per la notifica della pagina {#customizing-email-templates-for-page-notification}

Per personalizzare il modello e-mail inglese per la notifica della pagina:

1. In CRXDE, aprite il file:

   `/etc/notification/email/default/com.day.cq.wcm.core.page/en.txt`

1. Modificate il file in base alle vostre esigenze.
1. Salva le modifiche.

Il modello deve avere il formato seguente:

```
 subject=<text_1>
 header=<text_2>
 message=<text_3>
 footer=<text_4>
```

Dove &lt;text_x> può essere un mix di testo statico e variabili di stringa dinamiche. Le seguenti variabili possono essere utilizzate nel modello e-mail per le notifiche di pagina:

* `${time}`, la data e l’ora dell’evento.

* `${userFullName}`, il nome completo dell&#39;utente che ha attivato l&#39;evento.

* `${userId}`, l&#39;ID dell&#39;utente che ha attivato l&#39;evento.
* `${modifications}`, descrive il tipo di evento pagina e il percorso della pagina nel formato:

   &lt;page event=&quot;&quot; type=&quot;&quot;> =>  &lt;page path=&quot;&quot;>

   Esempio:

   PageModified => /content/geometrixx/en/products

### Modelli e-mail per notifica forum {#email-templates-for-forum-notification}

I modelli e-mail per le notifiche dei forum si trovano in:

`/etc/notification/email/default/com.day.cq.collab.forum`

Il modello inglese predefinito ( `en.txt`) è definito come segue:

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

1. In CRXDE, aprite il file:

   `/etc/notification/email/default/com.day.cq.collab.forum/en.txt`

1. Modificate il file in base alle vostre esigenze.
1. Salva le modifiche.

Il modello deve avere il formato seguente:

```
 subject=<text_1>
 header=<text_2>
 message=<text_3>
 footer=<text_4>
```

Dove `<text_x>` può essere un mix di testo statico e variabili stringa dinamiche.

Le seguenti variabili possono essere utilizzate nel modello e-mail per le notifiche del forum:

* `${time}`, la data e l’ora dell’evento.

* `${forum.path}`, il percorso della pagina del forum.

### Modelli e-mail per notifica flusso di lavoro {#email-templates-for-workflow-notification}

Il modello e-mail per le notifiche del flusso di lavoro (inglese) si trova in:

`/etc/workflow/notification/email/default/en.txt`

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

#### Personalizzazione dei modelli e-mail per la notifica del flusso di lavoro {#customizing-email-templates-for-workflow-notification}

Per personalizzare il modello e-mail inglese per la notifica dell&#39;evento del flusso di lavoro:

1. In CRXDE, aprite il file:

   `/etc/workflow/notification/email/default/en.txt`

1. Modificate il file in base alle vostre esigenze.
1. Salva le modifiche.

Il modello deve avere il formato seguente:

```
subject=<text_1>
 header=<text_2>
 message=<text_3>
 footer=<text_4>
```

>[!NOTE]
>
>Dove `<text_x>` può essere un mix di testo statico e variabili stringa dinamiche. Ogni riga di un elemento `<text_x>` deve essere terminata con una barra rovesciata ( `\`), fatta eccezione per l&#39;ultima istanza, quando l&#39;assenza della barra rovesciata indica la fine della variabile di stringa `<text_x>`.
>
>Ulteriori informazioni sul formato del modello sono disponibili in [javadocs del metodo Properties.load()](https://docs.oracle.com/javase/8/docs/api/java/util/Properties.html#load-java.io.InputStream-).

Il metodo `${payload.path.open}` rivela il percorso del payload dell&#39;elemento di lavoro. Ad esempio, per una pagina in Sites, `payload.path.open` sarà simile a `/bin/wcmcommand?cmd=open&path=…`.; senza il nome del server, motivo per cui il modello prepende questo con `${host.prefix}`.

Le seguenti variabili possono essere utilizzate nel modello e-mail:

* `${event.EventType}`, tipo dell&#39;evento
* `${event.TimeStamp}`, data e ora dell&#39;evento
* `${event.User}`, l&#39;utente che ha attivato l&#39;evento
* `${initiator.home}`, il percorso del nodo iniziatore

* `${initiator.name}`, il nome dell&#39;iniziatore

* `${initiator.email}`, indirizzo e-mail del promotore
* `${item.id}`, l&#39;ID dell&#39;elemento di lavoro
* `${item.node.id}`, id del nodo nel modello di workflow associato a questo elemento di lavoro
* `${item.node.title}`, titolo dell&#39;elemento di lavoro
* `${participant.email}`, indirizzo e-mail del partecipante
* `${participant.name}`, nome del partecipante
* `${participant.familyName}`, cognome del partecipante
* `${participant.id}`id del partecipante
* `${participant.language}`, la lingua del partecipante
* `${instance.id}`, l&#39;ID del flusso di lavoro
* `${instance.state}`, lo stato del flusso di lavoro
* `${model.title}`, titolo del modello di workflow
* `${model.id}`, l&#39;ID del modello di workflow

* `${model.version}`, la versione del modello di workflow
* `${payload.data}`, il payload

* `${payload.type}`, il tipo di payload
* `${payload.path}`, percorso del payload
* `${host.prefix}`, prefisso dell&#39;host, ad esempio: http://localhost:4502

### Aggiunta di un modello e-mail per una nuova lingua {#adding-an-email-template-for-a-new-language}

Per aggiungere un modello per una nuova lingua:

1. In CRXDE, aggiungete un file `<language-code>.txt` sotto:

   * `/etc/notification/email/default/com.day.cq.wcm.core.page` : per le notifiche di pagina
   * `/etc/notification/email/default/com.day.cq.collab.forum` : per le notifiche forum
   * `/etc/workflow/notification/email/default` : per le notifiche sul flusso di lavoro

1. Adattare il file alla lingua.
1. Salva le modifiche.

>[!NOTE]
>
>Il `<language-code>` utilizzato come nome file per il modello e-mail deve essere un codice della lingua minuscola a due lettere riconosciuto da AEM. Per i codici lingua, AEM si basa su ISO-639-1.

## Configurazione  notifiche e-mail AEM Assets {#assetsconfig}

Quando le raccolte in  AEM Assets vengono condivise o non condivise, gli utenti possono ricevere notifiche e-mail da AEM. Per configurare le notifiche e-mail, effettuate le seguenti operazioni.

1. Configurate il servizio e-mail, come descritto sopra in [Configurazione del servizio e-mail](/help/sites-administering/notification.md#configuring-the-mail-service).
1. Accedete a AEM come amministratore. Fare clic su **Strumenti** > **Operazioni** > **Console Web** per aprire Configurazione console Web.
1. Modificare **Giorno CQ DAM Resource Collection Servlet**. Selezionare **Invia e-mail**. Fai clic su **Salva**.

