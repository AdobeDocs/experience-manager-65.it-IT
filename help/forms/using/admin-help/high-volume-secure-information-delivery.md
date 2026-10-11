---
title: Consegna sicura delle informazioni con volumi elevati
description: Protezione dei documenti supporta l’associazione delle licenze agli utenti, anziché ai documenti negli ambienti di produzione di massa.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
exl-id: 616e8821-ca96-4471-9120-0e1076a06178
solution: Experience Manager, Experience Manager Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 50158d81-1c06-57f7-8bd7-e8ff76a93f85
    internal-label: Document Security
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 100%
---
# Consegna sicura delle informazioni con volumi elevati {#high-volume-secure-information-delivery}

In un ambiente di produzione di massa, ad esempio quello che genera fatture mensili protette per una società di telecomunicazioni, la creazione di licenze specifiche per ciascun documento può diventare un processo che richiede molte risorse. In questi casi, la protezione dei documenti supporta l’associazione delle licenze agli utenti anziché ai documenti. La licenza generata per un utente viene utilizzata per tutti i documenti protetti per tale utente.

Un vantaggio di questo approccio è che le dimensioni del database di protezione dei documenti non crescono in modo lineare con i documenti, ma con il numero di utenti. Inoltre, poiché è necessario creare la licenza una sola volta per un utente, la successiva protezione dei documenti diventa più veloce tramite questi criteri. Funzioni quali l’accesso offline, la scadenza e la revoca dei documenti sono supportate per tutti questi documenti.

La protezione dei documenti supporta anche Criteri astratti. I criteri astratti sono modelli di criteri che contengono tutti gli attributi degli stessi, ad esempio le impostazioni di protezione dei documenti e i diritti di utilizzo, ma non contengono un elenco di entità principali. Gli amministratori possono creare un numero qualsiasi di criteri dalla policy astratta con entità diverse che devono avere accesso ai documenti. Le modifiche apportate al criterio astratto non influiscono sui criteri effettivi generati dai criteri astratti.

Se viene generata una fattura mensile per una società di telecomunicazioni, è possibile creare un criterio astratto, creare utenti e quindi generare licenze univoche per ciascun utente. Le licenze vengono successivamente applicate ai documenti per ogni utente.

La creazione di un criterio astratto è supportata solo tramite Java SDK per la protezione dei documenti. È tuttavia possibile amministrare i criteri creati dai quelli astratti dalle pagine web sulla sicurezza dei documenti. I criteri creati con questo metodo hanno lo stesso comportamento di quelli creati dalle pagine web sulla sicurezza dei documenti.

Per ulteriori informazioni, vedi [Programmazione con AEM Forms](https://www.adobe.com/go/learn_aemforms_programming_63_it).
