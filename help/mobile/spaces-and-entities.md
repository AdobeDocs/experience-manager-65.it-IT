---
title: Spazi ed entità
seo-title: Sviluppo  AEM Mobile Content Services
description: Questa pagina contiene una pagina di destinazione per lo sviluppo  AEM Mobile Content Services.
seo-description: Questa pagina contiene una pagina di destinazione per lo sviluppo  AEM Mobile Content Services.
uuid: eab5a61b-a9e8-4863-90a3-df1f18510cd8
contentOwner: Jyotika Syal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: ef568577-c74e-4fc2-b66e-eedac2948310
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 2%

---


# Spazi ed entità{#spaces-and-entities}

>[!NOTE]
>
> Adobe consiglia di utilizzare l&#39;editor SPA per i progetti che richiedono il rendering lato client basato sul framework dell&#39;applicazione a pagina singola (ad es. React). [Per saperne di più](/help/sites-developing/spa-overview.md).

Uno spazio è una posizione comoda per memorizzare le entità esposte tramite Content Services REST API. Ciò è particolarmente utile perché un&#39;app (o qualsiasi canale) può essere associata a più entità. Forzare le entità all&#39;interno di uno spazio forza la best practice per raggruppare i requisiti di un&#39;app. Facoltativamente, puoi associare un&#39;app in AEM a un numero limitato di spazi.

>[!NOTE]
>
>Per rendere disponibile qualcosa a qualsiasi canale da Content Services, deve trovarsi in uno spazio.

## Creazione di uno spazio {#creating-a-space}

Se l&#39;utente desidera esporre un insieme di contenuti e risorse a un&#39;app mobile, crea lo spazio utilizzando la dashboard AEM Mobile .

Per la prima volta che l&#39;utente non ha configurato i servizi di contenuto per l&#39;utilizzo di spazi, il dashboard di AEM Mobile  visualizza solo le app dopo aver selezionato **Content Services**.

>[!CAUTION]
>
>**Prerequisiti per l’aggiunta di uno spazio**
>
>Controllare **Abilita AEM Content Services** per lavorare con Spaces e attivarlo nel dashboard  applicazione AEM Mobile.
>
>Per ulteriori informazioni, vedere [Amministrazione di Content Services](/help/mobile/developing-content-services.md).

Una volta configurati gli spazi nel dashboard, effettuate le seguenti operazioni per creare spazi:

1. Scegliere **Spazi** da Content Services.

   ![chlimage_1-83](assets/chlimage_1-83.png)

1. Scegliere **Crea** per creare uno spazio. Immettere **Titolo**, **Nome** e **Descrizione** per lo spazio.

   Fai clic su **Crea**.

   ![chlimage_1-84](assets/chlimage_1-84.png)

## Gestione di uno spazio {#managing-a-space}

Dopo aver creato uno spazio, fate clic su a sinistra per gestire lo spazio nell’elenco.

Potete visualizzare le proprietà dello spazio, eliminare lo spazio o pubblicare lo spazio e il relativo contenuto in un’istanza di pubblicazione AEM.

![chlimage_1-85](assets/chlimage_1-85.png)

**Visualizzazione e modifica delle proprietà di uno spazio**

1. Selezionare lo spazio dall&#39;elenco
1. Scegliere **Proprietà** dalla barra degli strumenti
1. Fare clic su **Chiudi**

**Pubblicazione di uno** spazio: quando viene pubblicato uno spazio, vengono pubblicate anche tutte le cartelle e le entità in tale spazio.

1. Selezionare lo spazio facendo clic sulla relativa icona nell&#39;elenco Console spazio
1. Scegliere **Pubblica albero**

>[!NOTE]
>
>Potete **Annullare la pubblicazione** di uno spazio, rimuovendo così lo spazio dall&#39;istanza di pubblicazione.
>
>L’immagine seguente illustra le azioni che è possibile eseguire dopo la pubblicazione dello spazio.

![chlimage_1-86](assets/chlimage_1-86.png)

## Utilizzo delle cartelle in uno spazio {#working-with-folders-in-a-space}

Gli spazi possono includere cartelle per organizzare ulteriormente il contenuto e le risorse dello spazio. Gli utenti possono creare una propria gerarchia sotto uno spazio.

### Creazione di una cartella {#creating-a-folder}

1. Fare clic sullo spazio nell&#39;elenco nella console dello spazio e fare clic su **Crea cartella**

   ![chlimage_1-87](assets/chlimage_1-87.png)

1. Immettere **Titolo**, **Nome,** e **Descrizione** per la cartella

   ![chlimage_1-88](assets/chlimage_1-88.png)

1. Fare clic su **Crea** per creare la cartella in uno spazio

## Copia lingua {#language-copy}

>[!CAUTION]
>
>Copia lingua non è completamente funzionante per questa versione. Imposta solo la struttura.

La funzione **Copia lingua** consente agli autori di copiare la copia lingua principale e quindi creare un progetto e un flusso di lavoro per tradurre automaticamente il contenuto. Copia lingua crea la struttura corretta. Dopo aver aggiunto una cartella in uno spazio, potete aggiungere una copia della lingua allo spazio.

>[!NOTE]
>
>È consigliabile che tutti i contenuti che possono essere convertiti, siano inseriti nel nodo Copia lingua.

### Aggiunta di una copia della lingua {#adding-language-copy}

1. Una volta creato lo spazio, fate clic su tale spazio per creare una copia per la lingua.

   Fare clic su **Crea** e scegliere **Copia lingua**.

   ![chlimage_1-89](assets/chlimage_1-89.png)

   >[!NOTE]
   >
   >I nodi Copia lingua possono esistere solo come figlio diretto dello Spazio.

1. Scegliete **Lingua&amp;amp pacchetto contenuto;ast;** e immettete il **Titolo&amp;ast;** nella finestra di dialogo **Crea copia lingua**.

   Fai clic su **Crea**.

   ![chlimage_1-90](assets/chlimage_1-90.png)

1. Dopo aver creato una copia della lingua, questa viene visualizzata nello spazio in **Language Master**.

   ![chlimage_1-91](assets/chlimage_1-91.png)

   >[!NOTE]
   >
   >Selezionare **Language Master** per visualizzare le cartelle di copia lingua.

### Rimozione di una cartella dallo spazio {#removing-a-folder-from-the-space}

1. Selezionate la cartella dall’elenco dei contenuti spaziali
1. Fare clic su **Elimina** dalla barra degli strumenti

   >[!NOTE]
   >
   >Per navigare in una cartella e visualizzarne il contenuto o aggiungere una sottocartella o un&#39;entità, fate clic sul titolo della cartella nell&#39;elenco del contenuto dello spazio.

## Utilizzo delle entità in uno spazio {#working-with-entities-in-a-space}

Le entità rappresentano il contenuto esposto tramite l&#39;endpoint del servizio Web. Le entità sono memorizzate in spazi in modo che possano essere facilmente reperite e sono tenute indipendenti dalla struttura del repository AEM che contiene il relativo contenuto.

È possibile raggruppare le entità in una raccolta logica. A questo scopo, potete creare un numero qualsiasi di cartelle.

Se gli elementi figlio dell&#39;entità, che sono altre entità, vengono raccolti per la modellazione dei dati, l&#39;utente sviluppatore può creare specifici &quot;Modelli di gruppo&quot; dal tipo di modello &quot;Gruppo entità&quot; fornito out-of-the-box.

>[!NOTE]
>
>Le entità sono sempre associate a uno spazio, per cui la maggior parte dell&#39;interfaccia utente dell&#39;entità è accessibile tramite la console dello spazio.

### Creazione di un&#39;entità {#creating-an-entity}

1. Aprite la console Spazio e fate clic sul titolo dello spazio.

   Facoltativamente, potete passare alla cartella facendo clic sul titolo della cartella nell’elenco.

   ![chlimage_1-92](assets/chlimage_1-92.png)

1. Scegliete il modello per l&#39;entità. Questo è il tipo di entità che si desidera creare. Fai clic su Avanti.

   ![chlimage_1-93](assets/chlimage_1-93.png)

   >[!NOTE]
   >
   >È possibile scegliere il **Modello risorse**, **Modello pagine** o un modello di entità creato in precedenza.
   >
   >Per creare un&#39;entità personalizzata, vedere [Creazione di un modello](/help/mobile/administer-mobile-apps.md).

1. Immettere un **Titolo**, **Nome**, **Descrizione** e **Tag** per l&#39;entità. Fai clic su **Crea**.

   ![chlimage_1-94](assets/chlimage_1-94.png)

   Al termine, l&#39;entità viene visualizzata nei discendenti dello spazio.

### Modifica di un&#39;entità {#editing-an-entity}

1. Dopo aver creato un&#39;entità, accedete alla cartella o allo spazio e scegliete l&#39;entità dalla console Spazio da modificare.

   ![chlimage_1-95](assets/chlimage_1-95.png)

1. Selezionate un&#39;entità da modificare e fate clic su **Modifica**.

   ![chlimage_1-96](assets/chlimage_1-96.png)

   >[!CAUTION]
   >
   >A seconda del modello scelto per creare l&#39;entità, l&#39;interfaccia utente sarà diversa per entrambi, per la modifica e la visualizzazione delle proprietà dell&#39;entità. Per ulteriori informazioni, consulta i passaggi riportati di seguito.

   ***Se scegliete il modello per la creazione dell&#39;entità come modelli*** di risorse, facendo clic su  **** Modifica potete aggiungere risorse come illustrato nella figura seguente:

   ![chlimage_1-97](assets/chlimage_1-97.png)

   In alternativa, puoi fare clic su **Anteprima** per visualizzare il collegamento json.

   ![chlimage_1-98](assets/chlimage_1-98.png)

   ***Se scegliete il modello per la creazione dell&#39;entità come Modelli*** di pagine, facendo clic su  **** Modifica potete aggiungere risorse come illustrato nella figura seguente:

   ![chlimage_1-99](assets/chlimage_1-99.png)

   Fate clic sull&#39;icona in **Path** per aggiungere una risorsa

   ![chlimage_1-100](assets/chlimage_1-100.png)

   >[!NOTE]
   >
   >Una volta aggiunta un&#39;entità, questa deve essere salvata per consentire il funzionamento del collegamento Anteprima. Per visualizzare l&#39;anteprima, fare clic su **Salva**. Facendo clic su **Preview** viene visualizzato il json della risorsa aggiunta, come illustrato nella figura seguente:

   ![chlimage_1-101](assets/chlimage_1-101.png)

   >[!NOTE]
   >
   >Dopo aver aggiunto le risorse all&#39;entità, potete scegliere **Salva** per salvare le modifiche oppure scegliere **Salva e chiudi** per salvare e reindirizzare l&#39;elenco della console Spazio in cui sono definite le entità.

   Inoltre, selezionate un&#39;entità dall&#39;elenco della console spaziale e fate clic su **Proprietà** per visualizzare e modificare le proprietà di un&#39;entità definita.

   ![chlimage_1-102](assets/chlimage_1-102.png)

   Potete modificare il titolo, la descrizione, i tag e aggiungere le risorse all&#39;entità.

   ![chlimage_1-103](assets/chlimage_1-103.png)

### Rimozione di un&#39;entità {#removing-an-entity}

1. Selezionare l&#39;entità dall&#39;elenco dei contenuti dello spazio

   ![chlimage_1-104](assets/chlimage_1-104.png)

1. Fare clic su **Elimina** nella barra degli strumenti per rimuovere l&#39;entità specifica dallo spazio

### Pubblicazione di un&#39;entità {#publishing-an-entity}

È possibile scegliere **Pubblica albero** o **Pubblicazione rapida** per pubblicare l&#39;entità.

1. Selezionate un&#39;entità dall&#39;elenco della console dello spazio e fate clic su **Pubblica albero **per pubblicare tale entità e i relativi elementi secondari.

   ![chlimage_1-105](assets/chlimage_1-105.png)

   **Oppure**,

   Fate clic su **Pubblicazione rapida** per pubblicare tale entità specifica.
