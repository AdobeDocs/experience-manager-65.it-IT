---
title: Utilizzare modelli e-mail personalizzati in un passaggio Assegna attività
description: Modelli e-mail personalizzati per le notifiche e-mail del flusso di lavoro dei moduli
topic-tags: publish
docset: aem65
exl-id: d4035c91-ee8d-4f12-bdac-e3912be732d7
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 0%

---

# Utilizzare modelli e-mail personalizzati in un passaggio Assegna attività{#use-custom-email-templates-in-an-assign-task-step}

È possibile utilizzare il passaggio Assegna attività per creare e assegnare attività a un utente o a un gruppo. Quando un’attività viene assegnata a un utente o a un gruppo, viene inviata una notifica e-mail all’utente definito o a ciascun membro del gruppo definito. Una tipica notifica e-mail contiene il collegamento dell’attività assegnata e le informazioni relative all’attività. L’immagine seguente mostra un esempio di notifica e-mail:

![Notifica e-mail con modello predefinito](do-not-localize/default_email_template_new.png)

Puoi personalizzare l’aspetto e utilizzare metadati personalizzati in una notifica e-mail. AEM Forms fornisce un modello preconfigurato per le notifiche e-mail. Puoi personalizzare il modello preconfigurato o crearne uno nuovo.

I modelli di notifica e-mail si basano su [E-mail HTML](https://en.wikipedia.org/wiki/HTML_email). Queste e-mail si adattano a client e-mail e dimensioni di schermo diversi. Inoltre, lo stile dell’e-mail è definito all’interno del modello.

L’immagine seguente mostra una notifica e-mail personalizzata:

![Notifica e-mail tramite modello personalizzato](do-not-localize/customized-email.png)

## Personalizza il modello esistente {#customize-the-existing-template}

AEM Forms fornisce automaticamente un modello per le notifiche e-mail. Il modello fornisce la descrizione del titolo, la data di scadenza, la priorità, il nome del flusso di lavoro e il collegamento dell&#39;attività assegnata. Potete personalizzare il modello per modificare l&#39;aspetto. Per personalizzare il modello, effettua le seguenti operazioni:

1. Accedi a CRXDE con l’account amministratore.

1. Passa a /libs/fd/dashboard/templates/email.

1. Apri il file htmlEmailTemplate.txt. Contiene il modello predefinito.

1. Sostituisci il contenuto del file htmlEmailTemplate.txt con contenuto personalizzato.

   Un modello di notifica e-mail è un [E-mail HTML](https://en.wikipedia.org/wiki/HTML_email). Per modificare l’aspetto del modello, puoi sostituire il codice html esistente con il codice personalizzato.

1. Salva il file. Ora il modello personalizzato è pronto per l’uso.

## Creare un modello e-mail {#create-an-email-template}

AEM Forms fornisce automaticamente un modello per le notifiche e-mail. Il modello fornisce la descrizione del titolo, la data di scadenza, la priorità, il nome del flusso di lavoro e il collegamento dell&#39;attività assegnata. Puoi anche aggiungere un modello e-mail personalizzato (il tuo) per i passaggi dell’attività Assegna. Per aggiungere un modello e-mail personalizzato, effettua le seguenti operazioni:

1. Accedi a CRXDE con l’account amministratore.

1. Passa a /libs/fd/dashboard/templates/email.

1. Crea un file .txt. Ad esempio, EmailOnTaskAssign.txt.

1. Aggiungi al file un codice HTML personalizzato.

   Un modello di notifica e-mail è un [E-mail HTML](https://en.wikipedia.org/wiki/HTML_email). Puoi aggiungere al file un codice HTML personalizzato per creare un modello.

1. Salva il file. Il modello è pronto per essere utilizzato nel passaggio Assegna attività.

## Utilizzare un modello e-mail in un passaggio Assegna attività {#use-an-email-template-in-an-assign-task-step}

Il passaggio Assegna attività è configurato per l’utilizzo del modello predefinito htmlEmailTemplate.txt. Puoi scegliere di utilizzare un modello personalizzato. Per modificare il modello:

1. Apri il passaggio Assegna attività.

1. Passa a Assegnatario > Modello e-mail HTML.

1. Seleziona il modello e-mail di HTML appena creato.

1. Fare clic su OK. Il modello viene modificato.

Una notifica e-mail utilizza anche [metadati](../../forms/using/use-metadata-in-email-notifications.md). Ad esempio, data di scadenza, priorità, nome del flusso di lavoro e altro ancora. Puoi anche configurare il modello da utilizzare [metadati personalizzati](../../forms/using/use-metadata-in-email-notifications.md#using-custom-metadata-in-an-email-notification).
