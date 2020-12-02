---
title: Utilizzare modelli e-mail personalizzati in un passaggio Assegna attività
seo-title: Utilizzare modelli e-mail personalizzati in un passaggio Assegna attività
description: 'Modelli e-mail personalizzati per le notifiche e-mail del flusso di lavoro dei moduli '
seo-description: 'Modelli e-mail personalizzati per le notifiche e-mail del flusso di lavoro dei moduli '
uuid: ba453d54-813f-4a4f-a82e-1a6a28b6939c
topic-tags: publish
discoiquuid: 2ad4b7b5-2162-4599-af3f-9476f1256de6
docset: aem65
translation-type: tm+mt
source-git-commit: 76908a565bf9e6916db39d7db23c04d2d40b3247
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 0%

---


# Utilizzare i modelli di e-mail personalizzati in un passaggio Assegnazione attività{#use-custom-email-templates-in-an-assign-task-step}

È possibile utilizzare il passaggio Assegna attività per creare e assegnare attività a un utente o a un gruppo. Quando un&#39;attività viene assegnata a un utente o gruppo, viene inviata una notifica e-mail all&#39;utente definito o a ciascun membro del gruppo definito. Una tipica notifica e-mail contiene il collegamento dell’attività assegnata e le informazioni relative all’attività. L&#39;immagine seguente mostra un esempio di notifica e-mail:

![Notifica e-mail con modello out-of-box](do-not-localize/default_email_template_new.png)

Potete personalizzare l’aspetto e utilizzare metadati personalizzati in una notifica e-mail.  AEM Forms fornisce un modello standard per le notifiche e-mail. Potete personalizzare il modello out of the box o creare un nuovo modello da zero.

I modelli di notifica e-mail si basano su [e-mail HTML](https://en.wikipedia.org/wiki/HTML_email). Tali e-mail si adattano a diversi client e-mail e dimensioni dello schermo. Inoltre, lo stile dell’e-mail è definito all’interno del modello.

L&#39;immagine seguente mostra una notifica e-mail personalizzata:

![Notifica e-mail tramite modello personalizzato](do-not-localize/customized-email.png)

## Personalizzare il modello esistente {#customize-the-existing-template}

 AEM Forms fornisce un modello per le notifiche e-mail. Il modello fornisce la descrizione del titolo, la data di scadenza, la priorità, il nome del flusso di lavoro e il collegamento dell’attività assegnata. Potete personalizzare il modello per modificarne l’aspetto. Per personalizzare il modello, effettuate le seguenti operazioni:

1. Accedete a CRXDE con l&#39;account amministratore.

1. Andate a /libs/fd/dashboard/templates/email.

1. Aprite il file htmlEmailTemplate.txt. Contiene il modello predefinito.

1. Sostituite il contenuto del file htmlEmailTemplate.txt con contenuto personalizzato.

   Un modello di notifica e-mail è un [e-mail HTML](https://en.wikipedia.org/wiki/HTML_email). Potete sostituire il codice HTML esistente con il codice personalizzato per modificare l’aspetto del modello.

1. Salvate il file. Ora, il modello personalizzato è pronto per essere utilizzato.

## Creare un modello e-mail {#create-an-email-template}

 AEM Forms fornisce un modello per le notifiche e-mail. Il modello fornisce la descrizione del titolo, la data di scadenza, la priorità, il nome del flusso di lavoro e il collegamento dell’attività assegnata. Potete anche aggiungere un modello e-mail personalizzato (il modello personalizzato) per i passaggi Assegnazione attività. Per aggiungere un modello e-mail personalizzato, effettuate le seguenti operazioni:

1. Accedete a CRXDE con l&#39;account amministratore.

1. Andate a /libs/fd/dashboard/templates/email.

1. Create un file .txt. Ad esempio, EmailOnTaskAssign.txt.

1. Aggiungete codice HTML personalizzato al file.

   Un modello di notifica e-mail è un [e-mail HTML](https://en.wikipedia.org/wiki/HTML_email). Potete aggiungere al file codice HTML personalizzato per creare un nuovo modello.

1. Salvate il file. Il modello è pronto per essere utilizzato nel passaggio Assegna attività.

## Utilizzare un modello e-mail in un passaggio Assegna attività {#use-an-email-template-in-an-assign-task-step}

Il passaggio Assegna attività è configurato per utilizzare il modello predefinito, htmlEmailTemplate.txt. Potete scegliere di utilizzare un modello personalizzato. Per modificare il modello:

1. Aprire il passaggio Assegna attività.

1. Passa a Assegnatario > Modello e-mail HTML.

1. Selezionate il modello e-mail HTML appena creato.

1. Fai clic su OK. Il modello viene modificato.

Una notifica e-mail utilizza anche [metadata](../../forms/using/use-metadata-in-email-notifications.md). Ad esempio, data di scadenza, priorità, nome del flusso di lavoro e altro. Potete inoltre configurare il modello in modo che utilizzi [metadati personalizzati](../../forms/using/use-metadata-in-email-notifications.md#using-custom-metadata-in-an-email-notification).
