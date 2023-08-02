---
title: Comprimere e decomprimere file utilizzando un’istanza di AEM Forms su JEE DSC personalizzata
description: Scopri come comprimere e decomprimere i file utilizzando un DSC personalizzato di AEM Forms su JEE
exl-id: 1b950d8f-6b54-452a-831b-f5644370691d
source-git-commit: f0dd1ac3ab9c17a8b331f5048d84ec97dd23924f
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 0%

---

# Compressione e decompressione di file tramite un’istanza di AEM Forms su JEE Custom DSC {#compressing-decompressing-files}

## Conoscenze preliminari {#prerequisites}

Esperienza con AEM Forms nella gestione dei processi JEE, nella programmazione Java™ di base e nella creazione di componenti personalizzati.

**Altri prodotti aggiuntivi richiesti**

Editor Java™ come [Eclipse](https://www.eclipse.org/) o [IDE Netbeans](https://netbeans.apache.org/)

## Livello utente {#user-level}

Intermedio

AEM Forms su JEE consente agli sviluppatori di creare DSC (Document Service Container) personalizzato per arricchire le funzioni predefinite. La creazione di tali componenti è collegabile all’ambiente di runtime di AEM Forms su JEE e ha lo scopo previsto. Questo articolo spiega come creare un servizio ZIP personalizzato che può essere utilizzato per comprimere un elenco di file in un file .zip e decomprimere un .zip in un elenco di documenti.

## Creazione di un componente DSC personalizzato {#create-custom-dsc-component}

Creare un componente DSC personalizzato con due operazioni di servizio per comprimere e decomprimere l&#39;elenco di documenti. Questo componente utilizza il pacchetto java.util.zip per la compressione e la decompressione. Per creare un componente personalizzato, segui i passaggi seguenti:

1. Aggiungi il file adobe-livecycle-client.jar alla libreria
1. Aggiungi le icone richieste
1. Creare una classe pubblica
1. Creare due metodi pubblici denominati UnzipDocument e ZipDocuments
1. Scrivi la logica per Compressione e decompressione

Il codice si trova qui:

```java
/*
 * Custom DSC : ZIP Utility
 * Purpose: This is a LiveCycle ES2 custom component used to Compress & Decompress List of Documents
 * Author: Nithiyanandam Dharmadass
 * Organization: Ministry of Finance, Kingdom of Bahrain
 * Last modified Date: 18/Apr/2011
 */
package nith.lces2.dsc;

import java.util.zip.ZipEntry;
import java.util.zip.ZipInputStream;
import com.adobe.idp.Document;
import java.io.ByteArrayOutputStream;
import java.io.InputStream;
import java.util.ArrayList;
import java.util.List;
import java.util.zip.ZipOutputStream;

public class ZIPService {

    static final int BUFFER = 2048; // 2MB buffer size

    public java.util.List UnzipDocument(com.adobe.idp.Document zipDocument) throws Exception {
        ZipInputStream zis = new ZipInputStream(zipDocument.getInputStream());

        ZipEntry zipFile;

        List resultList = new ArrayList();

        while ((zipFile = zis.getNextEntry()) != null) {

            ByteArrayOutputStream byteArrayOutStream = new ByteArrayOutputStream();

            int count;  // an int variable to hold the number of bytes read from input stream
            byte data[] = new byte[BUFFER];
            while ((count = zis.read(data, 0, BUFFER)) != -1) {
                byteArrayOutStream.write(data, 0, count);   // write to byte array
            }

            com.adobe.idp.Document unzippedDoc = new Document(byteArrayOutStream.toByteArray());  // create an idp document
            unzippedDoc.setAttribute("file", zipFile.getName());
            unzippedDoc.setAttribute("wsfilename", zipFile.getName());  // update the wsfilename attribute
            resultList.add(unzippedDoc);
        }
        return resultList;  // List of uncompressed documents
    }

    public com.adobe.idp.Document ZipDocuments(java.util.List listOfDocuments,java.lang.String zipFileName) throws Exception {

        if (listOfDocuments == null || listOfDocuments.size() == 0) {
            return null;
        }

        ByteArrayOutputStream byteArrayOutStream = new ByteArrayOutputStream();
        ZipOutputStream zos = new ZipOutputStream(byteArrayOutStream);  // ZIP Output Stream

        for (int i = 0; i < listOfDocuments.size(); i++) {
            Document doc = (Document) listOfDocuments.get(i);
            InputStream docInputStream = doc.getInputStream();
            ZipEntry zipEntry = new ZipEntry(doc.getAttribute("file").toString());
            zos.putNextEntry(zipEntry);
            int count;
            byte data[] = new byte[BUFFER];
            while ((count = docInputStream.read(data, 0, BUFFER)) != -1) {
                zos.write(data, 0, count);  // Read document content and add to zip entry
            }
            zos.closeEntry();
        }
        zos.flush();
        zos.close();

        Document zippedDoc = new Document(byteArrayOutStream.toByteArray());
        if(zipFileName==null || zipFileName.equals(""))
        {
            zipFileName = "CompressedList.zip";
        }
        zippedDoc.setAttribute("file", zipFileName);
        return zippedDoc;
    }
}
```

## Creazione di un file Component.XML {#create-component-xml-file}

È necessario creare un file component.xml all&#39;interno della cartella principale del pacchetto che ha definito le operazioni del servizio e i relativi parametri.

Il file component.xml viene visualizzato qui:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<component xmlns="https://adobe.com/idp/dsc/component/document">
<!-- Unique id identifying this component -->
   <component-id>ZipService</component-id>

<!-- Version -->
   <version>1.0</version>

<!-- Start of the Service definition -->
   <services>
<!-- Unique name for service descriptor.
           The value is used as the default name for
           deployed services -->
      <service name="ZipService">
<!-- service implementation class definition -->
        <implementation-class>nith.lces2.dsc.ZIPService</implementation-class>

<!-- description -->
        <description>Compress or Decompress list of documents</description>

<!--  You can provide your own icons for a distinct look   -->
          <small-icon>icons/Zip_icon16.png</small-icon>
          <large-icon>icons/Zip_icon32.png</large-icon>


<!-- automatically deploys the service and starts it after installation -->
         <auto-deploy service-id="ZipService" />

         <operations>
<!-- method name in the interface setSmtpHost-->
            <operation name="UnzipDocument">
<!-- input parameters to the "send" method -->
              <input-parameter name="zipDocument" title="Input ZIP Document" type="com.adobe.idp.Document">
                    <hint>A ZIP File to be decompressed</hint>
                </input-parameter>
                <output-parameter name="resultList" title="Decompressed list of documents" type="java.util.List">
                    <hint>Decompressed ZIP list</hint>
                </output-parameter>
            </operation>
            <operation name="ZipDocuments">
<!-- input parameters to the "send" method -->
              <input-parameter name="listOfDocuments" title="List of Documents" type="java.util.List">
                    <hint>A list of documents to be Compressed</hint>
                </input-parameter>
                <input-parameter name="zipFileName" title="Result File Name" type="java.lang.String">
                    <hint>The name of compressed file (optional)</hint>
                </input-parameter>

                <output-parameter name="zippedDoc" title="Compressed Zip file" type="com.adobe.idp.Document">
                    <hint>Compressed ZIP File</hint>
                </output-parameter>
            </operation>
             </operations>
      </service>
   </services>
</component>
```

## Creazione pacchetti e distribuzione del componente {#packaging-deploying-component}

1. Compila il progetto Java™ e crea un file .JAR.
1. Distribuisci il componente (file .JAR) in AEM Forms sul runtime JEE tramite Workbench.
1. Avvia il servizio da Workbench (vedi la figura seguente).

![Progettazione processo](assets/process-design.jpg)

## Utilizzo del servizio ZIP nei flussi di lavoro {#using-zip-service-in-workflows}

L’operazione UnzipDocument del servizio personalizzato può ora accettare una variabile di documento come input e restituire un elenco di variabili di documento come output.

![Decomprimi documento](assets/unzip-doc.jpg)

Analogamente, l’operazione ZipDocuments del componente personalizzato può accettare come input un elenco di documenti, comprimerli come file zip e restituire il documento compresso.

![Documento ZIP](assets/zip-doc.jpg)

La seguente orchestrazione del flusso di lavoro mostra come decomprimere il file ZIP specificato, comprimerlo nuovamente in un altro file ZIP e restituisce l’output (vedi la figura seguente).

![Decomprimi flusso di lavoro ZIP](assets/unzip-zip-process.jpg)

## Alcuni casi d’uso aziendali {#business-use-cases}

Puoi utilizzare questo servizio ZIP per i seguenti casi d’uso:

* Trova tutti i file in una determinata cartella e restituisce i file come documento compresso.

* Fornisci un file ZIP contenente diversi documenti PDF che possono essere estesi in lettura dopo averli decompressi. Questo richiede il modulo AEM Forms on JEE Reader Extensions.

* Fornisci un file ZIP contenente un tipo di documento eterogeneo che può essere decompresso e convertito come documento PDF utilizzando il servizio Genera PDF.

* La policy protegge un elenco di documenti e lo restituisce come file ZIP.

* Consente agli utenti di scaricare tutti gli allegati di un&#39;istanza del processo come un singolo file ZIP.
