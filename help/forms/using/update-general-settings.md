---
title: Aggiornamento delle impostazioni generali
seo-title: Aggiornamento delle impostazioni generali
description: Aggiornare  impostazioni dell'app AEM Forms, ad esempio la schermata iniziale e le opzioni di richiamo e allegati
seo-description: Aggiornare  impostazioni dell'app AEM Forms, ad esempio la schermata iniziale e le opzioni di richiamo e allegati
uuid: 650d677e-2b3c-498e-9e46-fa659af934ca
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 7fdb9fab-6bae-49b8-86b6-66138a2a6cd3
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 1%

---


# Aggiornamento delle impostazioni generali{#updating-general-settings}

Le impostazioni generali dell&#39;app AEM Forms  consentono di specificare impostazioni quali il recupero di allegati, la modalità offline, la schermata di destinazione, la categoria predefinita e la frequenza di salvataggio automatico.

## Aggiornamento delle impostazioni Generali nell&#39;app {#working-with-the-form}

Quando si sincronizza l&#39;app con il server AEM Forms , tutti i moduli e le attività definite vengono scaricati sul dispositivo mobile.

La soluzione predefinita  app AEM Forms non scarica gli allegati associati a ciascun modulo quando l&#39;app viene sincronizzata.

Nella scheda Generale, modificare gli allegati di download, la modalità offline, la schermata di destinazione, il salvataggio automatico e le impostazioni di sincronizzazione. Puoi cambiare la [Home screen](../../forms/using/home-screen.md) dell&#39;app.

**Passate alla scheda Generale nella schermata Impostazioni**

1. Per passare alla schermata Impostazioni, toccate il pulsante Menu nell&#39;angolo superiore sinistro della schermata Home, quindi toccate **Impostazioni**.
1. Nella schermata Impostazioni, toccate la scheda Generale.

   ![Impostazioni generali nell&#39;app  AEM Forms](assets/gen-settings-1.png)

   Impostazioni generali, schermata

   >[!NOTE]
   >
   >Le opzioni possono essere visualizzate in modo diverso su diversi dispositivi mobili.

### Impostazioni generali {#general-settings}

Potete apportare le seguenti modifiche alle impostazioni dell&#39;app.

* **Recupera allegati** attività: Per specificare se scaricare o meno gli allegati associati quando ogni attività viene scaricata nell&#39;app.
* **Modalità** offline: Per abilitare o disabilitare il servizio offline per  app AEM Forms. Per ulteriori informazioni, vedere [Utilizzo della modalità offline](/help/forms/using/work-offline-mode.md).
* **Schermata** di destinazione: Per impostare la posizione iniziale (schermata[ ](../../forms/using/home-screen.md)iniziale) per l&#39;app.
Opzioni disponibili:

   * Forms
   * Attività
   * Preferiti

* **Categoria** predefinita: Consente di selezionare la categoria di moduli da visualizzare nella schermata iniziale. Quando si seleziona Tutto, è possibile visualizzare tutti i moduli nella schermata iniziale. Le categorie vengono popolate in base ai moduli caricati nell&#39;app. Forms è disponibile nell&#39;app in base alle impostazioni del modulo specificate nel server AEM Forms .

* **Frequenza** salvataggio automatico: Per impostare la frequenza con cui l&#39;app  [mobile salva i moduli ](../../forms/using/autosave-data-app.md) in modo datalocale.
* **Frequenza** sincronizzazione: Per impostare la frequenza con cui l&#39;app  [mobile viene ](../../forms/using/sync-app.md) sincronizzata con il server AEM Forms  in modalità online.
   **Cancella dati** locali: Cancellare il database, comprese le impostazioni e i dati locali per tutti gli utenti e l&#39;archiviazione dei file dal dispositivo.

>[!NOTE]
>
>La cancellazione della cache comporta l&#39;immediato disconnessione dall&#39;app.
>
>Tuttavia, vi verrà richiesto di confermare l&#39;operazione di cancellazione della cache.
