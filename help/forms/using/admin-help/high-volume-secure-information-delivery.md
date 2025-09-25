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
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '320'
ht-degree: 100%

---

# Consegna sicura delle informazioni con volumi elevati {#high-volume-secure-information-delivery}

In un ambiente di produzione di massa, ad esempio quello che genera fatture mensili protette per una società di telecomunicazioni, la creazione di licenze specifiche per ciascun documento può diventare un processo che richiede molte risorse. In questi casi, la protezione dei documenti supporta l’associazione delle licenze agli utenti anziché ai documenti. La licenza generata per un utente viene utilizzata per tutti i documenti protetti per tale utente.

Un vantaggio di questo approccio è che le dimensioni del database di protezione dei documenti non crescono in modo lineare con i documenti, ma con il numero di utenti. Inoltre, poiché è necessario creare la licenza una sola volta per un utente, la successiva protezione dei documenti diventa più veloce tramite questi criteri. Funzioni quali l’accesso offline, la scadenza e la revoca dei documenti sono supportate per tutti questi documenti.

La protezione dei documenti supporta anche Criteri astratti. I criteri astratti sono modelli di criteri che contengono tutti gli attributi degli stessi, ad esempio le impostazioni di protezione dei documenti e i diritti di utilizzo, ma non contengono un elenco di entità principali. Gli amministratori possono creare un numero qualsiasi di criteri dalla policy astratta con entità diverse che devono avere accesso ai documenti. Le modifiche apportate al criterio astratto non influiscono sui criteri effettivi generati dai criteri astratti.

Se viene generata una fattura mensile per una società di telecomunicazioni, è possibile creare un criterio astratto, creare utenti e quindi generare licenze univoche per ciascun utente. Le licenze vengono successivamente applicate ai documenti per ogni utente.

La creazione di un criterio astratto è supportata solo tramite Java SDK per la protezione dei documenti. È tuttavia possibile amministrare i criteri creati dai quelli astratti dalle pagine web sulla sicurezza dei documenti. I criteri creati con questo metodo hanno lo stesso comportamento di quelli creati dalle pagine web sulla sicurezza dei documenti.

Per ulteriori informazioni, vedi [Programmazione con AEM Forms](https://www.adobe.com/go/learn_aemforms_programming_63_it).
