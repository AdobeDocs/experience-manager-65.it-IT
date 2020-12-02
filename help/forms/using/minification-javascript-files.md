---
title: Riduzione dei file JavaScript
seo-title: Riduzione dei file JavaScript
description: Istruzioni per generare codice ridotto dopo  personalizzazioni dell’area di lavoro di AEM Forms per ottimizzare i file JS per il Web.
seo-description: Istruzioni per generare codice ridotto dopo  personalizzazioni dell’area di lavoro di AEM Forms per ottimizzare i file JS per il Web.
uuid: ad91e380-a988-4740-9534-e09657e0322a
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: c88a3013-5da2-4b09-9f29-ac1fb00822ec
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---


# Riduzione dei file JavaScript {#minification-of-the-javascript-files}

La riduzione rimuove dal codice sorgente i caratteri ridondanti, ad esempio lo spazio vuoto, la nuova riga e i commenti. Questo migliora le prestazioni riducendo le dimensioni del codice. Anche se la riduzione non influisce sulla funzionalità, riduce la leggibilità del codice.

Per generare codice ridotto per le modifiche semantiche, effettuate le seguenti operazioni.

1. Copiare `client-html/src/main/webapp/js` da src-package nel file system.

   >[!NOTE]
   >
   >Per ulteriori informazioni sui pacchetti, vedere [Introduzione alla personalizzazione  area di lavoro AEM Forms](/help/forms/using/introduction-customizing-html-workspace.md).

1. Aggiornate i percorsi in `main.js` ubicati in client-html/src/main/webapp/js, per i modelli/visualizzazioni aggiunti/aggiornati.

   Ad esempio, l&#39;aggiunta di un nuovo modello Sharequeue, ad esempio mySharequeue, modifica:

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/models/sharequeue',
   ```

   A

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/myModels/mySharequeue',
   ```

1. Aggiornare `registry-config.xml, located at client-html/src/main/webapp/js/resource_generator,` in caso di modifica/aggiunta di alias in `main.js`.

   Ad esempio, l&#39;aggiunta di un nuovo modello Sharequeue, ad esempio mySharequeue, modifica:

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

1. In client-html/src/main/webapp/js/minifier, eseguite il comando:

   ```shell
   mvn clean install
   ```

   Viene generata una cartella minified-files, in client-html/src/main/webapp/js con minified main.js e register.js.

>[!NOTE]
>
>La riduzione funziona solo su JVM a 64 bit.

>[!NOTE]
>
>Se si riduce il numero di utenti, l&#39;aggiornamento viene influenzato.
