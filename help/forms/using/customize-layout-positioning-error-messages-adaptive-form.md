---
title: Personalizzare il layout e il posizionamento dei messaggi di errore di un modulo adattivo
seo-title: Customize layout and positioning of error messages of an adaptive form
description: È possibile personalizzare il layout e il posizionamento dei messaggi di errore di un adattatore per.
seo-description: You can customize layout and positioning of the error messages of an adaptive for.
uuid: 6d3490f6-c867-44c9-a527-55f6d7221f99
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 136ac7e3-9d1f-4d58-bd4f-9dbe09eeafee
docset: aem65
exl-id: 5cb3ee55-f411-4692-84f7-89bf6ade729d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# Personalizzare il layout e il posizionamento dei messaggi di errore di un modulo adattivo{#customize-layout-and-positioning-of-error-messages-of-an-adaptive-form}

È possibile personalizzare il layout e il posizionamento dei messaggi di errore di un modulo adattivo. Puoi eseguire le seguenti personalizzazioni:

* Personalizzare la posizione e il layout della didascalia di un campo senza apportare alcuna modifica alle proprietà CSS corrispondenti
* Personalizzare la posizione dei messaggi di errore in linea
* Personalizzare il contenuto dell’indicatore della guida dinamica
* Personalizzare la posizione dei componenti campo (didascalie, widget, breve descrizione, descrizione lunga e componenti indicatore della guida) senza apportare alcuna modifica alle proprietà CSS corrispondenti

## Personalizzare il layout dei campi {#customize-layout-of-fields}

È possibile personalizzare il layout di un singolo campo o di tutti i campi per modificare la posizione della didascalia e dei messaggi di errore. Per applicare un layout personalizzato a un campo, effettua le seguenti operazioni:

### Personalizzare il layout di un singolo campo {#customize-layout-of-a-single-field}

Per applicare un layout personalizzato a un singolo campo, effettua le seguenti operazioni:

1. Apri il modulo in **Stile** modalità. Per aprire il modulo in modalità stile, nella barra degli strumenti della pagina tocca ![elenco a discesa canvas](assets/canvas-drop-down.png) > **Stile**.
1. Nella barra laterale, sotto **Oggetti modulo**, seleziona il campo e tocca il pulsante di modifica ![pulsante di modifica](assets/edit-button.png).
1. Selezionare lo stato del campo da personalizzare e specificare lo stile dello stato.

   ![Specifica dello stile in linea di un campo](assets/edit-error-state.png)

### Personalizzare il layout di tutti i campi di un modulo {#customize-layout-of-all-the-fields-of-a-form}

Con AEM Forms è ora possibile creare un tema e applicarlo al modulo. L’editor dei temi consente di specificare lo stile dei componenti modulo in un’unica posizione. Quando crei un tema, specifichi lo stile a livello di componente. Per ulteriori informazioni sui temi, vedi [Temi in AEM Forms](../../forms/using/themes.md).

Creare un tema utilizzando l’Editor tema per personalizzare il layout di tutti i campi del modulo. Dopo aver creato un tema, eseguire i seguenti passaggi per applicarlo a un modulo:

1. Apri il modulo in modalità di modifica.
1. In modalità di modifica, seleziona un componente, quindi tocca ![a livello di campo](assets/field-level.png) > **Contenitore di moduli adattivi**, quindi tocca ![cmppr](assets/cmppr.png).
1. Nella barra laterale, in Tema modulo adattivo, selezionare il tema creato utilizzando l’Editor tema.

## Creare un layout di campo personalizzato {#create-a-custom-field-layout}

1. Apri CRXDE lite. L’URL predefinito è https://&#39;[server]:[porta]&quot;/crx/de.
1. Copia un layout di campo dal nodo /libs/fd/af/layouts/field (Ad esempio, defaultFieldLayout) al nodo /apps (ad esempio, /apps/af-field-layout).
1. Rinominare il nodo copiato e il file defaultFieldLayout.jsp. Ad esempio, errorOnRight.jsp.

1. Modifica il valore delle proprietà qtip e jcr:description del nodo copiato. Ad esempio, modifica il valore delle proprietà in Errore a destra

1. Per aggiungere nuovi stili e comportamenti, crea una libreria client nel nodo /etc.

   Ad esempio, nel percorso /etc/af-field-layout-clientlib, crea il nodo client-library. Aggiungi la proprietà categories con il file af.field.errorOnRight e style.less con il seguente codice:

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

1. Per migliorare l&#39;aspetto e il comportamento, includi la libreria client creata nel file di layout (errorOnRight.jsp).
1. Apri la finestra di dialogo di modifica del campo e seleziona la **Stile** scheda . In **Configura layout campo** casella a discesa, seleziona il layout appena creato e fai clic su **OK**.

Il pacchetto ErrorOnRight.zip contiene codice per mostrare messaggi di errore sul lato destro dei campi.

[Ottieni file](assets/erroronright.zip)
