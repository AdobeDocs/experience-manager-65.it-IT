---
title: Rendi disponibili i font
description: Verificare che i caratteri utilizzati in un modulo siano disponibili per l'utilizzo nel server applicazioni J2EE che ospita i moduli AEM.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e9eae896-b1e4-4caa-b466-ac8c9e7416a4
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# Rendi disponibili i font {#make-fonts-available}

Verificare che i caratteri utilizzati in un modulo siano disponibili per l&#39;utilizzo nel server applicazioni J2EE che ospita i moduli AEM. Ad esempio, considera lo scenario seguente. Un progettista di moduli aggiunge un tipo di carattere alla directory dei tipi di carattere utilizzata da Designer e crea un modulo che utilizza tale tipo di carattere in un computer separato. Affinché il servizio di output utilizzi il carattere, inseriscilo nella directory dei caratteri del cliente. Se la directory dei caratteri del cliente non esiste, creare una directory nel server applicazioni J2EE che ospita i moduli AEM.

Per ulteriori informazioni sulle impostazioni dei caratteri, vedere [Configurare le impostazioni generali dei moduli AEM](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings).

**Specificare il percorso della directory dei font del cliente**

1. Nella console di amministrazione, fai clic su Impostazioni > Impostazioni sistemi core > Configurazioni.
1. Nella casella Posizione della directory dei caratteri di sistema digitare il percorso della directory dei caratteri del cliente. È possibile aggiungere più directory, separate da un punto e virgola **;**
1. Fare clic su OK.
1. Riavviare il sistema in cui è installato il modulo AEM.

>[!NOTE]
>
>I font vengono selezionati dalla cache dei font del sistema Windows ed è necessario riavviare il sistema per aggiornare la cache. Dopo aver specificato la directory dei caratteri del cliente, assicurarsi di riavviare il sistema in cui sono installati i moduli AEM.
