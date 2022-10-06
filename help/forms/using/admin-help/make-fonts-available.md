---
title: Rendi disponibili i font
seo-title: Make fonts available
description: Assicurarsi che i font utilizzati all’interno di un modulo siano disponibili per l’uso sul server applicazioni J2EE che ospita AEM moduli.
seo-description: Ensure that the fonts used within a form are available for use on the J2EE application server hosting AEM forms.
uuid: 6588b4b6-f866-4253-91c8-3aa174340e8c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9f58a6c4-3190-49d4-800c-4a55dca7c296
exl-id: e9eae896-b1e4-4caa-b466-ac8c9e7416a4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# Rendi disponibili i font {#make-fonts-available}

Assicurarsi che i font utilizzati all’interno di un modulo siano disponibili per l’uso sul server applicazioni J2EE che ospita AEM moduli. Ad esempio, considera lo scenario seguente. Una struttura del modulo aggiunge un font alla directory dei font utilizzata da Designer e crea un modulo che lo utilizza in un computer separato. Affinché il servizio Output utilizzi il font, inseriscilo nella directory dei font del cliente. Se la directory dei font del cliente non esiste, crea una directory sul server dell’applicazione J2EE che ospita i moduli AEM.

Per informazioni sulle impostazioni di font aggiuntive, consulta [Configurare le impostazioni generali dei moduli AEM](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings).

**Specificare il percorso della directory dei font del cliente**

1. Nella console di amministrazione, fai clic su Impostazioni > Impostazioni dei sistemi principali > Configurazioni.
1. Nella casella Posizione della directory dei font di sistema digitare il percorso della directory dei font del cliente. È possibile aggiungere più directory, separate da punto e virgola **;**
1. Fai clic su OK.
1. Riavviare il sistema in cui sono installati AEM moduli.

>[!NOTE]
>
>I font vengono selezionati dalla cache dei font di sistema di Windows ed è necessario un riavvio del sistema per aggiornare la cache. Dopo aver specificato la directory dei font per il cliente, assicurarsi di riavviare il sistema in cui sono installati AEM moduli.
