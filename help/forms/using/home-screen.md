---
title: Schermata iniziale
description: Descrizione dei componenti della schermata iniziale dell’app AEM Forms
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: 6c6fb516-1b11-4da4-b638-4388a070e397
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Schermata iniziale{#home-screen}

Quando accedi all’app AEM Forms, vieni reindirizzato alla schermata iniziale.

## Schermata iniziale predefinita {#default-home-screen}

Per impostazione predefinita, nella schermata iniziale vengono visualizzati tutti i moduli, compresi i punti d&#39;inizio e le attività (se il server connesso è abilitato per AEM Forms Workflow), insieme alle miniature associate. Puoi specificare le miniature in AEM Forms Server.

Nella figura seguente sono riportate le chiamate ai componenti essenziali nella schermata Home predefinita.

![Home schermata dell&#39;app Forms](assets/home-screen-1.png)

<!--Click to enlarge

![home-screen-1-1](assets/home-screen-1-1.png)-->

1. **Pulsante Menu**: selezionare il pulsante **Menu** per passare ad Attività, Forms, Posta in uscita e Impostazioni. Se la tua app AEM Forms è connessa a un server AEM Forms JEE, puoi visualizzare l’opzione Attività. L&#39;opzione Attività consente inoltre di memorizzare in un processo le bozze create dalle attività. Per i server AEM Forms OSGi, l’opzione Attività è nascosta. In Posta in uscita vengono memorizzati i moduli e le bozze salvati prima della sincronizzazione con il server. Tutti i moduli e le bozze salvati nella cartella Posta in uscita vengono caricati sul server AEM Forms quando l&#39;app è [sincronizzata con il server](../../forms/using/sync-app.md). Per informazioni sulle impostazioni, vedere [Aggiorna impostazioni generali](../../forms/using/update-general-settings.md).
1. **Attività o Modulo**: selezionare l&#39;attività o il modulo elencato che si desidera utilizzare.
1. **Puntini di sospensione orizzontali**: indica che sono disponibili azioni per il modulo. Toccando i puntini di sospensione vengono visualizzate le azioni e la descrizione fornite dall’autore. L&#39;opzione **Elimina bozza** e **Completa** è visibile quando si selezionano i puntini di sospensione.
1. **Icona di aggiornamento**: seleziona l&#39;icona di aggiornamento per sincronizzare l&#39;app con AEM Forms Server.

### Personalizzazione della schermata iniziale {#customizing-the-home-screen}

![Impostazioni generali](assets/gen-settings.png)

Puoi modificare la schermata iniziale predefinita dell&#39;app dalle **[Impostazioni generali](../../forms/using/update-general-settings.md)** dell&#39;app o dalla scheda **Preferenza** in HTML Workspace.

La modifica apportata all’impostazione della schermata iniziale nell’app influisce sulla schermata iniziale dell’utente attualmente connesso o dell’utente sul dispositivo mobile corrente.

Tuttavia, la modifica apportata in HTML Workspace ha effetto su tutti gli utenti dell’app AEM Forms che hanno effettuato l’accesso ad AEM Forms Server.
