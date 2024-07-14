---
title: Informazioni sulla struttura delle cartelle
description: Come comprendere la struttura di cartelle del codice sorgente dell’area di lavoro AEM Forms da personalizzare.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: a4c1d3d8-477e-4edf-9dde-4ef9c766be5a
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
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

**modelli** contiene modelli di backbone.

**visualizzazioni** Contiene visualizzazioni backbone.

**modelli** contiene solo i modelli HTML per i componenti.

**route** contiene route universali. La cartella Templates all’interno delle route contiene il codice HTML e i riferimenti ai componenti.

**servizi** contiene l&#39;interfaccia di servizio per chiamare le API del server Adobe Experience Manager sull&#39;endpoint REST.

**util** contiene utilità generiche utilizzabili da più componenti.
