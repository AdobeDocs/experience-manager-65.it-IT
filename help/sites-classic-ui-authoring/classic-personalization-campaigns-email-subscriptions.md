---
title: Gestione delle sottoscrizioni
description: Gli utenti possono essere invitati ad iscriversi alle mailing list del fornitore di servizi e-mail con l’aiuto del componente Modulo utilizzato in una pagina web dell’AEM. Per preparare una pagina AEM con un modulo di iscrizione per l'iscrizione alle mailing list del servizio di posta elettronica, è necessario applicare la configurazione del servizio corrispondente alla pagina AEM visitata dal potenziale abbonato.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: add05d22-3a11-49e9-a554-2315962552d5
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '917'
ht-degree: 1%

---

# Gestione delle sottoscrizioni{#managing-subscriptions}

>[!NOTE]
>
>Adobe non prevede di migliorare ulteriormente questa funzionalità (Gestione di lead ed elenchi).
>Si consiglia di utilizzare [Adobe Campaign e la relativa integrazione AEM](/help/sites-administering/campaign.md).

Agli utenti può essere richiesto di iscriversi alle mailing list **del provider di servizi e-mail** con l&#39;aiuto del componente **Modulo** utilizzato in una pagina Web AEM. Per preparare una pagina AEM con un modulo di iscrizione per l&#39;iscrizione alle mailing list del servizio di posta elettronica, è necessario applicare la configurazione del servizio corrispondente alla pagina AEM visitata dal potenziale abbonato.

## Applicazione della configurazione del servizio e-mail a una pagina {#applying-email-service-configuration-to-a-page}

Per configurare una pagina AEM:

1. Passare alla scheda **Siti Web**.
1. Seleziona la pagina da configurare per il servizio. Fare clic con il pulsante destro del mouse sulla pagina e selezionare **Proprietà**.

1. Seleziona **Cloud Service** e quindi **Aggiungi servizio**. Seleziona una configurazione dall’elenco delle configurazioni disponibili.

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. Fai clic su **OK**.

## Creazione di un modulo di iscrizione a una pagina AEM per iscriversi/annullare l’iscrizione agli elenchi {#creating-a-sign-up-form-on-an-aem-page-for-subscribing-unsubscribing-to-lists}

Per creare un modulo di iscrizione e configurarlo per gli abbonamenti alle mailing list del provider di servizi e-mail:

1. Apri la pagina dell’AEM che verrà visitata dall’utente.
1. Applica alla pagina la configurazione del provider di servizi e-mail.

1. Aggiungi un componente **Modulo** alla pagina trascinando il componente dalla barra laterale. Se il componente non è disponibile, passare alla modalità progettazione e abilitare il gruppo **Modulo**.
1. Fai clic su **Modifica** nella barra **Inizio modulo** e passa alla scheda **Avanzate**.
1. Nel menu a discesa **Modulo**, selezionare **Servizio di posta elettronica: crea sottoscrittore** e aggiungi all&#39;elenco.
1. Nella parte inferiore della finestra di dialogo, apri il menu a discesa **Configurazione azione**, che consente di selezionare uno o più elenchi di iscrizioni.
1. In **Seleziona elenco**, selezionare l&#39;elenco a cui si desidera che gli utenti effettuino la sottoscrizione. È possibile aggiungere più elenchi utilizzando il pulsante più (**Aggiungi elemento**).

   ![chlimage_1-10](assets/chlimage_1-10.jpeg)

   >[!NOTE]
   >
   >La finestra di dialogo può variare a seconda del provider di servizi di posta elettronica.

1. Nella scheda **Modulo** selezionare la pagina di ringraziamento a cui si desidera che gli utenti accedano dopo aver inviato il modulo. Se non si specifica alcun valore, il modulo verrà visualizzato nuovamente dopo l&#39;invio. Fare clic su **OK**. Nel modulo viene visualizzato un componente **ID e-mail** che consente di creare un modulo in cui gli utenti possono inviare i propri indirizzi e-mail per iscriversi o annullare l&#39;iscrizione a una mailing list.
1. Aggiungi il componente pulsante **Invia** dalla sezione **Modulo** nella barra laterale.

   Modulo pronto. Publish la pagina configurata nei passaggi precedenti insieme alla pagina **grazie** all&#39;istanza Publish. Tutti i potenziali abbonati che visitano la pagina possono compilare il modulo e iscriversi all’elenco fornito nella configurazione.

   >[!NOTE]
   >
   >Per eseguire correttamente la sottoscrizione del modulo, è necessario esportare e importare [le chiavi di crittografia dell&#39;autore nell&#39;istanza di pubblicazione](#exporting-keys-from-author-and-importing-on-publish).

## Esportazione delle chiavi dall’ambiente di authoring e importazione al momento della pubblicazione {#exporting-keys-from-author-and-importing-on-publish}

Affinché l’abbonamento e l’annullamento dell’abbonamento al servizio di posta elettronica funzionino tramite il modulo di abbonamento nell’istanza di pubblicazione, è necessario seguire questi passaggi:

1. Nell’istanza di authoring, passa a Gestione pacchetti.
1. Crea un pacchetto. Impostare il filtro come `/etc/key`.
1. Genera e scarica il pacchetto.
1. Passa a Gestione pacchetti nell’istanza di pubblicazione e carica questo pacchetto.
1. Passa alla console Publish osgi e riavvia il bundle denominato **Adobe Granite Crypto Support**.

## Annullamento dell’iscrizione degli utenti agli elenchi {#unsubscribing-users-from-lists}

Per annullare l’iscrizione degli utenti agli elenchi:

1. Apri le proprietà della pagina dell’AEM contenente il modulo di iscrizione per annullare l’iscrizione di un lead.
1. Applica la configurazione del servizio alla pagina.
1. Crea un modulo di iscrizione sulla pagina.
1. Durante la configurazione del componente, selezionare l&#39;azione **Servizio di posta elettronica**: **Annulla sottoscrizione utente da elenco.**
1. Dal menu a discesa, seleziona l’elenco appropriato da cui l’utente verrà rimosso al momento dell’annullamento dell’abbonamento.

   ![chlimage_1-11](assets/chlimage_1-11.jpeg)

1. Esporta le chiavi dall’autore alla pubblicazione.

## Configurazione delle e-mail di risposta automatica per il servizio e-mail {#configuring-auto-responder-emails-for-email-service}

Per configurare un messaggio e-mail di risposta automatica per un abbonato:

1. Apri le proprietà della pagina dell’AEM che dispongono del modulo di iscrizione per configurare il risponditore automatico per un lead.
1. Applica la configurazione ExactTarget alla pagina.

1. Aggiungi un componente **Modulo** alla pagina trascinando il componente dalla barra laterale. Se il componente non è disponibile, passare alla modalità progettazione e abilitare il gruppo **Modulo**.
1. Fai clic su **Modifica** nella barra **Inizio modulo** e passa alla scheda **Avanzate**.
1. Nel menu a discesa **Modulo**, selezionare **Servizio di posta elettronica: invia messaggio di posta elettronica con risposta automatica.**
1. **Selezionare un&#39;e-mail** (questa è l&#39;e-mail inviata come risposta automatica).

1. **Seleziona classificazione** (questa classificazione viene utilizzata per inviare l&#39;e-mail).
1. Seleziona la pagina **Grazie** (la pagina a cui gli utenti vengono indirizzati una volta inviato il modulo).

   Nella scheda **Modulo**, seleziona la pagina di ringraziamento a cui desideri che gli utenti vadano dopo aver inviato il modulo. Se non specificato, il modulo viene visualizzato nuovamente dopo l&#39;invio. Fai clic su **OK**.

1. Esporta le chiavi dall’autore alla pubblicazione.
1. Aggiungi il componente pulsante **Invia** dalla sezione **Modulo** nella barra laterale.

   Il modulo di iscrizione è pronto. Publish la pagina configurata nei passaggi precedenti insieme alla pagina **grazie** all&#39;istanza Publish. Tutti i potenziali abbonati che visitano la pagina possono compilare il modulo e all’invio del modulo il visitatore riceverà un’e-mail di risposta automatica sull’ID e-mail compilato nel modulo.

   >[!NOTE]
   >
   >Per garantire il corretto funzionamento della sottoscrizione del modulo di registrazione, è necessario esportare e importare [le chiavi di crittografia dell&#39;autore nell&#39;istanza di pubblicazione](#exporting-keys-from-author-and-importing-on-publish).

   ![chlimage_1-12](assets/chlimage_1-12.jpeg)
