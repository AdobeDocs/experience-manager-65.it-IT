---
title: Elaborare risorse utilizzando gestori di contenuti multimediali e flussi di lavoro
description: Scopri i gestori di contenuti multimediali e come utilizzare i flussi di lavoro per eseguire attività sulle risorse digitali.
mini-toc-levels: 1
contentOwner: AG
role: User
feature: Workflow,Renditions
exl-id: cfd6c981-1a35-4327-82d7-cf373d842cc3
solution: Experience Manager, Experience Manager Assets
source-git-commit: a28883778c5e8fb90cbbd0291ded17059ab2ba7e
workflow-type: tm+mt
source-wordcount: '2113'
ht-degree: 3%

---

# Elaborare risorse utilizzando gestori di contenuti multimediali e flussi di lavoro {#processing-assets-using-media-handlers-and-workflows}

[!DNL Adobe Experience Manager Assets] viene fornito con un set di flussi di lavoro e gestori di contenuti multimediali predefiniti per elaborare le risorse. Un flusso di lavoro definisce le attività da eseguire sulle risorse, quindi delega le attività specifiche ai gestori di contenuti multimediali, ad esempio la generazione di miniature o l’estrazione di metadati.

Un flusso di lavoro può essere configurato per essere eseguito automaticamente quando viene caricata una risorsa di un particolare tipo MIME. I passaggi di elaborazione sono definiti in termini di una serie di [!DNL Assets] gestori di contenuti multimediali. [!DNL Experience Manager] fornisce alcuni [gestori incorporati](#default-media-handlers), e quelli aggiuntivi possono essere [sviluppo personalizzato](#creating-a-new-media-handler) o definito delegando il processo a un [strumento da riga di comando](#command-line-based-media-handler).

I gestori di file multimediali sono servizi in [!DNL Assets] che eseguono azioni specifiche sulle risorse. Ad esempio, quando un file audio MP3 viene caricato in [!DNL Experience Manager], un flusso di lavoro attiva un gestore MP3 che estrae i metadati e genera una miniatura. I gestori di file multimediali vengono utilizzati con i flussi di lavoro. I tipi MIME più comuni sono supportati in [!DNL Experience Manager]. È possibile eseguire attività specifiche sulle risorse estendendo o creando flussi di lavoro, estendendo o creando gestori di supporti oppure disabilitando e abilitando i gestori di supporti.

>[!NOTE]
>
>Consulta la [Formati di risorse supportati](assets-formats.md) per una descrizione di tutti i formati supportati da [!DNL Assets] e funzioni supportate per ciascun formato.

## Gestori di file multimediali predefiniti {#default-media-handlers}

I seguenti gestori di file multimediali sono disponibili in [!DNL Assets] e gestisce i tipi MIME più comuni:

<!-- TBD: Java versions should not be set to 1.5. Must be updated.
-->

| Nome gestore | Nome servizio (nella console del sistema) | Tipi MIME supportati |
|--------------|--------------------------------------|----------------------|
| [!UICONTROL TextHandler] | com.day.cq.dam.core.impl.handler.TextHandler | text/plain |
| [!UICONTROL PdfHandler] | com.day.cq.dam.handler.standard.pdf.PdfHandler | <ul><li>application/pdf</li><li>application/illustrator</li></ul> |
| [!UICONTROL JpegHandler] | com.day.cq.dam.core.impl.handler.JpegHandler | image/jpeg |
| [!UICONTROL Mp3Handler] | com.day.cq.dam.handler.standard.mp3.Mp3Handler | audio/mpeg<br><b>Importante</b> - Un file MP3 caricato è [elaborati utilizzando una libreria di terze parti](https://www.zxdr.it/programmi/SistEvolBDD/LibJava/doc/de/vdheide/mp3/MP3File.html). La libreria calcola una lunghezza approssimativa non accurata se l&#39;MP3 ha un bitrate variabile (VBR). |
| [!UICONTROL ZipHandler] | com.day.cq.dam.handler.standard.zip.ZipHandler | <ul><li>application/java-archive </li><li> application/zip</li></ul> |
| [!UICONTROL PictHandler] | com.day.cq.dam.handler.standard.pict.PictHandler | image/pict |
| [!UICONTROL StandardImageHandler] | com.day.cq.dam.core.impl.handler.StandardImageHandler | <ul><li>image/gif </li><li> image/png </li> <li>application/photoshop </li> <li>image/jpeg </li><li> image/tiff </li> <li>image/x-ms-bmp </li><li> image/bmp</li></ul> |
| [!UICONTROL MSOfficeHandler] | com.day.cq.dam.handler.standard.msoffice.MSOfficeHandler | application/msword |
| [!UICONTROL MSPowerPointHandler] | com.day.cq.dam.handler.standard.msoffice.MSPowerPointHandler | application/vnd.ms-powerpoint |
| [!UICONTROL OpenOfficeHandler] | com.day.cq.dam.handler.standard.ooxml.OpenOfficeHandler | <ul><li>application/vnd.openxmlformats-officedocument.wordprocessingml.document</li><li> application/vnd.openxmlformats-officedocument.spreadsheetml.sheet</li><li> application/vnd.openxmlformats-officedocument.presentationml.presentation</li></ul> |
| [!UICONTROL EPubHandler] | com.day.cq.dam.handler.standard.epub.EPubHandler | application/epub+zip |
| [!UICONTROL GenericAssetHandler] | com.day.cq.dam.core.impl.handler.GenericAssetHandler | fallback nel caso in cui non sia stato trovato alcun altro gestore per estrarre dati da una risorsa |

{style="table-layout:auto"}

Tutti gli handler eseguono le operazioni seguenti:

* estrazione di tutti i metadati disponibili dalla risorsa.
* creazione di un’immagine in miniatura di una risorsa.

Per visualizzare i gestori di file multimediali attivi:

1. Nel browser, passa a `https://localhost:4502/system/console/components`.
1. Fai clic su `com.day.cq.dam.core.impl.store.AssetStoreImpl`.
1. Viene visualizzato un elenco con tutti i gestori di file multimediali attivi. Ad esempio:

![chlimage_1-437](assets/chlimage_1-437.png)

## Utilizzare i gestori di contenuti multimediali nei flussi di lavoro per eseguire attività sulle risorse {#using-media-handlers-in-workflows-to-perform-tasks-on-assets}

I gestori di file multimediali sono servizi utilizzati con i flussi di lavoro.

[!DNL Experience Manager] dispone di alcuni flussi di lavoro predefiniti per l’elaborazione delle risorse. Per visualizzarli, apri la console Flusso di lavoro e fai clic su **[!UICONTROL Modelli]** scheda: i titoli del flusso di lavoro che iniziano con [!DNL Assets] sono specifiche per le risorse.

È possibile estendere i flussi di lavoro esistenti e crearne di nuovi per elaborare le risorse in base a requisiti specifici.

L’esempio seguente mostra come migliorare il flusso di lavoro di **[!UICONTROL Sincronizzazione AEM Assets]** in modo che vengano generate le risorse secondarie di tutte le risorse, eccetto i documenti PDF.

### Disabilitare o abilitare un gestore di contenuti multimediali {#disabling-enabling-a-media-handler}

I gestori di file multimediali possono essere disabilitati o abilitati tramite la console di gestione web Apache Felix. Quando il gestore dei contenuti multimediali è disattivato, le relative attività non vengono eseguite sulle risorse.

Per attivare/disattivare un gestore di supporti:

1. Nel browser, passa a `https://<host>:<port>/system/console/components`.
1. Clic **[!UICONTROL Disattiva]** accanto al nome del gestore dei contenuti multimediali. Ad esempio: `com.day.cq.dam.handler.standard.mp3.Mp3Handler`.
1. Aggiorna la pagina: accanto al gestore dei contenuti multimediali viene visualizzata un’icona che indica che è disabilitato.
1. Per abilitare il gestore di file multimediali, fai clic su **[!UICONTROL Abilita]** accanto al nome del gestore dei contenuti multimediali.

### Creare un gestore di contenuti multimediali {#creating-a-new-media-handler}

Per supportare un nuovo tipo di file multimediale o per eseguire attività specifiche su una risorsa, è necessario creare un gestore di file multimediali. Questa sezione descrive come procedere.

#### Classi e interfacce importanti {#important-classes-and-interfaces}

Il modo migliore per avviare un’implementazione è ereditare da un’implementazione astratta fornita che si occupa della maggior parte delle cose e fornisce un comportamento predefinito ragionevole: `com.day.cq.dam.core.AbstractAssetHandler` classe.

Questa classe fornisce già un descrittore di servizio astratto. Pertanto, se hai ereditato da questa classe e utilizzi maven-sling-plugin, assicurati di impostare il flag inherit su `true`.

Implementa i seguenti metodi:

* `extractMetadata()`: estrae tutti i metadati disponibili.
* `getThumbnailImage()`: crea un’immagine di miniatura dalla risorsa passata.
* `getMimeTypes()`: restituisce i tipi MIME della risorsa.

Di seguito è riportato un modello di esempio:

```Java
package my.own.stuff; /** * @scr.component inherit="true" * @scr.service */ public class MyMediaHandler extends com.day.cq.dam.core.AbstractAssetHandler { // implement the relevant parts }
```

L’interfaccia e le classi includono:

* `com.day.cq.dam.api.handler.AssetHandler` Interfaccia: questa interfaccia descrive il servizio che aggiunge il supporto per tipi MIME specifici. L’aggiunta di un tipo MIME richiede l’implementazione di questa interfaccia. L’interfaccia contiene metodi per importare ed esportare documenti specifici, per creare miniature ed estrarre metadati.
* `com.day.cq.dam.core.AbstractAssetHandler` classe: questa classe funge da base per tutte le altre implementazioni dei gestori di risorse e fornisce funzionalità comuni.
* Classe `com.day.cq.dam.core.AbstractSubAssetHandler`:
   * Questa classe funge da base per tutte le altre implementazioni dei gestori di risorse e fornisce funzionalità comunemente utilizzate oltre a quelle più comuni per l’estrazione di risorse secondarie.
   * Il modo migliore per avviare un’implementazione è ereditare da un’implementazione astratta fornita che si occupa della maggior parte delle cose e fornisce un comportamento predefinito ragionevole: la classe com.day.cq.dam.core.AbstractAssetHandler.
   * Questa classe fornisce già un descrittore di servizio astratto. Pertanto, se hai ereditato da questa classe e utilizzi maven-sling-plugin, assicurati di impostare il flag inherit su true.

Devono essere implementati i seguenti metodi:

* `extractMetadata()`: questo metodo estrae tutti i metadati disponibili.
* `getThumbnailImage()`: questo metodo crea un’immagine di miniatura dalla risorsa passata.
* `getMimeTypes()`: questo metodo restituisce i tipi MIME delle risorse.

Di seguito è riportato un modello di esempio:

package my.own.stuff; /&amp;ast;&amp;ast; &amp;ast; @scr.component inherit=&quot;true&quot; &amp;ast; @scr.service &amp;ast;/ public class MyMediaHandler estende com.day.cq.dam.core.AbstractAssetHandler { // implementa le parti pertinenti }

L’interfaccia e le classi includono:

* `com.day.cq.dam.api.handler.AssetHandler` Interfaccia: questa interfaccia descrive il servizio che aggiunge il supporto per tipi MIME specifici. L’aggiunta di un tipo MIME richiede l’implementazione di questa interfaccia. L’interfaccia contiene metodi per importare ed esportare documenti specifici, per creare miniature ed estrarre metadati.
* `com.day.cq.dam.core.AbstractAssetHandler` classe: questa classe funge da base per tutte le altre implementazioni dei gestori di risorse e fornisce funzionalità comuni.
* `com.day.cq.dam.core.AbstractSubAssetHandler` classe: questa classe funge da base per tutte le altre implementazioni dei gestori di risorse e fornisce funzionalità comuni, oltre a quelle comuni per l’estrazione di risorse secondarie.

#### Esempio: creare un gestore di testo specifico {#example-create-a-specific-text-handler}

In questa sezione viene creato un gestore di testo specifico che genera le miniature con una filigrana.

Procedere come segue:

Fai riferimento a [Strumenti di sviluppo](../sites-developing/dev-tools.md) per installare e configurare Eclipse con un [!DNL Maven] e per la configurazione delle dipendenze necessarie per il [!DNL Maven] progetto.

Dopo aver eseguito la procedura seguente, quando carichi un file TXT in [!DNL Experience Manager], i metadati del file vengono estratti e vengono generate due miniature con una filigrana.

1. In Eclipse, crea `myBundle` [!DNL Maven] progetto:

   1. Nella barra dei menu, fai clic su **[!UICONTROL File]** > **[!UICONTROL Nuovo]** > **[!UICONTROL Altro]**.
   1. Nella finestra di dialogo, espandi [!DNL Maven] cartella, seleziona la [!DNL Maven] progetto, quindi fai clic su **[!UICONTROL Successivo]**.
   1. Seleziona la casella Crea un progetto semplice e la casella Usa percorso area di lavoro predefinito, quindi fai clic su **[!UICONTROL Successivo]**.
   1. Definisci un [!DNL Maven] progetto:

      * ID gruppo: `com.day.cq5.myhandler`.
      * ID artefatto: myBundle.
      * Nome: Il mio [!DNL Experience Manager] pacchetto.
      * Descrizione: Questo è il mio [!DNL Experience Manager] pacchetto.

   1. Clic **[!UICONTROL Fine]**.

1. Imposta il [!DNL Java™] alla versione 1.5:

   1. Fare clic con il pulsante destro del mouse `myBundle` progetto, seleziona [!UICONTROL Proprietà].
   1. Seleziona [!UICONTROL Compilatore Java™] e imposta le seguenti proprietà su 1.5:

      * Livello di conformità del compilatore
      * Compatibilità dei file .class generati
      * Compatibilità sorgente

   1. Clic **[!UICONTROL OK]**. Nella finestra di dialogo, fai clic su **[!UICONTROL Sì]**.

1. Sostituisci il codice in `pom.xml` file con il seguente codice:

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

1. Creare il pacchetto `com.day.cq5.myhandler` che contiene [!DNL Java™] classi in `myBundle/src/main/java`:

   1. In myBundle, fare clic con il pulsante destro del mouse `src/main/java`, selezionare Nuovo, quindi Pacchetto.
   1. Assegna un nome `com.day.cq5.myhandler` e fare clic su Fine.

1. Creare [!DNL Java™] classe `MyHandler`:

   1. In entrata [!DNL Eclipse], in `myBundle/src/main/java`, fare clic con il pulsante destro del mouse `com.day.cq5.myhandler` pacchetto. Seleziona [!UICONTROL Nuovo], quindi [!UICONTROL Classe].
   1. Nella finestra di dialogo, assegna un nome alla [!DNL Java™] classe `MyHandler` e fai clic su [!UICONTROL Fine]. [!DNL Eclipse] crea e apre il file `MyHandler.java`.
   1. In entrata `MyHandler.java`, sostituisci il codice esistente con il seguente e salva le modifiche:

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
      watermarkLayer = ImageHelper.createLayer(session, "/content/dam/we-retail/en/products/apparel/gloves/Gloves.jpg");
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
     // We need to keep track of the last character, if we have two whitespaces in a row we do not want to double count.
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

1. Compila il [!DNL Java™] e creare il bundle:

   1. Fare clic con il pulsante destro del mouse `myBundle` progetto, seleziona **[!UICONTROL Esegui come]**, quindi **[!UICONTROL Installazione Maven]**.
   1. Il bundle `myBundle-0.0.1-SNAPSHOT.jar` (contenente la classe compilata) viene creato in `myBundle/target`.

1. In CRX explorer, crea un nodo sotto `/apps/myApp`. Nome = `install`, Tipo = `nt:folder`.
1. Copiare il bundle `myBundle-0.0.1-SNAPSHOT.jar` e conservarlo in `/apps/myApp/install` ad esempio con WebDAV. Il nuovo gestore di testo è ora attivo in [!DNL Experience Manager].
1. Nel browser, apri la [!UICONTROL Console di gestione web Apache Felix]. Seleziona la [!UICONTROL Componenti] e disabilita il gestore di testo predefinito `com.day.cq.dam.core.impl.handler.TextHandler`.

## Gestore di supporti basato su riga di comando {#command-line-based-media-handler}

[!DNL Experience Manager] consente di eseguire qualsiasi strumento della riga di comando all’interno di un flusso di lavoro per convertire le risorse (ad esempio [!DNL ImageMagick]) e per aggiungere la nuova rappresentazione alla risorsa. Installare lo strumento della riga di comando solo sul disco che ospita [!DNL Experience Manager] e per aggiungere e configurare una fase del processo al flusso di lavoro. Il processo richiamato, denominato `CommandLineProcess`, filtra anche in base a tipi MIME specifici e per creare più miniature in base alla nuova rappresentazione.

Le seguenti conversioni possono essere eseguite e memorizzate automaticamente in [!DNL Assets]:

* Trasformazione di EPS e AI tramite [ImageMagick](https://www.imagemagick.org/script/index.php) e [Ghostscript](https://www.ghostscript.com/).
* Trascodifica video FLV tramite [FFmpeg](https://ffmpeg.org/).
* Codifica MP3 tramite [ZOPPICANTE](https://lame.sourceforge.io/).
* Elaborazione audio tramite [SOX](https://sourceforge.net/projects/sox/).

>[!NOTE]
>
>Nei sistemi non Windows, lo strumento FFmpeg restituisce un errore durante la generazione di rappresentazioni per una risorsa video il cui nome file contiene una virgoletta singola (&#39;). Se il nome del file video include una virgoletta singola, rimuovilo prima di caricarlo in [!DNL Experience Manager].

Il `CommandLineProcess` Il processo esegue le operazioni seguenti nell&#39;ordine elencato:

* Se specificato, filtra il file in base a tipi MIME specifici.
* Crea una directory temporanea sul disco che ospita [!DNL Experience Manager] server.
* Trasmette il file originale alla directory temporanea.
* Esegue il comando definito dagli argomenti del passaggio. Il comando viene eseguito all&#39;interno della directory temporanea con le autorizzazioni dell&#39;utente che esegue [!DNL Experience Manager].
* Trasmette il risultato nella cartella di rendering del [!DNL Experience Manager] server.
* Elimina la directory temporanea.
* Crea le miniature in base a tali rappresentazioni, se specificato. Il numero e le dimensioni delle miniature vengono definiti dagli argomenti del passaggio.

### Un esempio che utilizza [!DNL ImageMagick] {#an-example-using-imagemagick}

Nell&#39;esempio seguente viene illustrato come impostare il passaggio di elaborazione della riga di comando in modo che ogni volta che viene aggiunta una risorsa con GIF o TIFF di tipo e miMIME `/content/dam` il [!DNL Experience Manager] server, viene creata un&#39;immagine invertita dell&#39;originale. Vengono inoltre create altre tre miniature: 140x100, 48x48 e 10x250.

A tale scopo, utilizza [!DNL ImageMagick]. [!DNL ImageMagick] è un software gratuito per riga di comando utilizzato per creare, modificare e comporre immagini bitmap.

Installa [!DNL ImageMagick] sul disco che ospita il [!DNL Experience Manager] server:

1. Installa [!DNL ImageMagick]: vedi [Documentazione di ImageMagick](https://www.imagemagick.org/script/download.php).
1. Impostare lo strumento in modo che una delle righe di comando possa essere eseguita `convert`.
1. Per verificare se lo strumento è installato correttamente, eseguire il comando seguente `convert -h` sulla riga di comando.

   Viene visualizzata una schermata della guida con tutte le opzioni possibili dello strumento di conversione.

   >[!NOTE]
   >
   >In alcune versioni di Windows, l&#39;esecuzione del comando convert potrebbe non riuscire perché è in conflitto con l&#39;utilità di conversione nativa che fa parte di [!DNL Windows] installazione. In questo caso, indicare il percorso completo per [!DNL ImageMagick] software utilizzato per convertire i file immagine in miniature. Esempio: `"C:\Program Files\ImageMagick-6.8.9-Q16\convert.exe" -define jpeg:size=319x319 ${filename} -thumbnail 319x319 cq5dam.thumbnail.319.319.png`.

1. Per verificare se lo strumento viene eseguito correttamente, aggiungete un&#39;immagine JPG alla directory di lavoro ed eseguite il comando convert `<image-name>.jpg -flip <image-name>-flipped.jpg` sulla riga di comando. Un&#39;immagine capovolta viene aggiunta alla directory. Quindi, aggiungi il passaggio della riga di comando al **[!UICONTROL Aggiorna risorsa DAM]** flusso di lavoro.
1. Vai a **[!UICONTROL Flusso di lavoro]** console.
1. In **[!UICONTROL Modelli]** , modificare il **[!UICONTROL Aggiorna risorsa DAM]** modello.
1. Modificare il [!UICONTROL Argomenti] del **[!UICONTROL Rappresentazione abilitata per il Web]** passa a: `mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`.
1. Salva il flusso di lavoro.

Per verificare il flusso di lavoro modificato, aggiungi una risorsa a `/content/dam`.

1. Nel file system, ottenere un&#39;immagine TIFF desiderata. Rinomina in `myImage.tiff` e copiarlo in `/content/dam`, ad esempio utilizzando WebDAV.
1. Vai a **[!UICONTROL DAM CQ5]** console, ad esempio `https://localhost:4502/libs/wcm/core/content/damadmin.html`.
1. Apri la risorsa **[!UICONTROL myImage.tiff]** e verificare che l&#39;immagine capovolta e le tre miniature siano state create.

#### Configurare il passaggio del processo CommandLineProcess {#configuring-the-commandlineprocess-process-step}

Questa sezione descrive come impostare [!UICONTROL Argomenti processo] di [!UICONTROL CommandLineProcess].

Separa i valori della [!UICONTROL Argomenti processo] utilizzando la virgola e non iniziare con uno spazio vuoto.

| Formato argomento | Descrizione |
|---|---|
| mime:&lt;mime-type> | Argomento facoltativo. Il processo viene applicato se la risorsa ha lo stesso tipo MIME di quello nell’argomento. <br>È possibile definire diversi tipi MIME. |
| tn:&lt;width>:&lt;height> | Argomento facoltativo. Il processo crea una miniatura con le dimensioni definite nell&#39;argomento. <br>È possibile definire più miniature. |
| comando: &lt;command> | Definisce il comando eseguito. La sintassi dipende dallo strumento della riga di comando. È possibile definire un solo comando. <br>Per creare il comando è possibile utilizzare le seguenti variabili:<br>`${filename}`: nome del file di input, ad esempio original.jpg <br> `${file}`: nome del percorso completo del file di input, ad esempio, `/tmp/cqdam0816.tmp/original.jpg` <br> `${directory}`: directory del file di input, ad esempio, `/tmp/cqdam0816.tmp` <br>`${basename}`: nome del file di input senza estensione, ad esempio originale <br>`${extension}`: estensione del file di input, ad esempio JPG. |

Ad esempio, se [!DNL ImageMagick] è installato sul disco che ospita [!DNL Experience Manager] e se crei un passaggio del processo utilizzando [!UICONTROL CommandLineProcess] come Implementazione e i seguenti valori come [!UICONTROL Argomenti processo]:

`mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`

Quindi, quando il flusso di lavoro viene eseguito, il passaggio si applica solo alle risorse che hanno `image/gif` o `mime:image/tiff` as `mime-types`. Crea un&#39;immagine invertita dell&#39;originale, la converte in JPG e crea tre miniature con le dimensioni 140x100, 48x48 e 10x250.

Utilizza quanto segue [!UICONTROL Argomenti processo] per creare le tre miniature standard utilizzando [!DNL ImageMagick]:

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=319x319 -thumbnail "319x319>" -background transparent -gravity center -extent 319x319 -write png:cq5dam.thumbnail.319.319.png -thumbnail "140x100>" -background transparent -gravity center -extent 140x100 -write cq5dam.thumbnail.140.100.png -thumbnail "48x48>" -background transparent -gravity center -extent 48x48 cq5dam.thumbnail.48.48.png`

Utilizza quanto segue [!UICONTROL Argomenti processo] per creare la rappresentazione abilitata per il web utilizzando [!DNL ImageMagick]:

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=1280x1280 -thumbnail "1280x1280>" cq5dam.web.1280.1280.jpeg`

>[!NOTE]
>
>Il [!UICONTROL CommandLineProcess] il passaggio si applica solo alle risorse (nodi di tipo `dam:Asset`) o i discendenti di una risorsa.

>[!MORELIKETHIS]
>
>* [Elabora risorse](assets-workflow.md)
