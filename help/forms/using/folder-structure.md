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
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 97aafc4b-2598-52d6-9012-295a95969e38
    internal-label: HTML5 Forms
  - id: 59f95943-e802-56ac-990d-21ab923984c1
    internal-label: Mobile Forms
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 5%
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
