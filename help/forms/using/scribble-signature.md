---
title: Utilizzo della firma scarabocchio nei moduli di HTML5
description: I moduli HTML5 vengono utilizzati sempre più spesso sui dispositivi touch e un requisito comune è il supporto delle firme. La firma di documenti su dispositivi mobili sta diventando una modalità accettata per firmare moduli su dispositivi mobili.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: designer
docset: aem65
feature: Designer
exl-id: 2025182f-195b-40d0-aee7-67669f55b964
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 0%

---

# Utilizzo della firma scarabocchio nei moduli di HTML5{#using-scribble-signature-in-html-forms}

I moduli HTML5 vengono utilizzati sempre più spesso sui dispositivi touch e un requisito comune è il supporto delle firme. Scribing (scrittura con uno stilo o un dito) sta diventando un modo accettato di firmare moduli su dispositivi mobili. HTML5 Forms e Forms Designer ora abilitano l’opzione di avere un campo di firma scarabocchio sul modulo. Quando si esegue il rendering del modulo nel browser, è possibile firmare questi campi utilizzando uno stilo, un mouse o un tocco.

## Progettare un modulo utilizzando il campo Firma a mano {#how-to-design-a-form-using-scribble-signature-field}

1. Aprire un modulo in Forms Designer.
1. Trascina e rilascia il campo A mano libera nella pagina.

   ![designer_scribble](assets/designer_scribble.png)

   >[!NOTE]
   >
   >I Dimension del campo selezionato in Forms Designer si riflettono durante il rendering del campo. Tuttavia, la dimensione della casella della firma di cui è stato eseguito il rendering viene calcolata in base alle proporzioni del campo e non alla dimensione specificata in Forms Designer.

1. Configura il campo Disegno di firma.

   Per impostazione predefinita, il campo Scribble firma contrassegna le informazioni di geolocalizzazione come obbligatorie durante il processo di firma su iPad (ed è facoltativo per altri dispositivi). Questo comportamento predefinito può essere ignorato modificando il valore della proprietà `geoLocMandatoryOnIpad` proprietà. Questa proprietà viene esposta come extra nel campo a mano libera della firma. I passaggi per modificarlo sono i seguenti:

   1. Nel modulo selezionare il campo Disegno firma.
   1. Seleziona la **Origine XML** scheda.

      >[!NOTE]
      >
      >Per aprire la scheda Origine XML, fare clic su **Visualizza** > **Origine XML**.

   1. Individua il `<ui>` tag in `<field>` assegna tag e modifica al codice sorgente in modo che abbia l’aspetto seguente:

      ```xml
      <extras name="x-scribble-add-on">
      <boolean name="geoLocMandatoryOnIpad">0</boolean>
      </extras>
      ```

   1. Seleziona la **Visualizzazione Progettazione** scheda. Nella casella di conferma fare clic su **Sì**.
   1. Salvare il modulo.

1. Eseguire il rendering del modulo su un browser dispositivo/desktop supportato.

## Interfaccia con le firme scarabocchio {#interfacing-with-the-scribble-signatures}

### Firma {#signing}

Dopo aver aggiunto al modulo e aver eseguito il rendering di un campo a mano libera di firma, tocca o fai clic sul campo per aprire una finestra di dialogo. L&#39;utente può scrivere una firma nell&#39;area di disegno designata da un rettangolo punteggiato utilizzando un mouse, un dito o uno stilo.

![geolocalizzazione](assets/geolocation.png)

**R.** Pennello **B.** Gomma **C.** Geolocalizzazione **D.** Informazioni di geolocalizzazione

### Geo-tagging {#geo-tagging}

Facendo clic sull’icona di geolocalizzazione durante la creazione dello scarabocchio, le informazioni relative a posizione geografica e ora vengono incorporate nel campo.

>[!NOTE]
>
In iPad, per impostazione predefinita, è obbligatorio incorporare le informazioni di geolocalizzazione.

In iPad, l’icona di geolocalizzazione non viene visualizzata per impostazione predefinita e le informazioni di geolocalizzazione vengono incorporate automaticamente quando fai clic su **OK**.

Per gli iPad, questa impostazione può essere modificata modificando il valore di `geoLocManadatoryOnIpad` parametro a `0`, nei parametri iniziali del campo.

* Quando le informazioni di geolocalizzazione sono obbligatorie, l’utente dispone di un’area di prelievo ridotta. Il testo di geolocalizzazione viene aggiunto quando l’utente fa clic **OK** sull&#39;area rimanente.
* In altri casi, all’utilizzatore viene presentata un’area completamente estraibile. Se l’utente sceglie di incorporare le informazioni di geolocalizzazione, quest’area viene ridimensionata per contenere il testo di geolocalizzazione.

### Cancellazione di una firma {#clearing-a-signature}

Quando si utilizza questa funzione, un utente può fare clic sul pulsante **Gomma** per cancellare il campo e ricominciare da capo. Se sono state aggiunte informazioni di geolocalizzazione, anche queste vengono cancellate.

### Salvataggio di una firma {#saving-a-signature}

Facendo clic su **OK** salva lo scarabocchio come immagine nel campo. L&#39;immagine e i valori possono essere inviati al server per ulteriore elaborazione. Dopo aver fatto clic su un utente **OK**, il campo scarabocchio è bloccato. Impossibile modificare nuovamente la firma utilizzando il widget a mano libera.

Toccando o facendo clic sul campo Scarabocchio si apre la finestra di dialogo in modalità di sola lettura.

![3](assets/3.png)

### Selezione delle dimensioni della penna {#selecting-pen-size}

Fai clic su **Pennelli** per visualizzare un elenco delle dimensioni di penna disponibili. Fare clic su una penna per utilizzare la penna corrispondente.

### Elimina firme dal modulo {#delete-signatures-from-the-form}

Per eliminare le firme dal modulo:

* (Dispositivi mobili) Premi a lungo il campo della firma e, nella finestra di dialogo di conferma, seleziona **Sì**.
* (Desktop) Passa il puntatore del mouse sul campo firma, fai clic sul pulsante **Annulla** e nella finestra di dialogo di conferma, fai clic su **Sì**.
