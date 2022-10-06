---
title: Aggiornamento delle impostazioni generali
seo-title: Updating general settings
description: Aggiorna le impostazioni dell’app AEM Forms, ad esempio la schermata iniziale e le opzioni dei punti iniziali di recupero e degli allegati
seo-description: Update AEM Forms app settings such as the Home screen and fetch Startpoints and attachments options
uuid: 650d677e-2b3c-498e-9e46-fa659af934ca
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 7fdb9fab-6bae-49b8-86b6-66138a2a6cd3
docset: aem65
exl-id: 3e74cda2-ba3e-4ee9-b7d0-76a804232199
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 1%

---

# Aggiornamento delle impostazioni generali{#updating-general-settings}

Le impostazioni generali dell’app AEM Forms consentono di specificare impostazioni quali il recupero degli allegati, la modalità offline, la schermata di destinazione, la categoria predefinita e la frequenza di salvataggio automatico.

## Aggiornamento delle impostazioni Generali nell’app {#working-with-the-form}

Quando sincronizzi l’app con il server AEM Forms, tutti i moduli e le attività definite vengono scaricati sul dispositivo mobile.

La soluzione pronta all’uso per l’app AEM Forms non scarica gli allegati associati a ciascun modulo quando l’app viene sincronizzata.

Nella scheda Generale modificare gli allegati da scaricare, la modalità offline, la schermata di destinazione, l’salvataggio automatico e le impostazioni di sincronizzazione. È possibile modificare le [Schermata principale](../../forms/using/home-screen.md) della tua app.

**Passa alla scheda Generale nella schermata Impostazioni**

1. Per passare alla schermata di impostazione, tocca il pulsante Menu nell’angolo in alto a sinistra della schermata iniziale, quindi tocca **Impostazioni**.
1. Nella schermata Impostazioni , tocca la scheda Generale .

   ![Impostazioni generali nell’app AEM Forms](assets/gen-settings-1.png)

   Schermata Impostazioni generali

   >[!NOTE]
   >
   >Le opzioni possono essere visualizzate in modo diverso su diversi dispositivi mobili.

### Impostazioni generali {#general-settings}

Puoi apportare le seguenti modifiche alle impostazioni dell’app.

* **Recupera allegati attività**: Per specificare se scaricare o meno gli allegati associati quando ogni attività viene scaricata nell&#39;app.
* **Modalità offline**: Per abilitare o disabilitare il servizio offline per l’app AEM Forms. Vedi [Utilizzo della modalità offline](/help/forms/using/work-offline-mode.md) per i dettagli.
* **Schermo di destinazione**: Per impostare la posizione iniziale ([Schermata principale](../../forms/using/home-screen.md)) per l’app.
Opzioni disponibili:

   * Forms
   * Attività
   * Preferiti

* **Categoria predefinita**: Consente di selezionare la categoria di moduli da visualizzare nella schermata iniziale. Quando si seleziona Tutto, è possibile visualizzare tutti i moduli nella schermata iniziale. Le categorie vengono compilate in base ai moduli caricati nell’app. Forms è disponibile nell’app in base alle impostazioni del modulo specificate nel server AEM Forms.

* **Frequenza di salvataggio automatico**: Per impostare la frequenza alla quale [i dati del modulo vengono salvati in app mobile](../../forms/using/autosave-data-app.md) locale.
* **Frequenza di sincronizzazione**: Per impostare la frequenza alla quale [app mobile sincronizzata](../../forms/using/sync-app.md) con il server AEM Forms in modalità online.
   **Cancella dati locali**: Cancellare il database, incluse le impostazioni e i dati locali per tutti gli utenti e l&#39;archiviazione dei file dal dispositivo.

>[!NOTE]
>
>Cancellando la cache, disconnetti immediatamente l’app.
>
>Viene tuttavia richiesto di confermare l’operazione di cancellazione della cache.
