---
title: Uso della firma digitale nei moduli HTML5
seo-title: Uso della firma digitale nei moduli HTML5
description: I moduli HTML5 vengono sempre più utilizzati sui dispositivi touch e un requisito comune è il supporto delle firme. La firma di documenti su dispositivi mobili sta diventando un modo accettato di firmare moduli su dispositivi mobili.
seo-description: I moduli HTML5 vengono sempre più utilizzati sui dispositivi touch e un requisito comune è il supporto delle firme. La firma di documenti su dispositivi mobili sta diventando un modo accettato di firmare moduli su dispositivi mobili.
uuid: 163dd55a-971a-4dd4-93a7-a14e80184d9b
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: designer
discoiquuid: ecd7f538-9c24-48e7-8450-596851e99cff
docset: aem65
feature: Designer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 0%

---


# Uso della firma digitale nei moduli HTML5{#using-scribble-signature-in-html-forms}

I moduli HTML5 vengono sempre più utilizzati sui dispositivi touch e un requisito comune è il supporto delle firme. La scrittura (con un dito o uno stilo) sta diventando un modo accettato di firmare i moduli su dispositivi mobili. I moduli HTML5 e Forms Designer consentono ora l’opzione di avere un campo firma script sul modulo. Quando viene eseguito il rendering del modulo nel browser, è possibile accedere a tali campi utilizzando uno stilo, un mouse o un tocco.

## Come progettare un modulo utilizzando il campo Firma digitale {#how-to-design-a-form-using-scribble-signature-field}

1. Aprire un modulo in Forms Designer.
1. Trascinare il campo Firma digitale sulla pagina.

   ![designer_scribble](assets/designer_scribble.png)

   >[!NOTE]
   >
   >I Dimension del campo selezionato in Forms Designer vengono visualizzati durante il rendering del campo. Tuttavia, le dimensioni della casella della firma di cui è stato eseguito il rendering vengono calcolate in base alle proporzioni del campo e non in base alla dimensione specificata in Forms Designer.

1. Configurare il campo Firma digitale.

   Il campo Firma frammento, per impostazione predefinita, contrassegna le informazioni sulla geolocalizzazione come obbligatorie durante il processo di firma sull’iPad (ed è facoltativo per altri dispositivi). Per ignorare questo comportamento predefinito è possibile modificare il valore della proprietà `geoLocMandatoryOnIpad` . Questa proprietà viene esposta come extra nel campo Firma documento. I passaggi per modificarlo sono i seguenti:

   1. Nel modulo, selezionare il campo Firma.
   1. Selezionare la scheda **Origine XML**.

      >[!NOTE]
      >
      >Per aprire la scheda Sorgente XML, fare clic su **Visualizza** > **Sorgente XML**.

   1. Individua il tag `<ui>` nel tag `<field>` e modifica il codice sorgente nel modo seguente:

      ```xml
      <extras name="x-scribble-add-on">
      <boolean name="geoLocMandatoryOnIpad">0</boolean>
      </extras>
      ```

   1. Selezionare la scheda **Visualizzazione struttura**. Nella casella di conferma fare clic su **Sì**.
   1. Salvare il modulo.

1. Eseguire il rendering del modulo su un browser desktop/dispositivo supportato.

## Interfaccia con le firme scorrevoli {#interfacing-with-the-scribble-signatures}

### Firma {#signing}

Dopo aver aggiunto e eseguito il rendering di un campo Firma digitale al modulo, viene visualizzata una finestra di dialogo contenente un clic o un tocco sul campo. L&#39;utente può scarabocchiare una firma nell&#39;area di disegno designata da un rettangolo punteggiato utilizzando un mouse, un dito o uno stilo.

![geolocalizzazione](assets/geolocation.png)

**A.** Pennello  **B.** Gomma  **C.** Geolocation  **D.** Informazioni sulla geolocalizzazione

### Assegnazione di tag geografici {#geo-tagging}

Facendo clic sull’icona di geolocalizzazione durante la creazione dello scarabocchio, le informazioni relative alla posizione geografica e all’ora vengono incorporate nel campo.

>[!NOTE]
Per impostazione predefinita, sull’iPad è obbligatorio incorporare le informazioni sulla geolocalizzazione.

Sull’iPad, l’icona di geolocalizzazione non viene visualizzata per impostazione predefinita e le informazioni di geolocalizzazione vengono incorporate automaticamente quando si fa clic su **OK**.

Per gli iPad, questa impostazione può essere modificata modificando il valore del parametro `geoLocManadatoryOnIpad` in `0`, nei parametri init del campo.

* Quando le informazioni sulla geolocalizzazione sono obbligatorie, all&#39;utente viene presentata un&#39;area di disegno ridotta. Il testo di geolocalizzazione viene aggiunto quando l&#39;utente fa clic sull&#39;icona **OK** sull&#39;area rimanente.
* In altri casi, all&#39;utente viene presentata un&#39;area interamente disegnabile. Se l&#39;utente sceglie di incorporare le informazioni sulla geolocalizzazione, quest&#39;area viene ridimensionata per contenere il testo di geolocalizzazione.

### Cancellazione di una firma {#clearing-a-signature}

Durante l&#39;utilizzo di questa funzione, un utente può fare clic sull&#39;icona **Gomma** per cancellare il campo e ricominciare da capo. Se sono state aggiunte informazioni sulla geolocalizzazione, anche queste vengono eliminate.

### Salvataggio di una firma {#saving-a-signature}

Facendo clic sull&#39;icona **OK** si salva lo scarabocchio come immagine nel campo . L&#39;immagine e i valori possono essere inviati al server per un&#39;ulteriore elaborazione. Una volta che un utente ha fatto clic su **OK**, il campo di scribble è bloccato. Impossibile modificare nuovamente la firma utilizzando il widget scarabocchio.

Toccando o facendo clic sul campo Dispersione si apre la finestra di dialogo in modalità di sola lettura.

![3](assets/3.png)

### Selezione della dimensione della penna {#selecting-pen-size}

Fai clic sull&#39;icona **Pennelli** per visualizzare un elenco delle dimensioni della penna disponibili. Tocca o fai clic su una dimensione della penna per usare la penna corrispondente.

### Elimina firme dal modulo {#delete-signatures-from-the-form}

Per eliminare le firme dal modulo:

* (Dispositivi mobili) Premere a lungo il campo firma e, nella finestra di dialogo di conferma, toccare **Sì**.
* (Desktop) Passa il puntatore del mouse sul campo firma, fai clic sull&#39;icona **Annulla** e nella finestra di dialogo di conferma fai clic su **Sì**.
