---
title: Specificare i font da incorporare
seo-title: Specificare i font da incorporare
description: Scoprite come specificare i font da incorporare.
seo-description: Scoprite come specificare i font da incorporare.
uuid: 02da5c00-0467-4633-a076-c36725cbfbad
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 180f0448-d507-4b6d-bb8a-d12a434e1250
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---


# Specificare i font da incorporare{#specify-fonts-to-embed}

È possibile specificare i font sempre incorporati o mai incorporati nei moduli utilizzati da Output. L&#39;incorporazione dei font aumenta la dimensione del file dei moduli. Incorporare font insoliti che gli utenti probabilmente non avranno sui loro sistemi e non incorporare i font comuni che avranno installato.

>[!NOTE]
>
>Se per Output è stato specificato un file XCI personalizzato, l&#39;opzione font da incorporare nel file XCI ha la priorità su queste impostazioni. (Vedere [Specificare i percorsi dei file per Output](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).)

1. Nella console di amministrazione, fate clic su Servizi > output.
1. In Impostazioni incorporazione font, nella casella Incorpora sempre font digitare i nomi dei font da incorporare nei moduli, separati da virgole. I font specificati vengono incorporati nel modulo generato solo se vengono utilizzati nel modulo. Questa impostazione viene ignorata se l&#39;opzione font incorporato è stata attivata nel file XCI passato al servizio. In tal caso, tutti i font utilizzati nel PDF sono sempre incorporati.
1. Nella casella Font da non incorporare digitare i nomi dei font da non incorporare nei moduli, separati da virgole. I font specificati non vengono incorporati nel PDF, anche se sono utilizzati nel PDF generato. Questa impostazione viene ignorata se l&#39;opzione font incorporato è stata disattivata nel file XCI passato al servizio. In tal caso, nessuno dei font utilizzati nel PDF è incorporato.
1. Fate clic su Salva.

