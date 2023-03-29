---
title: Guida rapida alla creazione di un headless di configurazione
description: Crea una configurazione come primo passaggio per iniziare a utilizzare headless in AEM 6.5.
exl-id: f1df97a1-164f-4ed4-bb63-34caf35ae27c
source-git-commit: 7355c149500f9e5044c9ff78af208d36ee681f56
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 69%

---

# Guida rapida alla creazione di un headless di configurazione {#creating-configuration}

Come primo passo per iniziare a utilizzare headless in AEM 6.5, devi creare una configurazione.

## Cos&#39;è una configurazione? {#what-is-a-configuration}

Il browser di configurazioni fornisce un’API di configurazione generica, una struttura del contenuto e un meccanismo di risoluzione per le configurazioni in AEM.

Nel contesto della gestione dei contenuti headless in AEM, considera una configurazione come un’area di lavoro all’interno di AEM dove puoi creare modelli di contenuto, che definiscono la struttura dei contenuti e dei frammenti di contenuto futuri. Puoi avere più configurazioni per separare questi modelli.

>[!NOTE]
>
>Se hai familiarità con i [modelli di pagina in un’implementazione completa di AEM,](/help/sites-authoring/templates.md) l’utilizzo delle configurazioni per la gestione dei modelli di contenuto è simile.

## Come creare una configurazione {#how-to-create-a-configuration}

Un amministratore deve creare una configurazione solo una volta oppure, molto raramente, se è necessaria una nuova area di lavoro per organizzare i modelli di contenuto. Ai fini di questa guida introduttiva, è sufficiente creare una sola configurazione.

1. Accedi a AEM e dal menu principale seleziona **Strumenti -> Generale -> Browser di configurazione**.
1. Fornisci un **Titolo** per la configurazione.
   * Un nome viene generato automaticamente in base al titolo e regolato in base a [AEM convenzioni di denominazione.](/help/sites-developing/naming-conventions.md). Diventerà il nome del nodo nel repository.
1. Seleziona le seguenti opzioni:
   * **Modelli per frammenti di contenuto**
   * **Query GraphQL persistenti**

   ![Crea configurazione](assets/create-configuration.png)

1. Tocca o fai clic su **Crea**.

Se necessario, puoi creare più configurazioni. È inoltre possibile nidificare le configurazioni.

>[!NOTE]
>
>In base ai requisiti di implementazione, oltre a **Modelli per frammenti di contenuto** e **Query GraphQL persistenti** potrebbe essere necessario selezionare anche altre opzioni di configurazione.

## Passaggi successivi {#next-steps}

Utilizzando questa configurazione, ora puoi passare alla seconda parte della guida introduttiva e [creare modelli per frammenti di contenuto.](create-content-model.md)

<!--
>[!TIP]
>
>For complete details about the Configuration Browser, [see the Configuration Browser documentation.](/help/sites-developing/configurations.md)
-->
