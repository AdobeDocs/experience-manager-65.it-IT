---
title: Specificare i font da incorporare
description: Scopri come specificare i font da incorporare in un modulo adattivo. È possibile specificare quali tipi di carattere sono stati incorporati o non sono mai incorporati con i moduli generati dal servizio Forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 02c28b2c-0cab-4431-9fab-fa332c96e092
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 38%
---
# Specificare i font da incorporare{#specify-fonts-to-embed}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

È possibile specificare quali tipi di carattere devono essere sempre incorporati o non incorporati con i moduli utilizzati dall&#39;output. L’incorporamento di caratteri aumenta le dimensioni dei file dei moduli. Incorpora font insoliti che gli utenti non avranno probabilmente sui loro sistemi e non incorpora font comuni che avranno installato.

>[!NOTE]
>
>Se è stato specificato un file XCI personalizzato per l&#39;output, l&#39;opzione incorpora font nel file XCI ignora queste impostazioni. Consulta [Specificare i percorsi dei file per l’output](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).)

1. Nella Console di amministrazione, fai clic su Servizi > Output.
1. Nella casella Incorpora sempre caratteri della casella Impostazioni incorporamento caratteri digitare i nomi dei caratteri da incorporare con i moduli, separati da virgole. I tipi di font specificati vengono incorporati nel modulo generato solo se sono utilizzati nel modulo. Questa impostazione viene ignorata se l&#39;opzione incorpora font è stata attivata nel file XCI passato al servizio. In tal caso, tutti i font utilizzati in PDF sono sempre incorporati.
1. Nella casella Non incorporare mai i tipi di carattere digitare i nomi dei tipi di carattere da non incorporare con i moduli, separati da virgole. I font specificati non vengono incorporati nel PDF, anche se vengono utilizzati nel PDF generato. Questa impostazione viene ignorata se l&#39;opzione incorpora font è stata disattivata nel file XCI passato al servizio. In tal caso, nessuno dei tipi di carattere utilizzati in PDF è incorporato.
1. Fai clic su Salva.
