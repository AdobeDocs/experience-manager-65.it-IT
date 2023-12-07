---
title: Abilitazione degli allegati per un modulo HTML5
description: Per impostazione predefinita, il supporto degli allegati per i moduli HTML5 è disattivato.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
feature: Mobile Forms
exl-id: 68912260-179a-4d1b-b944-0a1777c021ac
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 1%

---

# Abilitazione degli allegati per un modulo HTML5 {#enabling-attachments-for-an-html-form}

Con i moduli HTML5 puoi caricare, visualizzare in anteprima e inviare allegati. Per impostazione predefinita, il supporto degli allegati è disattivato. Per attivare il supporto degli allegati:

1. Creare un [profilo personalizzato](/help/forms/using/custom-profile.md) con un `mfAttachmentOptions` proprietà stringa a selezione multipla. Ogni stringa nel `mfAttachmentOptions` la proprietà deve avere `property=value` per configurare le opzioni del widget file allegato. Il `property` e `value` può avere uno qualsiasi dei seguenti valori:

   | Proprietà | Valore |
   |--- |---|
   | multiSelect | true o false (true per impostazione predefinita) |
   | fileSizeLimit | Numero in MB (2 MB per impostazione predefinita). Ad esempio, 5. |
   | buttonText | Testo pulsante per finestra popup (&quot;Allega&quot; per impostazione predefinita) |
   | accetta | elenco separato da virgole dei tipi di file da accettare (&quot;audio/&amp;ast;, video/&amp;ast;, image/&amp;ast;, text/&amp;ast;, .pdf&quot; per impostazione predefinita) |

   Ad esempio:

   ![configurare le opzioni](assets/mfAttachmentOptions.png)

   Se necessario, puoi anche specificare altre opzioni personalizzate per il `mfAttachmentOptions` proprietà.

   >[!NOTE]
   >
   >In Microsoft Internet Explorer 9 gli utenti possono allegare file di dimensioni superiori al limite specificato. Si tratta di un problema noto.

1. Utilizza il [editor metadati](/help/forms/using/manage-form-metadata.md) per selezionare il profilo personalizzato creato in precedenza per i moduli di HTML 5.
1. Eseguire il rendering del modello di modulo con un profilo personalizzato. L&#39;icona degli allegati verrà visualizzata sulla barra degli strumenti Moduli.

   >[!NOTE]
   >
   >Il portale dei moduli fornisce automaticamente un profilo personalizzato con le funzionalità per bozze e allegati abilitate. Per ulteriori informazioni su **Salva come bozza** profilo, vedi [Salvataggio dei moduli HTML5 come bozza](/help/forms/using/saving-html5-form-draft.md).

1. Fare clic sull&#39;icona dell&#39;allegato per visualizzare una finestra di dialogo di selezione dell&#39;allegato. Sfoglia e seleziona l’allegato e fai clic su **Allega**.

   >[!NOTE]
   >
   >Per visualizzare l&#39;anteprima di un allegato, fare clic sul nome dell&#39;allegato.

   >[!NOTE]
   >
   >L’opzione di anteprima del file non è disponibile per gli utenti anonimi.

## Formato di invio dell’allegato {#attachment-submission-format}

Quando gli allegati sono abilitati, il modulo HTML5 invia dati multipart. I dati di invio in più parti sono composti da due parti **dataXml** e **allegati**.

>[!NOTE]
>
>Per compatibilità con le versioni precedenti, se `mfAllowAttachments` l&#39;opzione è disattivata, quindi i moduli HTML5 non inviano i dati in più parti. Invia dati XML semplici in **application/xml** formato.

Se il flag mfAllowAttachments è attivato, [invia servizio proxy](/help/forms/using/service-proxy.md) pubblica anche dati multipart con dataXml e allegati.
