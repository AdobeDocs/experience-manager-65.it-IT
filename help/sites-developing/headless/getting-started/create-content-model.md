---
title: Guida rapida alla creazione di modelli per frammenti di contenuto headless
description: Definisci la struttura del contenuto creato e distribuito utilizzando le funzionalità headless di Adobe Experience Manager (AEM) utilizzando i modelli per frammenti di contenuto.
exl-id: 653e35c9-7b6a-49ae-b55d-af2ec40e257d
source-git-commit: b66ec42c35b5b60804015d340b8194bbd6ef3e28
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 55%

---

# Guida rapida alla creazione di modelli per frammenti di contenuto headless {#creating-content-fragment-models}

Definisci la struttura del contenuto creato e distribuito utilizzando le funzionalità headless di Adobe Experience Manager (AEM) utilizzando i modelli per frammenti di contenuto.

## Cosa sono i modelli per frammenti di contenuto? {#what-are-content-fragment-models}

[Ora che hai creato una configurazione,](create-configuration.md) puoi utilizzarla per creare modelli per frammenti di contenuto.

I modelli per frammenti di contenuto definiscono la struttura dei dati e del contenuto che puoi creare e gestire in AEM. Servono come una sorta di impalcatura per i tuoi contenuti. Quando si sceglie di creare i contenuti, gli autori selezionano dai modelli per frammenti di contenuto da te definiti, che li guidano nella creazione del contenuto.

## Creare un modello per frammenti di contenuto {#how-to-create-a-content-fragment-model}

Un architetto dell’informazione esegue tali attività solo occasionalmente, quando sono necessari nuovi modelli. Ai fini di questa guida introduttiva, stai creando un solo modello.

1. Accedi all’AEM e dal menu principale seleziona **Strumenti -> Risorse -> Modelli per frammenti di contenuto**.
1. Tocca o fai clic sulla cartella creata durante la creazione della configurazione.

   ![Cartella dei modelli](assets/models-folder.png)
1. Tocca o fai clic su **Crea**.
1. Fornisci un **Titolo modello**, **Tag**, e **Descrizione**. Puoi anche selezionare/deselezionare **Abilita modello** per assicurarti che il modello venga subito abilitato al momento della creazione.

   ![Creare un modello](assets/models-create.png)
1. Nella finestra di conferma, tocca o fai clic su **Apri** per configurare il modello.

   ![Finestra di conferma](assets/models-confirmation.png)
1. Utilizzando l’**Editor modello per frammenti di contenuto**, crea il modello per frammenti di contenuto trascinando i campi dalla colonna **Tipi di dati**.

   ![Trascinare i campi](assets/models-drag-and-drop.png)

1. Dopo aver inserito un campo, è necessario configurarne le proprietà. L’editor passa automaticamente al **Proprietà** per il campo aggiunto, in cui è possibile fornire i campi obbligatori.

   ![Configurare proprietà](assets/models-configure-properties.png)
1. Al termine della creazione del modello, tocca o fai clic su **Salva**.

1. La modalità del modello appena creato dipende dalla selezione o meno dell’opzione **Abilita modello** durante la creazione dello stesso:
   * selezionato: il nuovo modello è già **Abilitato**
   * non selezionato: il nuovo modello viene creato nella modalità **Bozza**

1. Se non è già abilitato, per poter essere utilizzato il modello deve essere **abilitato**.
   1. Seleziona il modello creato, quindi tocca o fai clic su **Abilita**.

      ![Abilitazione del modello](assets/models-enable.png)
   1. Conferma l’abilitazione del modello toccando o facendo clic su **Abilita** nella finestra di dialogo di conferma.

      ![Abilitazione della finestra di dialogo di conferma](assets/models-enabling.png)
1. Il modello è ora abilitato e pronto per essere utilizzato.

   ![Modello abilitato](assets/models-enabled.png)

Il **Editor modello per frammenti di contenuto** supporta molti tipi di dati diversi, ad esempio campi di testo semplice, riferimenti a risorse, riferimenti ad altri modelli e dati JSON.

Puoi creare più modelli. I modelli possono fare riferimento ad altri frammenti di contenuto. Utilizza le [configurazioni](create-configuration.md) per organizzare i modelli.

## Passaggi successivi {#next-steps}

Dopo aver definito le strutture dei frammenti di contenuto mediante la creazione di modelli, puoi passare alla terza parte della guida introduttiva e [creare cartelle in cui memorizzare i frammenti.](create-assets-folder.md)

>[!TIP]
>
>Per informazioni complete sui modelli per frammenti di contenuto, consulta [Documentazione dei modelli per frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md)
