---
title: Schermata principale
seo-title: Schermata principale
description: Descrizione dei componenti dell’app AEM Forms, schermata iniziale
seo-description: Descrizione dei componenti dell’app AEM Forms, schermata iniziale
uuid: abc95e58-a685-42a9-82ab-4990155945d3
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: ba79479b-4159-4a39-95eb-2285e7ece9d4
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Schermata principale{#home-screen}

Quando effettuate l’accesso all’app AEM Forms, viene nuovamente visualizzata la schermata iniziale.

## Home page predefinita {#default-home-screen}

Per impostazione predefinita, nella schermata Home sono visualizzati tutti i moduli, inclusi i punti di avvio e le attività (se il server connesso è AEM Forms Workflow abilitato), insieme alle relative miniature. È possibile specificare le miniature nel server AEM Forms.

Nella figura riportata di seguito vengono annotate le chiamate ai componenti essenziali nella schermata iniziale predefinita.

![Schermata principale dell&#39;app Forms](assets/home-screen-1.png)

<!--Click to enlarge

![home-screen-1-1](assets/home-screen-1-1.png)-->

1. **Pulsante** menu: Toccate il pulsante **Menu** per passare a Attività, Moduli, In uscita e Impostazioni. Se l’app AEM Forms è connessa a un server AEM Forms JEE, è possibile visualizzare l’opzione Attività. L&#39;opzione Attività memorizza inoltre le bozze create dalle attività in un processo. Per i server AEM Forms OSGi, l&#39;opzione Attività è nascosta. In Output vengono memorizzati i moduli e le bozze salvati prima della sincronizzazione con il server. Tutti i moduli e le bozze salvati nella casella in uscita vengono caricati nel server AEM Forms quando l&#39;app viene [sincronizzata con il server](../../forms/using/sync-app.md). Per informazioni sulle impostazioni, consultate [Aggiornamento delle impostazioni](../../forms/using/update-general-settings.md)generali.
1. **Attività o modulo**: Toccare l&#39;attività o il modulo elencati con cui si desidera lavorare.
1. **Ellissi** orizzontale: Indica che sono disponibili azioni per il modulo. Toccando i puntini di sospensione vengono visualizzate le azioni e la descrizione fornite dall’autore. L&#39;opzione **Elimina bozza** e **Completa** è visibile quando si toccano i puntini di sospensione.
1. **Icona** Aggiorna: Toccate l&#39;icona di aggiornamento per sincronizzare l&#39;app con il server AEM Forms.

### Personalizzazione della schermata iniziale {#customizing-the-home-screen}

![Impostazioni generali](assets/gen-settings.png)

Potete modificare la schermata iniziale predefinita dell&#39;app sia dalle impostazioni **[](../../forms/using/update-general-settings.md)**generali dell&#39;app, sia dalla scheda **Preferenze**in HTML Workspace.

La modifica apportata alla schermata iniziale dell&#39;app ha effetto sulla schermata iniziale dell&#39;utente attualmente registrato o sul dispositivo mobile corrente.

Tuttavia, la modifica apportata in Area di lavoro HTML ha effetto su tutti gli utenti dell&#39;app AEM Forms che hanno eseguito l&#39;accesso al server AEM Forms.
