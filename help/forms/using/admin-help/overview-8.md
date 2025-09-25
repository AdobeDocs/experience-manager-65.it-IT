---
title: Panoramica sul servizio di output
description: L’output consente di unire i dati del modulo XML con una progettazione di modulo creata in Designer per creare un flusso di output di documenti in vari formati.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e99b72d0-fbd5-4150-a225-1a91ad4c5867
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: ht
source-wordcount: '260'
ht-degree: 100%

---

# Panoramica sul servizio di output {#overview-of-output-service}

L’output consente di unire i dati del modulo XML con una progettazione di modulo creata in Designer per creare un flusso di output di documenti in vari formati. Il flusso di output può essere inviato a una stampante di rete, a una stampante locale o a un file su disco

Puoi utilizzare la pagina Output nella console di amministrazione per amministrare il servizio di output. Le impostazioni configurate vengono utilizzate in fase di esecuzione quando le impostazioni equivalenti non sono state specificate tramite l’API di AEM Forms. La configurazione eseguita tramite l’SDK di AEM Forms sostituisce le impostazioni configurate tramite la console di amministrazione.

Per ulteriori informazioni sul servizio di output, consulta [Riferimento servizi](https://www.adobe.com/go/learn_aemforms_services_61).

Nelle pagine di output della console di amministrazione puoi eseguire diverse attività:

* Specifica i set di caratteri per l’internazionalizzazione. Consulta [Modificare il set di caratteri](/help/forms/using/admin-help/change-character-set.md#change-the-character-set).
* Specifica percorsi assoluti e relativi per URL, URI, XCI e posizioni di file. Consulta [Specificare i percorsi dei file per l’output](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).)
* Configura le dimensioni e i criteri della cache. Consulta [Specifica della modalità cache](/help/forms/using/admin-help/configuring-caching-output.md#specifying-the-cache-mode) e [Configurazione delle impostazioni della cache](/help/forms/using/admin-help/configuring-caching-output.md#configuring-cache-settings).
* Rendi disponibili i tipi di carattere nel server applicazioni. Consulta [Rendere disponibili i font](/help/forms/using/admin-help/make-fonts-available.md#make-fonts-available).
* Specifica i caratteri da incorporare. Consulta [Specificare i font da incorporare](/help/forms/using/admin-help/specify-fonts-embed.md#specify-fonts-to-embed).
* Specifica le opzioni di configurazione XCI. Consulta [Specificare le opzioni di configurazione XCI](/help/forms/using/admin-help/specify-xci-configuration-options.md#specify-xci-configuration-options).
* Specifica le impostazioni di protezione. Consulta [Specificare le impostazioni di protezione](/help/forms/using/admin-help/specify-security-settings.md#specify-security-settings).

Dopo aver modificato le impostazioni, fai clic su Salva per applicarle all’output. Non è necessario riavviare il server per rendere effettive le modifiche, ma potrebbe essere necessario riavviare il servizio di output durante la configurazione delle impostazioni della cache.
