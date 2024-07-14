---
title: Invio di una conferma per l’invio di un modulo tramite e-mail
description: AEM Forms consente di configurare l’azione di invio e-mail che invia una conferma a un utente al momento dell’invio del modulo.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
exl-id: bca4044a-18a9-4b97-92de-eff1e9a840f9
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 0%

---

# Invio di una conferma per l’invio di un modulo tramite e-mail {#sending-a-form-submission-acknowledgement-via-email}

## Invio di dati per moduli adattivi {#adaptive-form-data-submission}

Moduli adattivi fornisce diversi flussi di lavoro predefiniti di [invio](../../forms/using/configuring-submit-actions.md) per l&#39;invio dei dati del modulo a endpoint diversi.

Ad esempio, l&#39;azione di invio **[!UICONTROL Invia e-mail]** invia un messaggio e-mail in caso di invio corretto di un modulo adattivo. Può anche essere configurato per inviare i dati del modulo e il PDF nell’e-mail.

Questo articolo descrive i passaggi necessari per abilitare l’azione E-mail su un modulo adattivo e le diverse configurazioni fornite.

>[!NOTE]
>
>È inoltre possibile utilizzare l&#39;opzione **[!UICONTROL Invia PDF tramite posta elettronica]** per inviare il modulo completato tramite posta elettronica come allegato PDF. Le opzioni di configurazione disponibili per questa azione sono le stesse disponibili per l&#39;azione **[!UICONTROL Invia e-mail]**. L’azione E-mail PDF è disponibile solo per i moduli adattivi basati su XFA

## Azione Invia e-mail {#email-action}

L’azione Invia e-mail consente all’autore di inviare automaticamente e-mail a uno o più destinatari in caso di invio corretto di un modulo adattivo.

>[!NOTE]
>
>Per utilizzare l&#39;azione Invia e-mail, è necessario configurare il servizio di posta AEM come descritto in [Configurazione del servizio di posta](/help/sites-administering/notification.md#configuring-the-mail-service).

### Abilitazione dell’azione Invia e-mail su un modulo adattivo {#enabling-email-action-on-an-adaptive-form}

1. Apri un modulo adattivo in modalità **[!UICONTROL modifica]**.

1. Nella scheda **[!UICONTROL Contenuto]**, seleziona **[!UICONTROL Contenitore modulo]** e ![configura](assets/configure-icon.svg) per visualizzare le proprietà del modulo adattivo.

1. Nella sezione **[!UICONTROL Invio]**, seleziona **[!UICONTROL Invia e-mail]** dall&#39;elenco a discesa **[!UICONTROL Invia azione]**.

   ![Invia azioni](assets/submission-actions.png)

1. Specifica ID e-mail validi nei campi **[!UICONTROL To]**, **[!UICONTROL CC]** e **[!UICONTROL BCC]**.

   Specifica l&#39;oggetto e il corpo dell&#39;e-mail rispettivamente nei campi **[!UICONTROL Oggetto]** e **[!UICONTROL Modello e-mail]**.

   È inoltre possibile specificare segnaposto variabili nei campi, nel qual caso i valori dei campi vengono elaborati quando il modulo viene inviato correttamente da un utente finale. Per ulteriori informazioni, vedere [Utilizzo di nomi di campi modulo adattivo per creare in modo dinamico contenuto e-mail](../../forms/using/form-submission-receipt-via-email.md#p-using-adaptive-form-field-names-to-dynamically-create-email-content-p).

   Selezionare **[!UICONTROL Includi allegati]** se il modulo include file allegati e si desidera allegarli all&#39;e-mail.

   >[!NOTE]
   >
   >Se si sceglie l&#39;opzione **[!UICONTROL Invia PDF tramite posta elettronica]**, è necessario selezionare l&#39;opzione Includi allegati.

1. Fai clic su ![salva](assets/save_icon.svg) per salvare le modifiche.

### Utilizzo dei nomi dei campi del modulo adattivo per creare in modo dinamico contenuti e-mail {#using-adaptive-form-field-names-to-dynamically-create-email-content}

I nomi dei campi in un modulo adattivo sono denominati segnaposto e vengono sostituiti con il valore del campo dopo che un utente ha inviato il modulo.

Nell&#39;azione **[!UICONTROL Invia e-mail]** è possibile utilizzare segnaposto elaborati durante l&#39;esecuzione dell&#39;azione. Ciò implica che le intestazioni dell&#39;e-mail (ad esempio **[!UICONTROL To]**, **[!UICONTROL CC]**, **[!UICONTROL BCC]**, **[!UICONTROL Subject]**) vengono generate quando l&#39;utente invia il modulo.

Per definire un segnaposto, specificare `${<field name>}` in un campo dopo aver selezionato **[!UICONTROL Invia e-mail]** come azione di invio.

Ad esempio, se il modulo contiene il campo **[!UICONTROL Indirizzo e-mail]**, denominato `email_addr`, per l&#39;acquisizione dell&#39;ID e-mail di un utente, è possibile specificare quanto segue nei campi **[!UICONTROL To]**, **[!UICONTROL CC]** o **[!UICONTROL BCC]**.

`${email_addr}`

Quando un utente invia il modulo, viene inviata un’e-mail all’ID e-mail immesso nel campo `email_addr` del modulo.

>[!NOTE]
>
>Puoi trovare il nome di un campo nella finestra di dialogo **[!UICONTROL Modifica]** per il campo.

I segnaposto delle variabili possono essere utilizzati anche nei campi **[!UICONTROL Oggetto]** e **[!UICONTROL Modello e-mail]**.

Ad esempio:

`Hi ${first_name} ${last_name},`

`Your form has been received by our department. It usually takes ten business days to process the request.`

`Regards`

`Administrator`

>[!NOTE]
>
>I campi nei pannelli ripetibili non possono essere utilizzati come segnaposto per le variabili.
