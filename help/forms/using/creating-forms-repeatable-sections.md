---
title: Creazione di moduli con sezioni ripetibili
seo-title: Creating forms with repeatable sections
description: Le sezioni ripetibili sono pannelli che possono essere aggiunti o rimossi in modo dinamico da un modulo.
seo-description: Repeatable sections are panels that can be dynamically added or removed to a form.
uuid: c3fa2aa4-a6b4-458e-8534-138e075290b1
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 01724ca0-6901-45e7-b045-f44814ed574e
feature: Adaptive Forms
exl-id: f2abae0a-f7fd-4a39-bd8c-03492ce06fe9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1119'
ht-degree: 17%

---

# Creazione di moduli con sezioni ripetibili {#creating-forms-with-repeatable-sections}

Le sezioni ripetibili sono pannelli che possono essere aggiunti o rimossi in modo dinamico da un modulo.

Ad esempio, quando si richiede un lavoro, il ricercatore di lavoro fornisce i dettagli precedenti sull&#39;occupazione, come il nome dell&#39;azienda, il ruolo, il progetto e altre informazioni. L&#39;informazione di tutti i datori di lavoro richiede sezioni diverse ma simili. In questo caso, il modulo per l&#39;occupazione fornisce una sezione datore di lavoro e fornisce anche un&#39;opzione per aggiungere in modo dinamico altre sezioni di questo tipo. Queste sezioni, aggiunte in modo dinamico, sono note come sezioni ripetibili.

Per creare pannelli ripetibili è possibile utilizzare uno dei metodi seguenti:

## Utilizzo di Instance Manager tramite script  {#using-instance-manager-via-scripts-nbsp}

1. In modalità di modifica, seleziona un pannello, quindi tocca ![cmppr](assets/cmppr.png). Nella barra laterale, in Proprietà, abilita **Rendi pannello ripetibile**. Specifica i valori per **[!UICONTROL Massimo]** e **[!UICONTROL Minimo]** campi.

   Il campo Massimo specifica il numero massimo di volte in cui un pannello può essere visualizzato sulla pagina. Puoi specificare -1 nel campo Conteggio massimo per consentire la visualizzazione del pannello per un numero infinito di volte.

   Il campo Minimo specifica il numero minimo di volte in cui un pannello viene visualizzato sul modulo. Se in seguito si imposta il campo Conteggio minimo su zero, è possibile rimuovere tutte le istanze tramite script al termine del rendering.

   >[!NOTE]
   >
   >Per creare un pannello non ripetibile, impostare su uno il valore del campo Massimo e Minimo. Il layout a soffietto non supporta -1 nel campo Conteggio massimo . Puoi specificare un numero elevato per definire il concetto di valore infinito.

1. L’elemento padre del pannello, che deve essere ripetuto, deve contenere pulsanti di aggiunta ed eliminazione per gestire le istanze dei pannelli ripetibili. Effettuare le seguenti operazioni per inserire i pulsanti nell&#39;elemento padre e abilitare gli script nei pulsanti:

   1. Dalla barra laterale, trascinate un componente pulsante nell’elemento padre del pannello. Seleziona il componente e tocca ![edit-rules](assets/edit-rules.png). Le regole del pulsante si aprono nell’editor di regole.
   1. Nella finestra Editor regole, fai clic su **Crea**.

      Seleziona **Editor visivo** nella riga Oggetti modulo e funzioni.

      1. Nell&#39;area della regola, in QUANDO, selezionare stato **è selezionato**.
      1. Sotto THEN:

         * Per creare un pulsante Aggiungi pannello, seleziona **Aggiungi istanza** e trascina il pannello utilizzando ![pannello laterale di attivazione](assets/toggle-side-panel.png) o selezionalo utilizzando **Rilascia oggetto o seleziona qui.**
         * Per creare un pulsante Elimina pannello, seleziona **Rimuovi istanza** e trascina il pannello utilizzando ![pannello laterale di attivazione](assets/toggle-side-panel.png) o selezionalo utilizzando **Rilascia oggetto o seleziona qui.**

      Seleziona **Editor di codice** nella riga Oggetti modulo e funzioni. Fai clic su **Modifica regole** e nell&#39;area codice:

      * Per creare un pulsante Aggiungi pannello, specificare `this.panel.instanceManager.addInstance()`
      * Per creare un pulsante di eliminazione del pannello, specificare `this.panel.instanceManager.removeInstance(this.panel.instanceIndex)`

      Fai clic su **Fine**.

      >[!NOTE]
      >
      >Se un campo appartiene a un pannello ripetibile, non è possibile accedervi direttamente utilizzando il suo nome negli script. Per accedere al campo, specifica l’istanza ripetibile a cui appartiene il campo utilizzando la `instances` API in `InstanceManager`. La sintassi da utilizzare `instances` API in `InstanceManager` è:
      >
      >
      >`<panelName>.instanceManager.instances[<instanceNumber>].<fieldname>`
      >
      >
      >Ad esempio, è possibile creare un modulo adattivo con un pannello ripetibile con una casella di testo. Quando si precompila il modulo con tre caselle di testo ripetibili, è necessario utilizzare il codice xml sottostante:
      >
      >
      >`<panel1><textbox1>AA1</panel1></textbox1>`
      >
      >
      >`<panel1><textbox1>AA2</panel1></textbox1>`
      >
      >
      >`<panel1><textbox1>AA3</panel1></textbox1>`
      >
      >
      >Per leggere i dati AA1, specifica:
      >
      >
      >`Panel1.instanceManager.instances[0].textbox.value`
      >
      >
      >Per leggere i dati AA2, specifica:
      >
      >
      >`Panel1.instanceManager.instances[1].textbox.value`
      >
      >
      >Per ulteriori informazioni, consulta: Classe: InstanceManager#instances in [Riferimento API Java di AEM Forms](https://adobe.com/go/learn_aemforms_documentation_63).

      >[!NOTE]
      >
      >Quando tutte le istanze di un pannello vengono rimosse da un modulo adattivo, per aggiungere un’istanza del pannello rimosso, utilizza la sintassi _panelName per acquisire il gestore di istanze del pannello e l’API addInstance di instance manager per aggiungere l’istanza eliminata. Ad esempio, _panelName.addInstance(). Aggiunge un&#39;istanza del pannello rimosso.



## Utilizzo del layout a soffietto per il pannello principale   {#using-the-accordion-layout-for-the-parent-panel-nbsp}

Un pannello dispone di diverse opzioni di layout. L&#39;opzione Layout per il design accordiano è preconfigurata per pannelli ripetibili. Esegui i seguenti passaggi per il pannello ripetibile con l&#39;opzione Layout per la progettazione accordian:

1. Nell’elemento padre del pannello da ripetere, tocca ![cmppr](assets/cmppr.png). Puoi vedere le proprietà nella barra laterale. In **Layout** a discesa, seleziona **Accordion**.
1. Tocca su un pannello da ripetere ![cmppr](assets/cmppr.png). Puoi visualizzare le proprietà del pannello nella barra laterale. Abilita la **Rendi pannello ripetibile** e specifica il valore per **Massimo** e **Minimo** campi.

   Ora è possibile utilizzare il segno più (+) ed eliminare ( ![pannello di eliminazione](assets/delete-panel.png)) per aggiungere e rimuovere i pannelli.

## Uso di sottomoduli ripetuti da modello di modulo (XDP/XSD) {#using-repeating-subforms-from-form-template-xdp-xsd}

Il sottomodulo ripetibile è simile ai pannelli ripetibili in Forms adattivo. In AEM Forms Designer, eseguire i seguenti passaggi per creare un sottomodulo ripetuto:

1. Nella palette Gerarchia, selezionare il sottomodulo principale del sottomodulo che si desidera ripetere.
1. Nella palette Oggetto, fare clic sulla scheda Sottomodulo e selezionare Flusso dall’elenco Contenuto.
1. Selezionare il sottomodulo da ripetere.
1. Nella palette Oggetto fare clic sulla scheda Sottomodulo e selezionare Posizionato o Flusso dall’elenco Contenuto.
1. Fare clic sulla scheda Binding e selezionare Ripeti sottomodulo per ogni elemento dati.
1. Per specificare il numero minimo di ripetizioni, selezionare Conteggio min e digitare un numero nella casella associata. Se questa opzione viene impostata a 0 e al momento dell’unione di dati non vi sono dati per gli oggetti del sottomodulo, il sottomodulo non sarà posizionato per il rendering del modulo.
1. Per specificare il numero massimo di ripetizioni, selezionare Massimo e digitare un numero nella casella associata. Se non si specifica un valore nella casella Massimo, il numero di ripetizioni dei sottomoduli sarà illimitato.
1. Per specificare un numero prefissato per le ripetizioni del sottomodulo indipendentemente dalla quantità di dati, selezionare l’opzione Conteggio iniziale, quindi digitare il numero di ripetizioni desiderato nella casella associata. Se l’opzione è impostata e non è disponibile alcun dato o sono disponibili dati inferiori al valore di Conteggio iniziale, le istanze vuote del sottomodulo saranno ancora presenti nel modulo.
1. Aggiungere due pulsanti nel sottomodulo principale, uno per aggiungere un’istanza e l’altro per eliminare un’istanza di sottomodulo ripetibile. Per i passaggi dettagliati vedi [Creare un’azione](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c74572b5612a87ca2b56-8000.2.html#WS107c29ade9134a2c-1f74d86012a87d4fe55-8000.2).
1. Ora collega il modello di modulo al modulo adattivo. Per i passaggi dettagliati vedi [Creare un modulo adattivo basato su un modello](/help/forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-a-template).
1. Utilizzare i pulsanti creati nel passaggio 9 per aggiungere e rimuovere sottomoduli.

Il file .zip allegato contiene un sottomodulo ripetibile di esempio.

[Ottieni file](assets/samplerepeatablesubform.zip)

## Utilizzo delle impostazioni di ripetizione di uno schema XML (XSD) {#using-repeat-settings-of-an-xml-schema-xsd-br}

È possibile creare pannelli ripetibili da uno schema XML e dalla proprietà minOccours &amp; maxOccours di qualsiasi elemento di tipo complesso. Per informazioni dettagliate sullo schema XML, vedere [Creare moduli adattivi utilizzando lo schema XML come modello di modulo](/help/forms/using/adaptive-form-xml-schema-form-model.md).

Nel codice seguente, la `SampleType`Il pannello utilizza la proprietà minOccours e maxOccurs .

```xml
<?xml version="1.0" encoding="utf-8" ?>
    <xs:schema targetNamespace="https://adobe.com/sample.xsd"
                    xmlns="https://adobe.com/sample.xsd"
                    xmlns:xs="https://www.w3.org/2001/XMLSchema"
                >

        <xs:element name="sample" type="SampleType"/>

        <xs:complexType name="SampleType">
            <xs:sequence>
                <xs:element name="leaderName" type="xs:string" default="Enter Name"/>
                <xs:element name="assignmentStartDate" type="xs:date"/>
                <xs:element name="gender" type="GenderEnum"/>
                <xs:element name="noOfProjectsAssigned" type="IntType"/>
                <xs:element name="assignmentDetails" type="AssignmentDetails"
                                            minOccurs="0" maxOccurs="10"/>
            </xs:sequence>
        </xs:complexType>

        <xs:complexType name="AssignmentDetails">
            <xs:attribute name="name" type="xs:string" use="required"/>
            <xs:attribute name="durationOfAssignment" type="xs:unsignedInt" use="required"/>
            <xs:attribute name="numberOfMentees" type="xs:unsignedInt" use="required"/>
             <xs:attribute name="descriptionOfAssignment" type="xs:string" use="required"/>
             <xs:attribute name="financeRelatedProject" type="xs:boolean"/>
       </xs:complexType>
  <xs:simpleType name="IntType">
            <xs:restriction base="xs:int">
            </xs:restriction>
        </xs:simpleType>
  <xs:simpleType name="GenderEnum">
            <xs:restriction base="xs:string">
                <xs:enumeration value="Female"/>
                <xs:enumeration value="Male"/>
            </xs:restriction>
        </xs:simpleType>
    </xs:schema>
```

>[!NOTE]
>
>Per il layout non generico, utilizza i componenti pulsante per moduli adattivi per aggiungere e rimuovere istanze.
