---
title: Specificare le impostazioni di protezione
description: Scopri come specificare impostazioni di protezione per proteggere i file di dati XML. La funzionalità delle impostazioni di protezione controlla le entità esterne negli input XML.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 004b8a2f-66a0-43a4-be56-7e42b703ebb2
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 50158d81-1c06-57f7-8bd7-e8ff76a93f85
    internal-label: Document Security
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
source-wordcount: '101'
ht-degree: 100%
---
# Specificare le impostazioni di protezione {#specifying-security-settings}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

I moduli consentono di controllare se le entità esterne negli input XML vengono risolte. Per impostazione predefinita tali entità vengono risolte, ma è possibile modificare questo comportamento per aumentare la sicurezza del sistema AEM Forms.

**Impedire l’elaborazione di file di dati XML contenenti riferimenti a entità esterne**

1. Nella console di amministrazione, fai clic su **[!UICONTROL Servizi > Moduli]**.
1. Deseleziona la casella di controllo Risolvi entità esterne.
1. Fai clic su **[!UICONTROL Salva]**.
