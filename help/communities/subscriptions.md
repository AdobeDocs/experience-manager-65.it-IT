---
title: Iscrizioni alle community
description: I membri della community interagiscono con altri membri tramite e-mail
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 338be220-659a-459c-8e90-55e3a11ddeb0
solution: Experience Manager
feature: Communities
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 1%
---
# Iscrizioni alle community {#communities-subscriptions}

## Panoramica {#overview}

A partire da Communities [FP1](deploy-communities.md#latestfeaturepack), i membri della community possono interagire con la community tramite e-mail utilizzando una funzione definita come abbonamenti.

Gli abbonamenti sono simili alle [notifiche](notifications.md) in quanto i membri possono sottoscrivere quando seguono articoli di blog, argomenti dei forum o domande di qualità.

Ciò che distingue gli abbonamenti dalle notifiche è:

* I membri non possono sottoscrivere un abbonamento quando seguono altri membri.
* L&#39;unica azione che i membri possono eseguire è selezionare `Email Subscriptions` quando si esegue l&#39;operazione seguente.
* Una volta configurata la risposta e-mail, i membri possono pubblicare efficacemente il contenuto semplicemente rispondendo all’e-mail ricevuta.

### Requisiti {#requirements}

**Configura e-mail**

Affinché gli abbonamenti siano funzionali, è necessario configurare l’indirizzo e-mail e consentire ai membri di rispondere per e-mail.

Per istruzioni sulla configurazione dell&#39;e-mail, vedere [Configurazione dell&#39;e-mail](email.md).

**Abilita sottoscrizioni e segui**

I componenti devono essere configurati per abilitare le sottoscrizioni *e* dopo. Le funzionalità che consentono gli abbonamenti sono [blog](blog-feature.md), [forum](forum.md) e [QnA](working-with-qna.md).

## Abbonamenti da Segui {#subscriptions-from-following}

![abbonamento-successivo](assets/subscription-following.png)

Il pulsante **Segui** consente di seguire le voci come attività, abbonamenti e/o notifiche. Ogni volta che il pulsante **Segui** è selezionato, è possibile attivare o disattivare una selezione.

Se è selezionato un metodo qualsiasi di seguire, il testo del pulsante diventa **Segue**. Per comodità, è possibile selezionare `Unfollow All` per disattivare tutti i metodi.

Il pulsante **Segui** includerà l&#39;opzione `Email Subscriptions` solo quando un forum, un QnA o un blog è configurato per abilitare gli abbonamenti e-mail. Questo pulsante viene visualizzato:

* Nella pagina delle funzioni principale del forum, del QnA o del blog abilitato, verrà inviata un’e-mail per tutte le attività che rientrano in tale funzione.

* Per una voce specifica, ad esempio un argomento forum, una domanda di controllo qualità o un articolo di blog Invierà un’e-mail quando c’è attività per quella voce specifica.

## Rispondi per e-mail {#reply-by-email}

Quando l&#39;indirizzo e-mail è [configurato per rispondere tramite e-mail](email.md#configure-polling-importer), il membro che si è iscritto riceverà un&#39;e-mail con il contenuto pubblicato e un collegamento al contenuto online.

Se rispondono all&#39;e-mail, il contenuto immesso nella risposta verrà visualizzato come contenuto in linea.

![risposta e-mail](assets/email-reply.png)

Il tempo necessario per la pubblicazione di una risposta è controllato dall&#39;[intervallo di aggiornamento dell&#39;importazione polling](email.md#configure-polling-importer).

![QA](assets/qa.png)
