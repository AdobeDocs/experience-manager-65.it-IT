---
title: Minimizzazione dei file JavaScript
description: Istruzioni per generare codice ridotto dopo le personalizzazioni dell’area di lavoro di AEM Forms per ottimizzare i file JS per il web.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: d88c6831-8ae9-426d-acb5-2a7e066ad158
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 1%

---

# Minimizzazione dei file JavaScript {#minification-of-the-javascript-files}

La minimizzazione rimuove dal codice sorgente i caratteri ridondanti, come spazi vuoti, nuove righe e commenti. Questo migliora le prestazioni riducendo le dimensioni del codice. Anche se la minimizzazione non influisce sulla funzionalità, riduce la leggibilità del codice.

Per generare un codice minimizzato per le modifiche semantiche, segui la procedura riportata di seguito.

1. Copia `client-html/src/main/webapp/js` da src-package su filesystem.

   >[!NOTE]
   >
   >Consulta [Introduzione alla personalizzazione dell’area di lavoro di AEM Forms](/help/forms/using/introduction-customizing-html-workspace.md) per ulteriori dettagli sui pacchetti.

1. Aggiorna percorsi in `main.js` si trova in client-html/src/main/webapp/js, per modelli/viste aggiunti/aggiornati.

   Ad esempio, l&#39;aggiunta di un nuovo modello Sharequeue, ad esempio mySharequeue, cambia:

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/models/sharequeue',
   ```

   A

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/myModels/mySharequeue',
   ```

1. Aggiorna `registry-config.xml, located at client-html/src/main/webapp/js/resource_generator,` nel caso in cui venga modificato/aggiunto un alias in `main.js`.

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
