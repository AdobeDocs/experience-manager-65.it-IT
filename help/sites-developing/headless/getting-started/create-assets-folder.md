---
title: Guida rapida alla creazione di una cartella Assets Headless
description: Utilizza i modelli per frammenti di contenuto di AEM per definire la struttura dei frammenti di contenuto, che sta alla base dei contenuti headless.
exl-id: 8d913056-fcfa-4cdd-b40a-771f13dfd0f4
source-git-commit: a2ababa9dd9115e963b91a7271d204d287557c40
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 87%

---

# Guida rapida alla creazione di una cartella Assets Headless {#creating-an-assets-folder}

Utilizza i modelli per frammenti di contenuto di AEM per definire la struttura dei frammenti di contenuto, che sta alla base dei contenuti headless. I frammenti di contenuto vengono poi memorizzati nelle cartelle di risorse.

## Cos’è una cartella di risorse? {#what-is-an-assets-folder}

[Dopo aver creato i modelli per frammenti di contenuto](create-content-model.md) che definiscono la struttura per i futuri frammenti di contenuto, è ora di creare alcuni frammenti.

Tuttavia, è necessario innanzitutto creare una cartella di risorse in cui memorizzarli.

Le cartelle di risorse vengono utilizzate per [organizzare le risorse di contenuti tradizionali](/help/assets/manage-assets.md), come immagini e video, nonché i frammenti di contenuto.

## Creare una cartella di risorse {#how-to-create-an-assets-folder}

Di solito, un amministratore deve creare cartelle solo occasionalmente, per organizzare i contenuti al momento della creazione. Ai fini di questa guida introduttiva, è sufficiente creare una sola cartella.

1. Accedi a AEM e dal menu principale seleziona **Navigazione -> Risorse -> File**.
1. Tocca o fai clic su **Crea -> Cartella**.
1. Specifica il **titolo** e il **nome** da assegnare alla cartella.
   * Il **titolo** deve essere descrittivo.
   * Il **nome** diventerà il nome del nodo nell’archivio.
      * Viene generato automaticamente dal titolo, secondo le [convenzioni di denominazione di AEM.](/help/sites-developing/naming-conventions.md)
      * Se necessario è possibile modificarlo.

   ![Crea cartella](../assets/assets-folder-create.png)
1. Seleziona la cartella appena creata, quindi seleziona **Proprietà** dalla barra degli strumenti (oppure utilizza la `p` [scelte rapide da tastiera.](/help/sites-authoring/keyboard-shortcuts.md))
1. In **Proprietà**, seleziona la scheda **Servizi cloud**.
1. In **Configurazione cloud** seleziona la [configurazione creata in precedenza.](create-configuration.md)

   ![Configurare la cartella delle risorse](../assets/assets-folder-configure.png)
1. Tocca o fai clic su **Salva e chiudi**.
1. Nella finestra di conferma tocca o fai clic su **OK**.

   ![Finestra di conferma](../assets/assets-folder-confirmation.png)

Puoi creare ulteriori sottocartelle all’interno della cartella appena creata. Le sottocartelle ereditano la **configurazione cloud** della cartella principale. Tuttavia, questo può essere ignorato se vuoi utilizzare i modelli di un’altra configurazione.

Se utilizzi una struttura del sito localizzata, puoi [creare una directory principale della lingua](/help/assets/multilingual-assets.md) al di sotto della nuova cartella.

## Passaggi successivi {#next-steps}

Dopo aver creato una cartella per i frammenti di contenuto, puoi passare alla quarta parte della guida introduttiva e [creare frammenti di contenuto.](create-content-fragment.md)

>[!TIP]
>
>Per informazioni dettagliate sulla gestione dei frammenti di contenuto, consulta la [documentazione sui frammenti di contenuto](/help/assets/content-fragments/content-fragments.md).
