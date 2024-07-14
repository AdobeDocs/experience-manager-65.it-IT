---
title: Aggiornamento delle impostazioni generali
description: Aggiorna le impostazioni dell’app AEM Forms, ad esempio la schermata iniziale, e recupera le opzioni punti iniziali e allegati
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: 3e74cda2-ba3e-4ee9-b7d0-76a804232199
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 1%

---

# Aggiornamento delle impostazioni generali{#updating-general-settings}

Le impostazioni generali dell’app AEM Forms consentono di specificare impostazioni quali recupero di allegati, modalità offline, schermata di destinazione, categoria predefinita e frequenza di salvataggio automatico.

## Aggiornamento delle impostazioni generali nell’app {#working-with-the-form}

Quando sincronizzi l’app con il server AEM Forms, tutti i moduli e le attività definite vengono scaricati sul tuo dispositivo mobile.

La soluzione AEM Forms preconfigurata per l’app non scarica gli allegati associati a ciascun modulo quando l’app viene sincronizzata.

Nella scheda Generale, modifica le impostazioni di download allegati, modalità offline, schermata di destinazione, salvataggio automatico e sincronizzazione. Puoi modificare la [schermata iniziale](../../forms/using/home-screen.md) dell&#39;app.

**Passa alla scheda Generale nella schermata Impostazioni**

1. Per passare alla schermata Impostazioni, selezionare il pulsante Menu nell&#39;angolo superiore sinistro della schermata iniziale, quindi selezionare **Impostazioni**.
1. Nella schermata Settings, selezionare la scheda General.

   ![Impostazioni generali nell&#39;app AEM Forms](assets/gen-settings-1.png)

   Schermata Impostazioni generali

   >[!NOTE]
   >
   >Le opzioni possono essere visualizzate in modo diverso su dispositivi mobili diversi.

### Impostazioni generali {#general-settings}

Puoi apportare le seguenti modifiche alle impostazioni dell’app.

* **Recupera allegati attività**: per specificare se scaricare o meno gli allegati associati quando ogni attività viene scaricata nell&#39;app.
* **Modalità offline**: per abilitare o disabilitare il servizio offline per l&#39;app AEM Forms. Per ulteriori dettagli, vedere [Utilizzo della modalità offline](/help/forms/using/work-offline-mode.md).
* **Schermata di destinazione**: per impostare la posizione iniziale ([Schermata iniziale](../../forms/using/home-screen.md)) per l&#39;app.
Opzioni disponibili:

   * Moduli
   * Attività
   * Preferiti

* **Categoria predefinita**: consente di selezionare la categoria di moduli da visualizzare nella schermata iniziale. Quando si seleziona Tutto, è possibile visualizzare tutti i moduli nella schermata iniziale. Le categorie vengono compilate in base ai moduli caricati nell’app. I Forms sono disponibili nell’app in base alle impostazioni del modulo specificate nel server AEM Forms.

* **Frequenza salvataggio automatico**: per impostare la frequenza con cui l&#39;app [mobile salva localmente i dati del modulo](../../forms/using/autosave-data-app.md).
* **Frequenza di sincronizzazione**: per impostare la frequenza di sincronizzazione dell&#39;app [mobile](../../forms/using/sync-app.md) con il server AEM Forms in modalità online.
  **Cancella dati locali**: cancella il database, incluse le impostazioni e i dati locali per tutti gli utenti e l&#39;archiviazione dei file dal dispositivo.

>[!NOTE]
>
>Se si cancella la cache, si esce immediatamente dall’app.
>
>Tuttavia, verrà richiesto di confermare l&#39;operazione di cancellazione della cache.
