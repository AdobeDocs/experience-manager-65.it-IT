---
title: Panoramica del servizio di output
seo-title: Overview of output service
description: Output consente di unire i dati del modulo XML a una struttura del modulo creata in Designer per creare un flusso di output del documento in vari formati.
seo-description: Output lets you merge XML form data with a form design created in Designer to create a document output stream in various formats.
uuid: 7890b0a6-bae5-4ad5-ae41-503b988ba3da
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5a96f5ea-6fe3-44b1-b314-14097b9e9c01
exl-id: e99b72d0-fbd5-4150-a225-1a91ad4c5867
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# Panoramica del servizio di output {#overview-of-output-service}

Output consente di unire i dati del modulo XML a una struttura del modulo creata in Designer per creare un flusso di output del documento in vari formati. Il flusso di output può essere inviato a una stampante di rete, a una stampante locale o a un file disco

Puoi utilizzare la pagina Output nella console di amministrazione per amministrare il servizio Output. Le impostazioni configurate vengono utilizzate in fase di esecuzione quando le impostazioni equivalenti non sono state specificate tramite l’API dei moduli AEM. La configurazione eseguita tramite l’SDK di AEM forms sostituisce le impostazioni configurate tramite la console di amministrazione.

Per ulteriori informazioni sul servizio Output, vedi [Riferimento servizi](https://www.adobe.com/go/learn_aemforms_services_61).

Nelle pagine di output nella console di amministrazione è possibile eseguire diverse attività:

* Specifica i set di caratteri per l’internazionalizzazione. (Vedi [Modificare il set di caratteri](/help/forms/using/admin-help/change-character-set.md#change-the-character-set).)
* Specifica percorsi assoluti e relativi per URL, URI, XCI e percorsi di file. (Vedi [Specificare le posizioni dei file per l&#39;output](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).)
* Configura le dimensioni e i criteri della cache. (Vedi [Specifica della modalità cache](/help/forms/using/admin-help/configuring-caching-output.md#specifying-the-cache-mode) e [Configurazione delle impostazioni della cache](/help/forms/using/admin-help/configuring-caching-output.md#configuring-cache-settings).)
* Rendere disponibili i font sul server dell&#39;applicazione. (Vedi [Rendi disponibili i font](/help/forms/using/admin-help/make-fonts-available.md#make-fonts-available).)
* Specifica i font da incorporare. (Vedi [Specificare i font da incorporare](/help/forms/using/admin-help/specify-fonts-embed.md#specify-fonts-to-embed).)
* Specifica le opzioni di configurazione XCI. (Vedi [Specificare le opzioni di configurazione XCI](/help/forms/using/admin-help/specify-xci-configuration-options.md#specify-xci-configuration-options).)
* Specifica le impostazioni di protezione. (Vedi [Specificare le impostazioni di protezione](/help/forms/using/admin-help/specify-security-settings.md#specify-security-settings).)

Dopo aver modificato le impostazioni, fare clic su Salva per applicarle a Output. Non è necessario riavviare il server per rendere effettive le modifiche, ma potrebbe essere necessario riavviare il servizio Output durante la configurazione delle impostazioni della cache.
