---
title: Invio di un avviso di invio del modulo tramite e-mail
seo-title: Invio di un avviso di invio del modulo tramite e-mail
description: AEM Forms consente di configurare l’azione di invio tramite e-mail che invia un messaggio di conferma all’utente al momento dell’invio del modulo.
seo-description: AEM Forms consente di configurare l’azione di invio tramite e-mail che invia un messaggio di conferma all’utente al momento dell’invio del modulo.
uuid: c80b1ef4-8fe3-48e0-8fc6-3032dc022a38
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 574de3d5-69ba-4e2f-a8ab-c59f357e4386
docset: aem65
translation-type: tm+mt
source-git-commit: acc2a3977353386d7e1dfd1344a61d78812fe3fc

---


# Invio di un avviso di invio del modulo tramite e-mail {#sending-a-form-submission-acknowledgement-via-email}

## Invio di dati modulo adattivo {#adaptive-form-data-submission}

I moduli adattivi forniscono diversi flussi di lavoro per l&#39; [invio di azioni](../../forms/using/configuring-submit-actions.md) out-of-the-box per l&#39;invio dei dati del modulo a endpoint diversi.

Ad esempio, l’azione **[!UICONTROL Invia e-mail]** invia un messaggio e-mail all’invio corretto di un modulo adattivo. È inoltre possibile configurare l&#39;invio tramite e-mail dei dati del modulo e del PDF.

Questo articolo descrive in dettaglio i passaggi per attivare l’azione E-mail su un modulo adattivo e le diverse configurazioni che fornisce.

>[!NOTE]
>
>È inoltre possibile utilizzare l&#39;opzione **[!UICONTROL Invia PDF tramite e-mail]** per inviare il modulo compilato via e-mail come allegato PDF. Le opzioni di configurazione disponibili per questa azione sono le stesse opzioni disponibili per l’azione **[!UICONTROL Invia e-mail]** . L&#39;azione e-mail PDF è disponibile solo per i moduli adattivi basati su XFA

## Invia azione e-mail {#email-action}

L’azione Invia e-mail consente all’autore di inviare automaticamente e-mail a uno o più destinatari all’invio corretto di un modulo adattivo.

>[!NOTE]
>
>Per utilizzare l’azione Invia e-mail, è necessario configurare il servizio e-mail AEM come descritto in [Configurazione del servizio](/help/sites-administering/notification.md#configuring-the-mail-service)e-mail.

### Abilitazione di Invia azione e-mail su un modulo adattivo {#enabling-email-action-on-an-adaptive-form}

1. Aprire un modulo adattivo in modalità di **[!UICONTROL modifica]** .

1. Nella scheda **[!UICONTROL Contenuto]** , toccate Contenitore **** modulo e toccate ![Configura](assets/configure-icon.svg) per visualizzare le proprietà del modulo adattivo.

1. Nella sezione **[!UICONTROL Invio]** , selezionare **[!UICONTROL Invia e-mail]** dall&#39;elenco a discesa **[!UICONTROL Invia azione]** .

   ![Invia azioni](assets/submission-actions.png)

1. Specificate ID e-mail validi nei campi **[!UICONTROL A]**, **[!UICONTROL CC]** e **[!UICONTROL CCN]** .

   Specificate l’oggetto e il corpo dell’e-mail rispettivamente nei campi **[!UICONTROL Oggetto]** e Modello **[!UICONTROL e-]** mail.

   È inoltre possibile specificare segnaposto variabili nei campi, nel qual caso i valori dei campi vengono elaborati quando l&#39;utente finale invia correttamente il modulo. Per ulteriori informazioni, vedere [Uso dei nomi dei campi modulo adattivi per creare contenuti](../../forms/using/form-submission-receipt-via-email.md#p-using-adaptive-form-field-names-to-dynamically-create-email-content-p)e-mail in modo dinamico.

   Selezionare **[!UICONTROL Includi allegati]** se il modulo include allegati e si desidera allegare tali file all&#39;e-mail.

   >[!NOTE]
   >
   >Se scegliete l’opzione **[!UICONTROL Invia PDF tramite e-mail]** , dovete selezionare l’opzione Includi allegati.

1. Click ![save](assets/save_icon.svg) to save the changes.

### Uso dei nomi dei campi modulo adattivi per creare contenuto e-mail dinamico {#using-adaptive-form-field-names-to-dynamically-create-email-content}

I nomi dei campi di un modulo adattivo sono denominati segnaposto che vengono sostituiti con il valore di tale campo dopo l&#39;invio del modulo da parte dell&#39;utente.

Nell’azione **[!UICONTROL Invia e-mail]** , è possibile utilizzare i segnaposto elaborati al momento dell’esecuzione dell’azione. Ciò implica che le intestazioni del messaggio e-mail (come **[!UICONTROL A]**, **[!UICONTROL CC]**, **[!UICONTROL CCN]**, **[!UICONTROL Oggetto]**) vengono generate al momento dell&#39;invio del modulo da parte dell&#39;utente.

Per definire un segnaposto, specificate `${<field name>}` un campo dopo aver selezionato **[!UICONTROL Invia e-mail]** come azione di invio.

Ad esempio, se il modulo contiene il campo Indirizzo **[!UICONTROL e-]** mail, denominato `email_addr`, per l&#39;acquisizione dell&#39;ID e-mail di un utente, è possibile specificare quanto segue nei campi **[!UICONTROL A]**, **[!UICONTROL CC]** o **[!UICONTROL CCN]** .

`${email_addr}`

Quando un utente invia il modulo, viene inviato un messaggio e-mail all&#39;ID e-mail immesso nel `email_addr` campo del modulo.

>[!NOTE]
>
>È possibile trovare il nome di un campo nella finestra di dialogo **[!UICONTROL Modifica]** del campo.

I segnaposto variabili possono essere utilizzati anche nei campi **[!UICONTROL Oggetto]** e Modello **** e-mail.

Ad esempio:

`Hi ${first_name} ${last_name},`

`Your form has been received by our department. It usually takes ten business days to process the request.`

`Regards`

`Administrator`

>[!NOTE]
>
>I campi nei pannelli ripetibili non possono essere utilizzati come segnaposto variabili.

