---
title: Genera documento di registrazione per i moduli adattivi
seo-title: Genera documento di registrazione per i moduli adattivi
description: Spiega come generare un modello per un documento di record (DoR) per i moduli adattivi.
seo-description: Spiega come generare un modello per un documento di record (DoR) per i moduli adattivi.
uuid: 2dc7e0de-fff9-43fa-9426-e9b047eb2595
content-type: reference
topic-tags: adaptive_forms, develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ce65cb5f-94ec-4423-9fa9-d617e9703091
docset: aem65
translation-type: tm+mt
source-git-commit: fa3d5923784a8d89e2b440412d2b88790de3e39e
workflow-type: tm+mt
source-wordcount: '2663'
ht-degree: 3%

---


# Genera documento record per moduli adattivi{#generate-document-of-record-for-adaptive-forms}

## Panoramica {#overview}

Dopo l&#39;invio di un modulo, i clienti desiderano in genere tenere un record, in formato cartaceo o in formato documento, delle informazioni che hanno compilato nel modulo per il riferimento futuro. Tale documento è denominato documento di registrazione.

In questo articolo viene illustrato come generare un documento di record per i moduli adattivi.

>[!NOTE]
>
>La generazione automatica del documento di record non è supportata per i moduli adattivi basati su XFA. Tuttavia, è possibile utilizzare l&#39;XDP utilizzato per creare il modulo adattivo come documento di record.

## Tipi di moduli adattivi e relativi documenti di record {#adaptive-form-types-and-their-documents-of-record}

Quando si crea un modulo adattivo, è possibile selezionare un modello di modulo. Le opzioni disponibili sono:

* [](../../forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-an-xfa-form-template)
Modelli modulo: consente di selezionare un modello XFA per il modulo adattivo. Quando selezionate un modello XFA, potete utilizzare il file XDP associato per il documento del record come descritto sopra.

* [XML ](../../forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-xml-or-json-schema)
Schema: consente di selezionare una definizione di schema XML per il modulo adattivo. Quando si seleziona uno schema XML per il modulo adattivo, è possibile:

   * Associate un modello XFA per il documento del record. Verificare che il modello XFA associato utilizzi lo stesso schema XML del modulo adattivo
   * Genera automaticamente documento record

* None
Consente di creare un modulo adattivo senza un modello di modulo. Il documento di record viene generato automaticamente per il modulo adattivo.

Quando si seleziona un modello di modulo, configurare il documento di record utilizzando le opzioni disponibili in Configurazione modello documento di record. Vedere [Configurazione del modello del documento di registrazione](#document-of-record-template-configuration).

## Documento generato automaticamente {#automatically-generated-document-of-record}

Un documento di registrazione consente ai clienti di conservare una copia del modulo inviato a scopo di stampa. Quando si genera automaticamente un documento record, ogni volta che si modifica il modulo, il relativo documento record viene aggiornato immediatamente. Ad esempio, è possibile rimuovere il campo di età per i clienti che scelgono Stati Uniti d&#39;America come proprio paese. Quando tali clienti generano un documento di registrazione, il campo age non è visibile nel documento di registrazione.

Il documento generato automaticamente presenta i seguenti vantaggi:

* Si occupa del binding dei dati.
* Nasconde automaticamente i campi contrassegnati come esclusi dal documento al momento dell&#39;invio. Non è richiesto alcun sforzo supplementare.
* Consente di risparmiare tempo per la progettazione del modello di documento.
* Consente di provare stili e aspetto diversi utilizzando diversi modelli di base e di scegliere lo stile e l’aspetto migliori per il documento di registrazione. L&#39;aspetto dello stile è facoltativo e, se non si specifica lo stile, gli stili di sistema sono impostati come predefiniti.
* Garantisce che qualsiasi modifica del modulo venga immediatamente riflessa nel documento di registrazione.

## Componenti per generare automaticamente un documento di record {#components-to-automatically-generate-a-document-of-record}

Per generare un documento di record per i moduli adattivi, sono necessari i seguenti componenti:

**Modulo** adattivo per il quale si desidera generare un documento record.

**Modello di base (consigliato)modello** XFA (file XDP) creato in AEM Designer. Il modello di base viene utilizzato per specificare lo stile e le informazioni sul marchio per il modello del documento del record.

Vedere [Modello di base di un documento record](#base-template-of-a-document-of-record)

>[!NOTE]
>
>Il modello di base di un documento di record è anche denominato meta-template di un documento di record.

**Documento del modello** XFA record (file XDP) generato da un modulo adattivo.

Vedere [Configurazione del modello del documento di registrazione](#document-of-record-template-configuration).

**Dati** modulo: informazioni compilate da un utente nel modulo adattivo. Viene unito al modello del documento per generare il documento del record.

## Mappatura di elementi modulo adattivi {#mapping-of-adaptive-form-elements}

Le sezioni seguenti descrivono l’aspetto degli elementi modulo adattivi nel documento di record.

### espandibili {#fields}

<table>
 <tbody>
  <tr>
   <th>Componente modulo adattivo</th>
   <th>Componente XFA corrispondente</th>
   <th>Incluso per impostazione predefinita nel modello del documento?</th>
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
   <td>Firma scarabocchio</td>
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
   <td>Non disponibile nel modello del documento. Disponibile solo nel documento di registrazione attraverso gli allegati.</td>
  </tr>
 </tbody>
</table>

### Contenitori {#containers}

<table>
 <tbody>
  <tr>
   <th>Componente modulo adattivo</th>
   <th>Componente XFA corrispondente</th>
   <th>Note</th>
  </tr>
  <tr>
   <td>Pannello<br /> </td>
   <td>Sottomodulo<br /> </td>
   <td>Il pannello ripetibile viene mappato su un sottomodulo ripetibile.</td>
  </tr>
 </tbody>
</table>

### Componenti statici {#static-components}

| Componente modulo adattivo | Componente XFA corrispondente | Note |
|---|---|---|
| Immagine | Immagine | I componenti TestoDisegno e Immagine, associati o non associati, vengono sempre visualizzati nel documento record di un modulo adattivo basato su XSD, a meno che non venga escluso utilizzando le impostazioni del documento dei record. |
| Testo | Testo |

>[!NOTE]
>
>Nell’interfaccia classica, sono disponibili diverse schede per la modifica delle proprietà dei campi.

### Tabelle {#tables}

I componenti della tabella dei moduli adattivi, ad esempio intestazione, piè di pagina e riga, vengono mappati sui componenti XFA corrispondenti. È possibile mappare i pannelli ripetibili alle tabelle nel documento di registrazione.

## Modello di base di un documento di record {#base-template-of-a-document-of-record}

Il modello di base fornisce informazioni sullo stile e l&#39;aspetto al documento del record. Consente di personalizzare l&#39;aspetto predefinito del documento di record generato automaticamente. Ad esempio, è necessario aggiungere il logo aziendale nell&#39;intestazione e le informazioni sul copyright nel piè di pagina del documento di registrazione. La pagina master del modello di base viene utilizzata come pagina master per il modello di documento del record. La pagina master può contenere informazioni quali l&#39;intestazione della pagina, il piè di pagina e il numero di pagina che è possibile applicare al documento del record. È possibile applicare tali informazioni al documento di registrazione utilizzando il modello di base per la generazione automatica del documento di record. L&#39;utilizzo del modello base consente di modificare le proprietà predefinite dei campi.

Seguire le [convenzioni di base per i modelli](#base-template-conventions) quando si progetta un modello di base.

## Convenzioni dei modelli di base {#base-template-conventions}

Un modello di base viene utilizzato per definire l’intestazione, il piè di pagina, lo stile e l’aspetto di un documento del record. L’intestazione e il piè di pagina possono includere informazioni come il logo aziendale e il testo del copyright. La prima pagina master nel modello base viene copiata e utilizzata come pagina master per il documento del record, che contiene intestazione, piè di pagina, numero di pagina o qualsiasi altra informazione da visualizzare in tutte le pagine del documento del record. Se si utilizza un modello di base non conforme alle convenzioni del modello di base, la prima pagina master del modello di base viene comunque utilizzata nel modello di documento del record. Si consiglia vivamente di progettare il modello di base in base alle convenzioni e di utilizzarlo per la generazione automatica del documento di registrazione.

**Convenzioni per le pagine master**

* Nel modello di base, assegnare al sottomodulo principale il nome `AF_METATEMPLATE` e alla pagina master il nome `AF_MASTERPAGE`.

* Alla pagina master con il nome `AF_MASTERPAGE` che si trova sotto il sottomodulo principale `AF_METATEMPLATE` viene assegnata la preferenza per l&#39;estrazione di informazioni su intestazione, piè di pagina e stile.

* Se `AF_MASTERPAGE` è assente, viene utilizzata la prima pagina master presente nel modello di base.

**Convenzioni di stile per i campi**

* Per applicare lo stile ai campi nel documento del record, il modello di base fornisce i campi situati nel sottomodulo `AF_FIELDSSUBFORM` sotto il sottomodulo principale `AF_METATEMPLATE`.

* Le proprietà di questi campi sono applicate ai campi nel documento di record. Questi campi devono seguire la convenzione di denominazione `AF_<name of field in all caps>_XFO`. Ad esempio, il nome del campo per la casella di controllo deve essere `AF_CHECKBOX_XFO`.

Per creare un modello di base, effettuare le seguenti operazioni in AEM Designer.

1. Fare clic su **File > Nuovo**.
1. Selezionare l&#39;opzione **Basato su un modello**.

1. Selezionare la categoria **Forms - Documento di registrazione**.
1. Selezionare **Modello di base DoR**.
1. Fare clic su **Next** e fornire le informazioni richieste.

1. (Facoltativo) Modificare lo stile e l&#39;aspetto dei campi che si desidera applicare ai campi nel documento del record.
1. Salvare il modulo.

È ora possibile utilizzare il modulo salvato come modello di base per il documento record.
Non modificate o rimuovete gli script presenti nel modello di base.

**Modifica del modello di base**

* Se non si applica alcuno stile ai campi nel modello di base, è consigliabile rimuovere tali campi dal modello di base, in modo che tutti gli aggiornamenti al modello di base vengano prelevati automaticamente.
* Durante la modifica del modello di base, non rimuovere, aggiungere o modificare gli script.

>[!NOTE]
>
>Progettare i modelli di base utilizzando le convenzioni e seguendo rigorosamente i passaggi descritti in precedenza.

## Configurazione modello del documento record {#document-of-record-template-configuration}

Configurare il modello del documento di record del modulo per consentire ai clienti di scaricare una copia del modulo inviato in formato cartaceo. Un file XDP funge da modello del documento del record. Il documento di record scaricato dai clienti viene formattato in base al layout specificato nel file XDP.

Per configurare un documento di record per i moduli adattivi, procedere come segue:

1. AEM&#39;istanza di creazione, fare clic su **Forms > Forms e documenti.**
1. Selezionare un modulo e fare clic su **Visualizza proprietà**.
1. Nella finestra Proprietà, toccare **Modello modulo**.
È inoltre possibile selezionare un modello di modulo al momento della creazione del modulo.

   >[!NOTE]
   >
   >Nella scheda Modello modulo, assicurarsi di selezionare **Schema** o **None** dal menu a discesa **Seleziona da**. **[!UICONTROL Il documento del record non è supportato per i moduli XFA basati su moduli adattivi con il modello di modulo come modello di modulo.]**

1. Nella sezione Configurazione modello documento di record della scheda Modello di modulo, selezionare una delle opzioni seguenti.

   **** Nessuno: selezionare questa opzione se non si desidera configurare il documento record per il modulo.

   **Associa modello di modulo come** modello di documento di registrazione: selezionare questa opzione se si dispone di un file XDP che si desidera utilizzare come modello per il documento di record. Selezionando questa opzione, vengono visualizzati tutti i file XDP disponibili  archivio AEM Forms. Selezionare il file appropriato.

   Il file XDP selezionato viene associato al modulo adattivo.

   **Genera documento del** record: selezionare questa opzione per utilizzare un file XDP come modello di base per definire lo stile e l&#39;aspetto del documento del record. Selezionando questa opzione, vengono visualizzati tutti i file XDP disponibili  archivio AEM Forms. Selezionare il file appropriato.

   >[!NOTE]
   >
   >Verificare che lo schema utilizzato per creare il modulo adattivo e lo schema (schema dati) del modulo XFA sia lo stesso se:
   >
   >
   >
   >    * Il modulo adattivo è basato su schema
   >    * Per il documento di record si utilizza l&#39;opzione **Associa modello modulo come documento di record**


1. Fare clic su **Fine.**

## Personalizzare le informazioni sul marchio nel documento di registrazione {#customize-the-branding-information-in-document-of-record}

Durante la generazione di un documento di record, è possibile modificare le informazioni di branding per il documento di record nella scheda Documento di record. La scheda Documento di record include opzioni quali logo, aspetto, layout, intestazione e piè di pagina, dichiarazione di non responsabilità e se si desidera includere o meno le opzioni di casella di controllo e pulsante di scelta non selezionate.

Per localizzare le informazioni di branding immesse nella scheda Documento record, è necessario assicurarsi che le impostazioni internazionali del browser siano impostate correttamente. Per personalizzare le informazioni di branding del documento di registrazione, completare i seguenti passaggi:

1. Selezionate un pannello (pannello principale) nel documento del record, quindi toccate ![configure](assets/configure.png).
1. Toccate ![dortab](assets/dortab.png). Viene visualizzata la scheda Documento di registrazione.
1. Selezionare il modello predefinito o un modello personalizzato per il rendering del documento del record. Se selezionate il modello predefinito, sotto il menu a discesa Modello viene visualizzata una miniatura di anteprima del documento di record.

   ![brandingtemplate](assets/brandingtemplate.png)

   Se scegliete di selezionare un modello personalizzato, individuate un file XDP da selezionare sul server AEM Forms . Se desiderate utilizzare un modello che non è già presente nel server AEM Forms , dovete prima caricare l&#39;XDP nel server AEM Forms .

1. A seconda che sia selezionato un modello predefinito o personalizzato, nella scheda Documento di record vengono visualizzate tutte o alcune delle proprietà seguenti. Specificate i seguenti parametri:

   * **Immagine** logo: Potete scegliere di utilizzare l&#39;immagine logo nel modulo adattivo, sceglierne una da DAM o caricarne una dal computer.
   * **Titolo modulo**
   * **Testo intestazione**
   * **Etichetta di dichiarazione di non responsabilità**
   * **Liberatoria**
   * **Testo della liberatoria**
   * **Colore** accento: Colore in cui viene eseguito il rendering del testo dell&#39;intestazione e delle linee di separazione nel documento o nel record PDF
   * **Famiglia** font: Famiglia di font del testo nel documento PDF del record
   * **Per i componenti Casella di controllo e Pulsante di scelta, mostrare solo i valori selezionati**
   * **Separatore per più valori selezionati**
   * **Includi oggetti modulo non associati al modello dati**
   * **Escludere i campi nascosti dal documento record**
   * **Nascondi descrizione pannelli**

   >[!NOTE]
   >
   >Se si utilizza un modello di modulo adattivo creato con una versione di Designer precedente alla 6.3, per il funzionamento delle proprietà Colore accento e Famiglia font, assicurarsi che quanto segue sia presente nel modello di modulo adattivo sotto il sottomodulo principale:

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

1. Per salvare le modifiche al marchio, toccate Fine.

## Layout di tabelle e colonne per i pannelli in Documento di registrazione {#table-and-column-layouts-for-panels-in-document-of-record}

Il modulo adattivo può essere lungo e contenere più campi modulo. È possibile che non si desideri salvare un documento come copia esatta del modulo adattivo. Ora è possibile scegliere un layout di tabella o colonna per salvare uno o più pannelli di moduli adattivi nel documento PDF del record.

Prima di generare un documento di registrazione, nelle impostazioni di un pannello selezionare Layout per il documento di registrazione per tale pannello come Tabella o Colonna. I campi nel pannello vengono organizzati di conseguenza nel documento del record.

![Rendering dei campi in un pannello in un layout di tabella nel documento del record](assets/dortablelayout.png)

Rendering dei campi in un pannello in un layout di tabella nel documento del record

![Rendering dei campi di un pannello in un layout di colonna nel documento del record](assets/dorcolumnlayout.png)

Rendering dei campi di un pannello in un layout di colonna nel documento del record

## Impostazioni documento record {#document-of-record-settings}

Le impostazioni del documento dei record consentono di scegliere le opzioni che si desidera includere nel documento dei record. Ad esempio, una banca accetta nome, età, numero di previdenza sociale e numero di telefono in un modulo. Il modulo genera un numero di conto bancario e i dettagli della filiale. Potete scegliere di visualizzare solo il nome, il numero di previdenza sociale, il conto bancario e i dettagli del ramo nel documento del record.

Le impostazioni del documento di record di un componente sono disponibili nelle relative proprietà. Per accedere alle proprietà di un componente, selezionate il componente e fate clic su ![cmppr](assets/cmppr.png) nella sovrapposizione. Le proprietà sono elencate nella barra laterale ed è possibile trovare le seguenti impostazioni.

**Impostazioni a livello di campo**

* **Escludi Dal Documento Di Record**: Impostando la proprietà su true il campo viene escluso dal documento del record. Si tratta di una proprietà che può essere utilizzata come script denominata `excludeFromDoR`. Il suo comportamento dipende dalla proprietà a livello di modulo **Exclude fields from DoR if hidden**.

* **Visualizza il pannello come tabella:** Impostando la proprietà, il pannello viene visualizzato come tabella nel documento record se il pannello contiene meno di 6 campi. Applicabile solo al pannello.
* **Escludi titolo dal documento di registrazione:** l&#39;impostazione della proprietà esclude il titolo del pannello/tabella dal documento di registrazione. Applicabile solo al pannello e alla tabella.
* **Escludi descrizione dal documento di registrazione:** l&#39;impostazione della proprietà esclude la descrizione del pannello/tabella dal documento di registrazione. Applicabile solo al pannello e alla tabella.

**Impostazioni a livello di modulo**

* **Includi campi non associati in DoR:** l&#39;impostazione della proprietà include campi non associati da modulo adattivo basato su schema nel documento record. Per impostazione predefinita è true.
* **Escludi i campi dal DoR se nascosta:** l&#39;impostazione della proprietà sostituisce il comportamento della proprietà a livello di campo &quot;Escludi dal documento del record&quot; quando non è vera. Se i campi sono nascosti al momento dell&#39;invio del modulo, saranno esclusi dal documento se la proprietà è impostata su true, purché la proprietà &quot;Escludi dal documento di registrazione&quot; non sia impostata.

## Considerazioni chiave per l&#39;utilizzo del documento di record {#key-considerations-when-working-with-document-of-record}

Quando si lavora su un documento di record per i moduli adattivi, tenere presente le considerazioni e le limitazioni seguenti.

* Il documento dei modelli di record non supporta il testo RTF. Di conseguenza, il testo RTF nel modulo adattivo statico o nelle informazioni compilate dall’utente finale viene visualizzato come testo normale nel documento del record.
* I frammenti di documento in un modulo adattivo non vengono visualizzati nel documento del record. Tuttavia, i frammenti di modulo adattivo sono supportati.
* Il binding del contenuto nel documento del record generato per il modulo adattivo basato su schema XML non è supportato.
* La versione localizzata del documento del record viene creata su richiesta per una lingua quando l&#39;utente richiede il rendering del documento del record. La localizzazione del documento del record avviene insieme alla localizzazione del modulo adattivo. Per ulteriori informazioni sulla localizzazione di documenti di record e moduli adattivi, vedere [Utilizzo AEM flusso di lavoro di traduzione per localizzare moduli adattivi e documenti di record](/help/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.md).

