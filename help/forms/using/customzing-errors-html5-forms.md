---
title: Personalizzazione dei messaggi di errore per i moduli HTML5
seo-title: Personalizzazione dei messaggi di errore per i moduli HTML5
description: Scoprite come personalizzare la visualizzazione dei messaggi di errore per i moduli HTML5 e come modificarne posizione e aspetto.
seo-description: Scoprite come personalizzare la visualizzazione dei messaggi di errore per i moduli HTML5 e come modificarne posizione e aspetto.
uuid: 6f48b64e-858f-4323-ad50-88e25f3c2e3d
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 44e49789-9075-41b3-bce8-03e8efce2d5a
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 0%

---


# Personalizzazione dei messaggi di errore per i moduli HTML5 {#customizing-error-messages-for-html-forms}

Nei moduli HTML5, i messaggi di errore e gli avvisi hanno un aspetto e una posizione fissi (font e colore), l&#39;errore viene visualizzato solo per un campo selezionato e viene visualizzato un solo errore.

L’articolo fornisce i passaggi necessari per personalizzare i messaggi di errore dei moduli HTML5,

* modificare l&#39;aspetto e la posizione dei messaggi di errore. È possibile visualizzare un errore in alto, in basso e a destra di qualsiasi campo.
* visualizzare messaggi di errore per più campi in un dato momento.
* visualizza l&#39;errore indipendentemente dal fatto che sia selezionato o meno un campo.

## Personalizzazione dei messaggi di errore  {#customizing-error-messages-nbsp}

Prima di personalizzare i messaggi di errore, scaricate ed estraete il pacchetto allegato (CustomErrorManager-1.0-SNAPSHOT.zip).

Dopo aver estratto il pacchetto, aprite la cartella CustomErrorManager-1.0-SNAPSHOT. Contiene le cartelle jcr_root e META-INF. Queste cartelle contengono i file CSS e JS richiesti per personalizzare il messaggio di errore.

[Ottieni file](assets/customerrormanager-1.0-snapshot.zip)

### Personalizzazione della posizione dei messaggi di errore  {#customizing-the-position-of-error-messages-nbsp}

Per personalizzare la posizione del messaggio di errore, aggiungere il tag &lt;div> per ciascun campo di errore e di avviso, posizionare il tag &lt;div> a sinistra o a destra e applicare gli stili css al tag &lt;div>. Per i passaggi dettagliati, consulta la procedura indicata di seguito:

1. Andate alla cartella `CustomErrorManager-1.0-SNAPSHOT`e aprite la cartella `etc\clientlibs\mf-custom-error-manager\CustomErrorManager\javascript`.
1. Aprire il file `customErrorManager.js` per la modifica. La funzione `markError` nel file accetta i seguenti parametri:

   |  |  |
   |---|---|
   | jqWidget | jqWidget è la maniglia del widget. |
   | msg | contiene il messaggio di errore |
   | tipo | indica se si tratta di un errore o di un avviso |

1. All&#39;esterno dell&#39;implementazione, a destra del campo viene visualizzato un messaggio di errore. Per visualizzare i messaggi di errore nella parte superiore, utilizzate il seguente codice.

   ```javascript
   markError: function (jqWidget, msg, type) {
               var element = jqWidget.element,                                //Gives the div containing widget
                   pos = $(element).offset(),                          //Calculates the position of the div in the view port
                                                                   msgHeight = xfalib.view.util.TextMetrics.measureExtent(msg).height + 5;  //Calculating the height of the Error Message
                   styles = {};
                   styles.left = pos.left + "px";         // Assign the desired left position using pos.left. Here it is calculated for exact left of the field
                   styles.top = pos.top - msgHeight + "px";  // Assign the desired top position using pos.top. Here it is calculated for top of the field
               if (type != "warning") {
                   if(!jqWidget.errorDiv){
                                                                                   //Adding the warning div if it is not present already
                       jqWidget.errorDiv=$("<div id='customError'></div>").appendTo('body');
                   }
                   jqWidget.$css(jqWidget.errorDiv.get(0), styles); // Applying the styles to the warning div
                   jqWidget.errorDiv.text(msg).show();                     //Showing the warning message
               } else {
                   if(!jqWidget.errorDiv){
                                                                                   //Adding the error div if it is not present already
                       jqWidget.errorDiv=$("<div id='customWarning'></div>").appendTo('body');
                   }
                   jqWidget.$css(jqWidget.errorDiv.get(0), styles); // Applying the styles to the error div
                   jqWidget.errorDiv.text(msg).show();                     //Showing the warning message
               }
   
           },
   ```

1. Salvate e chiudete il file.
1. Andate alla cartella `CustomErrorManager-1.0-SNAPSHOT` e create un archivio delle cartelle jcr_root e META-INF. Rinominare l&#39;archivio in CustomErrorManager-1.0-SNAPSHOT.zip.
1. Utilizzate il gestore pacchetti per caricare e installare il pacchetto.

## Visualizza messaggi di errore per più campi  {#display-error-messages-for-multiple-fields-nbsp}

Usate il pacchetto allegato per visualizzare simultaneamente messaggi di errore per tutti i campi. Per visualizzare un singolo messaggio di errore, utilizzare il profilo predefinito.

### Personalizzazione dell&#39;aspetto dei messaggi di errore.  {#customizing-the-appearance-of-error-messages-nbsp}

1. Andate alla directory etc\clientlibs\mf-custom-error-manager\CustomErrorManager\css folder.

1. Aprite il file sample.css per la modifica. Il file css contiene 2 ID - #customError, #customWarning. Potete utilizzare questi ID per modificare diverse proprietà quali il colore, la dimensione del font e così via.

   Utilizzare il codice seguente per modificare la dimensione del font e il colore dei messaggi di errore/avviso.

   ```css
   #customError {
   color: #0000FF; // it changes the color of Error Message
   display:none;
   position:absolute;
   opacity:0.85;
   font-size: 24px;  // it changes the font size of Error Message
   z-index:5;
   }
   
   #customWarning {
   color: #00FF00;  // it changes the color of Warning Message
   display:none;
   position:absolute;
   opacity:0.85;
   font-size: 18px;   // it changes the font size of Warning Message
   z-index:5;
   }
   
   Save the changes.
   ```

1. Salvate e chiudete il file.
1. Andate alla cartella CustomErrorManager-1.0-SNAPSHOT e create un archivio delle cartelle jcr_root e META-INF. Rinominare l&#39;archivio in CustomErrorManager-1.0-SNAPSHOT.zip.
1. Utilizzate il gestore pacchetti per caricare e installare il pacchetto.

## Eseguire il rendering del modulo con il nuovo profilo.  {#render-the-form-with-the-new-profile-nbsp}

I moduli HTML5 utilizzano un profilo predefinito: https://&lt;server>/content/xfaforms/profiles/default.html?contentRoot=&lt;percorso xdp>&amp;template=&lt;nome dell&#39;xdp>

Per visualizzare un modulo con messaggi di errore personalizzati, eseguire il rendering del modulo con il profilo di errore: https://&lt;server>/content/xfaforms/profiles/error.html?contentRoot=&lt;percorso xdp>&amp;template=&lt;nome dell&#39;xdp>

>[!NOTE]
>
>Il pacchetto allegato installa il profilo di errore.

