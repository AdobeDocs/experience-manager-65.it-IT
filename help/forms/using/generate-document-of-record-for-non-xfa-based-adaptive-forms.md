---
title: Genera documento di record per i moduli adattivi
seo-title: Genera documento di record per i moduli adattivi
description: Spiega come generare un modello per un documento di record (DoR) per i moduli adattivi.
seo-description: Spiega come generare un modello per un documento di record (DoR) per i moduli adattivi.
uuid: 2dc7e0de-fff9-43fa-9426-e9b047eb2595
content-type: reference
topic-tags: adaptive_forms, develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ce65cb5f-94ec-4423-9fa9-d617e9703091
docset: aem65
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2665'
ht-degree: 3%

---


# Genera documento di record per i moduli adattivi{#generate-document-of-record-for-adaptive-forms}

## Panoramica {#overview}

Dopo l&#39;invio di un modulo, i clienti in genere desiderano conservare un record, in formato cartaceo o in formato documento, delle informazioni che hanno compilato nel modulo per il riferimento futuro. Tale documento è denominato documento di registrazione.

Questo articolo spiega come generare un documento di record per i moduli adattivi.

>[!NOTE]
>
>La generazione automatica del documento di record non è supportata per i moduli adattivi basati su XFA. Tuttavia, è possibile utilizzare XDP utilizzato per creare il modulo adattivo come documento di record.

## Tipi di moduli adattivi e relativi documenti di record {#adaptive-form-types-and-their-documents-of-record}

Quando si crea un modulo adattivo, è possibile selezionare un modello di modulo. Le opzioni disponibili sono:

* [Modelli di moduloConsente di selezionare un modello XFA per il modulo adattivo. ](../../forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-an-xfa-form-template)
Quando selezioni un modello XFA, puoi utilizzare il file XDP associato per il documento di record come descritto sopra.

* [XML ](../../forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-xml-or-json-schema)
SchemaConsente di selezionare una definizione di schema XML per il modulo adattivo. Quando si seleziona uno schema XML per il modulo adattivo, è possibile:

   * Associa un modello XFA per il documento del record. Assicurati che il modello XFA associato utilizzi lo stesso schema XML del modulo adattivo
   * Genera automaticamente il documento di registrazione

* Nessuno
Consente di creare un modulo adattivo senza un modello di modulo. Il documento di record viene generato automaticamente per il modulo adattivo.

Quando si seleziona un modello di modulo, configurare il documento di record utilizzando le opzioni disponibili in Configurazione modello documento di record. Vedere [Configurazione del modello del documento](#document-of-record-template-configuration).

## Documento generato automaticamente {#automatically-generated-document-of-record}

Un documento di registrazione consente ai clienti di conservare una copia del modulo inviato a scopo di stampa. Quando si genera automaticamente un documento di record, ogni volta che si modifica il modulo, il relativo documento di record viene aggiornato immediatamente. Ad esempio, è possibile rimuovere il campo di età per i clienti che selezionano Stati Uniti d’America come proprio paese. Quando tali clienti generano un documento di record, il campo età non è visibile nel documento di record.

Il documento generato automaticamente presenta i seguenti vantaggi:

* Si occupa del binding dei dati.
* Nasconde automaticamente i campi contrassegnati come esclusi dal documento al momento dell&#39;invio. Non è necessario uno sforzo supplementare.
* Consente di risparmiare tempo per la progettazione di documenti di modelli di record.
* Consente di provare stili e aspetto diversi utilizzando diversi modelli di base e scegliere lo stile e l&#39;aspetto migliori per il documento di record. Gli stili sono facoltativi e, se non si specifica lo stile, gli stili di sistema sono impostati come predefiniti.
* In questo modo qualsiasi modifica del modulo viene immediatamente riflessa nel documento di registrazione.

## Componenti per generare automaticamente un documento di record {#components-to-automatically-generate-a-document-of-record}

Per generare un documento di record per i moduli adattivi, sono necessari i seguenti componenti:

**Modulo** adattivo per il quale si desidera generare un documento di record.

**Modello di base (consigliato)** Modello XFA (file XDP) creato in AEM Designer. Il modello di base viene utilizzato per specificare le informazioni relative allo stile e al branding per il modello di documento.

Vedere [Modello di base di un documento di record](#base-template-of-a-document-of-record)

>[!NOTE]
>
>Il modello di base di un documento di record è anche chiamato meta-template di un documento di record.

**Documento del modello di record** XFA (file XDP) generato da un modulo adattivo.

Vedere [Configurazione del modello del documento](#document-of-record-template-configuration).

**Dati modulo** Informazioni compilate da un utente nel modulo adattivo. Si unisce al documento del modello di record per generare il documento di record.

## Mappatura degli elementi dei moduli adattivi {#mapping-of-adaptive-form-elements}

Nelle sezioni seguenti viene descritto come gli elementi modulo adattivi vengono visualizzati nel documento di registrazione.

### espandibili {#fields}

<table>
 <tbody>
  <tr>
   <th>Componente per moduli adattivi</th>
   <th>Componente XFA corrispondente</th>
   <th>Incluso per impostazione predefinita nel documento Modello record?</th>
   <th>Note</th>
  </tr>
  <tr>
   <td>Pulsante</td>
   <td>Pulsante</td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>Casella di selezione</td>
   <td>Casella di controllo</td>
   <td>vero</td>
   <td> </td>
  </tr>
  <tr>
   <td>Selettore data</td>
   <td>Campo data/ora</td>
   <td>vero</td>
   <td> </td>
  </tr>
  <tr>
   <td>Elenco a discesa</td>
   <td>Elenco a discesa</td>
   <td>vero</td>
   <td> </td>
  </tr>
  <tr>
   <td>Firma a mano</td>
   <td>Firma</td>
   <td>vero</td>
   <td> </td>
  </tr>
  <tr>
   <td>Casella numerica</td>
   <td>Campo numerico</td>
   <td>vero</td>
   <td> </td>
  </tr>
  <tr>
   <td>Casella password</td>
   <td>Campo password</td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>Pulsante di scelta</td>
   <td>Pulsante di scelta</td>
   <td>vero</td>
   <td> </td>
  </tr>
  <tr>
   <td>Casella di testo</td>
   <td>Campo testo</td>
   <td>vero</td>
   <td> </td>
  </tr>
  <tr>
   <td>Pulsante Ripristina</td>
   <td>Pulsante Ripristina</td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>Pulsante Invia</td>
   <td><p>Pulsante Invia per e-mail</p> <p>Pulsante Invia per HTTP</p> </td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>Termini e condizioni</td>
   <td> </td>
   <td>vero</td>
   <td> </td>
  </tr>
  <tr>
   <td>Allegato file</td>
   <td> </td>
   <td>false</td>
   <td>Non disponibile nel modello di documento. Disponibile solo nel documento di registrazione attraverso gli allegati.</td>
  </tr>
 </tbody>
</table>

### Contenitori {#containers}

<table>
 <tbody>
  <tr>
   <th>Componente per moduli adattivi</th>
   <th>Componente XFA corrispondente</th>
   <th>Note</th>
  </tr>
  <tr>
   <td>Pannello<br /> </td>
   <td>Sottomodulo<br /> </td>
   <td>Il pannello ripetibile è associato a un sottomodulo ripetibile.</td>
  </tr>
 </tbody>
</table>

### Componenti statici {#static-components}

| Componente per moduli adattivi | Componente XFA corrispondente | Note |
|---|---|---|
| Immagine | Immagine | I componenti TestoDisegno e Immagine, associati o non associati, vengono sempre visualizzati nel documento di record di un modulo adattivo basato su XSD, a meno che non vengano esclusi utilizzando le impostazioni del documento di record. |
| Testo | Testo |

>[!NOTE]
>
>Nell’interfaccia classica, sono disponibili diverse schede per la modifica delle proprietà dei campi.

### Tabelle {#tables}

I componenti della tabella dei moduli adattivi, come intestazione, piè di pagina e mappa di riga, vengono associati ai componenti XFA corrispondenti. È possibile mappare pannelli ripetibili su tabelle nel documento di registrazione.

## Modello di base di un documento di record {#base-template-of-a-document-of-record}

Il modello di base fornisce informazioni sullo stile e l&#39;aspetto del documento di record. Consente di personalizzare l&#39;aspetto predefinito del documento di record generato automaticamente. Ad esempio, aggiungere il logo della società nell’intestazione e le informazioni sul copyright nel piè di pagina del documento di registrazione. La pagina master del modello di base viene utilizzata come pagina master per il modello di documento. La pagina master può contenere informazioni quali intestazione di pagina, piè di pagina e numero di pagina che è possibile applicare al documento di record. È possibile applicare tali informazioni al documento di registrazione utilizzando il modello di base per la generazione automatica del documento di record. L’utilizzo del modello base consente di modificare le proprietà predefinite dei campi.

Seguire le [convenzioni di base del modello](#base-template-conventions) quando si progetta il modello di base.

## Convenzioni del modello di base {#base-template-conventions}

Un modello di base viene utilizzato per definire intestazione, piè di pagina, stile e aspetto di un documento di record. L’intestazione e il piè di pagina possono includere informazioni quali il logo dell’azienda e il testo del copyright. La prima pagina master del modello base viene copiata e utilizzata come pagina master per il documento del record, che contiene intestazione, piè di pagina, numero di pagina o qualsiasi altra informazione che deve essere visualizzata in tutte le pagine del documento del record. Se si utilizza un modello di base non conforme alle convenzioni del modello di base, la prima pagina master del modello di base viene ancora utilizzata nel modello di documento. Si consiglia vivamente di progettare il modello di base in base alle sue convenzioni e di utilizzarlo per la generazione automatica del documento di registrazione.

**Convenzioni delle pagine master**

* Nel modello di base, denominare il sottomodulo principale come `AF_METATEMPLATE` e la pagina master come `AF_MASTERPAGE`.

* Alla pagina master con il nome `AF_MASTERPAGE` situato sotto il sottomodulo principale `AF_METATEMPLATE` viene data la preferenza per l’estrazione di informazioni relative a intestazione, piè di pagina e stile.

* Se `AF_MASTERPAGE` è assente, viene utilizzata la prima pagina master presente nel modello base.

**Convenzioni di stile per i campi**

* Per applicare uno stile ai campi del documento record, il modello base fornisce i campi situati nel sottomodulo `AF_FIELDSSUBFORM` sotto il sottomodulo principale `AF_METATEMPLATE`.

* Le proprietà di questi campi vengono applicate ai campi del documento di registrazione. Questi campi devono seguire la convenzione di denominazione `AF_<name of field in all caps>_XFO` . Ad esempio, il nome del campo della casella di controllo deve essere `AF_CHECKBOX_XFO`.

Per creare un modello di base, eseguire le operazioni seguenti in AEM Designer.

1. Fare clic su **File > Nuovo**.
1. Selezionare l&#39;opzione **Basato su un modello**.

1. Selezionare la categoria **Forms - Documento di record**.
1. Selezionare **Modello di base DoR**.
1. Fare clic su **Avanti** e fornire le informazioni richieste.

1. (Facoltativo) Modificare lo stile e l’aspetto dei campi che si desidera applicare ai campi del documento di record.
1. Salvare il modulo.

È ora possibile utilizzare il modulo salvato come modello base per il documento di record.
Non modificare o rimuovere gli script presenti nel modello di base.

**Modifica del modello di base**

* Se non si applica alcuno stile sui campi nel modello di base, è consigliabile rimuovere tali campi dal modello di base in modo che tutti gli aggiornamenti al modello di base vengano prelevati automaticamente.
* Durante la modifica del modello di base, non rimuovere, aggiungere o modificare script.

>[!NOTE]
>
>Progettare un modello di base utilizzando le convenzioni e seguendo rigorosamente i passaggi descritti in precedenza.

## Configurazione modello del documento record {#document-of-record-template-configuration}

Configurare il modello di documento del modulo per consentire ai clienti di scaricare una copia del modulo inviato in formato cartaceo. Un file XDP funge da documento del modello di record. Il documento scaricato dai clienti del record viene formattato in base al layout specificato nel file XDP.

Per configurare un documento di record per i moduli adattivi, effettua le seguenti operazioni:

1. Nell&#39;istanza AEM autore, fai clic su **Forms > Forms e Documenti.**
1. Selezionare un modulo e fare clic su **Visualizza proprietà**.
1. Nella finestra Proprietà, tocca **Modello modulo**.
È inoltre possibile selezionare un modello di modulo quando si crea un modulo.

   >[!NOTE]
   >
   >Nella scheda Modello modulo, assicurarsi di selezionare **Schema** o **Nessuno** dal menu a discesa **Seleziona da**. **[!UICONTROL Il documento di record non è supportato per i moduli basati su XFA o adattivi con Modello di modulo come modello di modulo.]**

1. Nella sezione Configurazione modello documento della scheda Modello modulo selezionare una delle opzioni seguenti.

   **** NessunoSelezionare questa opzione se non si desidera configurare il documento di record per il modulo.

   **Associa modello di modulo come** modello di recordSelezionare questa opzione se si dispone di un file XDP che si desidera utilizzare come modello per il documento di record. Selezionando questa opzione, vengono visualizzati tutti i file XDP disponibili nell’archivio AEM Forms. Selezionare il file appropriato.

   Il file XDP selezionato viene associato al modulo adattivo.

   **Genera documento di** recordSelezionare questa opzione per utilizzare un file XDP come modello di base per definire lo stile e l&#39;aspetto del documento di record. Selezionando questa opzione, vengono visualizzati tutti i file XDP disponibili nell’archivio AEM Forms. Selezionare il file appropriato.

   >[!NOTE]
   >
   >Verificare che lo schema utilizzato per creare il modulo adattivo e lo schema (schema dati) del modulo XFA sia lo stesso se:
   >
   >
   >
   >    * Il modulo adattivo è basato su schema
   >    * Si sta utilizzando l&#39;opzione **Associa modello di modulo come modello di documento** per il documento di record


1. Fare clic su **Fine.**

## Personalizzare le informazioni sul marchio nel documento di record {#customize-the-branding-information-in-document-of-record}

Durante la generazione di un documento di record, è possibile modificare le informazioni di branding per il documento di record nella scheda Documento di record. La scheda Documento di record include opzioni quali logo, aspetto, layout, intestazione e piè di pagina, liberatoria e se si desidera includere o meno le opzioni della casella di controllo e dei pulsanti di scelta non selezionati.

Per localizzare le informazioni di branding immesse nella scheda Documento di record, è necessario assicurarsi che le impostazioni internazionali del browser siano impostate in modo appropriato. Per personalizzare le informazioni di branding del documento di registrazione, completa i seguenti passaggi:

1. Seleziona un pannello (pannello principale) nel documento di record, quindi tocca ![configura](assets/configure.png).
1. Tocca ![dortab](assets/dortab.png). Viene visualizzata la scheda Documento di record.
1. Selezionare il modello predefinito o un modello personalizzato per il rendering del documento di record. Se si seleziona il modello predefinito, sotto il menu a discesa Modello viene visualizzata una miniatura del documento di record.

   ![modello di branding](assets/brandingtemplate.png)

   Se scegli di selezionare un modello personalizzato, sfoglia e seleziona un XDP sul server AEM Forms. Se desideri utilizzare un modello che non è già sul server AEM Forms, devi prima caricare XDP sul server AEM Forms.

1. A seconda che si selezioni un modello predefinito o personalizzato, nella scheda Documento di record vengono visualizzate alcune o tutte le proprietà seguenti. Specifica in modo appropriato:

   * **Immagine** logo: Puoi scegliere di utilizzare l’immagine logo nel modulo adattivo, sceglierne uno da DAM o caricarne uno dal computer.
   * **Titolo modulo**
   * **Testo intestazione**
   * **Etichetta di dichiarazione di non responsabilità**
   * **Liberatoria**
   * **Testo della liberatoria**
   * **Colore** accento: Colore in cui viene eseguito il rendering del testo dell&#39;intestazione e delle linee di separazione nel documento o nel record PDF
   * **Famiglia** font: Famiglia di font del testo nel documento PDF del record
   * **Per i componenti Casella di controllo e Pulsante di scelta, mostrare solo i valori selezionati**
   * **Separatore per più valori selezionati**
   * **Includi oggetti modulo non associati a modelli dati**
   * **Escludere i campi nascosti dal documento del record**
   * **Nascondi descrizione pannelli**

   >[!NOTE]
   >
   >Se si utilizza un modello di modulo adattivo creato con una versione di Designer precedente alla versione 6.3, affinché le proprietà Colore accento e Famiglia font funzionino, assicurarsi che quanto segue sia presente nel modello di modulo adattivo sotto il sottomodulo principale:

   ```xml
   <proto>
   <font typeface="Arial"/>
   <fill>
   <color value="4,166,203"/>
   </fill>
   <edge>
   <color value="4,166,203"/>
   </edge>
   </proto>
   ```

1. Per salvare le modifiche di branding, tocca Fine.

## Layout di tabelle e colonne per pannelli nel documento di registrazione {#table-and-column-layouts-for-panels-in-document-of-record}

Il modulo adattivo può essere lungo e contenere diversi campi del modulo. Potrebbe non essere necessario salvare un documento di record come copia esatta del modulo adattivo. Ora è possibile scegliere il layout di una tabella o di una colonna per salvare uno o più pannelli di moduli adattivi nel documento PDF del record.

Prima di generare un documento di record, nelle impostazioni di un pannello selezionare Layout per il documento di record per tale pannello come Tabella o Colonna. I campi nel pannello vengono organizzati di conseguenza nel documento di registrazione.

![Campi di un pannello di cui è stato eseguito il rendering in un layout di tabella nel documento del record](assets/dortablelayout.png)

Campi di un pannello di cui è stato eseguito il rendering in un layout di tabella nel documento del record

![Rendering dei campi in un pannello con layout a colonne nel documento del record](assets/dorcolumnlayout.png)

Rendering dei campi in un pannello con layout a colonne nel documento del record

## Impostazioni del documento di registrazione {#document-of-record-settings}

Le impostazioni del documento di record consentono di scegliere le opzioni che si desidera includere nel documento di record. Ad esempio, una banca accetta un modulo nome, età, numero di previdenza sociale e numero di telefono. Il modulo genera un numero di conto bancario e i dettagli della filiale. È possibile scegliere di visualizzare solo il nome, il numero di previdenza sociale, il conto bancario e i dettagli del ramo nel documento di registrazione.

Il documento delle impostazioni di record di un componente è disponibile sotto le relative proprietà. Per accedere alle proprietà di un componente, selezionalo e fai clic su ![cmppr](assets/cmppr.png) nella sovrapposizione. Le proprietà sono elencate nella barra laterale ed è possibile trovare le seguenti impostazioni.

**Impostazioni a livello di campo**

* **Escludi Dal Documento Di Registrazione**: L&#39;impostazione della proprietà su true esclude il campo dal documento del record. Si tratta di una proprietà modificabile in script denominata `excludeFromDoR`. Il suo comportamento dipende dalla proprietà **Escludi campi da DoR se nascosta** a livello di modulo.

* **Visualizza il pannello come tabella:** l’impostazione della proprietà mostra il pannello come tabella nel documento di registrazione se il pannello contiene meno di 6 campi. Applicabile solo al pannello.
* **Escludi titolo dal documento di record:** l&#39;impostazione della proprietà esclude il titolo del pannello/tabella dal documento di record. Applicabile solo ai pannelli e alle tabelle.
* **Escludi descrizione dal documento di record:** l&#39;impostazione della proprietà esclude la descrizione del pannello/tabella dal documento di record. Applicabile solo ai pannelli e alle tabelle.

**Impostazioni a livello di modulo**

* **Includi campi non associati in DoR:** l’impostazione della proprietà include campi non associati di un modulo adattivo basato su schema nel documento di record. Per impostazione predefinita è true.
* **Escludi i campi dal DoR se nascosti:** l’impostazione della proprietà sostituisce il comportamento della proprietà a livello di campo &quot;Escludi dal documento di record&quot; quando non è vera. Se i campi sono nascosti al momento dell’invio del modulo, verranno esclusi dal documento se la proprietà è impostata su true, purché la proprietà &quot;Escludi dal documento di record&quot; non sia impostata.

## Considerazioni chiave durante l&#39;utilizzo del documento di record {#key-considerations-when-working-with-document-of-record}

Quando si lavora su un documento di record per i moduli adattivi, tenere presente le considerazioni e le limitazioni seguenti.

* I modelli dei documenti non supportano il testo RTF. Pertanto, qualsiasi testo RTF nel modulo adattivo statico o nelle informazioni inserite dall’utente finale viene visualizzato come testo normale nel documento di registrazione.
* I frammenti di documento in un modulo adattivo non vengono visualizzati nel documento di registrazione. Tuttavia, i frammenti di modulo adattivo sono supportati.
* Il binding del contenuto nel documento di record generato per il modulo adattivo basato su schema XML non è supportato.
* La versione localizzata del documento di record viene creata su richiesta per un&#39;impostazione internazionale quando l&#39;utente richiede il rendering del documento di record. La localizzazione del documento di record avviene insieme alla localizzazione del modulo adattivo. Per ulteriori informazioni sulla localizzazione di documenti di record e moduli adattivi, vedere [Utilizzo AEM flusso di lavoro di traduzione per localizzare moduli adattivi e documenti di record](/help/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.md).

