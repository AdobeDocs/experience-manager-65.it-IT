---
title: COMMERCE CLOUD SAP
seo-title: COMMERCE CLOUD SAP
description: Scopri come distribuire eCommerce con SAP Commerce Cloud.
seo-description: Scopri come distribuire eCommerce con SAP Commerce Cloud.
uuid: a16ae42b-9c33-4da8-a130-52b72a779ec7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: e-commerce
content-type: reference
discoiquuid: 44dfa10f-497e-473f-95d4-8dccae7ebf8e
pagetitle: Deploying eCommerce with SAP Commerce Cloud
translation-type: tm+mt
source-git-commit: 328e13eb2ce034b0b1ec7e5e0fb184de9435d1bc
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 0%

---


# COMMERCE CLOUD SAP{#sap-commerce-cloud}

>[!NOTE]
>
>Questa pagina contiene collegamenti al sito Web hybris. Per alcune pagine sarà necessario un account per accedere.

## Distribuzione di eCommerce con Commerce Cloud SAP {#deploying-ecommerce-with-sap-commerce-cloud}

>[!NOTE]
>
>Nelle seguenti procedure viene utilizzato il seguente catalogo dimostrativo per illustrare la distribuzione:
>
>`Geometrixx Outdoors Site English (US)`

L&#39;implementazione dei [pacchetti eCommerce necessari](#packages-needed-for-ecommerce-with-hybris) fornirà tutte le funzionalità del framework eCommerce, insieme a un&#39;implementazione di riferimento della funzionalità eCommerce come fornito con un&#39;implementazione hybris (incluso un catalogo dimostrativo)

Questo è disponibile nella sezione inglese (US) ( `/content/geometrixx-outdoors/en_US`) del sito Geometrixx Outdoors:

* [Informazioni](#productinformationwithcolorvariants)  sul prodotto (con eventuali varianti di colore)

* [Sovrapposizioni di contenuti del carrello](#shoppingcartcontentoverview)
* [Accesso ](#customersignup) e accesso  [del cliente](#customersignin)

* [Accesso alla console di gestione ibrida](#accesstothehybrismanagementconsole)

### Requisiti tecnici - hybris Server {#technical-requirements-hybris-server}

L&#39;estensione hybris di eCommerce Integration Framework è stata aggiornata per supportare Hybris 5 (come impostazione predefinita), mantenendo la compatibilità con le versioni precedenti con [Hybris 4](/help/sites-developing/sap-commerce-cloud.md#developing-for-hybris).

>[!NOTE]
>
>* Supporta le versioni 18.11 e successive.
>* Sarà necessario Java 7 per eseguire il server [hybris 5.](https://www.hybris.com/en/architecture-technology)
>* Il componente aggiuntivo hybris, [Telco Accelerator](https://www.hybris.com/en/products/telecommunication), non è supportato dall&#39;estensione AEM.

>



### Pacchetti necessari per eCommerce con hybris {#packages-needed-for-ecommerce-with-hybris}

Per installare la funzionalità eCommerce è necessario disporre di:

* Il server hybris
* AEM eCommerce framework:

   * fa parte di un&#39;installazione standard AEM

* AEM pacchetto di Geometrixx:

   * `cq-geometrixx-all-pkg`

* AEM pacchetti di contenuti ibridi:

   * `cq-hybris-content-6.3.2`
   * implementazione API specifica per hybris
   * `cq-geometrixx-hybris-content-6.3.2`
   * un&#39;implementazione di riferimento per illustrare l&#39;uso dell&#39;hybris ( `geometrixx-outdoors/en_US`)

### Installazione di eCommerce con hybris {#installation-of-ecommerce-with-hybris}

Per installare una configurazione completa (utilizzando il catalogo dimostrativo, Geometrixx Outdoors), i passaggi di base sono:

1. [Installare AEM](/help/sites-deploying/deploy.md).
1. Installare il pacchetto di Geometrixx

   1. ` [cq-geometrixx-all-pkg](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq60/product/cq-geometrixx-all-pkg)`

1. Installate i pacchetti di contenuto dimostrativo utilizzando il gestore [pacchetti](/help/sites-administering/package-manager.md):

   1. ` [cq-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-hybris-content)`
   1. ` [cq-geometrixx-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-geometrixx-hybris-content)`

1. [Scaricate e create il server](#download-and-build-your-hybris-server) hybris.
1. Crea il catalogo nel tuo motore eCommerce:

   1. [Installare il Geometrixx per esterni](#setup-the-geometrixx-outdoors-store).

1. [Consente di ](/help/sites-authoring/qg-page-authoring.md) immettere le pagine supplementari necessarie in AEM.

>[!CAUTION]
>
>L&#39;utilizzo del server hybris richiede una licenza hybris separata.

>[!NOTE]
>
>Per gli sviluppatori [Documentazione API](/help/sites-developing/ecommerce.md#api-documentation) è disponibile anche per il download.

### Scaricare e creare il server hybris {#download-and-build-your-hybris-server}

I passaggi descritti in questa procedura consentono di scaricare e creare il server hybris. Inoltre, verranno effettuate le configurazioni iniziali necessarie per i collegamenti tra hybris e cq. L&#39;estensione sarà quindi utilizzabile con le impostazioni predefinite.

>[!CAUTION]
>
>Le versioni di Hybris precedenti alla 5.5.1 non sono supportate.

>[!NOTE]
>
>Per completare questa operazione, è necessario installare [Groovy](https://groovy-lang.org/) nel sistema.

1. Scaricate la distribuzione **hybris Commerce Suite** dal sito di download di hybris.

   >[!CAUTION]
   >
   >Sarà necessario un account (da hybris) per accedere a questo.

1. Decomprimete il file di distribuzione nel percorso richiesto (denominato &lt;directory-radice-hybris>).
1. Dalla riga di comando, eseguire le operazioni seguenti:

   ```shell
   cd <hybris-root-directory>/bin/platform
   . ./setantenv.sh
   ant clean all
   cd ../..
   ```

   >[!NOTE]
   >
   >Durante l&#39;esecuzione:
   >
   >`ant clean all`
   >
   >Premere `Return` quando necessario.

1. Scaricate i seguenti file nella cartella principale della distribuzione degli ibridi estratti,

   ```
       <hybris-root-directory>
   ```


   [Ottieni file](assets/setup.groovy)

   >[!NOTE]
   >
   >Per hybris 5.6.0 e versioni successive, utilizzare il seguente setup.groovy.

   5.6.0 e versioni successive

   [Ottieni file](assets/setup-1.groovy)

1. Dalla riga di comando, eseguite quanto segue:

   * aggiornare la configurazione del server hybris (come richiesto dall&#39;estensione)
   * ricreare il server hybris con la configurazione modificata
   * avviare il server

   ```shell
   groovy setup.groovy
   cd bin/platform
   ant clean all
   sh hybrisserver.sh
   ```

   >[!NOTE]
   >
   >A seconda del sistema in uso, il completamento di diversi passaggi potrebbe richiedere alcuni minuti.

1. Nel browser, andate alla **console di amministrazione ibrida** all&#39;indirizzo:

   [Http://localhost:9002](Http://localhost:9002)

1. Fare clic su **Inizializza**, quindi confermare l&#39;azione di inizializzazione (in quanto eliminerà i dati esistenti).

   L&#39;avanzamento verrà visualizzato sulla console, con `FINISHED` indica il completamento.

   >[!NOTE]
   >
   >A seconda del sistema, il completamento dell&#39;operazione potrebbe richiedere alcuni minuti.

### Configurazione dell&#39;archivio Geometrixx Outdoors {#setup-the-geometrixx-outdoors-store}

Questa procedura consente di caricare e configurare il negozio dimostrativo - Geometrixx online.

1. Avviate l’istanza hybris. Dalla riga di comando, eseguire le operazioni seguenti:

   ```shell
   cd <hybris-root-directory>/bin/platform
   sh hybrisserver.sh
   ```

1. Nel browser, andate alla **console di gestione ibrida** all&#39;indirizzo:

   [https://localhost:9002/backoffice](https://localhost:9002/backoffice)

   Utilizzate le seguenti credenziali:
   * username: admin
   * password: nimda

1. Dalla navigazione della barra laterale, esplorare e **System** e **Tools**. Selezionare quindi **Importa** per aprire la **procedura guidata: Finestra Importazione CSV**.
1. Nella scheda **Configuration**, **Upload** il seguente file **Import**:

   [Ottieni file](assets/geometrixx-outdoors-export.csv)

1. Impostare l&#39;impostazione **Impostazioni internazionali** su:

   `en_US - English (United States)`

1. Aprire la scheda **Risorse**.
1. **Caricate** il file  **ZIP** seguente:

   [Ottieni file](assets/geometrixx-outdoors-images.zip)

1. Fare clic su **Start** per importare i file specificati. Nella scheda **Result** vengono visualizzate tutte le voci di registro.

1. Fate clic su **Fine** per chiudere la finestra di importazione.

1. Dalla barra laterale, selezionare **Sistema**, quindi **Strumenti**, quindi **Importa**.

1. **Carica** il file **di** importazione seguente:

   [Ottieni file](assets/base-store.csv)

   Per hybris 5.7, utilizzare quanto segue:

   [Ottieni file](assets/base-store-5_7.csv)

1. Impostare l&#39;impostazione **Impostazioni internazionali** su:

   `en_US - English (United States)`

1. Fare clic su **Start** per importare i file specificati. Nella scheda **Result** vengono visualizzate tutte le voci di registro.

1. Fate clic su **Fine** per chiudere la finestra di importazione.

1. È ora possibile utilizzare il cockpit prodotto per visualizzare i cataloghi e i prodotti importati:

   [http://localhost:9002/productcockpit](http://localhost:9002/productcockpit)

