---
title: Informazioni sulla struttura delle cartelle
seo-title: Informazioni sulla struttura delle cartelle
description: Come comprendere la struttura di cartelle del codice sorgente dell’area di lavoro di AEM Forms da personalizzare.
seo-description: Come comprendere la struttura di cartelle del codice sorgente dell’area di lavoro di AEM Forms da personalizzare.
uuid: ee844f89-887e-4f07-9db3-389859baa374
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 7427858d-8eec-423d-a0a9-444140420620
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Informazioni sulla struttura delle cartelle {#understanding-the-folder-structure}

I componenti dell’area di lavoro di AEM Forms sono progettati sull’architettura MVC mediante l’utilizzo di Backbone. Ogni componente ha un file per:

* Modello, che contiene logica di business.
* Modello, ovvero un file HTML contenente controlli di interfaccia.
* Visualizza, che funge da classe Controller in Modello.

Le risorse per tutti i componenti si trovano nella struttura di cartelle descritta di seguito. Per accedere alle risorse, accedete a CRXDE Lite e individuate `/libs/ws/js/runtime/`.

**modelli** Contiene modelli di dorsale.

**viste** Contiene le viste della colonna vertebrale.

**modelli** Contiene solo i modelli HTML per i componenti.

**route** Contiene route universali. La cartella Templates all&#39;interno delle route contiene il codice HTML e i riferimenti ai componenti.

**services** Contiene l’interfaccia del servizio per chiamare le API del server Adobe Experience Manager sull’endpoint REST.

**util** Contiene utility generiche utilizzabili da più componenti.
