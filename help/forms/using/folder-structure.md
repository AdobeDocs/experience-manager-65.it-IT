---
title: Informazioni sulla struttura delle cartelle
seo-title: Understanding the folder structure
description: Informazioni sulla struttura delle cartelle del codice sorgente dell’area di lavoro di AEM Forms da personalizzare.
seo-description: How to understand the folder structure of AEM Forms workspace source code to customize.
uuid: ee844f89-887e-4f07-9db3-389859baa374
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 7427858d-8eec-423d-a0a9-444140420620
exl-id: a4c1d3d8-477e-4edf-9dde-4ef9c766be5a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# Informazioni sulla struttura delle cartelle {#understanding-the-folder-structure}

I componenti dell’area di lavoro di AEM Forms sono progettati sull’architettura MVC utilizzando Backbone. Ogni componente ha un file per:

* Modello, che contiene la logica di business.
* Modello, ovvero un file HTML contenente i controlli dell’interfaccia.
* Visualizza, che funge da classe Controller in Modello.

Le risorse per tutti i componenti vengono posizionate nella struttura di cartelle descritta di seguito. Per accedere alle risorse, accedi a CRXDE Lite e sfoglia fino a `/libs/ws/js/runtime/`.

**modelli** Contiene modelli di dorsale.

**visualizzazioni** Contiene le visualizzazioni della spina dorsale.

**modelli** Contiene solo i modelli di HTML per i componenti.

**rotte** Contiene percorsi universali. La cartella Templates all&#39;interno delle route contiene il codice HTML e i riferimenti ai componenti.

**servizi** Contiene l’interfaccia del servizio per chiamare le API del server Adobe Experience Manager sull’endpoint REST.

**util** Contiene utilità generiche utilizzabili da più componenti.
