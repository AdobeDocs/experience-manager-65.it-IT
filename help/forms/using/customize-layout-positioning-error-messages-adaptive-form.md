---
title: Personalizzare il layout e il posizionamento dei messaggi di errore di un modulo adattivo
seo-title: Personalizzare il layout e il posizionamento dei messaggi di errore di un modulo adattivo
description: 'Potete personalizzare il layout e il posizionamento dei messaggi di errore di un adattatore per. '
seo-description: 'Potete personalizzare il layout e il posizionamento dei messaggi di errore di un adattatore per. '
uuid: 6d3490f6-c867-44c9-a527-55f6d7221f99
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 136ac7e3-9d1f-4d58-bd4f-9dbe09eeafee
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 0%

---


# Personalizzare il layout e il posizionamento dei messaggi di errore di un modulo adattivo{#customize-layout-and-positioning-of-error-messages-of-an-adaptive-form}

È possibile personalizzare il layout e il posizionamento dei messaggi di errore di un modulo adattivo. Potete eseguire le seguenti personalizzazioni:

* Personalizzare la posizione e il layout della didascalia di un campo senza apportare alcuna modifica alle proprietà CSS corrispondenti
* Personalizzazione della posizione dei messaggi di errore in linea
* Personalizzazione del contenuto dell’indicatore della guida dinamica
* Personalizzare la posizione dei componenti del campo (didascalie, widget, descrizione breve, descrizione lunga e componenti degli indicatori della guida) senza apportare alcuna modifica alle proprietà CSS corrispondenti

## Personalizzare il layout dei campi {#customize-layout-of-fields}

È possibile personalizzare il layout di un singolo campo o di tutti i campi per modificare la posizione di didascalie e messaggi di errore. Per applicare un layout personalizzato a un campo, effettuare le operazioni seguenti:

### Personalizzare il layout di un singolo campo {#customize-layout-of-a-single-field}

Per applicare un layout personalizzato a un singolo campo, effettuate le seguenti operazioni:

1. Aprire il modulo in modalità **Stile**. Per aprire il modulo in modalità stile, nella barra degli strumenti della pagina toccare ![a discesa quadro](assets/canvas-drop-down.png) > **Stile**.
1. Nella barra laterale, in **Oggetti modulo**, selezionare il campo e toccare il pulsante di modifica ![edit-button](assets/edit-button.png).
1. Selezionate lo stato del campo da personalizzare e specificate lo stile per tale stato.

   ![Specifica dello stile in linea di un campo](assets/edit-error-state.png)

### Personalizzare il layout di tutti i campi di un modulo {#customize-layout-of-all-the-fields-of-a-form}

Con  AEM Forms è ora possibile creare un tema e applicarlo al modulo. L’editor di temi consente di specificare lo stile dei componenti modulo in un’unica posizione. Quando create un tema, specificate lo stile a livello di componente. Per ulteriori informazioni sui temi, vedere [Temi in  AEM Forms](../../forms/using/themes.md).

Creare un tema utilizzando l&#39;Editor tema per personalizzare il layout di tutti i campi del modulo. Dopo aver creato un tema, effettuare le seguenti operazioni per applicarlo a un modulo:

1. Aprire il modulo in modalità di modifica.
1. In modalità di modifica, selezionate un componente, quindi toccate ![livello campo](assets/field-level.png) > **Contenitore modulo adattivo**, quindi toccate ![cmppr](assets/cmppr.png).
1. Nella barra laterale, in Tema modulo adattivo, selezionare il tema creato utilizzando l&#39;Editor tema.

## Creare un layout di campo personalizzato {#create-a-custom-field-layout}

1. Aprire CRXDE lite. L&#39;URL predefinito è https://&#39;[server]:[porta]&#39;/crx/de.
1. Copiate un layout di campo dal nodo /libs/fd/af/layouts/field (ad esempio, defaultFieldLayout) al nodo /apps (ad esempio, /apps/af-field-layout).
1. Rinominare il nodo copiato e il file defaultFieldLayout.jsp. Ad esempio, errorOnRight.jsp.

1. Modificate il valore delle proprietà qtip e jcr:description del nodo copiato. Ad esempio, modificare il valore delle proprietà in Errore a destra

1. Per aggiungere nuovi stili e comportamenti, create una libreria client nel nodo /etc.

   Ad esempio, nel percorso /etc/af-field-layout-clientlib, creare il nodo client-library. Aggiungete la proprietà category con il file af.field.errorOnRight e style.less con il seguente codice:

   ```css
   .widgetErrorWrapper {
   
    height: 38px;
    margin: 5px;
   
    .guideFieldWidget{
    width: 60%;
    float: left; 
    }
   
    .guideFieldError{
    overflow:hidden;
    width:40%; 
    }
   
   }
   ```

1. Per migliorare l&#39;aspetto e il comportamento, includete la libreria client creata nel file di layout (errorOnRight.jsp).
1. Aprire la finestra di dialogo di modifica del campo e selezionare la scheda **Attribuzione stile**. Nella casella a discesa **Configura layout campo**, selezionare il layout appena creato e fare clic su **OK**.

Il pacchetto ErrorOnRight.zip contiene codice che mostra i messaggi di errore sul lato destro dei campi.

[Ottieni file](assets/erroronright.zip)
