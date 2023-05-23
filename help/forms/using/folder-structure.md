---
title: Informazioni sulla struttura delle cartelle
seo-title: Understanding the folder structure
description: Come comprendere la struttura di cartelle del codice sorgente dell’area di lavoro AEM Forms da personalizzare.
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

I componenti dell’area di lavoro AEM Forms sono progettati sull’architettura MVC utilizzando Backbone. Ogni componente ha un file per:

* Modello, che contiene la logica di business.
* Modello, un file HTML contenente controlli di interfaccia.
* Visualizza, che funge da classe Controller per Template.

Le risorse di tutti i componenti si trovano nella struttura di cartelle descritta di seguito. Per accedere alle risorse, accedi a CRXDE Lite e passa a `/libs/ws/js/runtime/`.

**modelli** Contiene modelli di spina dorsale.

**visualizzazioni** Contiene le viste della spina dorsale.

**modelli** Contiene solo i modelli di HTML per i componenti.

**percorsi** Contiene percorsi universali. La cartella Templates all’interno delle route contiene il codice HTML e i riferimenti ai componenti.

**servizi** Contiene l’interfaccia di servizio per chiamare le API del server Adobe Experience Manager sull’endpoint REST.

**fino al** Contiene utility generiche utilizzabili da più componenti.
