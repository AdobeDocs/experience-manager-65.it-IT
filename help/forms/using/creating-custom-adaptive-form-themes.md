---
title: Creazione di temi di moduli adattivi personalizzati
seo-title: Creating custom adaptive form themes
description: Un tema per moduli adattivi è una libreria client AEM che puoi utilizzare per definire gli stili (look and feel) di un modulo adattivo. Scopri come creare temi di moduli adattivi personalizzati.
seo-description: An adaptive form theme is an AEM client library that you use to define the styles (look and feel) for an adaptive form. Learn how you can create custom adaptive form themes.
uuid: b25df10e-b07c-4e9d-a799-30f1c6fb3c44
content-type: reference
topic-tags: customization
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 437e6581-4eb1-4fbd-a6da-86b9c90cec89
exl-id: 73b0057f-082d-4502-90e2-5e41b52c1185
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 0%

---

# Creazione di temi di moduli adattivi personalizzati {#creating-custom-adaptive-form-themes}

>[!CAUTION]
>
>AEM Forms fornisce [Editor temi](/help/forms/using/themes.md) possibilità di creare e modificare moduli adattivi [temi](/help/forms/using/themes.md). Esegui i passaggi elencati in questo articolo solo se hai effettuato l’aggiornamento da una versione che non dispone di [Editor temi](/help/forms/using/themes.md) inoltre, è disponibile un investimento in temi creati utilizzando file Less/CSS (metodo di editor pre-tema).

## Prerequisiti {#prerequisites}

* Conoscenza del framework LESS (Leaner CSS)
* Creare una libreria client in Adobe Experience Manager
* [Creazione di un modello di modulo adattivo](/help/forms/using/custom-adaptive-forms-templates.md) per utilizzare il tema creato

## Tema modulo adattivo {#adaptive-form-theme}

Un **tema modulo adattivo** è una libreria client AEM che puoi utilizzare per definire gli stili (look and feel) di un modulo adattivo.

Crea un’ **modello adattivo** e applica il tema al modello. Puoi quindi utilizzare questo modello personalizzato per creare un’ **modulo adattivo**.

![Modulo adattivo e libreria client](assets/hierarchy.png)

## Per creare un tema per moduli adattivi {#to-create-an-adaptive-form-theme}

>[!NOTE]
>
>La procedura seguente viene descritta utilizzando nomi di esempio per gli oggetti AEM come nodo, proprietà e cartelle.
>
>Se si esegue la procedura seguente utilizzando i nomi, il modello risultante dovrebbe essere simile allo snapshot seguente:

![Snapshot modulo adattivo a tema foresta](assets/thumbnail.png)
**Figura:** *Esempio di tema foresta*

1. Creare un nodo di tipo `cq:ClientLibraryFolder` sotto `/apps`nodo.

   Ad esempio, crea il seguente nodo:

   `/apps/myAfThemes/forestTheme`

1. Aggiungere una proprietà stringa multivalore `categories` sul nodo e impostarne il valore in modo appropriato.

   Ad esempio, imposta la proprietà su: `af.theme.forest`.

   ![Snapshot dell’archivio CRX](assets/3-2.png)

1. Aggiungi due cartelle, `less` e `css`e un file `css.txt` al nodo creato nel passaggio 1:

   * `less` cartella: contiene `less` file di variabili in cui definire `less` variabili e `less mixins` utilizzati per gestire gli stili .css.

      Questa cartella è costituita da `less` file di variabili, `less` file mixin, `less` file che definiscono gli stili utilizzando mixin e variabili. E tutti questi meno file vengono poi importati in styles.less.

   * `css`cartella: contiene i file .css in cui si definiscono gli stili statici da utilizzare nel tema.

   **Meno file variabili**: questi sono i file in cui puoi definire o sovrascrivere le variabili utilizzate per definire gli stili CSS.

   I moduli adattivi forniscono variabili OOTB definite nei seguenti file .less:

   * `/apps/clientlibs/fd/af/guidetheme/common/less/globalvariables.less`
   * `/apps/clientlibs/fd/af/guidetheme/common/less/layoutvariables.less`

   I moduli adattivi forniscono anche variabili di terze parti definite in:

   `/apps/clientlibs/fd/af/third-party/less/variables.less`

   È possibile utilizzare un numero inferiore di variabili fornite con i moduli adattivi, ignorare tali variabili oppure creare un numero inferiore di variabili.

   >[!NOTE]
   >
   >Durante l&#39;importazione dei file del pre-processore meno, nell&#39;istruzione di importazione specificare il percorso relativo dei file.

   Esempio di variabili di sostituzione:

   ```css
   @button-background-color: rgb(19, 102, 44);
   @button-border-color: rgb(19, 102, 44);
   @button-border-size: 0px;
   @button-padding: 10px 15px;
   @button-font-color: #ffffff;
   ```

   Per ignorare `less`Variabili:

   1. Importa variabili modulo adattive predefinite:

      `/apps/clientlibs/fd/af/guidetheme/common/less/globalvariables.less/apps/clientlibs/fd/af/guidetheme/common/less/layoutvariables.less`

   1. Quindi importa il file meno che include le variabili sovrascritte.

   Esempio di nuove definizioni di variabili:

   ```css
   @button-focus-bg-color: rgb(40, 208, 90);
   @button-hover-bg-color: rgb(30, 156, 67);
   ```

   **Meno file mixin:** È possibile definire le funzioni che accettano le variabili come argomenti. L’output di queste funzioni sono gli stili risultanti. Utilizza questi mixin in stili diversi, per evitare di ripetere gli stili CSS.

   I moduli adattivi forniscono mixin OOTB definiti in:

   * `/apps/clientlibs/fd/af/guidetheme/common/less/adaptiveforms-mixins.less`

   I moduli adattivi forniscono anche mixin di terze parti definiti in:

   * `/apps/clientlibs/fd/af/third-party/less/mixins.less`

   Definizione mixin di esempio:

   ```css
   .rounded-corners (@radius) {
     -webkit-border-radius: @radius;
     -moz-border-radius: @radius;
     -ms-border-radius: @radius;
     -o-border-radius: @radius;
     border-radius: @radius;
   }
   
   .border(@color, @type, @size) {
      border: @color @size @type;
   }
   ```

   **File Styles.less:** Utilizza questo file per includere tutti i file meno importanti (variabili, mixin, stili) che devi utilizzare nella libreria client.

   Nell’esempio seguente `styles.less` file, l’istruzione di importazione può essere inserita in qualsiasi ordine.

   Le istruzioni per importare i seguenti file .less sono obbligatorie:

   * `globalvariables.less`
   * `layoutvariables.less`
   * `components.less`
   * `layouts.less`

   ```css
   @import "../../../clientlibs/fd/af/guidetheme/common/less/globalvariables.less";
   @import "../../../clientlibs/fd/af/guidetheme/common/less/layoutvariables.less";
   @import "forestTheme-variables";
   @import "../../../clientlibs/fd/af/guidetheme/common/less/components.less";
   @import "../../../clientlibs/fd/af/guidetheme/common/less/layouts.less";
   
   /* custom styles */
   
   .guidetoolbar {
     input[type="button"], button, .button {
       .rounded-corners (@button-radius);
       &:hover {
         background-color: @button-hover-bg-color;
       }
       &:focus {
         background-color: @button-focus-bg-color;
       }
     }
   }
   
   form {
       background-image: url(../images/forest.png);
    background-repeat: no-repeat;
    background-size: 100%;
   }
   ```

   Il `css.txt` contiene i percorsi dei file .css da scaricare per la libreria.

   Ad esempio:

   ```javascript
   #base=/apps/clientlibs/fd/af/third-party/css
   bootstrap.css
   
   #base=less
   styles.less
   
   #base=/apps/clientlibs/fd/xfaforms/xfalib/css
   datepicker.css
   listboxwidget.css
   scribble.css
   dialog.css
   ```

   >[!NOTE]
   >
   >Il file styles.less non è obbligatorio. Ciò significa che non è necessario creare questo file, se non sono stati definiti stili, variabili o mixin personalizzati.
   >
   >Tuttavia, se non si crea un file style.less, nel file css.txt è necessario rimuovere il commento dalla riga seguente:
   >
   >**`#base=less`**
   >
   >E commenta la seguente riga:
   >
   >**`styles.less`**

## Per utilizzare un tema in un modulo adattivo {#to-use-a-theme-in-an-adaptive-form}

Dopo aver creato un tema per moduli adattivi, effettua le seguenti operazioni per utilizzarlo in un modulo adattivo:

1. Per includere il tema creato in [per creare un tema per moduli adattivi](/help/forms/using/creating-custom-adaptive-form-themes.md#p-to-create-an-adaptive-form-theme-p) , crea una pagina personalizzata di tipo `cq:Component`.

   Ad esempio `/apps/myAfCustomizations/myAfPages/forestPage`

   1. Aggiungi un `sling:resourceSuperType` e impostarne il valore come `fd/af/components/page/base`.

      ![Snapshot dell’archivio CRX](assets/1-2.png)

   1. Per utilizzare un tema nella pagina, devi aggiungere al nodo un file library.jsp che esegue l’override.

      Importa quindi il tema creato in Per creare una sezione del tema per moduli adattivi in questo articolo.

      Il frammento di codice di esempio seguente importa `af.theme.forest` tema.

      ```jsp
      <%@include file="/libs/fd/af/components/guidesglobal.jsp"%>
      <cq:includeClientLib categories="af.theme.forest"/>
      ```

   1. **Facoltativo**: nella pagina personalizzata, esegui l’override di header.jsp, footer.jsp e body.jsp, come richiesto.

1. Creare un modello personalizzato (ad esempio: `/apps/myAfCustomizations/myAfTemplates/forestTemplate`) il cui jcr:content punta alla pagina personalizzata creata nel passaggio precedente (ad esempio: `myAfCustomizations/myAfPages/forestPage)`.

   ![Snapshot dell’archivio CRX](assets/2-1.png)

1. Crea un modulo adattivo utilizzando il modello creato nel passaggio precedente. L’aspetto del modulo adattivo è definito dal tema creato nella sezione Per creare un tema per modulo adattivo di questo articolo.
