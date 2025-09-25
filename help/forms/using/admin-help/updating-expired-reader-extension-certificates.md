---
title: Scadenza dei certificati delle estensioni di Reader e relativo impatto
description: Scadenza dei certificati delle estensioni di Reader e relativo impatto
exl-id: 4e14e0dc-f248-4f6e-a075-6012b6792d9d
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: ht
source-wordcount: '1088'
ht-degree: 100%

---


# Scadenza dei certificati delle estensioni di Reader e relativo impatto {#expiration-of-reader-extensions-certificates-and-its-impact}

I clienti Adobe Experience Manager Forms (AEM Forms) con licenze Adobe Managed Services o On-Premise Enterprise Base hanno diritto a utilizzare il servizio Acrobat Reader DC Extensions. Il servizio consente a un’organizzazione di condividere facilmente documenti PDF interattivi estendendo la funzionalità di Acrobat Reader con diritti di utilizzo aggiuntivi. Il servizio aggiunge i diritti di utilizzo a un documento PDF e attiva funzionalità non disponibili quando un documento PDF viene aperto tramite Adobe Acrobat Reader, come ad esempio l’aggiunta di commenti a un documento, la compilazione di moduli e il salvataggio del documento. Gli utenti di terze parti non richiedono software o plug-in aggiuntivi per lavorare con documenti con diritti abilitati. I documenti PDF a cui sono stati aggiunti i diritti di utilizzo si chiamano documenti con diritti abilitati. L’utente che apre in Acrobat Reader un documento PDF con diritti abilitati può eseguire le operazioni abilitate per quel documento.

Adobe utilizza un’infrastruttura a chiave pubblica (Public Key Infrastructure, PKI) per rilasciare certificati digitali da utilizzare durante la concessione di licenze e l’abilitazione delle funzioni. Adobe emette certificati con l’autorità di certificazione **Adobe Root CA**, con scadenza 7 gennaio 2023. La scadenza del certificato non influisce sui documenti PDF estesi utilizzando certificati di produzione rilasciati dai certificati basati su **Adobe Root CA** (certificati precedenti). Tutti i documenti PDF estesi da Reader utilizzando i certificati precedenti al 7 gennaio 2023, inclusi quelli scaricati dai clienti, continueranno a funzionare con tutti i diritti di utilizzo applicati e non sarà necessario aggiornarli.

È ora disponibile una nuova autorità di certificazione, **Adobe Root CA G2**, insieme ai certificati basati su tale nuova autorità di certificazione. A partire dal 7 gennaio 2023 o prima di tale data, inizia a utilizzare i nuovi certificati, basati su **Adobe Root CA G2** affinché Reader estenda i nuovi documenti PDF.  Puoi [ottenere nuovi certificati dal sito web Adobe Licensing Website](https://licensing.adobe.com/) o dal supporto di Adobe.

## Domande frequenti

**D. Qual è la differenza tra un certificato Adobe Root e un certificato Acrobat Reader Extensions? Il certificato Adobe Root si basa su un certificato Acrobat Reader Extensions? Entrambi questi certificati scadono a gennaio 2023?**

R. Adobe Root CA è l’autorità di certificazione che emette un certificato Acrobat Reader Extensions. Il 7 gennaio 2023 è la data di scadenza di “Adobe Root CA” e di tutti i certificati rilasciati da tale autorità di certificazione.

**D. In precedenza Adobe aveva comunicato la scadenza dei certificati e l’impatto sull’utilizzo o l’apertura di documenti PDF. Tale comunicazione deve essere ignorata?**

R. In base alla rivalutazione della situazione, tutti i documenti PDF estesi utilizzando i certificati di produzione rilasciati dalla precedente “Adobe Root CA” prima del 7 gennaio 2023 continuano a essere utilizzabili senza alcuna modifica dopo il 7 gennaio 2023. Se hai già aggiornato i documenti PDF, l’esperienza di utilizzo non subisce modifiche.

**D. A chi devo rivolgermi in caso di ulteriori domande?**

R. Puoi contattare il [supporto Adobe](https://experienceleague.adobe.com/it?support-solution=Experience+Manager&lang=it#support) o aprire un ticket di supporto.

**D. Cosa succede se non aggiorno il certificato prima del 7 gennaio 2023?**

R. Tutti i documenti PDF estesi utilizzando i certificati di produzione rilasciati dalla precedente “Adobe Root CA” prima del 7 gennaio 2023 continuano a essere utilizzabili senza alcuna modifica dopo il 7 gennaio 2023. I documenti PDF estesi con certificati di valutazione non sono più utilizzabili dopo la data di scadenza.

**D. La descrizione dei nuovi certificati è diversa da quella dei certificati precedenti?**

R. La descrizione dei nuovi certificati Acrobat Reader Extensions riporta la dicitura **G3-P24** come nome del programma. Nella descrizione dei certificati ancor meno recenti (certificati basati su “Adobe Root CA”), **P24** è la dicitura che fa riferimento al nome del programma.

**D. Come si ottengono i certificati più recenti?**

R. Tutti i clienti Forms autorizzati (con licenza attiva) possono scaricare i nuovi certificati (certificati basati su “Adobe Root CA G2”) dal sito web [Adobe Licensing Website](https://licensing.adobe.com/). Se non riesci a trovare il certificato sul sito web Adobe Licensing Website, contatta il [supporto Adobe](https://experienceleague.adobe.com/it?support-solution=Experience+Manager&lang=it#support) o apri un ticket di supporto.

**D. I miei documenti PDF estesi utilizzando certificati rilasciati da “Adobe Root CA” (la precedente autorità di certificazione) continuano a essere utilizzabili dopo il 7 gennaio 2023?**

R. Sì, tutti i documenti PDF estesi utilizzando certificati di produzione rilasciati da “Adobe Root CA” (la precedente autorità di certificazione) prima del 7 gennaio 2023 continuano a essere utilizzabili senza alcuna modifica dopo il 7 gennaio 2023. I documenti PDF estesi con certificati di valutazione non sono più utilizzabili dopo la data di scadenza.

**D. Quale versione di Adobe Acrobat Reader è necessaria per continuare a utilizzare i documenti PDF estesi con certificati rilasciati da “Adobe Root CA” (la precedente autorità di certificazione)?**

R. Per utilizzare i documenti PDF estesi con “Adobe Root CA” (l’autorità di certificazione precedente). è richiesto Adobe Acrobat Reader 2020 o versioni successive. Si tratta della versione supportata di Acrobat Reader al momento della pubblicazione del documento. Se utilizzi una [versione non supportata di Adobe Acrobat](https://helpx.adobe.com/it/support/programs/eol-matrix.html), Adobe consiglia di [scaricare e installare la versione più recente di Adobe Acrobat Reader](https://get.adobe.com/it/reader/).

**D. Quale versione di Adobe Acrobat Reader è necessaria per continuare a utilizzare i documenti PDF estesi con certificati rilasciati dalla “Adobe Root CA 2” (la nuova autorità di certificazione)?**

R. Per utilizzare i documenti PDF estesi con “Adobe Root CA 2” (la nuova autorità di certificazione). è richiesto Adobe Acrobat Reader 2020 o versioni successive. Se utilizzi una [versione non supportata di Adobe Acrobat Reader](https://helpx.adobe.com/it/support/programs/eol-matrix.html), Adobe consiglia di [scaricare e installare la versione più recente di Adobe Acrobat Reader](https://get.adobe.com/it/reader/).

**D. Posso eliminare un certificato delle estensioni di Acrobat Reader precedente e aggiungerne uno nuovo in un server Adobe Experience Manager Forms mentre continuo a utilizzare l’alias esistente?**

R. Sì, puoi eliminare un certificato delle estensioni di Acrobat Reader precedente e aggiungerne uno nuovo con l’alias esistente a un server Adobe Experience Manager Forms.

**D. Posso conservare i certificati delle estensioni di Acrobat Reader nuovi e vecchi su un server Adobe Experience Manager Forms?**

R. Sì, puoi mantenere entrambi i certificati ma con alias diversi su un server Adobe Experience Manager Forms. Dopo il 7 gennaio 2023, puoi utilizzare solo il nuovo certificato per estendere un documento PDF in Reader.

**D. Posso importare lo stesso certificato delle estensioni di Acrobat Reader in tutti gli ambienti Adobe Experience Manager Forms?**

R. Sì, puoi utilizzare lo stesso certificato delle estensioni di Acrobat Reader in più ambienti.

**D. Come posso verificare i diritti di utilizzo applicati a un documento PDF?**

R. Puoi utilizzare l’API [getDocumentUsageRights](https://experienceleague.adobe.com/docs/experience-manager-65/forms/developer-reference/programming-aem-forms-jee/java-api-quick-start-code-examples/acrobat-reader-dc-extensions-service.html?lang=it#quick-start-soap-mode-retrieving-credential-information-using-the-java-api) per recuperare le informazioni sui diritti di utilizzo applicati a un documento PDF.

**D. Come posso modificare la password di un file di certificato delle estensioni di Acrobat Reader?**

R. In Microsoft Windows, per modificare la password del certificato, installa il certificato utilizzando Microsoft Management Console (MMC) e seleziona **Contrassegna la chiave come esportabile**. Una volta installato, esporta il certificato con una chiave privata e utilizza un’altra password per il file PFX.


<!-- 
## Applying the certificates {#obtaning-and-applying-the-certificates} 

You can choose one of the following paths to apply latest certificates:

* [Updating certificates for an AEM Forms on JEE environment](#Updating-and-Applying-certificates-for-an-AEM-Forms-on-JEE-environment) 
* [Updating certificates for an AEM Forms on OSGi environment](#Updating-and-applying-certificates-for-an-AEM-Forms-on-OSGi-environment)

>[!NOTE]
>
>The document uses the term certificates and credentials interchangeably.

### Pre-requisites {#Pre-requisites}

Updating the certificates requires using actions available on AEM Forms administrator console and Reader Extension APIs provided by AEM Forms. The document is intended for users and administrators with knowledge of using Adobe Experience Manger Forms APIs. Before you start, ensure that: 

* the user has administrator rights on underlying AEM Forms environment. 
* the user has setup the [development environment](https://experienceleague.adobe.com/docs/experience-manager-65/developing/devtools/howto-projects-eclipse.html?lang=it) and has access to it.
* [obtain the certificates](#obtain-the-certificates).


### Obtain the certificates {#obtain-the-certificates}

The Rights credential is delivered as a digital certificate that contains the public key, the private key, and the password used to access the credential.

If your organization purchases a production version of Reader Extensions, the production Rights credential is delivered by Adobe Licensing Website (LWS). A production Rights credential is unique to your organization and can enable the specific usage rights that you require.

If you obtained Reader Extensions through a partner or software provider who integrated Reader Extensions into their software, the Rights credential is provided to you by that partner who, in turn, receives this credential from Adobe.

>[!NOTE]
>
>The Rights credential cannot be used for typical document signing or assertion of identity. For these applications, you can use a self-sign certificate or acquire an identity certificate from a Certificate Authority (CA).

The following types of Rights credentials are available:

**Customer Evaluation**: A credential with a short validity period that is provided to customers who want to evaluate Reader Extensions. Usage rights applied to documents using this credential expire when the credential expires. This type of credential is valid only for two to three months.

**Production**: A credential with a long validity period that is provided to customers who purchased the full product. Production credentials are unique to each customer but can be installed on multiple systems.

If you have already used certificates to reader extend PDF files, download a production certificate from [Adobe Licensing Website (LWS)](https://licensing.adobe.com/).

### Applying certificates for an AEM Forms on JEE environment {#Updating-and-Applying-certificates-for-an-AEM-Forms-on-JEE-environment} 

Applying new certificates on AEM Forms on JEE stack requires importing new credentials and applying usage rights. You can use admin console to import credentials and AEM Forms Reader Extension APIs to apply usage rights. 

#### Import and configure credentials 

You can use the Trust Store Management pages to import a new credential. The Trust Store may contain more than one Reader Extensions credential. Designate one of those credentials as the default Reader Extensions credential. The default credential is used when a Workbench user is unable to determine which credential to use during process creation. These rules apply to default credentials:

* If you import a Reader Extensions credential and the Trust Store contains no other Reader Extensions credentials, it is set as the default.
* If you import a Reader Extensions credential with the Default option selected, the default type is removed from an existing default credential. The imported credential becomes the default.
* You cannot delete a default Reader Extensions credential. To delete the default credential, first set another credential as the default. An exception to this rule is that if there is only one credential, you can delete it even though it is the default.
* You cannot update a default Reader Extensions credential.

To import the credentials: 

1. In administration console, click Settings > Trust Store Management > Local Credentials.
1. Click Import and, under Trust Store Type, select Acrobat Reader DC extensions Credential.
1. (Optional) To indicate that this credential is the default credential to use with Acrobat Reader DC extensions, select Default.
1. In the Alias box, type an identifier for the credential. This identifier is used as the display name for the credential in Acrobat Reader DC extensions. This alias is also used to access the credential programmatically using the AEM forms SDK.
1. Click Choose File to locate the credential, type the password of the credential, and then click OK.

If the error message "Failed to import credential due to either incorrect file format, or incorrect password" appears, verify that the password is valid.

You can also import and delete credentials programmatically. (See [Programming with AEM forms](../../developing/credentials.md).)

<!-- ### Remove usage rights from existing rights-enabled PDF documents

Remove usage rights from existing rights-enabled PDF documents before applying usage rights with latest credentials. AEM Forms on JEE provides APIs to remove usage rights. For detailed instructions, see [Removing Usage Rights from PDF Documents](../../developing/assigning-usage-rights.md#removing-usage-rights-from-pdf-documents).

To remove usage rights for AEM Forms on JEE processes developed in Workbench, see [Workbench Help](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/WorkbenchHelp.pdf). 

#### Apply the usage rights to PDF documents 

After importing new credentials, you can apply usage rights to PDF documents using the Acrobat Reader DC extensions Java Client API and web service.  For details, see [Applying Usage Rights to PDF Documents](../../developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents). 


### Applying certificates for an AEM Forms on OSGi environment {#Updating-and-applying-certificates-for-an-AEM-Forms-on-OSGi-environment}

Applying new certificates on AEM Forms on OSGi stack requires importing new credentials and applying usage rights. You can use admin console to import credentials and AEM Forms Reader Extension APIs to apply usage rights. 

#### Import credentials {#Import-credentials}

In an AEM Forms on OSGi environment, a Reader Extension credential is associated with fd-service user. Before adding credentials for fd-user key store, perform the following steps to create a key store: 

1. Log in to your AEM Author instance as an Administrator.
1. Go to **[!UICONTROL Tools]**> **[!UICONTROL Security]**>**[!UICONTROL Users]**.
1. Scroll down the list of users until you find fd-service user account.
1. Click **[!UICONTROL fd-service]** user.
1. Click keystore tab.
1. Click **[!UICONTROL Create KeyStore]**.
1. Set the KeyStore Access Password and save your settings to create the KeyStore password.

After creating the key-store, add credentials to fd-service user. The following video explains the steps: 

>[!VIDEO](https://images-tv.adobe.com/mpcv3/5577/8db8e554-f04b-4fae-8108-b9b5e0eb03ad_1627925794.854x480at800_h264.mp4)

The following command list the details of the pfx file. Before running the command, navigate to the directory that contains the .pfx file.

`keytool -v -list -storetype pkcs12 -keystore [name of your .pfx file]`

For example, keytool -v -list -storetype pkcs12 -keystore 1005566.pfx where 1005566.pfx is the name of my pfx file

<!-- ### Remove usage rights from existing rights-enabled PDF documents

Remove usage rights from existing rights-enabled PDF documents before applying usage rights with latest credentials. You can remove the usage rights for a document by invoking the removeUsageRights API from within the docAssuranceServiceAPI. For detailed information, see [Remove Usage Rights](/help/forms/using/aem-document-services-programmatically.md#removing-usage-rights) document.

#### Apply the usage rights to PDF documents 

To apply usage rights in an AEM Forms on OSGi environment, Create custom OSGi service to usage rights to the documents. You can also create a servlet with a POST method to return the reader extended PDF to the user. For detailed instructions, see [Applying Reader Extensions](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/document-services/apply-reader-extension-rights-to-pdf.html?lang=it).  -->
