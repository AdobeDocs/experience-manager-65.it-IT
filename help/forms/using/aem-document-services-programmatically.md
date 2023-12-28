---
title: Utilizzo dei servizi documentali AEM a livello di programmazione
description: Scopri come utilizzare le API di Document Services per apporre una firma digitale, crittografare e generare documenti PDF.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
feature: Document Services
source-git-commit: 744cfcee691ea71f33cd56509f65d4f640d4c6e3
workflow-type: tm+mt
source-wordcount: '6348'
ht-degree: 1%

---

# Utilizzo dei servizi documentali AEM a livello di programmazione  {#using-aem-document-services-programmatically}

Esempi ed esempi in questo documento sono utili per comprendere e utilizzare i servizi documentali AEM in un ambiente AEM Forms su OSGi. Per esempi ed esempi sull’ambiente AEM Forms su JEE, consulta

* [Guida introduttiva all’API Java di Signature Service](https://experienceleague.adobe.com/docs/experience-manager-65/forms/developer-reference/programming-aem-forms-jee/java-api-quick-start-code-examples/signature-service-java-api-quick.html?#programming-aem-forms-jee)

* [Servizio di crittografia API Java - Guida introduttiva](https://experienceleague.adobe.com/docs/experience-manager-65/forms/developer-reference/programming-aem-forms-jee/java-api-quick-start-code-examples/encryption-service-java-api-quick.html?#developer-reference)

* [Guida introduttiva al servizio Acrobat Reader extensions API Java](https://experienceleague.adobe.com/docs/experience-manager-65/forms/developer-reference/programming-aem-forms-jee/java-api-quick-start-code-examples/acrobat-reader-dc-extensions-service.html?#developer-reference)

## Prerequisito {#prerequisite}

* Prima di utilizzare le API del servizio DocAssurance, [configurare il servizio DocAssurance](/help/forms/using/install-configure-document-services.md).

* Scarica e configura [AEM Forms Client SDK](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) con te progetto AEM maven. Le classi client necessarie per creare progetti Maven utilizzando i servizi documentali AEM sono disponibili nel [AEM Forms Client SDK](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)

* Scopri [come creare il progetto AEM utilizzando Maven](/help/sites-developing/ht-projects-maven.md)

## Servizio DocAssurance {#docassurance-service}

Il servizio DocAssurance include i seguenti servizi:

* Servizio di firma
* Servizio Encryption
* Servizio Estensione Reader

È possibile eseguire le operazioni seguenti utilizzando il servizio DocAssurance:

* [Aggiungi firma invisibile](/help/forms/using/aem-document-services-programmatically.md#p-adding-an-invisible-signature-field-p)

* [Aggiungi campo firma](/help/forms/using/aem-document-services-programmatically.md#p-adding-a-signature-field-nbsp-p)
* [Applica la marca temporale al documento](/help/forms/using/aem-document-services-programmatically.md#apply-document-timestamp)

* [Ottieni firma](/help/forms/using/aem-document-services-programmatically.md#p-getting-signature-p)
* [Ottieni elenco campi firma](/help/forms/using/aem-document-services-programmatically.md#p-getting-signature-field-list-nbsp-p)
* [Modifica campi firma](/help/forms/using/aem-document-services-programmatically.md#p-modifying-signature-fields-nbsp-p)

* [Proteggi documento](/help/forms/using/aem-document-services-programmatically.md#p-securing-documents-p)

* [Ottieni diritti di utilizzo credenziali](/help/forms/using/aem-document-services-programmatically.md#p-getting-credential-usage-rights-p)

* [Ottieni diritti di utilizzo documento](/help/forms/using/aem-document-services-programmatically.md#p-getting-document-usage-rights-p)

* [Rimuovi diritti di utilizzo](/help/forms/using/aem-document-services-programmatically.md#p-removing-usage-rights-p)
* [Verifica firme digitali](/help/forms/using/aem-document-services-programmatically.md#p-verifying-digital-signatures-p)
* [Verifica più firme digitali](/help/forms/using/aem-document-services-programmatically.md#p-verifying-multiple-digital-signatures-p)
* [Rimuovi firme digitali](/help/forms/using/aem-document-services-programmatically.md#p-removing-digital-signatures-p)

* [Ottieni campo firma di certificazione](/help/forms/using/aem-document-services-programmatically.md#p-getting-certifying-signature-field-p)
* [Ottieni tipo di crittografia PDF](/help/forms/using/aem-document-services-programmatically.md#p-getting-pdf-encryption-type-p)
* [Rimuovi crittografia password](/help/forms/using/aem-document-services-programmatically.md#p-removing-password-encryption-from-pdf-p)

* [Rimuovi crittografia certificato](/help/forms/using/aem-document-services-programmatically.md#p-removing-certificate-encryption-p)

>[!NOTE]
>
>Tutti questi servizi utilizzano l’oggetto Document come parametro di input per il quale è possibile trovare Javadoc nell’URL [https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/index.html](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/index.html)

### Aggiunta di un campo di firma invisibile {#adding-an-invisible-signature-field}

Le firme digitali vengono visualizzate nei campi firma, ovvero nei campi modulo che contengono una rappresentazione grafica della firma. I campi di firma possono essere visibili o invisibili. I firmatari possono utilizzare un campo di firma preesistente oppure è possibile aggiungere un campo di firma a livello di programmazione. In entrambi i casi, il campo firma deve esistere prima che un documento PDF possa essere firmato. Puoi aggiungere un campo di firma a livello di programmazione utilizzando l’API Java di Signature Service o l’API del servizio web di firma. È possibile aggiungere più campi firma a un documento PDF. Tuttavia, ogni nome del campo firma deve essere univoco.

**Sintassi**: `addInvisibleSignatureField(Document inDoc, String signatureFieldName, FieldMDPOptionSpec fieldMDPOptionsSpec, PDFSeedValueOptionSpec seedValueOptionsSpec, UnlockOptions unlockOptions)`

**Parametri di input**

<table>
 <tbody>
  <tr>
   <th>Parametri</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td><code>inDoc</code></td>
   <td>Oggetto documento contenente PDF.<br /> </td>
  </tr>
  <tr>
   <td><code>signatureFieldName</code><br /> </td>
   <td>Nome del campo firma. Questo parametro è obbligatorio e non può avere un valore null.<br /> </td>
  </tr>
  <tr>
   <td><code>fieldMDPOptionsSpec</code></td>
   <td>A <code>FieldMDPOptionSpec</code> oggetto che specifica i campi del documento PDF bloccati dopo la firma del campo firma. Questo parametro è facoltativo e può accettare un valore nullo.</td>
  </tr>
  <tr>
   <td><code>seedValueOptionsSpec</code></td>
   <td>A <code>SeedValueOptions</code> oggetto che specifica i vari valori iniziali per il campo. T Questo parametro è facoltativo e può accettare un valore null.<span class="acrolinxCursorMarker"></span></td>
  </tr>
  <tr>
   <td><code>unlockOptions</code></td>
   <td>Include i parametri necessari per sbloccare un file crittografato. Questo parametro è necessario solo per i file crittografati.</td>
  </tr>
 </tbody>
</table>

Esempio di codice Java che aggiunge un campo di firma invisibile a un documento PDF.

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * ___________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.io.IOException;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceException;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.PositionRectangle;
import com.adobe.fd.signatures.client.types.exceptions.DuplicateSignatureFieldException;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.client.types.exceptions.PDFOperationException;
import com.adobe.fd.signatures.client.types.exceptions.PermissionsException;
import com.adobe.fd.signatures.client.types.exceptions.SignaturesBaseException;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;

/**
 * Digital signatures appear in signature fields, which are form fields that contain a graphic representation of the signature.
 * Signature fields can be visible or invisible. Signers can use a pre existing signature field, or a signature field can be
 * programmatically added. In either case, the signature field must exist before a PDF document can be signed.
 * You can programmatically add a signature field by using the Signature service Java API or Signature web service API.
 * You can add more than one signature field to a PDF document; however, each signature field name must be unique.
 *
 * The following Java code example adds an invisible signature field named SignatureField1 to a PDF document.
 */

@Component
@Service(value=AddInvisibleSignatureField.class)
public class AddInvisibleSignatureField {

 @Reference
 private DocAssuranceService docAssuranceService;

 /**
  *
  * @param inputFile - path to an pdf document stored at disk
  * @param outputFile - path where the output file has to be saved
  * @throws SignaturesBaseException
  * @throws DuplicateSignatureFieldException
  * @throws PermissionsException
  * @throws PDFOperationException
  * @throws InvalidArgumentException
  * @throws DocAssuranceException
  *
  */
 public void addInvisibleSignatureField(String inputFile, String outputFile) throws InvalidArgumentException, PDFOperationException, PermissionsException, DuplicateSignatureFieldException, SignaturesBaseException, DocAssuranceException {

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  File outFile = new File(outputFile);
  Document outDoc = null;

        //Specify the name of the signature field
        String fieldName = "SignatureField1";

        //Create a  PositionRectangle object that specifies
        //the signature fields location
        PositionRectangle post = new  PositionRectangle(193,47,133,12);

        //Specify the page number that will contain the signature field
        java.lang.Integer pageNum = new java.lang.Integer(1);

        //Add a signature field to the PDF document
        try {
   outDoc = docAssuranceService.addInvisibleSignatureField(
       inDoc,
       fieldName,
       null,
       null,
       null);
  } catch (Exception e1) {
   // TODO Auto-generated catch block
   e1.printStackTrace();
  } // for an encrypted PDF input, pass unlock options

        //save the outDoc
        try {
   outDoc.copyToFile(outFile);
  } catch (IOException e) {
   // TODO Auto-generated catch block
   e.printStackTrace();
  }
 }

 /**
  *
  * UnlockOptions to be passed to addSignatureField() API to add a signature field in an encrypted pdf document.
  */
 private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }
}
```

Puoi anche utilizzare [CAdES](https://en.wikipedia.org/wiki/CAdES_%28computing%29)specifica per la firma dei documenti. Utilizza il seguente codice di esempio per impostare il formato della firma su [CAdES](https://en.wikipedia.org/wiki/CAdES_%28computing%29)

```java
SigningFormat signingFormat = SigningFormat.CAdES;
sigAppearence.setSigningFormat(signingFormat);
signOptions.setSigAppearence(sigAppearence);
```

### Aggiunta di un campo firma  {#adding-a-signature-field-nbsp}

Puoi aggiungere un campo di firma a livello di programmazione utilizzando l’API Java di Signature Service o l’API del servizio web di firma. È possibile aggiungere più campi firma a un documento PDF. Tuttavia, ogni nome del campo firma deve essere univoco.

**Sintassi**:

```java
public Document addSignatureField(Document inDoc,
 String signatureFieldName,
 Integer pageNo,
 PositionRectangle positionRectangle,
 FieldMDPOptionSpec fieldMDPOptionsSpec,
 PDFSeedValueOptionSpec seedValueOptionsSpec, UnlockOptions unlockOptions)
```

**Parametri di input**

<table>
 <tbody>
  <tr>
   <th>Parametri</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td><code>inDoc</code></td>
   <td>Oggetto documento contenente PDF</td>
  </tr>
  <tr>
   <td><code>signatureFieldName</code></td>
   <td>Nome del campo firma. Questo parametro è obbligatorio e non può accettare un valore null.</td>
  </tr>
  <tr>
   <td><code>pageNumber</code></td>
   <td>Numero di pagina in cui viene aggiunto il campo firma. I valori validi sono compresi tra 1 e il numero di pagine contenute nel documento. Questo parametro è obbligatorio e non può accettare un valore null.<br /> </td>
  </tr>
  <tr>
   <td><code>positionRectangle</code></td>
   <td>A <code>PositionRectangle object</code> che specifica la posizione del campo firma. Questo parametro è obbligatorio e non può accettare un valore null. Se il rettangolo specificato non si trova almeno parzialmente nella casella di ritaglio della pagina specificata, <code>InvalidArgumentException</code> viene lanciato. Inoltre, né l'altezza né la larghezza del rettangolo specificato possono essere 0 o negative. Le coordinate X o Y in basso a sinistra possono essere 0 o maggiori ma non negative e sono relative alla casella di ritaglio della pagina.</td>
  </tr>
  <tr>
   <td><code>fieldMDPOptionsSpec</code></td>
   <td>A <code>FieldMDPOptionSpec</code> oggetto che specifica i campi del documento PDF bloccati dopo la firma del campo firma. Questo è un parametro facoltativo e può essere nullo.</td>
  </tr>
  <tr>
   <td><code>seedValueOptionsSpec</code></td>
   <td>A <code>SeedValueOptions</code> oggetto che specifica i vari valori iniziali per il campo. Questo è un parametro facoltativo e può essere nullo.</td>
  </tr>
  <tr>
   <td><code>unlockOptions</code></td>
   <td>Include i parametri necessari per sbloccare un file crittografato. Questo parametro è necessario solo per i file crittografati.</td>
  </tr>
 </tbody>
</table>

Di seguito è riportato un codice Java di esempio che aggiunge un campo di firma a un documento di PDF.

```java
/*************************************************************************
 *
-------------------------------------------------------------
*ADOBE SYSTEMS INCORPORATED
*Copyright 2014 Adobe Systems Incorporated
*All Rights Reserved.

*NOTICE:  Adobe permits you to use, modify, and distribute this file in accordance with the
*terms of the Adobe license agreement accompanying it.  If you have received this file from a
*source other than Adobe, then your use, modification, or distribution of it requires the prior
*written permission of Adobe.
-------------------------------------------------------------------------------------------------

 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.io.IOException;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceException;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.PositionRectangle;
import com.adobe.fd.signatures.client.types.exceptions.DuplicateSignatureFieldException;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.client.types.exceptions.PDFOperationException;
import com.adobe.fd.signatures.client.types.exceptions.PermissionsException;
import com.adobe.fd.signatures.client.types.exceptions.SignaturesBaseException;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;

/**
 * Digital signatures appear in signature fields, which are form fields that contain a graphic representation of the signature.
 * Signature fields can be visible or invisible. Signers can use a pre existing signature field, or a signature field can be
 * programmatically added. In either case, the signature field must exist before a PDF document can be signed.
 * You can programmatically add a signature field by using the Signature service Java API or Signature web service API.
 * You can add more than one signature field to a PDF document; however, each signature field name must be unique.
 *
 * The following Java code example adds a signature field named SignatureField1 to a PDF document.
 */

@Component
@Service(value=AddSignatureField.class)
public class AddSignatureField {

 @Reference
 private DocAssuranceService docAssuranceService;

 /**
  *
  * @param inputFile - path to an pdf document stored at disk
  * @param outputFile - path where the output file has to be saved
  * @throws SignaturesBaseException
  * @throws DuplicateSignatureFieldException
  * @throws PermissionsException
  * @throws PDFOperationException
  * @throws InvalidArgumentException
  * @throws DocAssuranceException
  *
  */
 public void addSignatureField(String inputFile, String outputFile) throws InvalidArgumentException, PDFOperationException, PermissionsException, DuplicateSignatureFieldException, SignaturesBaseException, DocAssuranceException {

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  File outFile = new File(outputFile);
  Document outDoc = null;

        //Specify the name of the signature field
        String fieldName = "SignatureField1";

        //Create a  PositionRectangle object that specifies
        //the signature fields location
        PositionRectangle post = new  PositionRectangle(193,47,133,12);

        //Specify the page number that will contain the signature field
        java.lang.Integer pageNum = new java.lang.Integer(1);

        //Add a signature field to the PDF document
        try {
   outDoc = docAssuranceService.addSignatureField(
       inDoc,
       fieldName,
       pageNum,
       post,
       null,
       null,
       null);
  } catch (Exception e1) {
   // TODO Auto-generated catch block
   e1.printStackTrace();
  } // for an encrypted PDF input, pass unlock options

        //save the outDoc
        try {
   outDoc.copyToFile(outFile);
  } catch (IOException e) {
   // TODO Auto-generated catch block
   e.printStackTrace();
  }
 }

 /**
  *
  * UnlockOptions to be passed to addSignatureField() API to add a signature field in an encrypted pdf document.
  */
 private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }
}
```

### Applica la marca temporale al documento {#apply-document-timestamp}

È possibile assegnare a un documento una marca temporale a livello di programmazione in base a [PAdES 4](https://en.wikipedia.org/wiki/PAdES) specifiche. Puoi anche utilizzare [CAdES](https://en.wikipedia.org/wiki/CAdES_%28computing%29) specifica per i documenti relativi alla transazione.

**Sintassi**: `applyDocumentTimeStamp(Document doc, VerificationTime verificationTime, ValidationPreferences dssPrefs, ResourceResolver resourceResolver, UnlockOptions unlockOptions)`

**Parametri di input**

<table>
 <tbody>
  <tr>
   <th>Parametri</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td><code>doc</code><br /> </td>
   <td>Oggetto documento contenente PDF.<br /> </td>
  </tr>
  <tr>
   <td><code>VerificationTime</code></td>
   <td>L’ora in cui la firma deve essere convalidata<br /> </td>
  </tr>
  <tr>
   <td><code>ValidationPreferences</code> </td>
   <td>Preferenze per controllare le configurazioni di convalida.</td>
  </tr>
  <tr>
   <td><code>ResourceResolver</code></td>
   <td>Risolutore risorse all'archivio attendibilità granite.</td>
  </tr>
  <tr>
   <td><code>UnlockOptions</code></td>
   <td>Include i parametri necessari per sbloccare un file crittografato. Questa opzione è necessaria solo se il file è crittografato.</td>
  </tr>
 </tbody>
</table>

Nei seguenti esempi di codice viene aggiunto un timestamp a un documento in base a [PAdES 4](https://en.wikipedia.org/wiki/PAdES).

```java
package com.adobe.signatures.test;

import java.io.File;

import javax.jcr.Session;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.jcr.api.SlingRepository;
import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.VerificationTime;
import com.adobe.fd.signatures.pdf.inputs.ValidationPreferences;
import com.adobe.fd.signatures.pdf.inputs.ValidationPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.common.RevocationCheckStyle;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.OCSPPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.TSPPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.TSPPreferencesImpl;

 @Component
 @Service(value=Test.class)
 public class Test {

     @Reference
     private DocAssuranceService docAssuranceService;

     @Reference
     private SlingRepository slingRepository;

     @Reference
     private JcrResourceResolverFactory jcrResourceResolverFactory ;

     /**
      *
      * @param inputFile - path to the pdf document stored at disk
      * @param outputFile - path to the pdf document where the output needs to be stored
      * @throws Exception
      */
     public void TimeStamp(String inputFile, String outputFile) throws Exception{

         File inFile = new File(inputFile);
         Document inDoc = new Document(inFile);

         File outFile = new File(outputFile);
         Document outDoc = null;

         Session adminSession = null;
         ResourceResolver resourceResolver = null;
         try {

              /** resourceResolver with admin privileges to be passed to SignatureServiceAPI and Reader Extensions
              the resource resolver for signature options has to be corresponding to the user who has the signing certificate in his granite key store
              the resource resolver for signature options has to be corresponding to the user who has the credential for reader extension in his granite key store
              here we are using the same resource resolver
              */
              adminSession = slingRepository.loginAdministrative(null);
              resourceResolver = jcrResourceResolverFactory.getResourceResolver(adminSession);

              VerificationTime verificationTime = getVerificationTimeForPades();
              ValidationPreferences dssPrefs = getValidationPreferences();

              //retrieve specifications for each of the services, you may pass null if you don't want to use that service
              //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
               outDoc = docAssuranceService.applyDocumentTimeStamp(inDoc, verificationTime, dssPrefs, resourceResolver, null);
         }
         finally{
             /**
              * always close the PDFDocument object after your processing is done.
              */
             if(inDoc != null){
                 inDoc.close();
             }
             if(adminSession != null && adminSession.isLive()){
                 if(resourceResolver != null){
                     resourceResolver.close();
                 }
                 adminSession.logout();
             }
         }

         outDoc.copyToFile(outFile);

     }

  public  VerificationTime getVerificationTimeForPades(){

         return VerificationTime.SECURE_TIME_ELSE_CURRENT_TIME;

     }

 /**
       * sets ValidationPreferences
       */
      private static ValidationPreferences getValidationPreferences(){

         ValidationPreferencesImpl prefs = new ValidationPreferencesImpl();
         prefs.setPKIPreferences(getPKIPreferences());

         //set the unlock options for processing an encrypted pdf document, do not set if the input doc is unprotected

         return prefs;

     }

   /**
       * sets PKIPreferences
       */
     private static PKIPreferences getPKIPreferences(){
         PKIPreferences pkiPref = new PKIPreferencesImpl();
         pkiPref.setCRLPreferences(getCRLPreferences());
         pkiPref.setPathPreferences(getPathValidationPreferences());
         pkiPref.setOCSPPreferences(getOCSPPref());
         pkiPref.setTSPPreferences(getTspPref());
         return pkiPref;
     }

   /**
      * sets CRL Preferences
      */
     private static CRLPreferences getCRLPreferences(){

         CRLPreferencesImpl crlPrefs = new CRLPreferencesImpl();
         crlPrefs.setRevocationCheck(RevocationCheckStyle.BestEffort);
         crlPrefs.setGoOnline(true);
         return crlPrefs;
     }

     /**
      *
      * sets PathValidationPreferences
      */
     private static PathValidationPreferences getPathValidationPreferences(){
         PathValidationPreferencesImpl pathPref = new PathValidationPreferencesImpl();
         pathPref.setDoValidation(true);
         return pathPref;

     }

   public static TSPPreferences getTspPref(){
   TSPPreferencesImpl tspPrefs=new TSPPreferencesImpl();
   char pass[]=new char[9];

   tspPrefs.setTspServerURL("TSPPrefs_ServerURL");
   tspPrefs.setUsername("TSPPrefs_Username");
   tspPrefs.setPassword(pass);
   tspPrefs.setSize(10240);
   return tspPrefs;
   }

     private static OCSPPreferencesImpl getOCSPPref(){
         OCSPPreferencesImpl ocsp = new OCSPPreferencesImpl();
         ocsp.setRevocationCheck(RevocationCheckStyle.BestEffort);
         return ocsp;
     }

}
```

### Recupero firma {#getting-signature}

È possibile recuperare i nomi di tutti i campi firma presenti in un documento PDF che si desidera firmare o certificare. Se non si è certi dei nomi dei campi di firma in un documento PDF o per verificarli, recuperare i nomi a livello di programmazione. Il servizio di firma restituisce il nome completo del campo della firma, ad esempio `form1[0].grantApplication[0].page1[0].SignatureField1[0]`.

**Sintassi**: `getSignature(Document doc, String signatureFieldName, UnlockOptions unlockOptions)`

**Parametri di input**

<table>
 <tbody>
  <tr>
   <th>Parametri</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td><code>doc</code><br /> </td>
   <td>Oggetto documento contenente PDF.<br /> </td>
  </tr>
  <tr>
   <td><code>signatureFieldName</code></td>
   <td>Nome del campo firma che contiene una firma. Specificare il nome completo del campo firma. Quando si utilizza un documento PDF basato su un modulo XFA, è possibile utilizzare il nome parziale del campo firma. Ad esempio: <code>form1[0].#subform[1].SignatureField3[3]</code> può essere specificato come <code>SignatureField3[3]</code>.</td>
  </tr>
  <tr>
   <td><code>UnlockOptions</code></td>
   <td>Include i parametri necessari per sbloccare un file crittografato. Questa opzione è necessaria solo se il file è crittografato.</td>
  </tr>
 </tbody>
</table>

Esempio Nell&#39;esempio di codice Java riportato di seguito vengono recuperate le informazioni sulla firma per il campo della firma specificato in un documento di PDF.

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * ___________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.util.Iterator;
import java.util.List;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.PDFSignatureField;
import com.adobe.fd.signatures.client.types.exceptions.DuplicateSignatureFieldException;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.client.types.exceptions.PDFOperationException;
import com.adobe.fd.signatures.client.types.exceptions.PermissionsException;
import com.adobe.fd.signatures.client.types.exceptions.SignaturesBaseException;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;
import com.adobe.fd.signatures.client.types.PDFSignature;

/**
 * You can retrieve the names of all signature fields that are in a PDF document that you want to sign or certify.
 * If you are unsure of the signature field names that are in a PDF document or you want to verify the names, you can
 * programmatically retrieve them. The Signature service returns the fully qualified name of the signature field, such as
 * form1[0].grantApplication[0].page1[0].SignatureField1[0].
 *
 * The following Java code example retrieves the Signature Info for the given signature field in a PDF document.
 */

@Component
@Service(value=GetSignature.class)
public class GetSignature {

 @Reference
 private DocAssuranceService docAssuranceService;

 /**
  *
  * @param inputFile - path to the pdf document stored at disk
  * @throws SignaturesBaseException
  * @throws DuplicateSignatureFieldException
  * @throws PermissionsException
  * @throws PDFOperationException
  * @throws InvalidArgumentException
  *
  */
 public void GetSignature(String inputFile) throws Exception {

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  //Retrieve signature data for a given signature field.
  //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
        PDFSignature pdfSignature = docAssuranceService.getSignature(inDoc,"fieldName",null);

   }

  /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }
}
```

### Recupero elenco campi firma  {#getting-signature-field-list-nbsp}

È possibile recuperare i nomi di tutti i campi firma presenti in un documento PDF che si desidera firmare o certificare. Se non si è sicuri dei nomi dei campi di firma in un documento PDF, è possibile recuperarli e verificarli a livello di programmazione. Il servizio di firma restituisce il nome completo del campo della firma, ad esempio `form1[0].grantApplication[0].page1[0].SignatureField1[0]`.

**Sintassi**: `public List <PDFSignatureField> getSignatureFieldList (Document inDoc, UnlockOptions unlockOptions)`

**Parametri di input**

| Parametri | Descrizione |
|---|---|
| `inDoc` | Oggetto documento contenente PDF |
| `unlockOptions` | Include i parametri necessari per sbloccare un file crittografato. Questa opzione è necessaria solo se il file è crittografato. |

Esempio Nell&#39;esempio di codice Java riportato di seguito vengono recuperati i nomi dei campi di firma in un documento di PDF.

```java
/*************************************************************************
 *
 *
-------------------------------------------------------------
*ADOBE SYSTEMS INCORPORATED
*Copyright 2014 Adobe Systems Incorporated
*All Rights Reserved.

*NOTICE:  Adobe permits you to use, modify, and distribute this file in accordance with the
*terms of the Adobe license agreement accompanying it.  If you have received this file from a
*source other than Adobe, then your use, modification, or distribution of it requires the prior
*written permission of Adobe.
-------------------------------------------------------------------------------------------------
**************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.util.Iterator;
import java.util.List;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.PDFSignatureField;
import com.adobe.fd.signatures.client.types.exceptions.DuplicateSignatureFieldException;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.client.types.exceptions.PDFOperationException;
import com.adobe.fd.signatures.client.types.exceptions.PermissionsException;
import com.adobe.fd.signatures.client.types.exceptions.SignaturesBaseException;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;

/**
 * You can retrieve the names of all signature fields that are in a PDF document that you want to sign or certify.
 * If you are unsure of the signature field names that are in a PDF document or you want to verify the names, you can
 * programmatically retrieve them. The Signature service returns the fully qualified name of the signature field, such as
 * form1[0].grantApplication[0].page1[0].SignatureField1[0].
 *
 * The following Java code example retrieves the names of signature fields in a PDF document.
 */

@Component
@Service(value=GetSignatureFields.class)
public class GetSignatureFields {

 @Reference
 private DocAssuranceService docAssuranceService;

 /**
  *
  * @param inputFile - path to the pdf document stored at disk
  * @throws SignaturesBaseException
  * @throws DuplicateSignatureFieldException
  * @throws PermissionsException
  * @throws PDFOperationException
  * @throws InvalidArgumentException
  *
  */
 public void getSignatureFields(String inputFile) throws Exception {

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  //Retrieve the name of the document's signature fields
  //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
        List fieldNames = docAssuranceService.getSignatureFieldList(inDoc,null);

        //Obtain the name of each signature field by iterating through the
        //List object
        Iterator iter = fieldNames.iterator();
        int i = 0 ;
        String fieldName="";
        while (iter.hasNext()) {
            PDFSignatureField signatureField = (PDFSignatureField)iter.next();
            fieldName = signatureField.getName();
            System.out.println("The name of the signature field is " +fieldName);
            i++;
        }
   }

  /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }
}
```

### Modifica dei campi della firma  {#modifying-signature-fields-nbsp}

È possibile modificare i campi della firma presenti in un documento PDF. La modifica di un campo di firma comporta la modifica dei valori del dizionario del blocco del campo di firma o dei valori del dizionario dei valori iniziali.

Un dizionario di blocco dei campi specifica un elenco di campi che vengono bloccati quando il campo firma è firmato. Un campo bloccato impedisce agli utenti di modificare il campo. Un dizionario dei valori iniziali contiene informazioni vincolanti utilizzate al momento dell&#39;applicazione della firma. È ad esempio possibile modificare le autorizzazioni che controllano le azioni che possono essere eseguite senza invalidare una firma.

Modificando un campo di firma esistente, è possibile modificare il documento PDF in modo che rifletta i requisiti aziendali in continua evoluzione. Ad esempio, un nuovo requisito aziendale richiede il blocco di tutti i campi del documento dopo la firma del documento.

**Sintassi**: `public Document modifySignatureField(Document inDoc, String signatureFieldName, PDFSignatureFieldProperties pdfSignatureFieldProperties, UnlockOptions unlockOptions)`

**Parametri di input**

<table>
 <tbody>
  <tr>
   <th>Parametri</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td><code>inDoc</code></td>
   <td>Oggetto documento contenente PDF</td>
  </tr>
  <tr>
   <td><code>signatureFieldName</code></td>
   <td>Nome del campo firma. Questo parametro è obbligatorio e non può accettare un valore null.<br /> </td>
  </tr>
  <tr>
   <td><code>pdfSignatureFieldProperties</code></td>
   <td>Oggetto che specifica informazioni sulla <code>PDFSeedValueOptionSpec</code> e <code>FieldMDPOptionSpec</code> valori del campo firma.</td>
  </tr>
  <tr>
   <td><code>unlockOptions</code></td>
   <td>Include i parametri necessari per sbloccare un file crittografato. Questa opzione è necessaria solo se il file è crittografato.</td>
  </tr>
 </tbody>
</table>

Nell&#39;esempio di codice Java seguente viene modificato un campo di firma bloccando tutti i campi del modulo quando viene applicata una firma al campo di firma.

```java
/*************************************************************************
 *

-------------------------------------------------------------
*ADOBE SYSTEMS INCORPORATED
*Copyright 2014 Adobe Systems Incorporated
*All Rights Reserved.

*NOTICE:  Adobe permits you to use, modify, and distribute this file in accordance with the
*terms of the Adobe license agreement accompanying it.  If you have received this file from a
*source other than Adobe, then your use, modification, or distribution of it requires the prior
*written permission of Adobe.
-------------------------------------------------------------------------------------------------

 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceException;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.FieldMDPAction;
import com.adobe.fd.signatures.client.types.FieldMDPOptionSpec;
import com.adobe.fd.signatures.client.types.MDPPermissions;
import com.adobe.fd.signatures.client.types.PDFSeedValueOptionSpec;
import com.adobe.fd.signatures.client.types.PDFSignatureFieldProperties;
import com.adobe.fd.signatures.client.types.PositionRectangle;
import com.adobe.fd.signatures.client.types.exceptions.DuplicateSignatureFieldException;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.client.types.exceptions.MissingSignatureFieldException;
import com.adobe.fd.signatures.client.types.exceptions.PDFOperationException;
import com.adobe.fd.signatures.client.types.exceptions.PermissionsException;
import com.adobe.fd.signatures.client.types.exceptions.SignatureFieldSignedException;
import com.adobe.fd.signatures.client.types.exceptions.SignaturesBaseException;
import com.adobe.fd.signatures.client.types.exceptions.SignaturesOtherException;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;

/**
 * You can modify signature fields that are in a PDF document by using the Java API and web service API. Modifying a signature field involves
 * manipulating its signature field lock dictionary values or seed value dictionary values.
 * A field lock dictionary specifies a list of fields that are locked when the signature field is signed. A locked field prevents users from making
 * changes to the field. A seed value dictionary contains constraining information that is used at the time the signature is applied.
 * For example, you can change permissions that control the actions that can occur without invalidating a signature.
 * By modifying an existing signature field, you can change the PDF document to reflect changing business requirements. For example,
 * a new business requirement may require locking all document fields after the document is signed.
 * This section explains how to modify a signature field by amending both field lock dictionary and seed value dictionary values.
 * Changes made to the signature field lock dictionary result in all fields in the PDF document being locked when a signature field is signed.
 * Changes made to the seed value dictionary prohibit specific types of changes to the document.
 *
 * The following Java code example modifies a signature field named SignatureField1 by locking all fields in the form when a signature is applied to the signature field and ensuring that no changes are allowed.
 * After the Signature service returns the PDF document that contains the modified signature field
 */

@Component
@Service(value=ModifySignatureField.class)
public class ModifySignatureField {

 @Reference
 private DocAssuranceService docAssuranceService;

 /**
  *
  * @param inputFile - path to the pdf document stored at disk
  * @param outFile - path where the output file has to be saved
  *
  *
  */
 public void modifySignatureField(String inputFile, String outFile) throws Exception {

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  //Specify the name of the signature field
        String fieldName = "SignatureField1";

        //Create a PDFSignatureFieldProperties
        PDFSignatureFieldProperties fieldProperties = new PDFSignatureFieldProperties();

         //Create a PDFSeedValueOptionSpec object that stores
         //seed value dictionary information.
         PDFSeedValueOptionSpec seedOptionsSpec = new PDFSeedValueOptionSpec();

         //Disallow changes to the PDF document. Any change to the document invalidates
         //the signature
         seedOptionsSpec.setMdpValue(MDPPermissions.NoChanges);

         //Create a FieldMDPOptionSpec object that stores
         //signature field lock dictionary information.
         FieldMDPOptionSpec fieldMDPOptionsSpec = new FieldMDPOptionSpec();

         //Lock all fields in the PDF document
         fieldMDPOptionsSpec.setAction(FieldMDPAction.ALL);

         //Set dictionary information
         fieldProperties.setSeedValue(seedOptionsSpec);
         fieldProperties.setFieldMDP(fieldMDPOptionsSpec);

         //Modify the signature field
         //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
         Document modSignatureField =  docAssuranceService.modifySignatureField(inDoc,fieldName,fieldProperties,null);

        //save the modSignatureField
         modSignatureField.copyToFile(new File(outFile));
 }

  /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }
}
```

### Certificazione dei documenti di PDF  {#certifying-pdf-documents-nbsp}

È possibile proteggere un documento PDF certificandolo con un tipo particolare di firma, denominata firma certificata. Una firma certificata si distingue da una firma digitale nei seguenti modi:

* Deve essere la prima firma applicata al documento PDF. In altre parole, quando viene applicata la firma certificata, gli altri campi firma del documento devono essere non firmati. In un documento PDF è consentita una sola firma certificata. Per firmare e certificare un documento PDF, certificalo prima di firmarlo. Dopo aver certificato un documento PDF, è possibile firmare digitalmente ulteriori campi di firma.
* L&#39;autore o l&#39;originatore del documento può specificare che il documento può essere modificato in alcuni modi senza invalidare la firma certificata. Ad esempio, il documento può consentire la compilazione di moduli o la creazione di commenti. Se l’autore specifica che una determinata modifica non è consentita, Acrobat impedisce agli utenti di modificare il documento in questo modo. Se vengono apportate tali modifiche, la firma certificata non è valida. Inoltre, Acrobat genera un avviso quando un utente apre il documento. Con le firme non certificate, le modifiche non vengono impedite e le normali operazioni di modifica non invalidano la firma originale.
* Al momento della firma, il documento viene analizzato per individuare tipi specifici di contenuto che potrebbero rendere ambiguo o fuorviante il contenuto di un documento. Ad esempio, un’annotazione potrebbe oscurare del testo su una pagina importante per comprendere cosa viene certificato. Su tale contenuto può essere fornita una spiegazione (attestazione legale).

**Sintassi**:

```java
secureDocument(Document inDoc, EncryptionOptions encryptionOptions,
 SignatureOptions signatureOptions, ReaderExtensionOptions readerExtensionOptions, UnlockOptions unlockOptions)
```

**Parametri di input**

<table>
 <tbody>
  <tr>
   <th>Parametri</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td><code>inDoc</code><br /> </td>
   <td>Documento input PDF documento<br /> </td>
  </tr>
  <tr>
   <td><code>encryptionOptions</code><br /> </td>
   <td>Include gli argomenti necessari per crittografare un documento PDF<br /> </td>
  </tr>
  <tr>
   <td><code>signatureOptions</code></td>
   <td>Include le opzioni necessarie per firmare/certificare un documento PDF</td>
  </tr>
  <tr>
   <td><code>readerExtensionOptions</code></td>
   <td>Include le opzioni necessarie per il Reader Estensione di un documento PDF</td>
  </tr>
  <tr>
   <td><code>unlockOptions</code></td>
   <td>Include i parametri necessari per sbloccare un file crittografato. Questa opzione è necessaria solo se il file è crittografato.<br /> </td>
  </tr>
 </tbody>
</table>

Il codice di esempio seguente certifica un documento PDF basato su un file PDF.

```java
/*************************************************************************

-------------------------------------------------------------
*ADOBE SYSTEMS INCORPORATED
*Copyright 2014 Adobe Systems Incorporated
*All Rights Reserved.

*NOTICE:  Adobe permits you to use, modify, and distribute this file in accordance with the
*terms of the Adobe license agreement accompanying it.  If you have received this file from a
*source other than Adobe, then your use, modification, or distribution of it requires the prior
*written permission of Adobe.
-------------------------------------------------------------------------------------------------

 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.io.IOException;

import javax.jcr.RepositoryException;
import javax.jcr.Session;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.jcr.api.SlingRepository;
import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceException;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.docassurance.client.api.DocAssuranceServiceOperationTypes;
import com.adobe.fd.docassurance.client.api.SignatureOptions;
import com.adobe.fd.signatures.client.types.MDPPermissions;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.pdf.inputs.CredentialContext;
import com.adobe.fd.signatures.pdf.inputs.DSSPreferences;
import com.adobe.fd.signatures.pdf.inputs.DSSPreferencesImpl;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions.PDFSignatureAppearanceType;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions.TextDirection;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;
import com.adobe.fd.signatures.pki.client.types.common.HashAlgorithm;
import com.adobe.fd.signatures.pki.client.types.common.RevocationCheckStyle;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.GeneralPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferencesImpl;

/**
 * You can secure a PDF document by certifying it with a particular type of signature called a certified signature.
 * A certified signature is distinguished from a digital signature in these ways:
 *
 * It must be the first signature applied to the PDF document; that is, at the time the certified signature is applied, any other signature fields in the document must be unsigned.
 * Only one certified signature is permitted in a PDF document. If you want to sign and certify a PDF document, you must certify it before signing it.
 * After you certify a PDF document, you can digitally sign additional signature fields.
 *
 * The author or originator of the document can specify that the document can be modified in certain ways without invalidating the certified signature. For example,
 * the document may permit filling in forms or commenting. If the author specifies that a certain modification is not permitted, Acrobat restricts users from modifying the document
 * in that way. If such modifications are made, such as by using another application, the certified signature is invalid and Acrobat issues a warning when a user opens the document.
 * (With non-certified signatures, modifications are not prevented, and normal editing operations do not invalidate the original signature.)
 *
 * At the time of signing, the document is scanned for specific types of content that could make the contents of a document ambiguous or misleading. For example, an annotation could
 * obscure some text on a page that is important for understanding what is being certified. An explanation (legal attestation) can be provided about such content.
 * You can programmatically certify PDF documents by using the Signature service Java API or the Signature web service API. When certifying a PDF document, you must reference a security
 * credential that exists in the Credential service.
 *
 * Note: When certifying and signing the same PDF document, if the certify signature is not trusted, a yellow triangle appears next to the first sign signature when you open the PDF document in Acrobat or Adobe Reader.
 * The certifying signature must be trusted to avoid this situation.
 *
 * The following Java code example certifies a PDF document that is based on a PDF file.
 *
 * PreRequisites - Digital certificate for certifying the document has to be uploaded on AEM Key Store.
 *
 */

@Component
@Service(value=Certify.class)
public class Certify {

 @Reference
 private DocAssuranceService docAssuranceService;

 @Reference
    private SlingRepository slingRepository;

 @Reference
    private JcrResourceResolverFactory jcrResourceResolverFactory ;

 /**
  *
  * @param inputFile - path to the pdf document stored at JCR node
  * @param outputFile - path to the pdf document where the output needs to be stored
  * @throws IOException
  * @throws RepositoryException
  * @throws InvalidArgumentException
  * @throws DocAssuranceException
  */
 public void certify(String inputFile, String outputFile) throws IOException, RepositoryException, InvalidArgumentException, DocAssuranceException{

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  File outFile = new File(outputFile);
  Document outDoc = null;

  Session adminSession = null;
        ResourceResolver resourceResolver = null;
        try {

          /** resourceResolver to be passed to SignatureServiceAPI and Reader Extensions
          the resource resolver for signature options has to be corresponding to the user who has the signing certificate in his granite key store
          the resource resolver for signature options has to be corresponding to the user who has the credential for reader extension in his granite key store
          here we are using the same resource resolver
          */
          adminSession = slingRepository.loginAdministrative(null);
             resourceResolver = jcrResourceResolverFactory.getResourceResolver(adminSession);

             //retrieve specifications for each of the services, you may pass null if you don't want to use that service
             //we are not extending the reader in this case, so passing null
             //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
    try {
    outDoc = docAssuranceService.secureDocument(inDoc, null, getCertificationOptions(resourceResolver), null,null);
   } catch (Exception e) {
    // TODO Auto-generated catch block
    e.printStackTrace();
   }

        }
        finally{
            /**
             * always close the PDFDocument object after your processing is done.
             */
            if(inDoc != null){
                inDoc.close();
            }
            if(adminSession != null && adminSession.isLive()){
                if(resourceResolver != null){
                    resourceResolver.close();
                }
                adminSession.logout();
            }
        }

        outDoc.copyToFile(outFile);

 }

 /**
  *
  * @param rr resource resolver corresponding to the user with the access to signing credential for the
  * given alias "allcertificatesanypolicytest11ee_new" in this case
  * @return SignatureOptions
  */
 private SignatureOptions getCertificationOptions(ResourceResolver rr){

  //create an instance of SignatureOptions
  SignatureOptions signatureOptions = SignatureOptions.getInstance();

  //set the operation you want to perform - SIGN/CERTIFY
  signatureOptions.setOperationType(DocAssuranceServiceOperationTypes.CERTIFY);

  //signature field to certify, pass null if invisible signature field
  String fieldName = "Signature1" ;

  //alias of the private credential uploaded on the Key Store
        String alias = "allcertificatesanypolicytest11ee_new";

        //Hash Algo to be used to compute digest the PDF document
        HashAlgorithm algo = HashAlgorithm.SHA256;

        //Reason for signing/certifying
        String reason = "Reason";

        //location of the signer
        String location = "Location";

        //contact info of the signer
        String contactInfo = "Contact Info";

        //DocMDP Permissions associated with certification
        MDPPermissions mdpPermissions = MDPPermissions.valueOf("FormChanges");

        //Create a PDFSignatureAppearanceOptions object
        //and show date information
        PDFSignatureAppearenceOptions appOptions = new PDFSignatureAppearenceOptions(
                PDFSignatureAppearanceType.NAME, null, 1.0d, null, true, true,
                true, true, false, true, true, TextDirection.AUTO);
        signatureOptions.setLockCertifyingField(true);
        signatureOptions.setSignatureFieldName(fieldName);
        signatureOptions.setAlgo(algo);
        signatureOptions.setContactInfo(contactInfo);
        signatureOptions.setLocation(location);
        signatureOptions.setSigAppearence(appOptions);
        signatureOptions.setReason(reason);
        signatureOptions.setDssPref(getDSSPreferences(rr));
        signatureOptions.setCredential(new CredentialContext(alias, rr));
        signatureOptions.setMdpPermissions(mdpPermissions);
  return signatureOptions;
 }

 private DSSPreferences getDSSPreferences(ResourceResolver rr){
  //sets the DSS Preferences
        DSSPreferencesImpl prefs = DSSPreferencesImpl.getInstance();
        prefs.setPKIPreferences(getPKIPreferences());
        GeneralPreferencesImpl gp = (GeneralPreferencesImpl) prefs.getPKIPreferences().getGeneralPreferences();
        gp.setDisableCache(true);
        return prefs;
    }

    private PKIPreferences getPKIPreferences(){
     //sets the PKI Preferences
        PKIPreferences pkiPref = new PKIPreferencesImpl();
        pkiPref.setCRLPreferences(getCRLPreferences());
        pkiPref.setPathPreferences(getPathValidationPreferences());
        return pkiPref;
    }

    private CRLPreferences getCRLPreferences(){
        //specifies the CRL Preferences
        CRLPreferencesImpl crlPrefs = new CRLPreferencesImpl();
        crlPrefs.setRevocationCheck(RevocationCheckStyle.CheckIfAvailable);
        crlPrefs.setGoOnline(true);
        return crlPrefs;
    }

    private PathValidationPreferences getPathValidationPreferences(){
     //sets the path validation preferences
        PathValidationPreferencesImpl pathPref = new PathValidationPreferencesImpl();
        pathPref.setDoValidation(false);
        return pathPref;

    }

    /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }

}
```

### Protezione dei documenti {#securing-documents}

secureDocument consente di crittografare, firmare/certificare ed estendere un documento PDF singolarmente o in qualsiasi combinazione in un determinato ordine. Per accedere a questa funzionalità, passa l’argomento corrispondente. Se null, si presume che l&#39;elaborazione non sia necessaria.

**Crittografia dei documenti PDF con password**

Quando crittografi un documento PDF con una password, un utente deve specificare la password per aprire il documento PDF in Adobe Reader o Acrobat. Inoltre, prima che un’altra operazione di AEM Forms Document Services utilizzi il documento, è necessario sbloccare un documento PDF crittografato con password.

**Crittografia di documenti PDF con certificati**

La crittografia basata su certificato consente di crittografare un documento per destinatari specifici utilizzando la tecnologia a chiave pubblica.

È possibile assegnare a diversi destinatari autorizzazioni diverse per il documento. Molti aspetti della crittografia sono resi possibili dalla tecnologia a chiave pubblica.

Un algoritmo viene utilizzato per generare due numeri grandi, noti come chiavi che hanno le seguenti proprietà:

* Una chiave viene utilizzata per crittografare un set di dati. In seguito, solo l’altra chiave può essere utilizzata per decrittografare i dati.
* È impossibile distinguere una chiave dall&#39;altra.
* Una delle chiavi funge da chiave privata di un utente. È importante che solo l’utente abbia accesso a questa chiave.
* L&#39;altra chiave è la chiave pubblica dell&#39;utente, che può essere condivisa con altri utenti.

Un certificato a chiave pubblica contiene la chiave pubblica e le informazioni di identificazione di un utente. Il formato X.509 viene utilizzato per l’archiviazione dei certificati. I certificati vengono generalmente rilasciati e firmati digitalmente da un&#39;autorità di certificazione (CA), un&#39;entità riconosciuta che fornisce una misura di affidabilità nella validità del certificato. I certificati hanno una data di scadenza dopo la quale non sono più validi.

Inoltre, gli elenchi di revoche di certificati (CRL) forniscono informazioni sui certificati revocati prima della data di scadenza. I CRL vengono pubblicati periodicamente dalle autorità di certificazione. Lo stato di revoca di un certificato può essere recuperato anche tramite il protocollo OCSP (Online Certificate Status Protocol) in rete.

>[!NOTE]
>
>Prima di poter crittografare un documento PDF con un certificato, è necessario assicurarsi di aggiungere il certificato all&#39;archivio fonti attendibili AEM.

**Applicazione dei diritti di utilizzo ai documenti di PDF**

Puoi applicare i diritti di utilizzo ai documenti di PDF utilizzando l’API client Java per le estensioni di Reader e il servizio web. I diritti di utilizzo riguardano funzionalità disponibili per impostazione predefinita in Acrobat ma non in Adobe Reader, ad esempio la possibilità di aggiungere commenti a un modulo o di compilare campi modulo e salvare il modulo. I documenti PDF a cui sono applicati diritti di utilizzo sono denominati documenti abilitati per i diritti. L’utente che apre un documento abilitato ai diritti in Adobe Reader può eseguire operazioni abilitate per quel documento specifico.

Prima di poter eseguire il Reader Estendi un documento PDF con un certificato, è necessario assicurarsi di aggiungere il certificato all&#39;archivio chiavi AEM.

**Firma digitale di documenti PDF**

Le firme digitali possono essere applicate ai documenti PDF per garantire un livello di sicurezza adeguato. Le firme digitali, come le firme scritte a mano, forniscono un mezzo mediante il quale i firmatari si identificano e rilasciano dichiarazioni su un documento.

La tecnologia utilizzata per apporre la firma digitale ai documenti consente di garantire che il firmatario e i destinatari siano chiari su ciò che è stato firmato e certi che il documento non sia stato modificato dopo la firma.

I documenti PDF sono firmati mediante una tecnologia a chiave pubblica. Un firmatario ha due chiavi: una chiave pubblica e una chiave privata. La chiave privata viene memorizzata nelle credenziali di un utente che devono essere disponibili al momento della firma.

La chiave pubblica viene archiviata nel certificato dell&#39;utente che deve essere disponibile per i destinatari per convalidare la firma. Le informazioni sui certificati revocati si trovano nelle risposte CRL (Certificate Revocation List) e OCSP (Online Certificate Status Protocol) distribuite dalle autorità di certificazione (CA). L’ora della firma può essere ottenuta da una fonte attendibile nota come autorità di marca temporale.

>[!NOTE]
>
>Prima di poter firmare digitalmente un documento PDF, è necessario assicurarsi di aggiungere le credenziali nel registro chiavi AEM. Le credenziali sono la chiave privata utilizzata per la firma.

>[!NOTE]
>
>AEM Forms supporta anche *[CAdES](https://en.wikipedia.org/wiki/CAdES_%28computing%29)* specifica per la firma digitale di documenti PDF.

**Certificazione dei documenti di PDF**

È possibile proteggere un documento PDF certificandolo con un tipo particolare di firma, denominata firma certificata. Una firma certificata si distingue da una firma digitale nei seguenti modi:

Deve essere la prima firma applicata al documento PDF, ovvero, al momento dell&#39;applicazione della firma certificata, tutti gli altri campi della firma presenti nel documento devono essere non firmati.

In un documento PDF è consentita una sola firma certificata. Se si desidera firmare e certificare un documento PDF, è necessario certificarlo prima di firmarlo.

Dopo aver certificato un documento PDF, è possibile firmare digitalmente ulteriori campi di firma.

L&#39;autore o l&#39;originatore del documento può specificare che il documento può essere modificato in alcuni modi senza invalidare la firma certificata.

Ad esempio, il documento può consentire la compilazione di moduli o la creazione di commenti. Se l’autore specifica che una determinata modifica non è consentita,

Acrobat impedisce agli utenti di modificare il documento in questo modo. Se vengono apportate tali modifiche, ad esempio utilizzando un’altra applicazione, la firma certificata non è valida e Acrobat genera un avviso quando un utente apre il documento. Con le firme non certificate, le modifiche non vengono impedite e le normali operazioni di modifica non invalidano la firma originale.

Al momento della firma, il documento viene analizzato per individuare tipi specifici di contenuto che potrebbero rendere ambiguo o fuorviante il contenuto di un documento.

Ad esempio, un’annotazione potrebbe oscurare del testo su una pagina importante per comprendere cosa viene certificato. Su tale contenuto può essere fornita una spiegazione (attestazione legale).

>[!NOTE]
>
>Prima di poter firmare digitalmente un documento PDF, è necessario assicurarsi di aggiungere le credenziali nel registro chiavi AEM. Le credenziali sono la chiave privata utilizzata per la firma.

**Sintassi**:

```java
secureDocument(Document inDoc,
 EncryptionOptions encryptionOptions,
 SignatureOptions signatureOptions,
 ReaderExtensionOptions readerExtensionOptions,
 UnlockOptions unlockOptions)
```

**Parametri di input**

<table>
 <tbody>
  <tr>
   <th>Parametri</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td><code>inDoc</code><br /> </td>
   <td>Documento input PDF Documento<br /> </td>
  </tr>
  <tr>
   <td><code>encryptionOptions</code><br /> </td>
   <td>Include gli argomenti necessari per crittografare un documento PDF<br /> </td>
  </tr>
  <tr>
   <td><code>signatureOptions</code></td>
   <td>Include le opzioni necessarie per firmare/certificare un documento PDF</td>
  </tr>
  <tr>
   <td><code>readerExtensionOptions</code></td>
   <td>Include le opzioni necessarie per il Reader Estensione di un documento PDF</td>
  </tr>
  <tr>
   <td><code>unlockOptions</code></td>
   <td>Include i parametri necessari per sbloccare un file crittografato. Questa opzione è necessaria solo se il file è crittografato.<br /> </td>
  </tr>
 </tbody>
</table>

**Esempio 1**: questo esempio viene utilizzato per eseguire la crittografia della password, certificando un campo di firma e un Reader Estensione del documento PDF.

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * ___________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.util.ArrayList;
import java.util.List;

import javax.jcr.Session;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.jcr.api.SlingRepository;
import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.docassurance.client.api.DocAssuranceServiceOperationTypes;
import com.adobe.fd.docassurance.client.api.EncryptionOptions;
import com.adobe.fd.docassurance.client.api.ReaderExtensionOptions;
import com.adobe.fd.docassurance.client.api.SignatureOptions;
import com.adobe.fd.encryption.client.PasswordEncryptionCompatability;
import com.adobe.fd.encryption.client.PasswordEncryptionOption;
import com.adobe.fd.encryption.client.PasswordEncryptionOptionSpec;
import com.adobe.fd.encryption.client.PasswordEncryptionPermission;
import com.adobe.fd.readerextensions.client.ReaderExtensionsOptionSpec;
import com.adobe.fd.readerextensions.client.UsageRights;
import com.adobe.fd.signatures.client.types.MDPPermissions;
import com.adobe.fd.signatures.pdf.inputs.CredentialContext;
import com.adobe.fd.signatures.pdf.inputs.DSSPreferences;
import com.adobe.fd.signatures.pdf.inputs.DSSPreferencesImpl;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions.PDFSignatureAppearanceType;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions.TextDirection;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;
import com.adobe.fd.signatures.pki.client.types.common.HashAlgorithm;
import com.adobe.fd.signatures.pki.client.types.common.RevocationCheckStyle;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.GeneralPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferencesImpl;

/**
 *
 * This class provides a sample code to use {@code DocAssuranceService} to carry out
 * password encryption, certifying a signature field and reader extending the pdf document.
 *
 * PreRequisites - Digital certificate for signing the document has to be uploaded on Granite Key Store
 * Digital certificate for reader extending the document has to be uploaded on Granite Key Store
 */

@Component
@Service(value=PassEncryptCertifyExtend.class)
public class PassEncryptCertifyExtend {

 @Reference
 private DocAssuranceService docAssuranceService;

 @Reference
    private SlingRepository slingRepository;

 @Reference
    private JcrResourceResolverFactory jcrResourceResolverFactory ;

 /**
  *
  * @param inputFile - path to the pdf document stored at disk
  * @param outputFile - path to the pdf document where the output needs to be stored
  * @throws Exception
  */
 public void SecureDocument(String inputFile, String outputFile) throws Exception{

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  File outFile = new File(outputFile);
  Document outDoc = null;

  Session adminSession = null;
        ResourceResolver resourceResolver = null;
        try {

          /** resourceResolver with admin privileges to be passed to SignatureServiceAPI and Reader Extensions
          the resource resolver for signature options has to be corresponding to the user who has the signing certificate in his granite key store
          the resource resolver for signature options has to be corresponding to the user who has the credential for reader extension in his granite key store
          here we are using the same resource resolver
          */
          adminSession = slingRepository.loginAdministrative(null);
             resourceResolver = jcrResourceResolverFactory.getResourceResolver(adminSession);

             //retrieve specifications for each of the services, you may pass null if you don't want to use that service
             //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
    outDoc = docAssuranceService.secureDocument(inDoc, getPassEncryptionOptions(), getCertificationOptions(resourceResolver), getReaderExtensionOptions(resourceResolver),null);
        }
        finally{
            /**
             * always close the PDFDocument object after your processing is done.
             */
            if(inDoc != null){
                inDoc.close();
            }
            if(adminSession != null && adminSession.isLive()){
                if(resourceResolver != null){
                    resourceResolver.close();
                }
                adminSession.logout();
            }
        }

        outDoc.copyToFile(outFile);

 }

  /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }

 /**
  * @return EncryptionOptions for password encrypting the document.
  *
  */
 private EncryptionOptions getPassEncryptionOptions(){

  //Create an instance of EncryptionOptions
  EncryptionOptions encryptionOptions = EncryptionOptions.getInstance();

  //Create a PasswordEncryptionOptionSpec object that stores encryption run-time values
        PasswordEncryptionOptionSpec passSpec = new PasswordEncryptionOptionSpec();

        //Specify the PDF document resource to encrypt
        passSpec.setEncryptOption(PasswordEncryptionOption.ALL);

        //Specify the permission associated with the password
        //These permissions enable data to be extracted from a password
        //protected PDF form
        List<PasswordEncryptionPermission> encrypPermissions = new ArrayList<PasswordEncryptionPermission>();
        encrypPermissions.add(PasswordEncryptionPermission.PASSWORD_EDIT_ADD);
        encrypPermissions.add(PasswordEncryptionPermission.PASSWORD_EDIT_MODIFY);
        passSpec.setPermissionsRequested(encrypPermissions);

        //Specify the Acrobat version
        passSpec.setCompatability(PasswordEncryptionCompatability.ACRO_7);

        //Specify the password values
        passSpec.setDocumentOpenPassword("OpenPassword");
        passSpec.setPermissionPassword("PermissionPassword");

        //Set the encryption type to Password Encryption
  encryptionOptions.setEncryptionType(DocAssuranceServiceOperationTypes.ENCRYPT_WITH_PASSWORD);
        encryptionOptions.setPasswordEncryptionOptionSpec(passSpec);

     return encryptionOptions;
 }

 /**
  *
  * @param resourceResolver corresponding to the user with the access to Reader Extension credential
  * for the given alias -"production" in this case
  * @return
  */
 private ReaderExtensionOptions getReaderExtensionOptions(ResourceResolver resourceResolver){

  //Create an instance of ReaderExtensionOptions
  ReaderExtensionOptions reOptions = ReaderExtensionOptions.getInstance();

  //Create instance for UsageRights to be enabled in the reader
  UsageRights uRights = new UsageRights();
  //enabling comments in the PDF Reader
  uRights.setEnabledComments(true);
  //setting ReaderExtensionsOptionSpec in the reOptions
  reOptions.setReOptions(new ReaderExtensionsOptionSpec(uRights, "Enable commenting in PDF"));
  //alias of the credential to be used for extending the PDF Reader
  reOptions.setCredentialAlias("production");
  //corresponding to the user with the access to Reader Extension credential
  reOptions.setResourceResolver(resourceResolver);

  return reOptions;
 }

 /**
  *
  * @param rr resource resolver corresponding to the user with the access to signing credential for the
  * given alias "allcertificatesanypolicytest11ee_new" in this case
  * @return SignatureOptions
  */
 private SignatureOptions getCertificationOptions(ResourceResolver rr){

  //create an instance of SignatureOptions
  SignatureOptions signatureOptions = SignatureOptions.getInstance();

  //set the operation you want to perform - SIGN/CERTIFY
  signatureOptions.setOperationType(DocAssuranceServiceOperationTypes.CERTIFY);

  //signature field to certify, pass null if invisible signature field
  String fieldName = "Signature1" ;

  //alias of the private credential uploaded on the Key Store
        String alias = "allcertificatesanypolicytest11ee_new";

        //Hash Algo to be used to compute digest the PDF document
        HashAlgorithm algo = HashAlgorithm.SHA384;

        //Reason for signing/certifying
        String reason = "Test Reason";

        //location of the signer
        String location = "Test Location";

        //contact info of the signer
        String contactInfo = "Test Contact";

        //DocMDP Permissions associated with certification
        MDPPermissions mdpPermissions = MDPPermissions.valueOf("FormChanges");

        //Create a PDFSignatureAppearanceOptions object
        //and show date information
        PDFSignatureAppearenceOptions appOptions = new PDFSignatureAppearenceOptions(
                PDFSignatureAppearanceType.NAME, null, 1.0d, null, true, true,
                true, true, true, true, true, TextDirection.AUTO);

        signatureOptions.setSignatureFieldName(fieldName);
        signatureOptions.setAlgo(algo);
        signatureOptions.setContactInfo(contactInfo);
        signatureOptions.setLocation(location);
        signatureOptions.setSigAppearence(appOptions);
        signatureOptions.setReason(reason);
        signatureOptions.setDssPref(getDSSPreferences(rr));
        signatureOptions.setCredential(new CredentialContext(alias, rr));
        signatureOptions.setMdpPermissions(mdpPermissions);
  return signatureOptions;
 }

 private DSSPreferences getDSSPreferences(ResourceResolver rr){
  //sets the DSS Preferences
        DSSPreferencesImpl prefs = DSSPreferencesImpl.getInstance();
        prefs.setPKIPreferences(getPKIPreferences());
        GeneralPreferencesImpl gp = (GeneralPreferencesImpl) prefs.getPKIPreferences().getGeneralPreferences();
        gp.setDisableCache(true);
        return prefs;
    }

    private PKIPreferences getPKIPreferences(){
     //sets the PKI Preferences
        PKIPreferences pkiPref = new PKIPreferencesImpl();
        pkiPref.setCRLPreferences(getCRLPreferences());
        pkiPref.setPathPreferences(getPathValidationPreferences());
        return pkiPref;
    }

    private CRLPreferences getCRLPreferences(){
        //specifies the CRL Preferences
        CRLPreferencesImpl crlPrefs = new CRLPreferencesImpl();
        crlPrefs.setRevocationCheck(RevocationCheckStyle.CheckIfAvailable);
        crlPrefs.setGoOnline(true);
        return crlPrefs;
    }

    private PathValidationPreferences getPathValidationPreferences(){
     //sets the path validation preferences
        PathValidationPreferencesImpl pathPref = new PathValidationPreferencesImpl();
        pathPref.setDoValidation(false);
        return pathPref;

    }

}
```

**Esempio 2**: questo esempio viene utilizzato per eseguire la crittografia PKI, firmare un campo di firma e un Reader Estensione del documento PDF.

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * ___________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.ByteArrayInputStream;
import java.io.File;
import java.io.IOException;
import java.io.InputStream;
import java.util.ArrayList;
import java.util.List;

import javax.jcr.Binary;
import javax.jcr.Node;
import javax.jcr.RepositoryException;
import javax.jcr.Session;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.jcr.api.SlingRepository;
import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceException;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.docassurance.client.api.DocAssuranceServiceOperationTypes;
import com.adobe.fd.docassurance.client.api.EncryptionOptions;
import com.adobe.fd.docassurance.client.api.ReaderExtensionOptions;
import com.adobe.fd.docassurance.client.api.SignatureOptions;
import com.adobe.fd.encryption.client.CertificateEncryptionCompatibility;
import com.adobe.fd.encryption.client.CertificateEncryptionIdentity;
import com.adobe.fd.encryption.client.CertificateEncryptionOption;
import com.adobe.fd.encryption.client.CertificateEncryptionOptionSpec;
import com.adobe.fd.encryption.client.CertificateEncryptionPermissions;
import com.adobe.fd.encryption.client.Recipient;
import com.adobe.fd.readerextensions.client.ReaderExtensionsOptionSpec;
import com.adobe.fd.readerextensions.client.UsageRights;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.pdf.inputs.CredentialContext;
import com.adobe.fd.signatures.pdf.inputs.DSSPreferences;
import com.adobe.fd.signatures.pdf.inputs.DSSPreferencesImpl;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions.PDFSignatureAppearanceType;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions.TextDirection;
import com.adobe.fd.signatures.pki.client.types.common.HashAlgorithm;
import com.adobe.fd.signatures.pki.client.types.common.RevocationCheckStyle;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.GeneralPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferencesImpl;

/**
 *
 * This class provides a sample code to use {@code DocAssuranceService} to carry out
 * certificate encryption, signing a signature field and reader extending the pdf document.
 *
 * PreRequisites - Digital certificate for encrypting the document has to be uploaded on Granite Trust Store
       Digital certificate for signing the document has to be uploaded on Granite Key Store
 * Digital certificate for reader extending the document has to be uploaded on Granite Key Store
 */

@Component
@Service(value=PassEncryptSignExtend.class)
public class PassEncryptSignExtend {

 @Reference
 private DocAssuranceService docAssuranceService;

 @Reference
    private SlingRepository slingRepository;

 @Reference
    private JcrResourceResolverFactory jcrResourceResolverFactory ;

 /**
  *
  * @param inputFile - path to the pdf document stored at disk
  * @param outputFile - path to the pdf document where the output needs to be stored
  * @throws Exception
  */
 public void CertEncryptSignReaderExtend(String inputFile, String outputFile) throws Exception{

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  File outFile = new File(outputFile);
  Document outDoc = null;

  Session adminSession = null;
        ResourceResolver resourceResolver = null;
        try {

          /** resourceResolver with admin privileges to be passed to SignatureServiceAPI and Reader Extensions
          the resource resolver for signature options has to be corresponding to the user who has the signing certificate in his granite key store
          the resource resolver for signature options has to be corresponding to the user who has the credential for reader extension in his granite key store
          here we are using the same resource resolver
          */
          adminSession = slingRepository.loginAdministrative(null);
             resourceResolver = jcrResourceResolverFactory.getResourceResolver(adminSession);

             //retrieve specifications for each of the services, you may pass null if you don't want to use that service
             //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
    outDoc = docAssuranceService.secureDocument(inDoc, getCertEncryptionOptions(), getSignatureOptions(resourceResolver), getReaderExtensionOptions(resourceResolver),null);
        }
        finally{
            /**
             * always close the PDFDocument object after your processing is done.
             */
            if(inDoc != null){
                inDoc.close();
            }
            if(adminSession != null && adminSession.isLive()){
                if(resourceResolver != null){
                    resourceResolver.close();
                }
                adminSession.logout();
            }
        }

        outDoc.copyToFile(outFile);

 }

  /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }

 /**
  * @return EncryptionOptions for password encrypting the document.
  *
  */
 private EncryptionOptions getCertEncryptionOptions(){

  //Create an instance of EncryptionOptions
  EncryptionOptions encryptionOptions = EncryptionOptions.getInstance();

        //Set the encryption type to Certificate Encryption
  encryptionOptions.setEncryptionType(DocAssuranceServiceOperationTypes.ENCRYPT_WITH_CERTIFCATE);

  //Set the List that stores PKI information
  List<CertificateEncryptionIdentity> pkiIdentities = new ArrayList<CertificateEncryptionIdentity>();

  //Set the Permission List
  List<CertificateEncryptionPermissions> permList = new ArrayList<CertificateEncryptionPermissions>();
  permList.add(CertificateEncryptionPermissions.PKI_ALL_PERM) ;

  //Create a Recipient object to store certificate information
  Recipient recipient = new Recipient();

  //Specify the alias of the public certificate present in the trust store that is used to encrypt the document
  recipient.setX509Cert("alias");
  /*
   * An alternative to add a certificate is by providing the alias
   * of the certificate stored in AEM trust store.
   * recipient.setAlias(alias);
   */

  //Create an EncryptionIdentity object
  CertificateEncryptionIdentity encryptionId = new CertificateEncryptionIdentity();
  encryptionId.setPerms(permList);
  encryptionId.setRecipient(recipient);

  //Add the EncryptionIdentity to the list
  pkiIdentities.add(encryptionId);

  //Set encryption run-time options
  CertificateEncryptionOptionSpec certOptionsSpec = new CertificateEncryptionOptionSpec();
  certOptionsSpec.setOption(CertificateEncryptionOption.ALL);
  certOptionsSpec.setCompat(CertificateEncryptionCompatibility.ACRO_9);

  //Set the certificate encryption option
  encryptionOptions.setCertOptionSpec(certOptionsSpec)

  //Set the PKI Identities in encryption Options
        encryptionOptions.setPkiIdentities(pkiIdentities);

     return encryptionOptions;
 }

 /**
  *
  * @param resourceResolver corresponding to the user with the access to Reader Extension credential
  * for the given alias -"production" in this case
  * @return
  */
 private ReaderExtensionOptions getReaderExtensionOptions(ResourceResolver resourceResolver){

  //Create an instance of ReaderExtensionOptions
  ReaderExtensionOptions reOptions = ReaderExtensionOptions.getInstance();

  //Create instance for UsageRights to be enabled in the reader
  UsageRights uRights = new UsageRights();
  //enabling comments in the PDF Reader
  uRights.setEnabledComments(true);
  //setting ReaderExtensionsOptionSpec in the reOptions
  reOptions.setReOptions(new ReaderExtensionsOptionSpec(uRights, "Enable commenting in PDF"));
  //alias of the credential to be used for extending the PDF Reader
  reOptions.setCredentialAlias("production");
  //corresponding to the user with the access to Reader Extension credential
  reOptions.setResourceResolver(resourceResolver);

  return reOptions;
 }

 /**
  *
  * @param rr resource resolver corresponding to the user with the access to signing credential for the
  * given alias "allcertificatesanypolicytest11ee_new" in this case
  * @return SignatureOptions
  */
 private SignatureOptions getSignatureOptions(ResourceResolver rr){

  //create an instance of SignatureOptions
  SignatureOptions signatureOptions = SignatureOptions.getInstance();

  //set the operation you want to perform - SIGN/CERTIFY
  signatureOptions.setOperationType(DocAssuranceServiceOperationTypes.SIGN);

  //field to sign
  String fieldName = "Signature1" ;

  //alias of the private credential uploaded on the Key Store
        String alias = "allcertificatesanypolicytest11ee_new";

        //Hash Algo to be used to compute digest the PDF document
        HashAlgorithm algo = HashAlgorithm.SHA384;

        //Reason for signing/certifying
        String reason = "Test Reason";

        //location of the signer
        String location = "Test Location";

        //contact info of the signer
        String contactInfo = "Test Contact";

        //Create a PDFSignatureAppearanceOptions object
        //and show date information
        PDFSignatureAppearenceOptions appOptions = new PDFSignatureAppearenceOptions(
                PDFSignatureAppearanceType.NAME, null, 1.0d, null, true, true,
                true, true, true, true, true, TextDirection.AUTO);

        signatureOptions.setSignatureFieldName(fieldName);
        signatureOptions.setAlgo(algo);
        signatureOptions.setContactInfo(contactInfo);
        signatureOptions.setLocation(location);
        signatureOptions.setSigAppearence(appOptions);
        signatureOptions.setReason(reason);
        signatureOptions.setDssPref(getDSSPreferences(rr));
        signatureOptions.setCredential(new CredentialContext(alias, rr));
  return signatureOptions;
 }

 private DSSPreferences getDSSPreferences(ResourceResolver rr){
  //sets the DSS Preferences
        DSSPreferencesImpl prefs = DSSPreferencesImpl.getInstance();
        prefs.setPKIPreferences(getPKIPreferences());
        GeneralPreferencesImpl gp = (GeneralPreferencesImpl) prefs.getPKIPreferences().getGeneralPreferences();
        gp.setDisableCache(true);
        return prefs;
    }

    private PKIPreferences getPKIPreferences(){
     //sets the PKI Preferences
        PKIPreferences pkiPref = new PKIPreferencesImpl();
        pkiPref.setCRLPreferences(getCRLPreferences());
        pkiPref.setPathPreferences(getPathValidationPreferences());
        return pkiPref;
    }

    private CRLPreferences getCRLPreferences(){
        //specifies the CRL Preferences
        CRLPreferencesImpl crlPrefs = new CRLPreferencesImpl();
        crlPrefs.setRevocationCheck(RevocationCheckStyle.CheckIfAvailable);
        crlPrefs.setGoOnline(true);
        return crlPrefs;
    }

    private PathValidationPreferences getPathValidationPreferences(){
     //sets the path validation preferences
        PathValidationPreferencesImpl pathPref = new PathValidationPreferencesImpl();
        pathPref.setDoValidation(false);
        return pathPref;

    }

}
```

Se durante l’estensione di un documento PDF viene visualizzato il seguente messaggio di errore:

```javascript
org.apache.sling.engine.impl.SlingRequestProcessorImpl service: Uncaught Throwable java.lang.ThreadDeath: null at com.adobe.internal.pdftoolkit.services.javascript.GibsonContextFactory.observeInstructionCount(GibsonContextFactory.java:138)
```

Significa che il servizio di estensione del Reader non è in grado di eseguire i JavaScript utilizzati nel documento entro l’intervallo di timeout definito.

Gestisci l’intervallo di timeout definito per JavaScript nel documento di PDF utilizzando:

```javascript
ReaderExtensionsOptionSpec optionSpec = new ReaderExtensionsOptionSpec(usageRights, message);
optionSpec.setJsScriptExecutionTimeoutInterval(100);
```

dove 100 si riferisce all’intervallo di timeout definito per l’esecuzione di JavaScript (in secondi). Imposta un valore appropriato per l’intervallo di timeout.

### Recupero diritti di utilizzo delle credenziali {#getting-credential-usage-rights}

Per recuperare le informazioni sui diritti di utilizzo delle credenziali specificate dalla `credentialAlias`, chiama questa API dall&#39;interno di `SecureDocument` API.

**Sintassi**: `getCredentialUsageRights(String credentialAlias, ResourceResolver resourceResolver)`

**Parametri di input**

<table>
 <tbody>
  <tr>
   <th>Parametri</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td><code>credentialAlias</code><br /> </td>
   <td>Il <code>credentialAlias</code> che specifica le credenziali.<br /> </td>
  </tr>
  <tr>
   <td><code>credentialPassword</code><br /> </td>
   <td>Password della credenziale se la credenziale è crittografata, se non è crittografata è necessario utilizzare null.<br /> </td>
  </tr>
 </tbody>
</table>

Nell&#39;esempio seguente vengono recuperate le informazioni sui diritti di utilizzo per le credenziali specificate.

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * __________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and may be covered by U.S. and Foreign Patents,
 * patents in process, and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.fd.readerextensions.samples;

import java.io.File;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.ResourceResolverFactory;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.docassurance.client.api.ReaderExtensionOptions;
import com.adobe.fd.readerextensions.client.GetUsageRightsResult;
import com.adobe.fd.readerextensions.client.ReaderExtensionsOptionSpec;
import com.adobe.fd.readerextensions.client.UsageRights;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;

/**
 *
 */
@Component(metatype = true, immediate = true, label = "ReaderExtensionsSampleService")
@Service(value = ReaderExtensionsSampleService.class)
public class ReaderExtensionsSampleService {

 @Reference(referenceInterface=DocAssuranceService.class)
 private DocAssuranceService docAssuranceService;

 @Reference(referenceInterface=ResourceResolverFactory.class)
 private ResourceResolverFactory resourceResolverFactory;
public void getCredentialUsageRights() {
  try {

   GetUsageRightsResult usageRightsResult = docAssuranceService.getCredentialUsageRights("production",
     resourceResolverFactory.getAdministrativeResourceResolver(null));

   System.out.println("Credential usage Rights are as follows");
   System.out.println(usageRightsResult.toString());

  } catch (Exception e) {
   e.printStackTrace();
  }
 }
}
```

### Recupero diritti di utilizzo documento {#getting-document-usage-rights}

Per recuperare le informazioni sui diritti di utilizzo per un dato documento, chiama questa API da `docAssuranceService`API.

**Sintassi**: `getDocumentUsageRights(Document inDocument, UnlockOptions unlockOptions)`

**Parametri di input**

<table>
 <tbody>
  <tr>
   <th>Parametri</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td><code>inDocument</code><br /> </td>
   <td>Documento da cui recuperare le informazioni sui diritti di utilizzo<br /> </td>
  </tr>
 </tbody>
</table>

Nel codice di esempio seguente vengono restituite le informazioni sui diritti di utilizzo per un documento.

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * __________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and may be covered by U.S. and Foreign Patents,
 * patents in process, and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.fd.readerextensions.samples;

import java.io.File;
import java.util.HashMap;
import java.util.Map;

import javax.jcr.SimpleCredentials;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.LoginException;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.api.resource.ResourceResolverFactory;
import org.apache.sling.jcr.resource.JcrResourceConstants;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.docassurance.client.api.ReaderExtensionOptions;
import com.adobe.fd.readerextensions.client.GetUsageRightsResult;
import com.adobe.fd.readerextensions.client.ReaderExtensionsOptionSpec;
import com.adobe.fd.readerextensions.client.UsageRights;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;

@Component(metatype = true, immediate = true, label = "ReaderExtensionsSampleService")
@Service(value = ReaderExtensionsSampleService.class)
public class ReaderExtensionsSampleService {

 @Reference(referenceInterface=DocAssuranceService.class)
 private DocAssuranceService docAssuranceService;

 @Reference(referenceInterface=ResourceResolverFactory.class)
private ResourceResolverFactory resourceResolverFactory;

public void getDocumentUsageRights() {
  Document inputDocument = null;
  try {
   //Name of the input file on which usage rights is to be applied.
   String inputFileName = "C:/RETest/input/GetUsageRightsInfo/02_fromAcrobat7.0.8_Acro700_UB8_BS_signed_commenting.pdf";

   //Document to be input to Doc Assurance Service
   inputDocument = new Document(new File(inputFileName));

   //Unlock options to unlock the document if some kind of security is set on it.
   //Currently set to null because input document has no security.
   UnlockOptions unlockOptions = null;

   GetUsageRightsResult usageRightsResult = docAssuranceService.getDocumentUsageRights(inputDocument, unlockOptions);

   System.out.println("Document usage Rights are as follows");
   System.out.println(usageRightsResult.toString());

  } catch (Exception e) {
   e.printStackTrace();
  } finally {
//   if (inputDocument != null) {
//    inputDocument.dispose(); //dispose off the document.
//   }
  }
}

/**
  * Resource resolver of the user in whose keystore Reader Extensions Certificate is installed.
  * @param resourceResolverFactory
  * @return
  * @throws LoginException
  */
 public ResourceResolver getResourceResolver() throws LoginException{
  Map<String,Object> authInfo = new HashMap<String,Object>();
  //Username and password of the user in whose keystore Reader Extensions Certificate is installed
  SimpleCredentials credentials = new SimpleCredentials("username"/*UserName*/, "password"/*Password*/.toCharArray());
  authInfo.put(JcrResourceConstants.AUTHENTICATION_INFO_CREDENTIALS,credentials);
  return resourceResolverFactory.getResourceResolver(authInfo);
}

}
```

### Rimozione dei diritti di utilizzo {#removing-usage-rights}

È possibile rimuovere i diritti di utilizzo per un documento chiamando il `removeUsageRights`API dall&#39;interno di `docAssuranceService`API.

**Parametri di input**

<table>
 <tbody>
  <tr>
   <th>Parametri</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td><code>inDocument</code><br /> </td>
   <td>Documento da cui rimuovere i diritti di utilizzo.<br /> </td>
  </tr>
  <tr>
   <td><code>unlockOptions</code><br /> </td>
   <td>Include i parametri necessari per sbloccare un file crittografato. Questa opzione è necessaria solo se il file è crittografato.<br /> </td>
  </tr>
 </tbody>
</table>

Nell&#39;esempio seguente vengono rimossi i diritti di utilizzo per un determinato documento.

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * __________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and may be covered by U.S. and Foreign Patents,
 * patents in process, and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.fd.readerextensions.samples;

import java.io.File;
import java.util.HashMap;
import java.util.Map;

import javax.jcr.SimpleCredentials;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.LoginException;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.api.resource.ResourceResolverFactory;
import org.apache.sling.jcr.resource.JcrResourceConstants;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.docassurance.client.api.ReaderExtensionOptions;
import com.adobe.fd.readerextensions.client.GetUsageRightsResult;
import com.adobe.fd.readerextensions.client.ReaderExtensionsOptionSpec;
import com.adobe.fd.readerextensions.client.UsageRights;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;

@Component(metatype = true, immediate = true, label = "ReaderExtensionsSampleService")
@Service(value = ReaderExtensionsSampleService.class)
public class ReaderExtensionsSampleService {

 @Reference(referenceInterface=DocAssuranceService.class)
 private DocAssuranceService docAssuranceService;

 @Reference(referenceInterface=ResourceResolverFactory.class)
private ResourceResolverFactory resourceResolverFactory;

public void removeDocumentUsageRights() {
  Document inputDocument = null;
  Document outDocument = null;
  try {
   //Name of the input file on which usage rights is to be applied.
   String inputFileName = "C:/RETest/input/RemoveUsageRights/01_Ubiquitized_50-267_PDF1.5_UB2_Rights.pdf";

   //Name of the output file where result will be saved.
   String outputFileName = "C:/RETest/output/samples/removeUsageRightsOutput.pdf";

   //Document to be input to Doc Assurance Service
   inputDocument = new Document(new File(inputFileName));

   //Unlock options to unlock the document if some kind of security is set on it.
   //Currently set to null because input document has no security.
   UnlockOptions unlockOptions = null;

   //Specify null encryption options and signatures options.
   //If requirement is also to encrypt and sign the document then, corresponding options can also be specified.
   outDocument = docAssuranceService.removeUsageRights(inputDocument, unlockOptions);

   File outputdir = new File("C:/RETest/output/samples");
   outputdir.mkdirs();

   outDocument.copyToFile(new File(outputFileName));
  } catch (Exception e) {
   e.printStackTrace();
  }
}

/**
  * Resource resolver of the user in whose keystore Reader Extensions Certificate is installed.
  * @param resourceResolverFactory
  * @return
  * @throws LoginException
  */
 public ResourceResolver getResourceResolver() throws LoginException{
  Map<String,Object> authInfo = new HashMap<String,Object>();
  //Username and password of the user in whose keystore Reader Extensions Certificate is installed
  SimpleCredentials credentials = new SimpleCredentials("username"/*UserName*/, "password"/*Password*/.toCharArray());
  authInfo.put(JcrResourceConstants.AUTHENTICATION_INFO_CREDENTIALS,credentials);
  return resourceResolverFactory.getResourceResolver(authInfo);
}

}
```

#### Verifica delle firme digitali {#verifying-digital-signatures}

PDF È possibile verificare che le firme digitali non siano state modificate e che la firma digitale sia valida. Durante la verifica di una firma digitale, è possibile controllare lo stato della firma e le relative proprietà, ad esempio l&#39;identità del firmatario. Prima di considerare attendibile una firma digitale, è consigliabile verificarla. Durante la verifica di una firma digitale, fare riferimento a un documento PDF contenente una firma digitale.

**Sintassi**: `verify( inDoc, signatureFieldName, revocationCheckStyle, verificationTime, dssPrefs, ResourceResolver resourceResolver)`

**Parametri di input**

<table>
 <tbody>
  <tr>
   <th>Parametri</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td><code>inDoc</code><br /> </td>
   <td>Oggetto documento contenente PDF<br /> </td>
  </tr>
  <tr>
   <td><code class="code">signatureField
      Name</code><br /> </td>
   <td>Nome del campo firma da convalidare. è possibile specificare un nome completo o parziale<br /> </td>
  </tr>
  <tr>
   <td><code>revocationCheckStyle</code></td>
   <td>Opzione per gestire il controllo delle revoche dei certificati rilevati durante la convalida</td>
  </tr>
  <tr>
   <td><code>verificationTime</code></td>
   <td>L’ora in cui la firma deve essere convalidata</td>
  </tr>
  <tr>
   <td><code>dssPrefs</code></td>
   <td>Preferenze per controllare varie configurazioni di convalida. Per un documento crittografato, impostare le opzioni di sblocco utilizzando <code>setUnlockOptions()</code></td>
  </tr>
  <tr>
   <td><code>resourceResolver</code></td>
   <td>Risolutore risorse all'archivio attendibilità granite</td>
  </tr>
 </tbody>
</table>

Questo codice di esempio utilizza `DocAssuranceService` per verificare un campo firma in un documento PDF crittografato.

```java
/*************************************************************************
 *
-------------------------------------------------------------
*ADOBE SYSTEMS INCORPORATED
*Copyright 2014 Adobe Systems Incorporated
*All Rights Reserved.

*NOTICE:  Adobe permits you to use, modify, and distribute this file in accordance with the
*terms of the Adobe license agreement accompanying it.  If you have received this file from a
*source other than Adobe, then your use, modification, or distribution of it requires the prior
*written permission of Adobe.
-------------------------------------------------------------------------------------------------

 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.io.IOException;

import javax.jcr.RepositoryException;
import javax.jcr.Session;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.jcr.api.SlingRepository;
import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceException;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.IdentityInformation;
import com.adobe.fd.signatures.client.types.IdentityStatus;
import com.adobe.fd.signatures.client.types.PDFSignatureType;
import com.adobe.fd.signatures.client.types.PDFSignatureVerificationInfo;
import com.adobe.fd.signatures.client.types.SignatureProperties;
import com.adobe.fd.signatures.client.types.SignatureStatus;
import com.adobe.fd.signatures.client.types.SignatureType;
import com.adobe.fd.signatures.client.types.VerificationTime;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;
import com.adobe.fd.signatures.pdf.inputs.ValidationPreferences;
import com.adobe.fd.signatures.pdf.inputs.ValidationPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.common.RevocationCheckStyle;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.OCSPPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.TSPPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.TSPPreferencesImpl;

/**
 *
 * This class provides a sample code to use {@code DocAssuranceService} to carry out
 * verification of a signature field in an already Encrypted PDF Document
 *
 * Digital signatures can be verified to ensure that a signed PDF document was not modified and that the digital signature is valid.
 * When verifying a digital signature, you can check the signature's status and the signature's properties, such as the signer's identity.
 * Before trusting a digital signature, it is recommended that you verify it. When verifying a digital signature, reference a PDF document
 * that contains a digital signature.
 *
 * For unprotected document, you are not required to set UnlockOptions in ValidationPreferences
 * PreRequisites - The certificate chain upto the Root Certificate should be uploaded on CQ trust Store
 */

@Component
@Service(value=VerifyFieldEncryptedPDF.class)
public class VerifyFieldEncryptedPDF {

 @Reference
 private DocAssuranceService docAssuranceService;

 @Reference
    private SlingRepository slingRepository;

 @Reference
    private JcrResourceResolverFactory jcrResourceResolverFactory ;

 /**
  *
  * @param inputFile - path to an encrypted pdf document stored at JCR node
  * @throws IOException
  * @throws RepositoryException
  * @throws InvalidArgumentException
  * @throws DocAssuranceException
  */
 public void verifyFieldEncryptedPDF(String inputFile,String fieldName) throws IOException, RepositoryException, InvalidArgumentException, DocAssuranceException{

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  Session adminSession = null;
        ResourceResolver resourceResolver = null;
        try {

         //the resource resolver has to be corresponding to the user who has access to CQ Trust Store
          adminSession = slingRepository.loginAdministrative(null);
             resourceResolver = jcrResourceResolverFactory.getResourceResolver(adminSession);

           //Specify the name of the signature field

             RevocationCheckStyle revocationCheckStyle = RevocationCheckStyle.AlwaysCheck;
             VerificationTime verificationTime = VerificationTime.CURRENT_TIME;
             ValidationPreferences dssPrefs = getValidationPreferences();

             //Verify the digital signature
             PDFSignatureVerificationInfo  signInfo = docAssuranceService.verify(
                 inDoc,
                 fieldName,
                 revocationCheckStyle,
                 verificationTime,
                 dssPrefs,
                 resourceResolver);

             //Get the Signature Status
             SignatureStatus sigStatus = signInfo.getStatus();
             String myStatus="";

             //Determine the status of the signature
             if (sigStatus == SignatureStatus.DynamicFormSignatureUnknown)
                 myStatus = "The signatures in the dynamic PDF form are unknown";
             else if (sigStatus == SignatureStatus.DocumentSignatureUnknown)
                 myStatus = "The signatures in the PDF document are unknown";
             else if (sigStatus == SignatureStatus.CertifiedDynamicFormSignatureTamper)
                 myStatus = "The signatures in a certified PDF form are valid";
             else if (sigStatus == SignatureStatus.SignedDynamicFormSignatureTamper)
                 myStatus = "The signatures in a signed dynamic PDF form are valid";
             else if (sigStatus == SignatureStatus.CertifiedDocumentSignatureTamper)
                 myStatus = "The signatures in a certified PDF document are valid";
             else if (sigStatus == SignatureStatus.SignedDocumentSignatureTamper)
                 myStatus = "The signatures in a signed PDF document are valid";
             else if (sigStatus == SignatureStatus.SignatureFormatError)
                 myStatus = "The format of a signature in a signed document is invalid";
             else if (sigStatus == SignatureStatus.DynamicFormSigNoChanges)
                 myStatus = "No changes were made to the signed dynamic PDF form";
             else if (sigStatus == SignatureStatus.DocumentSigNoChanges)
                 myStatus = "No changes were made to the signed PDF document";
             else if (sigStatus == SignatureStatus.DynamicFormCertificationSigNoChanges)
                 myStatus = "No changes were made to the certified dynamic PDF form";
             else if (sigStatus == SignatureStatus.DocumentCertificationSigNoChanges)
                 myStatus = "No changes were made to the certified PDF document";
             else if (sigStatus == SignatureStatus.DocSigWithChanges)
                 myStatus = "There were changes to a signed PDF document";
            else if (sigStatus == SignatureStatus.CertificationSigWithChanges)
                 myStatus = "There were changes made to the PDF document.";

             //Get the signature type
             SignatureType sigType = signInfo.getSignatureType();
             String myType = "";

             if (sigType.getType() == PDFSignatureType.AUTHORSIG)
                    myType="Certification";
             else if(sigType.getType() == PDFSignatureType.RECIPIENTSIG)
                    myType="Recipient";

             //Get the identity of the signer
             IdentityInformation signerId = signInfo.getSigner();
             String signerMsg = "";

            if (signerId.getStatus() == IdentityStatus.UNKNOWN)
                signerMsg = "Identity Unknown";
            else if (signerId.getStatus() == IdentityStatus.TRUSTED)
                signerMsg = "Identity Trusted";
            else if (signerId.getStatus() == IdentityStatus.NOTTRUSTED)
                signerMsg = "Identity Not Trusted";

            //Get the Signature properties returned by the Signature service
            SignatureProperties sigProps = signInfo.getSignatureProps();
            String signerName =  sigProps.getSignerName();

           System.out.println("The status of the signature is: "+myStatus +". The signer identity is "+signerMsg +". The signature type is "+myType +". The name of the signer is "+signerName+".");
           }
           catch (Exception ee)
           {
               ee.printStackTrace();
           }
         finally{
             /**
              * always close the PDFDocument object after your processing is done.
              */
             if(inDoc != null){
                 inDoc.close();
             }
             if(adminSession != null && adminSession.isLive()){
                 if(resourceResolver != null){
                     resourceResolver.close();
                 }
                 adminSession.logout();
             }
         }

 }

 /**
   * sets ValidationPreferences
   */
  private static ValidationPreferences getValidationPreferences(){

        ValidationPreferencesImpl prefs = new ValidationPreferencesImpl();
        prefs.setPKIPreferences(getPKIPreferences());

        //set the unlock options for processing an encrypted pdf document, do not set if the input doc is unprotected
        prefs.setUnlockOptions(getUnlockOptions());
        return prefs;

    }

  /**
   * sets PKIPreferences
   */
    private static PKIPreferences getPKIPreferences(){
        PKIPreferences pkiPref = new PKIPreferencesImpl();
        pkiPref.setCRLPreferences(getCRLPreferences());
        pkiPref.setPathPreferences(getPathValidationPreferences());
        pkiPref.setOCSPPreferences(getOCSPPref());
        pkiPref.setTSPPreferences(getTspPref());
        return pkiPref;
    }

    private static TSPPreferences getTspPref(){
     TSPPreferencesImpl tsp = new TSPPreferencesImpl();
     tsp.setRevocationCheck(RevocationCheckStyle.BestEffort);
     return tsp;
    }
    private static OCSPPreferencesImpl getOCSPPref(){
     OCSPPreferencesImpl ocsp = new OCSPPreferencesImpl();
     ocsp.setRevocationCheck(RevocationCheckStyle.BestEffort);
     return ocsp;
    }
    /**
     * sets CRL Preferences
     */
    private static CRLPreferences getCRLPreferences(){

        CRLPreferencesImpl crlPrefs = new CRLPreferencesImpl();
        crlPrefs.setRevocationCheck(RevocationCheckStyle.BestEffort);
        crlPrefs.setGoOnline(true);
        return crlPrefs;
    }

    /**
     *
     * sets PathValidationPreferences
     */
    private static PathValidationPreferences getPathValidationPreferences(){
        PathValidationPreferencesImpl pathPref = new PathValidationPreferencesImpl();
        pathPref.setDoValidation(true);
        return pathPref;

    }

    /**
     * sets Unlock Options for encrypted PDF
     */
    private static UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }

}
```

### Verifica di più firme digitali {#verifying-multiple-digital-signatures}

AEM consente di verificare le firme digitali nei documenti di PDF. Un documento PDF può contenere più firme digitali se è soggetto a un processo aziendale che richiede firme da più firmatari. Ad esempio, una transazione finanziaria richiede le firme sia del responsabile del prestito che del manager. È possibile utilizzare l’API del servizio di firma per verificare tutte le firme all’interno del documento di PDF. Quando si verificano più firme digitali, è possibile controllare lo stato e le proprietà di ogni firma. Prima di considerare attendibile una firma digitale, l&#39;Adobe consiglia di verificarla.

**Sintassi**: `verifyDocument(Document doc, RevocationCheckStyle revocationCheckStyle, VerificationTime verificationTime, ValidationPreferences prefStore, ResourceResolver resourceResolver)`

**Parametri di input**

<table>
 <tbody>
  <tr>
   <th>Parametri</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td><code>inDoc</code><br /> </td>
   <td>Oggetto documento contenente PDF<br /> </td>
  </tr>
  <tr>
   <td><code>revocationCheckStyle</code></td>
   <td>Opzione per gestire il controllo delle revoche dei certificati rilevati durante la convalida</td>
  </tr>
  <tr>
   <td><code>verificationTime</code></td>
   <td>L’ora in cui la firma deve essere convalidata</td>
  </tr>
  <tr>
   <td><code>dssPrefs</code></td>
   <td>Preferenze per controllare varie configurazioni di convalida. Per un documento crittografato, impostare le opzioni di sblocco utilizzando <code>setUnlockOptions()</code></td>
  </tr>
  <tr>
   <td><code>resourceResolver</code></td>
   <td>Risolutore risorse all'archivio attendibilità granite</td>
  </tr>
 </tbody>
</table>

Nel codice di esempio seguente viene utilizzato DocAssuranceService per verificare i campi della firma in un documento PDF già crittografato.

```java
/*************************************************************************
 *
  *
-------------------------------------------------------------
*ADOBE SYSTEMS INCORPORATED
*Copyright 2014 Adobe Systems Incorporated
*All Rights Reserved.

*NOTICE:  Adobe permits you to use, modify, and distribute this file in accordance with the
*terms of the Adobe license agreement accompanying it.  If you have received this file from a
*source other than Adobe, then your use, modification, or distribution of it requires the prior
*written permission of Adobe.
-------------------------------------------------------------------------------------------------

 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.io.IOException;
import java.util.Iterator;
import java.util.List;

import javax.jcr.RepositoryException;
import javax.jcr.Session;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.jcr.api.SlingRepository;
import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceException;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.PDFDocumentVerificationInfo;
import com.adobe.fd.signatures.client.types.PDFSignatureType;
import com.adobe.fd.signatures.client.types.PDFSignatureVerificationInfo;
import com.adobe.fd.signatures.client.types.SignatureProperties;
import com.adobe.fd.signatures.client.types.SignatureStatus;
import com.adobe.fd.signatures.client.types.SignatureType;
import com.adobe.fd.signatures.client.types.VerificationTime;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;
import com.adobe.fd.signatures.pdf.inputs.ValidationPreferences;
import com.adobe.fd.signatures.pdf.inputs.ValidationPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.common.RevocationCheckStyle;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferencesImpl;

/**
 *
 * This class provides a sample code to use {@code DocAssuranceService} to carry out
 * verification of all the signature fields in an already Encrypted PDF Document
 *
 * Assume that a PDF document contains multiple digital signatures as a result of a business process that requires signatures from multiple
 * signers. For example, consider a financial transaction that requires both a loan officer's and a manager's signature. You can use the
 * Signature service Java API or web service API to verify all signatures within the PDF document. When verifying multiple digital signatures,
 * you can check the status and properties of each signature. Before you trust a digital signature, it is recommended that you verify it. It
 * is recommended that you are familiar with verifying a single digital signature.
 *
 * For unprotected document, you are not required to set UnlockOptions in ValidationPreferences
 * PreRequisites - The certificate chain upto the Root Certificate should be uploaded on CQ trust Store
 */

@Component
@Service(value=VerifyEncryptedPDFDoc.class)
public class VerifyEncryptedPDFDoc {

 @Reference
 private DocAssuranceService docAssuranceService;

 @Reference
    private SlingRepository slingRepository;

 @Reference
    private JcrResourceResolverFactory jcrResourceResolverFactory ;

 /**
  *
  * @param inputFile - path to an encrypted pdf document stored at JCR node
  * @throws IOException
  * @throws RepositoryException
  * @throws InvalidArgumentException
  * @throws DocAssuranceException
  */
 public void verifyEncryptedPDFDoc(String inputFile) throws IOException, RepositoryException, InvalidArgumentException, DocAssuranceException{

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  Session adminSession = null;
        ResourceResolver resourceResolver = null;
        try {

          //the resource resolver has to be corresponding to the user who has access to CQ Trust Store
          adminSession = slingRepository.loginAdministrative(null);
             resourceResolver = jcrResourceResolverFactory.getResourceResolver(adminSession);

             RevocationCheckStyle revocationCheckStyle = RevocationCheckStyle.CheckIfAvailable;
             VerificationTime verificationTime = VerificationTime.CURRENT_TIME;
             ValidationPreferences dssPrefs = getValidationPreferences();

             //Verify the digital signature
             PDFDocumentVerificationInfo  docInfo = docAssuranceService.verifyDocument(
                 inDoc,
                 revocationCheckStyle,
                 verificationTime,
                 dssPrefs,
                 resourceResolver);

             //Get a list of all signatures that are in the PDF document
             List allSignatures = docInfo.getVerificationInfos();

           //Create an Iterator object and iterate through
           //the List object
           Iterator<PDFSignatureVerificationInfo> iter = allSignatures.iterator();

           while (iter.hasNext()) {
                  PDFSignatureVerificationInfo signInfo = (PDFSignatureVerificationInfo)iter.next();

                  //Get the Signature Status
                     SignatureStatus sigStatus = signInfo.getStatus();
                     String myStatus="";

                   //Determine the status of the signature
                     if (sigStatus == SignatureStatus.DynamicFormSignatureUnknown)
                         myStatus = "The signatures in the dynamic PDF form are unknown";
                     else if (sigStatus == SignatureStatus.DocumentSignatureUnknown)
                         myStatus = "The signatures in the PDF document are unknown";
                     else if (sigStatus == SignatureStatus.CertifiedDynamicFormSignatureTamper)
                         myStatus = "The signatures in a certified PDF form are valid";
                     else if (sigStatus == SignatureStatus.SignedDynamicFormSignatureTamper)
                         myStatus = "The signatures in a signed dynamic PDF form are valid";
                     else if (sigStatus == SignatureStatus.CertifiedDocumentSignatureTamper)
                         myStatus = "The signatures in a certified PDF document are valid";
                     else if (sigStatus == SignatureStatus.SignedDocumentSignatureTamper)
                         myStatus = "The signatures in a signed PDF document are valid";
                     else if (sigStatus == SignatureStatus.SignatureFormatError)
                         myStatus = "The format of a signature in a signed document is invalid";
                     else if (sigStatus == SignatureStatus.DynamicFormSigNoChanges)
                         myStatus = "No changes were made to the signed dynamic PDF form";
                     else if (sigStatus == SignatureStatus.DocumentSigNoChanges)
                         myStatus = "No changes were made to the signed PDF document";
                     else if (sigStatus == SignatureStatus.DynamicFormCertificationSigNoChanges)
                         myStatus = "No changes were made to the certified dynamic PDF form";
                     else if (sigStatus == SignatureStatus.DocumentCertificationSigNoChanges)
                         myStatus = "No changes were made to the certified PDF document";
                     else if (sigStatus == SignatureStatus.DocSigWithChanges)
                         myStatus = "There were changes to a signed PDF document";
                    else if (sigStatus == SignatureStatus.CertificationSigWithChanges)
                         myStatus = "There were changes made to the PDF document.";

                     //Get the signature type
                    SignatureType sigType = signInfo.getSignatureType();
                    String myType = "";

                    if (sigType.getType() == PDFSignatureType.AUTHORSIG)
                        myType="Certification";
                    else if(sigType.getType() == PDFSignatureType.RECIPIENTSIG)
                        myType="Recipient";

                    //Get the Signature properties returned by the Signature service
                    SignatureProperties sigProps = signInfo.getSignatureProps();
                    String signerName =  sigProps.getSignerName();

                   System.out.println("The status of the signature is: "+myStatus +". The signature type is "+myType +". The name of the signer is "+signerName+".");
               }
           }
           catch (Exception ee)
           {
               ee.printStackTrace();
           }
         finally{
             /**
              * always close the PDFDocument object after your processing is done.
              */
             if(inDoc != null){
                 inDoc.close();
             }
             if(adminSession != null && adminSession.isLive()){
                 if(resourceResolver != null){
                     resourceResolver.close();
                 }
                 adminSession.logout();
             }
         }

 }

 /**
   * sets ValidationPreferences
   */
  private static ValidationPreferences getValidationPreferences(){

        ValidationPreferencesImpl prefs = new ValidationPreferencesImpl();
        prefs.setPKIPreferences(getPKIPreferences());

        //set the unlock options for processing an encrypted pdf document, do not set if the document is unprotected
        prefs.setUnlockOptions(getUnlockOptions());
        return prefs;

    }

  /**
   * sets PKIPreferences
   */
    private static PKIPreferences getPKIPreferences(){
        PKIPreferences pkiPref = new PKIPreferencesImpl();
        pkiPref.setCRLPreferences(getCRLPreferences());
        pkiPref.setPathPreferences(getPathValidationPreferences());
        return pkiPref;
    }

    /**
     * sets CRL Preferences
     */
    private static CRLPreferences getCRLPreferences(){

        CRLPreferencesImpl crlPrefs = new CRLPreferencesImpl();
        crlPrefs.setRevocationCheck(RevocationCheckStyle.CheckIfAvailable);
        crlPrefs.setGoOnline(true);
        return crlPrefs;
    }

    /**
     *
     * sets PathValidationPreferences
     */
    private static PathValidationPreferences getPathValidationPreferences(){
        PathValidationPreferencesImpl pathPref = new PathValidationPreferencesImpl();
        pathPref.setDoValidation(false);
        return pathPref;

    }

    /**
     * sets Unlock Options for encrypted PDF
     */
    private static UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }

}
```

### Rimozione delle firme digitali {#removing-digital-signatures}

È possibile applicare una nuova firma digitale a un campo firma solo dopo aver rimosso la firma digitale precedente. Impossibile sovrascrivere una firma digitale. Se si tenta di applicare una firma digitale a un campo firma che contiene già una firma, si verifica un&#39;eccezione.

**Sintassi**: `clearSignatureField(Document inDoc, String signatureFieldName, UnlockOptions unlockOptions)`

**Parametri di input**

<table>
 <tbody>
  <tr>
   <th>Parametri</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td><code>inDoc</code><br /> </td>
   <td>Oggetto documento contenente PDF<br /> </td>
  </tr>
  <tr>
   <td><code>signatureFieldName</code></td>
   <td>Nome del campo firma<br /> </td>
  </tr>
  <tr>
   <td><code>unlockOptions</code><br /> </td>
   <td>Include i parametri necessari per sbloccare un file crittografato. Questa opzione è necessaria solo se il file è crittografato<br /> </td>
  </tr>
 </tbody>
</table>

Nell&#39;esempio di codice Java seguente viene rimossa una firma digitale da un campo di firma.

```java
/*************************************************************************
 *
  *
-------------------------------------------------------------
*ADOBE SYSTEMS INCORPORATED
*Copyright 2014 Adobe Systems Incorporated
*All Rights Reserved.

*NOTICE:  Adobe permits you to use, modify, and distribute this file in accordance with the
*terms of the Adobe license agreement accompanying it.  If you have received this file
*from a source other than Adobe, then your use, modification, or distribution of it requires
*the prior written permission of Adobe.
-------------------------------------------------------------------------------------------------

 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.io.IOException;

import javax.jcr.RepositoryException;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceException;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.client.types.exceptions.PDFOperationException;
import com.adobe.fd.signatures.client.types.exceptions.PermissionsException;
import com.adobe.fd.signatures.client.types.exceptions.SignaturesOtherException;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;

/**
 * Digital signatures must be removed from a signature field before a newer digital signature can be applied.
 * A digital signature cannot be overwritten.
 * If you attempt to apply a digital signature to a signature field that contains a signature, an exception occurs
 *
 *The following Java code example removes a digital signature from a signature field named SignatureField1.
 *The name of the PDF file that contain the signature field is LoanSigned.pdf
 */

@Component
@Service(value=ClearSignatureField.class)
public class ClearSignatureField {

 @Reference
 private DocAssuranceService docAssuranceService;
 /**
  *
  * @param inputFile - path to an encrypted pdf document stored at disk
  * @param outFile - path where the output file has to be saved
  * @throws Exception
  */
 public void clearSignatureField(String inputFile, String outFile) throws Exception{

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

        //Specify the name of the signature field
        String fieldName = "SignatureField1";

        //Clear the signature field
        //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
        Document outPDF = docAssuranceService.clearSignatureField(inDoc,fieldName,null);

        //save the outPDF
        outPDF.copyToFile(new File(outFile));
 }

  /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }
}
```

### Recupero campo firma di certificazione {#getting-certifying-signature-field}

È possibile recuperare i nomi di tutti i campi firma presenti in un documento PDF che si desidera firmare o certificare. Se non si è certi dei nomi dei campi firma presenti in un documento PDF o si desidera verificarli, è possibile recuperarli a livello di programmazione. Il servizio di firma restituisce il nome completo del campo della firma, ad esempio `form1[0].grantApplication[0].page1[0].SignatureField1[0]`.

**Sintassi**: `getCertifyingSignatureField(Document inDoc, UnlockOptions unlockOptions)`

**Parametri di input**

<table>
 <tbody>
  <tr>
   <th>Parametri</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td><code>inDoc</code><br /> </td>
   <td>Oggetto documento contenente PDF.<br /> </td>
  </tr>
  <tr>
   <td><code>UnlockOptions</code></td>
   <td>UnlockOptions include i parametri necessari per sbloccare un file crittografato. Questa opzione è necessaria solo se il file è crittografato.</td>
  </tr>
 </tbody>
</table>

Esempio Nell&#39;esempio di codice Java riportato di seguito viene recuperato il campo della firma utilizzato per certificare il documento.

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * ___________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.util.Iterator;
import java.util.List;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.PDFSignatureField;
import com.adobe.fd.signatures.client.types.exceptions.DuplicateSignatureFieldException;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.client.types.exceptions.PDFOperationException;
import com.adobe.fd.signatures.client.types.exceptions.PermissionsException;
import com.adobe.fd.signatures.client.types.exceptions.SignaturesBaseException;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;

/**
 * You can retrieve the names of all signature fields that are in a PDF document that you want to sign or certify.
 * If you are unsure of the signature field names that are in a PDF document or you want to verify the names, you can
 * programmatically retrieve them. The Signature service returns the fully qualified name of the signature field, such as
 * form1[0].grantApplication[0].page1[0].SignatureField1[0].
 *
 * The following Java code example retrieves the ignature field that was used to certify the document.
 */

@Component
@Service(value=GetCertifyingSignatureField.class)
public class GetCertifyingSignatureField {

 @Reference
 private DocAssuranceService docAssuranceService;

 /**
  *
  * @param inputFile - path to the pdf document stored at disk
  * @throws SignaturesBaseException
  * @throws DuplicateSignatureFieldException
  * @throws PermissionsException
  * @throws PDFOperationException
  * @throws InvalidArgumentException
  *
  */
 public void getCertifyingSignatureField(String inputFile) throws Exception {

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  //Retrieve signature data for a given signature field.
  //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
        PDFSignatureField pdfSignature = docAssuranceService.getCertifyingSignatureField(inDoc,null);

   }

  /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }
}
```

### Recupero tipo di crittografia PDF {#getting-pdf-encryption-type}

È possibile recuperare i nomi di tutti i campi firma presenti in un documento PDF che si desidera firmare o certificare. Se non si è certi dei nomi dei campi firma presenti in un documento PDF o si desidera verificarli, è possibile recuperarli a livello di programmazione. Il servizio di firma restituisce il nome completo del campo della firma, ad esempio `asform1[0].grantApplication[0].page1[0].SignatureField1[0]`.

**Sintassi**: `void getPDFEncryption(Document inDoc)`

**Parametri di input**

<table>
 <tbody>
  <tr>
   <th>Parametri</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td><code>inDoc</code><br /> </td>
   <td>Documento fornito come input. Può essere crittografato o meno.<br /> </td>
  </tr>
 </tbody>
</table>

Esempio Nell&#39;esempio di codice Java riportato di seguito vengono recuperate le informazioni sulla firma per il campo di firma specificato in un documento PDF.

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * ___________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.util.Iterator;
import java.util.List;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.PDFSignatureField;
import com.adobe.fd.signatures.client.types.exceptions.DuplicateSignatureFieldException;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.client.types.exceptions.PDFOperationException;
import com.adobe.fd.signatures.client.types.exceptions.PermissionsException;
import com.adobe.fd.signatures.client.types.exceptions.SignaturesBaseException;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;
import com.adobe.fd.encryption.client.EncryptionTypeResult;

/**
 * You can retrieve the names of all signature fields that are in a PDF document that you want to sign or certify.
 * If you are unsure of the signature field names that are in a PDF document or you want to verify the names, you can
 * programmatically retrieve them. The Signature service returns the fully qualified name of the signature field, such as
 * form1[0].grantApplication[0].page1[0].SignatureField1[0].
 *
 * The following Java code example retrieves the Signature Info for the given signature field in a PDF document.
 */

@Component
@Service(value=GetPDFEncryption.class)
public class GetPDFEncryption {

 @Reference
 private DocAssuranceService docAssuranceService;

 /**
  *
  * @param inputFile - path to the pdf document stored at disk
  * @throws SignaturesBaseException
  * @throws DuplicateSignatureFieldException
  * @throws PermissionsException
  * @throws PDFOperationException
  * @throws InvalidArgumentException
  *
  */
 public void getPDFEncryption(String inputFile) throws Exception {

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  //Retrieve signature data for a given signature field.
  //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
        EncryptionTypeResult encryptionTypeResult = docAssuranceService.getPDFEncryption(inDoc);

   }

  /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }
}
```

### Rimozione della crittografia della password da PDF {#removing-password-encryption-from-pdf}

Rimuovi la crittografia basata su password da un documento PDF per consentire agli utenti di aprire il documento PDF in Adobe Reader o Acrobat senza dover specificare una password. Dopo aver rimosso la crittografia basata su password da un documento PDF, il documento non è più protetto.

**Sintassi**: `Document removePDFPasswordSecurity (Document inDoc,String password)`

**Parametri di input**

<table>
 <tbody>
  <tr>
   <th>Parametri</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td><code>inDoc</code><br /> </td>
   <td>Documento fornito come input. Deve essere protetto da password.<br /> </td>
  </tr>
  <tr>
   <td><code>password</code><br /> </td>
   <td>Un documento aperto o una password di autorizzazione da utilizzare per rimuovere la protezione dal documento.<br /> </td>
  </tr>
 </tbody>
</table>

Nell&#39;esempio di codice seguente viene rimossa la crittografia basata su password da un documento PDF.

```java
    package com.adobe.docassurance.samples;

    import java.io.File;
    import java.io.FileNotFoundException;
    import org.apache.felix.scr.annotations.Component;
    import org.apache.felix.scr.annotations.Reference;
    import org.apache.felix.scr.annotations.Service;
    import org.apache.sling.jcr.api.SlingRepository;

    import com.adobe.aemfd.docmanager.Document;
    import com.adobe.fd.docassurance.client.api.DocAssuranceService;

    /**
    * The following Java code example removes password-based encryption from a PDF document.
    * The master password value used to remove password-based encryption is PermissionPassword
    *
    */
    @Component(enabled=true,immediate=true)
    @Service(value=RemovePasswordEncryption.class)
    public class RemovePasswordEncryption {

    // Create reference for DocAssuranceService
    @Reference
    private DocAssuranceService docAssuranceService;

    @Reference
        private SlingRepository slingRepository;

    /**
    * The below sample code demonstrates removing password encryption from a PDF using AEM EncryptionService.
    *
    * @param inFilePath  path of the input PDF File
    * Path Example for Files stored at hardDisk = "C:/temp/test.pdf"
    *
    * @param outFilePath path where the output PDF File needs to be saved
    * Path Example for Files stored at hardDisk = "C:/temp/test_out.pdf"
    * @throws Exception
    */
    public void removePasswordEncryption(String inputFile, String outputFile) throws Exception {

    File inFile = new File(inputFile);
    Document inDoc = new Document(inFile);

    File outFile = new File(outputFile);
    Document outDoc = null;

        try{

        String password = "PermissionPassword"; //master password with which the pdf was encrypted
                    //in case if the pdf is encrypted only with user password, specify the
                    //user password
        //Remove password-based encryption from the PDF document
        outDoc = docAssuranceService.removePDFPasswordSecurity(inDoc,password);

        }finally{
                    /**
                    * always close the PDFDocument object after your processing is done.
                    */
                    if(inDoc != null){
                        inDoc.close();
                    }

            }

            outDoc.copyToFile(outFile);

    }

    }
```

### Rimozione della crittografia del certificato {#removing-certificate-encryption}

È possibile rimuovere la crittografia basata su certificato da un documento PDF in modo che gli utenti possano aprire il documento PDF in Adobe Reader o Acrobat. Per rimuovere la crittografia da un documento PDF crittografato con un certificato, fare riferimento a una chiave privata. Una volta rimossa da un documento PDF, la crittografia non è più sicura.

**Sintassi**: `removePDFCertificateSecurity(Document inDoc, String alias, ResourceResolver resourceResolver)`

**Parametri di input**

<table>
 <tbody>
  <tr>
   <th>Parametri</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td><code>inDoc</code><br /> </td>
   <td>Oggetto Document che rappresenta il documento PDF crittografato con certificato.<br /> </td>
  </tr>
  <tr>
   <td><code>alias</code><br /> </td>
   <td>Alias che corrisponde alla chiave nell'archivio fonti attendibili Granite utilizzata per rimuovere la crittografia basata su certificati dal documento PDF.<br /> </td>
  </tr>
  <tr>
   <td><code>ResourceResolver</code></td>
   <td>ResourceResolver per accedere all'archivio chiavi di un utente specifico per recuperare le credenziali.</td>
  </tr>
 </tbody>
</table>

Nell&#39;esempio di codice Java seguente viene rimossa la crittografia basata su certificato da un documento PDF.

```java
    package com.adobe.docassurance.samples;

    import java.io.File;

    import javax.jcr.Session;

    import org.apache.felix.scr.annotations.Component;
    import org.apache.felix.scr.annotations.Reference;
    import org.apache.felix.scr.annotations.Service;
    import org.apache.sling.api.resource.ResourceResolver;
    import org.apache.sling.jcr.api.SlingRepository;
    import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

    import com.adobe.aemfd.docmanager.Document;
    import com.adobe.fd.docassurance.client.api.DocAssuranceService;

    /**
    * The following Java code example removes certificate-based encryption from a PDF document
    *
    */
    @Component(enabled=true,immediate=true)
    @Service(value=RemovePKIEncryption.class)
    public class RemovePKIEncryption {

    // Create reference for docAssuranceServiceInterface
    @Reference
    private DocAssuranceService docAssuranceService;

    @Reference
        private SlingRepository slingRepository;

    @Reference
        private JcrResourceResolverFactory jcrResourceResolverFactory ;

    /**
    * The below sample code demonstrates encrypting PDF with Password using AEM docAssuranceService.
    *
    * @param inFilePath  path of the input PDF File
    * Path Example for Files stored at hardDisk = "C:/temp/test.pdf"
    *
    * @param outFilePath path where the output PDF File needs to be saved
    * Path Example for Files stored at hardDisk = "C:/temp/test_Encrypted.pdf"
    *
    * @throws Exception
    */
    public void removePKIEncryption(String inputFile, String outputFile) throws Exception {

    File inFile = new File(inputFile);
    Document inDoc = new Document(inFile);

    File outFile = new File(outputFile);
    Document outDoc = null;

            Session adminSession = null;
            ResourceResolver resourceResolver = null;
            try{
        adminSession = slingRepository.loginAdministrative(null);
        resourceResolver = jcrResourceResolverFactory.getResourceResolver(adminSession);

        //Remove certificate-based encryption from the PDF document
        /**
        * Here the alias("encryption") of the private credential stored in the keystore of the
        * user has been provided with the user's resource resolver
        */
        outDoc = docAssuranceService.removePDFCertificateSecurity(inDoc, "encryption",resourceResolver);

            }catch(Exception e){

            // TODO Auto-generated catch block
            }finally{
                /**
                * always close the PDFDocument object after your processing is done.
                */
                if(inDoc != null){
                    inDoc.close();
                }
                if(adminSession != null && adminSession.isLive()){
                    if(resourceResolver != null){
                        resourceResolver.close();
                    }
                    adminSession.logout();
                }
            }

            outDoc.copyToFile(outFile);
    }

    }
```

## Servizio di output {#output-service}

Il servizio di output fornisce API per il rendering di un file XDP nei formati .pdf, .pcl, .zpl e .ps. Il servizio supporta le seguenti API:

* **[generatePDFOutput](/help/forms/using/aem-document-services-programmatically.md#p-generatepdfoutput-p):** Genera un documento PDF unendo una struttura di modulo con i dati memorizzati in un percorso di rete, un file system locale o un percorso HTTP come valori letterali.

* **[generatePDFOutput](/help/forms/using/aem-document-services-programmatically.md#p-generatepdfoutput-p):** Genera un documento PDF unendo una struttura di modulo con i dati memorizzati in un&#39;applicazione.
* **[generatePDFOutputBatch](/help/forms/using/aem-document-services-programmatically.md#p-generatepdfoutputbatch-p):** Unisce una struttura di modulo ai dati per creare un documento PDF. Facoltativamente, genera un file di metadati per ogni record o salva l&#39;output in un file PDF.
* **[generatePrintedOutput](/help/forms/using/aem-document-services-programmatically.md#p-generateprintedoutput-p):** Genera un output PCL, PostScript o ZPL da una struttura di modulo e un file di dati archiviato in un percorso di rete, in un file system locale o in un percorso HTTP come valori letterali.

* **[generatePrintedOutput](/help/forms/using/aem-document-services-programmatically.md#p-generateprintedoutput-p):** Genera un output PCL, PostScript e ZPL da un progetto di modulo e da un file di dati archiviati in un&#39;applicazione.

### generatePDFOutput {#generatepdfoutput}

L’API generatePDFOutput genera un documento PDF unendo una progettazione di moduli con i dati. Facoltativamente, genera un file di metadati per ogni record o salva l&#39;output in un file PDF. Utilizza l’API generatePDFOutput per le progettazioni dei moduli o i dati memorizzati in un percorso di rete, in un file system locale o in un percorso HTTP come valori letterali. Se la struttura del modulo e i dati XML sono memorizzati in un&#39;applicazione, utilizzare [generatePDFOutput](/help/forms/using/aem-document-services-programmatically.md#p-generatepdfoutput-p) API.

**Sintassi:** `Document generatePDFOutput(String uriOrFileName, Document data, PDFOutputOptions options);`

#### Parametri di input {#input-parameters}

<table>
 <tbody>
  <tr>
   <th>Parametri</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td>uriOrFileName</td>
   <td>Specifica il percorso e il nome del file di input. Il file può essere di tipo PDF o XDP. Se si specifica solo il nome del file, il file viene letto in relazione al contentRoot specificato nelle opzioni.</td>
  </tr>
  <tr>
   <td>dati</td>
   <td>File XML contenente i dati uniti al documento PDF.<br /> </td>
  </tr>
  <tr>
   <td>opzioni</td>
   <td>Specifica i valori delle variabili contentRoot, locale, AcrobatVersion, linearizedPDF e taggedPDF. Il parametro options accetta un oggetto di tipo PDFOutputOptions. <br /> </td>
  </tr>
 </tbody>
</table>

Esempio Nell&#39;esempio di codice Java riportato di seguito viene generato un documento PDF unendo una struttura di modulo con i dati memorizzati in un file XML.

```java
    @Reference private OutputService outputService;

    private File generatePDFOutput(String contentRoot,File inputXML,String templateStr,String acrobatVersion,String tagged,String linearized, String locale) {

    String outputFolder="C:/Output";

    Document doc=null;

    try {

            PDFOutputOptions option = new PDFOutputOptions();         option.setContentRoot(contentRoot);         if(acrobatVersion.equalsIgnoreCase("Acrobat_10"))

            {

                option.setAcrobatVersion(com.adobe.fd.output.api.AcrobatVersion.Acrobat_10);

            } else if(acrobatVersion.equalsIgnoreCase("Acrobat_10_1")) {

                option.setAcrobatVersion(com.adobe.fd.output.api.AcrobatVersion.Acrobat_10_1);

            } else if(acrobatVersion.equalsIgnoreCase("Acrobat_11")) {             option.setAcrobatVersion(com.adobe.fd.output.api.AcrobatVersion.Acrobat_11);

            }

            if (tagged.equalsIgnoreCase("true") ) {

                option.setTaggedPDF(true );

            }

            if (linearized.equalsIgnoreCase("true") ) {

                option.setTaggedPDF(true );

            }

            if(locale!=null)

            {

                option.setLocale(locale);

            }

            InputStream in = new FileInputStream(inputXML);

            doc = outputService.generatePDFOutput(templateStr,new Document(in),option);         File toSave = new File(outputFolder+"Output.pdf");

            doc.copyToFile(toSave);

            return toSave;

        } catch (OutputServiceException e) {

            e.printStackTrace();

        }catch (FileNotFoundException e) {

            e.printStackTrace();

        } catch (IOException e) {

            e.printStackTrace();

        }finally{

                    doc.dispose();

        }

        return null;

    }
```

### generatePDFOutput {#generatepdfoutput-1}

L’API generatePDFOutput genera un documento PDF unendo una progettazione di moduli con i dati. Facoltativamente, genera un file di metadati per ogni record o salva l’output in un file PDF. Utilizza l’API generatePrintedOutput per le progettazioni dei moduli o i dati memorizzati in un’applicazione. Se la struttura del modulo e i dati XML vengono memorizzati in un percorso di rete, in locale o in un percorso HTTP come valori letterali, utilizzare [generatePDFOutput](/help/forms/using/aem-document-services-programmatically.md#p-generatepdfoutput-p) API.

**Sintassi:** `Document generatePDFOutput(Document inputdocument, Document data, PDFOutputOptions options)`

#### Parametro di input {#input-parameter}

<table>
 <tbody>
  <tr>
   <th>Parametri</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td>Inputdocument<br /> </td>
   <td>Specifica il percorso e il nome del file di input. Il file può essere di tipo PDF o XDP. Se si specifica solo il nome del file, il file viene letto in relazione al contentRoot specificato nelle opzioni. <br /> </td>
  </tr>
  <tr>
   <td>dati</td>
   <td>File XML contenente i dati uniti al documento PDF.<br /> </td>
  </tr>
  <tr>
   <td>opzioni</td>
   <td>Specifica i valori delle variabili contentRoot, locale, AcrobatVersion, linearizedPDF e taggedPDF. Il parametro options accetta oggetti di tipo PDFOutputOptions.</td>
  </tr>
 </tbody>
</table>

Esempio Nell&#39;esempio di codice Java riportato di seguito viene generato un documento PDF unendo una struttura di modulo con i dati memorizzati in un file XML.

```java
    @Reference private OutputService outputService;

    private File generatePDFOutput2(String contentRoot, File inputXML, File templateStr, String acrobatVersion, String tagged, String linearized, String locale) {

    String outputFolder="C:/Output";

    Document doc=null;

        try {

                PDFOutputOptions option = new PDFOutputOptions();             option.setContentRoot(contentRoot);
                if(locale!=null)

                {

                    option.setLocale(locale);

                }

                if(acrobatVersion.equalsIgnoreCase("Acrobat_10"))

                {

                    option.setAcrobatVersion(com.adobe.fd.output.api.AcrobatVersion.Acrobat_10);

                } else if(acrobatVersion.equalsIgnoreCase("Acrobat_10_1")) {                 option.setAcrobatVersion(com.adobe.fd.output.api.AcrobatVersion.Acrobat_10_1);

                } else if(acrobatVersion.equalsIgnoreCase("Acrobat_11")) {                 option.setAcrobatVersion(com.adobe.fd.output.api.AcrobatVersion.Acrobat_11);

                }

                if (tagged.equalsIgnoreCase("true") ) {

                    option.setTaggedPDF(true );

                }

                if (linearized.equalsIgnoreCase("true") ) {

                    option.setTaggedPDF(true );

                }

                InputStream inputXMLStream = new FileInputStream(inputXML);

                InputStream templateStream = new FileInputStream(templateStr);;

                doc = outputService.generatePDFOutput(new Document(templateStream),new             Document(inputXMLStream),option);

                        File toSave = new File(outputFolder,"Output.pdf");

                        doc.copyToFile(toSave);

                        return toSave;

                    } catch (OutputServiceException e) {

                            e.printStackTrace();

                }catch (FileNotFoundException e) {

                            e.printStackTrace();

                } catch (IOException e) {

                            e.printStackTrace();

                }finally{

                                doc.dispose();

                }

                    return null;

    }
```

### generatePDFOutputBatch {#generatepdfoutputbatch}

Unisce una struttura di modulo ai dati per creare un documento PDF. Facoltativamente, genera un file di metadati per ogni record o salva l&#39;output in un file PDF. Utilizza l’API generatePDFOutputBatch per progettare moduli o dati memorizzati in un percorso di rete, in un file system locale o in un percorso HTTP come valori letterali.

**Sintassi:** `BatchResult generatePDFOutputBatch(Map templates, Map data, PDFOutputOptions options, BatchOptions batchOptions);`

#### Parametri di input {#input-parameters-1}

<table>
 <tbody>
  <tr>
   <th>Parametro</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td>modelli<br /> </td>
   <td>Specifica la mappa del nome file della chiave e del modello.<br /> </td>
  </tr>
  <tr>
   <td>dati</td>
   <td>Specifica la mappa della chiave e del documento di dati. Se la chiave non è null, viene eseguito il rendering del documento dati con il modello per la chiave corrispondente specificato nella mappa dei modelli. </td>
  </tr>
  <tr>
   <td>opzioni</td>
   <td>Specifica i valori delle variabili contentRoot, locale, AcrobatVersion, linearizedPDF e taggedPDF. Il parametro options accetta oggetti di tipo PDFOutputOptions.</td>
  </tr>
  <tr>
   <td>batchOptions</td>
   <td>Specifica il valore della variabile <code>generateManyFiles</code>. Impostare il flag generateManyFiles per generare più file. Il parametro options accetta oggetti di tipo BatchOptions.</td>
  </tr>
 </tbody>
</table>

Esempio Nell&#39;esempio di codice Java riportato di seguito viene generata la creazione di documenti PDF mediante l&#39;unione di progettazioni di moduli con dati memorizzati in un file XML.

```java
private ArrayList generatePDFBatch(String contentRoot,String multipleFiles) {

String outputFolder="C:/Output";

    try {

        PDFOutputOptions option = new PDFOutputOptions();         option.setContentRoot(contentRoot);

        Map templates = new LinkedHashMap();

        Map data = new LinkedHashMap();

        String template1 = "PurchaseOrder.xdp"; String template2 = "CardApp.xdp";         templates.put(template1.substring(0, template1.indexOf(".xdp")),template1);         templates.put(template1.substring(0, template2.indexOf(".xdp")),template2);

        File inputXML1 = new File("c:/InputFolder/PurchaseOrder.xml");

        File inputXML2 = new File("c:/InputFolder/CardApp.xml");

        InputStream in1 = new FileInputStream(inputXML1);

        InputStream in2 = new FileInputStream(inputXML2);

        data.put(template1.substring(0, template1.indexOf(".xdp")),new         Document((in1))); data.put(template1.substring(0,         template1.indexOf(".xdp")),new Document((in2))); BatchOptions bo = new         BatchOptions(); BatchResult ret=null;         if(multipleFiles.equalsIgnoreCase("true"))

        {

            bo.setGenerateManyFiles(true);

            ret = outputService.generatePDFOutputBatch(templates, data, option, bo);

        } else {

            ret = outputService.generatePDFOutputBatch(templates, data, option, new             BatchOptions());

        }

        ArrayList outputs = new ArrayList();

        int counter=0;

        if(ret.getMetaDataDoc() !=null ){

        File toSave = new File(outputFolder+"Output.xml");

        ret.getMetaDataDoc().copyToFile(toSave);

        outputs.add(toSave);

        List<Document> list = ret.getGeneratedDocs();

        for(Document doc:list){

        File toSave = new File(outputFolder,"Output"+"_"+counter+".pdf");         doc.copyToFile(toSave);                    outputs.add(toSave);

        counter++;

        doc.dispose();

        }

        return outputs;

       } catch (OutputServiceException e) {

            e.printStackTrace();

       }catch (FileNotFoundException e) {

            e.printStackTrace();

       }catch (IOException e) {

            e.printStackTrace();

       }

       return null;

}
```

### generatePrintedOutput {#generateprintedoutput}

Genera un output PCL, PostScript e ZPL da un file di progettazione e dati di un modulo. Il file di dati viene unito alla struttura del modulo e formattato per la stampa. È possibile inviare l&#39;output direttamente a una stampante o salvarlo come file. Utilizza l’API generatePrintedOutput per le progettazioni dei moduli o i dati memorizzati in un’applicazione.

**Sintassi:** `Document generatePrintedOutput(String uriOrFileName, Document data, PrintedOutputOptions);`

#### Parametri di input {#input-parameters-2}

<table>
 <tbody>
  <tr>
   <th>Parametro</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td>uriOrFileName<br /> </td>
   <td>Specifica il percorso e il nome del file di input. Se si specifica solo il nome del file, il file viene letto in relazione al contentRoot specificato nelle opzioni. Il file può essere di tipo PDF o XDP.<br /> </td>
  </tr>
  <tr>
   <td>dati</td>
   <td>File XML contenente dati uniti a documenti PDF.<br /> </td>
  </tr>
  <tr>
   <td>opzioni</td>
   <td>Specifica i valori delle variabili contentRoot, locale, AcrobatVersion, linearizedPDF e taggedPDF. Il parametro options accetta un oggetto di tipo PrintedOutputOptions.<br /> </td>
  </tr>
 </tbody>
</table>

Nell&#39;esempio di codice Java riportato di seguito viene generato un output PCL, PostScript e ZPL da un progetto di modulo e da dati. Il tipo di output dipende dal valore passato al `printConfig`parametro.

```java
@Reference private OutputService outputService;

private File generatePrintedOutput(String contentRoot,File inputXML,String templateStr,String printConfig) {

String outputFolder="C:/Output";

Document doc=null;

    try {

            PrintedOutputOptions options = new PrintedOutputOptions();                           options.setContentRoot(contentRoot);

            if(printConfig.equalsIgnoreCase("ps"))

            {

                options.setPrintConfig(PrintConfig.PS_PLAIN);

            }else if(printConfig.equalsIgnoreCase("pcl")) {

                            options.setPrintConfig(PrintConfig.HP_PCL_5e);

                     }else if(printConfig.equalsIgnoreCase("zpl")) {                                                                       options.setPrintConfig(PrintConfig.ZPL300);

            }

            InputStream in = new FileInputStream(inputXML);

            doc = outputService.generatePrintedOutput(templateStr,new             Document(in),options);

            in.close();

            File toSave = new File(outputFolder,"Output"+"."+printConfig);             doc.copyToFile(toSave);

            return  toSave;

        } catch (OutputServiceException e) {

             e.printStackTrace();

        }catch (FileNotFoundException e) {

             e.printStackTrace();

        }catch (IOException e) {

             e.printStackTrace();

        }finally{

             doc.dispose();

        }

        return null;

}
```

### generatePrintedOutput {#generateprintedoutput-1}

Genera un output PCL, PostScript e ZPL in base alla progettazione del modulo e al file di dati. Il file di dati viene unito alla struttura del modulo e formattato per la stampa. L&#39;output può essere inviato direttamente a una stampante o salvato come file. Utilizza l’API generatePrintedOutput per le progettazioni dei moduli o i dati memorizzati in un’applicazione.

**Sintassi:** `Document generatePrintedOutput(Document inputdocument, Document data, PrintedOutputOptions);`

#### Parametri di input {#input-parameters-3}

<table>
 <tbody>
  <tr>
   <th>Parametro</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td>Inputdocument<br /> </td>
   <td>Specifica il percorso e il nome del file di input. Se si specifica solo il nome del file, il file viene letto in relazione al contentRoot specificato nelle opzioni. Il file può essere di tipo XDP. </td>
  </tr>
  <tr>
   <td>dati</td>
   <td>File XML contenente dati uniti a documenti PDF.<br /> </td>
  </tr>
  <tr>
   <td>opzioni</td>
   <td>Questo oggetto viene utilizzato per impostare i valori di contentRoot, locale, printConfig, copy e paginationOverride. Il parametro options accetta un oggetto di tipo PrintedOutputOptions.<br /> </td>
  </tr>
 </tbody>
</table>

Nell&#39;esempio di codice Java riportato di seguito viene generato un output PCL, PostScript e ZPL da un progetto di modulo e da dati. Il tipo di output dipende dal valore passato al `printConfig`parametro.

```java
@Reference private OutputService outputService;

private File generatePrintedOutput2(File  inputXML,File templateStr,String printConfig) {

String outputFolder="C:/Output";

Document doc=null;

       try {

            PrintedOutputOptions options = new PrintedOutputOptions();             if(printConfig.equalsIgnoreCase("ps"))

            {

                options.setPrintConfig(PrintConfig.PS_PLAIN);

            }else if(printConfig.equalsIgnoreCase("pcl")) {                                   options.setPrintConfig(PrintConfig.HP_PCL_5e);

            }else if(printConfig.equalsIgnoreCase("zpl")) {                                                                       options.setPrintConfig(PrintConfig.ZPL300);

                             }

            InputStream inputXMlStream = new FileInputStream(inputXML);

            InputStream templateStream = new FileInputStream(templateStr); doc =             outputService.generatePrintedOutput(new Document(templateStream),new             Document(inputXMlStream),options);

            File toSave = new File(outputFolder,"Output"+"."+printConfig);             doc.copyToFile(toSave);

            return toSave;

            } catch (OutputServiceException e) {

                e.printStackTrace();

            }catch (FileNotFoundException e) {

                e.printStackTrace();

            } catch (IOException e) {

                e.printStackTrace();

            }finally{

                doc.dispose();

            }

            return null;

}
```

### generatePrintedOutputBatch {#generateprintedoutputbatch}

Genera un documento in formato PS, PCL e ZPL unendo un progetto di modulo con i dati. Facoltativamente, genera un file di metadati per ogni record o salva l’output in un file PDF. Utilizza l’API generatePrintedOutputBatch per le progettazioni dei moduli o i dati memorizzati in un percorso di rete, in un file system locale o in un percorso HTTP come valori letterali.

**Sintassi`:`** `BatchResult generatePrintedOutputBatch(Map templates, Map data, PrintedOutputOptions options, BatchOptions batchOptions);`

#### Parametri di input {#input-parameters-4}

<table>
 <tbody>
  <tr>
   <th>Parametro</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td>modelli<br /> </td>
   <td>Specifica la mappa del nome file della chiave e del modello.<br /> </td>
  </tr>
  <tr>
   <td>dati</td>
   <td>Specifica la mappa della chiave e del documento di dati. Se la chiave non è null, il documento di dati viene renderizzato con il modello per la chiave corrispondente nella mappa dei modelli.<br /> </td>
  </tr>
  <tr>
   <td>opzioni</td>
   <td>Specifica un oggetto di tipo PrintedOutputOptions. Questo oggetto viene utilizzato per impostare i valori di contentRoot, locale, printConfig, copy, paginationOverride.<br /> </td>
  </tr>
  <tr>
   <td>batchOptions</td>
   <td>Specifica il valore della variabile generateManyFiles. Impostare il flag generateManyFiles per generare più file. Il parametro options accetta oggetti di tipo BatchOptions.<br /> </td>
  </tr>
 </tbody>
</table>

Nell&#39;esempio di codice Java riportato di seguito vengono generati output PCL, PostScript e ZPL in batch da più modelli di progettazione di moduli e file di dati. Il tipo di output dipende dal valore passato al `printConfig`parametro.

```java
@Reference private OutputService outputService;

private ArrayList generatePrintedOutputBatch(String contentRoot,String multipleFiles,String printConfig) {

String outputFolder="C:/Output";

        try {

                PrintedOutputOptions option = new PrintedOutputOptions();                 option.setContentRoot(contentRoot);

                Map templates = new LinkedHashMap();

                Map data = new LinkedHashMap();

                String template1 = "PurchaseOrder.xdp";

                String template2 = "CardApp.xdp";

                templates.put(template1.substring(0,                 template1.indexOf(".xdp")),template1);                 templates.put(template1.substring(0,                 template2.indexOf(".xdp")),template2);

                File inputXML1 = new                                   File("c:/InputFolder/PurchaseOrder.xml");

                File inputXML2 = new File("c:/InputFolder/CardApp.xml");

                InputStream in1 = new FileInputStream(inputXML1);

                InputStream in2 = new FileInputStream(inputXML2);                  data.put(template1.substring(0,                     template1.indexOf(".xdp")),new Document((in1)));

                 data.put(template2.substring(0,                     template2.indexOf(".xdp")),new Document((in2)));

                 if(printConfig.equalsIgnoreCase("ps"))

                 {

                    option.setPrintConfig(PrintConfig.PS_PLAIN);

                 } else if(printConfig.equalsIgnoreCase("pcl"))

                 {

                    option.setPrintConfig(PrintConfig.HP_PCL_5e);

                 } else if(printConfig.equalsIgnoreCase("zpl")){

                                         option.setPrintConfig(PrintConfig.ZPL300);

                 }

                 option.setContentRoot(contentRoot);

                 BatchOptions bo = new BatchOptions();

                 BatchResult ret =                             outputService.generatePrintedOutputBatch(temp                                    lates, data, option, new                                                     BatchOptions());

                 ArrayList outputs = new ArrayList();

                 int counter=0;

                 if(ret.getMetaDataDoc() !=null ){

                 File toSave = new File(outputFolder,"Output"+".xml");                    ret.getMetaDataDoc().copyToFile(toSave);

                 outputs.add(toSave);

                 List<Document> list = ret.getGeneratedDocs();

                 for(Document doc:list){

                 File toSave = new                                                               File(outputFolder,"Output"+"_"+counter+".                                        "+printConfig);                                    doc.copyToFile(toSave);

                 outputs.add(toSave);

                 counter++;

                 doc.dispose();

                 }

                 return outputs;

          }

            catch (OutputServiceException e) {

                e.printStackTrace();

          }catch (FileNotFoundException e) {

                e.printStackTrace();

          } catch (IOException e) {

                e.printStackTrace();

          }

            return null;

  }
```

## Servizio Forms {#forms-service}

Il servizio Forms fornisce API per importare ed esportare dati da e verso un modulo interattivo di PDF. Un modulo PDF interattivo è un documento PDF che contiene uno o più campi utilizzati per visualizzare e raccogliere informazioni dagli utenti. Il servizio supporta le seguenti API:

* **[exportData](/help/forms/using/aem-document-services-programmatically.md#p-exportdata-p):** esporta dati da un modulo PDF.
* **[importData](/help/forms/using/aem-document-services-programmatically.md#p-importdata-p):** importa i dati in un modulo PDF interattivo.

### exportData {#exportdata}

Esporta i dati di un modulo PDF interattivo in formati XML e XDP.

**Sintassi:** `Document exportData(Document xdpOrPdf, DataFormat dataFormat)`

#### Parametri di input {#input-parameters-5}

<table>
 <tbody>
  <tr>
   <th>Parametro</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td>xdpOrPdf<br /> </td>
   <td>Specifica un oggetto documento contenente un file XDP o PDF. </td>
  </tr>
  <tr>
   <td>dataFormat<br /> </td>
   <td>Specifica il formato in cui vengono esportati i dati. Accetta una variabile di tipo enum(XDP, XmlData, Auto).<br /> </td>
  </tr>
 </tbody>
</table>

Nell&#39;esempio di codice Java riportato di seguito vengono esportati i dati di un modulo PDF interattivo in formati XML e XDP.

#### Esempio {#sample}

```java
@Reference private FormsService formsService;
private File exportData(String  dataFormat, File  inDoc) {

String outputFolder="C:/Output";

InputStream in; Document doc=null;

try {

        in = new FileInputStream(inDoc);

        if(dataFormat.equalsIgnoreCase("xml"))

        {

          doc=formsService.exportData(new Document(in),                                       DataFormat.XmlData);

        }

        else if(dataFormat.equalsIgnoreCase("xdp")) {

        doc =formsService.exportData(new Document(in),                       DataFormat.XDP);

        }

        File toSave = new File(outputFolder,"Output"+"."+dataFormat);

        doc.copyToFile(toSave);

        return toSave;

    } catch (FormsServiceException e) {

       e.printStackTrace();

    }catch (FileNotFoundException e) {

       e.printStackTrace();

    } catch (IOException e) {

       e.printStackTrace();

    }finally{

        doc.dispose();

    }

    return null;

 }
```

### importData {#importdata}

Importa i dati del modulo in un modulo PDF interattivo.

**Sintassi:** `Document importData(Document PDF, Document data)`

#### Parametri di input {#input-parameters-6}

<table>
 <tbody>
  <tr>
   <th>Parametro</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td>PDF<br /> </td>
   <td>Specifica un oggetto documento contenente file PDF. </td>
  </tr>
  <tr>
   <td>Dati<br /> </td>
   <td>File XML contenente dati in formato XML.</td>
  </tr>
 </tbody>
</table>

Il codice Java di esempio seguente importa i dati del modulo in un modulo PDF interattivo.

#### Esempio {#sample-1}

```java
@Reference private FormsService formsService

private File importData(File inDoc, File inXML)

{

 String outputFolder="C:/Output";

 Document doc=null;

 try {

        InputStream in = new FileInputStream(inDoc);

        InputStream in2 = new FileInputStream(inXML);

        doc=formsService.importData(new Document(in), new Document(in2));

        File toSave = new File(outputFolder,"Output.pdf");

        doc.copyToFile(toSave);

    } catch (FormsServiceException e) {

         e.printStackTrace();

    }catch (FileNotFoundException e) {

         e.printStackTrace();

    } catch (IOException e) {

         e.printStackTrace();

    }finally{

        doc.dispose();

    }

    return null;

}
```

## Servizio PDF Generator {#pdfgeneratorservice}

Il servizio PDF Generator fornisce API per la conversione di formati di file nativi in PDF. Converte inoltre PDF in altri formati di file e ottimizza le dimensioni dei documenti PDF.

### GeneraServizioPDF {#generatepdfservice}

GeneratePDFService fornisce API per la conversione di vari formati di file, ad esempio doc, docx, ppt, pptx, xls, xlsx, odp, odt, ods, swf (obsoleto), jpg, bmp, tif, png, html e molti altri formati di file in PDF. Fornisce inoltre API per esportare PDF in vari formati di file e ottimizzare i PDF. Il servizio supporta le seguenti API:

* **createPDF**: converte un tipo di file supportato in un documento PDF. Supporta formati di file come Microsoft Word, Microsoft PowerPoint, Microsoft Excel e Microsoft Project. Oltre a queste applicazioni, qualsiasi PDF generico di terze parti che generi un tipo di applicazione può anche essere collegato all’API.
* **exportPDF**: converte un documento PDF in un tipo di file supportato. Il metodo accetta un PDF come input ed esporta il contenuto del PDF nel formato di file specificato. È possibile esportare un documento di PDF in Encapsulated PostScript( eps), HTML 3.2( htm, html), HTML 4.01 con CSS 1.0( htm, html), JPEG( jpg, jpeg, jpe), JPEG2000( jpf, jpx, jp2, j2k, j2c, jpc), Microsoft Word Document( doc, docx) Microsoft Excel Workbook( xlsx), Microsoft PowerPoint Presentation( pptx), PNG( png), PostScript( Rich Text Format( rtf), Text(Accessible)( txt), Text(Plain)( txt) TIFF( tif, tiff), XML 1.0( xml), PDF/A-1a(sRGB), PDF/A-1b, PDF/A-2a(sRGB), PDF/A-2b(sRGB), PDF/A-3a(sRGB), PDF/A-3a(sRGB), formati/A-3b(sRGB). Puoi anche specificare [profili di verifica preliminare personalizzati](https://helpx.adobe.com/acrobat/using/preflight-profiles-acrobat-pro.html) per le uscite PDF.

* **optimizePDF**: ottimizza il documento PDF e converte anche un documento PDF da un tipo a un altro. Il metodo accetta un documento PDF come input.
* **htmlToPdf2**: converte una pagina HTML in un documento PDF. Accetta l’URL della pagina HTML come input.

>[!NOTE]
>
>L’API HTMLtoPDF è obsoleta per il server AEM Forms in esecuzione sul sistema operativo AIX.

#### API PDF Generator disponibile su Microsoft Windows e Linux {#pdf-generator-api-available-on-microsoft-windows-and-linux}

<table>
 <tbody>
  <tr>
   <td><strong>API</strong></td>
   <td><p><strong>Microsoft Windows </strong></p> </td>
   <td><strong>Linux </strong></td>
  </tr>
  <tr>
   <td>createPDF</td>
   <td><strong>✓</strong></td>
   <td><strong>✓</strong></td>
  </tr>
  <tr>
   <td>htmlToPDF</td>
   <td><strong>✓</strong></td>
   <td><strong>✓</strong></td>
  </tr>
   <td>optimizePDF</td>
   <td><strong>✓</strong></td>
   <td>✖</td>
  </tr>
  <tr>
   <td>exportPDF</td>
   <td><strong>✓</strong></td>
   <td>✖</td>
  </tr>
  <tr>
   <td>OCR PDF (PDF ricercabile)</td>
   <td><strong>✓</strong></td>
   <td>✖</td>
  </tr>
 </tbody>
</table>

#### createPDF {#createpdf}

L’API createPDF converte un tipo di file supportato in un documento PDF. Supporta vari formati di file come Microsoft Word, Microsoft PowerPoint, Microsoft Excel e Microsoft Project. Oltre a queste applicazioni, qualsiasi PDF generico di terze parti che generi un tipo di applicazione può anche essere collegato all’API.

Per la conversione, sono obbligatori solo alcuni parametri. Un documento di input è un parametro obbligatorio. È possibile applicare successivamente le autorizzazioni di protezione, le impostazioni di output di PDF e le informazioni sui metadati al documento di output di PDF.

Il servizio createPDF restituisce un file java.util.Map con i risultati. Le chiavi della mappa sono:

* ConvertedDoc: contiene il documento PDF appena creato.
* LogDoc: contiene il file di registro.

Il servizio createPDF genera le seguenti eccezioni:

* ConversionException
* InvalidParameterException
* FileFormatNotSupportedException

**Sintassi:** `Map createPDF(Document inputDoc, String inputFilename, String fileTypeSettings, String pdfSettings, String securitySettings, Document settingsDoc, Document xmpDoc) throws InvalidParameterException, ConversionException, FileFormatNotSupportedException;`

#### Parametri di input {#input-parameters-7}

<table>
 <tbody>
  <tr>
   <th>Parametro</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td>inputDoc<br /> </td>
   <td>Specifica un oggetto documento. L'oggetto documento contiene il file di input. Crea un oggetto com.adobe.aemfd.docmanager.Document sul documento di input. È un parametro obbligatorio.</td>
  </tr>
  <tr>
   <td>inputFileName<br /> </td>
   <td>Il nome del file di input con l’estensione. È un parametro obbligatorio.<br /> </td>
  </tr>
  <tr>
   <td>fileTypeSettings</td>
   <td>Si tratta di un parametro facoltativo.</td>
  </tr>
  <tr>
   <td>pdfSettings</td>
   <td><p>Output PDF per il documento convertito. È possibile applicare solo le impostazioni seguenti:</p>
    <ul>
     <li>Stampa_alta_qualità<br /> </li>
     <li>PDFA1b_2005_RGB<br /> </li>
     <li>PDFA1b_2005_CMYK<br /> </li>
     <li>PDFX1a_2001<br /> </li>
     <li>PDFX3_2002<br /> </li>
     <li>Press_Quality<br /> </li>
     <li>Dimensione_File_Più_Piccola</li>
    </ul> <p>Si tratta di un parametro facoltativo.<br /> </p> </td>
  </tr>
  <tr>
   <td>securitySettings</td>
   <td><p>Impostazioni di protezione per il documento convertito. Puoi applicare le seguenti impostazioni:</p>
    <ul>
     <li>Nessuna protezione</li>
     <li>Sicurezza password<br /> </li>
     <li>Sicurezza dei certificati<br /> </li>
     <li>Server dei criteri Adobe</li>
    </ul> <p>Si tratta di un parametro facoltativo.</p> </td>
  </tr>
  <tr>
   <td>settingsDoc</td>
   <td>Il file contiene le impostazioni applicate durante la generazione del documento PDF (ad esempio, Ottimizzazione del documento PDF per la visualizzazione Web) e le impostazioni applicate dopo la creazione del documento PDF (ad esempio, Visualizzazione iniziale e Protezione). Si tratta di un parametro facoltativo.<br /> </td>
  </tr>
  <tr>
   <td>xmpDoc </td>
   <td>Il file contiene informazioni sui metadati applicate al documento PDF generato. Questo parametro è facoltativo.<br /> </td>
  </tr>
 </tbody>
</table>

Il codice Java seguente converte un documento di tipo file supportato in un documento PDF.

```java
@Reference GeneratePDFService generatePdfService;
File createPDF(File inputFile, String inputFilename, String fileTypeSettings, String pdfSettings, String securitySettings, File settingsFile, File xmpFile) throws Exception
{
 Transaction tx = OSGiUtils.getTransactionManager().getTransaction();
 // Begin transaction
 if (tx == null)
 OSGiUtils.getTransactionManager().begin();
 String outputFolder="C:/Output"
 Document convertedDoc = null;
 Document inDoc = null;
 Document settingsDoc = null;
 Document xmpDoc = null;
 try
 {
  inDoc = new Document(inputFile);
  if(inputFilename == null || inputFilename.trim().equals("")) {
   throw new Exception("Input file name cannot be null");
  }
  if(inputFileExtension.lastIndexOf('.') == -1) {
   throw new Exception("Input file should have an extension");
  }
  if(settingsFile != null && settingsFile.exists() && settingsFile.isFile())
  settingsDoc = new Document(settingsFile);
  if(xmpFile != null && xmpFile.exists() && xmpFile.isFile())
  xmpDoc = new Document(xmpFile);
  Map result = generatePdfService.createPDF(inDoc, inputFilename, fileTypeSettings, pdfSettings, securitySettings, settingsDoc, xmpDoc);
  convertedDoc = (Document)result.get("ConvertedDoc");
  OSGiUtils.getTransactionManager().commit();
  File outputFile = new File(outputFolder,"Output.pdf");
  doc.copyToFile(outputFile);
  return outputFile;
 }
 catch (Exception e)
 {
  if (OSGiUtils.getTransactionManager().getTransaction() != null)
  OSGiUtils.getTransactionManager().rollback();
  throw e;
 }
 finally {
  if (convertedDoc != null) {
   convertedDoc.dispose();
   convertedDoc = null;
  }
  if (inDoc != null) {
   inDoc.dispose();
   inDoc = null;
  }
  if (settingsDoc != null) {
   settingsDoc.dispose();
   settingsDoc = null;
  }
  if (xmpDoc != null) {
   xmpDoc.dispose();
   xmpDoc = null;
  }
 }
}
```

#### exportPDF {#exportpdf}

Converte un documento PDF in un tipo di file supportato. Il metodo accetta un PDF come input ed esporta il contenuto del PDF nel formato di file specificato.

Il servizio createPDF restituisce un file java.util.Map con i risultati. Le chiavi della mappa sono:

* ConvertedDoc: contiene il documento di output.

Il servizio createPDF genera le seguenti eccezioni:

* ConversionException
* InvalidParameterException
* FileFormatNotSupportedException

**Sintassi:**

```java
Map exportPDF(Document inputDoc, String inputFileName, String formatType, Document settingsDoc) throws ConversionException, InvalidParameterException, FileFormatNotSupportedException;
```

#### Parametri di input {#input-parameters-8}

<table>
 <tbody>
  <tr>
   <th>Parametro</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td>inputDoc<br /> </td>
   <td>Specifica il documento da convertire. </td>
  </tr>
  <tr>
   <td>inputFileName<br /> </td>
   <td>Il nome del file e l’estensione.<br /> </td>
  </tr>
  <tr>
   <td>formatType</td>
   <td>Il formato del file di output per l’API exportPDF.<br /> </td>
  </tr>
  <tr>
   <td>settingsDoc </td>
   <td>Il file contiene le configurazioni da applicare durante la generazione del documento di output. In genere si tratta di un file XML.</td>
  </tr>
 </tbody>
</table>

Nell&#39;esempio di codice Java seguente un documento PDF viene convertito nel tipo di file specificato.

```java
(tx == null)
OSGiUtils.getTransactionManager().begin();
String outputFolder="C:/Output"
Document convertedDoc = null;
Document inDoc = null;
Document settingsDoc = null;
try
{
 inDoc = new Document(inputFile);
 if(inputFileName == null || inputFileName.trim().equals("")) {
  throw new Exception("Input file name cannot be null");
 }
 if(inputFileExtension.lastIndexOf('.') == -1) {
  throw new Exception("Input file should have an extension");
 }
 if(settingsFile != null && settingsFile.exists() && settingsFile.isFile())
 settingsDoc = new Document(settingsFile);
 Map result = generatePdfService.exportPDF(inDoc, inputFileName, formatType, settingsDoc);
 convertedDoc = (Document)result.get("ConvertedDoc");
 OSGiUtils.getTransactionManager().commit();
 File outputFile = new File(outputFolder,"OutputFile");
 doc.copyToFile(outputFile);
 return outputFile;
}
catch (Exception e)
{
 if (OSGiUtils.getTransactionManager().getTransaction() != null)
 OSGiUtils.getTransactionManager().rollback();
 throw e;
}
finally {
 if (convertedDoc != null) {
  convertedDoc.dispose();
  convertedDoc = null;
 }
 if (inDoc != null) {
  inDoc.dispose();
  inDoc = null;
 }
 if (settingsDoc != null) {
  settingsDoc.dispose();
  settingsDoc = null;
 }
}
}
```

#### optimizePDF {#optimizepdf}

L’API OptimizePDF ottimizza i file PDF riducendone le dimensioni. Il risultato di questa conversione è costituito da file PDF che potrebbero essere più piccoli delle versioni originali. Questa operazione converte anche i documenti PDF nella versione PDF specificata nei parametri di ottimizzazione. Restituisce l&#39;oggetto OptimizePDFResult contenente optimized PDF.

Il servizio createPDF genera le seguenti eccezioni:

* ConversionException
* InvalidParameterException
* FileFormatNotSupportedException

**Sintassi:**

```java
OptimizePDFResult optimizePDF(Document inputDoc, String fileTypeSettings, Document settingsDoc) throws ConversionException, InvalidParameterException, FileFormatNotSupportedException;
```

#### Parametri di input {#input-parameters-9}

<table>
 <tbody>
  <tr>
   <th>Parametro</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td>inputDoc<br /> </td>
   <td>Specifica il documento di input. È un parametro obbligatorio.</td>
  </tr>
  <tr>
   <td>fileTypeSettings<br /> </td>
   <td>Si tratta di un parametro facoltativo.<br /> </td>
  </tr>
  <tr>
   <td>settingsDoc </td>
   <td>Il file contiene le impostazioni applicate durante la generazione del documento PDF (ad esempio, Ottimizzazione del documento PDF per la visualizzazione Web) e le impostazioni applicate dopo la creazione del documento PDF (ad esempio, Visualizzazione iniziale e Protezione). Si tratta di un parametro facoltativo.<br /> </td>
  </tr>
 </tbody>
</table>

Il codice Java di esempio seguente ottimizza il file PDF di input riducendone le dimensioni.

```java
@Reference GeneratePDFService generatePdfService;
File optimizePDF(File inputFile, String fileTypeSettings, File settingsFile) throws Exception
{
 Transaction tx = OSGiUtils.getTransactionManager().getTransaction();
 // Begin transaction
 if (tx == null)
 OSGiUtils.getTransactionManager().begin();
 String outputFolder="C:/Output"
 Document convertedDoc = null;
 Document inDoc = null;
 Document settingsDoc = null;
 try
 {
  inDoc = new Document(inputFile);
  if(settingsFile != null && settingsFile.exists() && settingsFile.isFile())
  settingsDoc = new Document(settingsFile);
  OptimizePDFResult result = generatePdfService.optimizePDF(inDoc, fileTypeSettings, settingsDoc);
  convertedDoc = result.getConvertedDocument();
  OSGiUtils.getTransactionManager().commit();
  File outputFile = new File(outputFolder,"Output.pdf");
  doc.copyToFile(outputFile);
  return outputFile;
 }
 catch (Exception e)
 {
  if (OSGiUtils.getTransactionManager().getTransaction() != null)
  OSGiUtils.getTransactionManager().rollback();
  throw e;
 }
 finally {
  if (convertedDoc != null) {
   convertedDoc.dispose();
   convertedDoc = null;
  }
  if (inDoc != null) {
   inDoc.dispose();
   inDoc = null;
  }
  if (settingsDoc != null) {
   settingsDoc.dispose();
   settingsDoc = null;
  }
 }
}
```

#### htmlToPdf2 {#htmltopdf}

Converte una pagina HTML in un documento PDF. Accetta l’URL della pagina HTML come input.

Il servizio htmlToPdf2 restituisce un oggetto HtmlToPdfResult. È possibile ottenere il PDF convertito tramite result.getConvertedDocument().

Il servizio htmlToPdf2 genera le seguenti eccezioni:

* ConversionException
* InvalidParameterException
* FileFormatNotSupportedException

**Sintassi:**

```java
HtmlToPdfResult htmlToPdf2(String inputUrl, String fileTypeSettingsName, String securitySettingsName, Document settingsDoc, Document xmpDoc) throws ConversionException, InvalidParameterException, FileFormatNotSupportedException;
```

#### Parametri di input {#input-parameters-10}

<table>
 <tbody>
  <tr>
   <th>Parametro</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td>inputDoc<br /> </td>
   <td>Specifica il documento di input. È un parametro obbligatorio.</td>
  </tr>
  <tr>
   <td>fileTypeSettings<br /> </td>
   <td>Si tratta di un parametro facoltativo.<br /> </td>
  </tr>
  <tr>
   <td>settingsDoc </td>
   <td>Il file contiene le impostazioni applicate durante la generazione del documento PDF (ad esempio, Ottimizzazione del documento PDF per la visualizzazione Web) e le impostazioni applicate dopo la creazione del documento PDF (ad esempio, Visualizzazione iniziale e Protezione). Si tratta di un parametro facoltativo.<br /> </td>
  </tr>
 </tbody>
</table>

Esempio Nell&#39;esempio di codice Java riportato di seguito viene convertita una pagina HTML in un documento PDF.

```java
Reference GeneratePDFService generatePdfService;
File htmlToPdf(String inputUrl, String fileTypeSettingsName, String securitySettingsName, File settingsFile, File xmpFile) throws Exception
{
 Transaction tx = OSGiUtils.getTransactionManager().getTransaction();
 // Begin transaction
 if (tx == null)
 OSGiUtils.getTransactionManager().begin();
 String outputFolder="C:/Output"
 Document convertedDoc = null;
 Document settingsDoc = null;
 Document xmpDoc = null;
 try
 {
  if(settingsFile != null && settingsFile.exists() && settingsFile.isFile())
  settingsDoc = new Document(settingsFile);
  if(xmpFile != null && xmpFile.exists() && xmpFile.isFile())
  xmpDoc = new Document(xmpFile);
  HtmlToPdfResult result = generatePdfService.htmlToPdf2(inputURL, fileTypeSettingsName, securitySettingsName, settingsDoc, xmpDoc);;
  convertedDoc = result.getConvertedDocument();
  OSGiUtils.getTransactionManager().commit();
  File outputFile = new File(outputFolder,"Output.pdf");
  doc.copyToFile(outputFile);
  return outputFile;
 }
 catch (Exception e)
 {
  if (OSGiUtils.getTransactionManager().getTransaction() != null)
  OSGiUtils.getTransactionManager().rollback();
  throw e;
 }
 finally {
  if (convertedDoc != null) {
   convertedDoc.dispose();
   convertedDoc = null;
  }
  if (xmpDoc != null) {
   xmpDoc.dispose();
   xmpDoc = null;
  }
  if (settingsDoc != null) {
   settingsDoc.dispose();
   settingsDoc = null;
  }
 }
}
```

### DistillerService {#distillerservice}

Il servizio Distiller converte i file PostScript, Incapsulated PostScript (EPS) e PRN (Printer Text File) in file PDF. Il servizio Distiller viene spesso utilizzato per convertire grandi quantità di documenti stampati in documenti elettronici, come fatture e rendiconti. La conversione dei documenti in PDF consente inoltre alle aziende di inviare ai propri clienti una versione cartacea e una versione elettronica di un documento. I formati di file supportati sono .ps, .eps e .prn. Il servizio supporta le seguenti API:

Il servizio createPDF restituisce un file java.util.Map con i risultati. Le chiavi della mappa sono:

* ConvertedDoc : Contiene il documento PDF appena creato.
* LogDoc : Contiene il file di registro.

Il servizio createPDF genera le seguenti eccezioni:

* ConversionException
* InvalidParameterException
* FileFormatNotSupportedException

#### createPDF {#createpdf-1}

Converte i formati supportati in documenti PDF. Il metodo accetta i formati di file ps, eps e prn come input. È possibile applicare al documento di PDF di output autorizzazioni di protezione, impostazioni di output e informazioni sui metadati specifiche.

**Sintassi:**

```java
Map createPDF(Document inputDoc, String inputFileName, String pdfSettings, String securitySettings, Document settingsDoc, Document xmpDoc) throws ConversionException, InvalidParameterException, FileFormatNotSupportedException;
```

#### Parametri di input {#input-parameters-11}

<table>
 <tbody>
  <tr>
   <th>Parametro</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td>inputDoc<br /> </td>
   <td>Specifica il documento di input. È un parametro obbligatorio.</td>
  </tr>
  <tr>
   <td>inputFileName</td>
   <td>Specifica il nome completo del file di input e l'estensione del file. È un parametro obbligatorio.</td>
  </tr>
  <tr>
   <td>pdfSettings</td>
   <td><p>Impostazioni di output PDF per il documento convertito. È possibile applicare solo le impostazioni seguenti:</p>
    <ul>
     <li>Stampa_alta_qualità<br /> </li>
     <li>PDFA1b_2005_RGB<br /> </li>
     <li>PDFA1b_2005_CMYK<br /> </li>
     <li>PDFX1a_2001<br /> </li>
     <li>PDFX3_2002<br /> </li>
     <li>Press_Quality<br /> </li>
     <li>Dimensione_File_Più_Piccola</li>
    </ul> <p>Si tratta di un parametro facoltativo.</p> </td>
  </tr>
  <tr>
   <td>securitySettings</td>
   <td><p>Impostazioni di protezione per il documento convertito. Puoi applicare le seguenti impostazioni:</p>
    <ul>
     <li>Nessuna protezione</li>
     <li>Sicurezza password<br /> </li>
     <li>Sicurezza dei certificati<br /> </li>
     <li>Server dei criteri Adobe</li>
    </ul> <p>Si tratta di un parametro facoltativo.</p> </td>
  </tr>
  <tr>
   <td>settingsDoc </td>
   <td>Il file contiene le impostazioni applicate durante la generazione del documento PDF (ad esempio, Ottimizzazione del documento PDF per la visualizzazione Web) e le impostazioni applicate dopo la creazione del documento PDF (ad esempio, Visualizzazione iniziale e Protezione). Si tratta di un parametro facoltativo.<br /> </td>
  </tr>
  <tr>
   <td>xmpDoc </td>
   <td>Il file contiene informazioni sui metadati per il documento PDF generato. Si tratta di un parametro facoltativo.</td>
  </tr>
 </tbody>
</table>

Nell&#39;esempio di codice Java seguente i file di input di tipo PostScript (PS), Encapsulated PostScript (EPS) e i file di testo della stampante (PRN) vengono convertiti in file PDF.

```java
@Reference DistillerService distillerService;
File createPDF(File inputFile, String inputFilename, String pdfSettings, String securitySettings, File settingsFile, File xmpFile) throws Exception
{
 Transaction tx = OSGiUtils.getTransactionManager().getTransaction();
 // Begin transaction
 if (tx == null)
 OSGiUtils.getTransactionManager().begin();
 String outputFolder="C:/Output"
 Document convertedDoc = null;
 Document inDoc = null;
 Document settingsDoc = null;
 Document xmpDoc = null;
 try
 {
  inDoc = new Document(inputFile);
  if(inputFilename == null || inputFilename.trim().equals("")) {
   throw new Exception("Input file name cannot be null");
  }
  if(inputFileExtension.lastIndexOf('.') == -1) {
   throw new Exception("Input file should have an extension");
  }
  if(settingsFile != null && settingsFile.exists() && settingsFile.isFile())
  settingsDoc = new Document(settingsFile);
  if(xmpFile != null && xmpFile.exists() && xmpFile.isFile())
  xmpDoc = new Document(xmpFile);
  Map result = distillerService.createPDF(inDoc, inputFilename, pdfSettings, securitySettings, settingsDoc, xmpDoc);
  convertedDoc = (Document)result.get("ConvertedDoc");
  OSGiUtils.getTransactionManager().commit();
  File outputFile = new File(outputFolder,"Output.pdf");
  doc.copyToFile(outputFile);
  return outputFile;
 }
 catch (Exception e)
 {
  if (OSGiUtils.getTransactionManager().getTransaction() != null)
  OSGiUtils.getTransactionManager().rollback();
  throw e;
 }
 finally {
  if (convertedDoc != null) {
   convertedDoc.dispose();
   convertedDoc = null;
  }
  if (inDoc != null) {
   inDoc.dispose();
   inDoc = null;
  }
  if (settingsDoc != null) {
   settingsDoc.dispose();
   settingsDoc = null;
  }
  if (xmpDoc != null) {
   xmpDoc.dispose();
   xmpDoc = null;
  }
 }
}
```
