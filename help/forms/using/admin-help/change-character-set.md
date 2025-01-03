---
title: Modificare il set di caratteri
description: Puoi specificare il set di caratteri utilizzato per codificare il flusso di output. Scopri come modificare il set di caratteri.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 9ff75d98-54ad-425d-912f-d5a7501bf564
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 1%

---

# Modificare il set di caratteri {#change-the-character-set}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Puoi specificare il set di caratteri utilizzato per codificare il flusso di output.

1. Nella console di amministrazione, fare clic su **[!UICONTROL Servizi > output]**.
1. In Internazionalizzazione selezionare un set di caratteri nell&#39;elenco Set di caratteri. Questa impostazione dipende da `TransformationFormat` e `PrintFormat` specificati tramite l&#39;API. Per specificare un set di caratteri diverso da quelli elencati, selezionare Personalizzato e specificare un valore di codifica nella casella visualizzata.

   Se `TransformationFormat` è PDF e PDF/A o `PrintFormat` è PCL, PostScript, etichetta Zebra, IPL, DPL, TPCL, GenericColorPCL o GenericPSLevel3, sono supportati solo set di caratteri specifici.

   Il set di caratteri deve essere un nome canonico valido. Il valore predefinito è ISO-8859-1.

1. Fai clic su **[!UICONTROL Salva]**.
