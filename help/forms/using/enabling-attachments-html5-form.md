---
title: Abilitazione degli allegati per un modulo HTML5
description: Per impostazione predefinita, il supporto degli allegati per i moduli HTML5 è disattivato.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 8eebfcd6-0597-44ed-b718-bf9a1baa6c12
feature: HTML5 Forms,Mobile Forms
exl-id: 68912260-179a-4d1b-b944-0a1777c021ac
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 97aafc4b-2598-52d6-9012-295a95969e38
    internal-label: HTML5 Forms
  - id: 59f95943-e802-56ac-990d-21ab923984c1
    internal-label: Mobile Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 5%
---
# Abilitazione degli allegati per un modulo HTML5 {#enabling-attachments-for-an-html-form}

Con i moduli HTML5 è possibile caricare, visualizzare in anteprima e inviare allegati. Per impostazione predefinita, il supporto degli allegati è disattivato. Per attivare il supporto degli allegati:

1. Crea un [profilo personalizzato](/help/forms/using/custom-profile.md) con una proprietà stringa multiselezionata `mfAttachmentOptions`. Ogni stringa nella proprietà `mfAttachmentOptions` deve avere un formato `property=value` per configurare le opzioni del widget degli allegati. `property` e `value` possono avere uno qualsiasi dei seguenti valori:

   | Proprietà | Valore |
   |--- |---|
   | multiSelect | true o false (true per impostazione predefinita) |
   | fileSizeLimit | Numero in MB (2 MB per impostazione predefinita). Ad esempio, 5. |
   | buttonText | Testo pulsante per finestra popup (&quot;Allega&quot; per impostazione predefinita) |
   | accetta | elenco separato da virgole dei tipi di file da accettare (&quot;audio/&ast;, video/&ast;, image/&ast;, text/&ast;, .pdf&quot; per impostazione predefinita) |

   Ad esempio:

   ![configura opzioni](assets/mfAttachmentOptions.png)

   Se necessario, è inoltre possibile specificare altre opzioni personalizzate per la proprietà `mfAttachmentOptions`.

   >[!NOTE]
   >
   >In Microsoft Internet Explorer 9 gli utenti possono allegare file di dimensioni superiori al limite specificato. Si tratta di un problema noto.

1. Utilizza l&#39;[editor metadati](/help/forms/using/manage-form-metadata.md) per selezionare il profilo personalizzato creato in precedenza per i moduli di HTML 5.
1. Eseguire il rendering del modello di modulo con un profilo personalizzato. L&#39;icona degli allegati verrà visualizzata sulla barra degli strumenti Moduli.

   >[!NOTE]
   >
   >Il portale dei moduli fornisce automaticamente un profilo personalizzato con le funzionalità per bozze e allegati abilitate. Per ulteriori informazioni sul profilo **Salva come bozza**, vedere [Salvataggio dei moduli HTML5 come bozza](/help/forms/using/saving-html5-form-draft.md).

1. Fare clic sull&#39;icona dell&#39;allegato per visualizzare una finestra di dialogo di selezione dell&#39;allegato. Sfoglia e seleziona l&#39;allegato e fai clic su **Allega**.

   >[!NOTE]
   >
   >Per visualizzare l&#39;anteprima di un allegato, fare clic sul nome dell&#39;allegato.

   >[!NOTE]
   >
   >L’opzione di anteprima del file non è disponibile per gli utenti anonimi.

## Formato di invio dell’allegato {#attachment-submission-format}

Quando gli allegati sono abilitati, il modulo HTML5 invia dati multipart. I dati di invio in più parti contengono due parti: **dataXml** e **allegati**.

>[!NOTE]
>
>Per compatibilità con le versioni precedenti, se l&#39;opzione `mfAllowAttachments` è disattivata, i moduli HTML5 non inviano i dati in più parti. Invia dati XML semplici nel formato **application/xml**.

Se il flag mfAllowAttachments è attivato, anche il servizio proxy [submit](/help/forms/using/service-proxy.md) pubblica dati multipart con dataXml e allegati.
