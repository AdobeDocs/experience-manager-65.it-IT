---
title: Iscrizioni community
seo-title: Iscrizioni community
description: I membri della community interagiscono con altri membri tramite e-mail
seo-description: I membri della community interagiscono con altri membri tramite e-mail
uuid: a4b98769-c219-4e18-8e80-9a806ab979ff
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 33c85af4-4c56-487a-ba60-55211cb9f72c
translation-type: tm+mt
source-git-commit: 2fcd87cd1def7fc265ba40c83b50db86618f3b70
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 0%

---


# Iscrizioni community {#communities-subscriptions}

## Panoramica {#overview}

A partire da Communities [FP1](deploy-communities.md#latestfeaturepack), i membri della community possono interagire con la community tramite e-mail utilizzando una funzione denominata come abbonamenti.

Le iscrizioni sono simili alle [notifiche](notifications.md) in quanto i membri possono iscriversi quando seguono articoli di blog, argomenti di forum o domande di QnA.

Ciò che distingue le sottoscrizioni dalle notifiche è:

* I membri non possono iscriversi quando seguono altri membri.
* L&#39;unica azione che i membri devono intraprendere è selezionare `Email Subscriptions` quando segue.
* Quando è configurata la risposta e-mail, i membri possono pubblicare efficacemente il contenuto semplicemente rispondendo all&#39;e-mail ricevuta.

### Requisiti {#requirements}

**Configura e-mail**

Affinché le iscrizioni funzionino e i membri rispondano via e-mail, è necessario configurare l&#39;e-mail.

Per istruzioni sulla configurazione dell&#39;e-mail, vedere [Configurazione di e-mail](email.md).

**Abilita iscrizioni e segui**

I componenti devono essere configurati per abilitare le iscrizioni *e* seguenti. Le funzioni che consentono l&#39;iscrizione sono [blog](blog-feature.md), [forum](forum.md) e [QnA](working-with-qna.md).

## Iscrizioni da {#subscriptions-from-following}

![subscription-follow](assets/subscription-following.png)

Il pulsante **Segui** consente di seguire le voci come attività, iscrizioni e/o notifiche. Ogni volta che il tasto **Segui** è selezionato, è possibile attivare o disattivare una selezione.

Se è selezionato un metodo di seguito, il testo del pulsante diventa **Successivo**. Per comodità, è possibile selezionare `Unfollow All` per disattivare tutti i metodi.

Il pulsante **Segui** includerà l&#39;opzione `Email Subscriptions` solo quando un forum, QnA o un blog è configurato per abilitare le iscrizioni alle e-mail. Verrà visualizzato il pulsante:

* Nella pagina delle funzioni principali per il forum abilitato, QnA o il blog verrà inviato un messaggio e-mail per tutte le attività in tale funzione.

* Per un post specifico, come un argomento del forum, una domanda QnA o un articolo del blog, verrà inviato un messaggio e-mail quando esiste attività per quel post specifico.

## Rispondi per e-mail {#reply-by-email}

Quando l&#39;e-mail è [configurata per la risposta tramite e-mail](email.md#configure-polling-importer), il membro che ha effettuato l&#39;iscrizione riceverà un&#39;e-mail con il contenuto pubblicato e un collegamento al contenuto online.

Se rispondono all’e-mail, il contenuto immesso nella risposta verrà visualizzato come contenuto online.

![email-response](assets/email-reply.png)

Il tempo necessario per inviare una risposta è controllato dall&#39;intervallo di aggiornamento dell&#39;importatore [polling ](email.md#configure-polling-importer).

![Controllo qualità](assets/qa.png)

