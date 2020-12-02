---
title: Abilitazione degli allegati per un modulo HTML5
seo-title: Abilitazione degli allegati per un modulo HTML5
description: Per impostazione predefinita, il supporto degli allegati per i moduli HTML5 è disabilitato.
seo-description: Per impostazione predefinita, il supporto degli allegati per i moduli HTML5 è disabilitato.
uuid: 2c62ac3e-4b27-46c7-a61d-a805fb5d26fb
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 8eebfcd6-0597-44ed-b718-bf9a1baa6c12
translation-type: tm+mt
source-git-commit: 00e14be8a0775149b3ee7ce8cd781dd7f1e49e4f
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 0%

---


# Abilitazione degli allegati per un modulo HTML5 {#enabling-attachments-for-an-html-form}

È possibile caricare, visualizzare in anteprima e inviare allegati con moduli HTML5. Per impostazione predefinita, il supporto degli allegati è disabilitato. Per abilitare il supporto degli allegati:

1. Create un [profilo personalizzato](/help/forms/using/custom-profile.md) con mutiselezionate la proprietà stringa `mfAttachmentOptions`.
1. Nel profilo personalizzato, specificare le proprietà `fileSizeLimit`, `multiSelect` e `buttonTex`t per configurare le opzioni del widget degli allegati. Se necessario, potete anche specificare altre proprietà personalizzate.

1. Nel profilo personalizzato, utilizzate le seguenti configurazioni:

   * **multiSelect** -> true o false (true per impostazione predefinita)
   * **fileSizeLimit** -> value_in_mb (ad esempio 5) (2 MB per impostazione predefinita)
   * **buttonText** -> Testo pulsante per la finestra a comparsa (&quot;Allega&quot; per impostazione predefinita)
   * **accettare** -> i tipi di file da accettare (&quot;audio/&amp;ast;, video/&amp;ast;, image/&amp;ast;, text/&amp;ast;, .pdf&quot; per impostazione predefinita)

   >[!NOTE]
   >
   >In Microsoft Internet Explorer 9, gli utenti possono allegare file superiori al limite specificato. È un problema noto.

1. Per selezionare il profilo personalizzato creato sopra per i moduli HTML 5, utilizzare l&#39;editor di metadati [metadata](/help/forms/using/manage-form-metadata.md).
1. Il rendering del modello di modulo con un profilo personalizzato e l&#39;icona degli allegati viene visualizzato sulla barra degli strumenti dei moduli.

   >[!NOTE]
   >
   >Il portale dei moduli fornisce un profilo personalizzato con le funzionalità di bozze e allegati abilitate. Per ulteriori informazioni sul profilo **Salva come bozza**, vedere [Salvataggio di moduli HTML5 come bozza](/help/forms/using/saving-html5-form-draft.md).

1. Fare clic sull&#39;icona dell&#39;allegato per visualizzare una finestra di dialogo per la selezione dell&#39;allegato. Selezionare l&#39;allegato e fare clic su **Allega**.

   >[!NOTE]
   >
   >Per visualizzare l&#39;anteprima di un allegato, fare clic sul nome dell&#39;allegato.

   >[!NOTE]
   >
   >L’opzione di anteprima del file non è disponibile per gli utenti anonimi.

## Formato di invio allegati {#attachment-submission-format}

Quando gli allegati sono attivati, i moduli HTML5 inviano dati multiparte. I dati di invio multiparte sono composti da due parti **dataXml** e **allegati**.

>[!NOTE]
>
>Per compatibilità con le versioni precedenti, se l&#39;opzione `mfAllowAttachments` è disattivata, i moduli HTML5 non inviano i dati di più parti. Invia un XML di dati semplice in formato **application/xml**.

Se il flag mfAllowAttachments è attivato, il servizio proxy [submit service](/help/forms/using/service-proxy.md) invia anche dati multiparte con dataXml e allegati.
