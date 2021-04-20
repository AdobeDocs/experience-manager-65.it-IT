---
title: Consegna sicura di informazioni ad alto volume
seo-title: Consegna sicura di informazioni ad alto volume
description: La sicurezza dei documenti supporta l’associazione di licenze agli utenti, anziché ai documenti negli ambienti di produzione di massa.
seo-description: La sicurezza dei documenti supporta l’associazione di licenze agli utenti, anziché ai documenti negli ambienti di produzione di massa.
uuid: 9747d283-506c-434e-9850-e50b95290cc8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b76d7d93-23a5-4c08-81f5-a56267b1556a
feature: Document Security
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---


# Consegna di informazioni sicure ad alto volume {#high-volume-secure-information-delivery}

In un ambiente di produzione di massa, come quello che genera fatture mensili protette per una società di telecomunicazioni, la creazione di licenze specifiche per ogni documento può diventare un processo ad alta intensità di risorse. In questi casi, la sicurezza dei documenti supporta l&#39;associazione di licenze agli utenti, anziché ai documenti. La licenza generata per un utente viene utilizzata per tutti i documenti protetti per tale utente.

Uno dei vantaggi di questo approccio è che la dimensione del database di sicurezza dei documenti non cresce in modo lineare con i documenti, ma con il numero di utenti. Inoltre, poiché è necessario creare la licenza una sola volta per un utente, la successiva protezione dei documenti attraverso questi criteri diventa più veloce. Funzionalità quali accesso offline, scadenza dei documenti e revoca sono supportate per tutti questi documenti.

La sicurezza dei documenti supporta anche i criteri astratti. I criteri astratti sono modelli di criteri che contengono tutti gli attributi dei criteri, ad esempio le impostazioni di protezione dei documenti e i diritti di utilizzo, ma non contengono un elenco di entità. Gli amministratori possono creare un numero qualsiasi di criteri dal criterio astratto con entità diverse che devono avere accesso ai documenti. Le modifiche apportate al criterio astratto non influiscono sui criteri effettivi generati dai criteri astratti.

Nel caso della generazione di fatture mensili per un&#39;azienda di telefonia, si crea una politica astratta, si creano utenti e quindi si generano licenze univoche per ogni utente. Le licenze vengono successivamente applicate ai documenti per ogni utente.

La creazione di un criterio astratto è supportata solo tramite l’SDK Java per la sicurezza dei documenti. Tuttavia, è possibile amministrare i criteri creati dal criterio astratto dalle pagine web di sicurezza dei documenti. I criteri creati utilizzando questo metodo hanno un comportamento identico a quelli creati dalle pagine Web di sicurezza dei documenti.

Per ulteriori informazioni, vedere [Programmazione con AEM moduli](https://www.adobe.com/go/learn_aemforms_programming_63) .
