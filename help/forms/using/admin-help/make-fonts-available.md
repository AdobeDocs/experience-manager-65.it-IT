---
title: Rendere disponibili i font
description: Verifica che i font utilizzati in un modulo siano disponibili per l’utilizzo nel server applicazioni J2EE che ospita AEM Forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e9eae896-b1e4-4caa-b466-ac8c9e7416a4
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
source-wordcount: '228'
ht-degree: 100%
---
# Rendere disponibili i font {#make-fonts-available}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Verifica che i font utilizzati in un modulo siano disponibili per l’utilizzo nel server applicazioni J2EE che ospita AEM Forms. Ad esempio, prendi in considerazione lo scenario seguente. Un designer di moduli aggiunge un font alla directory dei font utilizzata dal designer e crea un modulo che utilizza tale font in un computer a parte. Affinché il servizio di output utilizzi il font, inseriscilo nella directory dei font del cliente. Se non esiste una directory dei font del cliente, crea una directory nel server applicazioni J2EE che ospita AEM Forms.

Per ulteriori informazioni sulle impostazioni dei font, consulta [Configurare le impostazioni generali di AEM Forms](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings).

**Specificare il percorso della directory dei font del cliente**

1. Nella console di amministrazione, fai clic su Impostazioni > Impostazioni sistema core > Configurazioni.
1. Nella casella Posizione della directory dei font di sistema digita il percorso della directory dei font del cliente. Puoi aggiungere più directory, separate da un punto e virgola **;**
1. Fai clic su OK.
1. Riavvia il sistema in cui è installato AEM Forms.

>[!NOTE]
>
>I font vengono selezionati dalla cache dei font di sistema di Windows e per aggiornare la cache è necessario riavviare il sistema. Dopo aver specificato la directory dei font del cliente, assicurati di riavviare il sistema in cui è installato AEM Forms.
