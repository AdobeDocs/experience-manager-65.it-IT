---
title: Modifica della combinazione di colori dell’interfaccia
seo-title: Modifica della combinazione di colori dell’interfaccia
description: Come modificare selettivamente lo schema di colori delle porzioni dell'interfaccia utente dell'area di lavoro AEM Forms.
seo-description: Come modificare selettivamente lo schema di colori delle porzioni dell'interfaccia utente dell'area di lavoro AEM Forms.
uuid: 32c32f7a-8271-4d2c-8a1f-ad5ab3c90b83
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 18dab82a-badf-4c32-83a2-cd5cb04cae89
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Modifica della combinazione di colori dell’interfaccia {#changing-the-color-scheme-of-the-interface}

È possibile modificare lo schema di colori delle porzioni dell&#39;interfaccia utente dell&#39;area di lavoro AEM Forms in base alle proprie esigenze. Di seguito sono riportati alcuni esempi di personalizzazioni rappresentative dello schema di colori. Oltre ai passaggi descritti in questo articolo, consulta Procedura [generica per la personalizzazione](/help/forms/using/generic-steps-html-workspace-customization.md)dell’area di lavoro AEM Forms.

## Barra di navigazione superiore {#top-navigation-bar}

### Utilizzo dell&#39;immagine di sfondo {#using-background-image}

Per aggiornare la barra di navigazione nella parte superiore dell&#39;area di lavoro Moduli AEM.

1. Create un&#39;immagine di sfondo per aggiornare il colore. Denominate il file come newBackground.jpg.
1. Caricate il file di immagine di sfondo nella cartella /apps/ws/images utilizzando un client WebDAV.

   >[!NOTE]
   >
   >Per ulteriori informazioni sull&#39;accesso WebDAV, vedere [https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://docs.adobe.com/docs/en/crx/current/how_to/webdav_access.html).

1. Fate riferimento alla nuova immagine di sfondo in /apps/ws/css/newStyle.css aggiungendo il seguente stile.

   ```css
   #header {
       background:#292929 url(../images/newBackground.jpg) repeat-x;
   }
   ```

### Utilizzo della proprietà colore nei CSS {#using-color-property-in-css}

1. Aggiungi il seguente stile in newStyle.css in /apps/ws/css

   ```css
   #header {
   background : none;
   background-color: gray;
   }
   ```

## Componente categoria {#category-component}

Il componente Categoria visualizza le varie categorie di attività nel pannello a sinistra. Per modificarne il colore, definite il colore di sfondo nell’ `.category` elemento del file CSS.

## Componente attività {#task-component}

Le attività vengono visualizzate nel pannello centrale denominato Componente TaskList. Per modificarne il colore, modificare lo stile associato al selettore .task nel foglio di stile.
