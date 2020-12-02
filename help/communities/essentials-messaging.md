---
title: Nozioni di base sui messaggi
seo-title: Nozioni di base sui messaggi
description: Panoramica del componente Messaggistica
seo-description: Panoramica del componente Messaggistica
uuid: e0dad45e-d84d-4b28-b357-aded1c5d2605
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 98f70093-e786-4555-8aaa-d0df4c977dc0
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 3%

---


# Nozioni di base sui messaggi {#messaging-essentials}

Questa pagina illustra i dettagli dell’utilizzo del componente Messaggi per includere una funzione di messaggistica in un sito Web.

## Essentials for Client-Side {#essentials-for-client-side}

**Componi messaggio**

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td><p>social/messaging/components/hbs/composemessaggio</p> </td>
  </tr>
  <tr>
   <td> <a href="/help/communities/client-customize.md#clientlibs-for-scf" target="_blank"><strong>clientllibs</strong></a></td>
   <td><p>cq.social.hbs.messaging</p> </td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td>/libs/social/messaging/components/hbs/composemessage/composemessage.hbs</td>
  </tr>
  <tr>
   <td><strong>css</strong></td>
   <td>/libs/social/messaging/components/hbs/composemessage/clientlibs/composemessage.css</td>
  </tr>
  <tr>
   <td><strong>proprietà</strong></td>
   <td>Vedere <a href="/help/communities/configure-messaging.md" target="_blank">Configurare i messaggi</a></td>
  </tr>
  <tr>
   <td><strong>configurazione amministratore</strong></td>
   <td><a href="/help/communities/messaging.md">Configurare i messaggi</a></td>
  </tr>
 </tbody>
</table>

**Elenco messaggi**

(per Inbox, Inviato e Cestino)

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td><p>social/messaging/components/hbs/messagebox</p> </td>
  </tr>
  <tr>
   <td> <a href="/help/communities/client-customize.md#clientlibs-for-scf" target="_blank"><strong>clientllibs</strong></a></td>
   <td><p>cq.social.hbs.messaging</p> </td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td>/libs/social/messaging/components/hbs/messagebox/messagebox.hbs</td>
  </tr>
  <tr>
   <td><strong>css</strong></td>
   <td>/libs/social/messaging/components/hbs/messagebox/clientlibs/messagebox.css</td>
  </tr>
  <tr>
   <td><strong>proprietà</strong></td>
   <td>Vedere <a href="/help/communities/configure-messaging.md" target="_blank">Configurare i messaggi</a></td>
  </tr>
  <tr>
   <td><strong>configurazione amministratore</strong></td>
   <td><a href="/help/communities/messaging.md" target="_blank">Configurare i messaggi</a></td>
  </tr>
 </tbody>
</table>

Vedere anche [Personalizzazioni lato client](/help/communities/client-customize.md)

## Essentials for Server-Side {#essentials-for-server-side}

* [Configurazione dei messaggi](/help/communities/configure-messaging.md)
* [Messaggistica ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/messaging/client/api/package-summary.html) API client per componenti SCF
* [API ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/messaging/api/package-summary.html) di messaggistica per il servizio
* [Endpoint di messaggistica](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/messaging/client/endpoints/package-summary.html)
* [Personalizzazioni lato server](/help/communities/server-customize.md)

>[!CAUTION]
>
>Il parametro String deve contenere *not* una barra finale &quot;/&quot; per i seguenti metodi di MessageBuilder:
>
>* `setInboxPath`()
>* `setSentItemsPath`()

>
>
Esempio:
>
>
```
>valid: mb.setInboxPath( "/mail/inbox" );
> not valid: mb.setInboxPath( "/mail/inbox/" );
>```

### Sito community {#community-site}

Una struttura del sito community, creata utilizzando la procedura guidata, include la funzione di messaggistica selezionata. Vedere Impostazioni `User Management` della [console Siti della community](/help/communities/sites-console.md#user-management).

### Codice di esempio: Messaggio ricevuto notifica {#sample-code-message-received-notification}

La funzione Messaggi social genera eventi per le operazioni, ad esempio `send`, `marking read`, `marking delete`. Questi eventi possono essere rilevati e le azioni eseguite sui dati contenuti nell’evento.

L&#39;esempio seguente fa riferimento a un gestore eventi in ascolto dell&#39;evento `message sent` e invia un&#39;e-mail a tutti i destinatari del messaggio utilizzando la variabile `Day CQ Mail Service`.

Per provare lo script di esempio lato server, è necessario un ambiente di sviluppo e la capacità di creare un bundle OSGi:

1. Accedete come amministratore a ` [CRXDE|Lite](https://localhost:4502/crx/de)`.
1. Create un `bundle node`in `/apps/engage/install` con nomi arbitrari, ad esempio:

   * Nome simbolico: `com.engage.media.social.messaging.MessagingNotification`
   * Nome: Notifica dei messaggi per l’esercitazione introduttiva
   * Descrizione: Un servizio di esempio per inviare una notifica e-mail agli utenti che ricevono un messaggio
   * Pacchetto: `com.engage.media.social.messaging.notification`

1. Passare a `/apps/engage/install/com.engage.media.social.messaging.MessagingNotification/src/main/java/com/engage/media/social/messaging/notification`, quindi:

   1. Eliminate la classe `Activator.java` creata automaticamente.
   1. Creare la classe `MessageEventHandler.java`.
   1. Copiate e incollate il codice riportato di seguito in `MessageEventHandler.java`.

1. Fare clic su **Salva tutto**.
1. Passare a `/apps/engage/install/com.engage.media.social.messaging.MessagingNotification/com.engage.media.social.messaging.MessagingNotification.bnd` e aggiungere tutte le istruzioni di importazione come scritte nel codice `MessageEventHandler.java`.
1. Create il bundle.
1. Verificare che il servizio `Day CQ Mail Service`OSGi sia configurato.
1. Effettuate l&#39;accesso come utente dimostrativo e inviate un&#39;e-mail a un altro utente.
1. Il destinatario riceve un&#39;e-mail relativa a un nuovo messaggio.

#### MessageEventHandler.java {#messageeventhandler-java}

```java
package com.engage.media.social.messaging.notification;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Properties;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;
import org.apache.felix.scr.annotations.Reference;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.api.resource.ResourceResolverFactory;
import org.apache.sling.api.resource.Resource;
import org.apache.commons.mail.Email;
import org.apache.commons.mail.EmailException;
import org.apache.commons.mail.SimpleEmail;
import org.apache.commons.mail.HtmlEmail;
import java.util.List;
import org.osgi.service.event.Event;
import org.osgi.service.event.EventHandler;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import com.adobe.cq.social.messaging.api.Message;
import com.adobe.cq.social.messaging.api.MessagingEvent;
import com.day.cq.mailer.MessageGatewayService;
import com.day.cq.mailer.MessageGateway;

@Component(immediate=true)
@Service(EventHandler.class)
@Properties({
        @Property(name = "event.topics", value = "com/adobe/cq/social/message")
})
public class MessagingEventHandler implements EventHandler {
    private Logger logger = LoggerFactory.getLogger(MessagingEventHandler.class);

    @Reference
    ResourceResolverFactory resourceResolverFactory;

    @Reference
    private MessageGatewayService messageGatewayService;

    ResourceResolver resourceResolver=null;
    MessageGateway messageGateway=null;

    public void sendMail(String from, String to,String subject, String content){
        Email email = new SimpleEmail();
        messageGateway = messageGatewayService.getGateway(SimpleEmail.class);
        try {
         email.addTo(to);
            email.addReplyTo(from);
            email.setFrom(from);
            email.setMsg(content);
            email.setSubject(subject);
         messageGateway.send(email);
        } catch(EmailException ex) {
            logger.error("MessageNotificaiton : Error sending email : "+ex.getMessage());
        }
        logger.info("**** MessageNotification **** Mail sent to " + to);
    }

    public void handleEvent(Event event) {
        //Get Message Path and originator User's ID from event
        String messagePath = (String) event.getProperty("path");
        String senderId = (String) event.getProperty("userId");
        MessagingEvent.MessagingActions action = (MessagingEvent.MessagingActions) event.getProperty("action");
        try{
            if(MessagingEvent.MessagingActions.MessageSent.equals(action)){
                resourceResolver = resourceResolverFactory.getAdministrativeResourceResolver(null);

                //Read message
                Resource resource = resourceResolver.getResource(messagePath);
                Message msg = resource.adaptTo(Message.class);

                //Get list of recipient Ids from message
                //For Getting Started Tutorial, Id is same as email. If that is not the case in your site,
                //an additional step is needed to retrieve the email for the Id
                List<String> reclist = msg.getRecipientIdList();
                for(int i=0;i<reclist.size();i++){
                    //Send Email using Mailing Service
                    sendMail("admin@cqadmin.qqq",reclist.get(i),"New message on Getting Started Tutorial", "Hi\nYou have received a new message from  " +  senderId + ". To read it, sign in to Getting Started Tutorial.\n\n-Engage Admin");
                }
            }
        } catch(Exception ex){
            logger.error("Error getting message info : " + ex.getMessage());
        } finally {
            resourceResolver.close();
        }

    }
}
```

