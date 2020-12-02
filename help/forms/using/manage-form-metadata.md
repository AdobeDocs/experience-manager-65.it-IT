---
title: Gestire i metadati dei moduli
seo-title: Gestire i metadati dei moduli
description: I metadati semplificano la categorizzazione e l’organizzazione delle risorse e aiutano gli utenti che cercano una risorsa specifica.
seo-description: I metadati semplificano la categorizzazione e l’organizzazione delle risorse e aiutano gli utenti che cercano una risorsa specifica.
uuid: d982df6f-a256-4bad-868f-74fcd08350f8
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: ba571f8e-8bd3-48eb-82e1-c93b14ffe44a
docset: aem65
translation-type: tm+mt
source-git-commit: 06335b9a85414b6b1141dd19c863dfaad0812503
workflow-type: tm+mt
source-wordcount: '1994'
ht-degree: 1%

---


# Gestire i metadati del modulo{#manage-form-metadata}

## Panoramica  {#overview-nbsp}

I metadati semplificano la categorizzazione e l’organizzazione delle risorse e aiutano gli utenti che cercano una risorsa specifica.

 AEM Forms, per impostazione predefinita, fornisce un set definito di metadati per ciascun tipo di risorsa. Oltre ai metadati predefiniti, potete aggiungere metadati personalizzati a ciascun tipo di risorsa.  AEM Forms offre inoltre i mezzi giusti per creare, gestire e scambiare questi metadati in modo efficiente per i moduli.

Se siete uno sviluppatore o un proprietario del sito, potete personalizzare Forms Portal, l’interfaccia utente finale per  AEM Forms in modo che rifletta i metadati utilizzati nell’organizzazione. Per ulteriori informazioni su Forms Portal, vedere [Introduzione alla pubblicazione di moduli su un portale](../../forms/using/introduction-publishing-forms.md).

## Metadati in  AEM Forms {#metadata-in-aem-forms}

In  AEM Forms, l’elenco delle proprietà dei metadati associate a una risorsa dipende dal tipo. Inoltre, se aggiungete delle proprietà di metadati personalizzate, queste vengono aggiunte a tutte le risorse del tipo in cui sono stati aggiunti i metadati personalizzati.

### Tipi di risorse {#asset-types}

In  AEM Forms sono supportati i seguenti tipi di risorse:

* Modelli per moduli (moduli XFA)
* PDF forms
* Documento (PDF semplici)
* Moduli adattivi
* Riferimenti
* XFS

#### Ampio elenco di metadati {#extensive-list-of-metadata}

Di seguito è riportato un elenco completo delle proprietà di metadati supportate in  AEM Forms:

<table>
 <tbody> 
  <tr> 
   <td><strong>Nome proprietà</strong></td> 
   <td><strong>Tipo risorsa</strong></td> 
   <td><strong>Descrizione</strong><br /> </td> 
  </tr> 
  <tr> 
   <td>Titolo</td> 
   <td>Tutto tranne risorsa</td> 
   <td>Nome visualizzato del modulo.<br /> </td> 
  </tr> 
  <tr> 
   <td>Descrizione</td> 
   <td>Tutto tranne risorsa</td> 
   <td>Descrizione del modulo. L'utente può specificare questo valore.<br /> </td> 
  </tr> 
  <tr> 
   <td>Tipo</td> 
   <td>Tutti i bundle </td> 
   <td><p>Un valore di sola lettura che specifica il tipo di risorsa. Può avere uno dei seguenti valori:</p> 
    <ul> 
     <li>Modello di modulo</li> 
     <li>Modulo PDF, modulo PDF (Acrobat) o modulo PDF (firmato)</li> 
     <li>Documento, Documento (Firmato)</li> 
     <li>Modulo adattivo</li> 
     <li>Risorsa</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Creato</td> 
   <td>Tutti i bundle </td> 
   <td>Un valore di sola lettura che specifica l’ora di creazione delle risorse.</td> 
  </tr> 
  <tr> 
   <td>Data ultima modifica</td> 
   <td>Tutti i bundle </td> 
   <td>Valore di sola lettura che specifica l’ora dell’ultima modifica apportata alla risorsa.</td> 
  </tr> 
  <tr> 
   <td>Autore</td> 
   <td>Tutto tranne risorsa</td> 
   <td><p>Valore di sola lettura calcolato automaticamente in base al tipo di modulo.</p> 
    <ul> 
     <li>PDF/Modello/Documento modulo - recuperato dal file binario caricato.</li> 
     <li>Modulo adattivo: accesso utente al momento della creazione del modulo.</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Stato</td> 
   <td>Tutto tranne risorsa</td> 
   <td><p> Valore di sola lettura che definisce uno dei seguenti stati di un modulo:</p> 
    <ul> 
     <li>Nessun valore: Se un modulo non è mai stato pubblicato.</li> 
     <li>Pubblicato: Quando viene pubblicato un modulo.</li> 
     <li>Modificato: Quando un modulo è stato modificato dopo essere stato pubblicato una volta.</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Data ultima pubblicazione</td> 
   <td>Tutto tranne risorsa</td> 
   <td>Valore di sola lettura che specifica l'ora dell'ultima pubblicazione del modulo.</td> 
  </tr> 
  <tr> 
   <td>Ora di attivazione/disattivazione pubblicazione</td> 
   <td>Tutto tranne risorsa</td> 
   <td><p>Data e ora in cui è pianificata la pubblicazione automatica del modulo/annullamento della pubblicazione. Questo valore viene impostato dall’utente al momento della modifica dei metadati.</p> 
    <ul> 
     <li>L’ora di attivazione e disattivazione della pubblicazione deve essere successiva alla data corrente. </li> 
     <li>Il tempo di pubblicazione deve essere oltre il tempo di pubblicazione attivato. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Invia URL</td> 
   <td><p>Modello di modulo</p> <p>modulo PDF</p> </td> 
   <td><p>Per configurare un URL specificato dall'utente per l'invio dei dati del modulo a un servlet.</p> <p>Invia URL può essere configurato utilizzando uno dei seguenti metodi, elencati in ordine di precedenza:</p> 
    <ul> 
     <li>Per specificare un URL di invio direttamente in un modello di modulo, utilizzare il pulsante Invia per HTTP durante la creazione di un modulo XFA in  AEM Forms Designer.</li> 
     <li>Nellinterfaccia utente di AEM Forms, selezionare un modulo e specificare un URL di invio per la modifica delle proprietà dei metadati.</li> 
     <li>In Forms Portal, modificate il componente Ricerca e filtro e specificate un URL di invio nella scheda Collegamento modulo.</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Profilo di rendering HTML</td> 
   <td>Modello di modulo</td> 
   <td>Profilo di rendering HTML utilizzato per il rendering di un modello di modulo in formato HTML.</td> 
  </tr> 
  <tr> 
   <td>Formato di rendering</td> 
   <td><p>Modello di modulo</p> <p>Modulo adattivo</p> </td> 
   <td><p>Questa opzione consente all'utente di specificare il formato di rendering del modulo quando i moduli vengono pubblicati:</p> 
    <ul> 
     <li>HTML</li> 
     <li>PDF</li> 
     <li>Entrambe</li> 
    </ul> <p>Questa opzione è utilizzata per limitare il formato di rendering dei moduli solo sul portale dei moduli, dove sono visibili all'utente finale.</p> </td> 
  </tr> 
  <tr> 
   <td>Tag</td> 
   <td>Tutto tranne risorsa</td> 
   <td>Etichette associate al modulo per semplificare la ricerca.</td> 
  </tr> 
  <tr> 
   <td>Riferimenti</td> 
   <td><p>Modulo adattivo</p> <p>Modello di modulo</p> <p>Risorsa</p> </td> 
   <td><p>Elenco delle risorse (altri moduli o risorse) a cui è correlato il modulo. Tali attività possono essere suddivise in due categorie:</p> 
    <ul> 
     <li>Riferimenti: Risorse a cui fa riferimento il modulo corrente.</li> 
     <li>Con riferimento: Risorse che fanno riferimento alla risorsa corrente.</li> 
    </ul> <p>Queste risorse vengono visualizzate come collegamenti e i relativi metadati sono accessibili direttamente facendo clic su di esse.<br /> </p> </td> 
  </tr> 
  <tr> 
   <td>Selezione del modello di modulo (XDP/XSD)</td> 
   <td>Modulo adattivo</td> 
   <td><p>Specifica quale modello di modulo viene utilizzato per la creazione del modulo adattivo. Questa proprietà può avere i seguenti valori:</p> 
    <ul> 
     <li>Modello di modulo: Un modello di modulo viene selezionato tra quelli esistenti nella directory archivio. Questo valore può essere aggiornato.</li> 
     <li>Schema XML: Viene caricato un file XSD. Questo valore può essere aggiornato.</li> 
     <li>Nessuno</li> 
    </ul> 
    <div>
      Una volta selezionato, un modello di modulo può essere aggiornato ma non rimosso. 
    </div> </td> 
  </tr> 
 </tbody> 
</table>

## Visualizza metadati modulo {#view-form-metadata}

Le risorse dispongono di valori di proprietà esistenti, che possono essere visualizzati in modalità di sola lettura. Questi metadati vengono generati al momento del caricamento del modulo o della creazione del modulo.

1. Andate alla posizione della risorsa per la quale desiderate visualizzare i metadati.

1. Aprire la pagina delle proprietà utilizzando uno dei seguenti modi:

   1. Fate clic sull&#39;icona Visualizza proprietà ![e_reviewmode_properties_n](assets/e_reviewmode_properties_n.png) da Azioni rapide.

      >[!NOTE]
      >
      >Azioni rapide sono gli elementi di azione visualizzati sopra una miniatura al passaggio del mouse.

   1. Selezionare il modulo e fare clic sull&#39;icona Visualizza proprietà ![e_reviewmode_properties_n](assets/e_reviewmode_properties_n.png) visualizzata nella barra degli strumenti.
   1. Passare alla pagina dei dettagli del modulo facendo clic sulla miniatura del modulo quando non è attiva la modalità di selezione. A questo punto, fare clic sull&#39;icona occhio ![aem6forms_eye_viewon](assets/aem6forms_eye_viewon.png) in alto a destra, quindi fare clic su Proprietà nell&#39;elenco al di sotto.

1. Nella pagina delle proprietà visualizzata viene visualizzato uno schema contenente solo le proprietà dei metadati che contengono un certo valore.

   La pagina delle proprietà include una barra degli strumenti contenente due icone di azione:

   * Modifica: ![aem6forms_edit](assets/aem6forms_edit.png) Modificare i valori delle proprietà dei metadati
   * Visualizza: ![aem6forms_eye_viewon](assets/aem6forms_eye_viewon.png) Passare alla pagina dei dettagli del modulo, che apre il modulo in modalità di anteprima.

   La parte contenuto è divisa in due parti:

   * Il pannello a sinistra contiene la miniatura del modulo
   * Il pannello a destra contiene le proprietà dei metadati in modalità di sola lettura, distribuite tra varie schede.


## Aggiungere/aggiornare i valori dei metadati del modulo {#add-update-form-metadata-values}

Potete modificare il valore delle proprietà di metadati esistenti o aggiungere nuovi valori a un campo di proprietà di metadati esistente (ad esempio, se un campo di metadati è vuoto).

### Aggiorna valori proprietà metadati {#update-metadata-property-values}

1. Seguire i passaggi indicati nella sezione precedente per aprire la pagina delle proprietà in cui è possibile visualizzare i metadati esistenti del modulo selezionato.

1. Dalla barra degli strumenti, fare clic sull&#39;icona di modifica ![aem6forms_edit](assets/aem6forms_edit.png) per passare dalla modalità di sola lettura alla modalità di lettura/scrittura.

1. La pagina delle proprietà che si apre contiene uno schema che contiene un insieme di campi di input modificabili e testo statico.

1. Le proprietà visualizzate nel testo statico sono quelle che non è possibile modificare.

1. Potete spostarvi in altre schede per trovare i campi di input per le proprietà dei metadati inserite al loro interno.

   Questa pagina dispone di una barra degli strumenti contenente due icone di azione diverse da quelle presenti in modalità di visualizzazione:

   * Annulla: ![aem6forms_close](assets/aem6forms_close.svg_w24.png) Annulla tutte le modifiche apportate ai valori delle proprietà dei metadati
   * Fatto: ![aem6forms_check](assets/aem6forms_check.png) Salvare tutte le modifiche apportate finora ai valori delle proprietà dei metadati

   Entrambe queste azioni indirizzano l&#39;utente alla modalità di sola lettura della pagina delle proprietà contenente i valori aggiornati.

### Aggiornare la miniatura del modulo {#update-the-form-thumbnail}

Il pannello a sinistra nella pagina delle proprietà mostra la miniatura del modulo. Per impostazione predefinita, la miniatura visualizzata è quella generata al momento della creazione del modulo (modulo adattivo) o al momento del caricamento del modulo.

Per tutti i tipi di modulo, è possibile caricare un&#39;immagine facendo clic su **[!UICONTROL Carica immagine]** e individuando un file immagine nella directory locale. L&#39;immagine selezionata viene utilizzata come miniatura invece di quella predefinita.

Per i moduli adattivi, sono disponibili funzionalità aggiuntive che consentono all&#39;utente di generare una miniatura come istantanea dell&#39;anteprima del modulo adattivo corrente. Poiché  AEM Forms supporta anche la creazione di moduli adattivi, l&#39;anteprima del modulo adattivo può essere modificata ogni volta che si modifica il modulo adattivo. Questa funzionalità per generare una miniatura consente di ottenere una nuova miniatura per il modulo adattivo in base allo stato di anteprima corrente. Fare clic su **[!UICONTROL Genera anteprima]** per eseguire questa azione.

>[!NOTE]
>
>* Usate un’immagine quadrata per la miniatura. Quando usate un’immagine non quadrata e visualizzate la miniatura nella vista a elenco, la miniatura appare troncata.
>* Una volta caricata o generata una nuova immagine, la miniatura viene sostituita da questa e non può essere reimpostata sull’immagine precedente.

>



## Aggiunta di metadati personalizzati {#add-custom-metadata}

Oltre ai metadati forniti,  AEM Forms supporta nuovi metadati personalizzati.

È disponibile uno strumento (Editor schema metadati) per definire lo schema per il layout dei metadati; ovvero il layout di ciò che viene visualizzato nella pagina **[!UICONTROL Proprietà]** di un modulo. L’Editor schema metadati consente di aggiungere o modificare uno schema personalizzato per le risorse.

 AEM Forms espone gli schemi di metadati dei tipi di moduli supportati in questo strumento. In questo modo, potete accedere a questi schemi e utilizzare la funzionalità fornita nell&#39;editor di schemi di metadati per aggiungere proprietà personalizzate.

### Spostarsi nell&#39;editor dello schema di metadati {#navigate-the-metadata-schema-editor}

1. Passa a **[!UICONTROL Strumenti > Risorse > Schemi metadati]**.

1. Fare clic su **[!UICONTROL forms]** dai moduli dello schema elencati.

1. Dall’elenco visualizzato, fate clic sul tipo di risorsa per il quale desiderate aggiungere metadati personalizzati.

   >[!NOTE]
   >
   >Questi schemi contengono proprietà di metadati che non possono essere modificate o modificate (selezionando la casella di controllo e facendo clic su Modifica dalla barra degli strumenti) per evitare problemi di funzionamento.

1. Qualsiasi tipo di risorsa su cui si fa clic apre un elenco contenente l&#39;opzione `extendedmetadata`. Modificate questo schema.

1. Selezionare la casella di controllo accanto a `extendedmetadata`, quindi fare clic sull&#39;icona di modifica ![aem6forms_edit](assets/aem6forms_edit.png) visualizzata nella barra degli strumenti.

1.  AEM Forms apre l’editor di schemi di metadati/il generatore di moduli del tipo di risorsa selezionato (in questo caso modulo adattivo).

   ![Editor schema metadati per il tipo di modulo adattivo](assets/metadata-schema-editor-for-adaptive-form-type.png)

   Editor metadati

   1. Il pannello a sinistra contiene le sezioni a schede in cui sono posizionati i campi e il pannello a destra visualizza tutti i componenti dell’interfaccia utente disponibili e le proprietà del campo selezionato dal pannello a sinistra.

   1. La sezione bloccata non è modificabile e contiene campi per tutte le proprietà di metadati fornite al di fuori della casella.

   1. Per aggiungere altre schede, fare clic sul simbolo +.

   1. È possibile aggiungere un campo personalizzato del tipo desiderato trascinando il componente campo dalla sezione **[!UICONTROL Crea modulo]** nella pagina dello schema.
   1. Le specifiche per questo campo possono essere fornite nella sezione **[!UICONTROL Impostazioni]** dopo aver fatto clic sul campo.

### Aggiungi proprietà metadati personalizzata nell&#39;editor dello schema {#add-custom-metadata-property-in-schema-editor}

1. Passate alla scheda (esistente o nuova) in cui desiderate aggiungere la proprietà personalizzata.

1. Trascinate un componente del tipo desiderato dalla sezione **[!UICONTROL Crea modulo]** al pannello sinistro e posizionatelo in una posizione comoda.

   >[!NOTE]
   >
   >Non è possibile spostare le sezioni bloccate, ma è possibile posizionare il componente in uno qualsiasi degli spazi vuoti.

1. Fate clic su un componente appena trascinato. Nella scheda Impostazioni che si apre nel pannello a destra, inserite le informazioni per i seguenti campi:

   1. Specificare un&#39;etichetta campo da utilizzare come nome visualizzato sopra il campo inserito nello schema (ad esempio: Dipartimento)
   1. Nel campo Mappa su proprietà è possibile visualizzare un valore precompilato **&#39;./jcr:content/metadata/default&#39;**. Modificate l&#39;impostazione &quot;**default**&quot; in un nome di proprietà desiderato, che viene utilizzato per memorizzare la proprietà nell&#39;archivio crx (ad esempio: &quot;./jcr:content/metadata/dipartimento&#39;)

      >[!NOTE]
      >
      >Non modificate il prefisso ‘./jcr:content/metadata/’ definisce il percorso in cui è memorizzata la proprietà.
      >
      >Inoltre, il nome della proprietà deve essere univoco per evitare di scrivere valori per due o più proprietà nella stessa posizione nell&#39;archivio. È quindi consigliabile modificare il valore &#39;default&#39;.

   1. Riempire altre impostazioni in base ai requisiti. Ad esempio: selezionate l&#39;opzione Obbligatorio se desiderate rendere il campo obbligatorio.
   1. Per eliminare un campo aggiunto, selezionarlo e fare clic sull&#39;icona Elimina ![delete-1](assets/delete-1.png).

1. Se necessario, seguite i passaggi da 1 a 3 per aggiungere un&#39;altra proprietà.
1. Fare clic su **Fine** dopo aver apportato tutte le modifiche.

   È stata aggiunta correttamente una proprietà di metadati personalizzata.

Tutti i moduli adattivi in  AEM Forms ora contengono questa proprietà di metadati aggiuntiva. È possibile modificarlo dalla pagina delle proprietà.
