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
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 2%

---

# Aggiornamento del collegamento alla documentazione {#updating-the-link-to-the-documentation}

Puoi accedere al contenuto predefinito della guida per l’area di lavoro di AEM Forms selezionando **Aiuto > Aiuto di Workspace**. Fa riferimento alla documentazione online sul sito web di Adobe. Tuttavia, puoi aggiornarla per puntare a qualsiasi altro URL.

Considera i seguenti casi d’uso in cui potresti voler modificare l’URL predefinito della guida:

* Per fornire assistenza localizzata in una lingua a scelta.
* Per fornire contenuti di supporto personalizzati per l&#39;area di lavoro personalizzata.

Per aggiornare l’URL della documentazione online, segui la [Passaggi generici della personalizzazione](/help/forms/using/generic-steps-html-workspace-customization.md) e quindi i seguenti passaggi.

1. Copia il `userinfo.html` file da `/libs/ws/js/runtime/templates` a `/apps/ws/js/runtime/templates`.
1. Modifica:

   ```html
   <ul class="helpmenu">
     <li>
       <a href="https://www.adobe.com/go/learn_aemforms_documentation_63" title="<%= $.t('index.header.dropdown.WorkspaceHelp')%>" target="_blank"><%= $.t('index.header.dropdown.WorkspaceHelp')%></a>
     </li>
   ```

   in

   ```html
   <ul class="helpmenu">
     <li>
       <a href="<!--place new help url here-->" title="<%= $.t('index.header.dropdown.WorkspaceHelp')%>" target="_blank"><%= $.t('index.header.dropdown.WorkspaceHelp')%></a>
     </li>
   ```

1. Effettua le seguenti operazioni:

   1. Apri /apps/ws/js/registry.js per la modifica.
   1. Cerca e sostituisci `text!/lc/libs/ws/js/runtime/templates/userinfo.html` con `text!/lc/apps/ws/js/runtime/templates/userinfo.html`.
