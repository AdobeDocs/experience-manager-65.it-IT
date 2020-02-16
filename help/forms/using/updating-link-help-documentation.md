---
title: Aggiornamento del collegamento alla documentazione
seo-title: Aggiornamento del collegamento alla documentazione
description: Come aggiornare la destinazione del collegamento della guida di Workspace nell’area di lavoro Moduli AEM per fare riferimento al collegamento della documentazione personalizzato.
seo-description: Come aggiornare la destinazione del collegamento della guida di Workspace nell’area di lavoro Moduli AEM per fare riferimento al collegamento della documentazione personalizzato.
uuid: 64056d10-1451-44ed-8f25-81a21037dc75
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 788c427f-190f-4580-9efd-6a4c4a008837
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Aggiornamento del collegamento alla documentazione {#updating-the-link-to-the-documentation}

Per accedere al contenuto della guida predefinita per l’area di lavoro Moduli AEM, seleziona **Aiuto > Guida** di Workspace. Indica la documentazione online sul sito Web di Adobe. Tuttavia, potete aggiornarlo in modo che punti a qualsiasi altro URL.

Considerate i seguenti casi di utilizzo in cui potete modificare l’URL della guida predefinito:

* Per fornire assistenza localizzata in una lingua di vostra scelta.
* Per fornire contenuti della guida personalizzati per l’area di lavoro personalizzata.

Per aggiornare l’URL della documentazione online, seguite i passi [generici di personalizzazione](/help/forms/using/generic-steps-html-workspace-customization.md) e quindi i seguenti passaggi.

1. Copiate il `userinfo.html` file da `/libs/ws/js/runtime/templates` a `/apps/ws/js/runtime/templates`.
1. Cambia:

   ```
   <ul class="helpmenu">
     <li>
       <a href="https://www.adobe.com/go/learn_aemforms_documentation_63" title="<%= $.t('index.header.dropdown.WorkspaceHelp')%>" target="_blank"><%= $.t('index.header.dropdown.WorkspaceHelp')%></a>
     </li>
   ```

   a

   ```
   <ul class="helpmenu">
     <li>
       <a href="<!--place new help url here-->" title="<%= $.t('index.header.dropdown.WorkspaceHelp')%>" target="_blank"><%= $.t('index.header.dropdown.WorkspaceHelp')%></a>
     </li>
   ```

1. Effettua le seguenti operazioni:

   1. Aprite /apps/ws/js/registry.js per la modifica.
   1. Cerca e sostituisci `text!/lc/libs/ws/js/runtime/templates/userinfo.html` con `text!/lc/apps/ws/js/runtime/templates/userinfo.html`.

[Contattare il supporto](https://www.adobe.com/account/sign-in.supportportal.html)
