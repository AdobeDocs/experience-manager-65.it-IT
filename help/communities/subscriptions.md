---
title: Iscrizioni alle community
description: I membri della community interagiscono con altri membri tramite e-mail
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 338be220-659a-459c-8e90-55e3a11ddeb0
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 1%

---

# Iscrizioni alle community {#communities-subscriptions}

## Panoramica {#overview}

A partire da Communities [FP1](deploy-communities.md#latestfeaturepack), i membri della community possono interagire con la community tramite e-mail utilizzando una funzione definita abbonamenti.

Gli abbonamenti sono simili a [notifiche](notifications.md) I membri possono effettuare la sottoscrizione quando seguono articoli di blog, argomenti di forum o domande di controllo qualità.

Ciò che distingue gli abbonamenti dalle notifiche è:

* I membri non possono sottoscrivere un abbonamento quando seguono altri membri.
* L&#39;unica azione che i membri possono intraprendere è selezionare `Email Subscriptions` quando segue.
* Una volta configurata la risposta e-mail, i membri possono pubblicare efficacemente il contenuto semplicemente rispondendo all’e-mail ricevuta.

### Requisiti {#requirements}

**Configura e-mail**

Affinché gli abbonamenti siano funzionali, è necessario configurare l’indirizzo e-mail e consentire ai membri di rispondere per e-mail.

Per istruzioni sulla configurazione dell’e-mail, consulta [Configurazione dell’e-mail](email.md).

**Abilita abbonamenti e segui**

I componenti devono essere configurati per abilitare le sottoscrizioni *e* segue. Le funzionalità che consentono gli abbonamenti sono [blog](blog-feature.md), [forum](forum.md) e [D/R](working-with-qna.md).

## Abbonamenti da Segui {#subscriptions-from-following}

![abbonamento-segue](assets/subscription-following.png)

Il **Segui** fornisce un mezzo per seguire le voci come attività, abbonamenti e/o notifiche. Ogni volta che **Segui** è selezionato, è possibile attivare o disattivare una selezione.

Se è selezionato un metodo qualsiasi di seguito, il testo del pulsante diventa **Segue**. Per comodità, è possibile selezionare `Unfollow All` per disattivare tutti i metodi.

Il **Segui** includerà il pulsante `Email Subscriptions` opzione solo quando un forum, un QnA o un blog è configurato per abilitare gli abbonamenti e-mail. Questo pulsante viene visualizzato:

* Nella pagina delle funzioni principale del forum, del QnA o del blog abilitato, verrà inviata un’e-mail per tutte le attività che rientrano in tale funzione.

* Per una voce specifica, ad esempio un argomento forum, una domanda di controllo qualità o un articolo di blog Invierà un’e-mail quando c’è attività per quella voce specifica.

## Rispondi per e-mail {#reply-by-email}

Quando l’e-mail è [configurato per rispondere tramite e-mail](email.md#configure-polling-importer), il membro che si è iscritto riceverà un’e-mail con i contenuti pubblicati e un collegamento ai contenuti online.

Se rispondono all&#39;e-mail, il contenuto immesso nella risposta verrà visualizzato come contenuto in linea.

![risposta e-mail](assets/email-reply.png)

Il tempo necessario per la pubblicazione di una risposta è controllato dal [intervallo di aggiornamento dell&#39;importazione polling](email.md#configure-polling-importer).

![QA](assets/qa.png)
