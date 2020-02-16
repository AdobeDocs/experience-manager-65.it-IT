---
title: Font disponibili
seo-title: Font disponibili
description: Verificate che i font utilizzati all'interno di un modulo siano disponibili per l'uso nel server applicazione J2EE in cui sono ospitati i moduli AEM.
seo-description: Verificate che i font utilizzati all'interno di un modulo siano disponibili per l'uso nel server applicazione J2EE in cui sono ospitati i moduli AEM.
uuid: 6588b4b6-f866-4253-91c8-3aa174340e8c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9f58a6c4-3190-49d4-800c-4a55dca7c296
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Font disponibili {#make-fonts-available}

Verificate che i font utilizzati all&#39;interno di un modulo siano disponibili per l&#39;uso nel server applicazione J2EE in cui sono ospitati i moduli AEM. Ad esempio, considerare lo scenario seguente. Una struttura del modulo aggiunge un font alla directory dei font utilizzata da Designer e crea un modulo che utilizza tale font in un computer a parte. Affinché il servizio Output utilizzi il font, inserirlo nella directory dei font del cliente. Se la directory dei font del cliente non esiste, create una directory sul server applicazione J2EE in cui sono ospitati i moduli AEM.

Per informazioni su ulteriori impostazioni dei font, consultate [Configurare le impostazioni](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)generali dei moduli AEM.

**Specificare il percorso della directory dei font del cliente**

1. Nella console di amministrazione, fate clic su Impostazioni > Impostazioni sistemi di base > Configurazioni.
1. Nella casella Posizione della directory dei font di sistema, digitare il percorso della directory dei font del cliente. È possibile aggiungere più directory, separate da punto e virgola **;**
1. Fate clic su OK.
1. Riavviate il sistema in cui sono installati i moduli AEM.

>[!NOTE]
>
> I font vengono selezionati dalla cache dei font di sistema di Windows e per aggiornare la cache è necessario riavviare il sistema. Dopo aver specificato la directory dei font del cliente, accertatevi di riavviare il sistema in cui sono installati i moduli AEM.

