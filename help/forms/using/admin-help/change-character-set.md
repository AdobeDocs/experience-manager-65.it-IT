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
workflow-type: ht
source-wordcount: '144'
ht-degree: 100%

---

# Modificare il set di caratteri {#change-the-character-set}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Puoi specificare il set di caratteri utilizzato per codificare il flusso di output.

1. Nella console di amministrazione fai clic su **[!UICONTROL Servizi > Output]**.
1. Seleziona un set di caratteri sell’elenco Set di caratteri in Internazionalizzazione. Questa impostazione dipende dalle opzioni `TransformationFormat` e `PrintFormat` specificate tramite l’API. Per specificare un set di caratteri diverso da quelli elencati, seleziona Personalizzato e specifica un valore di codifica nella casella visualizzata.

   Se `TransformationFormat` è PDF e PDF/A o `PrintFormat` è PCL, PostScript, etichetta Zebra, IPL, DPL, TPCL, GenericColorPCL o GenericPSLevel3, sono supportati solo set di caratteri specifici.

   Il set di caratteri deve essere un nome canonico valido. Il valore predefinito è ISO-8859-1.

1. Fai clic su **[!UICONTROL Salva]**.
