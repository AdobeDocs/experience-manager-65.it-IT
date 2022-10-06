---
title: Uso della firma digitale nei moduli di HTML5
seo-title: Using Scribble Signature in HTML5 forms
description: I moduli di HTML5 vengono sempre più utilizzati sui dispositivi touch e un requisito comune consiste nel supportare le firme. La firma di documenti su dispositivi mobili sta diventando un modo accettato di firmare moduli su dispositivi mobili.
seo-description: HTML5 forms are increasingly used on touch devices, and one common requirement is to support signatures. Signing documents on mobile devices is becoming an accepted way of signing forms on mobile devices.
uuid: 163dd55a-971a-4dd4-93a7-a14e80184d9b
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: designer
discoiquuid: ecd7f538-9c24-48e7-8450-596851e99cff
docset: aem65
feature: Designer
exl-id: 2025182f-195b-40d0-aee7-67669f55b964
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 0%

---

# Uso della firma digitale nei moduli di HTML5{#using-scribble-signature-in-html-forms}

I moduli HTML5 vengono sempre più utilizzati sui dispositivi touch e un requisito comune è il supporto delle firme. La scrittura (con un dito o uno stilo) sta diventando un modo accettato di firmare i moduli su dispositivi mobili. I moduli di HTML5 e Forms Designer consentono ora di utilizzare un campo firma script sul modulo. Quando viene eseguito il rendering del modulo nel browser, è possibile accedere a tali campi utilizzando uno stilo, un mouse o un tocco.

## Progettazione di un modulo con il campo Firma digitale {#how-to-design-a-form-using-scribble-signature-field}

1. Aprire un modulo in Forms Designer.
1. Trascinare il campo Firma digitale sulla pagina.

   ![designer_scribble](assets/designer_scribble.png)

   >[!NOTE]
   >
   >I Dimension del campo selezionato in Forms Designer vengono visualizzati durante il rendering del campo. Tuttavia, le dimensioni della casella della firma di cui è stato eseguito il rendering vengono calcolate in base alle proporzioni del campo e non in base alla dimensione specificata in Forms Designer.

1. Configurare il campo Firma digitale.

   Il campo Firma frammento, per impostazione predefinita, contrassegna le informazioni sulla geolocalizzazione come obbligatorie durante il processo di firma su iPad (ed è facoltativo per altri dispositivi). Questo comportamento predefinito può essere ignorato modificando il valore del `geoLocMandatoryOnIpad` proprietà. Questa proprietà viene esposta come extra nel campo Firma documento. I passaggi per modificarlo sono i seguenti:

   1. Nel modulo, selezionare il campo Firma.
   1. Seleziona la **Sorgente XML** scheda .

      >[!NOTE]
      >
      >Per aprire la scheda Sorgente XML, fare clic su **Visualizza** > **Sorgente XML**.

   1. Individua il `<ui>` in `<field>` assegna tag al codice sorgente e modificalo nel modo seguente:

      ```xml
      <extras name="x-scribble-add-on">
      <boolean name="geoLocMandatoryOnIpad">0</boolean>
      </extras>
      ```

   1. Seleziona la **Visualizzazione Struttura** scheda . Nella casella di conferma, fai clic su **Sì**.
   1. Salvare il modulo.

1. Eseguire il rendering del modulo su un browser desktop/dispositivo supportato.

## Interfaccia con le firme scorrevoli {#interfacing-with-the-scribble-signatures}

### Firma {#signing}

Una volta aggiunto al modulo un campo Firma digitale ed eseguito il rendering, si apre una finestra di dialogo facendo clic o toccando il campo. L&#39;utente può scarabocchiare una firma nell&#39;area di disegno designata da un rettangolo punteggiato utilizzando un mouse, un dito o uno stilo.

![geolocalizzazione](assets/geolocation.png)

**A.** Pennello **B.** Gomma **C.** Geolocalizzazione **D.** Informazioni sulla geolocalizzazione

### Geo-tagging {#geo-tagging}

Facendo clic sull’icona di geolocalizzazione durante la creazione dello scarabocchio, le informazioni relative alla posizione geografica e all’ora vengono incorporate nel campo.

>[!NOTE]
In iPad, per impostazione predefinita, è obbligatorio incorporare le informazioni sulla geolocalizzazione.

In iPad, l’icona di geolocalizzazione non viene visualizzata per impostazione predefinita e le informazioni di geolocalizzazione vengono incorporate automaticamente quando fai clic su **OK**.

Per gli iPad, questa impostazione può essere modificata modificando il valore di `geoLocManadatoryOnIpad` parametro a `0`, nei parametri init del campo .

* Quando le informazioni sulla geolocalizzazione sono obbligatorie, all&#39;utente viene presentata un&#39;area di disegno ridotta. Il testo di geolocalizzazione viene aggiunto quando l’utente fa clic su **OK** sull&#39;area rimanente.
* In altri casi, all&#39;utente viene presentata un&#39;area interamente disegnabile. Se l&#39;utente sceglie di incorporare le informazioni sulla geolocalizzazione, quest&#39;area viene ridimensionata per contenere il testo di geolocalizzazione.

### Cancellazione di una firma {#clearing-a-signature}

Quando utilizzi questa funzione, un utente può fare clic sul pulsante **Gomma** per cancellare il campo e ricominciare da capo. Se sono state aggiunte informazioni sulla geolocalizzazione, anche queste vengono eliminate.

### Salvataggio di una firma {#saving-a-signature}

Fai clic su **OK** salva lo scarabocchio come immagine nel campo . L&#39;immagine e i valori possono essere inviati al server per un&#39;ulteriore elaborazione. Una volta fatto clic su **OK**, il campo scarabocchio è bloccato. Impossibile modificare nuovamente la firma utilizzando il widget scarabocchio.

Toccando o facendo clic sul campo Dispersione si apre la finestra di dialogo in modalità di sola lettura.

![3](assets/3.png)

### Selezione della dimensione della penna {#selecting-pen-size}

Fai clic sul pulsante **Pennelli** per visualizzare un elenco delle dimensioni disponibili della penna. Tocca o fai clic su una dimensione della penna per usare la penna corrispondente.

### Elimina firme dal modulo {#delete-signatures-from-the-form}

Per eliminare le firme dal modulo:

* (Dispositivi mobili) Premere a lungo il campo firma e, nella finestra di dialogo di conferma, toccare **Sì**.
* (Desktop) Passa il puntatore del mouse sul campo firma e fai clic sul pulsante **Annulla** e nella finestra di dialogo di conferma fai clic su **Sì**.
