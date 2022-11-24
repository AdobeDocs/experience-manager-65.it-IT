---
title: Scadenza dei certificati di estensione del Reader e relativo impatto
description: Scadenza dei certificati di estensione del Reader e relativo impatto
exl-id: 4e14e0dc-f248-4f6e-a075-6012b6792d9d
source-git-commit: f35a35577f06686558bb1277b0d9bb17f6f0b7bf
workflow-type: tm+mt
source-wordcount: '1114'
ht-degree: 2%

---


# Scadenza dei certificati di estensione del Reader e relativo impatto {#expiration-of-reader-extensions-certificates-and-its-impact}

I clienti Adobe Experience Manager Forms (AEM Forms) con Adobe Managed Services o licenze Enterprise Base locali possono utilizzare il servizio Acrobat Reader DC Extensions. Il servizio consente a un’organizzazione di condividere facilmente i documenti PDF interattivi estendendo le funzionalità di Acrobat Reader con diritti di utilizzo aggiuntivi. Il servizio aggiunge diritti di utilizzo a un documento di PDF e attiva le funzioni non disponibili quando un documento di PDF viene aperto tramite Adobe Acrobat Reader, ad esempio l’aggiunta di commenti a un documento, la compilazione di moduli e il salvataggio del documento. Gli utenti di terze parti non richiedono software o plug-in aggiuntivi per lavorare con documenti abilitati per i diritti. I documenti di PDF a cui sono stati aggiunti i diritti di utilizzo sono denominati documenti abilitati per i diritti. Un utente che apre un documento PDF abilitato per i diritti in Acrobat Reader può eseguire le operazioni abilitate per tale documento.

Adobe sfrutta un’infrastruttura a chiave pubblica (PKI) per rilasciare certificati digitali da utilizzare in licenze e abilitazione delle funzioni. L’Adobe ha rilasciato certificati nell’ambito dell’autorità di certificazione &quot;Adobe Root CA&quot;, che scade il 7 gennaio 2023. Sono ora disponibili una nuova autorità di certificazione, &quot;Adobe Root CA G2&quot;, e certificati basati sulla nuova autorità di certificazione.

I vecchi certificati (certificati basati su &quot;Adobe Root CA&quot;) non funzionano più dopo il 7 gennaio 2023. L’Adobe consiglia di iniziare a utilizzare i nuovi certificati, quelli basati su &quot;Adobe Root CA G2&quot;, per Reader estendere i documenti PDF a partire dal 7 gennaio 2023 o prima di tale data.  È possibile [ottenere nuovi certificati dal sito web Adobe Licensing](https://licensing.adobe.com/) o Adobe Support.

Tutti i documenti PDF, il Reader esteso utilizzando i certificati precedenti prima del 7 gennaio 2023, inclusi quelli scaricati dai clienti, continueranno a funzionare con tutti i diritti di utilizzo ad essi applicati e non richiedono alcun aggiornamento.

## Domande frequenti

**D. Qual è la differenza tra un certificato radice di Adobe e un certificato di estensione di Acrobat Reader? L’Adobe del certificato radice dipende da un certificato delle estensioni Acrobat Reader? Entrambi questi certificati scadono nel gennaio 2023?**

A. Adobe Root CA è l’autorità di certificato da cui viene rilasciato un certificato di estensione Acrobat Reader. Il 7 gennaio 2023, &quot;Adobe Root CA&quot; e tutti i certificati rilasciati da esso scadono.

**D. C&#39;era una comunicazione precedente dell&#39;Adobe relativa alla scadenza dei certificati e all&#39;impatto sull&#39;utilizzo/apertura di documenti PDF. Questa comunicazione dovrebbe essere ignorata?**
A. Sulla base della rivalutazione della situazione, tutti i documenti PDF estesi utilizzando i certificati di produzione rilasciati dal vecchio &quot;Adobe Root CA&quot; prima del 7 gennaio 2023 continuano a funzionare senza alcuna modifica dopo il 7 gennaio 2023. Se hai già aggiornato i PDF, l’esperienza non subirà modifiche

**D. Chi devo contattare se ho ulteriori domande?**

A. È possibile contattare [Supporto Adobe](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;lang=it#support) o aumentare un ticket di supporto.

**D. Cosa succede se non aggiorno il certificato prima del 7 gennaio 2023?**

R. Tutti i documenti PDF estesi utilizzando i certificati di produzione rilasciati dal vecchio &#39;Adobe Root CA&#39; prima del 7 gennaio 2023 continuano a funzionare senza modifiche dopo il 7 gennaio 2023. I PDF estesi con i certificati di valutazione non funzionano dopo la data di scadenza.

**D. La descrizione dei nuovi certificati è diversa da quella dei vecchi certificati?**

A. La descrizione dei nuovi certificati delle estensioni Acrobat Reader menziona **G3-P24** come nome del programma. Nella descrizione dei certificati precedenti (certificati basati su &quot;Adobe Root CA&quot;), **P24** è indicato come nome del programma.

**D. Come posso ottenere i certificati più recenti?**

A. Tutti i clienti Forms autorizzati (con licenza attiva) possono scaricare i nuovi certificati (certificati basati su &quot;Adobe Root CA G2&quot;) dal [Sito Web Adobe Licensing](https://licensing.adobe.com/). Se non riesci a trovare il certificato sul sito Web Adobe Licensing, contatta [Supporto Adobe](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;lang=en#support) o aumentare un ticket di supporto.

**D. I miei documenti PDF estesi utilizzando i certificati rilasciati da &quot;Adobe Root CA&quot; (la vecchia autorità di certificazione) continuano a funzionare dopo il 7 gennaio 2023?**

R. Sì, tutti i documenti PDF estesi utilizzando i certificati di produzione rilasciati dalla &quot;Adobe Root CA&quot; (la vecchia autorità di certificazione) prima del 7 gennaio 2023, continuano a funzionare senza alcuna modifica dopo il 7 gennaio 2023. I documenti PDF estesi con certificati di valutazione cessano di funzionare oltre la data di scadenza.

**D. Quale versione di Adobe Acrobat Reader è necessaria per continuare a utilizzare i documenti di PDF estesi con i certificati rilasciati da &quot;Adobe Root CA&quot; (la vecchia autorità di certificazione)?**

A. Adobe Acrobat Reader 2020 o versione successiva è necessario per utilizzare i documenti PDF estesi con &quot;Adobe Root CA&quot; (la vecchia autorità di certificazione). È la versione supportata di Acrobat Reader al momento della pubblicazione del documento. Se utilizzi un [versione non supportata di Adobe Acrobat](https://helpx.adobe.com/it/support/programs/eol-matrix.html), l’Adobe consiglia di: [scarica e installa la versione più recente di Adobe Acrobat Reader](https://get.adobe.com/reader/).

**D. Quale versione di Adobe Acrobat Reader è necessaria per continuare a utilizzare i documenti di PDF estesi con i certificati rilasciati da &quot;Adobe Root CA 2&quot; (la nuova autorità di certificazione)?**

A. Adobe Acrobat Reader 2020 o versione successiva è necessario per utilizzare i documenti PDF estesi con &quot;Adobe Root CA 2&quot; (la nuova autorità di certificazione). Se utilizzi un [versione non supportata di Adobe Acrobat Reader](https://helpx.adobe.com/support/programs/eol-matrix.html), l’Adobe consiglia di: [scarica e installa la versione più recente di Adobe Acrobat Reader](https://get.adobe.com/reader/).

**D. Posso eliminare un vecchio certificato delle estensioni Acrobat Reader e aggiungerne uno nuovo su un server Adobe Experience Manager Forms mentre continuo a utilizzare l&#39;alias esistente?**

R. Sì, puoi eliminare un vecchio certificato delle estensioni Acrobat Reader e aggiungerne uno nuovo con l’alias esistente a un server Adobe Experience Manager Forms.

**D. Posso mantenere certificati di estensioni Acrobat Reader sia nuovi che vecchi su un server Adobe Experience Manager Forms?**

R. Sì, è possibile conservare entrambi i certificati ma con alias diversi su un server Adobe Experience Manager Forms. Dopo il 7 gennaio 2023, è possibile utilizzare solo il nuovo certificato per estendere un documento PDF in Reader.

**D. Posso importare lo stesso certificato delle estensioni Acrobat Reader in tutti gli ambienti Adobe Experience Manager Forms?**

R. Sì, lo stesso certificato delle estensioni Acrobat Reader può essere utilizzato in più ambienti.

**D. Come posso verificare i diritti di utilizzo applicati a un documento PDF?**

A. È possibile utilizzare il [getDocumentUsageRights](https://experienceleague.adobe.com/docs/experience-manager-65/forms/developer-reference/programming-aem-forms-jee/java-api-quick-start-code-examples/acrobat-reader-dc-extensions-service.html?lang=en#quick-start-soap-mode-retrieving-credential-information-using-the-java-api) API per recuperare le informazioni sui diritti di utilizzo applicati a un documento PDF.

**D. Come posso modificare la password di un file di certificato delle estensioni Acrobat Reader?**

A. In Microsoft Windows, per modificare la password del certificato, installare il certificato utilizzando la console di gestione Microsoft (MMC) e selezionare **Contrassegna la chiave come esportabile**. Una volta installato, esporta il certificato con una chiave privata e utilizza un&#39;altra password per il file PFX.


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
* the user has setup the [development environment](https://experienceleague.adobe.com/docs/experience-manager-65/developing/devtools/howto-projects-eclipse.html) and has access to it.
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

You can use the Trust Store Management pages to import a new credential. The Trust Store may contain more than one Reader Extensions credential. You must designate one of those credentials as the default Reader Extensions credential. The default credential is used when a Workbench user is unable to determine which credential to use during process creation. These rules apply to default credentials:

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

For example keytool -v -list -storetype pkcs12 -keystore 1005566.pfx where 1005566.pfx is the name of my pfx file

<!-- ### Remove usage rights from existing rights-enabled PDF documents

Remove usage rights from existing rights-enabled PDF documents before applying usage rights with latest credentials. You can remove the usage rights for a document by invoking the removeUsageRights API from within the docAssuranceServiceAPI. For detailed information, see [Remove Usage Rights](/help/forms/using/aem-document-services-programmatically.md#removing-usage-rights) document.

#### Apply the usage rights to PDF documents 

To apply usage rights in an AEM Forms on OSGi environment, Create custom OSGi service to usage rights to the documents. You can also create a servlet with a POST method to return the reader extended PDF to the user. For detailed instructions, see [Applying Reader Extensions](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/document-services/apply-reader-extension-rights-to-pdf.html).  -->
