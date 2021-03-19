---
title: Personalizza editor di testo
seo-title: Personalizza editor di testo
description: Scopri come personalizzare l’editor di testo.
seo-description: Scopri come personalizzare l’editor di testo.
uuid: 598246fe-8f15-49b6-b6d3-9154bebcd27e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 666fee78-a103-44dc-afe7-71b90ce219b7
docset: aem65
feature: Gestione della corrispondenza
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 0%

---


# Personalizza editor di testo{#customize-text-editor}

## Panoramica {#overview}

Puoi personalizzare l’editor di testo, nell’interfaccia utente Gestione risorse e Crea corrispondenza, per aggiungere altri font e dimensioni di font. Questi font includono inglese e non inglese, ad esempio giapponese, font.

È possibile personalizzare per modificare quanto segue nelle impostazioni dei font:

* Famiglia e dimensioni dei font
* Proprietà quali l’altezza e la spaziatura tra le lettere
* Valori predefiniti per famiglia e dimensione del font, altezza, spaziatura tra le lettere e formato della data
* Punti elenco

A questo scopo, devi:

1. [Personalizza i font modificando il file tbxeditor-config.xml in CRX](#customizefonts)
1. [Aggiungi font personalizzati al computer client](#addcustomfonts)

## Personalizza i font modificando il file tbxeditor-config.xml in CRX {#customizefonts}

Per personalizzare i font modificando il file tbxeditor-config.xml, procedi come segue:

1. Vai a `https://'[server]:[port]'/[ContextPath]/crx/de` e accedi come amministratore.
1. Nella cartella delle app, crea una cartella denominata config con percorso/struttura simile alla cartella di configurazione, che si trova in libs/fd/cm/config, utilizzando i seguenti passaggi:

   1. Fai clic con il pulsante destro del mouse sulla cartella degli elementi nel percorso seguente e seleziona **Sovrapponi nodo**:

      `/libs/fd/cm/config`

      ![nodo di sovrapposizione](assets/1-1.png)

   1. Assicurati che la finestra di dialogo Sovrapponi nodo abbia i seguenti valori:

      **Percorso:** /libs/fd/cm/config

      **Posizione:** /apps/

      **Tipi di nodo di corrispondenza:** selezionati

      ![nodo di sovrapposizione](assets/2.png)

   1. Fai clic su **OK**. La struttura delle cartelle viene creata nella cartella delle app.

   1. Fare clic su **Salva tutto**.

1. Crea una copia del file tbxeditor-config.xml nella cartella di configurazione appena creata, seguendo la procedura seguente:

   1. Fai clic con il pulsante destro del mouse sul file tbxeditor-config.xml in libs/fd/cm/config e seleziona **Copia**.
   1. Fai clic con il pulsante destro del mouse sulla cartella seguente e seleziona **Incolla:**

      `apps/fd/cm/config`

   1. Per impostazione predefinita, il nome del file incollato è `copy of tbxeditor-config.xml.` Rinomina il file in `tbxeditor-config.xml` e fai clic su **Salva tutto**.

1. Apri il file tbxeditor-config.xml in apps/fd/cm/config e apporta le modifiche necessarie.

   1. Fai doppio clic sul file tbxeditor-config.xml in apps/fd/cm/config. Viene aperto il file .

      ```xml
      <editorConfig>
         <bulletIndent>0.25in</bulletIndent>
      
         <defaultDateFormat>DD-MM-YYYY</defaultDateFormat>
      
         <fonts>
            <default>Times New Roman</default>
            <font>_sans</font>
            <font>_serif</font>
            <font>_typewriter</font>
            <font>Arial</font>
            <font>Courier</font>
            <font>Courier New</font>
            <font>Geneva</font>
            <font>Georgia</font>
            <font>Helvetica</font>
            <font>Tahoma</font>
            <font>Times New Roman</font>
            <font>Times</font>
            <font>Verdana</font>
         </fonts>
      
         <fontSizes>
            <default>12</default>
            <fontSize>8</fontSize>
            <fontSize>9</fontSize>
            <fontSize>10</fontSize>
            <fontSize>11</fontSize>
            <fontSize>12</fontSize>
            <fontSize>14</fontSize>
            <fontSize>16</fontSize>
            <fontSize>18</fontSize>
            <fontSize>20</fontSize>
            <fontSize>22</fontSize>
            <fontSize>24</fontSize>
            <fontSize>26</fontSize>
            <fontSize>28</fontSize>
            <fontSize>36</fontSize>
            <fontSize>48</fontSize>
            <fontSize>72</fontSize>
         </fontSizes>
      
         <lineHeights>
            <default>2</default>     
            <lineHeight>2</lineHeight>
            <lineHeight>3</lineHeight>
            <lineHeight>4</lineHeight>
            <lineHeight>5</lineHeight>
            <lineHeight>6</lineHeight>
            <lineHeight>7</lineHeight>
            <lineHeight>8</lineHeight>
            <lineHeight>9</lineHeight>
            <lineHeight>10</lineHeight>
            <lineHeight>11</lineHeight>
            <lineHeight>12</lineHeight>
            <lineHeight>13</lineHeight>
            <lineHeight>14</lineHeight>
            <lineHeight>15</lineHeight>
            <lineHeight>16</lineHeight>
         </lineHeights>
      
         <letterSpacings>
            <default>0</default>
            <letterSpacing>0</letterSpacing>
            <letterSpacing>1</letterSpacing>
            <letterSpacing>2</letterSpacing>
            <letterSpacing>3</letterSpacing>
            <letterSpacing>4</letterSpacing>
            <letterSpacing>5</letterSpacing>
            <letterSpacing>6</letterSpacing>
            <letterSpacing>7</letterSpacing>
            <letterSpacing>8</letterSpacing>
            <letterSpacing>9</letterSpacing>
            <letterSpacing>10</letterSpacing>
            <letterSpacing>11</letterSpacing>
            <letterSpacing>12</letterSpacing>
            <letterSpacing>13</letterSpacing>
            <letterSpacing>14</letterSpacing>
            <letterSpacing>15</letterSpacing>
            <letterSpacing>16</letterSpacing>
         </letterSpacings>
      </editorConfig>
      ```

   1. Apporta le modifiche necessarie nel file per modificare quanto segue nelle impostazioni dei font:

      * Aggiungi o rimuovi la famiglia e la dimensione del font
      * Proprietà quali l’altezza e la spaziatura tra le lettere
      * Valori predefiniti per famiglia e dimensione del font, altezza, spaziatura tra le lettere e formato della data
      * Punti elenco

      Ad esempio, per aggiungere un font giapponese denominato Sazanami Mincho Medium, è necessario inserire la seguente voce nel file XML: `<font>Sazanami Mincho Medium</font>`. È inoltre necessario che questo font sia installato nel computer client utilizzato per accedere e lavorare con la personalizzazione del font. Per ulteriori informazioni, vedere [Aggiungere font personalizzati al computer client](#addcustomfonts).

      È inoltre possibile modificare le impostazioni predefinite per vari aspetti del testo e, rimuovendo le voci, rimuovere i font dall’editor di testo.

   1. Fare clic su **Salva tutto**.


## Aggiungi font personalizzati al computer client {#addcustomfonts}

Quando si accede a un font nell’editor di testo Gestione Corrispondenza, deve essere presente nel computer client che si sta utilizzando per accedere a Gestione Corrispondenza. Per poter utilizzare un font personalizzato nell’editor di testo, è innanzitutto necessario installarlo sul computer client.

Per ulteriori informazioni sull&#39;installazione dei font, consulta quanto segue:

* [Installa o disinstalla i font in Windows](https://windows.microsoft.com/en-us/windows-vista/install-or-uninstall-fonts)
* [Nozioni di base su Mac: Font Book](https://support.apple.com/en-us/HT201749)

## Accedi alle personalizzazioni dei font {#access-font-customizations}

Dopo aver apportato modifiche ai font nel file tbxeditor-config.xml in CRX e installato i font richiesti sul computer client utilizzato per accedere ad AEM Forms, le modifiche vengono visualizzate nell&#39;editor di testo.

Ad esempio, il font Sazanami Mincho Medium aggiunto in [Personalizza font modificando il file tbxeditor-config.xml nella procedura CRX](#customizefonts) viene visualizzato nell&#39;interfaccia utente dell&#39;editor di testo come segue:

![sazanamiminchointext](assets/sazanamiminchointext.png)

>[!NOTE]
>
>Per visualizzare il testo in giapponese, è innanzitutto necessario immettere il testo con caratteri giapponesi. L&#39;applicazione di un font giapponese personalizzato formatta solo il testo in un certo modo. L&#39;applicazione di un font giapponese personalizzato non cambia l&#39;inglese o altri caratteri in caratteri giapponesi.

