---
title: Aggiungere proprietà personalizzate alle risorse di Gestione Corrispondenza
seo-title: Aggiungere proprietà personalizzate alle risorse di Gestione Corrispondenza
description: Scopri come aggiungere proprietà personalizzate alle risorse Gestione Corrispondenza.
seo-description: Scopri come aggiungere proprietà personalizzate alle risorse Gestione Corrispondenza.
uuid: 4716e181-d3ea-424b-9544-376cc649bce7
content-type: reference
topic-tags: correspondence-management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 79437b96-7b57-4581-b7e7-fcaedc3d05de
docset: aem65
feature: Correspondence Management
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '4462'
ht-degree: 4%

---


# Aggiungi proprietà personalizzate alle risorse di Gestione Corrispondenza{#add-custom-properties-to-correspondence-management-assets}

## Panoramica {#overview}

Puoi personalizzare l’interfaccia utente di Gestione Corrispondenza e presentare agli utenti un set personalizzato di proprietà e schede. Questa personalizzazione include l’aggiunta di campi/proprietà e schede personalizzati a tipi/lettere di risorse specifiche o a tutti i tipi e le lettere di risorse.

## Aggiunta di proprietà personalizzate alle risorse di Gestione Corrispondenza {#adding-custom-properties-to-correspondence-management-assets}

Gli scenari seguenti mostrano come aggiungere proprietà/schede alle risorse e alle lettere di Gestione Corrispondenza:

* Aggiunta di una proprietà comune a tutti i tipi di risorse
* Aggiunta di una scheda comune a tutti i tipi di risorse
* Aggiunta di proprietà personalizzate a tipi di risorse specifici

Modificando le proprietà, i percorsi e i valori in questi scenari, puoi aggiungere proprietà e schede personalizzate a un diverso set di risorse in base alle tue esigenze.

### Scenario: Aggiunta di un campo comune (proprietà) a tutti i tipi di risorse {#scenario-adding-a-common-field-property-to-all-the-asset-types}

In questo scenario viene illustrato come aggiungere una proprietà personalizzata a tutti i tipi di risorse (testo, elenco, condizione e frammenti di layout) e alle lettere. Utilizzando questo scenario, puoi aggiungere una proprietà, Posizione dei destinatari, a tutte le risorse e le lettere. La proprietà Posizione dei destinatari consente di identificare l’area geografica di consegna di una risorsa o di una lettera pertinente.

>[!NOTE]
>
>Se hai già aggiunto una proprietà personalizzata, la proprietà inizia a comparire nella pagina di creazione della risorsa. Per nascondere tale proprietà, consulta Visualizzare/nascondere proprietà personalizzate nelle pagine Creazione risorse e Proprietà .

![Proprietà personalizzata aggiunta a tutti i tipi di risorse](assets/lcoationofrecipientsui.png)

Per aggiungere una proprietà personalizzata a tutti i tipi di risorse e alle lettere, effettua le seguenti operazioni:

1. Vai a `https://'[server]:[port]'/[ContextPath]/crx/de` e accedi come amministratore.
1. Nella cartella delle app, crea una cartella denominata css con percorso/struttura simile alla cartella css (che si trova nella cartella ccrui) seguendo i passaggi seguenti:

   1. Fai clic con il pulsante destro del mouse sulla cartella degli elementi nel percorso seguente e seleziona **Sovrapponi nodo**:

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties/commonproperties/col1/items`

      ![nodo di sovrapposizione](assets/itemsoverlaynode.png)

   1. Assicurati che la finestra di dialogo Sovrapponi nodo abbia i seguenti valori:

      **Percorso:** /libs/fd/cm/ma/gui/content/cmmetadataproperties/commonproperties/col1/items

      **Posizione:** /apps/

      **Tipi di nodo di corrispondenza:** selezionati

      ![nodo di sovrapposizione](assets/cmmetapropertiesoverlaynode.png)

   1. Fai clic su **OK**. La struttura delle cartelle viene creata nella cartella delle app.

   1. Fare clic su **Salva tutto**.

1. Nella cartella degli elementi appena creati, aggiungi un nodo per la proprietà personalizzata in tutta la risorsa (Esempio: GeoLocation) con i seguenti passaggi:

   1. Fai clic con il pulsante destro del mouse sulla cartella degli elementi e seleziona **Crea** > **Crea nodo**.

      ![Crea nodo in CRX](assets/itemscreatenode.png)

   1. Assicurati che la finestra di dialogo Crea nodo abbia i seguenti valori e fai clic su **OK**:

      **Nome:** GeoLocation (o il nome che si desidera assegnare a questa proprietà)

      **Tipo:** nt:unstructured

      ![Crea nodo: GeoLocation](assets/geographicallocationcreatenode.png)

   1. Fai clic sul nuovo nodo creato (qui GeoLocation). CRX visualizza le proprietà del nodo.
   1. Aggiungi le seguenti proprietà al nodo (qui GeoLocation):

      | **Nome** | **Tipo** | **Valore** |
      |---|---|---|
      | fieldLabel | Stringa | Nome che si desidera assegnare al campo o alla proprietà. (Qui: Posizione dei destinatari) |
      | name | Stringa | `./extendedproperties/GeoLocation` (Mantieni lo stesso valore del nome campo creato sotto il nodo elementi) |
      | renderReadOnly | Booleano | vero |
      | sling:resourceType | Stringa | `granite/ui/components/coral/foundation/form/textfield` |

   1. Fare clic su **Salva tutto**.

1. Per visualizzare la personalizzazione, passa il puntatore del mouse su una risorsa (testo, elenco, condizione o frammento di layout) o su una lettera, fai clic su **Visualizza proprietà**, quindi fai clic su **Modifica**. Il nuovo campo (Posizione dei destinatari) viene visualizzato nella scheda Base delle proprietà della risorsa/lettera.

   >[!NOTE]
   >
   >Potrebbe essere necessario cancellare la cache del browser prima che la personalizzazione appaia nell’interfaccia utente.

   ![Proprietà personalizzata aggiunta a tutte le risorse](assets/lcoationofrecipientsui-1.png)

   >[!NOTE]
   >
   >Le proprietà comuni per tutte le risorse aggiunte vengono visualizzate nella scheda di base delle proprietà della risorsa. Per impostazione predefinita, le proprietà comuni aggiunte per tutte le risorse vengono visualizzate nella pagina delle proprietà e nella pagina di creazione delle risorse. Per nascondere le proprietà comuni, è necessario <!--link to show / hide properties]-->.

### Scenario: Aggiungi valori e menu a discesa personalizzati a una proprietà/campo personalizzato {#scenario-add-custom-drop-down-and-values-to-a-custom-property-field}

Questo scenario mostra come aggiungere una proprietà personalizzata a tutti i tipi di risorse e valori a discesa.

1. Fai clic con il pulsante destro del mouse sulla cartella degli elementi nel percorso seguente e seleziona **Sovrapponi nodo**:

   `/libs/fd/cm/ma/gui/content/cmmetadataproperties/commonproperties/col1/items`

1. Sotto il nodo di sovrapposizione appena creato (/apps/fd/cm/ma/gui/content/cmmetadataproperties/commonproperties/col1/items)
Crea un nodo per ciascuna delle proprietà (campi) per le quali devi creare un elenco a discesa (qui `geographicallocation`) del tipo nt:unstructured.
1. Aggiungi le seguenti proprietà al nodo (qui geografia, allocazione) e fai clic su **Salva tutto**:

   <table>
   <tbody>
   <tr>
      <td><strong>Nome</strong></td>
      <td><strong>Tipo</strong></td>
      <td><strong>Valore</strong></td>
   </tr>
   <tr>
      <td>fieldLabel</td>
      <td>Stringa</td>
      <td>Nome che si desidera assegnare al campo o alla proprietà. (Qui: geografia)</td>
   </tr>
   <tr>
      <td>name</td>
      <td>Stringa</td>
      <td>./extension dedproperties/geographicallocation (Mantieni il valore uguale al nome del campo creato sotto il nodo items)</td>
   </tr>
   <tr>
      <td>renderReadOnly</td>
      <td>Booleano</td>
      <td>vero</td>
   </tr>
   <tr>
      <td>sling:resourceType</td>
      <td>Stringa</td>
      <td>granite/ui/components/coral/foundation/form/select<br /> </td>
   </tr>
   </tbody>
   </table>

1. Sotto il nodo di proprietà (qui geografia, allocazione), aggiungi un nuovo nodo con nome `items`. Sotto il nodo elementi, aggiungi un nodo ciascuno per i valori nel menu a discesa. Come procedura ottimale, aggiungi il primo nodo come vuoto da utilizzare come valore predefinito del menu a discesa e un’opzione che consente all’utente di non specificare alcun valore per il campo. Per aggiungere più opzioni/valori a discesa, ripeti i seguenti passaggi:

   1. Fai clic con il pulsante destro del mouse sul nodo della proprietà (in questo caso, geografia, allocazione) e seleziona **Crea** > **Crea nodo**.
   1. Immetti il nome del campo come `item1,` mantieni il tipo come nt:unstructured e fai clic su **OK**.
   1. Aggiungi le seguenti proprietà al nodo appena creato (qui elemento1), quindi fai clic su **Salva tutto**:

      <table>
         <tbody>
         <tr>
          <td><strong>Nome</strong></td>
          <td><strong>Tipo</strong></td>
          <td><strong>Valore</strong></td>
         </tr>
         <tr>
          <td>testo</td>
          <td>Stringa</td>
          <td>Valore dell’opzione a discesa visibile all’utente. Lascialo vuoto per il valore vuoto (predefinito) o inserisci il valore, ad esempio <strong>Internazionale</strong> o <strong>Entro US</strong>.<br /> </td>
         </tr>
         <tr>
          <td>valore</td>
          <td>Stringa</td>
          <td>Valore memorizzato in CRXDE per il testo. Immetti una parola chiave univoca. <br /> </td>
         </tr>
         </tbody>
   </table>

   ![customizationdropdownvalues escrxde](assets/customizationdropdownvaluescrxde.png)

Il menu a discesa personalizzato viene visualizzato come segue nelle proprietà della risorsa:

![drop-down_customization](assets/drop-down_customization.png)

### Scenario: Scheda comune per tutti i tipi di risorse {#scenario-common-tab-for-all-asset-types}

Questo scenario mostra come aggiungere una scheda personalizzata, Destinatari, a tutti i tipi di risorse (frammenti di testo, elenco, condizione e layout) e alle lettere. La scheda Destinatari consente di pianificare l’inserimento di tutte le proprietà personalizzate pertinenti ai destinatari.

![È stata aggiunta una scheda personalizzata per tutti i tipi di risorse](assets/recipientstab.png)

Utilizzando la procedura seguente, puoi aggiungere una scheda con un campo a tutte le risorse:

1. Vai a `https://'[server]:[port]'/[ContextPath]/crx/de` e accedi come amministratore.
1. Nella cartella delle app, crea una cartella denominata cmmetadataproperties con percorso/struttura simile alla cartella cmmetadataproperties (che si trova nella cartella del contenuto) seguendo i passaggi seguenti:

   1. Fai clic con il pulsante destro del mouse sulla cartella cmmetadataproperties al seguente percorso e seleziona **Sovrapponi nodo**:

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties`

      ![nodo di sovrapposizione](assets/cmmetadatapropertiesoverlaynode.png)

   1. Assicurati che la finestra di dialogo Sovrapponi nodo abbia i seguenti valori:

      **Percorso:** /libs/fd/cm/ma/gui/content/cmmetadataproperties

      **Posizione:** /apps/

      **Tipi di nodo di corrispondenza:** selezionati

   1. Fai clic su **OK**. La struttura delle cartelle viene creata nella cartella delle app.

      ![Sovrapponi la struttura della cartella creata in CRX](assets/cmmetadatapropertiesappsfolder.png)

      Fare clic su **Salva tutto**.

1. Nella cartella delle proprietà dei metadati , aggiungi un nodo per creare una scheda personalizzata per tutte le risorse (Esempio: commontab) utilizzando i seguenti passaggi:

   1. Fai clic con il pulsante destro del mouse sulla cartella delle proprietà dei metadati e seleziona **Crea** > **Crea nodo**.

      ![Crea nodo](assets/cmmetadatapropertiescreatenode.png)

   1. Assicurati che la finestra di dialogo Crea nodo abbia i seguenti valori e fai clic su **OK**:

      **Nome:** commontab (o il nome che si desidera assegnare a questa proprietà)

      **Tipo:** nt:unstructured

   1. Fare clic sul nuovo nodo creato (qui commontab). CRX visualizza le proprietà del nodo.
   1. Aggiungi le seguenti proprietà al nodo (qui commontab):

      <table>
         <tbody>
         <tr>
          <td><strong>Nome</strong></td>
          <td><strong>Tipo</strong></td>
          <td><strong>Valore</strong></td>
         </tr>
         <tr>
          <td>jcr:title</td>
          <td>Stringa</td>
          <td>Nome da assegnare alla colonna. (Qui: Destinatari)</td>
         </tr>
         <tr>
          <td>sling:resourceType</td>
          <td>Stringa</td>
          <td>granite/ui/components/coral/foundation/container<br /> </td>
   </tr>
         </tbody>
       </table>

   1. Fare clic su **Salva tutto**.

1. Per il nodo tabulazione creato nell&#39;ultimo passaggio (qui commontab), crea un nodo chiamato elemento utilizzando il seguente passaggio:

   1. Fai clic con il pulsante destro del mouse sul nodo pertinente (qui commontab) e seleziona **Crea** > **Crea nodo**.
   1. Assicurati che la finestra di dialogo Crea nodo abbia i seguenti valori e fai clic su **OK**:

      **Nome:** elementi

      **Tipo:** nt:unstructured

   1. Fare clic su **Salva tutto:**

1. Nel nodo elementi creato nel passaggio precedente (in commontab), aggiungi un nodo per la creazione di una colonna (qui Colonna1) nella scheda personalizzata (commontab) seguendo i passaggi seguenti (per aggiungere altre colonne, ripeti questo passaggio):

   1. Fai clic con il pulsante destro del mouse sul nodo elementi e seleziona **Crea** > **Crea nodo**.
   1. Assicurati che la finestra di dialogo Crea nodo abbia i seguenti valori e fai clic su **OK**:

      **Nome:** Colonna1 (o il nome che si desidera assegnare al nodo - questo nome non viene visualizzato nell&#39;interfaccia utente).

      **Tipo:** nt:unstructured

   1. Aggiungi la seguente proprietà al nodo (Qui Colonna1), quindi fai clic su **Salva tutto**:

      <table>
         <tbody>
         <tr>
           <td><strong>Nome</strong></td>
           <td><strong>Tipo</strong></td>
           <td><strong>Valore</strong></td>
         </tr>
         <tr>
           <td>sling:resourceType</td>
           <td>Stringa</td>
           <td>granite/ui/components/coral/foundation/container<br /> </td>
         </tr>
         </tbody>
       </table>

1. Nel nodo creato nel passaggio precedente (qui Colonna1), aggiungi un nodo denominato elementi utilizzando i seguenti passaggi:

   1. Fai clic con il pulsante destro del mouse sul nodo (qui Colonna1) e seleziona **Crea** > **Crea nodo**.
   1. Assicurati che la finestra di dialogo Crea nodo abbia i seguenti valori e fai clic su **OK**:

      **Nome:** elementi

      **Tipo:** nt:unstructured

   1. Fare clic su **Salva tutto**.

1. Per creare un campo nella scheda personalizzata (in questo caso Destinatari), aggiungi un nodo (in questo caso Posizione geografica). Questa proprietà corrisponde alla colonna creata. Utilizza i seguenti passaggi per creare il campo (per creare altri campi/nodi, ripeti questi passaggi).:

   1. Fai clic con il pulsante destro del mouse sul nodo elementi e seleziona **Crea** > **Crea nodo**.
   1. Assicurati che la finestra di dialogo Crea nodo abbia i seguenti valori e fai clic su **OK**:

      **Nome:** GeographicLocation (o un altro nome per la proprietà del campo)

      **Tipo:** nt:unstructured

   1. Aggiungi le seguenti proprietà al nodo del campo (qui GeographicLocation) e fai clic su **Salva tutto**.

      | **Nome** | **Tipo** | **Valore** |
      |---|---|---|
      | fieldLabel | Stringa | Posizione dei destinatari (o nome a cui assegnare il campo). |
      | name | Stringa | ./extensionsproperties/GeographicLocation |
      | renderReadOnly | Booleano | vero |
      | sling:resourceType | Stringa | `/libs/granite/ui/components/coral/foundation/form/textfield` |

1. Per aggiungere questa scheda per Lettere, crea una cartella di sovrapposizione con percorso/struttura simile alla cartella degli elementi riportata di seguito nel seguente percorso:

   `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/letter/items/tabs/items`

   Per creare sovrapposizione per una lettera o una risorsa diversa utilizza il seguente percorso sostituendo [assettype] con testo, condizione, elenco, dizionario dati o frammento:

   `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/[assettype]/items/tabs/items`

   1. Fai clic con il pulsante destro del mouse sulla cartella degli elementi nel percorso seguente e seleziona **Sovrapponi nodo**:

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/letter/items/tabs/items`

   1. Assicurati che la finestra di dialogo Sovrapponi nodo abbia i seguenti valori:

      **Percorso:** `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/letter/items/tabs/items`

      **Posizione:** /apps/

      **Tipi di nodo di corrispondenza:** selezionati

   1. Fai clic su **OK**. La cartella viene creata. Fare clic su **Salva tutto**.

1. Nella cartella degli elementi appena creati, aggiungi un nodo per la scheda personalizzata nella risorsa (in questo caso mytab - questo nome non viene visualizzato nell’interfaccia utente) seguendo i seguenti passaggi:

   1. Fai clic con il pulsante destro del mouse sulla cartella degli elementi e seleziona **Crea** > **Crea nodo**.
   1. Assicurati che la finestra di dialogo Crea nodo abbia i seguenti valori e fai clic su **OK**:

      **Nome:** mytab (o il nome che si desidera assegnare a questa proprietà)

      **Tipo:** nt:unstructured

   1. Fai clic sul nuovo nodo creato (qui mytab). CRX visualizza le proprietà del nodo.
   1. Aggiungi le due seguenti proprietà al nodo (qui customtab):

      <table>
         <tbody>
         <tr>
           <td><strong>Nome</strong></td>
           <td><strong>Tipo</strong></td>
           <td><strong>Valore</strong></td>
         </tr>
         <tr>
           <td>path<br /> </td>
           <td>Stringa</td>
           <td>fd/cm/ma/gui/content/cmmetadataproperties/commontab<br /> </td>
         </tr>
         <tr>
           <td>sling:resourceType</td>
           <td>Stringa</td>
           <td>granite/ui/components/coral/foundation/include<br /> </td>
         </tr>
         </tbody>
       </table>

   1. Fare clic su **Salva tutto**.

1. Per visualizzare la personalizzazione, passa il puntatore del mouse sulla risorsa pertinente (qui una lettera), fai clic su Visualizza proprietà e fai clic su **Modifica**. La nuova scheda (Destinatari) e il nuovo campo (Posizione dei destinatari) vengono visualizzati nell’interfaccia utente.

   >[!NOTE]
   >
   >Potrebbe essere necessario cancellare la cache del browser prima che la personalizzazione appaia nell’interfaccia utente.

   ![Scheda personalizzata aggiunta alle lettere](assets/recipientstab-1.png)

### Scenario: Aggiunta di proprietà personalizzate per tipi di risorse specifici {#scenario-adding-custom-properties-for-specific-asset-types}

Questo scenario mostra come aggiungere una proprietà a un particolare tipo di risorsa, ad esempio un campo a tutte le risorse di testo. Utilizzando questo processo, puoi aggiungere proprietà a una delle seguenti operazioni:

* Testo
* Condizione
* Elenco
* Frammento layout
* Dizionario dati
* Lettera

Ad esempio, solo per le risorse di testo, vuoi aggiungere una proprietà, Posizione dei destinatari, per identificare l’area geografica di una risorsa pertinente.  ![Proprietà personalizzata aggiunta a una risorsa](assets/newtabui.png)

Per aggiungere una proprietà a un tipo di risorsa, completa i passaggi seguenti:

1. Vai a `https://'[server]:[port]'/[ContextPath]/crx/de` e accedi come amministratore.
1. Per creare una scheda in un tipo di risorsa (ad esempio Testo), crea la seguente struttura di cartelle nella cartella delle app:

   `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/[AssetType]/items/tabs/items`

   [AssetType]  = testo, condizione, elenco, lettera, dizionario dati o frammento

   Di seguito sono riportati i passaggi per creare questa struttura di cartelle:

   1. Fai clic con il pulsante destro del mouse sulla cartella degli elementi nel percorso seguente e seleziona **Sovrapponi nodo**:

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/[AssetType]/items/tabs/items`

      Ad esempio, se desideri creare una proprietà per le risorse di testo, seleziona la cartella seguente:

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/text/items/tabs/items`

      ![nodo di sovrapposizione](assets/textitemstabsitemsoverlaynode1.png)

   1. Assicurati che la finestra di dialogo Sovrapponi nodo abbia i seguenti valori:

      **Percorso:** /libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/[AssetType]/items/tabs/items

      **Posizione:** /apps/

      **Tipi di nodo di corrispondenza:** selezionati

   1. Fai clic su **OK**. La struttura delle cartelle viene creata nella cartella delle app.

      Fare clic su **Salva tutto**.

1. Nella cartella degli elementi appena creati, aggiungi un nodo per la scheda personalizzata nella risorsa (Esempio: customtab) seguendo i seguenti passaggi:

   1. Fai clic con il pulsante destro del mouse sulla cartella degli elementi e seleziona **Crea** > **Crea nodo**.
   1. Assicurati che la finestra di dialogo Crea nodo abbia i seguenti valori e fai clic su **OK**:

      **Nome:** customtab (o il nome che si desidera assegnare a questa proprietà)

      **Tipo:** nt:unstructured

   1. Fai clic sul nuovo nodo creato (qui customtab). CRX visualizza le proprietà del nodo.
   1. Aggiungi le due seguenti proprietà al nodo (qui customtab):

      | **Nome** | **Tipo** | **Valore** |
      |---|---|---|
      | sling:resourceType | Stringa | granite/ui/components/coral/foundation/container |
      | jcr:title | Stringa | Nome del campo nell’interfaccia utente (in questa scheda) |

   1. Fare clic su **Salva tutto**.

1. Nel nodo creato nel passaggio precedente (qui customtab), aggiungi un nodo denominato items utilizzando i seguenti passaggi:

   1. Fai clic con il pulsante destro del mouse sul nodo (qui customtab) e seleziona **Crea** > **Crea nodo**.
   1. Assicurati che la finestra di dialogo Crea nodo abbia i seguenti valori e fai clic su **OK**:

      **Nome:** elementi

      **Tipo:** nt:unstructured

   1. Fare clic su **Salva tutto**.

1. Nel nodo elementi creato nel passaggio precedente (in customtab), aggiungi un nodo per la creazione di una colonna (qui Colonna1) nella scheda personalizzata seguendo i passaggi seguenti (per aggiungere altre colonne, ripeti questo passaggio):

   1. Fai clic con il pulsante destro del mouse sul nodo elementi e seleziona **Crea** > **Crea nodo**.
   1. Assicurati che la finestra di dialogo Crea nodo abbia i seguenti valori e fai clic su **OK**:

      **Nome:** Colonna1 (o il nome che si desidera assegnare al nodo)

      **Tipo:** nt:unstructured

   1. Aggiungi la seguente proprietà al nodo (Qui Colonna1), quindi fai clic su **Salva tutto**.

      <table>
         <tbody>
         <tr>
           <td><strong>Nome</strong></td>
           <td><strong>Tipo</strong></td>
           <td><strong>Valore</strong></td>
         </tr>
         <tr>
           <td>sling:resourceType</td>
           <td>Stringa</td>
           <td>granite/ui/components/coral/foundation/container<br /> </td>
         </tr>
         </tbody>
       </table>

1. Per ogni colonna creata (come specificato nel passaggio precedente - qui Colonna1), crea un nodo denominato elemento seguendo i passaggi seguenti:

   1. Fai clic con il pulsante destro del mouse sul nodo della colonna pertinente (qui Colonna1) e seleziona **Crea** > **Crea nodo**.
   1. Assicurati che la finestra di dialogo Crea nodo abbia i seguenti valori e fai clic su **OK**:

      **Nome:** elementi

      **Tipo:** nt:unstructured

   1. Fare clic su **Salva tutto:**

1. Per ciascuna delle colonne create, crea un nodo sotto il nodo elementi per creare un campo nella nuova scheda nell’interfaccia utente. Ripeti questo passaggio per creare altri campi nella colonna:

   1. Fai clic con il pulsante destro del mouse sul nodo pertinente (qui elementi sotto Colonna1) e seleziona **Crea** > **Crea nodo**.
   1. Assicurati che la finestra di dialogo Crea nodo abbia i seguenti valori e fai clic su **OK**:

      **Nome:** un nome a scelta (qui GeoLocation)

      **Tipo:** nt:unstructured

   1. Aggiungi le seguenti proprietà al nodo e fai clic su **Salva tutto**.

      | **Nome** | **Tipo** | **Valore** |
      |---|---|---|
      | fieldLabel | Stringa | Posizione dei destinatari (o nome a cui assegnare il campo). |
      | name | Stringa | `./extendedproperties/GeoLocation` |
      | renderReadOnly | Booleano | vero |
      | sling:resourceType | Stringa | granite/ui/components/coral/foundation/form/textfield |

1. Per visualizzare la personalizzazione, passa il puntatore del mouse sulla risorsa in questione (qui testo), fai clic su Visualizza proprietà e fai clic su **Modifica**. La nuova scheda e il nuovo campo (Posizione dei destinatari) vengono visualizzati nell’interfaccia utente.

   >[!NOTE]
   >
   >Potrebbe essere necessario cancellare la cache del browser prima che la personalizzazione appaia nell’interfaccia utente.

   ![Proprietà personalizzata aggiunta a una risorsa specifica](assets/newtabui-1.png)

### Visualizza le proprietà personalizzate nella pagina di creazione delle risorse {#display-custom-properties-on-the-asset-creation-page}

Per impostazione predefinita, le proprietà personalizzate aggiunte alle nuove schede sono visibili solo nella pagina delle proprietà e non nella pagina di creazione della risorsa, in quanto la pagina di creazione della risorsa non ha layout a schede. Per visualizzare le proprietà personalizzate nella pagina di creazione della risorsa insieme ad altre proprietà, è necessario effettuare le seguenti operazioni:

1. Fai clic con il pulsante destro del mouse sulla cartella degli elementi nel percorso seguente e seleziona **Sovrapponi nodo**:

   `/libs/fd/cm/ma/gui/content/createasset/createletter/jcr:content/body/items/form/items/letterWizard/items/properties/items/properties/items/letterproperties/items`

1. Assicurati che la finestra di dialogo Sovrapponi nodo abbia i seguenti valori, per lettera. Per altri tipi di risorse, il percorso è indicato nella tabella seguente:

   **Percorso:** /libs/fd/cm/ma/gui/content/createasset/createletter/jcr:content/body/items/form/items/letterWizard/items/properties/items/properties/items/letterproperties/items

   **Posizione:** /apps/

   **Tipi di nodo di corrispondenza:** selezionati

   A seconda del tipo di risorsa, il percorso deve essere il seguente:

   | **Tipo di risorsa/documento** | **Percorso da aggiungere** |
   |---|---|
   | Testo | /libs/fd/cm/ma/gui/content/createasset/createtext/jcr:content/body/items/form/items/textwWizard/items/editproperties/items/properties/items/tabs/items/tab1/items |
   | Elenco | /libs/fd/cm/ma/gui/content/createasset/createlist/jcr:content/body/items/form/items/listWizard/items/editproperties/items/properties/items/tabs/items/tab1/items |
   | Condizione | /libs/fd/cm/ma/gui/content/createasset/createcondizione/jcr:content/body/items/form/items/condition/Wizard/items/editproperties/items/items/tabs/items/tab1/items |
   | Frammento | /libs/fd/cm/ma/gui/content/createasset/createfragment/jcr:content/body/items/form/items/fragmentWizard/items/properties/items/properties/items/tabs2/items/tab1/items |
   | Lettera | /libs/fd/cm/ma/gui/content/createasset/createletter/jcr:content/body/items/form/items/letterWizard/items/properties/items/properties/items/letterproperties/items |

1. Fai clic su **OK**. La struttura delle cartelle viene creata nella cartella delle app.

1. Sotto il nodo degli elementi di sovrapposizione creato, crea un nodo del nome col4 (o qualsiasi altro nome) e fai clic su **Salva tutto**.

   Di seguito, ad esempio, il nodo di sovrapposizione creato per le lettere.

   `/apps/fd/cm/ma/gui/content/createasset/createletter/jcr:content/body/items/form/items/letterWizard/items/properties/items/properties/items/letterproperties/items`

1. Aggiungi le seguenti proprietà al nodo appena creato (qui col4) e fai clic su **Salva tutto**:

<table>
 <tbody>
  <tr>
   <td><strong>Nome</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Valore</strong></td>
  </tr>
  <tr>
   <td>path</td>
   <td>Stringa</td>
   <td><p>Questo percorso è il puntatore della colonna creata in:</p>
    <ul>
     <li>Per la scheda comune per tutti i tipi di risorse: /apps/fd/cm/ma/gui/content/cmmetadataproperties/commontab/items/col1</li>
     <li>Per proprietà diverse per diversi tipi di risorse: /apps/fd/cm/ma/gui/content/cmmetadataproperties/properties//items/tabs/items/customtab/items/col1</li>
    </ul> </td>
  </tr>
  <tr>
   <td>sling:resourceType</td>
   <td>Stringa</td>
   <td> granite/ui/components/coral/foundation/include<br /> </td>
  </tr>
 </tbody>
</table>

![customfieldappearinsitoproprietà](assets/customfieldappearinginmainproperties.png)

Proprietà personalizzata, Lingua, visualizzata nell&#39;interfaccia utente per la creazione di una lettera

## Personalizzare la vista a elenco per visualizzare le proprietà personalizzate {#customize-the-list-view-to-show-custom-properties}

Dopo aver aggiunto una proprietà personalizzata alle risorse di Gestione Corrispondenza, devi apportare ulteriori modifiche in CRX/DE per assicurarti che la proprietà personalizzata sia visualizzata nell’interfaccia utente di Gestione Corrispondenza.

Completa i seguenti passaggi per visualizzare la proprietà personalizzata nell’interfaccia utente dell’elenco delle risorse di Gestione Corrispondenza:

1. Vai a `https://'[server]:[port]'/[ContextPath]/crx/de` e accedi come amministratore.
1. Crea la seguente struttura di cartelle nella cartella delle app:

   `/libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/lists/columns`

   Di seguito sono riportati i passaggi per creare questa struttura di cartelle:

   1. Fai clic con il pulsante destro del mouse sulla cartella delle colonne nel percorso seguente e seleziona **Sovrapponi nodo**:

      `/libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/lists/columns`

   1. Assicurati che la finestra di dialogo Sovrapponi nodo abbia i seguenti valori:

      **Percorso:** /libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/lists/columns

      **Posizione:** /apps/

      **Tipi di nodo di corrispondenza:** selezionati

   1. Fai clic su **OK**. La struttura delle cartelle viene creata nella cartella delle app.

      Fare clic su **Salva tutto**.

1. Per ciascuna delle proprietà create, crea un nodo sotto il nodo delle colonne per creare una colonna nell&#39;interfaccia utente. Ripeti questo passaggio per creare altre colonne nell’interfaccia utente:

   1. Fai clic con il pulsante destro del mouse sul nodo (colonne) pertinente e seleziona **Crea** > **Crea nodo**.
   1. Assicurati che la finestra di dialogo Crea nodo abbia i seguenti valori e fai clic su **OK**:

      **Nome:** un nome a tua scelta (qui GeographicLocation)

      **Tipo:** nt:unstructured

   1. Aggiungi le seguenti proprietà al nodo e fai clic su **Salva tutto**.

      <table>
         <tbody>
         <tr>
           <td><strong>Nome</strong></td>
           <td><strong>Tipo</strong></td>
           <td><strong>Valore</strong></td>
         </tr>
         <tr>
           <td>jcr:primaryType</td>
           <td>Nome</td>
           <td><p>nt:unstructured</p> </td>
         </tr>
         <tr>
           <td>jcr:title</td>
           <td>Stringa</td>
           <td><p>Posizione geografica</p> <p>Questo valore viene visualizzato come intestazione di colonna nell’interfaccia utente. </p> </td>
         </tr>
         <tr>
           <td>ordinabile</td>
           <td>Booleano</td>
           <td><p>vero</p> <p>Un valore true indica che l’utente può ordinare i valori in questa colonna. </p> </td>
         </tr>
         </tbody>
       </table>

1. Crea la seguente struttura di cartelle nella cartella delle app:

   `/libs/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage`

   Di seguito sono riportati i passaggi per creare questa struttura di cartelle:

   1. Fai clic con il pulsante destro del mouse sulla cartella delle colonne nel percorso seguente e seleziona **Sovrapponi nodo**:

      `/libs/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage`

   1. Assicurati che la finestra di dialogo Sovrapponi nodo abbia i seguenti valori:

      **Percorso:** /libs/fd/cm/ma/gui/components/admin/infagerenderer/infellistpage

      **Posizione:** /apps/

      **Tipi di nodo di corrispondenza:** selezionati

   1. Fai clic su **OK**. La struttura delle cartelle viene creata nella cartella delle app.

      Fare clic su **Salva tutto**.

1. Copia il file inflistpage.jsp dal seguente percorso:

   /libs/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage/childlistpage.jsp

   Incolla il file nel percorso seguente:

   /apps//fd/cm/ma/gui/components/admin/child pagerenderer/inflistpage/.

1. Apri il file inflistpage.jsp (/apps/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage/childlistpage.jsp) e apporta le seguenti modifiche:

   1. Aggiungi quanto segue alla riga 19 del file (seguendo l&#39;istruzione di copyright).

      ```jsp
      <%@page import="java.util.Map"%>
      ```

   1. Aggiungi il seguente codice di una funzione che ottiene il valore per ogni proprietà personalizzata alla fine del file:

      ```jsp
      <%!
          private String getCustomPropertyValue(Map<String, Object> extendedProperties, String propertyName) {
      
              String propertyValue = "";
              if (extendedProperties.containsKey(propertyName)) {
                  propertyValue = (String) extendedProperties.get(propertyName);
              }
      
              return propertyValue;
          }
      %>
      ```

   1. Aggiungi quanto segue prima dell&#39;inizio del tag &lt;tr> (&lt;tr &lt;%= attrs.build() %>>):

      ```jsp
      <%
          String GeoLocation = "";
          if (asset != null) {
                  Map<String, Object> extendedProperties = asset.getExtendedProperties();
                  if (extendedProperties != null) {
                      GeoLocation = getCustomPropertyValue(extendedProperties,"GeoLocation");
                  }
          }
      %>
      ```

      Nel codice, GeoLocation è il valore impostato nella proprietà name durante la creazione del nodo/campo personalizzato. Durante la creazione di un nodo/campo personalizzato, hai specificato il nome della proprietà con ./extension dedproperties/ prefisso: ./extensionsproperties/GeoLocation. Nel codice, il prefisso non è obbligatorio.

   1. Per visualizzare la nuova proprietà nell&#39;interfaccia utente, aggiungi un tag TD come segue prima del tag di chiusura tr (&lt;/tr>):

      ```jsp
      <td is="coral-td" value="<%= xssAPI.encodeForHTMLAttr(geographicalLocation) %>"><%= xssAPI.encodeForHTML(geographicalLocation) %></td>
      ```

      Per aggiungere altre colonne, ripeti i passaggi 6.3 e 6.4.

   1. Fare clic su **Salva tutto**.

1. Per visualizzare la personalizzazione, aprire la visualizzazione a elenco dei frammenti di documento o delle lettere in cui è stata aggiunta la proprietà personalizzata.

   La colonna e la proprietà dell’interfaccia utente aggiunte in questa procedura vengono visualizzate per tutti i tipi di risorse. Tuttavia, i valori contenuti in queste proprietà possono essere immessi e visualizzati solo per i tipi di risorse per i quali è stata originariamente aggiunta la proprietà personalizzata.

   Ad esempio, utilizzando lo Scenario: Aggiungendo proprietà personalizzate per tipi di risorse specifici si aggiunge una proprietà personalizzata alle risorse di testo, è possibile immettere proprietà personalizzate solo per le risorse di testo. Tuttavia, se visualizzi tale proprietà personalizzata nell’interfaccia utente, la colonna viene visualizzata per tutti i tipi di risorse.

   ![custompropertyinlistview](assets/custompropertyinlistview.png)

1. (Facoltativo) Per impostazione predefinita, la nuova colonna viene visualizzata come ultima colonna dell’interfaccia utente. Per visualizzare la colonna in una posizione specifica, aggiungi la seguente proprietà al nodo della colonna:

<table>
 <tbody>
  <tr>
   <td><strong>Nome</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Valore</strong></td>
  </tr>
  <tr>
   <td>sling:orderBefore</td>
   <td>Stringa</td>
   <td><p>Il nome del nodo della colonna nel percorso "/libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/list/columns" prima del quale la colonna personalizzata deve essere visualizzata nell'interfaccia utente.</p> <p>In questo caso, se desideri che la colonna Posizione geografica sia visualizzata prima (a sinistra) della colonna Versione, aggiungi la proprietà sling:orderBefore al nodo GeoLocation nel percorso ""/apps/fd/cm/ma/gui/content/cmassets/jcr:content/views/list/columns/GeoLocation" e imposta il valore della proprietà sulla versione.</p> </td>
  </tr>
 </tbody>
</table>

Quando si aggiunge la proprietà sling:orderBefore per specificare la posizione della colonna, è necessario aggiornare anche l&#39;ordine del tag &lt;td> corrispondente specificato nel passaggio 6.4 di questa procedura. Ad esempio, in questo caso, è necessario assicurarsi che il tag &lt;td> della posizione geografica sia posizionato prima del tag &lt;td> della colonna Versione :

```xml
<td is="coral-td" value="<%= xssAPI.encodeForHTMLAttr(geographicalLocation) %>"><%= xssAPI.encodeForHTML(geographicalLocation) %></td>
<td is="coral-td" value="<%= xssAPI.encodeForHTMLAttr(version) %>"><%= xssAPI.encodeForHTML(version) %></td>
```

## Abilita la ricerca di proprietà personalizzate {#enable-search-for-custom-properties}

Per impostazione predefinita, la ricerca full text non include proprietà personalizzate aggiunte all’interfaccia utente utilizzando CRX/DE.

Per includere le proprietà personalizzate nella ricerca, devi consentire l’indicizzazione delle proprietà personalizzate.

Per consentire l’indicizzazione delle proprietà personalizzate, completa i passaggi seguenti:

1. Vai a `https://'[server]:[port]'/[ContextPath]/crx/de` e accedi come amministratore.
1. Vai a `/oak:index/cmLucene`e aggiungi sotto di esso un nodo denominato **aggregates**.

   1. Fai clic con il pulsante destro del mouse sulla cartella cmLucene e seleziona **Crea** > **Crea nodo**.
   1. Assicurati che la finestra di dialogo Crea nodo abbia i seguenti valori e fai clic su **OK**:

      **Nome:** aggregati

      **Tipo:** nt:unstructured

   1. Fare clic su **Salva tutto**.

1. Nella cartella aggregazioni appena creata, aggiungi un nodo cm:resource. E sotto cm:resource, aggiungi un nodo chiamato include0.

   1. Fai clic con il pulsante destro del mouse sulla cartella aggregates e seleziona **Crea** > **Crea nodo**. Assicurati che la finestra di dialogo Crea nodo abbia i seguenti valori e fai clic su **OK**:

      **Nome:** cm:resource

      **Tipo:** nt:unstructured

   1. Fai clic con il pulsante destro del mouse sulla cartella cm:resource e seleziona **Crea** > **Crea nodo**. Assicurati che la finestra di dialogo Crea nodo abbia i seguenti valori e fai clic su **OK**:

      **Nome:** include0

      **Tipo:** nt:unstructured

   1. Fai clic sul nuovo nodo creato (qui include0). CRX visualizza le proprietà del nodo.
   1. Aggiungi la seguente proprietà al nodo (qui include0):

      <table>
         <tbody>
         <tr>
           <td><strong>Nome</strong></td>
           <td><strong>Tipo</strong></td>
           <td><strong>Valore</strong></td>
         </tr>
         <tr>
           <td>path</td>
           <td>Stringa</td>
           <td>ExtendedProperties<br /> </td>
         </tr>
         </tbody>
       </table>

   1. Fare clic su **Salva tutto**.

1. Vai a proprietà nella posizione seguente e aggiungi una posizione del nodo sotto di esso: `/oak:index/cmLucene/indexRules/cm:resource/properties`

   Ripeti questo passaggio per ciascuna delle proprietà personalizzate che desideri aggiungere alla ricerca.

   1. Fai clic con il pulsante destro del mouse sulla cartella delle proprietà e seleziona **Crea** > **Crea nodo**.
   1. Assicurati che la finestra di dialogo Crea nodo abbia i seguenti valori e fai clic su **OK**:

      **Nome:** posizione (o il nome della proprietà personalizzata che desideri aggiungere alla ricerca)

      **Tipo:** nt:unstructured

   1. Fai clic sul nuovo nodo creato (qui posizione). CRX visualizza le proprietà del nodo.
   1. Aggiungi le seguenti proprietà al nodo (qui posizione):

      | **Nome** | **Tipo** | **Valore** |
      |---|---|---|
      | analizzato | Stringa | vero |
      | name | Stringa | ExtendedProperties/location (o il nome della proprietà che desideri aggiungere alla ricerca) |
      | propertyIndex | Booleano | vero |
      | useInSuggest | Booleano | vero |

   1. Fare clic su **Salva tutto**.

1. Ora puoi utilizzare i valori delle proprietà personalizzate nella ricerca full text per individuare le risorse rilevanti.

>[!NOTE]
>
>Se non riesci ancora a eseguire la ricerca, potrebbe essere a causa di un problema di indicizzazione. Per la reindicizzazione, vai al seguente nodo e cambia il valore della proprietà &quot;re-index&quot; in true:
>
>/oak:index/cmLucene&quot; e modifica il valore della proprietà

## Modificare la visualizzazione predefinita della pagina di ricerca {#change-default-view-of-the-search-page}

1. Vai a `https://'[server]:[port]'/[ContextPath]/crx/de` e accedi come amministratore.
1. Nella cartella delle app, crea una cartella denominata list con percorso/struttura simile alla cartella dell’elenco che si trova in /libs/granite/ui/content/shell/omnisearch/searchresults/singleresults/views:

   1. Fai clic con il pulsante destro del mouse sulla cartella degli elementi nel percorso seguente e seleziona **Sovrapponi nodo**:

      `/libs/granite/ui/content/shell/omnisearch/searchresults/singleresults/views/list`

   1. Assicurati che la finestra di dialogo Sovrapponi nodo abbia i seguenti valori:

      **Percorso:** /libs/granite/ui/content/shell/omnisearch/searchresults/singleresuls/views/list

      **Posizione:** /apps/

      **Tipi di nodo di corrispondenza:** selezionati

   1. Fai clic su **OK**. La struttura delle cartelle viene creata nella cartella delle app.

   1. Fare clic su **Salva tutto**.

1. Nel nodo appena creato, elencare, aggiungi la seguente proprietà e fai clic su **Salva tutto**:

   <table>
   <tbody>
   <tr>
      <td><strong>Nome</strong></td>
      <td><strong>Tipo</strong></td>
      <td><strong>Valore</strong></td>
   </tr>
   <tr>
      <td>sling:orderBefore<br /> </td>
      <td>Stringa</td>
      <td>scheda</td>
   </tr>
   </tbody>
   </table>

1. La personalizzazione mostra i risultati della ricerca nella vista a elenco per tutte le console, compresi Forms e Documenti, Risorse e Siti.

## Modificare la visualizzazione predefinita della pagina delle risorse {#change-default-view-of-the-assets-page}

>[!NOTE]
>
>Questi passaggi consentono di modificare la visualizzazione predefinita di tutte le console, ad esempio Forms e Documenti, Risorse e Siti.

1. Vai a `https://'[server]:[port]'/[ContextPath]/crx/de` e accedi come amministratore.
1. Nella cartella delle app, crea una cartella denominata list con percorso/struttura simile alla cartella dell’elenco che si trova in:

   /libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/

   1. Fai clic con il pulsante destro del mouse sulla cartella degli elementi nel percorso seguente e seleziona **Sovrapponi nodo**:

      `/libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/list`

   1. Assicurati che la finestra di dialogo Sovrapponi nodo abbia i seguenti valori:

      **Percorso:** /libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/list

      **Posizione:** /apps/

      **Tipi di nodo di corrispondenza:** selezionati

   1. Fai clic su **OK**. La struttura delle cartelle viene creata nella cartella delle app.

   1. Fare clic su **Salva tutto**.

1. Nel nodo appena creato, elencare, aggiungi la seguente proprietà e fai clic su **Salva tutto**:

   <table>
   <tbody>
   <tr>
      <td><strong>Nome</strong></td>
      <td><strong>Tipo</strong></td>
      <td><strong>Valore</strong></td>
   </tr>
   <tr>
      <td>sling:orderBefore<br /> </td>
      <td>Stringa</td>
      <td>scheda</td>
   </tr>
   </tbody>
   </table>

1. Cancella i cookie del browser o utilizza la modalità in incognito del browser per visualizzare le risorse. La pagina delle risorse, per impostazione predefinita, viene visualizzata nel layout della scheda.

## Mostra/nascondi proprietà personalizzate nelle pagine Creazione risorse e Proprietà {#show-hide-custom-properties-on-asset-creation-and-properties-pages}

Per visualizzare o nascondere le proprietà personalizzate, completa i passaggi seguenti:

1. Sotto il nodo di proprietà personalizzato, ad esempio geographicAllocation, crea un nuovo nodo con il nome &quot;granite:rendercondition&quot; di tipo &quot;nt:unstructured&quot;.
1. Aggiungi la seguente proprietà al nodo e fai clic su **Salva tutto**:

   <table>
   <tbody>
   <tr>
      <td><strong>Nome</strong></td>
      <td><strong>Tipo</strong></td>
      <td><strong>Valore</strong></td>
   </tr>
   <tr>
      <td>sling:resourceType<br /> </td>
      <td>Stringa</td>
      <td>fd/cm/ma/gui/components/admin/assetsproperties/customproperty<br /> </td>
   </tr>
   </tbody>
   </table>

1. Per nascondere questa proprietà nella pagina di creazione della risorsa, aggiungi la seguente proprietà e fai clic su **Salva tutto**:

   <table>
   <tbody>
   <tr>
      <td><strong>Nome</strong></td>
      <td><strong>Tipo</strong></td>
      <td><strong>Valore</strong></td>
   </tr>
   <tr>
      <td>hideOnCreate<br /> </td>
      <td>Booleano</td>
      <td>vero<br /> </td>
   </tr>
   </tbody>
   </table>

1. Per nascondere la proprietà personalizzata nella pagina delle proprietà delle risorse, aggiungi la seguente proprietà e fai clic su **Salva tutto**:

   <table>
   <tbody>
   <tr>
      <td><strong>Nome</strong></td>
      <td><strong>Tipo</strong></td>
      <td><strong>Valore</strong></td>
   </tr>
   <tr>
      <td>hideOnEdit<br /> </td>
      <td>Booleano</td>
      <td>vero<br /> </td>
   </tr>
   </tbody>
   </table>

   Per visualizzare nuovamente i valori, reimpostare i valori delle proprietà su `false` o eliminare le voci della proprietà.
