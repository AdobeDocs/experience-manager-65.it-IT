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

[!DNL Adobe Experience Manager Assets] viene fornito con un set di flussi di lavoro predefiniti e gestori di contenuti multimediali per elaborare le risorse. Un flusso di lavoro definisce le attività da eseguire sulle risorse, quindi delega le attività specifiche ai gestori di contenuti multimediali, ad esempio la generazione di miniature o l’estrazione di metadati.

Un flusso di lavoro può essere configurato per essere eseguito automaticamente quando viene caricata una risorsa di un particolare tipo MIME. I passaggi di elaborazione sono definiti in termini di una serie di [!DNL Assets] gestori di supporti. [!DNL Experience Manager] fornisce alcuni [gestori incorporati](#default-media-handlers) e altri possono essere [personalizzati](#creating-a-new-media-handler) o definiti delegando il processo a uno [strumento da riga di comando](#command-line-based-media-handler).

I gestori di file multimediali sono servizi in [!DNL Assets] che eseguono azioni specifiche sulle risorse. Ad esempio, quando un file audio MP3 viene caricato in [!DNL Experience Manager], un flusso di lavoro attiva un gestore MP3 che estrae i metadati e genera una miniatura. I gestori di file multimediali vengono utilizzati con i flussi di lavoro. I tipi MIME più comuni sono supportati in [!DNL Experience Manager]. È possibile eseguire attività specifiche sulle risorse estendendo o creando flussi di lavoro, estendendo o creando gestori di supporti oppure disabilitando e abilitando i gestori di supporti.

>[!NOTE]
>
>Per una descrizione di tutti i formati supportati da [!DNL Assets] e delle funzionalità supportate per ciascun formato, vedere la pagina [Formati risorse supportati](assets-formats.md).

## Gestori di file multimediali predefiniti {#default-media-handlers}

I seguenti gestori multimediali sono disponibili in [!DNL Assets] e gestiscono i tipi MIME più comuni:

<!-- TBD: Java versions should not be set to 1.5. Must be updated.
-->

| Nome gestore | Nome servizio (nella console del sistema) | Tipi MIME supportati |
|--------------|--------------------------------------|----------------------|
| [!UICONTROL GestoreTesto] | com.day.cq.dam.core.impl.handler.TextHandler | text/plain |
| [!UICONTROL GestorePdf] | com.day.cq.dam.handler.standard.pdf.PdfHandler | <ul><li>application/pdf</li><li>application/illustrator</li></ul> |
| [!UICONTROL JpegHandler] | com.day.cq.dam.core.impl.handler.JpegHandler | image/jpeg |
| [!UICONTROL Mp3Handler] | com.day.cq.dam.handler.standard.mp3.Mp3Handler | audio/mpeg<br><b>Importante</b> - Un file MP3 caricato è [elaborato utilizzando una libreria di terze parti](https://www.zxdr.it/programmi/SistEvolBDD/LibJava/doc/de/vdheide/mp3/MP3File.html). La libreria calcola una lunghezza approssimativa non accurata se l&#39;MP3 ha un bitrate variabile (VBR). |
| [!UICONTROL GestoreZip] | com.day.cq.dam.handler.standard.zip.ZipHandler | <ul><li>application/java-archive </li><li> application/zip</li></ul> |
| [!UICONTROL PictHandler] | com.day.cq.dam.handler.standard.pict.PictHandler | image/pict |
| [!UICONTROL GestoreImmagineStandard] | com.day.cq.dam.core.impl.handler.StandardImageHandler | <ul><li>image/gif </li><li> image/png </li> <li>application/photoshop </li> <li>image/jpeg </li><li> image/tiff </li> <li>image/x-ms-bmp </li><li> image/bmp</li></ul> |
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

[!DNL Experience Manager] dispone di alcuni flussi di lavoro predefiniti per elaborare le risorse. Per visualizzarli, apri la console Flusso di lavoro e fai clic sulla scheda **[!UICONTROL Modelli]**: i titoli del flusso di lavoro che iniziano con [!DNL Assets] sono quelli specifici delle risorse.

È possibile estendere i flussi di lavoro esistenti e crearne di nuovi per elaborare le risorse in base a requisiti specifici.

L’esempio seguente mostra come migliorare il flusso di lavoro di **[!UICONTROL Sincronizzazione AEM Assets]** in modo che vengano generate le risorse secondarie di tutte le risorse, eccetto i documenti PDF.

### Disabilitare o abilitare un gestore di contenuti multimediali {#disabling-enabling-a-media-handler}

I gestori di file multimediali possono essere disabilitati o abilitati tramite la console di gestione web Apache Felix. Quando il gestore dei contenuti multimediali è disattivato, le relative attività non vengono eseguite sulle risorse.

Per attivare/disattivare un gestore di supporti:

1. Nel browser, passa a `https://<host>:<port>/system/console/components`.
1. Fare clic su **[!UICONTROL Disable]** accanto al nome del gestore di supporti. Ad esempio: `com.day.cq.dam.handler.standard.mp3.Mp3Handler`.
1. Aggiorna la pagina: accanto al gestore dei contenuti multimediali viene visualizzata un’icona che indica che è disabilitato.
1. Per abilitare il gestore di supporti, fare clic su **[!UICONTROL Abilita]** accanto al nome del gestore di supporti.

### Creare un gestore di contenuti multimediali {#creating-a-new-media-handler}

Per supportare un nuovo tipo di file multimediale o per eseguire attività specifiche su una risorsa, è necessario creare un gestore di file multimediali. Questa sezione descrive come procedere.

#### Classi e interfacce importanti {#important-classes-and-interfaces}

Il modo migliore per avviare un&#39;implementazione è ereditare da un&#39;implementazione astratta fornita che si occupa della maggior parte delle cose e fornisce un comportamento predefinito ragionevole: la classe `com.day.cq.dam.core.AbstractAssetHandler`.

Questa classe fornisce già un descrittore di servizio astratto. Pertanto, se hai ereditato da questa classe e utilizzi maven-sling-plugin, assicurati di impostare il flag inherit su `true`.

Implementa i seguenti metodi:

* `extractMetadata()`: estrae tutti i metadati disponibili.
* `getThumbnailImage()`: crea un&#39;immagine di miniatura dalla risorsa passata.
* `getMimeTypes()`: restituisce i tipi MIME della risorsa.

Di seguito è riportato un modello di esempio:

```Java
package my.own.stuff; /** * @scr.component inherit="true" * @scr.service */ public class MyMediaHandler extends com.day.cq.dam.core.AbstractAssetHandler { // implement the relevant parts }
```

L’interfaccia e le classi includono:

* Interfaccia `com.day.cq.dam.api.handler.AssetHandler`: descrive il servizio che aggiunge il supporto per tipi MIME specifici. L’aggiunta di un tipo MIME richiede l’implementazione di questa interfaccia. L’interfaccia contiene metodi per importare ed esportare documenti specifici, per creare miniature ed estrarre metadati.
* Classe `com.day.cq.dam.core.AbstractAssetHandler`: questa classe funge da base per tutte le altre implementazioni dei gestori di risorse e fornisce funzionalità comuni.
* Classe `com.day.cq.dam.core.AbstractSubAssetHandler`:
   * Questa classe funge da base per tutte le altre implementazioni dei gestori di risorse e fornisce funzionalità comunemente utilizzate oltre a quelle più comuni per l’estrazione di risorse secondarie.
   * Il modo migliore per avviare un’implementazione è ereditare da un’implementazione astratta fornita che si occupa della maggior parte delle cose e fornisce un comportamento predefinito ragionevole: la classe com.day.cq.dam.core.AbstractAssetHandler.
   * Questa classe fornisce già un descrittore di servizio astratto. Pertanto, se hai ereditato da questa classe e utilizzi maven-sling-plugin, assicurati di impostare il flag inherit su true.

Devono essere implementati i seguenti metodi:

* `extractMetadata()`: questo metodo estrae tutti i metadati disponibili.
* `getThumbnailImage()`: questo metodo crea un&#39;immagine di miniatura dalla risorsa passata.
* `getMimeTypes()`: questo metodo restituisce i tipi MIME delle risorse.

Di seguito è riportato un modello di esempio:

package my.own.stuff; /&amp;ast;&amp;ast; &amp;ast; @scr.component inherit=&quot;true&quot; &amp;ast; @scr.service &amp;ast;/ public class MyMediaHandler estende com.day.cq.dam.core.AbstractAssetHandler { // implementa le parti pertinenti }

L’interfaccia e le classi includono:

* Interfaccia `com.day.cq.dam.api.handler.AssetHandler`: descrive il servizio che aggiunge il supporto per tipi MIME specifici. L’aggiunta di un tipo MIME richiede l’implementazione di questa interfaccia. L’interfaccia contiene metodi per importare ed esportare documenti specifici, per creare miniature ed estrarre metadati.
* Classe `com.day.cq.dam.core.AbstractAssetHandler`: questa classe funge da base per tutte le altre implementazioni dei gestori di risorse e fornisce funzionalità comuni.
* Classe `com.day.cq.dam.core.AbstractSubAssetHandler`: questa classe funge da base per tutte le altre implementazioni dei gestori di risorse e fornisce funzionalità comuni oltre a quelle comuni per l&#39;estrazione di risorse secondarie.

#### Esempio: creare un gestore di testo specifico {#example-create-a-specific-text-handler}

In questa sezione viene creato un gestore di testo specifico che genera le miniature con una filigrana.

Procedere come segue:

Consulta [Strumenti di sviluppo](../sites-developing/dev-tools.md) per installare e configurare Eclipse con un plug-in [!DNL Maven] e per configurare le dipendenze necessarie per il progetto [!DNL Maven].

Dopo aver eseguito la procedura seguente, quando si carica un file TXT in [!DNL Experience Manager], i metadati del file vengono estratti e vengono generate due miniature con una filigrana.

1. In Eclipse, crea il progetto `myBundle` [!DNL Maven]:

   1. Nella barra dei menu, fai clic su **[!UICONTROL File]** > **[!UICONTROL Nuovo]** > **[!UICONTROL Altro]**.
   1. Nella finestra di dialogo, espandi la cartella [!DNL Maven], seleziona il progetto [!DNL Maven], quindi fai clic su **[!UICONTROL Avanti]**.
   1. Selezionare la casella Crea un progetto semplice e la casella Usa percorso Workspace predefinito, quindi fare clic su **[!UICONTROL Avanti]**.
   1. Definisci un progetto [!DNL Maven]:

      * ID gruppo: `com.day.cq5.myhandler`.
      * ID artefatto: myBundle.
      * Nome: il mio bundle [!DNL Experience Manager].
      * Descrizione: questo è il pacchetto [!DNL Experience Manager].

   1. Fare clic su **[!UICONTROL Fine]**.

1. Impostare il compilatore [!DNL Java™] sulla versione 1.5:

   1. Fare clic con il pulsante destro del mouse sul progetto `myBundle` e selezionare [!UICONTROL Proprietà].
   1. Selezionare [!UICONTROL Java™ Compiler] e impostare le proprietà seguenti su 1.5:

      * Livello di conformità del compilatore
      * Compatibilità dei file .class generati
      * Compatibilità con Source

   1. Fare clic su **[!UICONTROL OK]**. Nella finestra di dialogo, fai clic su **[!UICONTROL Sì]**.

1. Sostituire il codice nel file `pom.xml` con il seguente codice:

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

1. Creare il pacchetto `com.day.cq5.myhandler` che contiene le classi [!DNL Java™] in `myBundle/src/main/java`:

   1. In myBundle fare clic con il pulsante destro del mouse su `src/main/java`, selezionare Nuovo, quindi Pacchetto.
   1. Assegnare un nome a `com.day.cq5.myhandler` e fare clic su Fine.

1. Creare la classe [!DNL Java™] `MyHandler`:

   1. In [!DNL Eclipse], in `myBundle/src/main/java`, fare clic con il pulsante destro del mouse sul pacchetto `com.day.cq5.myhandler`. Seleziona [!UICONTROL Nuovo], quindi [!UICONTROL Classe].
   1. Nella finestra di dialogo, assegnare un nome alla classe [!DNL Java™] `MyHandler` e fare clic su [!UICONTROL Fine]. [!DNL Eclipse] crea e apre il file `MyHandler.java`.
   1. In `MyHandler.java`, sostituire il codice esistente con il seguente, quindi salvare le modifiche:

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

1. Compila la classe [!DNL Java™] e crea il bundle:

   1. Fare clic con il pulsante destro del mouse sul progetto `myBundle`, selezionare **[!UICONTROL Esegui come]**, quindi **[!UICONTROL Installazione Maven]**.
   1. Il bundle `myBundle-0.0.1-SNAPSHOT.jar` (contenente la classe compilata) è stato creato in `myBundle/target`.

1. In Esplora risorse di CRX, creare un nodo in `/apps/myApp`. Nome = `install`, Tipo = `nt:folder`.
1. Copiare il bundle `myBundle-0.0.1-SNAPSHOT.jar` e archiviarlo in `/apps/myApp/install` (ad esempio, con WebDAV). Il nuovo gestore di testo è ora attivo in [!DNL Experience Manager].
1. Nel browser, apri [!UICONTROL Apache Felix Web Management Console]. Selezionare la scheda [!UICONTROL Componenti] e disattivare il gestore di testo predefinito `com.day.cq.dam.core.impl.handler.TextHandler`.

## Gestore di supporti basato su riga di comando {#command-line-based-media-handler}

[!DNL Experience Manager] consente di eseguire qualsiasi strumento da riga di comando all&#39;interno di un flusso di lavoro per convertire le risorse (ad esempio [!DNL ImageMagick]) e aggiungere la nuova rappresentazione alla risorsa. Installare lo strumento della riga di comando solo sul disco che ospita il server [!DNL Experience Manager] e aggiungere e configurare un passaggio del processo al flusso di lavoro. Il processo richiamato, denominato `CommandLineProcess`, filtra anche in base a tipi MIME specifici e per creare più miniature in base alla nuova rappresentazione.

Le seguenti conversioni possono essere eseguite e memorizzate automaticamente in [!DNL Assets]:

* Trasformazione di EPS e AI tramite [ImageMagick](https://www.imagemagick.org/script/index.php) e [Ghostscript](https://www.ghostscript.com/).
* Trascodifica video FLV tramite [FFmpeg](https://ffmpeg.org/).
* Codifica MP3 tramite [LAME](https://lame.sourceforge.io/).
* Elaborazione audio tramite [SOX](https://sourceforge.net/projects/sox/).

>[!NOTE]
>
>Nei sistemi non Windows, lo strumento FFmpeg restituisce un errore durante la generazione di rappresentazioni per una risorsa video il cui nome file contiene una virgoletta singola (&#39;). Se il nome del file video include virgolette singole, rimuoverlo prima di caricarlo in [!DNL Experience Manager].

Il processo `CommandLineProcess` esegue le operazioni seguenti nell&#39;ordine elencato:

* Se specificato, filtra il file in base a tipi MIME specifici.
* Crea una directory temporanea sul disco che ospita il server [!DNL Experience Manager].
* Trasmette il file originale alla directory temporanea.
* Esegue il comando definito dagli argomenti del passaggio. Il comando viene eseguito nella directory temporanea con le autorizzazioni dell&#39;utente che esegue [!DNL Experience Manager].
* Riporta il risultato nella cartella di rendering del server [!DNL Experience Manager].
* Elimina la directory temporanea.
* Crea le miniature in base a tali rappresentazioni, se specificato. Il numero e le dimensioni delle miniature vengono definiti dagli argomenti del passaggio.

### Esempio con [!DNL ImageMagick] {#an-example-using-imagemagick}

Nell&#39;esempio seguente viene illustrato come impostare il passaggio dell&#39;elaborazione della riga di comando in modo che ogni volta che una risorsa con GIF o TIFF di tipo e miMIME viene aggiunta a `/content/dam` nel server [!DNL Experience Manager], venga creata un&#39;immagine invertita dell&#39;originale. Vengono inoltre create altre tre miniature: 140x100, 48x48 e 10x250.

Per eseguire questa operazione, utilizzare [!DNL ImageMagick]. [!DNL ImageMagick] è un software gratuito per riga di comando utilizzato per creare, modificare e comporre immagini bitmap.

Installa [!DNL ImageMagick] sul disco che ospita il server [!DNL Experience Manager]:

1. Installa [!DNL ImageMagick]: consulta la [documentazione di ImageMagick](https://www.imagemagick.org/script/download.php).
1. Configurare lo strumento in modo da poter eseguire `convert` da una riga di comando.
1. Per verificare se lo strumento è installato correttamente, eseguire il comando seguente `convert -h` sulla riga di comando.

   Viene visualizzata una schermata della guida con tutte le opzioni possibili dello strumento di conversione.

   >[!NOTE]
   >
   >In alcune versioni di Windows è possibile che il comando convert non venga eseguito perché è in conflitto con l&#39;utilità di conversione nativa che fa parte dell&#39;installazione di [!DNL Windows]. In questo caso, indicare il percorso completo del software [!DNL ImageMagick] utilizzato per convertire i file immagine in miniature. Esempio: `"C:\Program Files\ImageMagick-6.8.9-Q16\convert.exe" -define jpeg:size=319x319 ${filename} -thumbnail 319x319 cq5dam.thumbnail.319.319.png`.

1. Per verificare il corretto funzionamento dello strumento, aggiungere un&#39;immagine JPG alla directory di lavoro ed eseguire il comando convert `<image-name>.jpg -flip <image-name>-flipped.jpg` sulla riga di comando. Un&#39;immagine capovolta viene aggiunta alla directory. Quindi, aggiungi il passaggio della riga di comando al flusso di lavoro **[!UICONTROL Risorsa di aggiornamento DAM]**.
1. Passa alla console **[!UICONTROL Flusso di lavoro]**.
1. Nella scheda **[!UICONTROL Modelli]**, modifica il modello **[!UICONTROL Risorsa di aggiornamento DAM]**.
1. Modifica [!UICONTROL Argomenti] del passaggio **[!UICONTROL Rendering abilitato per Web]** in: `mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`.
1. Salva il flusso di lavoro.

Per verificare il flusso di lavoro modificato, aggiungere una risorsa a `/content/dam`.

1. Nel file system, ottenere un&#39;immagine TIFF desiderata. Rinominarlo in `myImage.tiff` e copiarlo in `/content/dam`, ad esempio utilizzando WebDAV.
1. Passa alla console **[!UICONTROL CQ5 DAM]**, ad esempio `https://localhost:4502/libs/wcm/core/content/damadmin.html`.
1. Apri la risorsa **[!UICONTROL myImage.tiff]** e verifica che l&#39;immagine capovolta e le tre miniature siano state create.

#### Configurare il passaggio del processo CommandLineProcess {#configuring-the-commandlineprocess-process-step}

Questa sezione descrive come impostare [!UICONTROL Argomenti processo] di [!UICONTROL CommandLineProcess].

Separare i valori di [!UICONTROL Argomenti processo] utilizzando la virgola e non iniziare con uno spazio vuoto.

| Formato argomento | Descrizione |
|---|---|
| mime:&lt;tipo-mime> | Argomento facoltativo. Il processo viene applicato se la risorsa ha lo stesso tipo MIME di quello nell’argomento. <br>È possibile definire diversi tipi MIME. |
| tn:&lt;larghezza>:&lt;altezza> | Argomento facoltativo. Il processo crea una miniatura con le dimensioni definite nell&#39;argomento. <br>È possibile definire più miniature. |
| cmd: &lt;comando> | Definisce il comando eseguito. La sintassi dipende dallo strumento della riga di comando. È possibile definire un solo comando. <br>Per creare il comando è possibile utilizzare le seguenti variabili:<br>`${filename}`: nome del file di input, ad esempio original.jpg <br> `${file}`: nome del percorso completo del file di input, ad esempio `/tmp/cqdam0816.tmp/original.jpg` <br> `${directory}`: directory del file di input, ad esempio `/tmp/cqdam0816.tmp` <br>`${basename}`: nome del file di input senza estensione, ad esempio <br>`${extension}` originale: estensione del file di input, ad esempio JPG. |

Ad esempio, se [!DNL ImageMagick] è installato sul disco che ospita il server [!DNL Experience Manager] e si crea un passaggio di processo utilizzando [!UICONTROL CommandLineProcess] come implementazione e i valori seguenti come [!UICONTROL Argomenti processo]:

`mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`

Quindi, quando il flusso di lavoro viene eseguito, il passaggio si applica solo alle risorse con `image/gif` o `mime:image/tiff` come `mime-types`. Crea un&#39;immagine invertita dell&#39;originale, la converte in JPG e crea tre miniature con le dimensioni 140x100, 48x48 e 10x250.

Utilizza i seguenti [!UICONTROL Argomenti processo] per creare le tre miniature standard utilizzando [!DNL ImageMagick]:

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=319x319 -thumbnail "319x319>" -background transparent -gravity center -extent 319x319 -write png:cq5dam.thumbnail.319.319.png -thumbnail "140x100>" -background transparent -gravity center -extent 140x100 -write cq5dam.thumbnail.140.100.png -thumbnail "48x48>" -background transparent -gravity center -extent 48x48 cq5dam.thumbnail.48.48.png`

Utilizza i seguenti [!UICONTROL Argomenti processo] per creare la rappresentazione abilitata per il Web utilizzando [!DNL ImageMagick]:

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=1280x1280 -thumbnail "1280x1280>" cq5dam.web.1280.1280.jpeg`

>[!NOTE]
>
>Il passaggio [!UICONTROL CommandLineProcess] si applica solo alle risorse (nodi di tipo `dam:Asset`) o ai discendenti di una risorsa.

>[!MORELIKETHIS]
>
>* [Elabora risorse](assets-workflow.md)
