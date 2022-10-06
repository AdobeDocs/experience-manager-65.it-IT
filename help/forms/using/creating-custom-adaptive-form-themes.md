---
title: Creazione di temi modulo adattivo personalizzati
seo-title: Creating custom adaptive form themes
description: Un tema modulo adattivo è una libreria client AEM che consente di definire gli stili (aspetto e aspetto) di un modulo adattivo. Scopri come creare temi di modulo adattivo personalizzati.
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

# Creazione di temi modulo adattivo personalizzati {#creating-custom-adaptive-form-themes}

>[!CAUTION]
>
>AEM Forms fornisce [Editor tema](/help/forms/using/themes.md) capacità di creare e modificare moduli adattivi [temi](/help/forms/using/themes.md). Esegui i passaggi elencati in questo articolo, solo se hai effettuato l’aggiornamento da una versione che non ha [Editor tema](/help/forms/using/themes.md) e disponi di un investimento esistente nei temi creati utilizzando i file Less/CSS (metodo dell&#39;editor pre-theme).

## Prerequisiti {#prerequisites}

* Conoscenza del framework LESS (Leaner CSS)
* Come creare una libreria client in Adobe Experience Manager
* [Creazione di un modello di modulo adattivo](/help/forms/using/custom-adaptive-forms-templates.md) per utilizzare il tema creato

## Tema modulo adattivo {#adaptive-form-theme}

Un **tema modulo adattivo** è una libreria client AEM utilizzata per definire gli stili (aspetto e aspetto) di un modulo adattivo.

Crea un **modello adattivo** e applica il tema al modello. Quindi utilizza questo modello personalizzato per creare un **modulo adattivo**.

![Moduli adattivi e libreria client](assets/hierarchy.png)

## Per creare un tema modulo adattivo {#to-create-an-adaptive-form-theme}

>[!NOTE]
>
>La procedura seguente viene descritta utilizzando nomi di esempio per oggetti AEM quali nodo, proprietà e cartelle.
>
>Se si seguono questi passaggi utilizzando i nomi, il modello risultante dovrebbe essere simile al seguente snapshot:

![Snapshot dei moduli adattivi a tema foresta](assets/thumbnail.png)
**Figura:** *Esempio di tema della foresta*

1. Crea un nodo di tipo `cq:ClientLibraryFolder` in `/apps`nodo.

   Ad esempio, crea il seguente nodo:

   `/apps/myAfThemes/forestTheme`

1. Aggiungi una proprietà stringa con più valori `categories` sul nodo e impostarne il valore in modo appropriato.

   Ad esempio, impostare la proprietà su: `af.theme.forest`.

   ![Snapshot archivio CRX](assets/3-2.png)

1. Aggiungi due cartelle, `less` e `css`e un file `css.txt` al nodo creato nel passaggio 1:

   * `less` cartella: Contiene la `less` file variabili in cui si definiscono i `less` variabili e `less mixins` utilizzati per gestire gli stili .css.

      Questa cartella è costituita da `less` file variabili, `less` file misti, `less` file che definiscono gli stili utilizzando mixin e variabili. E tutti questi file in meno vengono importati in style.less.

   * `css`cartella: Contiene i file .css in cui si definiscono gli stili statici da utilizzare nel tema.

   **Meno file variabili**: Si tratta dei file , in cui definisci o sovrascrivi le variabili utilizzate nella definizione degli stili CSS.

   I moduli adattivi forniscono variabili OOTB definite nei seguenti file .less:

   * `/apps/clientlibs/fd/af/guidetheme/common/less/globalvariables.less`
   * `/apps/clientlibs/fd/af/guidetheme/common/less/layoutvariables.less`

   I moduli adattivi forniscono anche variabili di terze parti definite in:

   `/apps/clientlibs/fd/af/third-party/less/variables.less`

   È possibile utilizzare le variabili minori fornite con i moduli adattivi, sovrascrivere queste variabili o creare nuove variabili minori.

   >[!NOTE]
   >
   >Durante l’importazione dei file dei meno preprocessori, nell’istruzione di importazione specificare il percorso relativo dei file.

   Esempio di variabili di override:

   ```css
   @button-background-color: rgb(19, 102, 44);
   @button-border-color: rgb(19, 102, 44);
   @button-border-size: 0px;
   @button-padding: 10px 15px;
   @button-font-color: #ffffff;
   ```

   Per ignorare il `less`variabili:

   1. Importa variabili di modulo adattivo predefinite:

      `/apps/clientlibs/fd/af/guidetheme/common/less/globalvariables.less/apps/clientlibs/fd/af/guidetheme/common/less/layoutvariables.less`

   1. Quindi importa il file less che include le variabili sostituite.

   Esempio di nuove definizioni di variabili:

   ```css
   @button-focus-bg-color: rgb(40, 208, 90);
   @button-hover-bg-color: rgb(30, 156, 67);
   ```

   **Meno file mixin:** Puoi definire le funzioni che accettano le variabili come argomenti. L&#39;output di queste funzioni sono gli stili risultanti. Utilizza questi mixin all’interno di stili diversi, per evitare di ripetere stili CSS.

   I moduli adattivi forniscono mixer OOTB definiti in:

   * `/apps/clientlibs/fd/af/guidetheme/common/less/adaptiveforms-mixins.less`

   I moduli adattivi forniscono anche mixin di terze parti definiti in:

   * `/apps/clientlibs/fd/af/third-party/less/mixins.less`

   Definizione del mixin campione:

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

   **File Styles.less:** Usa questo file per includere tutti i file minori (variabili, mixin, stili) che devi utilizzare nella libreria client.

   Nel seguente esempio: `styles.less` file, l&#39;istruzione import può essere inserita in qualsiasi ordine.

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

   La `css.txt` contiene i percorsi dei file .css da scaricare per la libreria.

   Esempio:

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
   >Il file Styles.less non è obbligatorio. Questo significa che non devi creare questo file, se non hai definito stili, variabili o mixin personalizzati.
   >
   >Tuttavia, se non si crea un file style.less, nel file css.txt, è necessario rimuovere il commento dalla seguente riga:
   >
   >**`#base=less`**
   >
   >E commenta la seguente riga:
   >
   >**`styles.less`**

## Per utilizzare un tema in un modulo adattivo {#to-use-a-theme-in-an-adaptive-form}

Dopo aver creato un tema del modulo adattivo, esegui i seguenti passaggi per utilizzare questo tema in un modulo adattivo:

1. Per includere il tema creato in [per creare un tema modulo adattivo](/help/forms/using/creating-custom-adaptive-form-themes.md#p-to-create-an-adaptive-form-theme-p) sezione, creare una pagina personalizzata di tipo `cq:Component`.

   Esempio, `/apps/myAfCustomizations/myAfPages/forestPage`

   1. Aggiungi un `sling:resourceSuperType` e impostarne il valore come `fd/af/components/page/base`.

      ![Snapshot archivio CRX](assets/1-2.png)

   1. Per utilizzare un tema nella pagina, è necessario aggiungere un file di override library.jsp al nodo.

      Quindi importi il tema creato in Per creare una sezione del tema del modulo adattivo di questo articolo.

      Il frammento di codice di esempio seguente importa il `af.theme.forest` tema.

      ```jsp
      <%@include file="/libs/fd/af/components/guidesglobal.jsp"%>
      <cq:includeClientLib categories="af.theme.forest"/>
      ```

   1. **Facoltativo**: Nella pagina personalizzata, sovrascrivi header.jsp, footer.jsp e body.jsp, come necessario.

1. Crea un modello personalizzato (ad esempio: `/apps/myAfCustomizations/myAfTemplates/forestTemplate`) il cui jcr:content punta alla pagina personalizzata creata nel passaggio precedente (ad esempio: `myAfCustomizations/myAfPages/forestPage)`.

   ![Snapshot archivio CRX](assets/2-1.png)

1. Crea un modulo adattivo utilizzando il modello creato nel passaggio precedente. L’aspetto del modulo adattivo è definito dal tema creato in Per creare un modulo adattivo sezione del tema di questo articolo.
