---
title: Nozioni di base sulla messaggistica
description: Scopri i dettagli sull’utilizzo di e con il componente Messaggistica per includere una funzione di messaggistica su un sito web.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: b941b5e0-f768-4393-9a9d-ded2cd7d10c4
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 2%

---

# Nozioni di base sulla messaggistica {#messaging-essentials}

Questa pagina illustra i dettagli dell’utilizzo del componente Messaggistica per includere una funzione di messaggistica su un sito web.

## Nozioni di base per lato client {#essentials-for-client-side}

**Componi messaggio**

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td><p>social/messaggistica/componenti/hbs/composemessage</p> </td>
  </tr>
  <tr>
   <td> <a href="/help/communities/client-customize.md#clientlibs-for-scf" target="_blank"><strong>clientllibs</strong></a></td>
   <td><p>cq.social.hbs.messaging</p> </td>
  </tr>
  <tr>
   <td> <strong>modelli</strong></td>
   <td>/libs/social/messaging/components/hbs/composemessage/composemessage.hbs</td>
  </tr>
  <tr>
   <td><strong>css</strong></td>
   <td>/libs/social/messaging/components/hbs/composemessage/clientlibs/composemessage.css</td>
  </tr>
  <tr>
   <td><strong>proprietà</strong></td>
   <td>Consulta <a href="/help/communities/configure-messaging.md" target="_blank">Configurare la messaggistica</a></td>
  </tr>
  <tr>
   <td><strong>configurazione amministratore</strong></td>
   <td><a href="/help/communities/messaging.md">Configurare la messaggistica</a></td>
  </tr>
 </tbody>
</table>

**Elenco messaggi**

(per Posta in arrivo, Inviato e Cestino)

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td><p>social/messaggistica/componenti/hbs/messagebox</p> </td>
  </tr>
  <tr>
   <td> <a href="/help/communities/client-customize.md#clientlibs-for-scf" target="_blank"><strong>clientllibs</strong></a></td>
   <td><p>cq.social.hbs.messaging</p> </td>
  </tr>
  <tr>
   <td> <strong>modelli</strong></td>
   <td>/libs/social/messaging/components/hbs/messagebox/messagebox.hbs</td>
  </tr>
  <tr>
   <td><strong>css</strong></td>
   <td>/libs/social/messaging/components/hbs/messagebox/clientlibs/messagebox.css</td>
  </tr>
  <tr>
   <td><strong>proprietà</strong></td>
   <td>Consulta <a href="/help/communities/configure-messaging.md" target="_blank">Configurare la messaggistica</a></td>
  </tr>
  <tr>
   <td><strong>configurazione amministratore</strong></td>
   <td><a href="/help/communities/messaging.md" target="_blank">Configurare la messaggistica</a></td>
  </tr>
 </tbody>
</table>

Vedi anche [Personalizzazioni lato client](/help/communities/client-customize.md)

## Nozioni di base per lato server {#essentials-for-server-side}

* [Configurazione della messaggistica](/help/communities/configure-messaging.md)
* [API client di messaggistica](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/messaging/client/api/package-summary.html) per i componenti SCF
* [API di messaggistica](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/messaging/api/package-summary.html) per il servizio
* [Endpoint di messaggistica](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/messaging/client/endpoints/package-summary.html)
* [Personalizzazioni lato server](/help/communities/server-customize.md)

>[!CAUTION]
>
>Il parametro String deve *non* contengono una barra finale &quot;/&quot; per i seguenti metodi MessageBuilder:
>
>* `setInboxPath`()
>* `setSentItemsPath`()
>
>Ad esempio:
>
>```
>valid: mb.setInboxPath( "/mail/inbox" );
> not valid: mb.setInboxPath( "/mail/inbox/" );
>```

### Sito community {#community-site}

Una struttura del sito della community, creata mediante la procedura guidata, include la funzione di messaggistica se selezionata. Consulta `User Management` impostazioni di [Console Siti community](/help/communities/sites-console.md#user-management).

### Codice di esempio: messaggio ricevuto notifica {#sample-code-message-received-notification}

La funzione di messaggistica social genera eventi per le operazioni, ad esempio `send`, `marking read`, `marking delete`. Questi eventi possono essere rilevati e possono essere intraprese azioni sui dati contenuti nell’evento.

L&#39;esempio seguente è di un gestore eventi che ascolta `message sent` e invia un messaggio e-mail a tutti i destinatari utilizzando `Day CQ Mail Service`.

Per provare lo script di esempio lato server, è necessario un ambiente di sviluppo e la possibilità di creare un bundle OSGi:

1. Accedi come amministratore a ` [CRXDE|Lite](https://localhost:4502/crx/de)`.
1. Creare un `bundle node`in `/apps/engage/install` con nomi arbitrari, ad esempio:

   * Nome simbolico: `com.engage.media.social.messaging.MessagingNotification`
   * Nome: Avvio Notifica del messaggio del tutorial
   * Descrizione: servizio di esempio per l’invio di una notifica e-mail agli utenti quando ricevono un messaggio
   * Pacchetto: `com.engage.media.social.messaging.notification`

1. Accedi a `/apps/engage/install/com.engage.media.social.messaging.MessagingNotification/src/main/java/com/engage/media/social/messaging/notification`e quindi:

   1. Elimina `Activator.java` classe creata automaticamente.
   1. Crea classe `MessageEventHandler.java`.
   1. Copia e incolla il codice seguente in `MessageEventHandler.java`.

1. Clic **Salva tutto**.
1. Accedi a `/apps/engage/install/com.engage.media.social.messaging.MessagingNotification/com.engage.media.social.messaging.MessagingNotification.bnd`e aggiungere tutte le istruzioni di importazione come scritto nella `MessageEventHandler.java` codice.
1. Crea il bundle.
1. Assicurare `Day CQ Mail Service`Il servizio OSGi è configurato.
1. Accedi come utente demo e invia un’e-mail a un altro utente.
1. Il destinatario riceve un’e-mail relativa a un nuovo messaggio.

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
