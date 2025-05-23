---
title: Generare un documento di record per i moduli adattivi
description: Spiega come generare un documento di record (DoR) per i moduli adattivi.
content-type: reference
topic-tags: adaptive_forms, develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Adaptive Forms,Foundation Components
solution: Experience Manager, Experience Manager Forms
role: User, Developer
exl-id: 7240897f-6b3a-427a-abc6-66310c2998f3
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '4308'
ht-degree: 2%

---

# Genera documento di record per moduli adattivi o frammenti di moduli adattivi {#generate-document-of-record-for-adaptive-forms}

<span class="preview"> Adobe consiglia di utilizzare l&#39;acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [la creazione di un nuovo Forms adattivo](/help/forms/using/create-an-adaptive-form-core-components.md) o [l&#39;aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base. </span>

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/generate-document-of-record-for-non-xfa-based-adaptive-forms.html?lang=it) |
| AEM 6.5 | Questo articolo |


## Panoramica {#overview}

Dopo aver inviato un modulo, i clienti in genere desiderano conservare una registrazione, in formato cartaceo o documentale, delle informazioni che hanno compilato nel modulo per riferimento futuro. Tale documento è denominato documento di record.

Questo articolo spiega come generare un documento di record per un frammento di Forms adattivo o di modulo adattivo.

>[!NOTE]
>
> Il supporto per personalizzare i frammenti di moduli adattivi e i relativi campi nell’editor di moduli adattivi è stato introdotto con AEM 6.5 Forms Service Pack 19 (6.5.19.0).


>[!NOTE]
>
>La generazione automatica di documenti di record non è supportata per i moduli adattivi basati su XFA. Tuttavia, puoi utilizzare l’XDP utilizzato per creare il modulo adattivo come documento di record.

## Tipi di moduli adattivi e relativi documenti di record {#adaptive-form-types-and-their-documents-of-record}

Quando crei un modulo adattivo, puoi selezionare un modello di modulo. Le opzioni disponibili sono:

* [Modelli di modulo](../../forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-an-xfa-form-template)
Consente di selezionare un modello XFA per il modulo adattivo. Quando selezioni un modello XFA, puoi utilizzare il file XDP associato per il documento di record come descritto in precedenza.

* [Schema XML](../../forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-xml-or-json-schema)
Consente di selezionare una definizione di schema XML per il modulo adattivo. Quando selezioni uno schema XML per il modulo adattivo, puoi:

   * Associa un modello XFA per un documento record. Assicurati che il modello XFA associato utilizzi lo stesso schema XML del modulo adattivo
   * Genera automaticamente documento record

* Nessuno
Consente di creare un modulo adattivo senza un modello di modulo. Il documento di record viene generato automaticamente per il modulo adattivo.

Quando selezioni un modello di modulo, configura il documento di record utilizzando le opzioni disponibili in Configurazione modello documento di record. Vedi [Configurazione modello documento record](#document-of-record-template-configuration).

## Documento di record generato automaticamente {#automatically-generated-document-of-record}

Un documento record consente ai clienti di conservare una copia del modulo inviato a scopo di stampa. Quando si genera automaticamente un documento di record, ogni volta che si modifica il modulo, il relativo documento di record viene aggiornato immediatamente. Ad esempio, rimuovi il campo età per i clienti che hanno selezionato Stati Uniti d’America come paese. Quando tali clienti generano un documento di record, il campo età non è visibile nel documento di record.

Il documento di record generato automaticamente presenta i seguenti vantaggi:

* Si occupa dell’associazione dei dati.
* Nasconde automaticamente i campi contrassegnati come esclusi dal documento record al momento dell’invio. Non è richiesto alcuno sforzo aggiuntivo.
* Consente di risparmiare tempo per la progettazione di un documento di modello record.
* Consente di provare stili e aspetti diversi utilizzando diversi modelli di base e di scegliere lo stile e l&#39;aspetto migliori per il documento di record. Gli aspetti degli stili sono facoltativi. Se non specificate gli stili, gli stili di sistema vengono impostati come predefiniti.
* Garantisce che qualsiasi modifica apportata al modulo venga immediatamente riportata nel documento di record.

## Componenti per generare automaticamente un documento di record {#components-to-automatically-generate-a-document-of-record}

Per generare un documento di record per i moduli adattivi, sono necessari i seguenti componenti:

**Modulo adattivo** Modulo adattivo per il quale si desidera generare un documento di record.

**Frammento di modulo adattivo** Frammento di modulo adattivo per il quale si desidera generare un documento di record.

**Modello di base (consigliato)** Modello XFA (file XDP) creato in Designer AEM. Il modello base viene utilizzato per specificare lo stile e le informazioni di branding per il modello del documento record.

Vedi [Modello base di un documento record](#base-template-of-a-document-of-record)

>[!NOTE]
>
>Il modello base di un documento record è anche chiamato metamodello di un documento record.

**Modello del documento record** Modello XFA (file XDP) generato da un modulo adattivo.

Vedi [Configurazione modello documento record](#document-of-record-template-configuration).

**Dati modulo** Informazioni inserite da un utente nel modulo adattivo. Si unisce con il modello del documento record per generare il documento record.

## Mappatura degli elementi del modulo adattivo {#mapping-of-adaptive-form-elements}

Nelle sezioni seguenti viene descritto come gli elementi di un modulo adattivo vengono visualizzati nel documento di record.

### Campi {#fields}

<table>
 <tbody>
  <tr>
   <th>Componente modulo adattivo</th>
   <th>Componente XFA corrispondente</th>
   <th>Incluso per impostazione predefinita nel modello del documento record?</th>
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
   <td>Disegno a mano</td>
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
   <td><p>Pulsante Invia e-mail</p> <p>Pulsante invio HTTP</p> </td>
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
   <td>Non disponibile nel modello del documento record. Disponibile solo in un documento record tramite allegati.</td>
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
   <td>Il pannello ripetibile viene mappato su una sottomaschera ripetibile.</td>
  </tr>
 </tbody>
</table>

### Componenti statici {#static-components}

| Componente modulo adattivo | Componente XFA corrispondente | Note |
|---|---|---|
| Immagine | Immagine | I componenti TextDraw e Image, sia associati che non associati, vengono sempre visualizzati nel documento di record di un modulo adattivo basato su XSD, a meno che non vengano esclusi utilizzando le impostazioni del documento di record. |
| Testo | Testo |

>[!NOTE]
>
>Nell’interfaccia classica, si ottengono schede diverse per la modifica delle proprietà dei campi.

### Tabelle {#tables}

I componenti della tabella per moduli adattivi come intestazione, piè di pagina e riga vengono mappati sui componenti XFA corrispondenti. Puoi mappare i pannelli ripetibili alle tabelle nel documento di record.

## Modello di base di un documento record {#base-template-of-a-document-of-record}

Il modello base fornisce informazioni sullo stile e sull&#39;aspetto del documento di record. Consente di personalizzare l’aspetto predefinito del documento di record generato automaticamente. Ad esempio, si desidera aggiungere il logo della società nell&#39;intestazione e le informazioni sul copyright nel piè di pagina del documento record. La pagina master del modello base viene utilizzata come pagina master per il modello del documento record. La pagina master può contenere informazioni quali intestazione di pagina, piè di pagina e numero di pagina che è possibile applicare al documento di record. È possibile applicare tali informazioni al documento record utilizzando il modello base per la generazione automatica del documento record. L&#39;utilizzo del modello di base consente di modificare le proprietà predefinite dei campi.

Assicurati di seguire [convenzioni modello base](#base-template-conventions) durante la progettazione del modello base.

## Convenzioni modello base {#base-template-conventions}

Un modello di base viene utilizzato per definire intestazione, piè di pagina, stile e aspetto di un documento di record. L&#39;intestazione e il piè di pagina possono includere informazioni quali il logo aziendale e il testo del copyright. La prima pagina master del modello di base viene copiata e utilizzata come pagina master per il documento di record, che contiene intestazione, piè di pagina, numero di pagina o qualsiasi altra informazione da visualizzare in tutte le pagine del documento di record. Se si utilizza un modello di base non conforme alle convenzioni del modello di base, la prima pagina master del modello di base viene ancora utilizzata nel modello del documento record. È consigliabile progettare il modello di base in base alle relative convenzioni e utilizzarlo per la generazione automatica del documento di record.

**Convenzioni pagina master**

* Nel modello di base, è necessario denominare il sottomodulo principale `AF_METATEMPLATE` e la pagina master `AF_MASTERPAGE`.

* Alla pagina master con il nome `AF_MASTERPAGE` che si trova nella sottomaschera principale `AF_METATEMPLATE` viene data la preferenza per l&#39;estrazione di informazioni su intestazione, piè di pagina e stile.

* Se `AF_MASTERPAGE` è assente, viene utilizzata la prima pagina master presente nel modello di base.

**Convenzioni di stile per i campi**

* Per applicare lo stile ai campi nel documento record, il modello base fornisce i campi nel sottomodulo `AF_FIELDSSUBFORM` sotto il sottomodulo principale `AF_METATEMPLATE`.

* Le proprietà di questi campi vengono applicate ai campi del documento record. Questi campi devono seguire la convenzione di denominazione `AF_<name of field in all caps>_XFO`. Ad esempio, il nome del campo per la casella di controllo deve essere `AF_CHECKBOX_XFO`.

Per creare un modello di base, eseguire le operazioni seguenti in AEM Designer.

1. Fare clic su **File > Nuovo**.
1. Seleziona l&#39;opzione **Basato su un modello**.

1. Selezionare la categoria **Forms - Documento di record**.
1. Selezionare **Modello base DoR**.
1. Fai clic su **Avanti** e fornisci le informazioni richieste.

1. (Facoltativo) Modificare lo stile e l&#39;aspetto dei campi che si desidera applicare ai campi del documento record.
1. Salvare il modulo.

È ora possibile utilizzare il modulo salvato come modello di base per il documento di record.
Non modificare o rimuovere gli script presenti nel modello di base.

**Modifica del modello di base**

* Se non si applica alcuno stile ai campi nel modello di base, è consigliabile rimuovere tali campi dal modello di base in modo che gli aggiornamenti al modello di base vengano selezionati automaticamente.
* Durante la modifica del modello di base, non rimuovere, aggiungere o modificare gli script.

>[!NOTE]
>
>Progettare il modello base utilizzando le convenzioni e seguendo rigorosamente i passaggi descritti in precedenza.

## Configurazione modello del documento record {#document-of-record-template-configuration}

Configurare il modello del documento di record del modulo per consentire ai clienti di scaricare una copia stampabile del modulo inviato. Un file XDP funge da modello del documento di record. Il documento di record che i clienti scaricano viene formattato in base al layout specificato nel file XDP.

Per configurare un documento di record per i moduli adattivi, effettua le seguenti operazioni:

1. Nell&#39;istanza dell&#39;autore AEM, fare clic su **Forms > Forms and Documents.**
1. Selezionare un modulo e fare clic su **Visualizza proprietà**.
1. Nella finestra Proprietà, selezionare **Modello modulo**.
È inoltre possibile selezionare un modello di modulo durante la creazione di un modulo.

   >[!NOTE]
   >
   >Nella scheda Modello modulo, accertati di selezionare **Schema** o **Nessuno** dal menu a discesa **Seleziona da**. **[!UICONTROL Documento record non supportato per moduli basati su XFA o adattivi con modello modulo come modello modulo.]**

1. Nella sezione Configurazione modello documento record della scheda Modello modulo selezionare una delle opzioni seguenti:

   **Nessuno** Selezionare questa opzione se non si desidera configurare il documento di record per il modulo.

   **Associa modello modulo come modello del documento record** Selezionare questa opzione se si dispone di un file XDP da utilizzare come modello per il documento record. Quando si seleziona questa opzione, vengono visualizzati tutti i file XDP disponibili nell’archivio di AEM Forms. Selezionare il file appropriato.

   Il file XDP selezionato viene associato al modulo adattivo.

   **Genera documento di record** Selezionare questa opzione per utilizzare un file XDP come modello di base per definire lo stile e l&#39;aspetto del documento di record. Quando si seleziona questa opzione, vengono visualizzati tutti i file XDP disponibili nell’archivio di AEM Forms. Selezionare il file appropriato.

   >[!NOTE]
   >
   >Assicurati che lo schema utilizzato per creare il modulo adattivo e lo schema (schema dati) del modulo XFA siano gli stessi se:
   >
   >
   >
   >    * Il modulo adattivo è basato su schema
   >    * Stai utilizzando **Associa modello modulo come opzione Modello documento record** per documento record
   >
   >

1. Fai clic su **Fine.**

## Personalizzare le informazioni di branding nel documento record {#customize-the-branding-information-in-document-of-record}

Durante la generazione di un documento record, è possibile modificare le informazioni di branding per il documento record nella scheda Documento record. La scheda Documento record include opzioni quali logo, aspetto, layout, intestazione e piè di pagina, liberatoria e se si desidera includere o meno le opzioni di caselle di controllo e pulsanti di scelta non selezionate.

Per localizzare le informazioni di branding immesse nella scheda Documento record, è necessario assicurarsi che le impostazioni internazionali del browser siano impostate in modo appropriato. La procedura seguente illustra come personalizzare le informazioni di branding del documento record:

1. Selezionare un pannello (pannello principale) nel documento di record, quindi selezionare ![configura](assets/configure.png).
1. Seleziona ![dortab](/help/forms/using/assets/dortab.png). Viene visualizzata la scheda Documento record.
1. Selezionare il modello predefinito o un modello personalizzato per il rendering del documento record. Se selezioni il modello predefinito, sotto il menu a discesa Modello viene visualizzata un’anteprima in miniatura del documento di record.

   ![brandingtemplate](/help/forms/using/assets/brandingtemplateupdate.png)

   Se scegli di selezionare un modello personalizzato, sfoglia e seleziona un XDP sul server AEM Forms. Se desideri utilizzare un modello che non è già presente nel server AEM Forms, devi innanzitutto caricare XDP nel server AEM Forms.

### Proprietà pagina master (#master-page-properties)

Se si seleziona un modello predefinito o personalizzato, nella scheda Documento record verranno visualizzate alcune o tutte le seguenti proprietà della pagina master, come illustrato nell&#39;immagine precedente. Specifica questi elementi in modo appropriato:

* **Immagine logo**: puoi scegliere di utilizzare l&#39;immagine logo dal modulo adattivo, sceglierne una da DAM o caricarne una dal computer.
* **Titolo modulo**
* **Testo intestazione**
* **Etichetta liberatoria**
* **Dichiarazione di non responsabilità**
* **Testo liberatoria**

  <!--
    * **Accent Color**: The color in which header text and separator lines are rendered in the document or record PDF
    * **Font Family**: Font family of the text in the document of record PDF
    * **For Check Box and Radio Button components, show only the selected values**
    * **Separator for multiple selected value(s)**
    * **Include form objects that are not bound to data model**
    * **Exclude hidden fields from the document of record**
    * **Hide description of panels**
    -->

  Se il modello XDP personalizzato selezionato include più pagine master, le proprietà per tali pagine vengono visualizzate nella sezione **[!UICONTROL content]** della scheda **[!UICONTROL Document of Record]**.

  ![Proprietà pagina master](assets/master-page-properties.png)

  Le proprietà della pagina master includono l&#39;immagine del logo, il testo dell&#39;intestazione, il titolo del modulo, l&#39;etichetta della liberatoria e il testo della liberatoria. Puoi applicare le proprietà del modulo adattivo o del modello XDP al documento di record. Per impostazione predefinita, AEM Forms applica le proprietà del modello al documento di record. È inoltre possibile definire valori personalizzati per le proprietà della pagina master. Per informazioni su come applicare più pagine master in un documento di record, vedere [Applicare più pagine master a un documento di record](#apply-multiple-master-pages-dor).

  >[!NOTE]
  >
  >Se utilizzi un modello di modulo adattivo creato con una versione di Designer precedente alla 6.3, affinché le proprietà Colore accento e Famiglia font funzionino, accertati che nel modello di modulo adattivo nel sottomodulo principale sia presente quanto segue:

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

1. Per salvare le modifiche di branding, selezionate Fatto (Done).

## Layout di tabella e colonna per i pannelli nel documento record {#table-and-column-layouts-for-panels-in-document-of-record}

Il modulo adattivo potrebbe essere lungo e contenere diversi campi modulo. È possibile che non si desideri salvare un documento record come copia esatta del modulo adattivo. Ora puoi scegliere un layout di tabella o colonna per salvare uno o più pannelli di moduli adattivi nel documento di record PDF.

Prima di generare un documento di record, nelle impostazioni di un pannello, selezionate Layout per il documento di record del pannello come Tabella o Colonna. I campi nel pannello vengono organizzati di conseguenza nel documento di record.

![Campi in un pannello sottoposti a rendering in un layout di tabella nel documento di record](assets/dortablelayout.png)

Campi in un pannello sottoposti a rendering in un layout di tabella nel documento di record

![Campi in un pannello sottoposti a rendering in un layout di colonna nel documento di record](assets/dorcolumnlayout.png)

Campi in un pannello di cui è stato eseguito il rendering in un layout di colonna nel documento record

## Impostazioni del documento record {#document-of-record-settings}

Le impostazioni del documento record consentono di scegliere le opzioni da includere nel documento record. Ad esempio, una banca accetta in un modulo nome, età, numero di previdenza sociale e numero di telefono. Il modulo genera un numero di conto bancario e i dettagli della filiale. È possibile scegliere di visualizzare solo il nome, il numero di previdenza sociale, il conto bancario e i dettagli della filiale nel documento di record.

Le impostazioni del documento record di un componente sono disponibili nelle relative proprietà. Per accedere alle proprietà di un componente, selezionarlo e fare clic su ![cmppr](assets/cmppr.png) nella sovrapposizione. Le proprietà sono elencate nella barra laterale e le impostazioni seguenti sono disponibili.

**Impostazioni a livello di campo**

* **Escludi da documento record**: impostando la proprietà true, il campo viene escluso dal documento record. Si tratta di una proprietà che supporta lo script denominata `excludeFromDoR`. Il suo comportamento dipende da **Escludi campi dal DoR se nascosto** proprietà a livello di modulo.

* **Visualizza il pannello come tabella:** Se la proprietà viene impostata, il pannello viene visualizzato come tabella nel documento di record se il pannello contiene meno di 6 campi. Applicabile solo al pannello.
* **Escludi titolo da documento record:** L&#39;impostazione della proprietà esclude il titolo del pannello o della tabella dal documento record. Applicabile solo al pannello e alla tabella.
* **Escludi descrizione da documento record:** L&#39;impostazione della proprietà esclude la descrizione del pannello o della tabella dal documento record. Applicabile solo al pannello e alla tabella.
* **[!UICONTROL Paginazione]** > **[!UICONTROL Posizione]**: determina la posizione in cui si seleziona il pannello.
   * **[!UICONTROL Inserisci]** > **[!UICONTROL Successivo]**: inserisce il pannello dopo l&#39;oggetto precedente nel pannello principale.
   * **[!UICONTROL Inserisci]** > **[!UICONTROL Nell&#39;area contenuto]** > Nome area contenuto: inserisce il pannello nell&#39;area contenuto specificata.
   * **[!UICONTROL Colloca]** > **[!UICONTROL Inizio area contenuti successiva]**: colloca il pannello nella parte superiore dell&#39;area contenuti successiva.
   * **[!UICONTROL Posizione]** > **[!UICONTROL Inizio area contenuto]** > Nome area contenuto: posiziona il pannello nella parte superiore dell&#39;area contenuto specificata.
   * **[!UICONTROL Inserisci]** > **[!UICONTROL A pagina]** > Nome della pagina master: inserisce il pannello nella pagina specificata. Se un&#39;interruzione di pagina non viene inserita automaticamente, [!DNL AEM Forms] aggiunge un&#39;interruzione di pagina.
   * **[!UICONTROL Inserisci]** > **[!UICONTROL Inizio pagina successiva]**: inserisce il pannello nella parte superiore della pagina successiva. Se un&#39;interruzione di pagina non viene inserita automaticamente, [!DNL AEM Forms] aggiunge un&#39;interruzione di pagina.
   * **[!UICONTROL Inserisci]** > **[!UICONTROL Inizio pagina]** > Nome della pagina master: inserisce il pannello nella parte superiore della pagina, quando viene eseguito il rendering della pagina specificata. Se un&#39;interruzione di pagina non viene inserita automaticamente, [!DNL AEM Forms] aggiunge un&#39;interruzione di pagina.
* **[!UICONTROL Paginazione]** > **[!UICONTROL Dopo]**: determina quale area riempire dopo aver posizionato un pannello. I campi seguenti sono disponibili nella sezione **[!UICONTROL Dopo]**:
   * **[!UICONTROL Dopo]** > **[!UICONTROL Continua a riempire l&#39;elemento padre]**: continua l&#39;unione dei dati per tutti gli oggetti che devono ancora essere riempiti nel pannello padre.
   * **[!UICONTROL Dopo]** > **[!UICONTROL Vai all&#39;area contenuto successiva]**: inizia a riempire l&#39;area contenuto successiva dopo l&#39;inserimento del pannello.
   * **[!UICONTROL Dopo]** > **[!UICONTROL Vai all&#39;area dei contenuti]** > Nome dell&#39;area dei contenuti: inizia a riempire l&#39;area dei contenuti specificata dopo l&#39;inserimento del pannello.
   * **[!UICONTROL Dopo]** > **[!UICONTROL Vai alla pagina successiva]**: inizia a riempire la pagina successiva dopo aver inserito il pannello.
   * **[!UICONTROL Dopo]** > **[!UICONTROL Vai alla pagina]** > Nome della pagina: inizia a riempire la pagina specificata dopo aver inserito il pannello.
* **[!UICONTROL Paginazione]** > **[!UICONTROL Overflow]**: imposta un overflow per un pannello o una tabella che si estende su più pagine. I campi seguenti sono disponibili nella sezione **[!UICONTROL Overflow]**:
   * **[!UICONTROL Overflow]** > **[!UICONTROL Nessuno]**: inizia a riempire la pagina successiva. Se un&#39;interruzione di pagina non viene inserita automaticamente, [!DNL AEM Forms] aggiunge un&#39;interruzione di pagina.
   * **[!UICONTROL Overflow]** > **[!UICONTROL Vai all&#39;area dei contenuti]** > Nome dell&#39;area dei contenuti: inizia a riempire l&#39;area dei contenuti specificata.
   * **[!UICONTROL Overflow]** > **[!UICONTROL Vai alla pagina]** > Nome della pagina: inizia a riempire la pagina specificata.

  >[!NOTE]
  >
  > La proprietà Paginazione non è disponibile per i frammenti di modulo adattivi.

Per informazioni su come applicare le interruzioni di pagina e applicare più pagine master in un documento record, vedere [Applica interruzione di pagina in un documento record](#apply-page-breaks-in-dor) e [Applica più pagine master a un documento record](#apply-multiple-master-pages-dor).

**Impostazioni livello modulo**

* **[!UICONTROL BASE]**
   * **Modello:** Puoi selezionare il modello predefinito o personalizzato.

     ![testo alternativo](image.png)
   * **Colore accento:** È possibile predefinire il colore del modello del [!UICONTROL Documento di record].
   * **Famiglia di caratteri:** Seleziona il tipo di carattere per il [!UICONTROL documento di record] testi.
   * **Includi campi non associati nel DoR:** L&#39;impostazione della proprietà include campi non associati del modulo adattivo basato su schema in [!UICONTROL Documento di record]. Per impostazione predefinita è true.
   * **Escludi campi dal DoR se nascosto:** Imposta la proprietà per escludere i campi nascosti dal [!UICONTROL Documento di record] all&#39;invio del modulo. Quando abiliti [Riconvalida sul server](/help/forms/using/configuring-submit-actions.md#server-side-revalidation-in-adaptive-form-server-side-revalidation-in-adaptive-form), il server ricalcola i campi nascosti prima di escluderli dal [!UICONTROL documento di record]
* **[!UICONTROL PROPRIETÀ CAMPO MODULO]**
   * Se si seleziona l&#39;opzione **Per il componente Casella di controllo e Pulsante di opzione, mostrare solo il valore selezionato**, verrà generato l&#39;output DoR con solo il valore selezionato.
   * È possibile selezionare Separatore per più valori selezionati oppure scegliere qualsiasi altro tipo di separatore.
   * Allineamento opzioni
      * Verticale
      * Orizzontale
      * Come Modulo adattivo

     >[!NOTE]
     > L’allineamento verticale e orizzontale è applicabile solo a     Pulsante di opzione e casella di controllo
* **[!UICONTROL PROPRIETÀ PAGINA MASTER]** Fare clic per ulteriori informazioni sulle [proprietà pagina master](#master-page-properties-master-page-properties)

## Applicare un’interruzione di pagina a un documento record {#apply-page-breaks-in-dor}

È possibile applicare le interruzioni di pagina a un documento di record utilizzando più metodi.

Per applicare un&#39;interruzione di pagina a un documento di record:

1. Seleziona il pannello e seleziona ![Configura](/help/forms/using/assets/configure.png)
1. Espandere **[!UICONTROL Documento record]** per visualizzare le proprietà.

1. Nella sezione **[!UICONTROL Paginazione]**, seleziona ![Cartella](/help/forms/using/assets/folder-icon.png) nel campo **[!UICONTROL Luogo]**.
1. Seleziona **[!UICONTROL Inizio pagina successiva]** e seleziona **[!UICONTROL Seleziona]**. Puoi anche selezionare **[!UICONTROL Inizio pagina]**, selezionare la pagina master e **[!UICONTROL Seleziona]** per applicare l&#39;interruzione di pagina.
1. Seleziona ![Salva](/help/forms/using/assets/save_icon.png) per salvare le proprietà.

Il pannello selezionato passa alla pagina successiva.

## Applicare più pagine master a un documento record {#apply-multiple-master-pages-dor}

Se il modello XDP personalizzato selezionato include più pagine master, le proprietà per tali pagine vengono visualizzate nella sezione [!UICONTROL content] della scheda [!UICONTROL Document of Record]. Per ulteriori informazioni, vedere [Personalizzare le informazioni di branding nel documento di record](#customize-the-branding-information-in-document-of-record).

Per applicare più pagine master a un documento record, devi applicare pagine master diverse ai componenti di un modulo adattivo. Utilizza la sezione [Paginazione](#document-of-record-settings) delle proprietà del documento di record per applicare più pagine master.

Di seguito è riportato un esempio di applicazione di più pagine master a un documento di record:
Caricare un modello XDP che includa quattro pagine master nel server [!DNL AEM Forms]. [!DNL AEM Forms] applica le proprietà del modello al documento di record per impostazione predefinita. [!DNL AEM Forms] applica anche le proprietà della prima pagina master nel modello al documento di record.

Per applicare le proprietà della seconda pagina master a un pannello e della terza pagina master ai pannelli che seguono, eseguire la procedura seguente:

1. Selezionare il pannello per applicare la seconda pagina master e selezionare ![Configura](assets/cmppr.png).
1. Nella sezione **[!UICONTROL Paginazione]**, seleziona ![Cartella](/help/forms/using/assets/folder-icon.png) nel campo **[!UICONTROL Luogo]**.
1. Selezionare **[!UICONTROL A pagina]**, selezionare la seconda pagina master e selezionare **[!UICONTROL Seleziona]**.
AEM Forms applica la seconda pagina master al pannello e a tutti i pannelli successivi nel modulo adattivo.
1. Nella sezione **[!UICONTROL Paginazione]**, seleziona ![Cartella](/help/forms/using/assets/folder-icon.png) nel campo **[!UICONTROL Dopo]**.
1. Selezionare **[!UICONTROL Vai a pagina]**, selezionare la terza pagina master e selezionare **[!UICONTROL Seleziona]**.
1. Seleziona ![Salva](/help/forms/using/assets/save_icon.png) per salvare le proprietà.
AEM Forms applica la terza pagina master al pannello e a tutti i pannelli successivi nel modulo adattivo.

>[!NOTE]
>
> Non è possibile applicare più pagine master a un documento record per un frammento di modulo adattivo.

## Considerazioni chiave durante l’utilizzo del documento record {#key-considerations-when-working-with-document-of-record}

Quando lavori su un documento record per moduli adattivi, tieni presenti le considerazioni e le limitazioni seguenti.

* I modelli di documento record non supportano il formato RTF. Pertanto, qualsiasi testo RTF nel modulo adattivo statico o nelle informazioni fornite dall’utente finale viene visualizzato come testo normale nel documento di record.
* I frammenti di documento in un modulo adattivo non vengono visualizzati nel documento di record. Tuttavia, sono supportati i frammenti di modulo adattivi.
* L’associazione del contenuto nel documento record generato per un modulo adattivo basato su schema XML non è supportata.
* La versione localizzata del documento record viene creata su richiesta per una lingua quando l’utente richiede il rendering del documento record. La localizzazione del documento di record si verifica insieme alla localizzazione del modulo adattivo. Per ulteriori informazioni sulla localizzazione di documenti di record e moduli adattivi, consulta [Utilizzo del flusso di lavoro di traduzione AEM per localizzare moduli adattivi e documenti di record](/help/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.md).

## Usa un file XCI personalizzato

Un file XCI consente di impostare varie proprietà di un documento. <!-- Forms as a Cloud Service has a master XCI file.--> È possibile utilizzare un file XCI personalizzato per sostituire una o più proprietà predefinite specificate nel file XCI esistente. È ad esempio possibile scegliere di incorporare un tipo di carattere in un documento o di attivare la proprietà con tag per tutti i documenti. La tabella seguente specifica le opzioni XCI:

| Opzione XCI | Descrizione |
|--- |--- |
| config/present/pdf/creator | Identifica il creatore del documento utilizzando la voce Creator nel dizionario Document Information. Per informazioni su questo dizionario, vedere la [Guida di riferimento PDF](https://opensource.adobe.com/dc-acrobat-sdk-docs/acrobatsdk/). |
| config/present/pdf/producer | Identifica il produttore del documento utilizzando la voce Producer nel dizionario Document Information. Per informazioni su questo dizionario, vedere la [Guida di riferimento PDF](https://opensource.adobe.com/dc-acrobat-sdk-docs/acrobatsdk/). |
| config/present/layout | Controlla se l’output è un singolo pannello o impaginato. |
| config/present/pdf/compression/level | Specifica il grado di compressione da utilizzare durante la generazione di un documento PDF. |
| config/present/pdf/fontInfo/embed | Controlla l&#39;incorporamento del carattere nel documento di output. |
| config/present/pdf/scriptModel | Controlla se le informazioni specifiche XFA vengono incluse nel documento di output PDF. |
| config/present/common/data/adjustData | Controlla se l&#39;applicazione XFA regola i dati dopo l&#39;unione. |
| config/present/pdf/renderPolicy | Controlla se la generazione del contenuto della pagina viene eseguita sul server o differita al client. |
| config/present/common/locale | Specifica le impostazioni locali predefinite utilizzate nel documento di output. |
| config/present/destination | Quando è contenuto da un elemento presente, specifica il formato di output. Quando è contenuto in un elemento openAction, specifica l&#39;azione da eseguire all&#39;apertura del documento in un client interattivo. |
| config/present/output/type | Specifica il tipo di compressione da applicare a un file o il tipo di output da produrre. |
| config/present/common/temp/uri | Specifica l&#39;URI del modulo. |
| config/present/common/template/base | Specifica una posizione di base per gli URI nella progettazione del modulo. Quando questo elemento è assente o vuoto, la posizione della struttura del modulo viene utilizzata come base. |
| config/present/common/log/to | Controlla la posizione in cui vengono scritti i dati di log o di output. |
| config/present/output/to | Controlla la posizione in cui vengono scritti i dati di log o di output. |
| config/present/script/currentPage | Specifica la pagina iniziale all&#39;apertura del documento. |
| config/present/script/exclude | Indica a Forms as a Cloud Service gli eventi da ignorare. |
| config/present/pdf/linearized | Controlla se il documento PDF di output è linearizzato. |
| config/present/script/runScript | Controlla il set di script eseguiti da Forms as a Cloud Service. |
| config/present/pdf/tagged | Controlla l&#39;inclusione dei tag nel documento PDF di output. I tag, nel contesto di PDF, sono informazioni aggiuntive incluse in un documento per esporre la struttura logica del documento. I tag facilitano l’accesso facilitato e la riformattazione. Ad esempio, un numero di pagina può essere contrassegnato come un artefatto in modo che un assistente vocale non lo enunci al centro del testo. Sebbene i tag rendano un documento più utile, aumentano anche le dimensioni del documento e il tempo di elaborazione necessario per crearlo. |
| config/present/pdf/fontInfo/alwaysEmbed | Specifica un tipo di carattere incorporato nel documento di output. |
| config/present/pdf/fontInfo/NeverEmbed | Specifica un tipo di carattere che non deve mai essere incorporato nel documento di output. |
| config/present/pdf/pdfa/part | Specifica il numero di versione della specifica PDF/A a cui è conforme il documento. |
| config/present/pdf/pdfa/amd | Specifica il livello di modifica della specifica PDF/A. |
| config/present/pdf/pdfa/conformance | Specifica il livello di conformità con la specifica PDF/A. |
| config/present/pdf/version | Specifica la versione del documento PDF da generare |
| config/present/pdf/version/map | Specifica i caratteri di fallback per il documento |


<!--

### Use a custom XCI file in your AEM Forms environment

  1. Add the custom XCI file to your development project.
  1. Specify the following inline property:(/help/implementing/deploying/configuring-osgi.md)
  1. Deploy the project to your AEM Forms environment. <!--Cloud Service environment
  
-->

### Utilizzare un file XCI personalizzato nell’ambiente di sviluppo Forms locale

1. Carica il file XCI nell’ambiente di sviluppo locale.
1. Aprire Gestione configurazione <!--Cloud Service SDK-->. <!--The default URL is: <http://localhost:4502/system/console/configMgr>.-->
1. Individua e apri la configurazione **[!UICONTROL Adaptive Forms and Interactive Communication Web Channel]**.
1. Specifica il percorso del file XCI e fai clic su **[!UICONTROL Salva]**.
