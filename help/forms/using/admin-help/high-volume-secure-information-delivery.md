---
title: Distribuzione sicura delle informazioni ad alto volume
seo-title: Distribuzione sicura delle informazioni ad alto volume
description: Document Security supporta l'associazione di licenze agli utenti, anziché ai documenti negli ambienti di produzione di massa.
seo-description: Document Security supporta l'associazione di licenze agli utenti, anziché ai documenti negli ambienti di produzione di massa.
uuid: 9747d283-506c-434e-9850-e50b95290cc8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b76d7d93-23a5-4c08-81f5-a56267b1556a
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---


# Distribuzione di informazioni sicure ad alto volume {#high-volume-secure-information-delivery}

In un ambiente di produzione di massa, come quello in cui vengono generate fatture mensili protette per una società di telecomunicazioni, la creazione di licenze specifiche per ciascun documento può diventare un processo ad alta intensità di risorse. In tali casi, Document Security supporta l&#39;associazione di licenze agli utenti, anziché ai documenti. La licenza generata per un utente viene utilizzata per tutti i documenti protetti per tale utente.

Uno dei vantaggi di questo approccio è che la dimensione del database di protezione dei documenti non aumenta in modo lineare con i documenti, ma con il numero di utenti. Inoltre, poiché è necessario creare la licenza una sola volta per un utente, la successiva protezione dei documenti attraverso questi criteri diventa più rapida. Funzionalità quali accesso offline, scadenza dei documenti e revoca sono supportate per tutti questi documenti.

Document Security supporta anche i criteri astratti. I criteri astratti sono modelli di criteri che contengono tutti gli attributi dei criteri, ad esempio le impostazioni di protezione dei documenti e i diritti di utilizzo, ma non contengono un elenco di entità. Gli amministratori possono creare un numero qualsiasi di criteri dal criterio astratto con entità diverse che devono avere accesso ai documenti. Le modifiche apportate al criterio astratto non influiscono sui criteri effettivi generati dai criteri astratti.

Nel caso della generazione mensile di fatture per una società di telecomunicazioni, create un criterio astratto, create utenti e quindi generate licenze univoche per ogni utente. Le licenze vengono successivamente applicate ai documenti per ogni utente.

La creazione di un criterio astratto è supportata solo tramite l&#39;SDK Java per la protezione dei documenti. È tuttavia possibile amministrare i criteri creati dai criteri astratti dalle pagine Web di protezione dei documenti. I criteri creati con questo metodo hanno lo stesso comportamento di quelli creati con le pagine Web per la protezione dei documenti.

Per ulteriori informazioni, vedere [Programmazione con moduli AEM](https://www.adobe.com/go/learn_aemforms_programming_63).
