---
title: Font disponibili
seo-title: Font disponibili
description: Assicurarsi che i font utilizzati all'interno di un modulo siano disponibili per l'uso nel server applicazione J2EE in cui sono ospitati AEM moduli.
seo-description: Assicurarsi che i font utilizzati all'interno di un modulo siano disponibili per l'uso nel server applicazione J2EE in cui sono ospitati AEM moduli.
uuid: 6588b4b6-f866-4253-91c8-3aa174340e8c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9f58a6c4-3190-49d4-800c-4a55dca7c296
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---


# Disponibilità di font {#make-fonts-available}

Assicurarsi che i font utilizzati all&#39;interno di un modulo siano disponibili per l&#39;uso nel server applicazione J2EE in cui sono ospitati AEM moduli. Ad esempio, considerare lo scenario seguente. Una struttura del modulo aggiunge un font alla directory dei font utilizzata da Designer e crea un modulo che utilizza tale font in un computer a parte. Affinché il servizio Output possa utilizzare il font, inserirlo nella directory dei font del cliente. Se la directory dei font del cliente non esiste, creare una directory sul server applicazione J2EE in cui sono ospitati AEM moduli.

Per ulteriori informazioni sulle impostazioni dei font, vedere [Configurare le impostazioni generali dei moduli AEM](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings).

**Specificare il percorso della directory dei font del cliente**

1. Nella console di amministrazione, fate clic su Impostazioni > Impostazioni sistemi di base > Configurazioni.
1. Nella casella Posizione della directory dei font di sistema, digitare il percorso della directory dei font del cliente. È possibile aggiungere più directory, separate da un punto e virgola **;**
1. Fai clic su OK.
1. Riavviare il sistema in cui sono installati AEM moduli.

>[!NOTE]
>
>I font vengono selezionati dalla cache dei font di sistema di Windows e per aggiornare la cache è necessario riavviare il sistema. Dopo aver specificato la directory dei font del cliente, assicurarsi di riavviare il sistema in cui sono installati AEM moduli.

