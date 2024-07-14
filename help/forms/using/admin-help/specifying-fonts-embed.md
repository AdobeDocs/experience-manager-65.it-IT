---
title: Specifica dei font da incorporare
description: Scopri come specificare i font da incorporare in un modulo adattivo. È possibile specificare i tipi di carattere incorporati o mai incorporati con i moduli generati dal servizio Forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: b2cbf5f3-ee13-47bf-bf7f-f6a1884cee66
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---

# Specifica dei font da incorporare {#specifying-fonts-to-embed}

È possibile specificare quali tipi di carattere devono essere sempre incorporati o meno con i moduli generati dal servizio Forms. L&#39;incorporamento di caratteri aumenta le dimensioni dei file dei moduli. Incorpora font insoliti che gli utenti raramente hanno sui loro sistemi. Non incorporare i tipi di carattere comuni che in genere sono installati.

>[!NOTE]
>
>Se è stato specificato un file XCI personalizzato per Forms, l&#39;opzione incorpora font nel file XCI sostituisce queste impostazioni. (Vedi [Configurazione delle posizioni per Forms](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms).)

1. Nella console di amministrazione, fare clic su **[!UICONTROL Servizi > Forms]**.
1. In **[!UICONTROL Impostazioni incorporamento caratteri]**, nella casella **[!UICONTROL Incorpora sempre caratteri]** digitare i nomi dei caratteri da incorporare con i moduli, separati da virgole. I tipi di carattere specificati vengono incorporati nel modulo generato solo se vengono utilizzati nel modulo. Questa impostazione viene ignorata se l&#39;opzione incorpora font è stata attivata nel file XCI passato al servizio perché in tal caso, tutti i font utilizzati nel PDF sono sempre incorporati.
1. Nella casella **[!UICONTROL Non incorporare mai i tipi di carattere]** digitare i nomi dei tipi di carattere da non incorporare con i moduli, separati da virgole. I font specificati non sono incorporati nel PDF, anche se sono utilizzati nel PDF generato. Questa impostazione viene ignorata se l&#39;opzione incorpora font è stata disattivata nel file XCI passato al servizio perché in tal caso nessuno dei font utilizzati nel PDF è incorporato.
1. Fai clic su **[!UICONTROL Salva]**.
