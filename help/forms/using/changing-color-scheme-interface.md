---
title: Modifica della combinazione di colori dell’interfaccia
seo-title: Changing the color scheme of the interface
description: Come modificare selettivamente la combinazione di colori delle parti dell’interfaccia utente di AEM Forms Workspace.
seo-description: How to modify the color scheme of AEM Forms workspace user interface portions selectively.
uuid: 32c32f7a-8271-4d2c-8a1f-ad5ab3c90b83
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 18dab82a-badf-4c32-83a2-cd5cb04cae89
exl-id: e0a261a2-518b-4984-a5b5-24f0b9222e24
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# Modifica della combinazione di colori dell’interfaccia {#changing-the-color-scheme-of-the-interface}

Puoi modificare la combinazione di colori delle porzioni dell’interfaccia utente di AEM Forms Workspace in base alle tue esigenze. Di seguito sono riportati alcuni esempi di personalizzazioni rappresentative delle combinazioni di colori. Oltre ai passaggi descritti in questo articolo, consulta [Passaggi generici per la personalizzazione dell’area di lavoro AEM Forms](/help/forms/using/generic-steps-html-workspace-customization.md).

## Barra di navigazione superiore {#top-navigation-bar}

### Utilizzo dell&#39;immagine di sfondo {#using-background-image}

Per aggiornare la barra di navigazione nella parte superiore dell’area di lavoro di AEM Forms.

1. Crea un&#39;immagine di sfondo per aggiornare il colore. Denomina il file come newBackground.jpg.
1. Carica il file di immagine di sfondo nella cartella /apps/ws/images utilizzando un client WebDAV.

   >[!NOTE]
   >
   >Per ulteriori informazioni sull&#39;accesso a WebDAV, vedi [https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://docs.adobe.com/docs/en/crx/current/how_to/webdav_access.html).

1. Fai riferimento alla nuova immagine di sfondo in /apps/ws/css/newStyle.css aggiungendo il seguente stile.

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

Il componente Categoria visualizza le varie categorie delle attività nel pannello a sinistra. Per modificarne il colore, definisci il colore di sfondo in `.category` elemento del file CSS.

## Componente attività {#task-component}

Le attività vengono visualizzate nel pannello centrale denominato Componente TaskList. Per modificarne il colore, modificare lo stile associato al selettore .task nel foglio di stile.
