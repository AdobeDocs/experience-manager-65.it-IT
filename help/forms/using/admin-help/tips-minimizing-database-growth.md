---
title: Suggerimenti per ridurre al minimo la crescita del database
seo-title: Suggerimenti per ridurre al minimo la crescita del database
description: I processi di lunga durata memorizzano i dati del processo nel database dei moduli di AEM. La crescita del database dei moduli AEM può essere ridotta al minimo utilizzando alcune semplici strategie di progettazione del processo e configurazione del prodotto.
seo-description: I processi di lunga durata memorizzano i dati del processo nel database dei moduli di AEM. La crescita del database dei moduli AEM può essere ridotta al minimo utilizzando alcune semplici strategie di progettazione del processo e configurazione del prodotto.
uuid: 13f99d4f-848e-451e-90d9-55e202dc0bdb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 89441336-babc-4d1f-9053-d1566cd42d22
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 0%

---


# Suggerimenti per ridurre al minimo la crescita del database {#tips-for-minimizing-database-growth}

I processi di lunga durata memorizzano i dati del processo nel database dei moduli di AEM. La crescita del database dei moduli AEM può essere ridotta al minimo utilizzando alcune semplici strategie di progettazione del processo e configurazione del prodotto.

## Suggerimenti per la progettazione del processo {#process-design-tips}

Utilizzare processi di breve durata quando possibile. I processi di breve durata non memorizzano i dati di processo nel database. Lo svantaggio di utilizzare i processi di breve durata è che il loro stato e stato non sono tracciati nella console di amministrazione e non c&#39;è alcuna storia del processo.

Alcune operazioni di servizio, come l&#39;operazione Assegna attività (servizio utente), richiedono che siano utilizzate in processi longevi. In questo caso, potete segmentare il processo in diversi sottoprocessi e renderlo di breve durata quando possibile. Se si utilizza questa strategia, i processi secondari di breve durata devono gestire elementi di dati di grandi dimensioni, come i valori del documento.

Usare le variabili con cautela. Quando si utilizzano processi longevi, per ogni istanza di processo viene allocato spazio nel database per ogni variabile del processo. L&#39;uso strategico delle variabili può risparmiare una notevole quantità di spazio. Ad esempio, è possibile sovrascrivere i valori delle variabili quando nel processo non sono più necessari valori precedenti. Eliminate inoltre tutte le variabili create e non utilizzate. È possibile convalidare il processo per trovare le variabili non utilizzate.

Utilizzate tipi di variabili semplici (ad esempio, stringa o int) ed evitate di utilizzare tipi di variabili complesse quando possibile. Lo spazio del database è allocato per le variabili anche se non contengono un valore. Le variabili complesse in genere richiedono più spazio rispetto a quelle semplici.

## Suggerimenti per l&#39;amministrazione dei prodotti {#product-administration-tips}

Utilizzate l&#39;archiviazione globale dei documenti (GDS) in modo efficace. La directory GDS sul server dei moduli viene utilizzata per memorizzare, tra le altre cose, i file che vengono passati ai servizi che fanno parte di moduli AEM nei processi. Per migliorare le prestazioni, i documenti più piccoli vengono invece memorizzati e memorizzati nel database.

la console di amministrazione espone la proprietà Default Document Max Inline Size (Dimensione massima documento in linea) per configurare la dimensione massima dei documenti memorizzati e memorizzati nel database. (Vedere [Configurare le impostazioni generali dei moduli AEM](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings).) Se si imposta questa proprietà su un valore basso, la maggior parte dei documenti viene mantenuta nella directory GDS anziché nel database. Il vantaggio è che si può eliminare più facilmente i file quando non sono più necessari quando sono memorizzati nella directory GDS.
