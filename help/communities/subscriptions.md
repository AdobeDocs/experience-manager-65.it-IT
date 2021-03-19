---
title: Iscrizioni alle community
seo-title: Iscrizioni alle community
description: I membri della community interagiscono con altri membri tramite e-mail
seo-description: I membri della community interagiscono con altri membri tramite e-mail
uuid: a4b98769-c219-4e18-8e80-9a806ab979ff
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 33c85af4-4c56-487a-ba60-55211cb9f72c
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 2%

---


# Iscrizioni alle community {#communities-subscriptions}

## Panoramica {#overview}

A partire da Communities [FP1](deploy-communities.md#latestfeaturepack), i membri della community possono interagire con la community tramite e-mail utilizzando una funzione definita come abbonamenti.

Gli abbonamenti sono simili alle [notifiche](notifications.md) in quanto i membri possono iscriversi quando seguono articoli di blog, argomenti di forum o domande di QnA.

Ciò che distingue gli abbonamenti dalle notifiche è:

* I membri non possono iscriversi quando seguono altri membri.
* L&#39;unica azione che i membri devono intraprendere è selezionare `Email Subscriptions` quando segue.
* Quando la risposta e-mail è configurata, i membri possono pubblicare efficacemente il contenuto semplicemente rispondendo all&#39;e-mail ricevuta.

### Requisiti {#requirements}

**Configura e-mail**

È necessario configurare l’e-mail affinché le iscrizioni funzionino e affinché i membri rispondano via e-mail.

Per istruzioni su come impostare l’e-mail, consulta [Configurazione di e-mail](email.md).

**Abilita sottoscrizioni e segui**

I componenti devono essere configurati per abilitare le sottoscrizioni *e* seguenti. Le funzioni che consentono gli abbonamenti sono [blog](blog-feature.md), [forum](forum.md) e [QnA](working-with-qna.md).

## Abbonamenti da {#subscriptions-from-following}

![seguito](assets/subscription-following.png)

Il pulsante **Segui** consente di seguire le voci come attività, abbonamenti e/o notifiche. Ogni volta che si seleziona il pulsante **Segui**, è possibile attivare o disattivare una selezione.

Se è selezionato un metodo qualsiasi, il testo del pulsante diventa **Seguente**. Per comodità, è possibile selezionare `Unfollow All` per disattivare tutti i metodi.

Il pulsante **Segui** includerà l&#39;opzione `Email Subscriptions` solo quando un forum, QnA o un blog è configurato per abilitare gli abbonamenti alle e-mail. Viene visualizzato questo pulsante:

* Nella pagina delle funzioni principali per il forum abilitato, QnA o blog verrà inviato un messaggio e-mail per tutte le attività che rientrano in tale funzione.

* Per un post specifico, ad esempio un argomento del forum, una domanda QnA o un articolo di blog, invia un&#39;e-mail quando è presente un&#39;attività per quel post specifico.

## Risposta tramite e-mail {#reply-by-email}

Quando l’e-mail è [configurata per la risposta tramite e-mail](email.md#configure-polling-importer), il membro che si è iscritto riceverà un’e-mail con il contenuto pubblicato e un collegamento al contenuto online.

Se rispondono all’e-mail, il contenuto inserito nella risposta verrà visualizzato come contenuto online.

![email-response](assets/email-reply.png)

Il tempo necessario per la registrazione di una risposta è controllato dall&#39; [intervallo di aggiornamento dell&#39;importatore di polling](email.md#configure-polling-importer).

![Controllo qualità](assets/qa.png)

