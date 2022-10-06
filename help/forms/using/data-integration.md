---
title: Integrazione dei dati di AEM Forms
seo-title: AEM Forms Data Integration
description: L’integrazione dei dati consente di integrare AEM Forms con diverse origini dati e di creare un modello di dati per i moduli per creare e utilizzare moduli adattivi e comunicazioni interattive.
seo-description: Data Integration lets you integrate AEM Forms with disparate data sources and create form data model to create and work with adaptive forms and interactive communications.
uuid: 01df045e-1b26-437c-9674-fd223ecd5097
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integration
discoiquuid: e397c6ce-d73f-4183-8445-1897a8906960
docset: aem65
feature: Form Data Model
exl-id: dd1146e4-952d-4dfa-8084-46c6096c4177
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# [!DNL AEM Forms] Integrazione dei dati {#aem-forms-data-integration}

![](do-not-localize/data-integeration.png)

Le infrastrutture aziendali includono diversi sistemi back-end o origini dati come database, servizi web, servizi REST, servizi OData e soluzioni CRM. Insieme, creano un sistema informativo che distribuisce i dati alle applicazioni aziendali per eseguire attività quotidiane. D&#39;altro canto, le applicazioni acquisiscono i dati e li inviano nuovamente per aggiornare le origini dati.

[!DNL AEM Forms] applicazioni come moduli adattivi e comunicazioni interattive richiedono l’integrazione con le origini dati per recuperare i dati dei clienti durante il rendering dei moduli e la creazione di comunicazioni interattive. Ci sono casi d’uso in cui i dati vengono recuperati da origini dati in base agli input degli utenti nei moduli adattivi. Inoltre, i dati del modulo adattivo inviati possono essere riscritti per aggiornare le rispettive origini dati.

Mentre un sistema modulare distribuito ha i suoi vantaggi, la sfida consiste nell&#39;integrare e creare associazioni di dati tra le origini dati. L&#39;integrazione dei dati è la chiave per un&#39;infrastruttura aziendale funzionale ed efficiente con diverse fonti di dati collegate alle applicazioni per lo scambio di dati aziendali.

## Panoramica sull’integrazione dei dati {#data-integration-overview}

![integrazione aem-forms-data-data](assets/aem-forms-data-integeration.png)

[!DNL AEM Forms] L&#39;integrazione dei dati consente di configurare e collegare diverse origini dati con [!DNL AEM Forms]. Offre un’interfaccia utente intuitiva per creare uno schema di rappresentazione dei dati unificato di entità e servizi aziendali tra origini dati collegate. La rappresentazione unificata è nota come modello di dati modulo, un&#39;estensione dello schema JSON. Le entità in un modello dati modulo sono definite oggetti modello dati. Un modello dati modulo consente di:

* Accedere a oggetti, proprietà e servizi del modello dati da origini dati connesse.
* Creazione di oggetti e proprietà del modello dati personalizzato
* Creare associazioni tra oggetti del modello dati all’interno e tra origini dati.
* Richiamare i servizi oggetti del modello dati per eseguire query o scrivere dati da e verso origini dati.

Una volta creato un modello dati modulo, è possibile utilizzarlo in vari flussi di lavoro per moduli adattivi e comunicazioni interattive, ad esempio:

* Creazione di moduli adattivi e comunicazioni interattive basate sul modello dati del modulo
* Precompilazione di moduli adattivi e comunicazioni interattive da origini dati configurate
* Richiamare servizi/operazioni dell’origine dati utilizzando le regole del modulo adattivo
* Scrittura dei dati del modulo adattivo inviati alle origini dati

## Guida introduttiva all’integrazione dei dati {#get-started-with-data-integration}

Il primo passaggio per implementare l’integrazione dei dati consiste nell’identificare e configurare le origini dati che memorizzano le informazioni da sfruttare nei casi di utilizzo di moduli adattivi e comunicazioni interattive. Successivamente, si crea un modello dati modulo che utilizza oggetti, proprietà e servizi del modello dati da una o più origini dati. È possibile creare moduli adattivi e comunicazioni interattive basate su un modello di dati modulo in cui i campi o i segnaposto dei moduli adattivi nelle comunicazioni interattive sono associati alle rispettive proprietà dell’origine dati.

[!DNL AEM Forms] consente inoltre di creare un modello dati modulo indipendente dalle origini dati e di associare o associare successivamente oggetti e proprietà del modello dati al modello dati del modulo con un’origine dati. Elimina tutte le dipendenze dalle origini dati mentre si lavora su un modello dati modulo.

Consulta i seguenti argomenti per iniziare, comprendere e implementare l’integrazione dei dati.

* [Configurare origini dati](../../forms/using/configure-data-sources.md)
* [Crea modello dati modulo](../../forms/using/create-form-data-models.md)
* [Utilizzare il modello dati del modulo](../../forms/using/work-with-form-data-model.md)
* [Utilizzare il modello dati del modulo](../../forms/using/using-form-data-model.md)
