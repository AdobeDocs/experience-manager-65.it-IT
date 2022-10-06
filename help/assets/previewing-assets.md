---
title: Visualizzare l’anteprima delle risorse
description: Scopri come visualizzare in anteprima le risorse in Dynamic Media.
uuid: 09e97245-373b-4d50-8ba3-5d1034a29988
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: bb8c355c-4475-45ec-9096-0975f0ce2c27
docset: aem65
feature: Asset Management
role: User, Admin
exl-id: 84f0c406-4ab6-48c7-8223-61a8c3ade363
source-git-commit: 363e5159d290ecfbf4338f6b9793e11b613389a5
workflow-type: tm+mt
source-wordcount: '1369'
ht-degree: 2%

---

# Anteprima delle risorse tramite l’interfaccia software {#previewing-assets}

Puoi utilizzare Anteprima per vedere l’aspetto di una risorsa digitale caricata quando viene visualizzata da un cliente nel proprio browser web. Per l’anteprima viene utilizzato il visualizzatore predefinito incorporato per più dispositivi assegnato alla risorsa.

Un visualizzatore è una raccolta di varie impostazioni o *predefiniti*, ad esempio dimensioni di visualizzazione, comportamento di zoom, schemi di colore, bordi e font del visualizzatore. Questi predefiniti determinano il modo in cui gli utenti visualizzano le risorse multimediali sullo schermo del computer e sui dispositivi mobili.

Oltre a utilizzare la funzione Anteprima dedicata per video, set 360 gradi e set di immagini, puoi anche visualizzare in anteprima una risorsa utilizzando i predefiniti visualizzatore creati. Oppure, utilizza i predefiniti immagine per visualizzare in anteprima le rappresentazioni delle immagini.

* [Applica predefiniti immagine](/help/assets/image-presets.md)
* [Applica predefiniti visualizzatore](/help/assets/viewer-presets.md)

>[!NOTE]
>
>Quando ti trovi su una pagina web (Sites) in Adobe Experience Manager, non puoi visualizzare in anteprima le risorse in **Modifica** modalità. Passa alla modalità Anteprima facendo clic su **[!UICONTROL Anteprima]** nell’angolo in alto a destra della pagina.

Per abilitare o disabilitare i predefiniti visualizzatore nell’interfaccia utente, vedi [Gestire i predefiniti per visualizzatori](/help/assets/managing-viewer-presets.md).

**Per visualizzare in anteprima le risorse utilizzando l’interfaccia software:**

1. Da **[!UICONTROL Adobe Experience Manager]**, sul **[!UICONTROL Navigazione]** pagina, seleziona **[!UICONTROL Risorse]**, quindi **[!UICONTROL File]** per accedere alle risorse.
1. Vicino all’angolo superiore destro della pagina, dal **[!UICONTROL Visualizza]** elenco a discesa, seleziona **[!UICONTROL Vista a elenco]**.
1. (Facoltativo) Utilizza il **[!UICONTROL Tipo]** per ordinare le risorse in base al tipo da visualizzare in anteprima.
1. Sotto la **[!UICONTROL Titolo]** fai clic sul nome del titolo (non sulla miniatura) della risorsa da visualizzare in anteprima.
1. A seconda del tipo di risorsa su cui hai fatto clic, effettua una delle seguenti operazioni:


   <table>
    <tbody>
      <tr>
      <td><strong>Tipo di risorsa su cui hai fatto clic</strong><br /> </td>
      <td><strong>In grado di visualizzare in anteprima la risorsa in un rendering specifico?</strong></td>
      <td><strong>In grado di visualizzare in anteprima la risorsa in un visualizzatore?</strong></td>
      <td> </td>
      </tr>
      <tr>
      <td><p>3D</p> </td>
      <td>No</td>
      <td>Sì</td>
      <td><p><strong>Visualizzazione in anteprima di una risorsa 3D nel visualizzatore dimensionale</strong></p>
      <ul>
      <li>Fai clic sull’icona nell’angolo in alto a sinistra della pagina per visualizzare l’elenco a discesa. Seleziona <strong>Visualizzatori</strong> dall’elenco, seleziona il visualizzatore dimensionale.</li>
      <li>Seleziona <strong>Reimposta</strong> per ripristinare l'immagine allo zoom originale.</li>
      <li>Seleziona <strong>Schermo intero</strong> per massimizzare il visualizzatore sul dispositivo di visualizzazione.</li>
      </ul>
      <p><strong>Navigazione nella scena 3D</strong></p>
      <ul>
      <li><p><strong>Girare la fotocamera 3D</strong> - Orbita la tua vista intorno alla scena e agli oggetti 3D.</p> Mouse: Clic a sinistra + Trascina </p> Schermo tattile: Premi + Trascina</p></li>
      <li><p><strong>Panning della fotocamera</strong> - Consente di scorrere la visualizzazione a sinistra, a destra, su e giù.</p> Mouse: Clic destro su + Trascina </p> Schermo tattile: Pressione a due dita + trascinamento</p></li>
      <li><p><strong>Zoom della fotocamera</strong> - Zoom della videocamera per entrare e uscire dalle aree della scena 3D.</p> Mouse: Rotellina di scorrimento </p> Schermo tattile: Pizzicotto</p></li>
      <li><p><strong>Ricollegare la fotocamera</strong> - Orbita la tua vista intorno alla scena e agli oggetti 3D.</p> Mouse: Fare doppio clic </p> Schermo tattile: Doppio tocco</li></ul></td>
      </tr>
      <tr>
      <td><p>Immagine</p> </td>
      <td>Sì</td>
      <td>Sì</td>
      <td><p><strong>Visualizzazione in anteprima della risorsa in un rendering specifico</strong></p>
      <ul>
      <li>Fai clic sull’icona nell’angolo in alto a sinistra della pagina per visualizzare l’elenco a discesa. Seleziona <strong>Rendering </strong>dall’elenco, selezionare un rendering specifico da visualizzare in anteprima.</li>
      </ul> <p><strong>Per visualizzare in anteprima la risorsa in un particolare visualizzatore</strong></p>
      <ul>
      <li>Fai clic sull’icona nell’angolo in alto a sinistra della pagina per visualizzare l’elenco a discesa. Seleziona <strong>Visualizzatori</strong> dall’elenco, seleziona un visualizzatore da applicare alla risorsa.</li>
      </ul> <p>Utilizza la <strong>+</strong> e <strong>-</strong> per aumentare o diminuire lo zoom dell’immagine selezionata, rispettivamente. Seleziona <strong>Reimposta</strong> per ripristinare l'immagine allo zoom originale.<br /> Se ti trovi su uno schermo tattile, tocca due volte l’immagine per ingrandirla in base ai passaggi. Quando raggiungete lo zoom massimo, toccate nuovamente l’immagine per ripristinare lo stato di zoom. Trascina l’immagine per eseguire il panning.</p> </td>
      </tr>
      <tr>
      <td>File multimediali</td>
      <td>Sì</td>
      <td>Sì</td>
      <td><p><strong>Visualizzazione in anteprima della risorsa in un rendering specifico</strong></p>
      <ul>
      <li>Fai clic sull’icona nell’angolo in alto a sinistra della pagina per visualizzare l’elenco a discesa. Seleziona <strong>Rendering </strong>dall’elenco, selezionare un rendering specifico da visualizzare in anteprima.</li>
      </ul> <p>Selezionando un rendering video a risoluzione più elevata per l'anteprima, il video potrebbe apparire troncato. Questo problema è dovuto al fatto che l’anteprima del rendering mostra la risoluzione esatta che i clienti vedranno tutti nel contesto del visualizzatore incorporato utilizzato per l’anteprima.</p> <p>Quando visualizzi l’anteprima di un set video adattivo a livello di risorsa, le rappresentazioni vengono raggruppate in un’unica esperienza di riproduzione. In altre parole, il video adattivo viene ridimensionato correttamente per la visualizzazione e la riproduzione utilizzando la migliore risoluzione nel contesto del dispositivo di visualizzazione e della velocità di connessione.<br /> </p> <p><strong>Per visualizzare in anteprima una risorsa in un particolare visualizzatore</strong></p>
      <ul>
      <li>Fai clic sull’icona nell’angolo in alto a sinistra della pagina per visualizzare l’elenco a discesa. Seleziona <strong>Visualizzatori</strong> dall’elenco, seleziona un visualizzatore da applicare alla risorsa.</li>
      </ul> </td>
      </tr>
      <tr>
      <td>Set immagini</td>
      <td>No</td>
      <td>Sì</td>
      <td><p><strong>Per visualizzare in anteprima una risorsa in un particolare visualizzatore</strong></p>
      <ul>
      <li>Fai clic sull’icona nell’angolo in alto a sinistra della pagina per visualizzare l’elenco a discesa. Seleziona <strong>Visualizzatori</strong> dall’elenco, seleziona un visualizzatore da applicare alla risorsa.</li>
      </ul> <p>Utilizza la <strong>+</strong> e <strong>-</strong> per aumentare o diminuire lo zoom dell'immagine selezionata. Seleziona <strong>Reimposta</strong> per ripristinare l'immagine allo zoom originale.<br /> Se ti trovi su uno schermo tattile, tocca due volte l’immagine per ingrandirla in base ai passaggi. Quando raggiungete lo zoom massimo, toccate nuovamente l’immagine per ripristinare lo stato di zoom. Trascina l’immagine per eseguire il panning.</p> </td>
      </tr>
      <tr>
      <td>Set 360 gradi</td>
      <td>No</td>
      <td>Sì</td>
      <td><p><strong>Per visualizzare in anteprima una risorsa in un particolare visualizzatore</strong></p>
      <ul>
      <li>Fai clic sull’icona nell’angolo in alto a sinistra della pagina per visualizzare l’elenco a discesa. Seleziona <strong>Visualizzatori</strong> dall’elenco, seleziona un visualizzatore da applicare alla risorsa.</li>
      </ul> <p>Utilizza la <strong>+</strong> e <strong>-</strong> per aumentare o diminuire lo zoom dell’immagine selezionata, rispettivamente. Seleziona <strong>Reimposta</strong> per ripristinare l'immagine allo zoom originale.<br /> Se ti trovi su uno schermo tattile, tocca due volte l’immagine per ingrandirla in base ai passaggi. Quando raggiungete lo zoom massimo, toccate nuovamente l’immagine per ripristinare lo stato di zoom. Trascina l’immagine per eseguire il panning.</p> </td>
      </tr>
      <tr>
      <td>Set di file multimediali diversi</td>
      <td>No</td>
      <td>Sì</td>
      <td><p><strong>Per visualizzare in anteprima una risorsa in un particolare visualizzatore</strong></p>
      <ul>
      <li>Fai clic sull’icona nell’angolo in alto a sinistra della pagina per visualizzare l’elenco a discesa. Seleziona <strong>Visualizzatori</strong> dall’elenco, seleziona un visualizzatore da applicare alla risorsa.</li>
      </ul> <p>Utilizza la <strong>+</strong> e <strong>-</strong> per aumentare o diminuire lo zoom dell’immagine selezionata, rispettivamente. Seleziona <strong>Reimposta</strong> per ripristinare l'immagine allo zoom originale.<br /> Se ti trovi su uno schermo tattile, tocca due volte l’immagine per ingrandirla in base ai passaggi. Quando raggiungete lo zoom massimo, toccate nuovamente l’immagine per ripristinare lo stato di zoom. Trascina l’immagine per eseguire il panning.</p> </td>
      </tr>
      <tr>
      <td>Set carosello</td>
      <td>No</td>
      <td>Sì</td>
      <td><strong>Per visualizzare in anteprima una risorsa in un particolare visualizzatore</strong>
      <ul>
      <li>Fai clic sull’icona nell’angolo in alto a sinistra della pagina per visualizzare l’elenco a discesa. Seleziona un visualizzatore da applicare alla risorsa.</li>
      </ul> </td>
      </tr>
      <tr>
      <td>Video a 360°<br /> </td>
      <td>Sì</td>
      <td>Sì</td>
      <td><p><strong>Visualizzazione in anteprima della risorsa in un rendering specifico</strong></p>
      <ul>
      <li>Nell’angolo in alto a sinistra della pagina, seleziona l’icona in modo che venga visualizzato l’elenco a discesa. Seleziona <strong>Rendering</strong>, quindi seleziona il rendering da visualizzare in anteprima.</li>
      </ul> <p><strong>Per visualizzare in anteprima la risorsa in un particolare visualizzatore</strong></p>
      <ul>
      <li>Nell’angolo in alto a sinistra della pagina, seleziona l’icona in modo che venga visualizzato l’elenco a discesa. Seleziona <strong>Visualizzatori</strong>, quindi seleziona un visualizzatore da applicare alla risorsa.</li>
      </ul> <p>Utilizza la <strong>+</strong> e <strong>-</strong> per aumentare o diminuire lo zoom dell’immagine selezionata, rispettivamente. Seleziona <strong>Reimposta</strong> per ripristinare l'immagine allo zoom originale.<br /> Se ti trovi su uno schermo tattile, tocca due volte l’immagine per ingrandirla in base ai passaggi. Quando raggiungete lo zoom massimo, toccate nuovamente l’immagine per ripristinare lo stato di zoom. Trascina l’immagine per eseguire il panning.</p> </td>
      </tr>
    </tbody>
    </table>

## Anteprima delle risorse tramite tastiera {#keyboard-navigation-asset-preview}

1. Dall’interfaccia utente di Assets, passa a una cartella contenente la risorsa da visualizzare in anteprima.

1. Nella cartella, premi il pulsante `<Tab>` per selezionare la risorsa, utilizza la tastiera o i tasti freccia.

1. Press `<Enter>` per aprire la risorsa selezionata in modalità Anteprima.

1. Effettua una delle operazioni seguenti:

   * Per ingrandire, premere `<Tab>` per spostare la messa a fuoco sull&#39;icona zoom in (+), quindi premere `<Enter>` una o più volte per ingrandire in modo incrementale.
   * Per ridurre lo zoom, premere `<Tab>` per spostare la messa a fuoco sull&#39;icona zoom out (-), quindi premere `<Enter>` una o più volte per ridurre gradualmente.
   * Per spostare la visualizzazione di un *ingrandito* premere i rispettivi tasti freccia in orizzontale o verticale.
   * Press `<Shift>` + `<Tab>` in modo da reimpostare la visualizzazione e riattivare la risorsa.
