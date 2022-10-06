---
title: Aggiunta di allegati
seo-title: Adding attachments
description: Aggiungi fotografie e note di scarabocchio come annotazioni all’attività nell’app AEM Forms
seo-description: Add photographs and scribble notes as annotations to your task in the AEM Forms app
uuid: 3d2738b4-fd43-44ec-8eaf-a2ad4b7e5af5
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: d5976ed2-4482-495c-bf77-6d192379cfef
docset: aem65
exl-id: 82282e2d-63a1-47e9-b2ec-f50a4bd32bd3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 0%

---

# Aggiunta di allegati{#adding-attachments}

## Aggiunta di allegati ai moduli sincronizzati con il server AEM Forms Workflow (AEM Forms su JEE) {#adding-annotations}

L’app AEM Forms ti consente di allegare immagini, note con script e note di testo al modulo sincronizzato con il server JEE di AEM Forms. Se il modulo viene caricato da un server AEM Forms Workflow, gli allegati vengono aggiunti al modulo. Tocca il pulsante allegato ![allegato-app](assets/attachments-app.png) per visualizzare tutti gli allegati di un modulo. La notifica rossa specifica il numero di allegati nel modulo. Se nel modulo non sono presenti allegati, non è possibile visualizzare il pulsante di notifica rosso. Se non sono presenti allegati nel modulo, quando si tocca il pulsante allegati ![attaccare](assets/attch.png), è possibile allegare foto o scarabocchi.

Le opzioni disponibili sono:

* **Galleria**: Consente di aggiungere un&#39;immagine dalle immagini salvate sul dispositivo.

* **Telecamera**: Consente di scattare una foto e aggiungerla al modulo.

* **Note**: Consente di aggiungere uno scarabocchio o una nota di testo. Utilizzo ![scarabocchio](assets/scribble.png) per aggiungere uno scarabocchio, e ![tastiera](assets/keyboard.png) per aggiungere una nota di testo.

>[!NOTE]
>
>Gli allegati aggiunti da un utente sono visibili ad altri utenti dell’app AEM Forms. Altri utenti non possono eliminare gli allegati aggiunti da un utente.

### Schermata Allegati {#the-attachments-screen}

Per visualizzare tutti gli allegati in una posizione, tocca ![allegato-app](assets/attachments-app.png). Qui è possibile aggiungere, rinominare ed eliminare gli allegati.

![Tutti gli allegati in un luogo](assets/attachments-screen.png)

È possibile utilizzare **+** nella schermata Allegati per allegare un&#39;altra immagine, un altro scarabocchio o un altro testo.

### Aggiunta di una fotografia {#adding-a-photograph}

È possibile utilizzare la fotocamera del dispositivo mobile o le immagini salvate nel dispositivo per allegare un&#39;immagine nel modulo.

1. Toccare il pulsante allegato ![attaccare](assets/attch.png) in fondo alla finestra.
1. Tocca **Galleria** o **Telecamera** nella finestra a comparsa visualizzata.
1. In base all’opzione selezionata, esegui le seguenti operazioni:

   1. Se si seleziona **Telecamera**.

      Scatta una fotografia. Quindi tocca **Utilizzo** ![use-pic](assets/use-pic.png) pulsante .

      Oppure tocca **Ritorno** ![nuovo](assets/retake.png) per riprendere la fotografia.

   1. Se si seleziona **Galleria**.

      Viene visualizzato il browser delle immagini del dispositivo. Nel browser delle immagini del dispositivo, toccare l&#39;immagine che si desidera allegare.

### Aggiunta di una nota {#adding-a-note}

La **Note** consente di aggiungere nel modulo script a mano libera e allegati di testo.

1. Toccare il pulsante allegato ![attaccare](assets/attch.png) in fondo alla finestra.
1. Tocca **Note** nella finestra a comparsa visualizzata.
1. Nell’interfaccia utente Note che viene avviata, acquisisci uno scarabocchio a mano libera.

   ![Interfaccia scribble](assets/scribble-ui.png)

   A mano

   Nell’interfaccia Scribble è possibile utilizzare le seguenti opzioni:

   * **Cancella**: Cancella lo schermo.
   * **Pulsante Fine**: Allega lo scarabocchio corrente.
   * **Pulsante Annulla**: Ignora lo scarabocchio corrente ed esce dall&#39;interfaccia utente Scribble.
   * ![tastiera](assets/keyboard.png): Cancella lo scarabocchio e consente di aggiungere una nota di testo.

   ![Tastiera nello scarabocchio dell’app AEM Forms](assets/keyboard-inapp.png)

## Allegati nei moduli sincronizzati con i server AEM Forms senza flusso di lavoro AEM Forms (AEM Forms su OSGi) {#attachments-in-forms-synced-with-the-aem-forms-servers-without-aem-forms-workflow-aem-forms-on-osgi}

Gli allegati per i moduli mobili sincronizzati con i server OSGi di AEM Forms funzionano in modo simile ai server JEE di AEM Forms.

Gli allegati a livello di modulo non sono supportati per i moduli adattivi caricati nell’app da un server OSGi di AEM Forms. Per allegare immagini o note di testo, abilitare gli allegati a livello di campo nel modulo durante la creazione. Trascina il componente File allegato dal browser Componenti sul campo .

Nel caso di moduli adattivi, è possibile visualizzare i file allegati nel documento di record (DoR). Vedi [Genera documento di record per moduli adattivi non XFA](../../forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md).
