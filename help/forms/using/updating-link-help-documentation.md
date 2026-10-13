---
title: Aggiornamento del collegamento alla documentazione
description: Aggiornare la destinazione del collegamento della Guida di Workspace nell’area di lavoro di AEM Forms in modo che punti al collegamento alla documentazione personalizzata.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: ca637bea-05c1-4920-9283-e782f07607de
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
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
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 11%
---
# Aggiornamento del collegamento alla documentazione {#updating-the-link-to-the-documentation}

È possibile accedere al contenuto predefinito della Guida per l&#39;area di lavoro di AEM Forms selezionando **Guida > Guida di Workspace**. Fa riferimento alla documentazione online sul sito web di Adobe. Tuttavia, puoi aggiornarla per puntare a qualsiasi altro URL.

Considera i seguenti casi d’uso in cui potresti voler modificare l’URL predefinito della guida:

* Per fornire assistenza localizzata in una lingua a scelta.
* Per fornire contenuti di supporto personalizzati per l&#39;area di lavoro personalizzata.

Per aggiornare l&#39;URL della documentazione online, seguire i [passaggi generici della personalizzazione](/help/forms/using/generic-steps-html-workspace-customization.md) e i passaggi seguenti.

1. Copia il file `userinfo.html` da `/libs/ws/js/runtime/templates` a `/apps/ws/js/runtime/templates`.
1. Modifica:

   ```html
   <ul class="helpmenu">
     <li>
       <a href="https://www.adobe.com/go/learn_aemforms_documentation_63" title="<%= $.t('index.header.dropdown.WorkspaceHelp')%>" target="_blank"><%= $.t('index.header.dropdown.WorkspaceHelp')%></a>
     </li>
   ```

   a

   ```html
   <ul class="helpmenu">
     <li>
       <a href="<!--place new help url here-->" title="<%= $.t('index.header.dropdown.WorkspaceHelp')%>" target="_blank"><%= $.t('index.header.dropdown.WorkspaceHelp')%></a>
     </li>
   ```

1. Effettua le seguenti operazioni:

   1. Apri /apps/ws/js/registry.js per la modifica.
   1. Cerca e sostituisci `text!/lc/libs/ws/js/runtime/templates/userinfo.html` con `text!/lc/apps/ws/js/runtime/templates/userinfo.html`.
