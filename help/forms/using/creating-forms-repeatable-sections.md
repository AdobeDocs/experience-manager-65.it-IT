---
title: Creazione di moduli con sezioni ripetibili
seo-title: Creazione di moduli con sezioni ripetibili
description: Le sezioni ripetibili sono pannelli che possono essere aggiunti o rimossi in modo dinamico da un modulo.
seo-description: Le sezioni ripetibili sono pannelli che possono essere aggiunti o rimossi in modo dinamico da un modulo.
uuid: c3fa2aa4-a6b4-458e-8534-138e075290b1
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 01724ca0-6901-45e7-b045-f44814ed574e
translation-type: tm+mt
source-git-commit: 9d90bc5f77f827925e3e1ecd12d56a94a2bbae30
workflow-type: tm+mt
source-wordcount: '1138'
ht-degree: 16%

---


# Creazione di moduli con sezioni ripetibili {#creating-forms-with-repeatable-sections}

Le sezioni ripetibili sono pannelli che possono essere aggiunti o rimossi in modo dinamico da un modulo.

Ad esempio, quando si richiede un lavoro, il job search fornisce i dettagli occupazionali precedenti come il nome della società, il ruolo, il progetto e altre informazioni. L&#39;informazione di tutti i datori di lavoro richiede sezioni diverse ma simili. In questo caso, il modulo per l&#39;impiego fornisce una sezione per il datore di lavoro e offre anche la possibilità di aggiungere in modo dinamico altre sezioni di questo tipo. Tali sezioni, aggiunte in modo dinamico, sono note come sezioni ripetibili.

Per creare pannelli ripetibili, potete usare uno dei seguenti metodi:

## Utilizzo di Instance Manager tramite script  {#using-instance-manager-via-scripts-nbsp}

1. In modalità di modifica, selezionate un pannello, quindi toccate ![cmppr](assets/cmppr.png). Nella barra laterale, in Proprietà, attivare **Realizza pannello ripetibile**. Specificare i valori per i campi **[!UICONTROL Maximum]** e **[!UICONTROL Minimum]**.

   Il campo Massimo specifica il numero massimo di volte in cui un pannello può essere visualizzato sulla pagina. Potete specificare -1 nel campo Conteggio massimo per consentire la visualizzazione del pannello per un numero infinito di volte.

   Il campo Minimo specifica il numero minimo di volte che un pannello viene visualizzato sul modulo. Se si imposta il campo Conteggio minimo su zero, in seguito sarà possibile rimuovere tutte le istanze tramite gli script al termine della rappresentazione.

   >[!NOTE]
   >
   >Per creare un pannello non ripetibile, impostate su uno il valore del campo Massimo e Minimo. Il layout a soffietto non supporta -1 nel campo Conteggio massimo. Potete specificare un numero elevato per definire il concetto di valore infinito.

1. L’elemento padre del pannello, che deve essere ripetuto, deve contenere pulsanti di aggiunta ed eliminazione per gestire le istanze dei pannelli ripetibili. Effettuare le seguenti operazioni per inserire i pulsanti per l&#39;elemento padre e attivare gli script sui pulsanti:

   1. Dalla barra laterale, trascinate un componente pulsante nell’elemento padre del pannello. Selezionate il componente e toccate ![edit-rules](assets/edit-rules.png). Le regole del pulsante si aprono nell&#39;editor delle regole.
   1. Nella finestra Editor regole, fare clic su **Crea**.

      Selezionare **Editor visivo** nella riga Oggetti modulo e funzioni.

      1. Nell&#39;area della regola, in WHEN, selezionare lo stato **su**.
      1. In THEN:

         * Per creare un pulsante Aggiungi pannello, selezionare **Aggiungi istanza**, quindi trascinare il pannello utilizzando ![il pannello di attivazione/disattivazione](assets/toggle-side-panel.png) oppure selezionarlo utilizzando l&#39;oggetto **Rilascia o selezionare qui.**
         * Per creare un pulsante per il pannello di eliminazione, selezionare **Rimuovi istanza**, quindi trascinare il pannello utilizzando ![il pannello di attivazione/disattivazione](assets/toggle-side-panel.png) oppure selezionarlo utilizzando l&#39;oggetto **Rilascia o selezionare qui.**

      Selezionare **Editor di codice** nella riga Oggetti modulo e funzioni. Fare clic su **Modifica regole** e nell&#39;area codice:

      * Per creare un pulsante Aggiungi pannello, specificate `this.panel.instanceManager.addInstance()`
      * Per creare un pulsante per il pannello di eliminazione, specificate `this.panel.instanceManager.removeInstance(this.panel.instanceIndex)`

      Fare clic su **Fine**.

      >[!NOTE]
      >
      >Se un campo appartiene a un pannello ripetibile, non è possibile accedervi direttamente utilizzando il suo nome negli script. Per accedere al campo, specificare l&#39;istanza ripetibile alla quale il campo appartiene utilizzando l&#39;API `instances` in `InstanceManager`. La sintassi per utilizzare l&#39;API `instances` in `InstanceManager` è la seguente:
      >
      >
      >`<panelName>.instanceManager.instances[<instanceNumber>].<fieldname>`
      >
      >
      >Ad esempio, è possibile creare un modulo adattivo con un pannello ripetibile dotato di una casella di testo. Quando si precompila il modulo con tre caselle di testo ripetibili, è necessario disporre del codice xml seguente:
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
      >Per leggere i dati AA1, specificare:
      >
      >
      >`Panel1.instanceManager.instances[0].textbox.value`
      >
      >
      >Per leggere i dati AA2, specificare:
      >
      >
      >`Panel1.instanceManager.instances[1].textbox.value`
      >
      >
      >Per ulteriori informazioni, vedi: Classe: InstanceManager#instance in [ riferimento API Java AEM Forms](https://adobe.com/go/learn_aemforms_documentation_63).

      >[!NOTE]
      >
      >Quando tutte le istanze di un pannello vengono rimosse da un modulo adattivo, per aggiungere un’istanza del pannello rimosso, utilizzate la sintassi _panelName per acquisire il instance manager del pannello e l’API addInstance di instance manager per aggiungere l’istanza eliminata. Ad esempio, _panelName.addInstance(). Aggiunge un’istanza del pannello rimosso.















## Utilizzo del layout a soffietto per il pannello principale   {#using-the-accordion-layout-for-the-parent-panel-nbsp}

Un pannello offre diverse opzioni di layout. L&#39;opzione Layout per la progettazione accordian offre supporto per pannelli ripetibili. Effettuate le seguenti operazioni per visualizzare il pannello ripetibile con l&#39;opzione Layout per la progettazione accordiera:

1. Sul pannello padre da ripetere, toccate ![cmppr](assets/cmppr.png). Potete visualizzare le proprietà nella barra laterale. Nel menu a discesa **Layout**, selezionare **Accordion**.
1. In un pannello, che deve essere ripetuto, toccare ![cmppr](assets/cmppr.png). Potete visualizzare le proprietà del pannello nella barra laterale. Attivate la scheda **Rendi pannello ripetibile** e specificate il valore per i campi **Massimo** e **Minimo**.

   Ora è possibile utilizzare i pulsanti più (+) ed eliminazione ( ![delete-panel](assets/delete-panel.png)) per aggiungere e rimuovere i pannelli.

## Utilizzo di sottomoduli ripetuti da Modello modulo (XDP/XSD) {#using-repeating-subforms-from-form-template-xdp-xsd}

Il sottomodulo ripetibile è simile ai pannelli ripetibili dell&#39;Forms adattivo. In  AEM Forms Designer, effettuare le seguenti operazioni per creare un sottomodulo ripetibile:

1. Nella palette Gerarchia, selezionare il sottomodulo principale del sottomodulo che si desidera ripetere.
1. Nella palette Oggetto, fare clic sulla scheda Sottomodulo e selezionare Flusso dall’elenco Contenuto.
1. Selezionare il sottomodulo da ripetere.
1. Nella palette Oggetto fare clic sulla scheda Sottomodulo e selezionare Posizionato o Flusso dall’elenco Contenuto.
1. Fare clic sulla scheda Binding e selezionare Ripeti sottomodulo per ogni elemento dati.
1. Per specificare il numero minimo di ripetizioni, selezionare Conteggio min e digitare un numero nella casella associata. Se questa opzione viene impostata a 0 e al momento dell’unione di dati non vi sono dati per gli oggetti del sottomodulo, il sottomodulo non sarà posizionato per il rendering del modulo.
1. Per specificare il numero massimo di ripetizioni, selezionare Massimo e digitare un numero nella casella associata. Se non si specifica un valore nella casella Massimo, il numero di ripetizioni del sottomodulo è illimitato.
1. Per specificare un numero prefissato per le ripetizioni del sottomodulo indipendentemente dalla quantità di dati, selezionare l’opzione Conteggio iniziale, quindi digitare il numero di ripetizioni desiderato nella casella associata. Se l’opzione è impostata e non è disponibile alcun dato o sono disponibili dati inferiori al valore di Conteggio iniziale, le istanze vuote del sottomodulo saranno ancora presenti nel modulo.
1. Aggiungere due pulsanti nel sottomodulo principale: uno per l&#39;aggiunta di un&#39;istanza e l&#39;altro per l&#39;eliminazione di un&#39;istanza di sottomodulo ripetibile. Per i passaggi dettagliati, vedere [Creazione di un&#39;azione](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c74572b5612a87ca2b56-8000.2.html#WS107c29ade9134a2c-1f74d86012a87d4fe55-8000.2).
1. A questo punto, collegare il modello di modulo al modulo adattivo. Per i passaggi dettagliati, vedere [Creare un modulo adattivo basato su un modello](/help/forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-a-template).
1. Utilizzare i pulsanti creati al punto 9 per aggiungere e rimuovere sottomoduli.

Il file .zip allegato contiene un sottomodulo ripetibile di esempio.

[Ottieni file](assets/samplerepeatablesubform.zip)

## Utilizzo delle impostazioni di ripetizione di uno schema XML (XSD) {#using-repeat-settings-of-an-xml-schema-xsd-br}

È possibile creare pannelli ripetibili da uno schema XML e dalla proprietà minOccours &amp; maxOccurs di qualsiasi elemento di tipo complesso. Per informazioni dettagliate sullo schema XML, vedere [Creazione di moduli adattivi utilizzando lo schema XML come modello di modulo](/help/forms/using/adaptive-form-xml-schema-form-model.md).

Nel codice seguente, il pannello `SampleType`utilizza la proprietà minOccours &amp; maxOccurs.

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
>Per il layout non conciliare, utilizzate i componenti pulsante per moduli adattivi per aggiungere e rimuovere istanze.
