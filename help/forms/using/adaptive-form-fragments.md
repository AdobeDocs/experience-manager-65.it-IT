---
title: Frammenti di moduli adattivi
description: I moduli adattivi forniscono un meccanismo per creare un segmento di modulo, ad esempio un pannello o un gruppo di campi, da utilizzare in qualsiasi modulo adattivo. Puoi anche salvare un pannello esistente come frammento.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
feature: Adaptive Forms, Foundation Components
discoiquuid: 1a32eb24-db3b-4fad-b1c7-6326b5af4e5e
docset: aem65
exl-id: 2f276e9d-b3c1-48f7-a94a-bdf7eb15a031
source-git-commit: d85fc98d9a31bc4014aef4311ba0f838c7ef619a
workflow-type: tm+mt
source-wordcount: '2359'
ht-degree: 1%

---

# Frammenti di moduli adattivi{#adaptive-form-fragments}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/adaptive-form-fragments-core-components.html) |
| AEM 6.5 | Questo articolo |

<span class="preview">Adobe Systems consiglia di utilizzare i componenti](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) core di acquisizione [dati moderni ed estensibili per [creare nuovi Forms adattivi o [aggiungere Forms](/help/forms/using/create-an-adaptive-form-core-components.md) adattivi alle pagine](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md) AEM Sites. Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base. </span>

Anche se ogni modulo è progettato per uno scopo specifico, nella maggior parte dei moduli sono presenti alcuni segmenti comuni, ad esempio per fornire dati personali come nome e indirizzo, dettagli sulla famiglia, dettagli sul reddito e così via. Gli sviluppatori di moduli devono creare questi segmenti comuni ogni volta che viene creato un nuovo modulo.

I moduli adattivi forniscono un meccanismo pratico per creare segmenti di modulo una sola volta, come un pannello o un gruppo di campi, e riutilizzarli nei moduli adattivi. Questi segmenti riutilizzabili e autonomi sono denominati frammenti di modulo adattivi.

## Crea un frammento {#create-a-fragment}

È possibile creare un frammento di modulo adattivo da zero o salvare un pannello in un modulo adattivo esistente come frammento.

### Crea frammento da zero {#create-fragment-from-scratch}

1. Accedi all AEM Forms istanza autore all&#39;indirizzo https://[*hostname*]:[*porta*]/aem/forms.html.
1. Fare clic su **Crea > frammento** di modulo adattivo.
1. Specifica titolo, nome, descrizione e tag per il frammento.

   >[!NOTE]
   >
   >Assicurati di specificare un nome univoco per il frammento. Se esiste già un altro frammento con lo stesso nome, la creazione del frammento non riesce.

1. Fai clic per aprire **Modello modulo** e dalla scheda **Seleziona da** dal menu a discesa, seleziona uno dei seguenti modelli per il frammento:

   * **Nessuno**: specifica di creare il frammento da zero senza utilizzare alcun modello di modulo.

     >[!NOTE]
     >
     > In Forms adattivo basato su componenti core, è possibile utilizzare più volte un singolo frammento di modulo in un modulo. Supporta sia frammenti di modulo basati su nessuno che frammenti di modulo basati su schema.

   * **Modello modulo**: specifica di creare il frammento utilizzando un modello XDP caricato in AEM Forms. Seleziona il modello XDP appropriato come modello di modulo per il frammento.

   ![Creazione di un modulo adattivo utilizzando un modello di modulo come modello](assets/form-template-model.png)

   Vengono visualizzati anche i sottomoduli contrassegnati come frammenti nel modello di modulo selezionato. Puoi selezionare un modulo secondario per il frammento di modulo adattivo dall’elenco a discesa.

   ![Seleziona sottomoduli dal modello di modulo specificato](assets/fragment-subform.png)

   È inoltre possibile creare un frammento di modulo adattivo utilizzando sottomoduli non contrassegnati come frammenti nel modello di modulo specificando l’espressione SOM per il sottomodulo nella casella a discesa.

   * **Schema XML**: specifica di creare il frammento utilizzando uno schema XML caricato in AEM Forms. Puoi caricare o selezionare dagli schemi XML disponibili come modello di modulo per il frammento.

   ![Creare un frammento di modulo adattivo basato su uno schema XML come modello](assets/xml-schema-model.png)

   Puoi anche creare un frammento di modulo adattivo selezionando dalla casella a discesa un complexType presente nello schema selezionato.

   ![Seleziona un tipo complesso dal modello di schema XML specificato](assets/complex-type.png)

1. Clic **Crea** e quindi fare clic su **Apri** per aprire il frammento, con un modello predefinito, in modalità di modifica.

In modalità di modifica puoi trascinare e rilasciare qualsiasi componente del modulo adattivo dalla barra laterale AEM sul frammento. Per informazioni sui componenti dei moduli adattivi, consulta [Introduzione all’authoring di moduli adattivi](../../forms/using/introduction-forms-authoring.md).

Inoltre, se hai selezionato uno schema XML o un modello di modulo XDP come modello di modulo per il frammento, nel Finder contenuto viene visualizzata una nuova scheda che mostra la gerarchia del modello di modulo. Consente di trascinare gli elementi del modello di modulo sul frammento. Gli elementi del modello modulo aggiunti vengono convertiti in componenti modulo mantenendo le proprietà originali dell’XDP o XSD associato.

### Salvare il pannello come frammento {#save-panel-as-a-fragment}

1. Apri un modulo adattivo contenente il pannello da salvare come frammento di modulo adattivo.
1. Nella barra degli strumenti del pannello, fai clic su **[!UICONTROL Salva come frammento]**. Viene visualizzata la finestra di dialogo Salva come frammento (Save As Fragment).

   >[!NOTE]
   >
   >Se il pannello che stai salvando come frammento contiene un pannello figlio, il frammento risultante li includerà.

1. Nella finestra di dialogo Creazione frammento, specifica le seguenti informazioni:

   * **Nome**: nome del frammento. Il valore predefinito è il nome dell’elemento del pannello. È un campo obbligatorio.
     >[!NOTE]
     >
     >Assicurati di specificare un nome univoco per il frammento. Se esiste già un altro frammento con lo stesso nome, la creazione del frammento non riesce.

   * **Titolo**: titolo del frammento. Il valore predefinito è il titolo del pannello.

   * **Descrizione**: descrizione del frammento.

   * **Tag**: assegna i tag ai metadati del frammento.

   * **Percorso di destinazione**: percorso dell’archivio in cui verrà salvato il frammento. Se non specifichi un percorso, viene creato un nodo con lo stesso nome del frammento accanto al nodo contenente il modulo adattivo. Il frammento viene salvato in questo nodo.

   * **Modello modulo**: a seconda del modello del modulo adattivo, questo campo mostra il **Schema XML**, **Modello modulo**, o **Nessuno**. È un campo non modificabile.

   * **Elemento principale modello frammento**: viene visualizzato solo nei moduli adattivi basati su XSD. Specifica la directory principale del modello per frammenti. Puoi scegliere **/** o il tipo complesso XSD dal menu a discesa. Puoi riutilizzare il frammento in un altro modulo adattivo solo se selezioni il tipo complesso come radice del modello di frammento.
Se si sceglie **/** come directory principale del modello di frammento, la struttura XSD completa dalla directory principale è visibile nella scheda modello dati del modulo adattivo. Per una directory principale del modello di frammento di tipo complesso, nella scheda del modello dati del modulo adattivo sono visibili solo i discendenti del tipo complesso selezionato. Se crei un frammento e scegli un tipo complesso come **Elemento principale modello frammento**, è possibile utilizzarlo ovunque venga utilizzato quel tipo complesso, all&#39;interno dello stesso modulo o in più moduli.

   * **Rif XSD**: viene visualizzato solo nei moduli adattivi basati su XSD. Viene visualizzata la posizione dello schema XML.

   * **Rif. XDP**: viene visualizzato solo nei moduli adattivi basati su XDP. Viene visualizzata la posizione del modello di modulo XDP.

   ![save-fragment](assets/save-fragment.png)

   Finestra di dialogo Salva come frammento

1. Fai clic su **OK**.

   Il pannello viene salvato nella posizione specificata o predefinita nell’archivio. Nel modulo adattivo, il pannello viene sostituito da un’istantanea del frammento. Come mostrato di seguito, il pannello Informazioni generali e i relativi pannelli secondari, Informazioni personali e Indirizzo, vengono salvati come frammento.

   Per modificare il frammento, fate clic su **[!UICONTROL Modifica risorsa]** nella barra degli strumenti del pannello. Il frammento viene aperto in una nuova scheda o finestra in modalità di modifica.

   ![Modifica di un frammento](assets/edit-fragment.png)

## Utilizzo dei frammenti {#working-with-fragments}

### Configurare l’aspetto del frammento {#configure-fragment-appearance}

Qualsiasi frammento inserito nei moduli adattivi viene visualizzato come immagine segnaposto. Il segnaposto visualizza titoli contenenti fino a un massimo di dieci pannelli secondari nel frammento. Puoi configurare AEM Forms in modo da visualizzare il frammento completo invece dell’immagine segnaposto.

Per visualizzare frammenti completi nei moduli, effettuare le seguenti operazioni:

1. Vai alla pagina di configurazione AEM console web all&#39;indirizzo https:host:[*[* porta *]*]/system/console/configMgr.

1. Search e fai clic su **[!UICONTROL Modulo adattivo e configurazione]** canale web comunicazione interattiva per aprirlo in modalità di modifica.
1. Disattiva **[!UICONTROL la casella di controllo Abilita segnaposto al posto del frammento]** per visualizzare frammenti completi anziché l&#39;immagine segnaposto.

### Inserire un frammento in un modulo adattivo {#insert-a-fragment-in-an-adaptive-form}

I frammenti di modulo adattivi creati vengono visualizzati nella scheda Frammenti di modulo adattivi del Content Finder AEM. Per inserire un frammento di modulo adattivo in un modulo adattivo:

1. Apri il modulo adattivo, in modalità di modifica, in cui desideri inserire un frammento di modulo adattivo.
1. Clic **Risorse** ![assets-browser](assets/assets-browser.png) nella barra laterale. Nel browser Risorse, seleziona **Frammenti di moduli adattivi** dal menu a discesa.

   È inoltre possibile scegliere di visualizzare tutti i frammenti di modulo adattivi o di filtrare in base al modello di modulo, ovvero Modello di modulo, Schema XML o Base.

1. Trascina un frammento di modulo adattivo nel modulo adattivo.

   >[!NOTE]
   >
   >Il frammento di modulo adattivo non è abilitato per la creazione dall’interno del modulo adattivo. Inoltre, non è possibile utilizzare un frammento basato su XSD in un modulo adattivo basato su JSON e viceversa.

Il frammento di modulo adattivo viene inserito per riferimento nel modulo adattivo e sincronizzato con il frammento di modulo adattivo autonomo. Ciò significa che quando aggiorni il frammento di modulo adattivo, le modifiche si riflettono in tutti i moduli adattivi in cui viene utilizzato il frammento.

### Incorporare un frammento in un modulo adattivo {#embed-a-fragment-in-adaptive-form}

Puoi scegliere di incorporare un frammento di modulo adattivo in un modulo adattivo facendo clic su **Incorpora risorsa: &lt;*fragmentName*>** sulla barra degli strumenti del pannello del frammento aggiunto, come illustrato nell’immagine di esempio seguente.

![Incorporare un frammento di modulo in un modulo adattivo](assets/embed-fragment.png)

>[!NOTE]
>
>Il frammento incorporato non è più collegato al frammento autonomo. Puoi modificare i componenti nel frammento incorporato direttamente dal modulo adattivo.

### Utilizzo di frammenti all’interno di frammenti {#using-fragments-within-fragments}

Puoi creare frammenti di modulo adattivi nidificati, il che significa che puoi trascinare un frammento all’interno di un altro frammento e disporre di una struttura di frammenti nidificata.

### Modifica frammenti {#change-fragments}

È possibile sostituire o modificare un frammento di modulo adattivo con un altro frammento utilizzando **Seleziona risorsa frammento** nella finestra di dialogo Modifica componente per il pannello di un frammento di modulo adattivo.

### Genera documento di record per frammento di modulo adattivo {#generate-DOR-for-fragments}

Documento di record (DOR) consente di conservare le informazioni dei moduli in formato di stampa o documento. In questo modo è possibile tenere traccia delle informazioni sui clienti in qualsiasi momento e utilizzare il documento di record per archiviare moduli e contenuti in formato PDF. [Scopri come generare un documento di record per i frammenti di modulo adattivo](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md).

### Utilizzo di un frammento di modulo più volte in un modulo adattivo {#using-form-fragment-mutiple-times-in-af}

È possibile utilizzare più volte un frammento di modulo basato su schema in un modulo adattivo per salvare i dati in modo univoco per ogni campo del frammento di modulo. Ad esempio, puoi utilizzare un frammento di modulo indirizzo per raccogliere i dettagli dell’indirizzo per indirizzi permanenti, di comunicazione e di presentazione in un modulo di richiesta di prestito.

![utilizzo di più frammenti in un modulo adattivo](/help/forms/using/assets/using-multiple-fragment-af.gif)

>[!NOTE]
>
> * Se in un modulo adattivo utilizzi più volte frammenti di modulo non basati su, si verifica la sincronizzazione dei dati tra i campi dei frammenti. Il problema di sincronizzazione dei dati non si verifica nei frammenti di modulo basati su componenti core, in cui è possibile utilizzare più volte un frammento basato su schema o nessuno in un modulo.

## Mappatura automatica dei frammenti per l’associazione dati {#auto-mapping-of-fragments-for-data-binding}

Quando crei un frammento di modulo adattivo utilizzando un modello di modulo XFA o un tipo complesso XSD e trascini il frammento in un modulo adattivo, il frammento XFA o il tipo complesso XSD viene sostituito automaticamente dal frammento di modulo adattivo corrispondente la cui radice del modello di frammento è mappata al frammento XFA o al tipo complesso XSD.

Puoi modificare la risorsa del frammento e i relativi binding dalla finestra di dialogo Modifica componente.

>[!NOTE]
>
>Puoi anche trascinare un frammento di modulo adattivo associato dalla libreria Frammento di modulo adattivo in AEM content finder e fornire il riferimento di associazione corretto dalla finestra di dialogo Modifica componente del pannello Frammento di modulo adattivo.

## Gestire i frammenti {#manage-fragments}

Puoi eseguire diverse operazioni sui frammenti di moduli adattivi utilizzando l’interfaccia utente di AEM Forms.

1. Passa a `https://[hostname]:'port'/aem/forms.html`.

1. Clic **Seleziona** nella barra degli strumenti dell’interfaccia utente di AEM Forms e seleziona un frammento di modulo adattivo. La barra degli strumenti mostra le seguenti operazioni che è possibile eseguire sul frammento di modulo adattivo selezionato.

<table>
 <tbody>
  <tr>
   <td><p><strong>Operazione</strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
  </tr>
  <tr>
   <td><p>Apri</p> </td>
   <td><p>Apre il frammento di modulo adattivo selezionato in modalità di modifica.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Visualizza proprietà</p> </td>
   <td><p>Apre il pannello Proprietà. Dal pannello Proprietà puoi visualizzare e modificare le proprietà, generare un’anteprima e caricare un’immagine in miniatura per il frammento selezionato. Per ulteriori informazioni, consulta <a href="../../forms/using/manage-form-metadata.md" target="_blank">Gestione dei metadati</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Copiare</p> </td>
   <td><p>Copia il frammento selezionato. Il pulsante Incolla viene visualizzato nella barra degli strumenti.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Scarica</p> </td>
   <td><p>Scarica il frammento selezionato.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Anteprima</p> </td>
   <td><p>Fornisce opzioni per visualizzare in anteprima il frammento come HTML o come anteprima personalizzata unendo i dati di un file XML con il frammento. Per ulteriori informazioni, consulta <a href="/help/forms/using/previewing-forms.md" target="_blank">Anteprima di un modulo</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Avvia revisione/Gestisci revisione</p> </td>
   <td><p>Consente di avviare e gestire la revisione del frammento selezionato. Per ulteriori informazioni, vedere <a href="../../forms/using/create-reviews-forms.md" target="_blank">Creazione e gestione delle recensioni</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Crea dizionario</p> </td>
   <td><p>Genera un dizionario per la localizzazione del frammento selezionato. Per ulteriori informazioni, consulta <a href="/help/forms/using/lazy-loading-adaptive-forms.md" target="_blank">Localizzazione di moduli adattivi</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Pubblica/Annulla pubblicazione</p> </td>
   <td><p>Pubblica o annulla la pubblicazione del frammento selezionato.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Eliminare</p> </td>
   <td><p>Elimina il frammento selezionato.<br /> <br /> </p> </td>
  </tr>
 </tbody>
</table>

## Localizzazione di un modulo adattivo contenente frammenti {#localizing-adaptive-form-containing-fragments}

Per localizzare un modulo adattivo che contiene frammenti di modulo adattivo, è necessario localizzare separatamente il frammento e il modulo. L&#39;idea è quella di localizzare un frammento una volta e riutilizzarlo in più moduli adattivi.

>[!NOTE]
>
>Le chiavi di localizzazione nel frammento non verranno visualizzate nel file XLIFF per un modulo adattivo.

## Punti chiave da ricordare quando si lavora con i frammenti {#key-points-to-remember-when-working-with-fragments}

* Assicurati che il nome del frammento sia univoco. Il frammento non viene creato se è presente un frammento con lo stesso nome.
* In un modulo adattivo basato su XDP, se salvi un pannello come frammento che include un altro frammento XDP, il frammento risultante verrà associato automaticamente al frammento XDP secondario. Se è presente un modulo adattivo basato su XSD, il frammento risultante sarà associato alla directory principale dello schema.
* Quando crei un frammento di modulo adattivo, viene creato un nodo di frammento, simile al nodo guideContainer per un modulo adattivo, in CRXDe Lite.
* Un frammento in un modulo adattivo che utilizza un modello dati modulo diverso non è supportato. Ad esempio, un frammento basato su XDP non è supportato in un modulo adattivo basato su XSD e viceversa.
* I frammenti di modulo adattivi sono disponibili per l’utilizzo tramite la scheda Frammenti di modulo adattivi nel Finder di contenuti AEM.
* Qualsiasi espressione, script o stile in un frammento di modulo adattivo indipendente viene mantenuto quando viene inserito tramite riferimento o incorporato in un modulo adattivo.
* Non è possibile modificare un frammento di modulo adattivo, inserito per riferimento, dall’interno di un modulo adattivo. Per apportare modifiche, puoi modificare il frammento di modulo adattivo autonomo o incorporarlo nel modulo adattivo.
* Quando pubblichi un modulo adattivo, devi pubblicare i frammenti di modulo adattivo autonomi inseriti per riferimento nel modulo adattivo.
* Quando ripubblichi un frammento di modulo adattivo aggiornato, le modifiche si riflettono nelle istanze pubblicate del modulo adattivo in cui viene utilizzato il frammento.
* Il modulo adattivo contenente il componente Verifica non supporta gli utenti anonimi. Inoltre, non è possibile utilizzare il componente Verifica in un frammento di modulo adattivo.
* (**Solo Mac**) Per garantire che la funzionalità dei frammenti di modulo funzioni perfettamente in tutti gli scenari, aggiungere la seguente voce al file /private/etc/hosts:
  `127.0.0.1 <Host machine>`**Computer host**: il computer Apple Mac su cui è distribuito AEM Forms.

## Frammenti di riferimento {#reference-fragments}

Sono disponibili frammenti di modulo adattivi di riferimento che è possibile utilizzare per creare il modulo. Per ulteriori informazioni, consulta [Frammenti di riferimento](../../forms/using/reference-adaptive-form-fragments.md).
