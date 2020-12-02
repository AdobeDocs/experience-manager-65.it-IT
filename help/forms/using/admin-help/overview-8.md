---
title: Panoramica del servizio di output
seo-title: Panoramica del servizio di output
description: Output consente di unire i dati del modulo XML a una struttura del modulo creata in Designer per creare un flusso di output del documento in vari formati.
seo-description: Output consente di unire i dati del modulo XML a una struttura del modulo creata in Designer per creare un flusso di output del documento in vari formati.
uuid: 7890b0a6-bae5-4ad5-ae41-503b988ba3da
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5a96f5ea-6fe3-44b1-b314-14097b9e9c01
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---


# Panoramica del servizio di output {#overview-of-output-service}

Output consente di unire i dati del modulo XML a una struttura del modulo creata in Designer per creare un flusso di output del documento in vari formati. Il flusso di output può essere inviato a una stampante di rete, a una stampante locale o a un file su disco

È possibile utilizzare la pagina Output nella console di amministrazione per amministrare il servizio Output. Le impostazioni configurate vengono utilizzate in fase di esecuzione quando le impostazioni equivalenti non sono state specificate tramite l&#39;API dei moduli AEM. La configurazione eseguita tramite l&#39;SDK dei moduli AEM ha la priorità sulle impostazioni configurate tramite la console di amministrazione.

Per ulteriori informazioni sul servizio Output, vedere [Guida di riferimento dei servizi](https://www.adobe.com/go/learn_aemforms_services_61).

Nelle pagine Output nella console di amministrazione è possibile eseguire diverse attività:

* Specificare i set di caratteri per l&#39;internazionalizzazione. (Vedere [Modificare il set di caratteri](/help/forms/using/admin-help/change-character-set.md#change-the-character-set).)
* Specificate percorsi assoluti e relativi per URL, URI, XCI e percorsi di file. (Vedere [Specificare i percorsi dei file per Output](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).)
* Configurare le dimensioni e i criteri della cache. (Vedere [Specifica della modalità cache](/help/forms/using/admin-help/configuring-caching-output.md#specifying-the-cache-mode) e [Configurazione delle impostazioni della cache](/help/forms/using/admin-help/configuring-caching-output.md#configuring-cache-settings).)
* Rendere i font disponibili sul server dell&#39;applicazione. (Vedere [Rendere disponibili i font](/help/forms/using/admin-help/make-fonts-available.md#make-fonts-available).)
* Specificate i font da incorporare. (Vedere [Specificare i font da incorporare](/help/forms/using/admin-help/specify-fonts-embed.md#specify-fonts-to-embed).)
* Specificate le opzioni di configurazione XCI. (Vedere [Specificare le opzioni di configurazione XCI](/help/forms/using/admin-help/specify-xci-configuration-options.md#specify-xci-configuration-options).)
* Specificate le impostazioni di protezione. (Vedere [Specificare le impostazioni di protezione](/help/forms/using/admin-help/specify-security-settings.md#specify-security-settings).)

Dopo aver modificato le impostazioni, fare clic su Salva per applicarle ad Output. Non è necessario riavviare il server per rendere effettive le modifiche, ma potrebbe essere necessario riavviare il servizio Output al momento della configurazione delle impostazioni della cache.
