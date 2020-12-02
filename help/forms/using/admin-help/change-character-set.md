---
title: Modificare il set di caratteri
seo-title: Modificare il set di caratteri
description: È possibile specificare il set di caratteri utilizzato per codificare il flusso di output. Scopri come modificare il set di caratteri.
seo-description: È possibile specificare il set di caratteri utilizzato per codificare il flusso di output. Scopri come modificare il set di caratteri.
uuid: ecb0c3ff-368c-4553-80e4-aa35fc15af62
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 811b31f8-5465-4fb2-b1f9-513936041771
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 1%

---


# Modificare il set di caratteri {#change-the-character-set}

È possibile specificare il set di caratteri utilizzato per codificare il flusso di output.

1. Nella console di amministrazione, fare clic su **[!UICONTROL Servizi > output]**.
1. In Internazionalizzazione, nell&#39;elenco Set di caratteri, selezionare un set di caratteri. Questa impostazione dipende da `TransformationFormat` e `PrintFormat` specificati tramite l&#39;API. Per specificare un set di caratteri diverso da quelli elencati, selezionare Personalizzato e specificare un valore di codifica nella casella visualizzata.

   Se `TransformationFormat` è PDF e PDF/A o `PrintFormat` è PCL, PostScript, etichetta Zebra, IPL, DPL, TPCL, GenericColorPCL o GenericPSLevel3, sono supportati solo set di caratteri specifici.

   Il set di caratteri deve essere un nome canonico valido. Il valore predefinito è ISO-8859-1.

1. Fai clic su **[!UICONTROL Salva]**.

