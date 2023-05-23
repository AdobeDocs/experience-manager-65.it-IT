---
title: Specifica dei font da incorporare
seo-title: Specifying fonts to embed
description: Scopri come specificare i font da incorporare.
seo-description: Learn how to specify fonts to embed.
uuid: 97de6f98-ed3b-4a93-854a-193a967b4672
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4c83694c-b00f-40be-9ac4-f5785cd60741
exl-id: b2cbf5f3-ee13-47bf-bf7f-f6a1884cee66
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# Specifica dei font da incorporare {#specifying-fonts-to-embed}

È possibile specificare quali tipi di carattere devono essere sempre incorporati o meno con i moduli generati dal servizio Forms. L&#39;incorporamento di caratteri aumenta le dimensioni dei file dei moduli. Incorpora font insoliti che gli utenti raramente hanno sui loro sistemi. Non incorporare i tipi di carattere comuni che in genere sono installati.

>[!NOTE]
>
>Se è stato specificato un file XCI personalizzato per Forms, l&#39;opzione incorpora font nel file XCI sostituisce queste impostazioni. (vedere [Configurazione delle posizioni per Forms](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms).)

1. Nella console di amministrazione, fai clic su **[!UICONTROL Servizi > Forms]**.
1. Sotto **[!UICONTROL Impostazioni incorporamento font]**, nella **[!UICONTROL Incorpora sempre font]** digitare i nomi dei tipi di carattere da incorporare con le maschere, separati da virgole. I tipi di carattere specificati vengono incorporati nel modulo generato solo se vengono utilizzati nel modulo. Questa impostazione viene ignorata se l&#39;opzione incorpora font è stata attivata nel file XCI passato al servizio perché in tal caso, tutti i font utilizzati nel PDF sono sempre incorporati.
1. In **[!UICONTROL Non incorporare mai i font]** digitare i nomi dei tipi di carattere da non incorporare nei form, separati da virgole. I font specificati non sono incorporati nel PDF, anche se sono utilizzati nel PDF generato. Questa impostazione viene ignorata se l&#39;opzione incorpora font è stata disattivata nel file XCI passato al servizio perché in tal caso nessuno dei font utilizzati nel PDF è incorporato.
1. Fai clic su **[!UICONTROL Salva]**.
