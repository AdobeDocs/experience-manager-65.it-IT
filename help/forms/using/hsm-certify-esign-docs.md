---
title: Utilizzare HSM per firmare o certificare digitalmente i documenti
seo-title: Utilizzare HSM per certificare i documenti firmati elettronicamente
description: Utilizzare dispositivi HSM o etoken per certificare i documenti firmati
seo-description: Utilizzare dispositivi HSM o etoken per certificare i documenti firmati
uuid: bbe057c1-6150-41f9-9c82-4979d31d305d
contentOwner: vishgupt
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 536bcba4-b754-4799-b0d2-88960cc4c44a
translation-type: tm+mt
source-git-commit: 35b2c9c8c79b3cc3d81e0b92ea17cd7d599fa7ee
workflow-type: tm+mt
source-wordcount: '1010'
ht-degree: 0%

---


# Utilizzare HSM per firmare o certificare digitalmente i documenti {#use-hsm-to-digitally-sign-or-certify-documents}

I moduli di sicurezza hardware (HSM) e i token sono dispositivi informatici dedicati, temprati e a resistenza agli urti progettati per gestire, elaborare e archiviare in modo sicuro le chiavi digitali. Tali dispositivi sono collegati direttamente a un computer o a un server di rete.

 Adobe Experience Manager Forms può utilizzare le credenziali archiviate in un HSM o collegate a eSign o applicare firme digitali lato server a un documento. Per utilizzare un dispositivo HSM o etoken con  AEM Forms:

1. Abilitare il servizio DocAssurance.
1. Configurate i certificati per l&#39;estensione del Reader.
1. Creare un alias per il dispositivo HSM o etoken nella console AEM Web.
1. Utilizzare le API DocAssurance Service per firmare o certificare i documenti con chiavi digitali memorizzate nel dispositivo.

## Prima di configurare i dispositivi HSM o etoken con  AEM Forms {#configurehsmetoken}

* Installate il pacchetto [ AEM Forms add-on](https://helpx.adobe.com/it/aem-forms/kb/aem-forms-releases.html).
* Installate e configurate il software client HSM o etoken sullo stesso computer AEM server. Il software client è richiesto per comunicare con i dispositivi HSM e etoken.
* (Solo Microsoft Windows) Impostate la variabile di ambiente JAVA_HOME_32 in modo che punti alla directory in cui è installata la versione a 32 bit di Java 8 Development Kit (JDK 8). Il percorso predefinito della directory è C:\Program Files(x86)\Java\jdk&lt;versione>
* ( AEM Forms solo su OSGi) Installate il certificato principale nell&#39;archivio delle fonti attendibili. È necessario verificare il PDF firmato

>[!NOTE]
>
>In Microsoft Windows, sono supportati solo client LunaSA o EToken a 32 bit.

## Abilita il servizio DocAssurance {#configuredocassurance}

Per impostazione predefinita, il servizio DocAssurance non è abilitato. Per abilitare il servizio, effettuate le seguenti operazioni:

1. Arrestate l&#39;istanza Author del vostro ambiente AEM Forms .

1. Aprire il file [AEM_root]\crx-quickstart\conf\sling.properties per la modifica.

   >[!NOTE]
   >
   >Se avete utilizzato il file [AEM_root]\crx-quickstart\bin\start.bat per avviare l&#39;istanza AEM, quindi aprite il file [AEM_root]\crx-quickstart\sling.properties per la modifica.

1. Aggiungete o sostituite le seguenti proprietà al file sling.properties:

   ```shell
   sling.bootdelegation.sun=sun.*,com.sun.*,sun.misc.*
   sling.bootdelegation.ibm=com.ibm.xml.*,com.ibm.*
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*  
   ```

1. Salvate e chiudete il file sling.properties.
1. Riavviate l&#39;istanza AEM.

## Configurare i certificati per le estensioni di Reader {#set-up-certificates-for-reader-extensions}

Per impostare i certificati, effettuate le seguenti operazioni:

1. Accedete all&#39;istanza di AEM Author come amministratore.

1. Fare clic su **Adobe Experience Manager** nella barra di navigazione globale. Accedete a **Strumenti** > **Sicurezza** > **Utenti**.
1. Fare clic sul campo **name** dell&#39;account utente. Viene visualizzata la pagina **Edit User Settings** (Modifica impostazioni utente&lt;a1/>).
1. Nell&#39;istanza di AEM Author, i certificati risiedono in un KeyStore. Se non avete creato un KeyStore in precedenza, fate clic su **Crea KeyStore** e impostate una nuova password per KeyStore. Se il server contiene già un KeyStore, ignora questo passaggio.

1. Nella pagina **Edit User Settings**, fare clic su **Manage KeyStore**.

1. Nella finestra di dialogo Gestione KeyStore, espandere l&#39;opzione **Aggiungi chiave privata dal file archivio chiavi** e fornire un alias. L&#39;alias viene utilizzato per eseguire l&#39;operazione Estensioni Reader.
1. Per caricare il file del certificato, fare clic su **Seleziona file archivio chiavi** e caricare un file `.pfx`.
1. Aggiungete la **Password archivio chiavi**,**Password chiave privata** e **Alias chiave privata** associata al certificato ai rispettivi campi. Fare clic su **Invia**.

   >[!NOTE]
   >
   >Per determinare l&#39;alias di chiave privata P **alias di chiave privata** di un certificato, è possibile utilizzare il comando Java keytool: `keytool -list -v -keystore [keystore-file] -storetype pkcs12`

   >[!NOTE]
   >
   >Nei campi **Password archivio chiavi** e **Password chiave privata**, specificare la password fornita con il file del certificato.

>[!NOTE]
>
>Per  AEM Forms su OSGi, per verificare il PDF firmato, il certificato principale installato nell&#39;archivio certificati attendibili.

>[!NOTE]
>
>Quando passate all&#39;ambiente di produzione, sostituite le credenziali di valutazione con le credenziali di produzione. Prima di aggiornare le credenziali scadute o di valutazione, assicurarsi di eliminare le credenziali di estensioni di Reader precedenti.

## Creare un alias per il dispositivo {#configuredeviceinaemconsole}

L&#39;alias contiene tutti i parametri richiesti da un HSM o etoken. Per creare un alias per ciascuna credenziale HSM o etoken utilizzata da eSign o Digital Signatures, attenersi alle istruzioni riportate di seguito.

1. Aprite AEM console. L&#39;URL predefinito di AEM console è https://&lt;host>:&lt;porta>/system/console/configMgr
1. Aprire il **servizio di configurazione delle credenziali HSM** e specificare i valori per i campi seguenti:

   * **Alias** credenziali: Specificare una stringa utilizzata per identificare l&#39;alias. Questo valore viene utilizzato come proprietà per alcune operazioni Digital Signatures, ad esempio l&#39;operazione Sign Signature Field.
   * **Percorso** DLL: Specificate il percorso completo della libreria HSM o client di etoken sul server. Ad esempio, C:\Program Files\LunaSA\cryptoki.dll. In un ambiente cluster, questo percorso deve essere identico per tutti i server del cluster.
   * **Fissa** HSM: Specificate la password necessaria per accedere al codice del dispositivo.
   * **ID** slot HSM: Specificare un identificatore di slot di tipo integer. L&#39;ID slot è impostato client per client. Se si registra un secondo computer in una partizione diversa (ad esempio, HSMPART2 sullo stesso dispositivo HSM), lo slot 1 è associato alla partizione HSMPART2 per il client.

   >[!NOTE]
   >
   >Durante la configurazione di Etoken, specificate un valore numerico per il campo ID slot HSM. Per il funzionamento delle operazioni Firme è necessario un valore numerico.

   * **Certificato SHA1**: Specificate il valore SHA1 (identificazione personale) del file della chiave pubblica (.cer) per la credenziale in uso. Verificare che non siano presenti spazi utilizzati nel valore SHA1. Se si utilizza un certificato fisico, non è richiesto.
   * **Tipo** di dispositivo HSM: Selezionate il produttore del dispositivo HSM (Luna o altro) o eToken.

   Fai clic su **Salva**. Il modulo di protezione hardware è configurato per  AEM Forms. Ora è possibile utilizzare il modulo di protezione hardware con  AEM Forms per firmare o certificare i documenti.

## Utilizzare le API DocAssurance Service per firmare o certificare un documento con chiavi digitali memorizzate nel dispositivo  {#programatically}

Il codice di esempio seguente utilizza un HSM o un token per firmare o certificare un documento.

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
import java.io.IOException;
import java.io.InputStream;

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
import com.adobe.fd.docassurance.client.api.SignatureOptions;
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
 * Digital signatures can be applied to PDF documents to provide a level of security. Digital signatures, like handwritten signatures, provide a means by which signers
 * identify themselves and make statements about a document. The technology used to digitally sign documents helps to ensure that both the signer and recipients are clear
 * about what was signed and confident that the document was not altered since it was signed.
 *
 * PDF documents are signed by means of public-key technology. A signer has two keys: a public key and a private key. The private key is stored in a user's credential that
 * must be available at the time of signing. The public key is stored in the user's certificate that must be available to recipients to validate the signature. Information
 * about revoked certificates is found in certificate revocation lists (CRLs) and Online Certificate Status Protocol (OCSP) responses distributed by Certificate Authorities (CAs).
 * The time of signing can be obtained from a trusted source known as a Timestamping Authority.
 *
 * The following Java code example digitally signs a PDF document that is based on a PDF file.
 * The alias that is specified for the security credential is secure, and revocation checking is performed.
 * Because no CRL or OCSP server information is specified, the server information is obtained from the certificate used to
 * digitally sign the PDF document
 *
 * PreRequisites - Digital certificate for signing the document has to be uploaded on Granite Key Store
 */

@Component
@Service(value=Sign.class)
public class Sign{
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
 public void signExtend(String inputFile, String outputFile, String alias) throws IOException, RepositoryException, InvalidArgumentException, DocAssuranceException{

  Document inDoc = new Document(inputFile);
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
             //as we don't want encryption in this case, passing null for Encryption Options
             //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
    outDoc = docAssuranceService.secureDocument(inDoc, null, getSignatureOptions(alias,resourceResolver),null,null);
        }
  catch(Exception e){
   e.printStackTrace();
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

        //flush the output document contents to JCR Node
  flush(outDoc, outputFile);

 }

 /**
  *
  * @param rr resource resolver corresponding to the user with the access to signing credential for the
  * given alias "allcertificatesanypolicytest11ee_new" in this case
  * @return SignatureOptions
  */
 private SignatureOptions getSignatureOptions(String alias, ResourceResolver rr){

  //create an instance of SignatureOptions
  SignatureOptions signatureOptions = SignatureOptions.getInstance();

  //set the operation you want to perform - SIGN/CERTIFY
  signatureOptions.setOperationType(DocAssuranceServiceOperationTypes.SIGN);

  //field to sign
  String fieldName = "Signature1" ;

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
        signatureOptions.setCredential(new CredentialContext(alias, rr, true));
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
    /**
     * This method copies the data from {@code Document}, to the specified file at the given resourcePath.
     * @param doc
     * @param resourcePath
     * @throws IOException
     */
    private void flush(Document doc, String resourcePath) throws IOException {
   //extracts the byte data from Document
   byte[] output = doc.getInlineData();
   Binary opBin;
   Session adminSession = null;
      try {
         adminSession = slingRepository.loginAdministrative(null);

         //get access to the specific node
         //here we are assuming that node exists
           Node node = adminSession.getNode(resourcePath);

           //convert byte[] to Binary
           opBin = adminSession.getValueFactory().createBinary((InputStream)new ByteArrayInputStream(output));

           //set the Binary data value to node's jcr:data
           node.getNode("jcr:content").getProperty("jcr:data").setValue(opBin);
      } catch (RepositoryException e) {

      }
      finally{

       if(adminSession != null && adminSession.isLive()){
        try {
      adminSession.save();
      adminSession.logout();
     } catch (RepositoryException e) {

     }

             }
      }

  }
}
```

Se hai effettuato l&#39;aggiornamento da AEM 6.0 Form o AEM 6.1 Forms e utilizzi il servizio DocAssurance nella versione precedente, allora:

* Per utilizzare il servizio DocAssurance senza un dispositivo HSM o etoken, continuare a utilizzare il codice esistente.
* Per utilizzare il servizio DocAssurance con un dispositivo HSM o etoken, sostituire il codice oggetto CredentialContext esistente con l&#39;API indicata di seguito.

```java
/**
  *
  * @param credentialAlias alias of the PKI Credential stored in CQ Key Store or
  * the alias of the HSM Credential configured using HSM Credentials Configuration Service.
  * @param resourceResolver corresponding to the user with the access to the key store and trust store.
  * @param isHSMCredential if the alias is corresponding to HSM Credential.
  */
 public CredentialContext(String credentialAlias, ResourceResolver resourceResolver, boolean isHSMCredential);
```

Per informazioni dettagliate sulle API e sul codice di esempio del servizio DocAssurance, vedere [Utilizzo di AEM Document Services a livello di programmazione](/help/forms/using/aem-document-services-programmatically.md).
