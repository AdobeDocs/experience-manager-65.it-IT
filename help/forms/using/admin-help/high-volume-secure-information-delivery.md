---
title: Consegna sicura delle informazioni a volumi elevati
seo-title: High-volume secure information delivery
description: Document Security supporta l’associazione delle licenze agli utenti, anziché ai documenti negli ambienti di produzione di massa.
seo-description: Document security supports the association of licenses to users, rather than to the documents in mass production environments.
uuid: 9747d283-506c-434e-9850-e50b95290cc8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b76d7d93-23a5-4c08-81f5-a56267b1556a
feature: Document Security
exl-id: 616e8821-ca96-4471-9120-0e1076a06178
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 0%

---

# Consegna sicura delle informazioni a volumi elevati {#high-volume-secure-information-delivery}

In un ambiente di produzione di massa, ad esempio quello che genera fatture mensili protette per una società di telecomunicazioni, la creazione di licenze specifiche per ciascun documento può diventare un processo che richiede molte risorse. In questi casi, la protezione dei documenti supporta l&#39;associazione delle licenze agli utenti anziché ai documenti. La licenza generata per un utente viene utilizzata per tutti i documenti protetti per tale utente.

Uno dei vantaggi di questo approccio è che le dimensioni del database di protezione dei documenti non crescono in modo lineare con i documenti, ma con il numero di utenti. Inoltre, poiché è necessario creare la licenza una sola volta per un utente, la successiva protezione dei documenti tramite queste policy diventa più veloce. Funzionalità quali l&#39;accesso offline, la scadenza e la revoca dei documenti sono supportate per tutti questi documenti.

La protezione dei documenti supporta anche Criteri astratti. I criteri astratti sono modelli di criteri che contengono tutti gli attributi dei criteri, ad esempio le impostazioni di protezione dei documenti e i diritti di utilizzo, ma non contengono un elenco di entità principali. Gli amministratori possono creare un numero qualsiasi di criteri dalla policy astratta con entità diverse che devono avere accesso ai documenti. Le modifiche apportate al criterio astratto non influiscono sui criteri effettivi generati dai criteri astratti.

Se viene generata una fattura mensile per una società di telecomunicazioni, è possibile creare una policy astratta, creare utenti e quindi generare licenze univoche per ogni utente. Le licenze vengono successivamente applicate ai documenti per ogni utente.

La creazione di un criterio astratto è supportata solo tramite l’SDK Java per la sicurezza dei documenti. È tuttavia possibile amministrare i criteri creati dai criteri astratti dalle pagine Web di Document Security. I criteri creati con questo metodo hanno lo stesso comportamento di quelli creati dalle pagine Web di Document Security.

Consulta [Programmazione con i moduli AEM](https://www.adobe.com/go/learn_aemforms_programming_63) per ulteriori informazioni.
