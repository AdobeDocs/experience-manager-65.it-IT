---
title: Integrazione dei dati  AEM Forms
seo-title: Integrazione dei dati  AEM Forms
description: L'integrazione dei dati consente di integrare  AEM Forms con origini dati diverse e di creare un modello di dati per i moduli per creare e utilizzare moduli adattivi e comunicazioni interattive.
seo-description: L'integrazione dei dati consente di integrare  AEM Forms con origini dati diverse e di creare un modello di dati per i moduli per creare e utilizzare moduli adattivi e comunicazioni interattive.
uuid: 01df045e-1b26-437c-9674-fd223ecd5097
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integration
discoiquuid: e397c6ce-d73f-4183-8445-1897a8906960
docset: aem65
translation-type: tm+mt
source-git-commit: 4e0709031aca030e50840811a9b3717f3cb20340
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---


# [!DNL AEM Forms] Integrazione dei dati {#aem-forms-data-integration}

![](do-not-localize/data-integeration.png)

Le infrastrutture aziendali includono diversi sistemi back-end o origini dati come database, servizi Web, servizi REST, servizi OData e soluzioni CRM. Insieme, creano un sistema informativo che trasmette dati alle applicazioni aziendali per svolgere attività quotidiane. D&#39;altro canto, le applicazioni acquisiscono i dati e li inviano di nuovo per aggiornare le origini dati.

[!DNL AEM Forms] applicazioni come moduli adattivi e comunicazioni interattive richiedono l&#39;integrazione con le origini dati per recuperare i dati dei clienti durante il rendering dei moduli e la creazione di comunicazioni interattive. Esistono casi d&#39;uso in cui i dati vengono estratti da origini dati in base agli input dell&#39;utente nei moduli adattivi. Inoltre, i dati del modulo adattivo inviati possono essere riscritti per aggiornare le rispettive origini dati.

Mentre un sistema modulare distribuito ha i propri vantaggi, la sfida consiste nell&#39;integrare e creare associazioni di dati tra le origini dati. L&#39;integrazione dei dati è la chiave per un&#39;infrastruttura aziendale funzionale ed efficiente con origini dati diverse collegate alle applicazioni per lo scambio di dati aziendali.

## Panoramica sull&#39;integrazione dei dati {#data-integration-overview}

![integrazione AEM-forms-data](assets/aem-forms-data-integeration.png)

[!DNL AEM Forms] L&#39;integrazione dei dati consente di configurare e collegare origini dati diverse con [!DNL AEM Forms]. Fornisce un&#39;interfaccia utente intuitiva per creare uno schema di rappresentazione dati unificato di entità e servizi aziendali tra origini dati connesse. La rappresentazione unificata è nota come modello dati modulo, un&#39;estensione dello schema JSON. Le entità in un modello dati modulo sono definite oggetti modello dati. Un modello dati del modulo consente di:

* Accesso a oggetti, proprietà e servizi del modello dati da origini dati connesse.
* Creazione di oggetti e proprietà del modello dati personalizzato
* Creare associazioni tra gli oggetti del modello dati all&#39;interno e tra le origini dati.
* Richiama i servizi oggetti del modello dati per eseguire query o scrivere dati da e verso origini dati.

Dopo aver creato un modello dati del modulo, è possibile utilizzarlo in vari flussi di lavoro per moduli adattivi e comunicazioni interattive, ad esempio:

* Creazione di moduli adattivi e comunicazioni interattive basate sul modello dati del modulo
* Precompilare moduli adattivi e comunicazioni interattive da origini dati configurate
* Richiamo di servizi/operazioni dell&#39;origine dati utilizzando le regole del modulo adattivo
* Scrittura dei dati del modulo adattivo inviati alle origini dati

## Introduzione all&#39;integrazione dei dati {#get-started-with-data-integration}

Il primo passo per implementare l&#39;integrazione dei dati è identificare e configurare le origini dati che archiviano le informazioni da utilizzare nei moduli adattivi e nei casi di utilizzo delle comunicazioni interattive. Successivamente, si crea un modello dati modulo che utilizza oggetti, proprietà e servizi del modello dati da una o più origini dati. È possibile creare moduli adattivi e comunicazioni interattive basate su un modello di dati del modulo in cui i campi o i segnaposto dei moduli adattivi nelle comunicazioni interattive sono associati alle rispettive proprietà dell&#39;origine dati.

[!DNL AEM Forms] consente inoltre di creare un modello dati modulo indipendente dalle origini dati e di associare o collegare successivamente oggetti e proprietà del modello dati nel modello dati del modulo con un&#39;origine dati. Elimina tutte le dipendenze dalle origini dati mentre si lavora su un modello dati del modulo.

Per iniziare, comprendere e implementare l&#39;integrazione dei dati, consulta quanto segue.

* [Configurare le origini dati](../../forms/using/configure-data-sources.md)
* [Crea modello dati modulo](../../forms/using/create-form-data-models.md)
* [Uso del modello dati del modulo](../../forms/using/work-with-form-data-model.md)
* [Usa modello dati modulo](../../forms/using/using-form-data-model.md)

