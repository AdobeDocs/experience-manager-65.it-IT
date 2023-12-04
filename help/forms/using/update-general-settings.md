---
title: Aggiornamento delle impostazioni generali
seo-title: Updating general settings
description: Aggiorna le impostazioni dell’app AEM Forms, ad esempio la schermata iniziale, e recupera le opzioni punti iniziali e allegati
seo-description: Update AEM Forms app settings such as the Home screen and fetch Startpoints and attachments options
uuid: 650d677e-2b3c-498e-9e46-fa659af934ca
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 7fdb9fab-6bae-49b8-86b6-66138a2a6cd3
docset: aem65
exl-id: 3e74cda2-ba3e-4ee9-b7d0-76a804232199
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 1%

---

# Aggiornamento delle impostazioni generali{#updating-general-settings}

Le impostazioni generali dell’app AEM Forms consentono di specificare impostazioni quali recupero di allegati, modalità offline, schermata di destinazione, categoria predefinita e frequenza di salvataggio automatico.

## Aggiornamento delle impostazioni generali nell’app {#working-with-the-form}

Quando sincronizzi l’app con il server AEM Forms, tutti i moduli e le attività definite vengono scaricati sul tuo dispositivo mobile.

La soluzione AEM Forms preconfigurata per l’app non scarica gli allegati associati a ciascun modulo quando l’app viene sincronizzata.

Nella scheda Generale, modifica le impostazioni di download allegati, modalità offline, schermata di destinazione, salvataggio automatico e sincronizzazione. È possibile modificare il [Schermata iniziale](../../forms/using/home-screen.md) della tua app.

**Passa alla scheda Generale nella schermata Impostazioni.**

1. Per passare alla schermata Setting (Impostazioni), selezionare il pulsante Menu nell&#39;angolo superiore sinistro della schermata Home, quindi Select (Seleziona) **Impostazioni**.
1. Nella schermata Settings, selezionare la scheda General.

   ![Impostazioni generali nell’app AEM Forms](assets/gen-settings-1.png)

   Schermata Impostazioni generali

   >[!NOTE]
   >
   >Le opzioni possono essere visualizzate in modo diverso su dispositivi mobili diversi.

### Impostazioni generali {#general-settings}

Puoi apportare le seguenti modifiche alle impostazioni dell’app.

* **Recupera allegati attività**: per specificare se scaricare o meno gli allegati associati quando ogni attività viene scaricata nell’app.
* **Modalità offline**: per abilitare o disabilitare il servizio offline per l’app AEM Forms. Consulta [Utilizzo della modalità offline](/help/forms/using/work-offline-mode.md) per i dettagli.
* **Schermata di destinazione**: per impostare la posizione iniziale ([Schermata iniziale](../../forms/using/home-screen.md)) per l&#39;app.
Opzioni disponibili:

   * Forms
   * Attività
   * Preferiti

* **Categoria predefinita**: consente di selezionare la categoria di moduli da visualizzare nella schermata iniziale. Quando si seleziona Tutto, è possibile visualizzare tutti i moduli nella schermata iniziale. Le categorie vengono compilate in base ai moduli caricati nell’app. I Forms sono disponibili nell’app in base alle impostazioni del modulo specificate nel server AEM Forms.

* **Frequenza salvataggio automatico**: per impostare la frequenza con cui [l&#39;app mobile salva i dati del modulo](../../forms/using/autosave-data-app.md) localmente.
* **Frequenza di sincronizzazione**: per impostare la frequenza con cui [l&#39;app mobile è sincronizzata](../../forms/using/sync-app.md) con il server AEM Forms in modalità online.
  **Cancella dati locali**: cancella il database, incluse le impostazioni e i dati locali per tutti gli utenti e l’archiviazione dei file dal dispositivo.

>[!NOTE]
>
>Se si cancella la cache, si esce immediatamente dall’app.
>
>Tuttavia, verrà richiesto di confermare l&#39;operazione di cancellazione della cache.
