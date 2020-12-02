---
title: Aggiunta di allegati
seo-title: Aggiunta di allegati
description: Aggiungere fotografie e note di script come annotazioni all'attività nell'app  AEM Forms
seo-description: Aggiungere fotografie e note di script come annotazioni all'attività nell'app  AEM Forms
uuid: 3d2738b4-fd43-44ec-8eaf-a2ad4b7e5af5
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: d5976ed2-4482-495c-bf77-6d192379cfef
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 0%

---


# Aggiunta di allegati{#adding-attachments}

## Aggiunta di allegati ai moduli sincronizzati con  server AEM Forms Workflow ( AEM Forms su JEE) {#adding-annotations}

&#39;app AEM Forms consente di allegare immagini, note con script e note di testo al modulo sincronizzate con  server AEM Forms JEE. Se il modulo viene caricato da un server AEM Forms Workflow , gli allegati vengono aggiunti al modulo. È possibile toccare il pulsante allegato ![allegati-app](assets/attachments-app.png) per visualizzare tutti gli allegati di un modulo insieme. La notifica rossa specifica il numero di allegati nel modulo. Se nel modulo non sono presenti allegati, non è possibile visualizzare il pulsante rosso delle notifiche. Se non sono presenti allegati nel modulo, toccando il pulsante degli allegati ![attaccare](assets/attch.png), è possibile allegare foto o script.

Le opzioni disponibili sono:

* **Galleria**: Consente di aggiungere un&#39;immagine dalle immagini salvate sul dispositivo.

* **Telecamera**: Consente di scattare una foto e aggiungerla al modulo.

* **Note**: Consente di aggiungere uno script o una nota di testo. Utilizzare ![scarabocchio](assets/scribble.png) per aggiungere uno scarabocchio e ![tastiera](assets/keyboard.png) per aggiungere una nota di testo.

>[!NOTE]
>
>Gli allegati aggiunti da un utente sono visibili agli altri utenti  app AEM Forms. Altri utenti non possono eliminare gli allegati aggiunti da un utente.


### Schermata Allegati {#the-attachments-screen}

Per visualizzare tutti gli allegati in una posizione, toccare ![attachments-app](assets/attachments-app.png). È possibile aggiungere, rinominare ed eliminare gli allegati.

![Tutti gli allegati in una posizione](assets/attachments-screen.png)

È possibile utilizzare il pulsante **+** nella schermata Allegati per allegare un&#39;altra immagine, un altro script o un altro testo.

### Aggiunta di una foto {#adding-a-photograph}

È possibile utilizzare la fotocamera del dispositivo mobile o le immagini salvate nel dispositivo per allegare un&#39;immagine al modulo.

1. Toccate il pulsante di attacco ![attaccare](assets/attch.png) nella parte inferiore della finestra.
1. Toccate **Gallery** o **Camera** nella finestra a comparsa che viene visualizzata.
1. In base all’opzione selezionata, effettuate le seguenti operazioni:

   1. Se si seleziona **Fotocamera**.

      Scatta una fotografia. Quindi toccate il pulsante **Use** ![use-pic](assets/use-pic.png).

      Oppure, toccate il pulsante **Riproduci** ![Riproduci](assets/retake.png) per riprendere nuovamente la foto.

   1. Se si seleziona **Gallery**.

      Viene visualizzato il browser delle immagini del dispositivo. Nel browser delle immagini del dispositivo, toccate l&#39;immagine da allegare.

### Aggiunta di una nota {#adding-a-note}

L&#39;opzione **Note** consente di aggiungere script a mano libera e allegati di testo nel modulo.

1. Toccate il pulsante di attacco ![attaccare](assets/attch.png) nella parte inferiore della finestra.
1. Toccate **Note** nella finestra a comparsa che viene visualizzata.
1. Nell’interfaccia utente Note che viene avviata, acquisite uno script a mano libera.

   ![Interfaccia scarabocchio](assets/scribble-ui.png)

   A mano

   Nell&#39;interfaccia Scribble è possibile utilizzare le seguenti opzioni:

   * **Cancella**: Cancella lo schermo.
   * **Pulsante** Fine: Associa lo script corrente.
   * **Pulsante** Annulla: Elimina lo script corrente ed esce dall&#39;interfaccia utente di Scribble.
   * ![tastiera](assets/keyboard.png): Cancella lo script e consente di aggiungere una nota di testo.

   ![Tastiera in  script app AEM Forms](assets/keyboard-inapp.png)

## Allegati in moduli sincronizzati con i server AEM Forms  senza  flusso di lavoro AEM Forms ( AEM Forms su OSGi) {#attachments-in-forms-synced-with-the-aem-forms-servers-without-aem-forms-workflow-aem-forms-on-osgi}

Gli allegati per i moduli mobili sincronizzati con  server AEM Forms OSGi funzionano in modo simile ai server AEM Forms JEE .

Gli allegati a livello di modulo non sono supportati per i moduli adattivi caricati nell&#39;app da un server AEM Forms OSGi . Per allegare immagini o note di testo, è necessario abilitare gli allegati a livello di campo nel modulo al momento della creazione. Trascinare il componente Allegato dal Browser componenti sul campo.

Nel caso di moduli adattivi, è possibile visualizzare i file allegati nel documento record (DoR). Vedere [Genera documento di registrazione per moduli adattivi non XFA](../../forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md).
