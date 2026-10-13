---
title: Minificazione dei file JavaScript
description: Istruzioni per generare codice ridotto dopo le personalizzazioni dell’area di lavoro di AEM Forms per ottimizzare i file JS per il web.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: d88c6831-8ae9-426d-acb5-2a7e066ad158
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
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
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 6%
---
# Minificazione dei file JavaScript {#minification-of-the-javascript-files}

La minimizzazione rimuove dal codice sorgente i caratteri ridondanti, come spazi vuoti, nuove righe e commenti. Questo migliora le prestazioni riducendo le dimensioni del codice. Anche se la minimizzazione non influisce sulla funzionalità, riduce la leggibilità del codice.

Per generare un codice minimizzato per le modifiche semantiche, segui la procedura riportata di seguito.

1. Copia `client-html/src/main/webapp/js` da src-package nel file system.

   >[!NOTE]
   >
   >Per ulteriori dettagli sui pacchetti, vedere [Introduzione alla personalizzazione dell&#39;area di lavoro di AEM Forms](/help/forms/using/introduction-customizing-html-workspace.md).

1. Aggiorna i percorsi in `main.js` che si trovano in client-html/src/main/webapp/js, per modelli/visualizzazioni aggiunti/aggiornati.

   Ad esempio, l&#39;aggiunta di un nuovo modello Sharequeue, ad esempio mySharequeue, cambia:

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/models/sharequeue',
   ```

   A

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/myModels/mySharequeue',
   ```

1. Aggiornare `registry-config.xml, located at client-html/src/main/webapp/js/resource_generator,` in caso di modifica/aggiunta dell&#39;alias in `main.js`.

   Ad esempio, l&#39;aggiunta di un nuovo modello Sharequeue, ad esempio mySharequeue, cambia:

   ```xml
   <sharequeue
               name="sharequeue"
               path="runtime/models/sharequeue.js"
               service="service"/>
   ```

   A

   ```xml
   <sharequeue
               name="sharequeue"
               path="runtime/myModels/mySharequeue.js"
               service="service"/>
   ```

1. In client-html/src/main/webapp/js/minifier, esegui il comando:

   ```shell
   mvn clean install
   ```

   Genera una cartella di file minimizzati, in client-html/src/main/webapp/js con main.js minimizzato e registry.js.

>[!NOTE]
>
>La minimizzazione funziona solo su una JVM a 64 bit.

>[!NOTE]
>
>Se minimizzi, l’aggiornamento è interessato.
