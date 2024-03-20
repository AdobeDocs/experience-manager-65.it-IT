---
title: Aggiunta di allegati
description: Aggiungi fotografie e note a mano come annotazioni per l’attività nell’app AEM Forms
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: 82282e2d-63a1-47e9-b2ec-f50a4bd32bd3
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 0%

---

# Aggiunta di allegati{#adding-attachments}

## Aggiunta di allegati nei moduli sincronizzati con il server flusso di lavoro di AEM Forms (AEM Forms su JEE) {#adding-annotations}

L’app AEM Forms consente di allegare immagini, note scarabocchiate e note di testo al modulo sincronizzato con il server AEM Forms JEE. Se il modulo viene caricato da un server di AEM Forms Workflow, gli allegati vengono aggiunti al modulo. È possibile selezionare il pulsante allegato ![allegati-app](assets/attachments-app.png) per visualizzare tutti gli allegati di un modulo insieme. La notifica rossa specifica il numero di allegati nel modulo. Se nel modulo non sono presenti allegati, il pulsante di notifica rosso non è visibile. Se nel modulo non sono presenti allegati, quando si seleziona il pulsante Allegati ![attaccare](assets/attch.png), vengono visualizzate le opzioni per allegare foto o scarabocchi.

Le opzioni disponibili sono:

* **Galleria**: consente di aggiungere un’immagine dalle immagini salvate sul dispositivo.

* **Fotocamera**: consente di scattare una foto e aggiungerla al modulo.

* **Note**: consente di aggiungere uno scarabocchio o una nota di testo. Utilizzare ![scarabocchio](assets/scribble.png) per aggiungere uno scarabocchio e ![tastiera](assets/keyboard.png) per aggiungere una nota di testo.

>[!NOTE]
>
>Gli allegati aggiunti da un utente sono visibili agli altri utenti dell’app AEM Forms. Gli altri utenti non possono eliminare gli allegati aggiunti da un utente.
>

### Schermata Allegato {#the-attachments-screen}

Per visualizzare tutti gli allegati in una posizione, selezionare ![allegati-app](assets/attachments-app.png). È possibile aggiungere, rinominare ed eliminare allegati qui.

![Tutti gli allegati in un luogo](assets/attachments-screen.png)

È possibile utilizzare **+** nella schermata Allegati per allegare un&#39;altra immagine, scarabocchio o testo.

### Aggiunta di una fotografia {#adding-a-photograph}

È possibile utilizzare la fotocamera del dispositivo mobile o le immagini salvate nel dispositivo per allegare un&#39;immagine nel modulo.

1. Seleziona il pulsante allegato ![attaccare](assets/attch.png) nella parte inferiore della finestra.
1. Seleziona **Galleria** o **Fotocamera** nel pop-up che viene visualizzato.
1. In base all’opzione selezionata, effettua le seguenti operazioni:

   1. Se si seleziona **Fotocamera**.

      Fai una fotografia. Quindi seleziona la **Utilizzare** ![use-pic](assets/use-pic.png) pulsante.

      Oppure seleziona la **Riprendi** ![ripresa](assets/retake.png) per riprendere la fotografia.

   1. Se si seleziona **Galleria**.

      Viene visualizzato il browser immagini del dispositivo. Nel browser immagini del dispositivo, selezionare l&#39;immagine che si desidera collegare.

### Aggiunta di una nota {#adding-a-note}

Il **Note** consente di aggiungere scarabocchi a mano libera e allegati di testo al modulo.

1. Seleziona il pulsante allegato ![attaccare](assets/attch.png) nella parte inferiore della finestra.
1. Seleziona **Note** nel pop-up che viene visualizzato.
1. Nell’interfaccia utente Notes avviata, acquisisci uno scarabocchio a mano libera.

   ![Interfaccia a mano](assets/scribble-ui.png)

   A mano

   Nell’interfaccia a mano puoi utilizzare le seguenti opzioni:

   * **Cancella**: cancella la schermata.
   * **Pulsante Fine**: collega lo scarabocchio corrente.
   * **Pulsante Annulla**: ignora lo scarabocchio corrente e chiude l’interfaccia utente di Scribble.
   * ![tastiera](assets/keyboard.png): cancella lo scarabocchio e consente di aggiungere una nota di testo.

   ![Tastiera nello scarabocchio dell’app AEM Forms](assets/keyboard-inapp.png)

## Allegati nei moduli sincronizzati con i server AEM Forms senza flusso di lavoro AEM Forms (AEM Forms su OSGi) {#attachments-in-forms-synced-with-the-aem-forms-servers-without-aem-forms-workflow-aem-forms-on-osgi}

Gli allegati per i moduli mobili sincronizzati con i server AEM Forms OSGi funzionano in modo simile ai server AEM Forms JEE.

Gli allegati a livello di modulo non sono supportati per i moduli adattivi caricati nell’app da un server OSGi di AEM Forms. Per allegare immagini o note di testo, attivare gli allegati a livello di campo nel modulo quando lo si crea. Trascina il componente allegato dal browser Componenti sul campo.

Se sono presenti moduli adattivi, puoi visualizzare i file allegati nel documento record (DoR). Vedi, [Genera documento di record per moduli adattivi non XFA](../../forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md).
