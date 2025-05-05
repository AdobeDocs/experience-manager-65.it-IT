---
title: Utilizzo della firma scarabocchio nei moduli di HTML5
description: I moduli HTML5 vengono utilizzati sempre più spesso sui dispositivi touch e un requisito comune è il supporto delle firme. La firma di documenti su dispositivi mobili sta diventando una modalità accettata per firmare moduli su dispositivi mobili.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: designer
docset: aem65
feature: Forms Designer,Designer
exl-id: 2025182f-195b-40d0-aee7-67669f55b964
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 0%

---

# Utilizzo della firma scarabocchio nei moduli di HTML5{#using-scribble-signature-in-html-forms}

I moduli HTML5 vengono utilizzati sempre più spesso sui dispositivi touch e un requisito comune è il supporto delle firme. Scribing (scrittura con uno stilo o un dito) sta diventando un modo accettato di firmare moduli su dispositivi mobili. HTML5 Forms e Forms Designer ora consentono di avere un campo di firma scarabocchio sul modulo. Quando si esegue il rendering del modulo nel browser, è possibile firmare questi campi utilizzando uno stilo, un mouse o un tocco.

## Progettare un modulo utilizzando il campo Firma a mano {#how-to-design-a-form-using-scribble-signature-field}

1. Aprire un modulo in Forms Designer.
1. Trascina e rilascia il campo A mano libera nella pagina.

   ![scarabocchio_designer](assets/designer_scribble.png)

   >[!NOTE]
   >
   >I Dimension del campo selezionato in Forms Designer vengono visualizzati durante il rendering del campo. Tuttavia, la dimensione della casella della firma sottoposta a rendering viene calcolata in base alle proporzioni del campo e non alla dimensione specificata in Forms Designer.

1. Configura il campo Disegno di firma.

   Per impostazione predefinita, il campo Scribble firma contrassegna le informazioni di geolocalizzazione come obbligatorie durante il processo di firma su iPad (ed è facoltativo per altri dispositivi). Questo comportamento predefinito può essere ignorato modificando il valore della proprietà `geoLocMandatoryOnIpad`. Questa proprietà viene esposta come extra nel campo a mano libera della firma. I passaggi per modificarlo sono i seguenti:

   1. Nel modulo selezionare il campo Disegno firma.
   1. Selezionare la scheda **XML Source**.

      >[!NOTE]
      >
      >Per aprire la scheda Source XML, fare clic su **Visualizza** > **Source XML**.

   1. Individuare il tag `<ui>` nel tag `<field>` e modificare il codice sorgente in modo che sia simile al seguente:

      ```xml
      <extras name="x-scribble-add-on">
      <boolean name="geoLocMandatoryOnIpad">0</boolean>
      </extras>
      ```

   1. Selezionare la scheda **Visualizzazione Struttura**. Nella casella di conferma fare clic su **Sì**.
   1. Salvare il modulo.

1. Eseguire il rendering del modulo su un browser dispositivo/desktop supportato.

## Interfaccia con le firme scarabocchio {#interfacing-with-the-scribble-signatures}

### Firma {#signing}

Dopo aver aggiunto al modulo e aver eseguito il rendering di un campo a mano libera di firma, tocca o fai clic sul campo per aprire una finestra di dialogo. L&#39;utente può scrivere una firma nell&#39;area di disegno designata da un rettangolo punteggiato utilizzando un mouse, un dito o uno stilo.

![geolocalizzazione](assets/geolocation.png)

**A.** Pennello **B.** Gomma **C.** Geolocalizzazione **D.** Informazioni di geolocalizzazione

### Geo-tagging {#geo-tagging}

Facendo clic sull’icona di geolocalizzazione durante la creazione dello scarabocchio, le informazioni relative a posizione geografica e ora vengono incorporate nel campo.

>[!NOTE]
>
>In iPad, per impostazione predefinita, è obbligatorio incorporare le informazioni di geolocalizzazione.

In iPad l&#39;icona di geolocalizzazione non viene visualizzata per impostazione predefinita e le informazioni di geolocalizzazione vengono incorporate automaticamente quando si fa clic su **OK**.

Per gli iPad, questa impostazione può essere modificata modificando il valore del parametro `geoLocManadatoryOnIpad` in `0` nei parametri iniziali del campo.

* Quando le informazioni di geolocalizzazione sono obbligatorie, l’utente dispone di un’area di prelievo ridotta. Il testo di geolocalizzazione viene aggiunto quando l&#39;utente fa clic sull&#39;icona **OK** nell&#39;area rimanente.
* In altri casi, all’utilizzatore viene presentata un’area completamente estraibile. Se l’utente sceglie di incorporare le informazioni di geolocalizzazione, quest’area viene ridimensionata per contenere il testo di geolocalizzazione.

### Cancellazione di una firma {#clearing-a-signature}

Durante l&#39;utilizzo di questa funzione, un utente può fare clic sull&#39;icona **Gomma** per cancellare il campo e ricominciare. Se sono state aggiunte informazioni di geolocalizzazione, anche queste vengono cancellate.

### Salvataggio di una firma {#saving-a-signature}

Facendo clic sull&#39;icona **OK**, lo scarabocchio viene salvato come immagine nel campo. L&#39;immagine e i valori possono essere inviati al server per ulteriore elaborazione. Dopo che un utente ha fatto clic su **OK**, il campo scarabocchio è bloccato. Impossibile modificare nuovamente la firma utilizzando il widget a mano libera.

Toccando o facendo clic sul campo Scarabocchio si apre la finestra di dialogo in modalità di sola lettura.

![3](assets/3.png)

### Selezione delle dimensioni della penna {#selecting-pen-size}

Fai clic sull&#39;icona **Pennelli** per visualizzare un elenco delle dimensioni di penna disponibili. Fare clic su una penna per utilizzare la penna corrispondente.

### Elimina firme dal modulo {#delete-signatures-from-the-form}

Per eliminare le firme dal modulo:

* (Dispositivi mobili) Premere a lungo il campo firma e nella finestra di dialogo di conferma selezionare **Sì**.
* (Desktop) Passa il puntatore del mouse sul campo firma, fai clic sull&#39;icona **Annulla** e nella finestra di dialogo di conferma fai clic su **Sì**.
