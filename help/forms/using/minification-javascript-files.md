---
title: Riduzione dei file JavaScript
seo-title: Riduzione dei file JavaScript
description: Istruzioni per generare codice ridotto dopo le personalizzazioni dell'area di lavoro AEM Forms per ottimizzare i file JS per il Web.
seo-description: Istruzioni per generare codice ridotto dopo le personalizzazioni dell'area di lavoro AEM Forms per ottimizzare i file JS per il Web.
uuid: ad91e380-a988-4740-9534-e09657e0322a
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: c88a3013-5da2-4b09-9f29-ac1fb00822ec
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Riduzione dei file JavaScript {#minification-of-the-javascript-files}

La riduzione rimuove dal codice sorgente i caratteri ridondanti, come lo spazio vuoto, la nuova riga e i commenti. Questo migliora le prestazioni riducendo le dimensioni del codice. Anche se la riduzione non influisce sulla funzionalità, riduce la leggibilità del codice.

Per generare codice ridotto per le modifiche semantiche, effettuate le seguenti operazioni.

1. Copiare `client-html/src/main/webapp/js` da src-package sul file system.

   >[!NOTE]
   >
   >Per ulteriori informazioni sui pacchetti, consultate [Introduzione alla personalizzazione dell&#39;area di lavoro](/help/forms/using/introduction-customizing-html-workspace.md) Moduli AEM.

1. Aggiornate i percorsi in `main.js` Client-html/src/main/webapp/js per modelli/visualizzazioni aggiunti/aggiornati.

   Ad esempio, l&#39;aggiunta di un nuovo modello Sharequeue, ad esempio mySharequeue, modifica:

   ```
   sharequeuemodel : pathprefix + 'runtime/models/sharequeue',
   
   To
   
   sharequeuemodel : pathprefix + 'runtime/myModels/mySharequeue',
   ```

1. Aggiorna `registry-config.xml, located at client-html/src/main/webapp/js/resource_generator,` in caso di modifica/aggiunta di alias in `main.js`.

   Ad esempio, l&#39;aggiunta di un nuovo modello Sharequeue, ad esempio mySharequeue, modifica:

   ```xml
   <sharequeue
               name="sharequeue"
               path="runtime/models/sharequeue.js"
               service="service"/>
   
   To
   
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

**[Contattare il supporto](https://www.adobe.com/account/sign-in.supportportal.html)**
