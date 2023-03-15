---
title: Guida rapida alla creazione di modelli di frammenti di contenuto headless
description: Definisci la struttura del contenuto da creare e distribuire utilizzando le funzionalità headless di AEM, mediante i modelli per frammenti di contenuto.
exl-id: 653e35c9-7b6a-49ae-b55d-af2ec40e257d
source-git-commit: a2ababa9dd9115e963b91a7271d204d287557c40
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 93%

---

# Guida rapida alla creazione di modelli di frammenti di contenuto headless {#creating-content-fragment-models}

Definisci la struttura del contenuto da creare e distribuire utilizzando le funzionalità headless di AEM, mediante i modelli per frammenti di contenuto.

## Cosa sono i modelli per frammenti di contenuto? {#what-are-content-fragment-models}

[Ora che hai creato una configurazione,](create-configuration.md) puoi utilizzarla per creare modelli per frammenti di contenuto.

I modelli per frammenti di contenuto definiscono la struttura dei dati e del contenuto da creare e gestire in AEM. Servono come una sorta di impalcatura per i tuoi contenuti. Nella creazione di contenuti, questi vengono selezionati dagli autori in base ai modelli per frammenti di contenuto da te definiti, utilizzati come riferimento.

## Creare un modello per frammenti di contenuto {#how-to-create-a-content-fragment-model}

Un architetto dell’informazione esegue tali attività solo occasionalmente, quando sono necessari nuovi modelli. Ai fini di questa guida introduttiva, è necessario creare un solo modello.

1. Accedi a AEM e dal menu principale seleziona **Strumenti -> Risorse -> Modelli per frammenti di contenuto**.
1. Tocca o fai clic sulla cartella creata durante la creazione della configurazione.

   ![Cartella dei modelli](../assets/models-folder.png)
1. Tocca o fai clic su **Crea**.
1. Specifica un **titolo modello**, **tag** e **descrizione**. Puoi anche selezionare/deselezionare **Abilita modello** per assicurarti che il modello venga subito abilitato al momento della creazione.

   ![Creare un modello](../assets/models-create.png)
1. Nella finestra di conferma, tocca o fai clic su **Apri** per configurare il modello.

   ![Finestra di conferma](../assets/models-confirmation.png)
1. Utilizzando l’**Editor modello per frammenti di contenuto**, crea il modello per frammenti di contenuto trascinando i campi dalla colonna **Tipi di dati**.

   ![Trascinare i campi](../assets/models-drag-and-drop.png)

1. Dopo aver inserito un campo, è necessario configurarne le proprietà. L’editor passa automaticamente alla scheda **Proprietà** per il campo aggiunto, dove puoi specificare i campi obbligatori.

   ![Configurare proprietà](../assets/models-configure-properties.png)
1. Al termine della creazione del modello, tocca o fai clic su **Salva**.

1. La modalità del modello appena creato dipende dalla selezione o meno dell’opzione **Abilita modello** durante la creazione dello stesso:
   * selezionato: il nuovo modello è già **abilitato**
   * non selezionato: il nuovo modello viene creato nella modalità **Bozza**

1. Se non abilitato, per poter essere utilizzato il modello deve essere **abilitato**.
   1. Seleziona il modello appena creato, quindi tocca o fai clic su **Abilita**.

      ![Abilitazione del modello](../assets/models-enable.png)
   1. Conferma l’abilitazione del modello toccando o facendo clic su **Abilita** nella finestra di dialogo di conferma.

      ![Abilitazione della finestra di dialogo di conferma](../assets/models-enabling.png)
1. Il modello è ora abilitato e pronto per essere utilizzato.

   ![Modello abilitato](../assets/models-enabled.png)

L’**Editor modello per frammenti di contenuto** supporta differenti tipi di dati, ad esempio campi di testo semplice, riferimenti alle risorse, riferimenti ad altri modelli e dati JSON.

Puoi creare più modelli. I modelli possono fare riferimento ad altri frammenti di contenuto. Utilizza le [configurazioni](create-configuration.md) per organizzare i modelli.

## Passaggi successivi {#next-steps}

Dopo aver definito le strutture dei frammenti di contenuto mediante la creazione di modelli, puoi passare alla terza parte della guida introduttiva e [creare cartelle in cui memorizzare gli stessi frammenti.](create-assets-folder.md)

>[!TIP]
>
>Per informazioni complete sui modelli per frammenti di contenuto, consulta la [documentazione sui modelli per frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md)
