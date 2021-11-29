---
title: Guida rapida alla creazione di modelli di frammenti di contenuto headless
description: Definisci la struttura del contenuto che creerai e distribuirai utilizzando AEM funzionalità headless utilizzando Modelli per frammenti di contenuto .
exl-id: 8e3e4d00-34d3-4d4f-bc3a-43b8a322b986
source-git-commit: a5cb385aa369a5e59889e77597119358b77b55be
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 1%

---

# Guida rapida alla creazione di modelli di frammenti di contenuto headless {#creating-content-fragment-models}

Definisci la struttura del contenuto che creerai e distribuirai utilizzando AEM funzionalità headless utilizzando Modelli per frammenti di contenuto .

## Cosa sono i modelli di frammento di contenuto? {#what-are-content-fragment-models}

[Ora che hai creato una configurazione,](create-configuration.md) puoi utilizzarlo per creare modelli di frammenti di contenuto.

I modelli per frammenti di contenuto definiscono la struttura dei dati e del contenuto che verranno creati e gestiti in AEM. Servono come una sorta di impalcatura per i vostri contenuti. Quando scegli di creare un contenuto, gli autori selezionano i modelli di frammento di contenuto da te definiti, che li guida nella creazione di contenuti.

## Come creare un modello di frammento di contenuto {#how-to-create-a-content-fragment-model}

Un architetto dell&#39;informazione eseguirà queste attività solo sporadicamente quando sono necessari nuovi modelli. Ai fini di questa guida introduttiva, è necessario creare un solo modello.

1. Accedi a AEM e dal menu principale seleziona **Strumenti -> Risorse -> Modelli per frammenti di contenuto**.
1. Tocca o fai clic sulla cartella creata creando la configurazione.

   ![La cartella dei modelli](../assets/models-folder.png)
1. Tocca o fai clic su **Crea**.
1. Fornisci un **Titolo modello**, **Tag** e **Descrizione**. Puoi anche selezionare/deselezionare **Abilita modello** per controllare se il modello è immediatamente abilitato al momento della creazione.

   ![Creare un modello](../assets/models-create.png)
1. Nella finestra di conferma, tocca o fai clic su **Apri** per configurare il modello.

   ![Finestra di conferma](../assets/models-confirmation.png)
1. Utilizzo della **Editor modello frammento di contenuto**, crea il modello per frammenti di contenuto trascinando i campi dalla **Tipi di dati** colonna.

   ![Trascinare i campi](../assets/models-drag-and-drop.png)

1. Una volta inserito un campo, è necessario configurarne le proprietà. L’editor passa automaticamente al **Proprietà** scheda per il campo aggiunto in cui è possibile fornire i campi obbligatori.

   ![Configurare le proprietà](../assets/models-configure-properties.png)
1. Al termine della creazione del modello, tocca o fai clic su **Salva**.

1. La modalità del modello appena creato dipende dalla selezione o meno dell&#39;opzione **Abilita modello** durante la creazione del modello:
   * selezionato - il nuovo modello sarà già **Abilitato**
   * non selezionato - il nuovo modello verrà creato in **Bozza** modalità

1. Se non è già abilitato, il modello deve essere **Abilitato** per utilizzarlo.
   1. Seleziona il modello appena creato, quindi tocca o fai clic su **Abilita**.

      ![Abilitazione del modello](../assets/models-enable.png)
   1. Conferma l’abilitazione del modello toccando o facendo clic su **Abilita** nella finestra di dialogo di conferma.

      ![Attivare la finestra di dialogo di conferma](../assets/models-enabling.png)
1. Il modello è ora abilitato e pronto per essere utilizzato.

   ![Modello abilitato](../assets/models-enabled.png)

La **Editor modello frammento di contenuto** supporta molti tipi di dati diversi, ad esempio campi di testo semplici, riferimenti alle risorse, riferimenti ad altri modelli e dati JSON.

Puoi creare più modelli. I modelli possono fare riferimento ad altri frammenti di contenuto. Utilizzo [configurazioni](create-configuration.md) per organizzare i modelli.

## Passaggi successivi {#next-steps}

Dopo aver definito le strutture dei frammenti di contenuto mediante la creazione di modelli, puoi passare alla terza parte della guida introduttiva e [creare cartelle in cui memorizzare i frammenti stessi.](create-assets-folder.md)

>[!TIP]
>
>Per informazioni complete sui modelli di frammenti di contenuto, consulta la sezione [Documentazione dei modelli di frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md)
