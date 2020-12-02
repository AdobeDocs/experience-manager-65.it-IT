---
title: Anteprima delle risorse
description: Scopri come visualizzare in anteprima le risorse in Contenuti multimediali dinamici
uuid: 09e97245-373b-4d50-8ba3-5d1034a29988
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: bb8c355c-4475-45ec-9096-0975f0ce2c27
docset: aem65
translation-type: tm+mt
source-git-commit: a1e4d64a9ac7dc02c5cf2ac6b01994736c45b449
workflow-type: tm+mt
source-wordcount: '1344'
ht-degree: 3%

---


# Anteprima delle risorse mediante l&#39;interfaccia software {#previewing-assets}

Potete utilizzare Anteprima per vedere l’aspetto di una risorsa digitale caricata quando viene visualizzata da un cliente nel proprio browser Web. Per l’anteprima viene utilizzato il visualizzatore predefinito incorporato per dispositivi assegnato alla risorsa.

Un visualizzatore è una raccolta di varie impostazioni o &quot;predefiniti&quot;, come le dimensioni di visualizzazione del visualizzatore, il comportamento di zoom, gli schemi di colori, i bordi, i font e così via, che determinano in che modo gli utenti possono visualizzare le risorse multimediali sullo schermo del computer e sui dispositivi mobili.

Oltre a usare la funzione di anteprima dedicata per video, set 360 gradi e set di immagini, potete anche visualizzare l’anteprima di una risorsa mediante i predefiniti per visualizzatori creati precedentemente. Oppure, usate i predefiniti per immagini per visualizzare in anteprima le rappresentazioni delle immagini.

* [Applicazione dei predefiniti per immagini](/help/assets/image-presets.md)
* [Applicazione dei predefiniti per visualizzatori](/help/assets/viewer-presets.md)

>[!NOTE]
>
>Quando ti trovi su una pagina web (Sites) in AEM, non puoi visualizzare in anteprima le risorse in modalità **Modifica**. Per passare alla modalità **Anteprima**, fare clic su **Anteprima** nell&#39;angolo superiore destro della pagina.

Per attivare o disattivare i predefiniti per visualizzatori nell&#39;interfaccia utente, consultate [Gestione dei predefiniti per visualizzatori](/help/assets/managing-viewer-presets.md).

**Per visualizzare in anteprima le risorse mediante l&#39;interfaccia software**

1. Da **[!UICONTROL Adobe Experience Manager]**, nella pagina **[!UICONTROL Navigazione]**, toccare **[!UICONTROL Risorse]**, quindi **[!UICONTROL File]** per accedere alle risorse.
1. Nell&#39;angolo superiore destro della pagina, dall&#39;elenco a discesa **[!UICONTROL View]**, toccare **[!UICONTROL List View (Visualizzazione elenco).]**
1. (Facoltativo) Utilizzate la colonna **[!UICONTROL Tipo]** per ordinare le risorse in base al tipo di cui desiderate visualizzare l&#39;anteprima.
1. Nella colonna **[!UICONTROL Titolo]**, fate clic sul nome del titolo (non sulla miniatura) della risorsa da visualizzare in anteprima.
1. A seconda del tipo di risorsa su cui avete fatto clic, effettuate una delle seguenti operazioni:


   <table>
    <tbody>
      <tr>
      <td><strong>Tipo di risorsa su cui hai fatto clic</strong><br /> </td>
      <td><strong>È possibile visualizzare in anteprima la risorsa in una rappresentazione particolare?</strong></td>
      <td><strong>È possibile visualizzare in anteprima la risorsa in un visualizzatore?</strong></td>
      <td> </td>
      </tr>
      <tr>
      <td><p>3D</p> </td>
      <td>No</td>
      <td>Sì</td>
      <td><p><strong>Per visualizzare in anteprima una risorsa 3D nel visualizzatore dimensionale</strong></p>
      <ul>
      <li>Nell’angolo superiore sinistro della pagina, fare clic sull’icona in modo che venga visualizzato l’elenco a discesa. Fate clic su <strong>Visualizzatori</strong> nell'elenco, quindi selezionate il visualizzatore dimensionale.</li>
      <li>Toccate <strong>Reimposta</strong> per ripristinare lo zoom originale dell'immagine.</li>
      <li>Toccate <strong>Schermo intero</strong> per ottimizzare il visualizzatore sul dispositivo di visualizzazione.</li>
      </ul>
      <p><strong>Navigazione nella scena 3D</strong></p>
      <ul>
      <li><p><strong>Girare la fotocamera</strong>  3D - Orbire la vista intorno alla scena e agli oggetti 3D.</p> Mouse: Fare clic con il pulsante sinistro del mouse + trascinare. </p> Touch-screen: Premere + trascinamento.</p></li>
      <li><p><strong>Scorrimento della telecamera</strong>  - Scorrimento della vista verso sinistra, destra, verso l'alto e verso il basso.</p> Mouse: Fare clic con il pulsante destro del mouse e trascinare. </p> Touch-screen: Premere due dita e trascinare.</p></li>
      <li><p><strong>Zoom della fotocamera</strong>  - Zoom della fotocamera per spostarsi all'interno e all'esterno delle aree della scena 3D.</p> Mouse: Ruota di scorrimento. </p> Touch-screen: Pizzicotto con dito.</p></li>
      <li><p><strong>Ricentra la fotocamera</strong>  - Orbita la vista intorno alla scena e agli oggetti 3D.</p> Mouse: Fate doppio clic. </p> Touch-screen: Doppio tocco.</li></ul></td>
      </tr>
      <tr>
      <td><p>Immagine</p> </td>
      <td>Sì</td>
      <td>Sì</td>
      <td><p><strong>Per visualizzare in anteprima la risorsa in una rappresentazione particolare</strong></p>
      <ul>
      <li>Nell’angolo superiore sinistro della pagina, fare clic sull’icona in modo che venga visualizzato l’elenco a discesa. Fare clic su <strong>Rendering </strong>dall'elenco, quindi selezionare una rappresentazione particolare da visualizzare in anteprima.</li>
      </ul> <p><strong>Per visualizzare in anteprima la risorsa in un particolare visualizzatore</strong></p>
      <ul>
      <li>Nell’angolo superiore sinistro della pagina, fare clic sull’icona in modo che venga visualizzato l’elenco a discesa. Fate clic su <strong>Visualizzatori</strong> nell’elenco, quindi selezionate un visualizzatore da applicare alla risorsa.</li>
      </ul> <p>Utilizzate le icone <strong>+</strong> e <strong>-</strong> rispettivamente per aumentare o diminuire lo zoom dell'immagine selezionata. Fare clic su <strong>Reimposta</strong> per ripristinare lo zoom originale dell'immagine.<br /> Se siete su uno schermo tattile, toccate due volte l’immagine per ingrandire la visualizzazione per passaggi. Quando raggiungete lo zoom massimo, toccate nuovamente l’immagine per ripristinare lo stato di zoom. Trascinate sull’immagine per scorrere.</p> </td>
      </tr>
      <tr>
      <td>File multimediali</td>
      <td>Sì</td>
      <td>Sì</td>
      <td><p><strong>Per visualizzare in anteprima la risorsa in una rappresentazione particolare</strong></p>
      <ul>
      <li>Nell’angolo superiore sinistro della pagina, fare clic sull’icona in modo che venga visualizzato l’elenco a discesa. Fare clic su <strong>Rendering </strong>dall'elenco, quindi selezionare una rappresentazione particolare da visualizzare in anteprima.</li>
      </ul> <p>Selezionando una rappresentazione video ad alta risoluzione per l'anteprima del video, il video potrebbe risultare troncato. Questo perché l’anteprima della rappresentazione mostra la risoluzione esatta che i clienti vedranno, il tutto nel contesto del visualizzatore incorporato utilizzato per l’anteprima.</p> <p>Quando visualizzate l’anteprima di un set video adattivo a livello di risorsa, le rappresentazioni vengono raggruppate in un’unica esperienza di riproduzione. In altre parole, il video adattivo viene ridimensionato correttamente per la visualizzazione e la riproduzione utilizzando la risoluzione migliore nel contesto del dispositivo di visualizzazione e della velocità di connessione.<br /> </p> <p><strong>Per visualizzare in anteprima una risorsa in un particolare visualizzatore</strong></p>
      <ul>
      <li>Nell’angolo superiore sinistro della pagina, fare clic sull’icona in modo che venga visualizzato l’elenco a discesa. Fate clic su <strong>Visualizzatori</strong> nell’elenco, quindi selezionate un visualizzatore da applicare alla risorsa.</li>
      </ul> </td>
      </tr>
      <tr>
      <td>Set di immagini</td>
      <td>No</td>
      <td>Sì</td>
      <td><p><strong>Per visualizzare in anteprima una risorsa in un particolare visualizzatore</strong></p>
      <ul>
      <li>Nell’angolo superiore sinistro della pagina, fare clic sull’icona in modo che venga visualizzato l’elenco a discesa. Fate clic su <strong>Visualizzatori</strong> nell’elenco, quindi selezionate un visualizzatore da applicare alla risorsa.</li>
      </ul> <p>Utilizzate le icone <strong>+</strong> e <strong>-</strong> rispettivamente per aumentare o diminuire lo zoom dell'immagine selezionata. Fare clic su <strong>Reimposta</strong> per ripristinare lo zoom originale dell'immagine.<br /> Se siete su uno schermo tattile, toccate due volte l’immagine per ingrandire la visualizzazione per passaggi. Quando raggiungete lo zoom massimo, toccate nuovamente l’immagine per ripristinare lo stato di zoom. Trascinate sull’immagine per scorrere.</p> </td>
      </tr>
      <tr>
      <td>Set 360 gradi</td>
      <td>No</td>
      <td>Sì</td>
      <td><p><strong>Per visualizzare in anteprima una risorsa in un particolare visualizzatore</strong></p>
      <ul>
      <li>Nell’angolo superiore sinistro della pagina, fare clic sull’icona in modo che venga visualizzato l’elenco a discesa. Fate clic su <strong>Visualizzatori</strong> nell’elenco, quindi selezionate un visualizzatore da applicare alla risorsa.</li>
      </ul> <p>Utilizzate le icone <strong>+</strong> e <strong>-</strong> rispettivamente per aumentare o diminuire lo zoom dell'immagine selezionata. Fare clic su <strong>Reimposta</strong> per ripristinare lo zoom originale dell'immagine.<br /> Se siete su uno schermo tattile, toccate due volte l’immagine per ingrandire la visualizzazione per passaggi. Quando raggiungete lo zoom massimo, toccate nuovamente l’immagine per ripristinare lo stato di zoom. Trascinate sull’immagine per scorrere.</p> </td>
      </tr>
      <tr>
      <td>Set di file multimediali diversi</td>
      <td>No</td>
      <td>Sì</td>
      <td><p><strong>Per visualizzare in anteprima una risorsa in un particolare visualizzatore</strong></p>
      <ul>
      <li>Nell’angolo superiore sinistro della pagina, fare clic sull’icona in modo che venga visualizzato l’elenco a discesa. Fate clic su <strong>Visualizzatori</strong> nell’elenco, quindi selezionate un visualizzatore da applicare alla risorsa.</li>
      </ul> <p>Utilizzate le icone <strong>+</strong> e <strong>-</strong> rispettivamente per aumentare o diminuire lo zoom dell'immagine selezionata. Fare clic su <strong>Reimposta</strong> per ripristinare lo zoom originale dell'immagine.<br /> Se siete su uno schermo tattile, toccate due volte l’immagine per ingrandire la visualizzazione per passaggi. Quando raggiungete lo zoom massimo, toccate nuovamente l’immagine per ripristinare lo stato di zoom. Trascinate sull’immagine per scorrere.</p> </td>
      </tr>
      <tr>
      <td>Set carosello</td>
      <td>No</td>
      <td>Sì</td>
      <td><strong>Per visualizzare in anteprima una risorsa in un particolare visualizzatore</strong>
      <ul>
      <li>Nell’angolo superiore sinistro della pagina, fare clic sull’icona in modo che venga visualizzato l’elenco a discesa. Selezionate un visualizzatore da applicare alla risorsa.</li>
      </ul> </td>
      </tr>
      <tr>
      <td>360 Video<br /> </td>
      <td>Sì</td>
      <td>Sì</td>
      <td><p><strong>Per visualizzare in anteprima la risorsa in una rappresentazione particolare</strong></p>
      <ul>
      <li>Nell’angolo superiore sinistro della pagina, toccate l’icona in modo da visualizzare l’elenco a discesa. Selezionare <strong>Rendering</strong>, quindi selezionare la rappresentazione da visualizzare in anteprima.</li>
      </ul> <p><strong>Per visualizzare in anteprima la risorsa in un particolare visualizzatore</strong></p>
      <ul>
      <li>Nell’angolo superiore sinistro della pagina, toccate l’icona in modo da visualizzare l’elenco a discesa. Selezionate <strong>Visualizzatori</strong>, quindi selezionate un visualizzatore da applicare alla risorsa.</li>
      </ul> <p>Utilizzate le icone <strong>+</strong> e <strong>-</strong> rispettivamente per aumentare o diminuire lo zoom dell'immagine selezionata. Fare clic su <strong>Reimposta</strong> per ripristinare lo zoom originale dell'immagine.<br /> Se siete su uno schermo tattile, toccate due volte l’immagine per ingrandire la visualizzazione per passaggi. Quando raggiungete lo zoom massimo, toccate nuovamente l’immagine per ripristinare lo stato di zoom. Trascinate sull’immagine per scorrere.</p> </td>
      </tr>
    </tbody>
    </table>

## Anteprima delle risorse mediante la tastiera {#keyboard-navigation-asset-preview}

1. Dall’interfaccia utente Risorse, individuate la cartella che contiene la risorsa da visualizzare in anteprima.

1. Nella cartella, premere il tasto `<Tab>` o i tasti freccia della tastiera per selezionare la risorsa.

1. Premere `<Enter>` per aprire la risorsa selezionata in modalità di anteprima.

1. Effettua una delle operazioni seguenti:

   * Per ingrandire, premere `<Tab>` per spostare la messa a fuoco sull&#39;icona di zoom in (+), quindi premere `<Enter>` una o più volte per ingrandire in modo incrementale.

   * Per ridurre la visualizzazione, premere `<Tab>` per spostare la messa a fuoco sull&#39;icona di zoom out (-), quindi premere `<Enter>` una o più volte per ridurre la visualizzazione in modo incrementale.

   * Per spostare la visualizzazione di una risorsa *ingrandita* orizzontalmente o verticalmente, premere i rispettivi tasti freccia.

   * Premere `<Shift>` + `<Tab>` per reimpostare la visualizzazione e riattivare la risorsa.
