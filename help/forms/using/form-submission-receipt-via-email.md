---
title: Invio di una conferma dell’invio di un modulo via e-mail
seo-title: Sending a form submission acknowledgement via email
description: AEM Forms consente di configurare l’azione di invio tramite e-mail che invia una conferma all’utente al momento dell’invio del modulo.
seo-description: AEM Forms allows you to configure the email submit action that sends an acknowledgement to a user on submitting the form.
uuid: c80b1ef4-8fe3-48e0-8fc6-3032dc022a38
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 574de3d5-69ba-4e2f-a8ab-c59f357e4386
docset: aem65
exl-id: bca4044a-18a9-4b97-92de-eff1e9a840f9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 0%

---

# Invio di una conferma dell’invio di un modulo via e-mail {#sending-a-form-submission-acknowledgement-via-email}

## Invio di dati del modulo adattivo {#adaptive-form-data-submission}

I moduli adattivi forniscono diversi elementi predefiniti [invia azioni](../../forms/using/configuring-submit-actions.md) flussi di lavoro per l’invio dei dati del modulo a endpoint diversi.

Ad esempio, il **[!UICONTROL Invia e-mail]** l’azione invia invia un’e-mail dopo l’invio di un modulo adattivo. Può anche essere configurato per inviare i dati del modulo e PDF nell’e-mail.

Questo articolo descrive i passaggi per abilitare l’azione E-mail su un modulo adattivo e le diverse configurazioni che fornisce.

>[!NOTE]
>
>È inoltre possibile utilizzare **[!UICONTROL Invia PDF tramite e-mail]** opzione per inviare il modulo completato tramite e-mail come allegato PDF. Le opzioni di configurazione disponibili per questa azione sono le stesse opzioni disponibili per la **[!UICONTROL Invia e-mail]** azione. L’azione E-mail PDF è disponibile solo per i moduli adattivi basati su XFA

## Invia azione e-mail {#email-action}

L’azione Invia e-mail consente all’autore di inviare automaticamente e-mail a uno o più destinatari dopo l’invio corretto di un modulo adattivo.

>[!NOTE]
>
>Per utilizzare l’azione Invia e-mail, è necessario configurare il servizio di posta AEM come descritto in [Configurazione del servizio di posta](/help/sites-administering/notification.md#configuring-the-mail-service).

### Abilitazione dell’azione Invia e-mail su un modulo adattivo {#enabling-email-action-on-an-adaptive-form}

1. Apri un modulo adattivo in **[!UICONTROL modifica]** modalità.

1. In **[!UICONTROL Contenuto]** tocca **[!UICONTROL Contenitore modulo]** e toccare ![configurare](assets/configure-icon.svg) per visualizzare le proprietà del modulo adattivo.

1. In **[!UICONTROL Invio]** sezione , seleziona **[!UICONTROL Invia e-mail]** dal **[!UICONTROL Invia azione]** elenco a discesa.

   ![Inviare azioni](assets/submission-actions.png)

1. Specifica di ID e-mail validi nella **[!UICONTROL A]**, **[!UICONTROL CC]** e **[!UICONTROL CCN]** campi.

   Specifica l’oggetto e il corpo dell’e-mail nel **[!UICONTROL Oggetto]** e **[!UICONTROL Modello e-mail]** rispettivamente.

   È inoltre possibile specificare segnaposto variabili nei campi. In tal caso, i valori dei campi vengono elaborati quando un utente finale invia correttamente il modulo. Per ulteriori informazioni, consulta [Utilizzo dei nomi dei campi del modulo adattivo per creare in modo dinamico contenuti e-mail](../../forms/using/form-submission-receipt-via-email.md#p-using-adaptive-form-field-names-to-dynamically-create-email-content-p).

   Seleziona **[!UICONTROL Includi allegati]** se il modulo include allegati di file e si desidera allegare tali file nell&#39;e-mail.

   >[!NOTE]
   >
   >Se scegli la **[!UICONTROL Invia PDF tramite e-mail]** è necessario selezionare l&#39;opzione Includi allegati.

1. Fai clic su ![save](assets/save_icon.svg) per salvare le modifiche.

### Utilizzo dei nomi dei campi del modulo adattivo per creare in modo dinamico contenuti e-mail {#using-adaptive-form-field-names-to-dynamically-create-email-content}

I nomi di campo in un modulo adattivo sono denominati segnaposto che vengono sostituiti con il valore di tale campo dopo l’invio del modulo da parte dell’utente.

In **[!UICONTROL Invia e-mail]** è possibile utilizzare segnaposto elaborati al momento dell&#39;esecuzione dell&#39;azione. Ciò implica che le intestazioni dell&#39;e-mail (come **[!UICONTROL A]**, **[!UICONTROL CC]**, **[!UICONTROL CCN]**, **[!UICONTROL Oggetto]**) vengono generate al momento dell’invio del modulo da parte dell’utente.

Per definire un segnaposto, specificare `${<field name>}` in un campo dopo aver selezionato **[!UICONTROL Invia e-mail]** come azione di invio.

Ad esempio, se il modulo contiene **[!UICONTROL Indirizzo e-mail]** campo denominato `email_addr`, per acquisire l’ID e-mail di un utente, puoi specificare quanto segue in **[!UICONTROL A]**, **[!UICONTROL CC]** oppure **[!UICONTROL CCN]** campi.

`${email_addr}`

Quando un utente invia il modulo, viene inviata un’e-mail all’ID e-mail immesso nel `email_addr` campo del modulo.

>[!NOTE]
>
>Puoi trovare il nome di un campo nella **[!UICONTROL Modifica]** finestra di dialogo per il campo .

I segnaposto variabili possono essere utilizzati anche nella variabile **[!UICONTROL Oggetto]** e **[!UICONTROL Modello e-mail]** campi.

Esempio:

`Hi ${first_name} ${last_name},`

`Your form has been received by our department. It usually takes ten business days to process the request.`

`Regards`

`Administrator`

>[!NOTE]
>
>I campi nei pannelli ripetibili non possono essere utilizzati come segnaposto variabili.
