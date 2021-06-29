---
title: Elabora le risorse utilizzando gestori e flussi di lavoro di contenuti multimediali
description: Scopri i gestori di contenuti multimediali e come utilizzare i flussi di lavoro per eseguire attività sulle risorse digitali.
mini-toc-levels: 1
contentOwner: AG
role: Business Practitioner
feature: Flusso di lavoro, rappresentazioni
exl-id: cfd6c981-1a35-4327-82d7-cf373d842cc3
source-git-commit: 0db95c4e7fc1ca20ce4f2d352c1276aa546dc7c3
workflow-type: tm+mt
source-wordcount: '2166'
ht-degree: 4%

---

# Elabora le risorse utilizzando gestori e flussi di lavoro di contenuti multimediali {#processing-assets-using-media-handlers-and-workflows}

[!DNL Adobe Experience Manager Assets] viene fornito con un set di flussi di lavoro predefiniti e gestori di contenuti multimediali per elaborare le risorse. Un flusso di lavoro definisce le attività da eseguire sulle risorse, quindi delega le attività specifiche ai gestori dei contenuti multimediali, ad esempio la generazione di miniature o l’estrazione dei metadati.

Puoi configurare un flusso di lavoro per l’esecuzione automatica quando viene caricata una risorsa di un particolare tipo MIME. Le fasi di elaborazione sono definite in termini di una serie di [!DNL Assets] gestori di contenuti multimediali. [!DNL Experience Manager] fornisce alcuni gestori  [incorporati ](#default-media-handlers) e altri possono essere  [personalizzati ](#creating-a-new-media-handler) sviluppati o definiti delegando il processo a uno strumento a  [riga di comando](#command-line-based-media-handler).

I gestori di file multimediali sono servizi in [!DNL Assets] che eseguono azioni specifiche sulle risorse. Ad esempio, quando un file audio MP3 viene caricato in [!DNL Experience Manager], un flusso di lavoro attiva un gestore MP3 che estrae i metadati e genera una miniatura. I gestori di file multimediali vengono generalmente utilizzati in combinazione con i flussi di lavoro. La maggior parte dei tipi MIME comuni è supportata in [!DNL Experience Manager]. È possibile eseguire attività specifiche sulle risorse estendendo/creando flussi di lavoro, estendendo/creando gestori di contenuti multimediali o disabilitando/abilitando gestori di contenuti multimediali.

>[!NOTE]
>
>Per una descrizione di tutti i formati supportati da [!DNL Assets] e delle funzioni supportate per ciascun formato, consulta la pagina [Formati supportati dalle risorse](assets-formats.md) .

## Gestori multimediali predefiniti {#default-media-handlers}

I seguenti gestori di contenuti multimediali sono disponibili in [!DNL Assets] e gestiscono i tipi MIME più comuni:

<!-- TBD: Java versions shouldn't be set to 1.5. Must be updated.
-->

| Nome gestore | Nome del servizio (nella console del sistema) | Tipi MIME supportati |
|--------------|--------------------------------------|----------------------|
| [!UICONTROL TextHandler] | com.day.cq.dam.core.impl.handler.TextHandler | text/plain |
| [!UICONTROL PdfHandler] | com.day.cq.dam.handler.standard.pdf.PdfHandler | <ul><li>application/pdf</li><li>applicazione/illustratore</li></ul> |
| [!UICONTROL JpegHandler] | com.day.cq.dam.core.impl.handler.JpegHandler | image/jpeg |
| [!UICONTROL Mp3Handler] | com.day.cq.dam.handler.standard.mp3.Mp3Handler | audio/mpeg<br><b>Importante</b> - Quando carichi un file MP3, questo viene [elaborato utilizzando una libreria di terze parti](http://www.zxdr.it/programmi/SistEvolBDD/LibJava/doc/de/vdheide/mp3/MP3File.html). La libreria calcola una lunghezza approssimativa non accurata se il MP3 ha un bitrate variabile (VBR). |
| [!UICONTROL ZipHandler] | com.day.cq.dam.handler.standard.zip.ZipHandler | <ul><li>application/java-archive </li><li> application/zip</li></ul> |
| [!UICONTROL PictHandler] | com.day.cq.dam.handler.standard.pict.PictHandler | immagine/immagine |
| [!UICONTROL StandardImageHandler] | com.day.cq.dam.core.impl.handler.StandardImageHandler | <ul><li>image/gif </li><li> image/png </li> <li>applicazione/photoshop </li> <li>image/jpeg </li><li> image/tiff </li> <li>immagine/x-ms-bmp </li><li> image/bmp</li></ul> |
| [!UICONTROL MSOfficeHandler] | com.day.cq.dam.handler.standard.msoffice.MSOfficeHandler | application/msword |
| [!UICONTROL MSPowerPointHandler] | com.day.cq.dam.handler.standard.msoffice.MSPowerPointHandler | application/vnd.ms-powerpoint |
| [!UICONTROL OpenOfficeHandler] | com.day.cq.dam.handler.standard.ooxml.OpenOfficeHandler | <ul><li>application/vnd.openxmlformats-officedocument.wordprocessingml.document</li><li> application/vnd.openxmlformats-officedocument.spreadsheetml.sheet</li><li> application/vnd.openxmlformats-officedocument.presentationml.presentation</li></ul> |
| [!UICONTROL EPubHandler] | com.day.cq.dam.handler.standard.epub.EPubHandler | application/epub+zip |
| [!UICONTROL GenericAssetHandler] | com.day.cq.dam.core.impl.handler.GenericAssetHandler | fallback nel caso in cui non sia stato trovato nessun altro gestore per estrarre dati da una risorsa |

{style=&quot;table-layout:auto&quot;}

Tutti i gestori eseguono le seguenti attività:

* estrazione di tutti i metadati disponibili dalla risorsa.
* creazione di una miniatura di una risorsa.

Per visualizzare i gestori di contenuti multimediali attivi:

1. Nel browser, passa a `http://localhost:4502/system/console/components`.
1. Clic `com.day.cq.dam.core.impl.store.AssetStoreImpl`.
1. Viene visualizzato un elenco con tutti i gestori di contenuti multimediali attivi. Esempio:

![chlimage_1-437](assets/chlimage_1-437.png)

## Utilizzare i gestori di contenuti multimediali nei flussi di lavoro per eseguire attività sulle risorse {#using-media-handlers-in-workflows-to-perform-tasks-on-assets}

I gestori di file multimediali sono servizi solitamente utilizzati in combinazione con i flussi di lavoro.

[!DNL Experience Manager] dispone di alcuni flussi di lavoro predefiniti per elaborare le risorse. Per visualizzarli, apri la console Flusso di lavoro e fai clic sulla scheda **[!UICONTROL Modelli]** : i titoli del flusso di lavoro che iniziano con [!DNL Assets] sono quelli specifici per le risorse.

I flussi di lavoro esistenti possono essere estesi e possono essere creati nuovi per elaborare le risorse in base a requisiti specifici.

L’esempio seguente mostra come migliorare il flusso di lavoro di **[!UICONTROL Sincronizzazione AEM Assets]** in modo che vengano generate le risorse secondarie di tutte le risorse, eccetto i documenti PDF.

### Disattivare o attivare un gestore di contenuti multimediali {#disabling-enabling-a-media-handler}

I gestori di contenuti multimediali possono essere disattivati o abilitati tramite la console di gestione web Apache Felix. Quando il gestore multimediale è disabilitato, le sue attività non vengono eseguite sulle risorse.

Per abilitare/disabilitare un gestore di file multimediali:

1. Nel browser, passa a `https://<host>:<port>/system/console/components`.
1. Fare clic su **[!UICONTROL Disabilita]** accanto al nome del gestore multimediale. Esempio: `com.day.cq.dam.handler.standard.mp3.Mp3Handler`.
1. Aggiorna la pagina: accanto al gestore multimediale viene visualizzata un&#39;icona che indica che è disattivato.
1. Per abilitare il gestore multimediale, fai clic su **[!UICONTROL Abilita]** accanto al nome del gestore multimediale.

### Crea un nuovo gestore di file multimediali {#creating-a-new-media-handler}

Per supportare un nuovo tipo di supporto o per eseguire attività specifiche su una risorsa, è necessario creare un nuovo gestore di contenuti multimediali. Questa sezione descrive come procedere.

#### Classi e interfacce importanti {#important-classes-and-interfaces}

Il modo migliore per avviare un’implementazione consiste nell’ereditare da un’implementazione astratta fornita che si occupa della maggior parte delle cose e fornisce un comportamento predefinito ragionevole: la classe `com.day.cq.dam.core.AbstractAssetHandler`.

Questa classe fornisce già un descrittore di servizio astratto. Quindi, se erediti da questa classe e utilizzi il maven-sling-plugin, assicurati di impostare il flag di ereditarietà su `true`.

Implementa i seguenti metodi:

* `extractMetadata()`: estrae tutti i metadati disponibili.
* `getThumbnailImage()`: crea una miniatura della risorsa passata.
* `getMimeTypes()`: restituisce i tipi MIME della risorsa.

Ecco un esempio di modello:

```Java
package my.own.stuff; /** * @scr.component inherit="true" * @scr.service */ public class MyMediaHandler extends com.day.cq.dam.core.AbstractAssetHandler { // implement the relevant parts }
```

L&#39;interfaccia e le classi includono:

* `com.day.cq.dam.api.handler.AssetHandler` interfaccia: Questa interfaccia descrive il servizio che aggiunge il supporto per tipi MIME specifici. Per implementare questa interfaccia è necessario aggiungere un nuovo tipo MIME. L’interfaccia contiene metodi per importare ed esportare i documenti specifici, per creare miniature ed estrarre metadati.
* `com.day.cq.dam.core.AbstractAssetHandler` Classe: Questa classe funge da base per tutte le altre implementazioni dei gestori di risorse e fornisce funzionalità comuni.
* Classe `com.day.cq.dam.core.AbstractSubAssetHandler`:
   * Questa classe funge da base per tutte le altre implementazioni dei gestori di risorse e fornisce funzionalità comuni, oltre a quelle comuni per l’estrazione di risorse secondarie.
   * Il modo migliore per avviare un’implementazione consiste nell’ereditare da un’implementazione astratta fornita che si occupa della maggior parte delle cose e fornisce un comportamento predefinito ragionevole: la classe com.day.cq.dam.core.AbstractAssetHandler .
   * Questa classe fornisce già un descrittore di servizio astratto. Quindi, se erediti da questa classe e utilizzi il maven-sling-plugin, assicurati di impostare il flag di ereditarietà su true.

È necessario implementare i seguenti metodi:

* `extractMetadata()`: questo metodo estrae tutti i metadati disponibili.
* `getThumbnailImage()`: questo metodo crea un’immagine di miniatura dalla risorsa passata.
* `getMimeTypes()`: questo metodo restituisce i tipi MIME della risorsa.

Ecco un esempio di modello:

package my.own.stuff; /&amp;ast;&amp;ast; &amp;ast; @scr.component inherit=&quot;true&quot; &amp;ast; @scr.service &amp;ast;/ classe pubblica MyMediaHandler estende com.day.cq.dam.core.AbstractAssetHandler { // implementa le parti pertinenti }

L&#39;interfaccia e le classi includono:

* `com.day.cq.dam.api.handler.AssetHandler` interfaccia: Questa interfaccia descrive il servizio che aggiunge il supporto per tipi MIME specifici. Per implementare questa interfaccia è necessario aggiungere un nuovo tipo MIME. L’interfaccia contiene metodi per importare ed esportare i documenti specifici, per creare miniature ed estrarre metadati.
* `com.day.cq.dam.core.AbstractAssetHandler` Classe: Questa classe funge da base per tutte le altre implementazioni dei gestori di risorse e fornisce funzionalità comuni.
* `com.day.cq.dam.core.AbstractSubAssetHandler` Classe: Questa classe funge da base per tutte le altre implementazioni dei gestori di risorse e fornisce funzionalità comuni, oltre a quelle comuni per l’estrazione di risorse secondarie.

#### Esempio: creare un gestore di testo specifico {#example-create-a-specific-text-handler}

In questa sezione viene creato un gestore di testo specifico che genera le miniature con una filigrana.

Procedere come segue:

Per installare e impostare Eclipse con un plug-in [!DNL Maven] e per impostare le dipendenze necessarie per il progetto [!DNL Maven], fai riferimento a [Strumenti di sviluppo](../sites-developing/dev-tools.md) .

Dopo aver eseguito la seguente procedura, quando carichi un file TXT in [!DNL Experience Manager], i metadati del file vengono estratti e vengono generate due miniature con una filigrana.

1. In Eclipse, crea un progetto `myBundle` [!DNL Maven] :

   1. Nella barra dei menu, fai clic su **[!UICONTROL File]** > **[!UICONTROL Nuovo]** > **[!UICONTROL Altro]**.
   1. Nella finestra di dialogo, espandi la cartella [!DNL Maven], seleziona il progetto [!DNL Maven] e fai clic su **[!UICONTROL Avanti]**.
   1. Seleziona la casella Crea un progetto semplice e la casella Usa posizioni area di lavoro predefinite , quindi fai clic su **[!UICONTROL Avanti]**.
   1. Definire un progetto [!DNL Maven]:

      * ID gruppo: `com.day.cq5.myhandler`.
      * Id Artifact: myBundle.
      * Nome: Il mio bundle [!DNL Experience Manager].
      * Descrizione: Questo è il mio bundle [!DNL Experience Manager].
   1. Fare clic su **[!UICONTROL Fine]**.


1. Impostare il compilatore [!DNL Java] sulla versione 1.5:

   1. Fai clic con il pulsante destro del mouse sul progetto `myBundle`, seleziona [!UICONTROL Proprietà].
   1. Seleziona [!UICONTROL Java Compiler] e imposta le seguenti proprietà su 1.5:

      * Livello di conformità del compilatore
      * Compatibilità con i file .class generati
      * Compatibilità sorgente
   1. Fai clic su **[!UICONTROL OK]**. Nella finestra di dialogo, fare clic su **[!UICONTROL Sì]**.


1. Sostituisci il codice nel file `pom.xml` con il seguente codice:

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

1. Crea il pacchetto `com.day.cq5.myhandler` che contiene le classi [!DNL Java] in `myBundle/src/main/java`:

   1. In myBundle, fai clic con il pulsante destro del mouse su `src/main/java`, seleziona Nuovo, quindi Pacchetto.
   1. Assegnare un nome `com.day.cq5.myhandler` e fare clic su Fine.

1. Crea la classe [!DNL Java] `MyHandler`:

   1. In [!DNL Eclipse], sotto `myBundle/src/main/java` fai clic con il pulsante destro del mouse sul pacchetto `com.day.cq5.myhandler`. Selezionare [!UICONTROL Nuovo], quindi [!UICONTROL Classe].
   1. Nella finestra di dialogo, denominare la classe [!DNL Java] `MyHandler` e fare clic su [!UICONTROL Fine]. [!DNL Eclipse] crea e apre il file  `MyHandler.java`.
   1. In `MyHandler.java` sostituisci il codice esistente con quanto segue, quindi salva le modifiche:

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

1. Compila la classe [!DNL Java] e crea il bundle:

   1. Fai clic con il pulsante destro del mouse sul progetto `myBundle`, seleziona **[!UICONTROL Esegui come]**, quindi **[!UICONTROL Installazione Maven]**.
   1. Il bundle `myBundle-0.0.1-SNAPSHOT.jar` (contenente la classe compilata) viene creato in `myBundle/target`.

1. In CRX explorer, crea un nuovo nodo sotto `/apps/myApp`. Nome = `install`, Tipo = `nt:folder`.
1. Copia il bundle `myBundle-0.0.1-SNAPSHOT.jar` e archivialo in `/apps/myApp/install` (ad esempio con WebDAV). Il nuovo gestore di testo è ora attivo in [!DNL Experience Manager].
1. Nel browser, apri la [!UICONTROL Console di gestione Web Apache Felix]. Seleziona la scheda [!UICONTROL Componenti] e disattiva il gestore di testo predefinito `com.day.cq.dam.core.impl.handler.TextHandler`.

## Gestore di file multimediali basati su riga di comando {#command-line-based-media-handler}

[!DNL Experience Manager] consente di eseguire qualsiasi strumento a riga di comando all’interno di un flusso di lavoro per convertire le risorse (ad esempio  [!DNL ImageMagick]) e aggiungere il nuovo rendering alla risorsa. È sufficiente installare lo strumento della riga di comando sul disco che ospita il server [!DNL Experience Manager] e aggiungere e configurare un passaggio del processo al flusso di lavoro. Il processo richiamato, denominato `CommandLineProcess`, consente inoltre di filtrare in base a tipi MIME specifici e di creare più miniature in base al nuovo rendering.

Le seguenti conversioni possono essere eseguite e memorizzate automaticamente in [!DNL Assets]:

* Trasformazione EPS e AI utilizzando [ImageMagick](https://www.imagemagick.org/script/index.php) e [Ghostscript](https://www.ghostscript.com/).
* transcodifica video FLV tramite [FFmpeg](https://ffmpeg.org/).
* Codifica MP3 con [LAME](https://lame.sourceforge.io/).
* Elaborazione audio tramite [SOX](https://sox.sourceforge.net/).

>[!NOTE]
>
>Nei sistemi non Windows, lo strumento FFmpeg restituisce un errore durante la generazione di rappresentazioni per una risorsa video con una virgoletta singola (&#39;) nel nome file. Se il nome del file video include una virgoletta singola, rimuovila prima di caricare su [!DNL Experience Manager].

Il processo `CommandLineProcess` esegue le seguenti operazioni nell&#39;ordine in cui sono elencate:

* Filtra il file in base a tipi MIME specifici, se specificato.
* Crea una directory temporanea sul disco che ospita il server [!DNL Experience Manager].
* Invia il file originale alla directory temporanea.
* Esegue il comando definito dagli argomenti del passaggio. Il comando viene eseguito all&#39;interno della directory temporanea con le autorizzazioni dell&#39;utente che esegue [!DNL Experience Manager].
* Invia nuovamente il risultato nella cartella di rendering del server [!DNL Experience Manager].
* Elimina la directory temporanea.
* Crea miniature in base a tali rappresentazioni, se specificato. Il numero e le dimensioni delle miniature sono definiti dagli argomenti del passaggio.

### Un esempio che utilizza [!DNL ImageMagick] {#an-example-using-imagemagick}

L’esempio seguente mostra come impostare il passaggio del processo della riga di comando in modo che ogni volta che una risorsa con il tipo di e-type GIF o TIFF miMIME viene aggiunta a `/content/dam` sul server [!DNL Experience Manager], venga creata un’immagine capovolta dell’originale insieme a tre miniature aggiuntive (140x100, 48x48 e 10x250) .

A questo scopo, utilizza [!DNL ImageMagick]. [!DNL ImageMagick] è un software gratuito della riga di comando utilizzato per creare, modificare e comporre immagini bitmap.

Installa [!DNL ImageMagick] sul disco che ospita il server [!DNL Experience Manager]:

1. Installa [!DNL ImageMagick]: Consulta la [documentazione ImageMagick](https://www.imagemagick.org/script/download.php).
1. Imposta lo strumento in modo da eseguire la conversione sulla riga di comando.
1. Per verificare se lo strumento è installato correttamente, esegui il seguente comando `convert -h` sulla riga di comando.

   Viene visualizzata una schermata di aiuto con tutte le opzioni possibili dello strumento di conversione.

   >[!NOTE]
   >
   >In alcune versioni di Windows, l&#39;esecuzione del comando di conversione potrebbe non riuscire perché è in conflitto con l&#39;utilità di conversione nativa che fa parte dell&#39;installazione di [!DNL Windows]. In questo caso, indicare il percorso completo del software [!DNL ImageMagick] utilizzato per convertire i file immagine in miniature. Esempio, `"C:\Program Files\ImageMagick-6.8.9-Q16\convert.exe" -define jpeg:size=319x319 ${filename} -thumbnail 319x319 cq5dam.thumbnail.319.319.png`.

1. Per verificare se lo strumento funziona correttamente, aggiungi un&#39;immagine JPG alla directory di lavoro ed esegui il comando convert `<image-name>.jpg -flip <image-name>-flipped.jpg` nella riga di comando. Un’immagine capovolta viene aggiunta alla directory. Quindi, aggiungi il passaggio della riga di comando al flusso di lavoro **[!UICONTROL Risorsa di aggiornamento DAM.]**
1. Vai alla console **[!UICONTROL Flusso di lavoro]** .
1. Nella scheda **[!UICONTROL Modelli]** , modifica il modello **[!UICONTROL Risorsa di aggiornamento DAM]** .
1. Modifica il passaggio [!UICONTROL Argomenti] del passaggio **[!UICONTROL Rendition abilitato per web]** in: `mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`.
1. Salva il flusso di lavoro.

Per testare il flusso di lavoro modificato, aggiungi una risorsa a `/content/dam`.

1. Nel file system, ottenere un&#39;immagine TIFF di vostra scelta. Rinomina in `myImage.tiff` e copialo in `/content/dam`, ad esempio utilizzando WebDAV.
1. Vai alla console **[!UICONTROL CQ5 DAM]**, ad esempio `http://localhost:4502/libs/wcm/core/content/damadmin.html`.
1. Apri la risorsa **[!UICONTROL myImage.tiff]** e verifica che sia stata creata l&#39;immagine capovolta e le tre miniature.

#### Configura il passaggio del processo CommandLineProcess {#configuring-the-commandlineprocess-process-step}

Questa sezione descrive come impostare [!UICONTROL Argomenti processo] di [!UICONTROL CommandLineProcess].

Separa i valori di [!UICONTROL Argomenti processo] utilizzando la virgola e non avviarli con uno spazio vuoto.

| Formato argomento | Descrizione |
|---|---|
| mime:&lt;mime-type> | Argomento facoltativo. Il processo viene applicato se la risorsa ha lo stesso tipo MIME di quello dell’argomento. <br>È possibile definire diversi tipi MIME. |
| tn:&lt;larghezza>:&lt;altezza> | Argomento facoltativo. Il processo crea una miniatura con le dimensioni definite nell’argomento. <br>È possibile definire diverse miniature. |
| Comando: &lt;command> | Definisce il comando eseguito. La sintassi dipende dallo strumento della riga di comando. È possibile definire un solo comando. <br>Per creare il comando è possibile utilizzare le seguenti variabili: <br>`${filename}`: nome del file di input, ad esempio original.jpg  <br> `${file}`: nome del percorso completo del file di input, ad esempio  `/tmp/cqdam0816.tmp/original.jpg` <br> `${directory}`: directory del file di input, ad esempio  `/tmp/cqdam0816.tmp` <br>`${basename}`: nome del file di input senza estensione, ad esempio originale  <br>`${extension}`: estensione del file di input, ad esempio JPG. |

Ad esempio, se [!DNL ImageMagick] è installato sul disco che ospita il server [!DNL Experience Manager] e se si crea un passaggio del processo utilizzando [!UICONTROL CommandLineProcess] come Implementazione e i seguenti valori come [!UICONTROL Argomenti del processo]:

`mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`

quindi, quando il flusso di lavoro viene eseguito, il passaggio si applica solo alle risorse con `image/gif` o `mime:image/tiff` come `mime-types`, crea un’immagine capovolta dell’originale, la converte in JPG e crea tre miniature con le dimensioni seguenti: 140x100, 48x48 e 10x250.

Utilizza le seguenti [!UICONTROL Argomenti processo] per creare le tre miniature standard utilizzando [!DNL ImageMagick]:

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=319x319 -thumbnail "319x319>" -background transparent -gravity center -extent 319x319 -write png:cq5dam.thumbnail.319.319.png -thumbnail "140x100>" -background transparent -gravity center -extent 140x100 -write cq5dam.thumbnail.140.100.png -thumbnail "48x48>" -background transparent -gravity center -extent 48x48 cq5dam.thumbnail.48.48.png`

Utilizza i seguenti [!UICONTROL Argomenti processo] per creare il rendering abilitato per il web utilizzando [!DNL ImageMagick]:

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=1280x1280 -thumbnail "1280x1280>" cq5dam.web.1280.1280.jpeg`

>[!NOTE]
>
>Il passaggio [!UICONTROL CommandLineProcess] si applica solo alle risorse (nodi di tipo `dam:Asset`) o ai discendenti di una risorsa.

>[!MORELIKETHIS]
>
>* [Elabora risorse](assets-workflow.md)

