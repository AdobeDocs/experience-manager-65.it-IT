---
title: Spazi ed entità
seo-title: Developing AEM Mobile Content Services
description: Questa pagina fornisce una pagina di destinazione per lo sviluppo di AEM Mobile Content Services.
seo-description: This page serves a landing page for developing AEM Mobile Content Services.
uuid: eab5a61b-a9e8-4863-90a3-df1f18510cd8
contentOwner: Jyotika Syal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: ef568577-c74e-4fc2-b66e-eedac2948310
exl-id: 44591900-b01b-4a33-9910-839564477e7d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1192'
ht-degree: 3%

---

# Spazi ed entità{#spaces-and-entities}

>[!NOTE]
>
>Adobe consiglia di utilizzare l’editor di SPA per i progetti che richiedono il rendering lato client basato sul framework di un’applicazione a pagina singola (ad esempio, React). [Per saperne di più](/help/sites-developing/spa-overview.md).

Uno spazio è una posizione comoda per memorizzare le entità esposte tramite l’API REST di Content Services. Questa funzione è particolarmente utile perché un’app (o qualsiasi canale) può essere associata a più entità. Forzare le entità all’interno di uno spazio forza la best practice per raggruppare i requisiti di un’app. Facoltativamente, puoi associare un’app in AEM a un numero ridotto di spazi.

>[!NOTE]
>
>Per rendere disponibile qualcosa a qualsiasi canale da Content Services, deve trovarsi in uno spazio.

## Creazione di uno spazio {#creating-a-space}

Se l’utente desidera esporre una serie di contenuti e risorse a un’app mobile, crea lo spazio utilizzando il dashboard di AEM Mobile.

Per la prima volta che l’utente non ha configurato i servizi di contenuto per lavorare con gli spazi, il dashboard di AEM Mobile visualizza solo le app dopo aver selezionato **Content Services**.

>[!CAUTION]
>
>**Prerequisiti per l’aggiunta di uno spazio**
>
>Controlla la **Abilita AEM Content Services** per lavorare con Spaces e abilitarlo nel dashboard delle applicazioni AEM Mobile.
>
>Vedi [Amministrazione dei servizi di contenuti](/help/mobile/developing-content-services.md) per ulteriori dettagli.

Dopo aver configurato Spaces nel dashboard, segui questi passaggi per creare Spaces:

1. Scegli **Spazi** da Content Services.

   ![chlimage_1-83](assets/chlimage_1-83.png)

1. Scegli **Crea** per creare uno spazio. Invio **Titolo**, **Nome** e **Descrizione** per lo spazio.

   Fai clic su **Crea**.

   ![chlimage_1-84](assets/chlimage_1-84.png)

## Gestione di uno spazio {#managing-a-space}

Dopo aver creato uno spazio, fai clic su a sinistra per gestire lo spazio nell’elenco.

Puoi visualizzare le proprietà dello spazio, eliminare lo spazio o pubblicare lo spazio e il relativo contenuto in un’istanza di pubblicazione AEM.

![chlimage_1-85](assets/chlimage_1-85.png)

**Visualizzazione e modifica delle proprietà di uno spazio**

1. Selezionare lo spazio dall’elenco
1. Scegli **Proprietà** dalla barra degli strumenti
1. Fai clic su **Chiudi** al termine

**Pubblicazione di uno spazio** Quando viene pubblicato uno spazio, vengono pubblicate anche tutte le cartelle e le entità in tale spazio.

1. Selezionare lo spazio facendo clic sulla relativa icona nell’elenco Console spazio
1. Scegli **Pubblica albero**

>[!NOTE]
>
>È possibile **Annulla pubblicazione** uno spazio, che rimuove lo spazio dall&#39;istanza di pubblicazione.
>
>L’immagine seguente illustra le azioni che possono essere eseguite dopo la pubblicazione dello spazio.

![chlimage_1-86](assets/chlimage_1-86.png)

## Utilizzo delle cartelle in uno spazio {#working-with-folders-in-a-space}

Gli spazi possono includere cartelle per organizzare ulteriormente il contenuto e le risorse dello spazio. Gli utenti possono creare una propria gerarchia sotto uno spazio.

### Creazione di una cartella {#creating-a-folder}

1. Fai clic sullo spazio nell’elenco della console spazio e fai clic su **Crea cartella**

   ![chlimage_1-87](assets/chlimage_1-87.png)

1. Inserisci il **Titolo**, **Nome,** e **Descrizione** per la cartella

   ![chlimage_1-88](assets/chlimage_1-88.png)

1. Fai clic su **Crea** per creare la cartella in uno spazio

## Copia lingua {#language-copy}

>[!CAUTION]
>
>La copia in lingua non funziona completamente per questa versione. Imposta solo la struttura.

La **Copia lingua** consente agli autori di copiare la copia principale della lingua e quindi di creare un progetto e un flusso di lavoro per tradurre automaticamente il contenuto. La copia in lingua crea la struttura corretta. Una volta aggiunta una cartella in uno spazio, è possibile aggiungere una copia per lingua allo spazio disponibile.

>[!NOTE]
>
>È consigliabile inserire qualsiasi contenuto che possa essere tradotto nel nodo Copia lingua.

### Aggiunta di una copia in lingua {#adding-language-copy}

1. Una volta creato lo spazio, fai clic su tale spazio per creare una copia per lingua.

   Fai clic su **Crea** e scegli **Copia lingua**.

   ![chlimage_1-89](assets/chlimage_1-89.png)

   >[!NOTE]
   >
   >I nodi Copia lingua possono esistere solo come elementi secondari diretti di Space.

1. Scegli **Lingua&amp;ast pacchetto contenuti;** e inserisci **Titolo&amp;ast;** in **Crea copia in lingua** finestra di dialogo.

   Fai clic su **Crea**.

   ![chlimage_1-90](assets/chlimage_1-90.png)

1. Una volta creata una copia in lingua, questa viene visualizzata nello spazio in **Master per lingua**.

   ![chlimage_1-91](assets/chlimage_1-91.png)

   >[!NOTE]
   >
   >Seleziona **Master per lingua** per visualizzare le cartelle di copia della lingua.

### Rimozione di una cartella dallo spazio {#removing-a-folder-from-the-space}

1. Selezionare la cartella dall’elenco dei contenuti spaziali
1. Fai clic su **Elimina** dalla barra degli strumenti

   >[!NOTE]
   >
   >Per spostarsi in una cartella e visualizzarne il contenuto o aggiungere una sottocartella o un’entità, fare clic sul titolo della cartella nell’elenco dei contenuti dello spazio.

## Utilizzo delle entità in uno spazio {#working-with-entities-in-a-space}

Le entità rappresentano il contenuto esposto tramite l’endpoint del servizio Web. Le entità vengono memorizzate in spazi in modo che possano essere facilmente trovate e mantenute indipendenti dalla struttura dell’archivio AEM che contiene il relativo contenuto.

È possibile raggruppare le entità in una raccolta logica. A questo scopo, puoi creare un numero qualsiasi di cartelle.

Se gli elementi figlio dell’entità, che sono altre entità, sono raccolti per la modellazione dei dati, l’utente sviluppatore può creare specifici &quot;Modelli di gruppo&quot; dal tipo di modello &quot;Gruppo di entità&quot;, fornito pronto all’uso.

>[!NOTE]
>
>Le entità sono sempre associate a uno spazio, pertanto la maggior parte dell’interfaccia utente dell’entità è accessibile tramite la console dello spazio.

### Creazione di un&#39;entità {#creating-an-entity}

1. Apri la console Spazio e fai clic sul titolo dello spazio.

   Facoltativamente, puoi passare alla cartella facendo clic sul titolo della cartella nell’elenco.

   ![chlimage_1-92](assets/chlimage_1-92.png)

1. Scegli il modello per l’entità. Questo è il tipo di entità che desideri creare. Fai clic su Avanti.

   ![chlimage_1-93](assets/chlimage_1-93.png)

   >[!NOTE]
   >
   >Hai la possibilità di scegliere la **Modello Assets**, **Modello Pagine** o un modello di tipo di entità creato in precedenza.
   >
   >Vedi [Creazione di un modello](/help/mobile/administer-mobile-apps.md), per creare l’entità personalizzata.

1. Inserisci un **Titolo**, **Nome**, **Descrizione** e **Tag** per l’entità. Fai clic su **Crea**.

   ![chlimage_1-94](assets/chlimage_1-94.png)

   Al termine, l’entità viene visualizzata nei discendenti dello spazio.

### Modifica di un&#39;entità {#editing-an-entity}

1. Dopo aver creato un’entità, accedi alla cartella o allo spazio e scegli l’entità dalla console Spazio da modificare.

   ![chlimage_1-95](assets/chlimage_1-95.png)

1. Seleziona un’entità da modificare e fai clic su **Modifica**.

   ![chlimage_1-96](assets/chlimage_1-96.png)

   >[!CAUTION]
   >
   >A seconda del modello che scegli di creare l’entità, l’interfaccia utente sarà diversa per entrambi, per la modifica e la visualizzazione delle proprietà dell’entità. Per ulteriori informazioni, consulta i passaggi seguenti.

   ***Se scegli il modello per la creazione dell’entità come modelli di risorse***, facendo clic su **Modifica** consente di aggiungere risorse come illustrato nella figura seguente:

   ![chlimage_1-97](assets/chlimage_1-97.png)

   In alternativa, puoi fare clic su **Anteprima** per visualizzare il collegamento json.

   ![chlimage_1-98](assets/chlimage_1-98.png)

   ***Se scegli il modello per la creazione dell’entità come modelli di pagine***, facendo clic su **Modifica** consente di aggiungere risorse come illustrato nella figura seguente:

   ![chlimage_1-99](assets/chlimage_1-99.png)

   Fai clic sull’icona nella **Percorso** per aggiungere una risorsa

   ![chlimage_1-100](assets/chlimage_1-100.png)

   >[!NOTE]
   >
   >Una volta aggiunta un’entità, questa deve essere salvata per il funzionamento del collegamento Anteprima . Per visualizzare l&#39;anteprima, fai clic su **Salva**. Fai clic sul pulsante **Anteprima** mostra il json della risorsa aggiunta, come illustrato nella figura seguente:

   ![chlimage_1-101](assets/chlimage_1-101.png)

   >[!NOTE]
   >
   >Al termine dell’aggiunta di risorse all’entità, potete scegliere **Salva** per salvare le modifiche o scegliere **Salva e chiudi** per salvare e reindirizzare all’elenco della console Spazio in cui sono definite le entità.

   Inoltre, seleziona un’entità dall’elenco della console spaziale e fai clic su **Proprietà** per visualizzare e modificare le proprietà di un’entità definita.

   ![chlimage_1-102](assets/chlimage_1-102.png)

   Puoi modificare il titolo, la descrizione, i tag e aggiungere le risorse all’entità.

   ![chlimage_1-103](assets/chlimage_1-103.png)

### Rimozione di un&#39;entità {#removing-an-entity}

1. Seleziona l’entità dall’elenco dei contenuti nello spazio

   ![chlimage_1-104](assets/chlimage_1-104.png)

1. Fai clic su **Elimina** dalla barra degli strumenti per rimuovere l’entità specifica dallo spazio

### Pubblicazione di un&#39;entità {#publishing-an-entity}

Hai la possibilità di scegliere **Pubblica albero** o **Pubblicazione rapida** per pubblicare l’entità.

1. Seleziona un’entità dall’elenco della console spazio e fai clic su **Pubblica albero **per pubblicare tale entità e i relativi elementi secondari.

   ![chlimage_1-105](assets/chlimage_1-105.png)

   **Oppure**,

   Fai clic su **Pubblicazione rapida** per pubblicare tale entità specifica.
