---
title: Invio di un avviso di invio del modulo tramite e-mail
seo-title: Invio di un avviso di invio del modulo tramite e-mail
description: ' AEM Forms consente di configurare l''azione di invio tramite e-mail che invia un messaggio di conferma all''utente al momento dell''invio del modulo.'
seo-description: ' AEM Forms consente di configurare l''azione di invio tramite e-mail che invia un messaggio di conferma all''utente al momento dell''invio del modulo.'
uuid: c80b1ef4-8fe3-48e0-8fc6-3032dc022a38
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 574de3d5-69ba-4e2f-a8ab-c59f357e4386
docset: aem65
translation-type: tm+mt
source-git-commit: acc2a3977353386d7e1dfd1344a61d78812fe3fc
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 0%

---


# Invio di un avviso di invio del modulo tramite e-mail {#sending-a-form-submission-acknowledgement-via-email}

## Invio dati modulo adattivo {#adaptive-form-data-submission}

I moduli adattivi forniscono diversi flussi di lavoro [per l&#39;invio di azioni](../../forms/using/configuring-submit-actions.md) pronte all&#39;uso per l&#39;invio dei dati del modulo a endpoint diversi.

Ad esempio, l&#39;azione di invio **[!UICONTROL Invia e-mail]** invia un messaggio e-mail all&#39;invio corretto di un modulo adattivo. È inoltre possibile configurare l&#39;invio tramite e-mail dei dati del modulo e del PDF.

Questo articolo descrive in dettaglio i passaggi per attivare l’azione E-mail su un modulo adattivo e le diverse configurazioni che fornisce.

>[!NOTE]
>
>È inoltre possibile utilizzare l&#39;opzione **[!UICONTROL Invia PDF tramite e-mail]** per inviare il modulo compilato via e-mail come allegato PDF. Le opzioni di configurazione disponibili per questa azione sono le stesse opzioni disponibili per l&#39;azione **[!UICONTROL Invia e-mail]**. L&#39;azione e-mail PDF è disponibile solo per i moduli adattivi basati su XFA

## Invia azione e-mail {#email-action}

L’azione Invia e-mail consente all’autore di inviare automaticamente e-mail a uno o più destinatari all’invio corretto di un modulo adattivo.

>[!NOTE]
>
>Per utilizzare l&#39;azione Invia e-mail, è necessario configurare il servizio di posta AEM come descritto in [Configurazione del servizio di posta ](/help/sites-administering/notification.md#configuring-the-mail-service).

### Abilitazione di Invia azione e-mail su un modulo adattivo {#enabling-email-action-on-an-adaptive-form}

1. Aprire un modulo adattivo in modalità **[!UICONTROL modifica]**.

1. Nella scheda **[!UICONTROL Contenuto]**, toccare **[!UICONTROL Contenitore modulo]** e toccare ![Configura](assets/configure-icon.svg) per visualizzare le proprietà del modulo adattivo.

1. Nella sezione **[!UICONTROL Invio]**, selezionare **[!UICONTROL Invia e-mail]** dall&#39;elenco a discesa **[!UICONTROL Invia azione]**.

   ![Invia azioni](assets/submission-actions.png)

1. Specificate ID e-mail validi nei campi **[!UICONTROL A]**, **[!UICONTROL CC]** e **[!UICONTROL CCN]**.

   Specificate l&#39;oggetto e il corpo dell&#39;e-mail rispettivamente nei campi **[!UICONTROL Subject]** e **[!UICONTROL Email Template]**.

   È inoltre possibile specificare segnaposto variabili nei campi, nel qual caso i valori dei campi vengono elaborati quando l&#39;utente finale invia correttamente il modulo. Per ulteriori informazioni, vedere [Uso dei nomi dei campi modulo adattivi per creare contenuti e-mail in modo dinamico](../../forms/using/form-submission-receipt-via-email.md#p-using-adaptive-form-field-names-to-dynamically-create-email-content-p).

   Selezionare **[!UICONTROL Includi allegati]** se il modulo include file allegati e si desidera allegare tali file nell&#39;e-mail.

   >[!NOTE]
   >
   >Se si sceglie l&#39;opzione **[!UICONTROL Invia PDF tramite e-mail]**, è necessario selezionare l&#39;opzione Includi allegati.

1. Fare clic su ![Salva](assets/save_icon.svg) per salvare le modifiche.

### Utilizzo dei nomi dei campi modulo adattivi per creare in modo dinamico contenuto e-mail {#using-adaptive-form-field-names-to-dynamically-create-email-content}

I nomi dei campi di un modulo adattivo sono denominati segnaposto che vengono sostituiti con il valore di tale campo dopo l&#39;invio del modulo da parte dell&#39;utente.

Nell&#39;azione **[!UICONTROL Invia e-mail]**, è possibile utilizzare i segnaposto elaborati al momento dell&#39;esecuzione dell&#39;azione. Ciò implica che le intestazioni dell&#39;e-mail (ad esempio **[!UICONTROL To]**, **[!UICONTROL CC]**, **[!UICONTROL BCC]**, **[!UICONTROL Subject]**) vengono generate al momento dell&#39;invio del modulo.

Per definire un segnaposto, specificare `${<field name>}` in un campo dopo aver selezionato **[!UICONTROL Invia e-mail]** come azione di invio.

Ad esempio, se il modulo contiene il campo **[!UICONTROL Indirizzo e-mail]**, denominato `email_addr`, per l&#39;acquisizione dell&#39;ID e-mail di un utente, è possibile specificare quanto segue nei campi **[!UICONTROL A]**, **[!UICONTROL CC]** o **[!UICONTROL CCN]**.

`${email_addr}`

Quando un utente invia il modulo, viene inviato un messaggio e-mail all&#39;ID e-mail immesso nel campo `email_addr` del modulo.

>[!NOTE]
>
>È possibile trovare il nome di un campo nella finestra di dialogo **[!UICONTROL Modifica]** del campo.

I segnaposto variabili possono essere utilizzati anche nei campi **[!UICONTROL Subject]** e **[!UICONTROL Email Template]**.

Esempio:

`Hi ${first_name} ${last_name},`

`Your form has been received by our department. It usually takes ten business days to process the request.`

`Regards`

`Administrator`

>[!NOTE]
>
>I campi nei pannelli ripetibili non possono essere utilizzati come segnaposto variabili.

