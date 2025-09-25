---
title: Specificare i font da incorporare
description: Scopri come specificare i font da incorporare in un modulo adattivo. È possibile specificare quali tipi di carattere sono stati incorporati o non sono mai incorporati con i moduli generati dal servizio Forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: b2cbf5f3-ee13-47bf-bf7f-f6a1884cee66
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '282'
ht-degree: 100%

---

# Specificare i font da incorporare {#specifying-fonts-to-embed}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

È possibile specificare quali tipi di carattere devono essere sempre incorporati o meno con i moduli generati dal servizio Forms. L’incorporamento di caratteri aumenta le dimensioni dei file dei moduli. Incorpora font insoliti che gli utenti raramente hanno sui loro sistemi. Non incorporare i font comuni che in genere sono installati.

>[!NOTE]
>
>Se è stato specificato un file XCI personalizzato per Forms, l’opzione incorpora font nel file XCI sostituisce queste impostazioni. (Consulta [Configurare le posizioni per Forms](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms).)

1. Nella console di amministrazione, fai clic su **[!UICONTROL Servizi > Moduli]**.
1. In **[!UICONTROL Impostazioni di incorporamento font]**, nella casella **[!UICONTROL Incorpora sempre font]**, digita i nomi dei font da incorporare con i moduli, separati da virgole. I tipi di font specificati vengono incorporati nel modulo generato solo se sono utilizzati nel modulo. Questa impostazione viene ignorata se l’opzione incorpora font è stata attivata nel file XCI passato al servizio perché in tal caso, tutti i font utilizzati in PDF sono sempre incorporati.
1. Nella casella **[!UICONTROL Non incorporare mai i font]**, digita i nomi dei font da non incorporare con i moduli, separati da virgole. I font specificati non vengono incorporati nel PDF, anche se vengono utilizzati nel PDF generato. Questa impostazione viene ignorata se l’opzione incorpora font è stata disattivata nel file XCI passato al servizio perché in tal caso nessuno dei font utilizzati nel PDF è incorporato.
1. Fai clic su **[!UICONTROL Salva]**.
