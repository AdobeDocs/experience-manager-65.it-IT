---
title: Gestire i metadati del modulo
description: I metadati semplificano la classificazione e l’organizzazione delle risorse e aiutano gli utenti che cercano una risorsa specifica.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
docset: aem65
role: Admin
exl-id: f82bbd39-b655-47a9-bca9-21d7cd30c082
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1967'
ht-degree: 2%

---

# Gestire i metadati del modulo{#manage-form-metadata}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/manage-metadata/manage-form-metadata.html) |
| AEM 6.5 | Questo articolo |

## Panoramica  {#overview-nbsp}

I metadati semplificano la classificazione e l’organizzazione delle risorse e aiutano gli utenti che cercano una risorsa specifica.

Per impostazione predefinita, AEM Forms fornisce un set definito di metadati per ogni tipo di risorsa. Oltre ai metadati predefiniti, puoi aggiungere metadati personalizzati a ciascun tipo di risorsa. AEM Forms offre inoltre i mezzi giusti per creare, gestire e scambiare tutti questi metadati in modo efficiente per i moduli.

Se sei uno sviluppatore o un proprietario del sito, puoi personalizzare Forms Portal, l’interfaccia utente finale di AEM Forms, in modo che rifletta i metadati utilizzati nella tua organizzazione. Per ulteriori informazioni su Forms Portal, consulta [Introduzione alla pubblicazione di moduli su un portale](../../forms/using/introduction-publishing-forms.md).

## Metadati in AEM Forms {#metadata-in-aem-forms}

In AEM Forms, l’elenco delle proprietà dei metadati associate a una risorsa dipende dal suo tipo. Inoltre, se aggiungi una proprietà di metadati personalizzata, questa viene aggiunta in tutte le risorse del tipo a cui sono stati aggiunti i metadati personalizzati.

### Tipi di risorse {#asset-types}

In AEM Forms sono supportati i seguenti tipi di risorse:

* Modelli di modulo (moduli XFA)
* PDF forms
* Documento (PDF flat)
* Moduli adattivi
* Riferimenti
* XFS

#### Ampio elenco di metadati {#extensive-list-of-metadata}

Di seguito è riportato un elenco completo delle proprietà di metadati supportate in AEM Forms:

<table>
 <tbody> 
  <tr> 
   <td><strong>Nome proprietà</strong></td> 
   <td><strong>Tipo risorsa</strong></td> 
   <td><strong>Descrizione</strong><br /> </td> 
  </tr> 
  <tr> 
   <td>Titolo</td> 
   <td>Tutto tranne la risorsa</td> 
   <td>Nome visualizzato del modulo.<br /> </td> 
  </tr> 
  <tr> 
   <td>Descrizione</td> 
   <td>Tutto tranne la risorsa</td> 
   <td>Descrizione del modulo. L’utente può specificare questo valore.<br /> </td> 
  </tr> 
  <tr> 
   <td>Tipo</td> 
   <td>Tutti i bundle </td> 
   <td><p>Valore di sola lettura che specifica il tipo di risorsa. Può avere uno dei seguenti valori:</p> 
    <ul> 
     <li>Modello di modulo</li> 
     <li>Modulo PDF, Modulo PDF (Acroform) o Modulo PDF (Signed)</li> 
     <li>Documento, Documento (Firmato)</li> 
     <li>Modulo adattivo</li> 
     <li>Risorsa</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Creato</td> 
   <td>Tutti</td> 
   <td>Valore di sola lettura che specifica l’ora di creazione della risorsa.</td> 
  </tr> 
  <tr> 
   <td>Data ultima modifica</td> 
   <td>Tutti</td> 
   <td>Valore di sola lettura che specifica l’ora dell’ultima modifica apportata alla risorsa.</td> 
  </tr> 
  <tr> 
   <td>Autore</td> 
   <td>Tutto tranne la risorsa</td> 
   <td><p>Valore di sola lettura calcolato automaticamente in base al tipo di modulo.</p> 
    <ul> 
     <li>PDF/Modello modulo/Documento: recuperato dal file binario caricato.</li> 
     <li>Modulo adattivo: utente connesso al momento della creazione del modulo.</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Stato</td> 
   <td>Tutto tranne la risorsa</td> 
   <td><p> Valore di sola lettura che definisce uno dei seguenti stati di un modulo:</p> 
    <ul> 
     <li>Nessun valore: se un modulo non è mai stato pubblicato.</li> 
     <li>Pubblicato: quando un modulo viene pubblicato.</li> 
     <li>Modificato: quando un modulo è stato modificato dopo essere stato pubblicato una volta.</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Data ultima pubblicazione</td> 
   <td>Tutto tranne la risorsa</td> 
   <td>Valore di sola lettura che specifica l'ora dell'ultima pubblicazione del modulo.</td> 
  </tr> 
  <tr> 
   <td>Ora di attivazione/disattivazione pubblicazione</td> 
   <td>Tutto tranne la risorsa</td> 
   <td><p>Ora in cui è pianificata la pubblicazione automatica o l'annullamento della pubblicazione del modulo. L’utente imposta questo valore durante la modifica dei metadati.</p> 
    <ul> 
     <li>L'ora di attivazione e disattivazione della pubblicazione deve essere successiva alla data corrente. </li> 
     <li>L'ora di disattivazione della pubblicazione deve essere successiva all'ora di attivazione della pubblicazione. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Invia URL</td> 
   <td><p>Modello di modulo</p> <p>Modulo PDF</p> </td> 
   <td><p>Per configurare un URL specificato dall'utente per l'invio dei dati del modulo a un servlet.</p> <p>L’URL di invio può essere configurato utilizzando uno dei seguenti metodi, elencati in ordine di precedenza:</p> 
    <ul> 
     <li>Specifica un URL di invio direttamente in un modello di modulo utilizzando il pulsante HTTP Invia durante la creazione di un modulo XFA in AEM Forms Designer.</li> 
     <li>Nell’interfaccia utente di AEM Forms, seleziona un modulo e specifica un URL di invio in caso di modifica delle proprietà dei metadati.</li> 
     <li>In Forms Portal, modifica il componente Ricerca ed Elenco e specifica un URL di invio nella scheda Collegamento modulo.</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Profilo rendering HTML</td> 
   <td>Modello di modulo</td> 
   <td>Il profilo di rendering HTML utilizzato durante il rendering di un modello di modulo in formato HTML.</td> 
  </tr> 
  <tr> 
   <td>Formato rendering</td> 
   <td><p>Modello di modulo</p> <p>Modulo adattivo</p> </td> 
   <td><p>Questa opzione consente di specificare il formato di rendering del modulo al momento della pubblicazione dei moduli:</p> 
    <ul> 
     <li>HTML</li> 
     <li>PDF</li> 
     <li>Entrambi</li> 
    </ul> <p>Questa opzione viene utilizzata per limitare il formato di rendering dei moduli solo nel portale dei moduli in cui sono visibili all'utente finale.</p> </td> 
  </tr> 
  <tr> 
   <td>Tag</td> 
   <td>Tutto tranne la risorsa</td> 
   <td>Etichette associate al modulo per facilitare la ricerca.</td> 
  </tr> 
  <tr> 
   <td>Riferimenti</td> 
   <td><p>Modulo adattivo</p> <p>Modello di modulo</p> <p>Risorsa</p> </td> 
   <td><p>Elenco delle risorse (altre forme o risorse) a cui è correlato questo modulo. Queste risorse possono rientrare nelle due categorie seguenti:</p> 
    <ul> 
     <li>Riferimenti: risorse a cui fa riferimento il modulo corrente.</li> 
     <li>Con riferimento da: risorse che fanno riferimento alla risorsa corrente.</li> 
    </ul> <p>Queste risorse vengono visualizzate come collegamenti e i relativi metadati sono accessibili direttamente facendo clic su di essi.<br /> </p> </td> 
  </tr> 
  <tr> 
   <td>Selezione del modello del modulo (XDP/XSD)</td> 
   <td>Modulo adattivo</td> 
   <td><p>Specifica quale modello di modulo viene utilizzato per la creazione del modulo adattivo. Questa proprietà può avere i seguenti valori:</p> 
    <ul> 
     <li>Modello di modulo: viene selezionato un modello di modulo tra quelli esistenti nel repository. Questo valore può essere aggiornato.</li> 
     <li>Schema XML: viene caricato un file XSD. Questo valore può essere aggiornato.</li> 
     <li>Nessuno</li> 
    </ul> 
    <div>
      Un modello di modulo selezionato può essere aggiornato ma non rimosso. 
    </div> </td> 
  </tr> 
 </tbody> 
</table>

## Visualizza metadati modulo {#view-form-metadata}

Le risorse presentano valori di proprietà esistenti che possono essere visualizzati in modalità di sola lettura. Questi metadati vengono generati al momento del caricamento del modulo o della creazione del modulo.

1. Passa alla posizione della risorsa di cui desideri visualizzare i metadati.

1. Aprire la pagina delle proprietà utilizzando uno dei modi seguenti:

   1. Fare clic su Visualizza proprietà ![e_reviewmode_properties_n](assets/e_reviewmode_properties_n.png) da Azioni rapide.

      >[!NOTE]
      >
      >Le Azioni rapide sono le azioni che vengono visualizzate su una miniatura al passaggio del mouse.

   1. Selezionare il modulo e fare clic su Visualizza proprietà ![e_reviewmode_properties_n](assets/e_reviewmode_properties_n.png) nella barra degli strumenti.
   1. Passare alla pagina dei dettagli del modulo facendo clic sulla miniatura del modulo quando non è attiva la modalità di selezione. A questo punto, fai clic su ![aem6forms_eye_viewon](assets/aem6forms_eye_viewon.png) icona a forma di occhio in alto a destra, quindi fare clic su Proprietà nell&#39;elenco sottostante.

1. Nella pagina delle proprietà visualizzata viene visualizzato uno schema contenente solo le proprietà dei metadati che contengono un certo valore.

   La pagina delle proprietà include una barra degli strumenti contenente due icone di azione:

   * Modifica: ![aem6forms_edit](assets/aem6forms_edit.png) Modificare i valori delle proprietà dei metadati
   * Visualizza: ![aem6forms_eye_viewon](assets/aem6forms_eye_viewon.png) Passare alla pagina dei dettagli del modulo, che apre il modulo in modalità anteprima.

   La porzione di contenuto è divisa in due parti:

   * Il pannello sinistro contiene la miniatura del modulo
   * Il pannello a destra contiene proprietà di metadati in modalità di sola lettura, distribuite tra varie schede.

## Aggiungi/aggiorna valori metadati modulo {#add-update-form-metadata-values}

Puoi modificare il valore delle proprietà dei metadati esistenti o aggiungere nuovi valori a un campo delle proprietà dei metadati esistente (ad esempio, quando un campo dei metadati è vuoto).

### Aggiorna valori proprietà metadati {#update-metadata-property-values}

1. Segui i passaggi indicati nella sezione precedente per aprire la pagina delle proprietà in cui è possibile visualizzare i metadati esistenti del modulo selezionato.

1. Dalla barra degli strumenti, fai clic sull’icona Modifica ![aem6forms_edit](assets/aem6forms_edit.png) per modificare la modalità della pagina da sola lettura a lettura/scrittura.

1. La pagina delle proprietà visualizzata contiene uno schema contenente una combinazione di campi di input modificabili e testo statico.

1. Le proprietà visualizzate nel testo statico sono quelle che non è possibile modificare.

1. Puoi passare ad altre schede per trovare i campi di input per le proprietà dei metadati posizionati sotto di esse.

   Questa pagina include una barra degli strumenti contenente due icone di azione diverse da quelle in modalità di visualizzazione:

   * Annulla: ![aem6forms_close](assets/aem6forms_close.svg_w24.png) Annulla eventuali modifiche apportate ai valori delle proprietà dei metadati
   * Fine: ![aem6forms_check](assets/aem6forms_check.png) Salva tutte le modifiche apportate ai valori delle proprietà dei metadati

   Entrambe queste azioni reindirizzano l’utente alla modalità di sola lettura della pagina delle proprietà contenente i valori aggiornati.

### Aggiornare la miniatura del modulo {#update-the-form-thumbnail}

Nel pannello sinistro della pagina delle proprietà viene visualizzata la miniatura del modulo. Per impostazione predefinita, la miniatura visualizzata è quella generata al momento della creazione del modulo (modulo adattivo) o al momento del caricamento del modulo.

Per tutti i tipi di modulo, puoi caricare un’immagine facendo clic su **[!UICONTROL Carica immagine]** e la ricerca di un file di immagine dalla directory locale. L&#39;immagine selezionata viene utilizzata come miniatura invece di quella predefinita.

Per i moduli adattivi, sono disponibili funzionalità aggiuntive che consentono all’utente di generare una miniatura come istantanea dell’anteprima del modulo adattivo corrente. Poiché AEM Forms supporta anche l’authoring di moduli adattivi, l’anteprima del modulo adattivo potrebbe cambiare ogni volta che lo si modifica. Questa funzionalità per generare una miniatura consente di ottenere una nuova miniatura per il modulo adattivo in base allo stato di anteprima corrente. Clic **[!UICONTROL Genera anteprima]** per eseguire questa azione.

>[!NOTE]
>
>* Utilizza un’immagine quadrata per la miniatura. Quando si utilizza un&#39;immagine non quadrata e si visualizza la miniatura nella vista a elenco, la miniatura appare ritagliata.
>* Una volta caricata o generata una nuova immagine, la miniatura viene sostituita da questa immagine e non può essere ripristinata all&#39;immagine precedente.
>

## Aggiungere metadati personalizzati {#add-custom-metadata}

Oltre ai metadati forniti come predefiniti, AEM Forms supporta nuovi metadati personalizzati.

Viene fornito uno strumento (Editor schema metadati) per definire lo schema per il layout dei metadati, ovvero il layout di ciò che viene visualizzato nel **[!UICONTROL Proprietà]** pagina di un modulo. L’Editor schema metadati consente di aggiungere o modificare uno schema personalizzato per le risorse.

AEM Forms espone gli schemi di metadati dei tipi di moduli supportati in questo strumento. In questo modo, puoi accedere a questi schemi e utilizzare la funzionalità fornita nell’editor schema metadati per aggiungere proprietà personalizzate.

### Navigare nell’editor schema metadati {#navigate-the-metadata-schema-editor}

1. Accedi a **[!UICONTROL Strumenti > Risorse > Schemi metadati]**.

1. Clic **[!UICONTROL moduli]** dai moduli schema elencati.

1. Nell’elenco visualizzato, fai clic sul tipo di risorsa per il quale desideri aggiungere metadati personalizzati.

   >[!NOTE]
   >
   >Questi schemi contengono proprietà di metadati che vengono fornite come predefinite e non devono essere modificate (selezionando la casella di controllo e facendo clic su modifica nella barra degli strumenti) per evitare problemi funzionali.

1. Qualsiasi tipo di risorsa su cui hai fatto clic apre un elenco contenente `extendedmetadata` opzione. Modifica questo schema.

1. Seleziona la casella di controllo accanto a `extendedmetadata` e quindi fare clic sul pulsante modifica ![aem6forms_edit](assets/aem6forms_edit.png) nella barra degli strumenti.

1. AEM Forms apre l’editor schema metadati o il generatore di moduli del tipo di risorsa selezionato (in questo caso modulo adattivo).

   ![Editor schema metadati per tipo di modulo adattivo](assets/metadata-schema-editor-for-adaptive-form-type.png)

   Editor metadati

   1. Il pannello sinistro contiene sezioni a schede in cui vengono inseriti i campi e il pannello destro visualizza tutti i componenti dell’interfaccia utente disponibili e le proprietà del campo selezionato dal pannello sinistro.

   1. La sezione bloccata non è modificabile e contiene campi per tutte le proprietà di metadati fornite come predefiniti.

   1. È possibile aggiungere altre schede facendo clic sul simbolo +.

   1. Puoi aggiungere un campo personalizzato del tipo desiderato trascinando il componente Campo dalla sezione **[!UICONTROL Genera modulo]** nella pagina dello schema.
   1. Le specifiche di questo campo possono essere fornite nel **[!UICONTROL Impostazioni]** dopo aver fatto clic sul campo.

### Aggiungi proprietà metadati personalizzata nell’editor schema {#add-custom-metadata-property-in-schema-editor}

1. Passa alla scheda (esistente o nuova) in cui desideri aggiungere la proprietà personalizzata.

1. Trascina un componente del tipo desiderato dalla sezione **[!UICONTROL Genera modulo]** sul pannello sinistro e posizionarlo in una posizione comoda.

   >[!NOTE]
   >
   >Non è possibile spostare le sezioni bloccate, ma è possibile inserire il componente in uno qualsiasi degli spazi vuoti.

1. Fai clic su un componente appena trascinato. Nella scheda Impostazioni visualizzata nel pannello di destra, inserisci le informazioni per i campi seguenti:

   1. Specifica un’Etichetta campo da utilizzare come nome visualizzato sopra il campo inserito nello schema (ad esempio: Reparto)
   1. Nel campo Mappa su proprietà puoi visualizzare un valore precompilato **&quot;./jcr:content/metadata/default&#39;**. Modificare il ‘**predefinito**&quot; al nome di proprietà desiderato, utilizzato per memorizzare la proprietà nell’archivio crx (ad esempio: &quot;./jcr:content/metadata/department&#39;)

      >[!NOTE]
      >
      >Non modificare il prefisso ‘./jcr:content/metadata/’, che definisce il percorso in cui è memorizzata la proprietà.
      >
      >Inoltre, il nome della proprietà deve essere univoco per evitare di scrivere valori per due o più proprietà nella stessa posizione nell’archivio. Pertanto, si consiglia di modificare il valore &quot;default&quot;.

   1. Compila altre impostazioni in base alle esigenze. Ad esempio: seleziona l’opzione Obbligatorio se desideri rendere obbligatorio il campo.
   1. Per eliminare un campo aggiunto, selezionarlo e quindi fare clic sul pulsante Elimina ![delete-1](assets/delete-1.png) icona.

1. Se necessario, segui i passaggi 1-3 per aggiungere un’altra proprietà.
1. Clic **Fine** dopo aver apportato tutte le modifiche.

   È stata aggiunta una proprietà di metadati personalizzata.

Tutti i moduli adattivi in AEM Forms ora contengono questa proprietà di metadati aggiuntiva. Puoi modificarlo dalla pagina delle proprietà.
