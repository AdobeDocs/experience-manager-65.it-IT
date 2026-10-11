---
title: Suggerimenti per ridurre al minimo la crescita del database
description: I processi di lunga durata memorizzano i dati di processo nel database di AEM Forms. La crescita del database di AEM Forms può essere ridotta al minimo utilizzando alcune semplici strategie di progettazione dei processi e configurazione dei prodotti.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: f64efb06-815a-4608-ba1c-39e22f344ebb
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 3%
---
# Suggerimenti per ridurre al minimo la crescita del database {#tips-for-minimizing-database-growth}

I processi di lunga durata memorizzano i dati di processo nel database di AEM Forms. La crescita del database di AEM Forms può essere ridotta al minimo utilizzando alcune semplici strategie di progettazione dei processi e configurazione dei prodotti.

## Suggerimenti per la progettazione dei processi {#process-design-tips}

Se possibile, utilizza processi di breve durata. I processi di breve durata non memorizzano i dati di processo nel database. L’utilizzo di processi di breve durata presenta lo svantaggio di non tenere traccia dello stato e della console di amministrazione e di non disporre di una cronologia del processo.

Alcune operazioni di servizio, come l&#39;operazione Assegna attività (servizio utente), richiedono l&#39;utilizzo in processi di lunga durata. In questo caso, è possibile segmentare il processo in diversi sottoprocessi e renderli di breve durata quando possibile. Se si utilizza questa strategia, i sottoprocessi di breve durata devono gestire elementi di dati di grandi dimensioni, ad esempio i valori dei documenti.

Utilizza le variabili con moderazione. Quando si utilizzano processi di lunga durata, per ogni istanza di processo viene allocato spazio nel database per ogni variabile del processo. L’uso strategico delle variabili può risparmiare una notevole quantità di spazio. Ad esempio, puoi sovrascrivere i valori delle variabili quando i vecchi valori non sono più necessari nel processo. Ed elimina tutte le variabili create e non utilizzate. Puoi convalidare il processo per trovare le variabili non utilizzate.

Utilizza tipi di variabili semplici (ad esempio stringa o int) ed evita di utilizzare tipi di variabili complessi quando possibile. Lo spazio del database viene allocato per le variabili anche quando non contengono un valore. Le variabili complesse in genere richiedono più spazio rispetto a quelle semplici.

## Suggerimenti per l’amministrazione del prodotto {#product-administration-tips}

Utilizzo efficace dell&#39;archiviazione globale dei documenti (GDS). La directory GDS sul server Forms viene utilizzata per memorizzare, tra le altre cose, i file passati ai servizi che fanno parte di AEM Forms nei processi. Per migliorare le prestazioni, i documenti più piccoli vengono invece memorizzati in memoria e memorizzati nel database.

La console di amministrazione espone la proprietà Dimensione massima in linea documento predefinita per configurare la dimensione massima dei documenti memorizzati in memoria e memorizzati nel database. Consulta [Configurare le impostazioni generali di AEM Forms](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings). Se si imposta questa proprietà su un valore basso, la maggior parte dei documenti viene salvata in modo permanente nella directory GDS anziché nel database. Il vantaggio è che è possibile eliminare più facilmente i file quando non sono più necessari quando vengono memorizzati nella directory GDS.
