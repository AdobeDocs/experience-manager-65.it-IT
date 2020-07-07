---
title: Elabora le risorse utilizzando gestori di contenuti multimediali e flussi di lavoro in [!DNL Adobe Experience Manager].
description: Scopri i gestori di contenuti multimediali e come utilizzare i flussi di lavoro per eseguire attività sulle risorse digitali.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 39bbb1d663bb54ef425dfeb5e0fc10ea37eb5708
workflow-type: tm+mt
source-wordcount: '2109'
ht-degree: 4%

---


# Elaborazione delle risorse tramite gestori e flussi di lavoro di contenuti multimediali {#processing-assets-using-media-handlers-and-workflows}

[!DNL Adobe Experience Manager Assets] viene fornito con un set di flussi di lavoro e gestori di contenuti multimediali predefiniti per l’elaborazione delle risorse. Un flusso di lavoro definisce le attività da eseguire sulle risorse, quindi delega le attività specifiche ai gestori dei contenuti multimediali, ad esempio generazione di miniature o estrazione di metadati.

Un flusso di lavoro può essere configurato per essere eseguito automaticamente quando viene caricata una risorsa di un particolare tipo MIME. Le fasi di elaborazione sono definite in termini di una serie di gestori di [!DNL Assets] supporti. [!DNL Experience Manager] fornisce alcuni gestori [integrati,](#default-media-handlers) e altri possono essere sviluppati [](#creating-a-new-media-handler) personalizzati o definiti delegando il processo a uno strumento [della riga di](#command-line-based-media-handler)comando.

I gestori di file multimediali sono servizi [!DNL Assets] che eseguono azioni specifiche sulle risorse. Ad esempio, quando un file audio MP3 viene caricato in [!DNL Experience Manager], un flusso di lavoro attiva un gestore MP3 che estrae i metadati e genera una miniatura. I gestori di file multimediali vengono generalmente utilizzati in combinazione con i flussi di lavoro. La maggior parte dei tipi MIME comuni sono supportati all&#39;interno [!DNL Experience Manager]. Per eseguire specifiche attività sulle risorse è possibile estendere/creare flussi di lavoro, estendere/creare gestori di contenuti multimediali o disattivare/abilitare i gestori di contenuti multimediali.

>[!NOTE]
>
>Consulta la pagina Formati [supportati da](assets-formats.md) Risorse per una descrizione di tutti i formati supportati [!DNL Assets] e delle funzioni supportate per ciascun formato.

## Gestori multimediali predefiniti {#default-media-handlers}

I seguenti gestori di supporti sono disponibili all&#39;interno [!DNL Assets] e gestiscono i tipi MIME più comuni:

<!-- TBD: Java versions shouldn't be set to 1.5. Must be updated.
-->

| Nome gestore | Nome servizio (nella console del sistema) | Tipi MIME supportati |
|--------------|--------------------------------------|----------------------|
| [!UICONTROL TextHandler] | `com.day.cq.dam.core.impl.handler.TextHandler` | text/plain |
| [!UICONTROL PdfHandler] | `com.day.cq.dam.handler.standard.pdf.PdfHandler` | <ul><li>application/pdf</li><li>application/illustrator</li></ul> |
| [!UICONTROL JpegHandler] | `com.day.cq.dam.core.impl.handler.JpegHandler` | image/jpeg |
| [!UICONTROL Mp3Handler] | `com.day.cq.dam.handler.standard.mp3.Mp3Handler` | audio/mpeg |
| [!UICONTROL ZipHandler] | `com.day.cq.dam.handler.standard.zip.ZipHandler` | <ul><li>application/java-archive </li><li> application/zip</li></ul> |
| [!UICONTROL PictHandler] | `com.day.cq.dam.handler.standard.pict.PictHandler` | image/pict |
| [!UICONTROL StandardImageHandler] | `com.day.cq.dam.core.impl.handler.StandardImageHandler` | <ul><li>image/gif </li><li> image/png </li> <li>application/photoshop </li> <li>image/jpeg </li><li> image/tiff </li> <li>image/x-ms-bmp </li><li> image/bmp</li></ul> |
| [!UICONTROL MSOfficeHandler] | `com.day.cq.dam.handler.standard.msoffice.MSOfficeHandler` | application/msword |
| [!UICONTROL MSPwerPointHandler] | `com.day.cq.dam.handler.standard.msoffice.MSPowerPointHandler` | application/vnd.ms-powerpoint |
| [!UICONTROL OpenOfficeHandler] | `com.day.cq.dam.handler.standard.ooxml.OpenOfficeHandler` | <ul><li>application/vnd.openxmlformats-officedocument.wordprocessingml.document</li><li> application/vnd.openxmlformats-officedocument.spreadsheetml.sheet</li><li> application/vnd.openxmlformats-officedocument.presentationml.presentation</li></ul> |
| [!UICONTROL EPubHandler] | `com.day.cq.dam.handler.standard.epub.EPubHandler` | application/epub+zip |
| [!UICONTROL GenericAssetHandler] | `com.day.cq.dam.core.impl.handler.GenericAssetHandler` | fallback nel caso in cui non sia stato trovato nessun altro gestore per estrarre dati da una risorsa |

Tutti i gestori eseguono le seguenti operazioni:

* estrazione di tutti i metadati disponibili dalla risorsa.
* creazione di una miniatura di una risorsa.

Per visualizzare i gestori di contenuti multimediali attivi:

1. In your browser, navigate to `http://localhost:4502/system/console/components`.
1. Clic `com.day.cq.dam.core.impl.store.AssetStoreImpl`.
1. Viene visualizzato un elenco con tutti i gestori di contenuti multimediali attivi. Ad esempio:

![chlimage_1-437](assets/chlimage_1-437.png)

## Utilizzo di gestori di contenuti multimediali nei flussi di lavoro per eseguire attività sulle risorse {#using-media-handlers-in-workflows-to-perform-tasks-on-assets}

I gestori di file multimediali sono servizi solitamente utilizzati in combinazione con i flussi di lavoro.

[!DNL Experience Manager] dispone di alcuni flussi di lavoro predefiniti per l’elaborazione delle risorse. Per visualizzarli, aprite la console Flusso di lavoro e fate clic sulla scheda **[!UICONTROL Modelli]** : i titoli del flusso di lavoro che iniziano con [!DNL Assets] sono le risorse specifiche.

I flussi di lavoro esistenti possono essere estesi e possono essere creati nuovi per elaborare le risorse in base a requisiti specifici.

L’esempio seguente mostra come migliorare il flusso di lavoro di **[!UICONTROL Sincronizzazione AEM Assets]** in modo che vengano generate le risorse secondarie di tutte le risorse, eccetto i documenti PDF.

### Disattivazione o attivazione di un gestore di supporti {#disabling-enabling-a-media-handler}

I gestori di contenuti multimediali possono essere disabilitati o abilitati tramite la console di gestione Web Apache Felix. Quando il gestore multimediale è disattivato, le attività non vengono eseguite sulle risorse.

Per attivare/disattivare un gestore di supporti:

1. In your browser, navigate to `https://<host>:<port>/system/console/components`.
1. Fate clic su **[!UICONTROL Disattiva]** accanto al nome del gestore multimediale. Esempio: `com.day.cq.dam.handler.standard.mp3.Mp3Handler`.
1. Aggiorna la pagina: accanto al gestore multimediale viene visualizzata un&#39;icona che indica che è disattivato.
1. Per abilitare il gestore di file multimediali, fate clic su **[!UICONTROL Abilita]** accanto al nome del gestore.

### Creare un nuovo gestore di file multimediali {#creating-a-new-media-handler}

Per supportare un nuovo tipo di supporto o eseguire attività specifiche su una risorsa, è necessario creare un nuovo gestore di supporti. Questa sezione descrive come procedere.

#### Classi e interfacce importanti {#important-classes-and-interfaces}

Il modo migliore per avviare un&#39;implementazione consiste nell&#39;ereditare da un&#39;implementazione astratta fornita che si occupa della maggior parte delle cose e fornisce un comportamento predefinito ragionevole: la `com.day.cq.dam.core.AbstractAssetHandler` classe.

Questa classe fornisce già un descrittore di servizio astratto. Quindi se ereditate da questa classe e utilizzate il plug-in maven-sling, accertatevi di impostare il flag inherit su `true`.

Implementate i seguenti metodi:

* `extractMetadata()`: estrae tutti i metadati disponibili.
* `getThumbnailImage()`: crea una miniatura della risorsa passata.
* `getMimeTypes()`: restituisce i tipi MIME della risorsa.

Di seguito è riportato un modello di esempio:

```Java
package my.own.stuff; /** * @scr.component inherit="true" * @scr.service */ public class MyMediaHandler extends com.day.cq.dam.core.AbstractAssetHandler { // implement the relevant parts }
```

L&#39;interfaccia e le classi includono:

* `com.day.cq.dam.api.handler.AssetHandler` interfaccia: Questa interfaccia descrive il servizio che aggiunge il supporto per tipi MIME specifici. L&#39;aggiunta di un nuovo tipo MIME richiede l&#39;implementazione di questa interfaccia. L&#39;interfaccia contiene metodi per importare ed esportare i documenti specifici, per creare miniature ed estrarre metadati.
* `com.day.cq.dam.core.AbstractAssetHandler` class: Questa classe funge da base per tutte le altre implementazioni dei gestori di risorse e fornisce funzionalità comuni utilizzate.
* Classe `com.day.cq.dam.core.AbstractSubAssetHandler`:
   * Questa classe funge da base per tutte le altre implementazioni dei gestori di risorse e fornisce funzionalità comuni più comuni per l’estrazione di risorse secondarie.
   * Il modo migliore per avviare un&#39;implementazione consiste nell&#39;ereditare da un&#39;implementazione astratta fornita che si occupa della maggior parte delle cose e fornisce un comportamento predefinito ragionevole: la classe com.day.cq.dam.core.AbstractAssetHandler.
   * Questa classe fornisce già un descrittore di servizio astratto. Quindi se ereditate da questa classe e utilizzate il plug-in maven-sling, accertatevi di impostare il flag inherit su true.

È necessario implementare i seguenti metodi:

* `extractMetadata()`: questo metodo estrae tutti i metadati disponibili.
* `getThumbnailImage()`: questo metodo crea una miniatura della risorsa passata.
* `getMimeTypes()`: questo metodo restituisce i tipi MIME della risorsa.

Di seguito è riportato un modello di esempio:

package my.own.things; /&amp;ast;&amp;ast; &amp;ast; @scr.component inherit=&quot;true&quot; &amp;ast; @scr.service &amp;ast;/ classe pubblica MyMediaHandler estende com.day.cq.dam.core.AbstractAssetHandler { // implementa le parti pertinenti }

L&#39;interfaccia e le classi includono:

* `com.day.cq.dam.api.handler.AssetHandler` interfaccia: Questa interfaccia descrive il servizio che aggiunge il supporto per tipi MIME specifici. L&#39;aggiunta di un nuovo tipo MIME richiede l&#39;implementazione di questa interfaccia. L&#39;interfaccia contiene metodi per importare ed esportare i documenti specifici, per creare miniature ed estrarre metadati.
* `com.day.cq.dam.core.AbstractAssetHandler` class: Questa classe funge da base per tutte le altre implementazioni dei gestori di risorse e fornisce funzionalità comuni utilizzate.
* `com.day.cq.dam.core.AbstractSubAssetHandler` class: Questa classe funge da base per tutte le altre implementazioni dei gestori di risorse e fornisce funzionalità comuni più comuni per l’estrazione di risorse secondarie.

#### Esempio: creazione di un gestore di testo specifico {#example-create-a-specific-text-handler}

In questa sezione verrà creato un gestore di testo specifico che genera le miniature con una filigrana.

Procedere come segue:

Fare riferimento a Strumenti [di](../sites-developing/dev-tools.md) sviluppo per installare e configurare Eclipse con un [!DNL Maven] plug-in e per impostare le dipendenze necessarie per il [!DNL Maven] progetto.

Dopo aver eseguito la procedura seguente, quando caricate un file TXT in [!DNL Experience Manager], i metadati del file vengono estratti e vengono generate due miniature con una filigrana.

1. In Eclipse, crea `myBundle`[!DNL Maven] progetto:

   1. Nella barra dei menu, fate clic su **[!UICONTROL File]** > **[!UICONTROL Nuovo]** > **[!UICONTROL Altro]**.
   1. Nella finestra di dialogo, espandete la [!DNL Maven] cartella, selezionate [!DNL Maven] il progetto e fate clic su **[!UICONTROL Avanti]**.
   1. Selezionare la casella Crea un progetto semplice e la casella Usa posizioni Workspace predefinite, quindi fare clic su **[!UICONTROL Avanti]**.
   1. Definire un [!DNL Maven] progetto:

      * ID gruppo: `com.day.cq5.myhandler`.
      * Id Artifact: myBundle.
      * Nome: Il mio [!DNL Experience Manager] fascio.
      * Descrizione: Questo è il mio [!DNL Experience Manager] pacchetto.
   1. Click **[!UICONTROL Finish]**.


1. Impostate il [!DNL Java] compilatore sulla versione 1.5:

   1. Fare clic con il pulsante destro del mouse sul `myBundle` progetto e selezionare [!UICONTROL Proprietà].
   1. Selezionare [!UICONTROL Java Compiler] e impostare le seguenti proprietà su 1.5:

      * Livello di conformità del compilatore
      * Compatibilità con i file .class generati
      * Compatibilità delle origini
   1. Fai clic su **[!UICONTROL OK]**. Nella finestra di dialogo, fare clic su **[!UICONTROL Sì]**.


1. Sostituite il codice nel `pom.xml` file con il seguente codice:

   ```xml
   <project xmlns="https://maven.apache.org/POM/4.0.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <!-- ====================================================================== -->
    <!-- P A R E N T P R O J E C T D E S C R I P T I O N -->
    <!-- ====================================================================== -->
    <parent>
     <groupId>com.day.cq.dam</groupId>
     <artifactId>dam</artifactId>
     <version>5.2.14</version>
     <relativePath>../parent</relativePath>
    </parent>
    <!-- ====================================================================== -->
    <!-- P R O J E C T D E S C R I P T I O N -->
    <!-- ====================================================================== -->
    <groupId>com.day.cq5.myhandler</groupId>
    <artifactId>myBundle</artifactId>
    <name>My CQ5 bundle</name>
    <version>0.0.1-SNAPSHOT</version>
    <description>This is my CQ5 bundle</description>
    <packaging>bundle</packaging>
    <!-- ====================================================================== -->
    <!-- B U I L D D E F I N I T I O N -->
    <!-- ====================================================================== -->
    <build>
     <plugins>
      <plugin>
       <groupId>org.apache.felix</groupId>
       <artifactId>maven-scr-plugin</artifactId>
      </plugin>
      <plugin>
       <groupId>org.apache.sling</groupId>
       <artifactId>maven-sling-plugin</artifactId>
       <configuration>
        <slingUrlSuffix>/libs/dam/install/</slingUrlSuffix>
       </configuration>
      </plugin>
      <plugin>
       <groupId>org.apache.felix</groupId>
       <artifactId>maven-bundle-plugin</artifactId>
       <extensions>true</extensions>
       <configuration>
        <instructions>
         <Bundle-Category>cq5</Bundle-Category>
         <Export-Package> com.day.cq5.myhandler </Export-Package>
        </instructions>
       </configuration>
      </plugin>
     </plugins>
    </build>
    <!-- ====================================================================== -->
    <!-- D E P E N D E N C I E S -->
    <!-- ====================================================================== -->
    <dependencies>
     <dependency>
      <groupId>com.day.cq.dam</groupId>
      <artifactId>cq-dam-api</artifactId>
      <version>5.2.10</version>
      <scope>provided</scope>
     </dependency>
     <dependency>
      <groupId>com.day.cq.dam</groupId>
      <artifactId>cq-dam-core</artifactId>
      <version>5.2.10</version>
      <scope>provided</scope>
     </dependency>
     <dependency>
      <groupId>com.day.cq</groupId>
      <artifactId>cq-commons</artifactId>
     </dependency>
     <dependency>
      <groupId>javax.jcr</groupId>
      <artifactId>jcr</artifactId>
     </dependency>
     <dependency>
      <groupId>org.apache.felix</groupId>
      <artifactId>org.osgi.compendium</artifactId>
     </dependency>
     <dependency>
      <groupId>org.slf4j</groupId>
      <artifactId>slf4j-api</artifactId>
     </dependency>
     <dependency>
      <groupId>commons-lang</groupId>
      <artifactId>commons-lang</artifactId>
     </dependency>
     <dependency>
      <groupId>commons-collections</groupId>
      <artifactId>commons-collections</artifactId>
     </dependency>
     <dependency>
      <groupId>commons-io</groupId>
      <artifactId>commons-io</artifactId>
     </dependency>
     <dependency>
      <groupId>com.day.commons</groupId>
      <artifactId>day-commons-gfx</artifactId>
     </dependency>
     <dependency>
      <groupId>com.day.commons</groupId>
      <artifactId>day-commons-text</artifactId>
     </dependency>
     <dependency>
      <groupId>com.day.cq.workflow</groupId>
      <artifactId>cq-workflow-api</artifactId>
     </dependency>
     <dependency>
      <groupId>com.day.cq.wcm</groupId>
      <artifactId>cq-wcm-foundation</artifactId>
      <version>5.2.22</version>
     </dependency>
    </dependencies>
   ```

1. Create il pacchetto `com.day.cq5.myhandler` che contiene le [!DNL Java] classi in `myBundle/src/main/java`:

   1. In myBundle, fai clic con il pulsante destro del mouse `src/main/java`, seleziona Nuovo, quindi Pacchetto.
   1. Assegnare un nome `com.day.cq5.myhandler` e fare clic su Fine.

1. Create la [!DNL Java] classe `MyHandler`:

   1. In [!DNL Eclipse], in `myBundle/src/main/java`, fate clic con il pulsante destro del mouse sul `com.day.cq5.myhandler` pacchetto. Selezionare [!UICONTROL Nuovo], quindi [!UICONTROL Classe].
   1. Nella finestra di dialogo, denominate la [!DNL Java] classe `MyHandler` e fate clic su [!UICONTROL Fine]. [!DNL Eclipse] crea e apre il file `MyHandler.java`.
   1. In `MyHandler.java` sostituzione del codice esistente con quanto segue, quindi salvare le modifiche:

   ```java
   package com.day.cq5.myhandler;
   import java.awt.Color;
   import java.awt.Rectangle;
   import java.awt.image.BufferedImage;
   import java.io.IOException;
   import java.io.InputStream;
   import java.io.InputStreamReader;
   import javax.jcr.Node;
   import javax.jcr.RepositoryException;
   import javax.jcr.Session;
   import org.apache.commons.io.IOUtils;
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   import com.day.cq.dam.api.metadata.ExtractedMetadata;
   import com.day.cq.dam.core.AbstractAssetHandler;
   import com.day.image.Font;
   import com.day.image.Layer;
   import com.day.cq.wcm.foundation.ImageHelper;
   
   /**
    * The <code>MyHandler</code> can extract text files
    * @scr.component inherit="true" immediate="true" metatype="false"
    * @scr.service
    *
    **/
   
   public class MyHandler extends AbstractAssetHandler {
    /** * Logger instance for this class. */
    private static final Logger log = LoggerFactory.getLogger(MyHandler.class);
    /** * Music icon margin */
    private static final int MARGIN = 10;
    /** * @see com.day.cq.dam.api.handler.AssetHandler#getMimeTypes() */
    public String[] getMimeTypes() {
     return new String[] {"text/plain"};
    }
   
    public ExtractedMetadata extractMetadata(Node asset) {
     ExtractedMetadata extractedMetadata = new ExtractedMetadata();
     InputStream data = getInputStream(asset);
     try {
      // read text data
      InputStreamReader reader = new InputStreamReader(data);
      char[] buffer = new char[4096];
      String text = "";
      while (reader.read(buffer) != -1) {
       text += new String(buffer);
      }
      reader.close();
      long wordCount = this.wordCount(text);
      extractedMetadata.setProperty("text", text);
      extractedMetadata.setMetaDataProperty("Word Count",wordCount);
      setMimetype(extractedMetadata, asset);
     } catch (Throwable t) {
      log.error("handling error: " + t.toString(), t);
     } finally {
      IOUtils.closeQuietly(data);
     }
     return extractedMetadata; }
    // ----------------------< helpers >----------------------------------------
    protected BufferedImage getThumbnailImage(Node node) {
     ExtractedMetadata metadata = extractMetadata(node);
     final String text = (String) metadata.getProperty("text");
     // create text layer
     final Layer layer = new Layer(500, 600, Color.WHITE);
     layer.setPaint(Color.black);
     Font font = new Font("Arial", 12);
     String displayText = this.getDisplayText(text, 600, 12);
     if(displayText!=null && displayText.length() > 0) {
      // commons-gfx Font class would throw IllegalArgumentException on empty or null text
      layer.drawText(10, 10, 500, 600, displayText, font, Font.ALIGN_LEFT, 0, 0);
     }
     // create watermark and merge with text layer
     Layer watermarkLayer;
     try {
      final Session session = node.getSession();
      watermarkLayer = ImageHelper.createLayer(session, "/content/dam/geometrixx/icons/certificate.png");
      watermarkLayer.setX(MARGIN);
      watermarkLayer.setY(MARGIN);
      layer.merge(watermarkLayer);
     } catch (RepositoryException e) {
      // TODO Auto-generated catch block
      e.printStackTrace();
     } catch (IOException e) {
      // TODO Auto-generated catch block
      e.printStackTrace(); }
     layer.crop(new Rectangle(510, 600));
     return layer.getImage(); }
    // ---------------< private >-----------------------------------------------
    /**
     * This method cuts lines if the text file is too long..
     * * @param text
     * * text to check
     * * @param height
     * * text box height (px)
     * * @param fontheight
     * * font height (px)
     * * @return the text which will fit into the box
     */
    private String getDisplayText(String text, int height, int fontheight) {
     String trimmedText = text.trim();
     int numOfLines = height / fontheight;
     String lines[] = trimmedText.split("\n");
     if (lines.length <= numOfLines) {
      return trimmedText;
     } else {
      String cuttetText = "";
      for (int i = 0; i < numOfLines; i++) {
       cuttetText += lines[i] + "\n";
      }
      return cuttetText;
     }
    }
    /**
     * * This method counts the number of words in a string
     * * @param text the String whose words would like to be counted
     * * @return the number of words in the string
     * */
    private long wordCount(String text) {
     // We need to keep track of the last character, if we have two whitespaces in a row we don't want to double count.
     // The starting of the document is always a whitespace.
     boolean prevWhiteSpace = true;
     boolean currentWhiteSpace = true;
     char c; long numwords = 0;
     int j = text.length();
     int i = 0;
     while (i < j) {
      c = text.charAt(i++);
      if (c == 0) { break; }
      currentWhiteSpace = Character.isWhitespace(c);
      if (currentWhiteSpace && !prevWhiteSpace) { numwords++; }
      prevWhiteSpace = currentWhiteSpace;
     }
     // If we do not end with a whitespace then we need to add one extra word.
     if (!currentWhiteSpace) { numwords++; }
     return numwords;
    }
   }
   ```

1. Compilate la [!DNL Java] classe e create il bundle:

   1. Fate clic con il pulsante destro del mouse sul `myBundle` progetto, selezionate **[!UICONTROL Esegui come]**, quindi Installazione **** Paradiso.
   1. Il bundle `myBundle-0.0.1-SNAPSHOT.jar` (contenente la classe compilata) viene creato in `myBundle/target`.

1. In CRX Explorer, create un nuovo nodo sotto `/apps/myApp`. Nome = `install`, Tipo = `nt:folder`.
1. Copiate il bundle `myBundle-0.0.1-SNAPSHOT.jar` e archiviatelo in `/apps/myApp/install` (ad esempio con WebDAV). Il nuovo gestore di testo ora è attivo in [!DNL Experience Manager].
1. Nel browser, aprite la console [!UICONTROL di gestione Web]Apache Felix. Selezionare la scheda [!UICONTROL Componenti] e disabilitare il gestore di testo predefinito `com.day.cq.dam.core.impl.handler.TextHandler`.

## Gestore dei supporti basati su riga di comando {#command-line-based-media-handler}

[!DNL Experience Manager] consente di eseguire qualsiasi strumento della riga di comando all’interno di un flusso di lavoro per convertire le risorse (ad esempio [!DNL ImageMagick]) e aggiungere la nuova rappresentazione alla risorsa. È sufficiente installare lo strumento della riga di comando sul disco che ospita il [!DNL Experience Manager] server e aggiungere e configurare un passaggio del processo al flusso di lavoro. Il processo invocato, denominato `CommandLineProcess`, consente inoltre di filtrare in base a tipi MIME specifici e di creare più miniature in base alla nuova rappresentazione.

Le seguenti conversioni possono essere eseguite automaticamente e memorizzate all&#39;interno di [!DNL Assets]:

* Trasformazione EPS e AI tramite [ImageMagick](https://www.imagemagick.org/script/index.php) e [Ghostscript](https://www.ghostscript.com/).
* Transcodifica video FLV tramite [FFmpeg](https://ffmpeg.org/).
* Codifica MP3 con [LAME](http://lame.sourceforge.net/).
* Elaborazione audio con [SOX](http://sox.sourceforge.net/).

>[!NOTE]
>
>Sui sistemi non Windows, lo strumento FFmpeg restituisce un errore durante la generazione di rappresentazioni per una risorsa video con un&#39;unica citazione (&#39;) nel nome del file. Se il nome del file video include un’unica citazione, rimuoverla prima di eseguire il caricamento in [!DNL Experience Manager].

Il `CommandLineProcess` processo esegue le seguenti operazioni nell&#39;ordine in cui sono elencate:

* Filtra il file in base a tipi MIME specifici, se specificato.
* Crea una directory temporanea sul disco che ospita il [!DNL Experience Manager] server.
* Invia il file originale alla directory temporanea.
* Esegue il comando definito dagli argomenti del passaggio. Il comando viene eseguito all&#39;interno della directory temporanea con le autorizzazioni dell&#39;utente in esecuzione [!DNL Experience Manager].
* Invia di nuovo il risultato nella cartella di rappresentazione del [!DNL Experience Manager] server.
* Elimina la directory temporanea.
* Crea le miniature in base a tali rappresentazioni, se specificate. Il numero e le dimensioni delle miniature sono definiti dagli argomenti del passaggio.

### Un esempio che utilizza [!DNL ImageMagick] {#an-example-using-imagemagick}

L’esempio seguente mostra come impostare il passaggio del processo della riga di comando in modo che ogni volta che una risorsa con GIF o TIFF di tipo e-MIME viene aggiunta `/content/dam` sul [!DNL Experience Manager] server, venga creata un’immagine capovolta dell’originale insieme a tre miniature aggiuntive (140x100, 48x48 e 10x250).

Per fare questo, utilizzate [!DNL ImageMagick]. [!DNL ImageMagick] è un software gratuito della riga di comando utilizzato per creare, modificare e comporre immagini bitmap.

Installate [!DNL ImageMagick] sul disco che ospita il [!DNL Experience Manager] server:

1. Installa [!DNL ImageMagick]: Consulta la documentazione [di](https://www.imagemagick.org/script/download.php)ImageMagick.
1. Impostare lo strumento in modo da poter eseguire la conversione sulla riga di comando.
1. Per verificare se lo strumento è installato correttamente, eseguire il comando seguente `convert -h` sulla riga di comando.

   Viene visualizzata una schermata della guida con tutte le opzioni possibili dello strumento di conversione.

   >[!NOTE]
   >
   >In alcune versioni di Windows, il comando convert potrebbe non essere eseguito perché in conflitto con l&#39;utilità di conversione nativa che fa parte dell&#39; [!DNL Windows] installazione. In questo caso, indicare il percorso completo del [!DNL ImageMagick] software utilizzato per convertire i file immagine in miniature. Esempio, `"C:\Program Files\ImageMagick-6.8.9-Q16\convert.exe" -define jpeg:size=319x319 ${filename} -thumbnail 319x319 cq5dam.thumbnail.319.319.png`.

1. Per verificare se lo strumento viene eseguito correttamente, aggiungete un&#39;immagine JPG alla directory di lavoro ed eseguite il comando convert `<image-name>.jpg -flip <image-name>-flipped.jpg` sulla riga di comando. Un’immagine capovolta viene aggiunta alla directory. Quindi, aggiungi il passaggio della riga di comando al flusso di lavoro **[!UICONTROL Risorsa di aggiornamento DAM.]**
1. Passate alla console **[!UICONTROL Flusso di lavoro]** .
1. Nella scheda **[!UICONTROL Modelli]** , modificate il modello di risorse **[!UICONTROL di aggiornamento]** DAM.
1. Modificate gli [!UICONTROL argomenti] del passaggio di rappresentazione **[!UICONTROL abilitato per il]** Web in: `mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`.
1. Salvare il flusso di lavoro.

Per testare il flusso di lavoro modificato, aggiungete una risorsa a `/content/dam`.

1. Nel file system, ottenere un&#39;immagine TIFF di vostra scelta. Rinominarlo in `myImage.tiff` e copiarlo in `/content/dam`, ad esempio utilizzando WebDAV.
1. Passate alla console **[!UICONTROL CQ5 DAM]** , ad esempio `http://localhost:4502/libs/wcm/core/content/damadmin.html`.
1. Aprite la risorsa **[!UICONTROL myImage.tiff]** e verificate che l’immagine capovolta e le tre miniature siano state create.

#### Configurare il passaggio del processo CommandLineProcess {#configuring-the-commandlineprocess-process-step}

Questa sezione descrive come impostare [!UICONTROL Argomenti processo] di [!UICONTROL CommandLineProcess].

Separate i valori degli argomenti di [!UICONTROL processo] utilizzando la virgola e non iniziate con uno spazio vuoto.

| Argument-Format | Descrizione |
|---|---|
| mime:&lt;mime-type> | Argomento facoltativo. Il processo viene applicato se la risorsa ha lo stesso tipo MIME dell’argomento. <br>È possibile definire diversi tipi MIME. |
| tn:&lt;larghezza>:&lt;altezza> | Argomento facoltativo. Viene creata una miniatura con le dimensioni definite nell’argomento. <br>È possibile definire diverse miniature. |
| cmd: &lt;comando> | Definisce il comando che viene eseguito. La sintassi dipende dallo strumento della riga di comando. È possibile definire un solo comando. <br>Per creare il comando è possibile utilizzare le seguenti variabili:<br>`${filename}`: nome del file di input, ad esempio Original.jpg <br> `${file}`: nome percorso completo del file di input, ad esempio `/tmp/cqdam0816.tmp/original.jpg` <br> `${directory}`: directory del file di input, ad esempio `/tmp/cqdam0816.tmp`<br>`${basename}`: nome del file di input senza estensione, ad esempio originale <br>`${extension}`: estensione del file di input, ad esempio JPG. |

Ad esempio, se [!DNL ImageMagick] è installato sul disco che ospita il [!DNL Experience Manager] server e si crea un passaggio di processo utilizzando [!UICONTROL CommandLineProcess] come implementazione e i seguenti valori come argomenti [!UICONTROL di]processo:

`mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`

quindi, quando il flusso di lavoro viene eseguito, il passaggio viene applicato solo alle risorse che hanno `image/gif` o `mime:image/tiff` come `mime-types`, crea un’immagine capovolta dell’originale, la converte in JPG e crea tre miniature con le dimensioni seguenti: 140x100, 48x48 e 10x250.

Per creare le tre miniature standard utilizzando i seguenti argomenti di [!UICONTROL processo] , utilizzate [!DNL ImageMagick]:

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=319x319 -thumbnail "319x319>" -background transparent -gravity center -extent 319x319 -write png:cq5dam.thumbnail.319.319.png -thumbnail "140x100>" -background transparent -gravity center -extent 140x100 -write cq5dam.thumbnail.140.100.png -thumbnail "48x48>" -background transparent -gravity center -extent 48x48 cq5dam.thumbnail.48.48.png`

Utilizzate i seguenti argomenti [!UICONTROL di] processo per creare la rappresentazione abilitata per il Web utilizzando [!DNL ImageMagick]:

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=1280x1280 -thumbnail "1280x1280>" cq5dam.web.1280.1280.jpeg`

>[!NOTE]
>
>Il passaggio [!UICONTROL CommandLineProcess] si applica solo alle risorse (nodi di tipo `dam:Asset`) o ai discendenti di una risorsa.

>[!MORELIKETHIS]
>
>* [Elabora risorse](assets-workflow.md)

