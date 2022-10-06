---
title: Gestione delle registrazioni
seo-title: Managing Subscriptions
description: Agli utenti può essere chiesto di iscriversi alle mailing list del Fornitore di servizi e-mail con l’aiuto del componente Modulo utilizzato in una pagina web di AEM. Per preparare una pagina AEM con un modulo per l’iscrizione alle mailing list dei servizi di posta elettronica, è necessario applicare la configurazione del servizio corrispondente alla pagina AEM che il potenziale sottoscrittore visiterà.
seo-description: Users can be asked to subscribe to Email Service Provider's mailing lists with the help of the Form component used on an AEM web page. To prepare an AEM page with a sign-up form for subscription to your e-mail service mailing lists, you must apply the corresponding service configuration to the AEM page that the potential subscriber will visit.
uuid: b2578a3d-dba1-4114-b21a-5f34c0cccc5a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 295cb0a6-29db-42aa-824e-9141b37b5086
exl-id: add05d22-3a11-49e9-a554-2315962552d5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 73%

---

# Gestione delle registrazioni{#managing-subscriptions}

>[!NOTE]
>
>Adobe non prevede di migliorare ulteriormente questa funzionalità (Gestione di lead ed elenchi).
>La raccomandazione è di sfruttare [Adobe Campaign e la sua integrazione AEM](/help/sites-administering/campaign.md).

È possibile chiedere agli utenti di iscriversi **Provider di servizi e-mail** mailing list con l&#39;aiuto di **Modulo** componente utilizzato in una pagina web AEM. Per preparare una pagina AEM con un modulo per l’iscrizione alle mailing list dei servizi di posta elettronica, è necessario applicare la configurazione del servizio corrispondente alla pagina AEM che il potenziale sottoscrittore visiterà.

## Applicazione della configurazione del servizio e-mail a una pagina {#applying-email-service-configuration-to-a-page}

Per configurare una pagina di AEM:

1. Passa alla scheda **Siti web**.
1. Seleziona la pagina da configurare per il servizio. Fai clic con il pulsante destro del mouse sulla pagina e seleziona **Proprietà**.

1. Seleziona **Cloud Services** then **Aggiungi servizio**. Selezionate una configurazione dall’elenco delle configurazioni disponibili.

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. Fai clic su **OK**.

## Creazione di un modulo di iscrizione su una pagina AEM per iscriversi o cancellarsi dalle liste {#creating-a-sign-up-form-on-an-aem-page-for-subscribing-unsubscribing-to-lists}

Per creare un modulo di registrazione e configurarlo per le iscrizioni alle mailing list del Fornitore di servizi e-mail:

1. Apri la pagina AEM che verrà visitata dall’utente.
1. Applica la configurazione del Fornitore di servizi e-mail alla pagina.

1. Aggiungi alla pagina un componente **Modulo** trascinandolo dalla barra laterale. Se il componente non è disponibile, passa alla modalità di progettazione e attiva il gruppo **Modulo**.
1. Fai clic su **Modifica** in **Inizio del modulo** e naviga fino al **Avanzate** scheda .
1. In **Modulo** menu a discesa, seleziona **Servizio e-mail: Crea utente con sottoscrizione** e aggiungi all&#39;elenco.
1. Nella parte inferiore della finestra di dialogo, apri le **Configurazione azione** a discesa, che consente di selezionare uno o più elenchi di sottoscrizioni.
1. In **Seleziona elenco**, seleziona la mailing list a cui iscrivere l’utente. Puoi aggiungere più elenchi utilizzando il pulsante più (**Aggiungi elemento**).

   ![chlimage_1-10](assets/chlimage_1-10.jpeg)

   >[!NOTE]
   >
   >La finestra di dialogo può variare a seconda del fornitore di servizio e-mail.

1. Nella scheda **Modulo**, seleziona la pagina di ringraziamento a cui vuoi indirizzare gli utenti quando inviano il modulo (se lasciato vuoto, il modulo mostra di nuovo l’invio. Fai clic su **OK**. Un componente **Id e-mail** viene visualizzato nel Modulo, che consente di creare un modulo in cui gli utenti possono registrare i propri indirizzi e-mail per effettuare o cancellare la sottoscrizione ad un elenco.
1. Aggiungi il componente per il pulsante **Invia** dalla sezione **Modulo** nella barra laterale.

   Il modulo ora è pronto. Pubblica la pagina configurata mediante i passaggi descritti qui sopra insieme alla pagina di **Ringraziamento** nell’istanza di pubblicazione. Gli utenti che visiteranno la pagina potranno compilare il modulo e iscriversi alla mailing list fornita nella configurazione.

   >[!NOTE]
   >
   >Affinché la funzione di iscrizione funzioni correttamente nel modulo, [occorre esportare le chiavi di codifica dall’istanza di creazione ed importarle nell’istanza di pubblicazione](#exporting-keys-from-author-and-importing-on-publish).

## Esportazione delle chiavi dall’istanza di creazione e importazione nell’istanza di pubblicazione {#exporting-keys-from-author-and-importing-on-publish}

Affinché la funzione di iscrizione e cancellazione funzioni correttamente nel modulo di registrazione dell’istanza di pubblicazione, effettua i seguenti passaggi:

1. Nell’istanza di creazione, vai a Gestione pacchetti.
1. Crea un nuovo pacchetto. Imposta il filtro come `/etc/key`.
1. Genera e scarica il pacchetto.
1. Passa a Gestione pacchetti nell’istanza di pubblicazione e carica il pacchetto.
1. Passa alla console di Pubblicazione osgi e riavvia il bundle denominato **Adobe Granite Crypto Support**.

## Cancellazione dell’iscrizione degli utenti dagli elenchi {#unsubscribing-users-from-lists}

Per cancellare la sottoscrizione degli utenti dagli elenchi:

1. Apri le proprietà della pagina AEM che contiene il modulo per la cancellazione della sottoscrizione.
1. Applica alla pagina la configurazione del servizio.
1. Crea un modulo di iscrizione sulla pagina.
1. Durante la configurazione del componente, seleziona l’azione . **Servizio e-mail**: **Annulla l’iscrizione all’elenco degli utenti.**
1. Dal menu a discesa, seleziona la mailing list da cui dovrà essere rimosso l’utente.

   ![chlimage_1-11](assets/chlimage_1-11.jpeg)

1. Esporta le chiavi dall’istanza di creazione all’istanza di pubblicazione.

## Configurazione di messaggi di risposta automatica per il servizio e-mail {#configuring-auto-responder-emails-for-email-service}

Per configurare un messaggio e-mail di risposta automatica quando un utente si iscrive:

1. Apri le proprietà della pagina AEM che dispone del modulo di registrazione per configurare la risposta automatica per un lead.
1. Applicate alla pagina la configurazione ExactTarget.

1. Aggiungi alla pagina un componente **Modulo** trascinandolo dalla barra laterale. Se il componente non è disponibile, passa alla modalità di progettazione e attiva il gruppo **Modulo**.
1. Fai clic su **Modifica** in **Inizio del modulo** e naviga fino al **Avanzate** scheda .
1. In **Modulo** menu a discesa, seleziona **Servizio e-mail: Invia messaggio di risposta automatica.**
1. **Selezionare un messaggio e-mail** (si tratta dell’e-mail inviata come risposta automatica).

1. **Seleziona classificazione** (classificazione utilizzata per inviare l’e-mail).
1. Seleziona la **Grazie** (pagina a cui vengono indirizzati gli utenti dopo l’invio del modulo).

   In **Modulo** selezionare la pagina di ringraziamento a cui si desidera indirizzare gli utenti dopo l’invio del modulo. Se lasciato vuoto, il modulo viene visualizzato nuovamente al momento dell’invio. Fai clic su **OK**.

1. Esporta le chiavi dall’istanza di creazione all’istanza di pubblicazione.
1. Aggiungi il componente per il pulsante **Invia** dalla sezione **Modulo** nella barra laterale.

   Il modulo d’iscrizione è pronto. Pubblica la pagina configurata mediante i passaggi descritti qui sopra insieme alla pagina di **Ringraziamento** nell’istanza di pubblicazione. I potenziali sottoscrittori che visitano la pagina possono compilare il modulo e dopo l’invio riceveranno il messaggio e-mail di risposta automatica, all’ID e-mail inserito nel modulo.

   >[!NOTE]
   >
   >Affinché la funzione di iscrizione funzioni correttamente nel modulo, [occorre esportare le chiavi di codifica dall’istanza di creazione ed importarle nell’istanza di pubblicazione](#exporting-keys-from-author-and-importing-on-publish).

   ![chlimage_1-12](assets/chlimage_1-12.jpeg)
