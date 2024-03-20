---
title: Personalizzazione dei messaggi di errore per i moduli HTML5
description: Scopri come personalizzare la visualizzazione dei messaggi di errore per i moduli HTML5, incluso come modificarne la posizione e l’aspetto.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
feature: HTML5 Forms
exl-id: c4ae53a3-8de1-4985-a73e-829749de9814
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 0%

---

# Personalizzazione dei messaggi di errore per i moduli HTML5 {#customizing-error-messages-for-html-forms}

Nei moduli di HTML5, i messaggi di errore e gli avvisi hanno una posizione e un aspetto fissi (carattere e colore), l’errore viene visualizzato solo per un campo selezionato e solo un errore.

L’articolo descrive i passaggi per personalizzare i messaggi di errore di HTML5 Forms in modo da poter effettuare le seguenti operazioni:

* modificare l&#39;aspetto e la posizione dei messaggi di errore. Puoi fare in modo che l’errore venga visualizzato nella parte superiore, inferiore e destra di qualsiasi campo.
* visualizza messaggi di errore per più campi in un dato momento.
* visualizza l’errore indipendentemente dal fatto che un campo sia selezionato o meno.

## Personalizzazione dei messaggi di errore  {#customizing-error-messages-nbsp}

Prima di personalizzare i messaggi di errore, scarica ed estrai il pacchetto associato (CustomErrorManager-1.0-SNAPSHOT.zip).

Dopo aver estratto il pacchetto, apri la cartella CustomErrorManager-1.0-SNAPSHOT. Contiene le cartelle jcr_root e META-INF. Queste cartelle contengono i file CSS e JS necessari per personalizzare il messaggio di errore.

[Ottieni file](assets/customerrormanager-1.0-snapshot.zip)

### Personalizzazione della posizione dei messaggi di errore  {#customizing-the-position-of-error-messages-nbsp}

Per personalizzare la posizione del messaggio di errore, aggiungere una &lt;div> per ogni campo di errore e avviso, posizionare il tag &lt;div> a sinistra o a destra e applicare gli stili css al &lt;div> tag. Per i passaggi dettagliati, consulta la procedura indicata di seguito:

1. Accedi a `CustomErrorManager-1.0-SNAPSHOT`e aprire la `etc\clientlibs\mf-custom-error-manager\CustomErrorManager\javascript` cartella.
1. Apri `customErrorManager.js` file per la modifica. Il `markError` nel file accetta i seguenti parametri:

   |   |  |
   |---|---|
   | jqWidget | jqWidget è l&#39;handle di un widget. |
   | msg | contiene il messaggio di errore |
   | tipo | indica se si tratta di un errore o di un avviso |

1. Nell’implementazione predefinita, a destra del campo vengono visualizzati messaggi di errore. Per visualizzare i messaggi di errore nella parte superiore, utilizzare il codice seguente.

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

1. Salva e chiudi il file.
1. Accedi a `CustomErrorManager-1.0-SNAPSHOT` e creare un archivio di cartelle jcr_root e META-INF. Rinomina l’archivio in CustomErrorManager-1.0-SNAPSHOT.zip.
1. Utilizza Gestione pacchetti per caricare e installare il pacchetto.

## Visualizzare messaggi di errore per più campi  {#display-error-messages-for-multiple-fields-nbsp}

Utilizza il pacchetto allegato per visualizzare simultaneamente i messaggi di errore per tutti i campi. Per visualizzare un singolo messaggio di errore, utilizza il profilo predefinito.

### Personalizzazione dell&#39;aspetto dei messaggi di errore.  {#customizing-the-appearance-of-error-messages-nbsp}

1. Passa alla cartella etc\clientlibs\mf-custom-error-manager\CustomErrorManager\css.

1. Apri il file sample.css per la modifica. Il file css contiene 2 id- #customError, #customWarning. Puoi utilizzare questi ID per modificare varie proprietà, come il colore e la dimensione del font.

   Utilizzare il codice seguente per modificare la dimensione e il colore del carattere dei messaggi di errore/avviso.

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

1. Salva e chiudi il file.
1. Passare alla cartella CustomErrorManager-1.0-SNAPSHOT e creare un archivio di cartelle jcr_root e META-INF. Rinomina l’archivio in CustomErrorManager-1.0-SNAPSHOT.zip.
1. Utilizza Gestione pacchetti per caricare e installare il pacchetto.

## Esegui il rendering del modulo con il nuovo profilo.  {#render-the-form-with-the-new-profile-nbsp}

I moduli html5 utilizzano un profilo predefinito per impostazione predefinita: `https://&lt;server&gt;/content/xfaforms/profiles/default.html?contentRoot=&lt;xdp location&gt;&template=&lt;name of the xdp&gt;`

Per visualizzare un modulo con i messaggi di errore personalizzati, esegui il rendering del modulo con il profilo di errore: `https://&lt;server&gt;/content/xfaforms/profiles/error.html?contentRoot=&lt;xdp location&gt;&template=&lt;name of the xdp&gt;`

>[!NOTE]
>
>Il pacchetto allegato installa il profilo di errore.
