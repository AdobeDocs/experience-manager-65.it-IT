---
title: Abilitazione degli allegati per un modulo HTML5
seo-title: Abilitazione degli allegati per un modulo HTML5
description: Per impostazione predefinita, il supporto allegato per i moduli HTML5 è disattivato.
seo-description: Per impostazione predefinita, il supporto allegato per i moduli HTML5 è disattivato.
uuid: 2c62ac3e-4b27-46c7-a61d-a805fb5d26fb
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 8eebfcd6-0597-44ed-b718-bf9a1baa6c12
feature: Mobile Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---


# Abilitazione degli allegati di un modulo HTML5 {#enabling-attachments-for-an-html-form}

È possibile caricare, visualizzare in anteprima e inviare allegati con moduli HTML5. Per impostazione predefinita, il supporto per gli allegati è disattivato. Per abilitare il supporto allegato:

1. Crea un [profilo personalizzato](/help/forms/using/custom-profile.md) con proprietà stringa mutiselezionata `mfAttachmentOptions`.
1. Nel profilo personalizzato, specifica le proprietà `fileSizeLimit`, `multiSelect` e `buttonTex`t per configurare le opzioni del widget di file allegato. Se necessario, puoi anche specificare altre proprietà personalizzate.

1. Nel profilo personalizzato, utilizza le seguenti configurazioni:

   * **multiSelect** -> true o false (true per impostazione predefinita)
   * **fileSizeLimit** -> value_in_mb (diciamo 5) (2 MB per impostazione predefinita)
   * **buttonText** -> Testo del pulsante per la finestra a comparsa (&quot;Allega&quot; per impostazione predefinita)
   * **accetta i tipi di file** -> da accettare (&quot;audio/&amp;ast;, video/&amp;ast;, image/&amp;ast;, text/&amp;ast;, .pdf&quot; per impostazione predefinita)

   >[!NOTE]
   >
   >In Microsoft Internet Explorer 9, gli utenti possono allegare file di dimensioni superiori al limite specificato. È un problema noto.

1. Utilizza l’ [editor di metadati](/help/forms/using/manage-form-metadata.md) per selezionare il profilo personalizzato creato in precedenza per i moduli HTML 5.
1. Eseguire il rendering del modello di modulo con un profilo personalizzato e l’icona degli allegati viene visualizzata sulla barra degli strumenti dei moduli.

   >[!NOTE]
   >
   >Con il portale dei moduli è disponibile un profilo personalizzato con le bozze e le funzionalità degli allegati abilitate. Per ulteriori informazioni sul profilo **Salva come bozza**, vedere [Salvataggio di moduli HTML5 come bozza](/help/forms/using/saving-html5-form-draft.md).

1. Fare clic sull&#39;icona dell&#39;allegato per visualizzare una finestra di dialogo per la selezione dell&#39;allegato. Sfoglia e seleziona l&#39;allegato e fai clic su **Allega**.

   >[!NOTE]
   >
   >Per visualizzare l&#39;anteprima di un allegato, fare clic sul nome dell&#39;allegato.

   >[!NOTE]
   >
   >L’opzione di anteprima del file non è disponibile per gli utenti anonimi.

## Formato di invio allegato {#attachment-submission-format}

Quando gli allegati sono abilitati, il modulo HTML5 invia dati multiparte. I dati di invio in più parti hanno due parti **dataXml** e **allegati**.

>[!NOTE]
>
>Per la compatibilità con le versioni precedenti, se l’opzione `mfAllowAttachments` è disattivata, i moduli HTML5 non inviano i dati in più parti. Invia dati xml semplici in formato **application/xml**.

Se il flag mfAllowAttachments è attivato, il [servizio proxy di invio del servizio](/help/forms/using/service-proxy.md) invia anche dati multiparte con dataXml e allegati.
