---
title: Uso della firma scorrevole nei moduli HTML5
seo-title: Uso della firma scorrevole nei moduli HTML5
description: I moduli HTML5 sono sempre più utilizzati sui dispositivi touch e un requisito comune è il supporto delle firme. La firma di documenti su dispositivi mobili sta diventando un metodo accettato per firmare moduli su dispositivi mobili.
seo-description: I moduli HTML5 sono sempre più utilizzati sui dispositivi touch e un requisito comune è il supporto delle firme. La firma di documenti su dispositivi mobili sta diventando un metodo accettato per firmare moduli su dispositivi mobili.
uuid: 163dd55a-971a-4dd4-93a7-a14e80184d9b
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: designer
discoiquuid: ecd7f538-9c24-48e7-8450-596851e99cff
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 0%

---


# Utilizzo della firma scorrevole nei moduli HTML5{#using-scribble-signature-in-html-forms}

I moduli HTML5 vengono sempre più utilizzati sui dispositivi touch e un requisito comune è il supporto delle firme. La creazione di script (con penna o dito) sta diventando un metodo accettato per firmare i moduli sui dispositivi mobili. I moduli HTML5 e Forms Designer consentono ora di inserire nel modulo un campo firma con script. Durante il rendering del modulo nel browser, è possibile accedere a tali campi utilizzando uno stilo, un mouse o un tocco.

## Come progettare un modulo utilizzando il campo Firma scarabocchio {#how-to-design-a-form-using-scribble-signature-field}

1. Aprire un modulo in Forms Designer.
1. Trascinare il campo Firma documento sulla pagina.

   ![designer_scribble](assets/designer_scribble.png)

   >[!NOTE]
   >
   >Dimension del campo selezionato in Forms Designer vengono visualizzati durante il rendering del campo. Tuttavia, le dimensioni della casella della firma sottoposta a rendering vengono calcolate in base alle proporzioni del campo e non in base alle dimensioni specificate in Forms Designer.

1. Configurare il campo Firma scarabocchio.

   Per impostazione predefinita, il campo Firma scarabocchio contrassegna le informazioni sulla geolocalizzazione come obbligatorie durante il processo di firma sull’iPad (ed è facoltativo per altri dispositivi). Questo comportamento predefinito può essere ignorato modificando il valore della proprietà `geoLocMandatoryOnIpad`. Questa proprietà è esposta come extras nel campo Firma scarabocchio. I passaggi per modificarlo sono:

   1. Nel modulo, selezionare il campo Firma tramite scarabocchio.
   1. Selezionare la scheda **Sorgente XML**.

      >[!NOTE]
      >
      >Per aprire la scheda Sorgente XML, fare clic su **Visualizza** > **Sorgente XML**.

   1. Individuate il tag `<ui>` nel tag `<field>` e modificate il codice sorgente in modo che abbia l&#39;aspetto seguente:

      ```xml
      <extras name="x-scribble-add-on">
      <boolean name="geoLocMandatoryOnIpad">0</boolean>
      </extras>
      ```

   1. Selezionare la scheda **Visualizzazione struttura**. Nella casella di conferma, fare clic su **Sì**.
   1. Salvare il modulo.

1. Eseguire il rendering del modulo su un browser dispositivo/desktop supportato.

## Interfacciamento con le firme scorrevoli {#interfacing-with-the-scribble-signatures}

### Firma {#signing}

Dopo aver aggiunto il campo Firma scarabocchio al modulo ed eseguito il rendering, si apre una finestra di dialogo facendo clic o toccando il campo. È possibile creare uno script con una firma nell&#39;area di disegno indicata da un rettangolo punteggiato utilizzando il mouse, un dito o uno stilo.

![geolocalizzazione](assets/geolocation.png)

**A.** Pennello  **B.** Gomma  **C.** Geolocalizzazione  **D.** Geolocalizzazione

### Assegnazione di tag geografici {#geo-tagging}

Facendo clic sull&#39;icona di geolocalizzazione durante la creazione dello script, le informazioni relative alla posizione geografica e all&#39;ora vengono incorporate nel campo.

>[!NOTE]
Per impostazione predefinita, sull’iPad le informazioni relative alla geolocalizzazione sono obbligatorie.

Sull&#39;iPad, l&#39;icona della geolocalizzazione non viene visualizzata per impostazione predefinita e le informazioni sulla geolocalizzazione vengono automaticamente incorporate quando si fa clic su **OK**.

Per gli iPad, questa impostazione può essere modificata modificando il valore del parametro `geoLocManadatoryOnIpad` in `0`, nei parametri init del campo.

* Quando le informazioni sulla geolocalizzazione sono obbligatorie, all&#39;utente viene presentata un&#39;area di disegno ridotta. Il testo della geolocalizzazione viene aggiunto quando l&#39;utente fa clic sull&#39;icona **OK** nell&#39;area rimanente.
* In altri casi, all&#39;utente viene presentata un&#39;area di disegno completa. Se l&#39;utente sceglie di incorporare le informazioni sulla geolocalizzazione, quest&#39;area viene ridimensionata per contenere il testo della geolocalizzazione.

### Cancellazione di una firma {#clearing-a-signature}

Durante l&#39;utilizzo di questa funzione, un utente può fare clic sull&#39;icona **Gomma** per cancellare il campo e ricominciare. Se sono state aggiunte informazioni sulla geolocalizzazione, anche queste vengono eliminate.

### Salvataggio di una firma {#saving-a-signature}

Facendo clic sull&#39;icona **OK** lo script viene salvato come immagine nel campo. L’immagine e i valori possono essere inviati al server per un’ulteriore elaborazione. Dopo che un utente ha fatto clic su **OK**, il campo dello script viene bloccato. La firma non può essere modificata di nuovo utilizzando il widget degli script.

Toccando o facendo clic sul campo scarabocchio si apre la finestra di dialogo in modalità di sola lettura.

![3](assets/3.png)

### Selezione della dimensione della penna {#selecting-pen-size}

Fate clic sull&#39;icona **Pennelli** per visualizzare un elenco delle dimensioni di penna disponibili. Tocca o fai clic su una dimensione della penna per usare la penna corrispondente.

### Eliminazione di firme dal modulo {#delete-signatures-from-the-form}

Per eliminare le firme dal modulo:

* (Dispositivi mobili) Tenere premuto il campo firma e, nella finestra di dialogo di conferma, toccare **Sì**.
* (Desktop) Passate il puntatore del mouse sul campo firma, fate clic sull&#39;icona **Annulla** e, nella finestra di dialogo di conferma, fate clic su **Sì**.
