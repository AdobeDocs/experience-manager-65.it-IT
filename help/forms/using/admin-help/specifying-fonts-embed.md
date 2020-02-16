---
title: Specifica dei font da incorporare
seo-title: Specifica dei font da incorporare
description: Scoprite come specificare i font da incorporare.
seo-description: Scoprite come specificare i font da incorporare.
uuid: 97de6f98-ed3b-4a93-854a-193a967b4672
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4c83694c-b00f-40be-9ac4-f5785cd60741
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Specifica dei font da incorporare {#specifying-fonts-to-embed}

È possibile specificare i font sempre incorporati o mai incorporati nei moduli generati dal servizio Forms. L&#39;incorporazione dei font aumenta la dimensione del file dei moduli. Incorporare font insoliti che gli utenti raramente hanno nei loro sistemi. Non incorporare i font comuni generalmente installati.

>[!NOTE]
>
>Se per Forms è stato specificato un file XCI personalizzato, l&#39;opzione font da incorporare nel file XCI sostituisce queste impostazioni. (Vedere [Configurazione delle posizioni per Forms](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms).)

1. Nella console di amministrazione, fare clic su **[!UICONTROL Servizi > Moduli]**.
1. In Impostazioni **[!UICONTROL incorporazione]** font, nella casella Incorpora **[!UICONTROL sempre font]** digitare i nomi dei font da incorporare nei moduli, separati da virgole. I font specificati vengono incorporati nel modulo generato solo se vengono utilizzati nel modulo. Questa impostazione viene ignorata se l&#39;opzione font da incorporare è stata attivata nel file XCI passato al servizio perché in tal caso, tutti i font utilizzati nel PDF sono sempre incorporati.
1. Nella casella **[!UICONTROL Non incorporare font]** digitare i nomi dei font da non incorporare nei moduli, separati da virgole. I font specificati non vengono incorporati nel PDF, anche se sono utilizzati nel PDF generato. Questa impostazione viene ignorata se l&#39;opzione font da incorporare è stata disattivata nel file XCI passato al servizio perché in tal caso, nessuno dei font utilizzati nel PDF è incorporato.
1. Fai clic su **[!UICONTROL Salva]**.

