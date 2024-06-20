---
title: Informazioni sulla struttura delle cartelle
description: Come comprendere la struttura di cartelle del codice sorgente dell’area di lavoro AEM Forms da personalizzare.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: a4c1d3d8-477e-4edf-9dde-4ef9c766be5a
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms, Adaptive Forms
role: Admin, User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# Informazioni sulla struttura delle cartelle {#understanding-the-folder-structure}

I componenti dell’area di lavoro AEM Forms sono progettati sull’architettura MVC utilizzando Backbone. Ogni componente ha un file per:

* Modello, che contiene la logica di business.
* Modello, un file HTML contenente controlli di interfaccia.
* Visualizza, che funge da classe Controller per Template.

Le risorse di tutti i componenti si trovano nella struttura di cartelle descritta di seguito. Per accedere alle risorse, accedi a CRXDE Liti e passa a `/libs/ws/js/runtime/`.

**modelli** Contiene modelli di spina dorsale.

**visualizzazioni** Contiene le viste della spina dorsale.

**modelli** Contiene solo i modelli di HTML per i componenti.

**percorsi** Contiene percorsi universali. La cartella Templates all’interno delle route contiene il codice HTML e i riferimenti ai componenti.

**servizi** Contiene l’interfaccia di servizio per chiamare le API del server Adobe Experience Manager sull’endpoint REST.

**fino al** Contiene utility generiche utilizzabili da più componenti.
