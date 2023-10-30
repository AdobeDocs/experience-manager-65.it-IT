---
title: Specificare i font da incorporare
description: Scopri come specificare i font da incorporare in un modulo adattivo. È possibile specificare i tipi di carattere incorporati o mai incorporati con i moduli generati dal servizio Forms.
uuid: 02da5c00-0467-4633-a076-c36725cbfbad
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 180f0448-d507-4b6d-bb8a-d12a434e1250
exl-id: 02c28b2c-0cab-4431-9fab-fa332c96e092
source-git-commit: 6caf3ef4a00275f0f73be52b6a9ccba77d277f1a
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# Specificare i font da incorporare{#specify-fonts-to-embed}

È possibile specificare quali tipi di carattere devono essere sempre incorporati o non incorporati con i moduli utilizzati dall&#39;output. L&#39;incorporamento di caratteri aumenta le dimensioni dei file dei moduli. Incorpora font insoliti che gli utenti non avranno probabilmente sui loro sistemi e non incorpora font comuni che avranno installato.

>[!NOTE]
>
>Se è stato specificato un file XCI personalizzato per l&#39;output, l&#39;opzione incorpora font nel file XCI ignora queste impostazioni. (vedere [Specificare i percorsi dei file per l&#39;output](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).)

1. Nella console di amministrazione, fai clic su Servizi > output.
1. Nella casella Incorpora sempre caratteri della casella Impostazioni incorporamento caratteri digitare i nomi dei caratteri da incorporare con i moduli, separati da virgole. I tipi di carattere specificati vengono incorporati nel modulo generato solo se vengono utilizzati nel modulo. Questa impostazione viene ignorata se l&#39;opzione incorpora font è stata attivata nel file XCI passato al servizio. In tal caso, tutti i font utilizzati nel PDF vengono sempre incorporati.
1. Nella casella Non incorporare mai i tipi di carattere digitare i nomi dei tipi di carattere da non incorporare con i moduli, separati da virgole. I font specificati non sono incorporati nel PDF, anche se sono utilizzati nel PDF generato. Questa impostazione viene ignorata se l&#39;opzione incorpora font è stata disattivata nel file XCI passato al servizio. In tal caso, nessuno dei tipi di carattere utilizzati nel PDF è incorporato.
1. Fai clic su Salva.
