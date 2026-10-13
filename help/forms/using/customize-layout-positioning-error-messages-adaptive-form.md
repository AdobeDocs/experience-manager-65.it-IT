---
title: Personalizzare il layout e il posizionamento dei messaggi di errore di un modulo adattivo
description: Puoi personalizzare il layout e il posizionamento dei messaggi di errore di un adattivo per.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
docset: aem65
exl-id: 5cb3ee55-f411-4692-84f7-89bf6ade729d
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,Foundation Components
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 7da902b6-fe94-5180-8e7c-f6d1e38d01d5
    internal-label: Foundation Components
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 5%
---
# Personalizzare il layout e il posizionamento dei messaggi di errore di un modulo adattivo{#customize-layout-and-positioning-of-error-messages-of-an-adaptive-form}

È possibile personalizzare il layout e il posizionamento dei messaggi di errore di un modulo adattivo. Puoi eseguire le seguenti personalizzazioni:

* Personalizza la posizione e il layout della didascalia di un campo senza modificare le proprietà CSS corrispondenti
* Personalizzare la posizione dei messaggi di errore in linea
* Personalizza il contenuto dell’indicatore della guida dinamica
* Personalizza la posizione dei componenti campo (sottotitoli, widget, descrizione breve, descrizione lunga e indicatori di aiuto) senza modificare le proprietà CSS corrispondenti

## Personalizzare il layout dei campi {#customize-layout-of-fields}

È possibile personalizzare il layout di un singolo campo o di tutti i campi per modificare la posizione della didascalia e dei messaggi di errore.

Per applicare un layout personalizzato a un campo, eseguire le operazioni seguenti:

### Personalizzare il layout di un singolo campo {#customize-layout-of-a-single-field}

1. Apri il modulo in modalità **Stile**. Per aprire il modulo in modalità stile, nella barra degli strumenti della pagina seleziona ![elenco a discesa nell&#39;area di lavoro](assets/canvas-drop-down.png) > **Stile**.
1. Nella barra laterale, in **Oggetti modulo**, seleziona il campo e il pulsante di modifica ![edit-button](assets/edit-button.png).
1. Seleziona lo stato del campo da personalizzare e specifica lo stile per tale stato.

   ![Specifica dello stile in linea di un campo](assets/edit-error-state.png)

### Personalizzare il layout di tutti i campi di un modulo {#customize-layout-of-all-the-fields-of-a-form}

Con AEM Forms, ora puoi creare un tema e applicarlo al modulo. L’editor tema consente di specificare lo stile dei componenti modulo in un’unica posizione. Quando create un tema, specificate lo stile a livello di componente. Per ulteriori informazioni sui temi, vedere [Temi in AEM Forms](../../forms/using/themes.md).

Creare un tema utilizzando Editor tema per personalizzare il layout di tutti i campi del modulo. Dopo aver creato un tema, effettuare le seguenti operazioni per applicarlo a un modulo:

1. Apri il modulo in modalità di modifica.
1. In modalità di modifica, seleziona un componente, quindi seleziona ![livello campo](assets/field-level.png) > **Contenitore modulo adattivo**, quindi seleziona ![cmppr](assets/cmppr.png).
1. Nella barra laterale, in Tema modulo adattivo, seleziona il tema creato utilizzando l’Editor tema.

## Creare un layout di campo personalizzato {#create-a-custom-field-layout}

1. Apri CRXDE Lite. L&#39;URL predefinito è https://&#39;[server]:[porta]&#39;/crx/de.
1. Copiare un layout di campo dal nodo /libs/fd/af/layouts/field (ad esempio, defaultFieldLayout) al nodo /apps (ad esempio, /apps/af-field-layout).
1. Rinomina il nodo copiato e il file defaultFieldLayout.jsp. Ad esempio, errorOnRight.jsp.

1. Modificare il valore delle proprietà qtip e jcr:description del nodo copiato. Ad esempio, modifica il valore delle proprietà in Errore a destra

1. Per aggiungere nuovi stili e comportamenti, crea una libreria client nel nodo /etc.

   Ad esempio, nella posizione /etc/af-field-layout-clientlib, crea la libreria client del nodo. Aggiungi la proprietà Categories con il valore af.field.errorOnRight e il file style.less con il seguente codice:

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

1. Per migliorare l’aspetto e il comportamento, includi la libreria client creata nel file di layout (errorOnRight.jsp).
1. Apri la finestra di dialogo di modifica del campo e seleziona la scheda **Stile**. Nella casella a discesa **Configura layout campo**, selezionare il layout appena creato e fare clic su **OK**.

Il pacchetto ErrorOnRight.zip contiene codice per visualizzare messaggi di errore sul lato destro dei campi.

[Ottieni il file](assets/erroronright.zip)
