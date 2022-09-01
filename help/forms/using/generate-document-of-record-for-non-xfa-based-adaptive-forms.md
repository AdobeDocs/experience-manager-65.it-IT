---
title: Genera documento di record per i moduli adattivi
seo-title: Generate Document of Record for adaptive forms
description: Spiega come generare un modello per un documento di record (DoR) per i moduli adattivi.
seo-description: Explains how you can generate a template for a document of record (DoR) for adaptive forms.
uuid: 2dc7e0de-fff9-43fa-9426-e9b047eb2595
content-type: reference
topic-tags: adaptive_forms, develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ce65cb5f-94ec-4423-9fa9-d617e9703091
docset: aem65
feature: Adaptive Forms
exl-id: 7240897f-6b3a-427a-abc6-66310c2998f3
source-git-commit: 9ee8e79777b89fbf4d6e5b5fd1dbb1ef3bc9ad5d
workflow-type: tm+mt
source-wordcount: '3483'
ht-degree: 2%

---

# Genera documento di record per i moduli adattivi{#generate-document-of-record-for-adaptive-forms}

## Panoramica {#overview}

Dopo l&#39;invio di un modulo, i clienti in genere desiderano conservare un record, in formato cartaceo o in formato documento, delle informazioni che hanno compilato nel modulo per il riferimento futuro. Tale documento è denominato documento di registrazione.

Questo articolo spiega come generare un documento di record per i moduli adattivi.

>[!NOTE]
>
>La generazione automatica del documento di record non è supportata per i moduli adattivi basati su XFA. Tuttavia, è possibile utilizzare XDP utilizzato per creare il modulo adattivo come documento di record.

## Tipi di moduli adattivi e relativi documenti di registrazione {#adaptive-form-types-and-their-documents-of-record}

Quando si crea un modulo adattivo, è possibile selezionare un modello di modulo. Le opzioni disponibili sono:

* [Modelli di modulo](../../forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-an-xfa-form-template)
Consente di selezionare un modello XFA per il modulo adattivo. Quando selezioni un modello XFA, puoi utilizzare il file XDP associato per il documento di record come descritto sopra.

* [Schema XML](../../forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-xml-or-json-schema)
Consente di selezionare una definizione di schema XML per il modulo adattivo. Quando si seleziona uno schema XML per il modulo adattivo, è possibile:

   * Associa un modello XFA per il documento del record. Assicurati che il modello XFA associato utilizzi lo stesso schema XML del modulo adattivo
   * Genera automaticamente il documento di registrazione

* Nessuno Consente di creare un modulo adattivo senza un modello di modulo. Il documento di record viene generato automaticamente per il modulo adattivo.

Quando si seleziona un modello di modulo, configurare il documento di record utilizzando le opzioni disponibili in Configurazione modello documento di record. Vedi [Configurazione del modello del documento di record](#document-of-record-template-configuration).

## Documento generato automaticamente {#automatically-generated-document-of-record}

Un documento di registrazione consente ai clienti di conservare una copia del modulo inviato a scopo di stampa. Quando si genera automaticamente un documento di record, ogni volta che si modifica il modulo, il relativo documento di record viene aggiornato immediatamente. Ad esempio, è possibile rimuovere il campo di età per i clienti che selezionano Stati Uniti d’America come proprio paese. Quando tali clienti generano un documento di record, il campo età non è visibile nel documento di record.

Il documento generato automaticamente presenta i seguenti vantaggi:

* Si occupa del binding dei dati.
* Nasconde automaticamente i campi contrassegnati come esclusi dal documento al momento dell&#39;invio. Non è necessario uno sforzo supplementare.
* Consente di risparmiare tempo per la progettazione di documenti di modelli di record.
* Consente di provare stili e aspetto diversi utilizzando diversi modelli di base e scegliere lo stile e l&#39;aspetto migliori per il documento di record. Gli stili sono facoltativi e, se non si specifica lo stile, gli stili di sistema sono impostati come predefiniti.
* In questo modo qualsiasi modifica del modulo viene immediatamente riflessa nel documento di registrazione.

## Componenti per generare automaticamente un documento di registrazione {#components-to-automatically-generate-a-document-of-record}

Per generare un documento di record per i moduli adattivi, sono necessari i seguenti componenti:

**Modulo adattivo** Modulo adattivo per il quale si desidera generare un documento di record.

**Modello di base (consigliato)** Modello XFA (file XDP) creato in AEM Designer. Il modello di base viene utilizzato per specificare le informazioni relative allo stile e al branding per il modello di documento.

Vedi [Modello di base di un documento di registrazione](#base-template-of-a-document-of-record)

>[!NOTE]
>
>Il modello di base di un documento di record è anche chiamato meta-template di un documento di record.

**Documento del modello di record** Modello XFA (file XDP) generato da un modulo adattivo.

Vedi [Configurazione del modello del documento di record](#document-of-record-template-configuration).

**Dati modulo** Informazioni inserite da un utente nel modulo adattivo. Si unisce al documento del modello di record per generare il documento di record.

## Mappatura degli elementi dei moduli adattivi {#mapping-of-adaptive-form-elements}

Nelle sezioni seguenti viene descritto come gli elementi modulo adattivi vengono visualizzati nel documento di registrazione.

### Campi {#fields}

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

## Modello di base di un documento di registrazione {#base-template-of-a-document-of-record}

Il modello di base fornisce informazioni sullo stile e l&#39;aspetto del documento di record. Consente di personalizzare l&#39;aspetto predefinito del documento di record generato automaticamente. Ad esempio, aggiungere il logo della società nell’intestazione e le informazioni sul copyright nel piè di pagina del documento di registrazione. La pagina master del modello di base viene utilizzata come pagina master per il modello di documento. La pagina master può contenere informazioni quali intestazione di pagina, piè di pagina e numero di pagina che è possibile applicare al documento di record. È possibile applicare tali informazioni al documento di registrazione utilizzando il modello di base per la generazione automatica del documento di record. L’utilizzo del modello base consente di modificare le proprietà predefinite dei campi.

Segui [Convenzioni dei modelli di base](#base-template-conventions) quando si progetta un modello di base.

## Convenzioni dei modelli di base {#base-template-conventions}

Un modello di base viene utilizzato per definire intestazione, piè di pagina, stile e aspetto di un documento di record. L’intestazione e il piè di pagina possono includere informazioni quali il logo dell’azienda e il testo del copyright. La prima pagina master del modello base viene copiata e utilizzata come pagina master per il documento del record, che contiene intestazione, piè di pagina, numero di pagina o qualsiasi altra informazione che deve essere visualizzata in tutte le pagine del documento del record. Se si utilizza un modello di base non conforme alle convenzioni del modello di base, la prima pagina master del modello di base viene ancora utilizzata nel modello di documento. Si consiglia vivamente di progettare il modello di base in base alle sue convenzioni e di utilizzarlo per la generazione automatica del documento di registrazione.

**Convenzioni delle pagine master**

* Nel modello di base, assegnare al sottomodulo principale un nome come `AF_METATEMPLATE` e la pagina master come `AF_MASTERPAGE`.

* La pagina master con il nome `AF_MASTERPAGE` situato sotto `AF_METATEMPLATE` al sottomodulo principale viene data la preferenza per l’estrazione di informazioni relative a intestazione, piè di pagina e stile.

* Se `AF_MASTERPAGE` è assente, viene utilizzata la prima pagina master presente nel modello base.

**Convenzioni di stile per i campi**

* Per applicare lo stile ai campi del documento di record, il modello di base fornisce i campi che si trovano nel `AF_FIELDSSUBFORM` sotto il `AF_METATEMPLATE` sottomodulo principale.

* Le proprietà di questi campi vengono applicate ai campi del documento di registrazione. Questi campi devono seguire `AF_<name of field in all caps>_XFO` convenzione di denominazione. Ad esempio, il nome del campo per la casella di controllo deve essere `AF_CHECKBOX_XFO`.

Per creare un modello di base, eseguire le operazioni seguenti in AEM Designer.

1. Fai clic su **File > Nuovo**.
1. Seleziona la **Basato su un modello** opzione .

1. Seleziona la **Forms - Documento di registrazione** categoria.
1. Seleziona **Modello di base DoR**.
1. Fai clic su **Successivo** e fornire le informazioni richieste.

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

1. Nell’istanza AEM autore, fai clic su **Forms > Forms e documenti.**
1. Selezionare un modulo e fare clic su **Visualizza proprietà**.
1. Nella finestra Proprietà, tocca **Modello Modulo**.
È inoltre possibile selezionare un modello di modulo quando si crea un modulo.

   >[!NOTE]
   >
   >Nella scheda Modello modulo, assicurarsi di selezionare **Schema** o **Nessuno** dal **Seleziona da** a discesa. **[!UICONTROL Il documento di record non è supportato per i moduli basati su XFA o adattivi con Modello di modulo come modello di modulo.]**

1. Nella sezione Configurazione modello documento della scheda Modello modulo selezionare una delle opzioni seguenti.

   **Nessuno** Selezionare questa opzione se non si desidera configurare il documento di record per il modulo.

   **Associa modello di modulo come modello di documento di record** Selezionare questa opzione se si dispone di un file XDP che si desidera utilizzare come modello per il documento di record. Selezionando questa opzione, vengono visualizzati tutti i file XDP disponibili nell’archivio AEM Forms. Selezionare il file appropriato.

   Il file XDP selezionato viene associato al modulo adattivo.

   **Genera documento di registrazione** Selezionare questa opzione per utilizzare un file XDP come modello di base per definire lo stile e l&#39;aspetto del documento di record. Selezionando questa opzione, vengono visualizzati tutti i file XDP disponibili nell’archivio AEM Forms. Selezionare il file appropriato.

   >[!NOTE]
   >
   >Verificare che lo schema utilizzato per creare il modulo adattivo e lo schema (schema dati) del modulo XFA sia lo stesso se:
   >
   >
   >
   >    * Il modulo adattivo è basato su schema
   >    * Stai utilizzando **Associa modello di modulo come modello del documento di record** opzione per il documento di registrazione


1. Fai clic su **Fatto.**

## Personalizzare le informazioni sul marchio nel documento di registrazione {#customize-the-branding-information-in-document-of-record}

Durante la generazione di un documento di record, è possibile modificare le informazioni di branding per il documento di record nella scheda Documento di record. La scheda Documento di record include opzioni quali logo, aspetto, layout, intestazione e piè di pagina, liberatoria e se si desidera includere o meno le opzioni della casella di controllo e dei pulsanti di scelta non selezionati.

Per localizzare le informazioni di branding immesse nella scheda Documento di record, è necessario assicurarsi che le impostazioni internazionali del browser siano impostate in modo appropriato. Per personalizzare le informazioni di branding del documento di registrazione, completa i seguenti passaggi:

1. Seleziona un pannello (pannello principale) nel documento del record, quindi tocca ![configurare](assets/configure.png).
1. Tocca ![scheda](assets/dortab.png). Viene visualizzata la scheda Documento di record.
1. Selezionare il modello predefinito o un modello personalizzato per il rendering del documento di record. Se si seleziona il modello predefinito, sotto il menu a discesa Modello viene visualizzata una miniatura del documento di record.

   ![modello di branding](assets/brandingtemplate.png)

   Se scegli di selezionare un modello personalizzato, sfoglia e seleziona un XDP sul server AEM Forms. Se desideri utilizzare un modello che non è già sul server AEM Forms, devi prima caricare XDP sul server AEM Forms.

1. A seconda che si selezioni un modello predefinito o personalizzato, nella scheda Documento di record vengono visualizzate alcune o tutte le proprietà seguenti. Specifica in modo appropriato:

   * **Immagine del logo**: Puoi scegliere di utilizzare l’immagine logo nel modulo adattivo, sceglierne uno da DAM o caricarne uno dal computer.
   * **Titolo modulo**
   * **Testo intestazione**
   * **Etichetta di dichiarazione di non responsabilità**
   * **Liberatoria**
   * **Testo della liberatoria**
   * **Colore accento**: Colore in cui viene eseguito il rendering del testo dell&#39;intestazione e delle righe separatore nel documento o nel PDF record
   * **Famiglia di font**: Famiglia di font del testo nel documento di record PDF
   * **Per i componenti Casella di controllo e Pulsante di scelta, mostrare solo i valori selezionati**
   * **Separatore per più valori selezionati**
   * **Includi oggetti modulo non associati a modelli dati**
   * **Escludere i campi nascosti dal documento del record**
   * **Nascondi descrizione pannelli**

   Se il modello XDP personalizzato selezionato include più pagine master, le proprietà di tali pagine vengono visualizzate nella **[!UICONTROL content]** della sezione **[!UICONTROL Documento di registrazione]** scheda .

   ![Proprietà pagina mastro](assets/master-page-properties.png)

   Le proprietà della pagina master includono Immagine logo, Testo intestazione, Titolo modulo, Etichetta liberatoria e Testo liberatoria. È possibile applicare le proprietà del modello XDP o del modulo adattivo al documento di record. Per impostazione predefinita, AEM Forms applica le proprietà del modello al documento di record. È inoltre possibile definire valori personalizzati per le proprietà della pagina master. Per informazioni su come applicare più pagine master in un documento di record, vedere [Applicare più pagine master a un documento di record](#apply-multiple-master-pages-dor).

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

Il modulo adattivo può essere lungo e contenere diversi campi del modulo. Potrebbe non essere necessario salvare un documento di record come copia esatta del modulo adattivo. Ora è possibile scegliere un layout di tabella o colonna per salvare uno o più pannelli di modulo adattivi nel documento di record PDF.

Prima di generare un documento di record, nelle impostazioni di un pannello selezionare Layout per il documento di record per tale pannello come Tabella o Colonna. I campi nel pannello vengono organizzati di conseguenza nel documento di registrazione.

![Rendering dei campi in un pannello con layout di tabella nel documento del record](assets/dortablelayout.png)

Rendering dei campi in un pannello con layout di tabella nel documento del record

![Rendering dei campi in un pannello con layout a colonne nel documento del record](assets/dorcolumnlayout.png)

Rendering dei campi in un pannello con layout a colonne nel documento del record

## Impostazioni del documento di registrazione {#document-of-record-settings}

Le impostazioni del documento di record consentono di scegliere le opzioni che si desidera includere nel documento di record. Ad esempio, una banca accetta un modulo nome, età, numero di previdenza sociale e numero di telefono. Il modulo genera un numero di conto bancario e i dettagli della filiale. È possibile scegliere di visualizzare solo il nome, il numero di previdenza sociale, il conto bancario e i dettagli del ramo nel documento di registrazione.

Il documento delle impostazioni di record di un componente è disponibile sotto le relative proprietà. Per accedere alle proprietà di un componente, selezionalo e fai clic su ![cmppr](assets/cmppr.png) nella sovrapposizione. Le proprietà sono elencate nella barra laterale ed è possibile trovare le seguenti impostazioni.

**Impostazioni a livello di campo**

* **Escludi Dal Documento Di Registrazione**: L&#39;impostazione della proprietà su true esclude il campo dal documento del record. Si tratta di una proprietà modificabile in script denominata `excludeFromDoR`. Il suo comportamento dipende da **Escludere i campi dal DoR se nascosti** proprietà a livello di modulo.

* **Visualizza pannello come tabella:** L’impostazione della proprietà visualizza il pannello come tabella nel documento se il pannello contiene meno di 6 campi. Applicabile solo al pannello.
* **Escludi titolo dal documento di registrazione:** L&#39;impostazione della proprietà esclude il titolo del pannello/tabella dal documento di registrazione. Applicabile solo ai pannelli e alle tabelle.
* **Escludi descrizione dal documento di registrazione:** L&#39;impostazione della proprietà esclude la descrizione del pannello/tabella dal documento di registrazione. Applicabile solo ai pannelli e alle tabelle.
* **[!UICONTROL Impaginazione]** > **[!UICONTROL Luogo]**: Determina la posizione in cui si seleziona di posizionare il pannello.
   * **[!UICONTROL Luogo]** > **[!UICONTROL Successivo]**: Posiziona il pannello dopo l’oggetto precedente nel pannello principale.
   * **[!UICONTROL Luogo]** > **[!UICONTROL Nell’area contenuto]** > Nome dell’area contenuto: Posiziona il pannello nell’area di contenuto specificata.
   * **[!UICONTROL Luogo]** > **[!UICONTROL Parte superiore area contenuto successiva]**: Posiziona il pannello nella parte superiore dell’area di contenuto successiva.
   * **[!UICONTROL Luogo]** > **[!UICONTROL Parte superiore dell’area contenuto]** > Nome dell’area contenuto: Posiziona il pannello nella parte superiore dell’area di contenuto specificata.
   * **[!UICONTROL Luogo]** > **[!UICONTROL Sulla pagina]** > Nome della pagina master: Posiziona il pannello nella pagina specificata. Se un&#39;interruzione di pagina non viene inserita automaticamente, [!DNL AEM Forms] aggiunge un’interruzione di pagina.
   * **[!UICONTROL Luogo]** > **[!UICONTROL Parte superiore pagina successiva]**: Posiziona il pannello nella parte superiore della pagina successiva. Se un&#39;interruzione di pagina non viene inserita automaticamente, [!DNL AEM Forms] aggiunge un’interruzione di pagina.
   * **[!UICONTROL Luogo]** > **[!UICONTROL Parte superiore pagina]** > Nome della pagina master: Posiziona il pannello nella parte superiore della pagina quando viene eseguito il rendering della pagina specificata. Se un&#39;interruzione di pagina non viene inserita automaticamente, [!DNL AEM Forms] aggiunge un’interruzione di pagina.
* **[!UICONTROL Impaginazione]** > **[!UICONTROL Dopo]**: Determina l’area da compilare dopo aver inserito un pannello.I campi seguenti sono disponibili nella **[!UICONTROL Dopo]** sezione:
   * **[!UICONTROL Dopo]** > **[!UICONTROL Continua riempimento padre]**: Continua a unire i dati per tutti gli oggetti da riempire nel pannello principale.
   * **[!UICONTROL Dopo]** > **[!UICONTROL Vai all’area contenuto successiva]**: Inizia a riempire l’area di contenuto successiva dopo il posizionamento del pannello.
   * **[!UICONTROL Dopo]** > **[!UICONTROL Vai all’area contenuto]** > Nome dell’area contenuto: Inizia a riempire l’area di contenuto specificata dopo il posizionamento del pannello.
   * **[!UICONTROL Dopo]** > **[!UICONTROL Vai alla pagina successiva]**: Inizia a riempire la pagina successiva dopo aver posizionato il pannello.
   * **[!UICONTROL Dopo]** > **[!UICONTROL Vai alla pagina]** > Nome della pagina: Inizia a riempire la pagina specificata dopo il posizionamento del pannello.
* **[!UICONTROL Impaginazione]** > **[!UICONTROL Overflow]**: Imposta un overflow per un pannello o una tabella che si estende su più pagine. I seguenti campi sono disponibili nella **[!UICONTROL Overflow]** sezione:
   * **[!UICONTROL Overflow]** > **[!UICONTROL Nessuno]**: Inizia a riempire la pagina successiva. Se un&#39;interruzione di pagina non viene inserita automaticamente, [!DNL AEM Forms] aggiunge un’interruzione di pagina.
   * **[!UICONTROL Overflow]** > **[!UICONTROL Vai all’area contenuto]** > Nome dell’area contenuto: Inizia a riempire l&#39;area di contenuto specificata.
   * **[!UICONTROL Overflow]** > **[!UICONTROL Vai alla pagina]** > Nome della pagina: Inizia a riempire la pagina specificata.

Per informazioni su come applicare interruzioni di pagina e applicare più pagine master in un documento di record, vedere [Applica interruzione di pagina in un documento di registrazione](#apply-page-breaks-in-dor) e [Applicare più pagine master a un documento di record](#apply-multiple-master-pages-dor).

**Impostazioni a livello di modulo**

* **Includi campi non associati in DoR:** L’impostazione della proprietà include campi non associati di un modulo adattivo basato su schema nel documento di registrazione. Per impostazione predefinita è true.
* **Escludere i campi dal DoR se nascosti:** L&#39;impostazione della proprietà sostituisce il comportamento della proprietà a livello di campo &quot;Escludi dal documento di record&quot; quando non è true. Se i campi sono nascosti al momento dell’invio del modulo, verranno esclusi dal documento se la proprietà è impostata su true, purché la proprietà &quot;Escludi dal documento di record&quot; non sia impostata.

## Applicazione di un&#39;interruzione di pagina in un documento di registrazione {#apply-page-breaks-in-dor}

È possibile applicare interruzioni di pagina in un documento di record utilizzando più metodi.

Per applicare un&#39;interruzione di pagina a un documento di record:

1. Tocca il pannello e seleziona ![Configura](assets/configure-icon.svg).

1. Espandi **[!UICONTROL Documento di registrazione]** per visualizzare le proprietà.

1. In **[!UICONTROL Impaginazione]** sezione, toccare ![Cartella](assets/folder-icon.svg) in **[!UICONTROL Luogo]** campo .
1. Tocca **[!UICONTROL Parte superiore pagina successiva]** e toccare **[!UICONTROL Seleziona]**. Puoi anche toccare **[!UICONTROL Parte superiore pagina]**, seleziona la pagina master e tocca **[!UICONTROL Seleziona]** per applicare l’interruzione di pagina.
1. Tocca ![Salva](assets/save_icon.svg) per salvare le proprietà.

Il pannello selezionato si sposta sulla pagina successiva.

## Applicare più pagine master a un documento di record {#apply-multiple-master-pages-dor}

Se il modello XDP personalizzato selezionato include più pagine master, le proprietà di tali pagine vengono visualizzate nella [!UICONTROL content] della sezione [!UICONTROL Documento di registrazione] scheda . Per ulteriori informazioni, consulta [Personalizzare le informazioni sul marchio nel documento di registrazione](#customize-the-branding-information-in-document-of-record).

È possibile applicare più pagine master a un documento di record applicando diverse pagine master ai componenti di un modulo adattivo. Utilizza la [Impaginazione](#document-of-record-settings) sezione delle proprietà Document of Record per applicare più pagine master.

Di seguito è riportato un esempio di come applicare più pagine master a un documento di record: Puoi caricare un modello XDP che include quattro pagine master [!DNL AEM Forms] server. [!DNL AEM Forms] applica le proprietà del modello al documento di record per impostazione predefinita. [!DNL AEM Forms] applica anche le proprietà della prima pagina master del modello al documento di record.

Per applicare le proprietà della seconda pagina master a un pannello e le proprietà della terza pagina master ai pannelli seguenti, eseguire la procedura seguente:

1. Toccare il pannello per applicare la seconda pagina master e selezionare ![Configura](assets/configure-icon.svg).
1. In **[!UICONTROL Impaginazione]** sezione, toccare ![Cartella](assets/folder-icon.svg) in **[!UICONTROL Luogo]** campo .
1. Tocca **[!UICONTROL Sulla pagina]**, seleziona la seconda pagina master e tocca **[!UICONTROL Seleziona]**.
AEM Forms applica la seconda pagina master al pannello e a tutti i pannelli successivi nel modulo adattivo.
1. In **[!UICONTROL Impaginazione]** sezione, toccare ![Cartella](assets/folder-icon.svg) in **[!UICONTROL Dopo]** campo .
1. Tocca **[!UICONTROL Vai alla pagina]**, seleziona la terza pagina master e tocca **[!UICONTROL Seleziona]**.
1. Tocca ![Salva](assets/save_icon.svg) per salvare le proprietà.
AEM Forms applica la terza pagina master al pannello e a tutti i pannelli successivi nel modulo adattivo.


## Considerazioni chiave durante l&#39;utilizzo del documento di registrazione {#key-considerations-when-working-with-document-of-record}

Quando si lavora su un documento di record per i moduli adattivi, tenere presente le considerazioni e le limitazioni seguenti.

* I modelli dei documenti non supportano il testo RTF. Pertanto, qualsiasi testo RTF nel modulo adattivo statico o nelle informazioni inserite dall’utente finale viene visualizzato come testo normale nel documento di registrazione.
* I frammenti di documento in un modulo adattivo non vengono visualizzati nel documento di registrazione. Tuttavia, i frammenti di modulo adattivo sono supportati.
* Il binding del contenuto nel documento di record generato per il modulo adattivo basato su schema XML non è supportato.
* La versione localizzata del documento di record viene creata su richiesta per un&#39;impostazione internazionale quando l&#39;utente richiede il rendering del documento di record. La localizzazione del documento di record avviene insieme alla localizzazione del modulo adattivo. Per ulteriori informazioni sulla localizzazione di documenti di record e moduli adattivi, consulta [Utilizzo AEM flusso di lavoro di traduzione per localizzare i moduli adattivi e il documento di registrazione](/help/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.md).
