---
title: Commerce Cloud SAP
seo-title: Commerce Cloud SAP
description: Scopri come implementare eCommerce con SAP Commerce Cloud.
seo-description: Scopri come implementare eCommerce con SAP Commerce Cloud.
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
translation-type: tm+mt
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 2%

---

# Commerce Cloud SAP{#sap-commerce-cloud}

>[!NOTE]
>
>Questa pagina contiene i collegamenti al sito web hybris. Per alcune pagine sarà necessario un account per effettuare l’accesso.

## Distribuzione di eCommerce con SAP Commerce Cloud {#deploying-ecommerce-with-sap-commerce-cloud}

>[!NOTE]
>
>Per illustrare la distribuzione, le procedure seguenti utilizzano il seguente catalogo dimostrativo:
>
>`Geometrixx Outdoors Site English (US)`

La distribuzione dei [pacchetti eCommerce necessari](#packages-needed-for-ecommerce-with-hybris) fornirà tutte le funzionalità del framework eCommerce, insieme a un&#39;implementazione di riferimento della funzionalità eCommerce fornita con un&#39;implementazione ibrida (incluso un catalogo dimostrativo)

Questo è disponibile sotto il ramo inglese (US) ( `/content/geometrixx-outdoors/en_US`) del sito Geometrixx Outdoors:

* [Informazioni sul prodotto](#productinformationwithcolorvariants)  (con varianti di colore se appropriato)

* [Panoramica dei contenuti del carrello](#shoppingcartcontentoverview)
* [Accesso del cliente ](#customersignup) e accesso  [del cliente](#customersignin)

* [Accesso alla console di gestione ibrida](#accesstothehybrismanagementconsole)

### Requisiti tecnici - hybris Server {#technical-requirements-hybris-server}

L&#39;estensione hybris di eCommerce Integration Framework è stata aggiornata per supportare Hybris 5 (come impostazione predefinita), mantenendo la compatibilità con le versioni precedenti con [Hybris 4](/help/commerce/cif-classic/developing/sap-commerce-cloud.md#developing-for-hybris).

>[!NOTE]
>
>* Supporta le versioni 18.11 e successive.
>* Sarà necessario Java 7 per eseguire il server [hybris 5.](https://www.hybris.com/en/architecture-technology)
>* L&#39;estensione AEM non supporta il componente aggiuntivo hybris [Telco Accelerator](https://www.hybris.com/en/products/telecommunication).

>



### Pacchetti necessari per eCommerce con hybris {#packages-needed-for-ecommerce-with-hybris}

Per installare la funzionalità eCommerce è necessario:

* Il tuo server ibrido
* Quadro AEM eCommerce:

   * fa parte di un&#39;installazione standard AEM

* AEM pacchetto tutto Geometrixx:

   * `cq-geometrixx-all-pkg`

* AEM pacchetti di contenuti ibridi:

   * `cq-hybris-content-6.3.2`
   * implementazione API specifica per hybris
   * `cq-geometrixx-hybris-content-6.3.2`
   * un&#39;implementazione di riferimento per illustrare l&#39;uso dell&#39;hybris ( `geometrixx-outdoors/en_US`)

### Installazione di e-commerce con hybris {#installation-of-ecommerce-with-hybris}

Per installare una configurazione completa (utilizzando il catalogo dimostrativo, Geometrixx Outdoors), i passaggi fondamentali sono i seguenti:

1. [Installa AEM](/help/sites-deploying/deploy.md).
1. Installa il pacchetto Geometrixx-all

   1. ` [cq-geometrixx-all-pkg](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq60/product/cq-geometrixx-all-pkg)`

1. Installa i pacchetti di contenuti dimostrativi utilizzando il [gestore di pacchetti](/help/sites-administering/package-manager.md):

   1. ` [cq-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-hybris-content)`
   1. ` [cq-geometrixx-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-geometrixx-hybris-content)`

1. [Scarica e genera il tuo hybris Server](#download-and-build-your-hybris-server).
1. Crea il catalogo nel tuo motore eCommerce:

   1. [Imposta il Negozio](#setup-the-geometrixx-outdoors-store) per esterni Geometrixx.

1. [](/help/sites-authoring/qg-page-authoring.md) Autorizza le pagine supplementari necessarie in AEM.

>[!CAUTION]
>
>L&#39;utilizzo del server hybris richiede una licenza hybris separata.

>[!NOTE]
>
>Per gli sviluppatori [È disponibile anche la documentazione API](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation) per il download.

### Scarica e genera il tuo server hybris {#download-and-build-your-hybris-server}

I passaggi descritti in questa procedura consentono di scaricare e creare il server hybris. Sarà anche fare le configurazioni iniziali necessarie per le connessioni tra hybris e cq. L&#39;estensione sarà quindi utilizzabile con le impostazioni predefinite.

>[!CAUTION]
>
>Le versioni di Hybris precedenti alla 5.5.1 non sono supportate.

>[!NOTE]
>
>Per completare questa operazione, è necessario [Groovy](https://groovy-lang.org/) installato sul sistema.

1. Scarica la distribuzione **hybris Commerce Suite** dal sito di download di hybris.

   >[!CAUTION]
   >
   >Per accedere a questo, è necessario un account (da hybris).

1. Decomprimere il file di distribuzione nella posizione richiesta (indicata come &lt;hybris-root-directory>).
1. Dalla riga di comando, esegui quanto segue:

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

1. Scarica i seguenti file nella cartella principale della distribuzione di hybris estratta,

   ```
       <hybris-root-directory>
   ```


   [Ottieni file](/help/sites-deploying/assets/setup.groovy)

   >[!NOTE]
   >
   >Per hybris 5.6.0 e versioni successive, utilizzare il seguente setup.groovy.

   5.6.0 e versioni successive

   [Ottieni file](/help/sites-deploying/assets/setup-1.groovy)

1. Dalla riga di comando, esegui quanto segue in:

   * aggiorna la configurazione del server hybris (come richiesto dall&#39;estensione)
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
   >A seconda del sistema, il completamento di alcuni di questi passaggi potrebbe richiedere alcuni minuti.

1. Nel browser, accedi alla **console di amministrazione ibrida** all&#39;indirizzo:

   [Http://localhost:9002](Http://localhost:9002)

1. Fare clic su **Inizializza**, quindi confermare l&#39;azione di inizializzazione (in quanto eliminerà i dati esistenti).

   L’avanzamento viene visualizzato nella console e `FINISHED` indica il completamento.

   >[!NOTE]
   >
   >A seconda del sistema, il completamento dell’operazione potrebbe richiedere alcuni minuti.

### Imposta l&#39;archivio Geometrixx Outdoors {#setup-the-geometrixx-outdoors-store}

Questa procedura consente di caricare e configurare l&#39;archivio dimostrativo - Geometrixx Online.

1. Avvia la tua istanza di hybris. Dalla riga di comando, esegui quanto segue:

   ```shell
   cd <hybris-root-directory>/bin/platform
   sh hybrisserver.sh
   ```

1. Nel browser, accedi alla **console di gestione ibrida** all&#39;indirizzo:

   [https://localhost:9002/backoffice](https://localhost:9002/backoffice)

   Utilizzare le seguenti credenziali:
   * nome utente: admin
   * password: nimda

1. Dalla navigazione della barra laterale, espandi **System** e **Tools**. Quindi selezionare **Importa** per aprire la procedura guidata **: Finestra Importazione CSV**.
1. Nella scheda **Configurazione**, **Carica** il seguente **File di importazione**:

   [Ottieni file](/help/sites-deploying/assets/geometrixx-outdoors-export.csv)

1. Imposta le **impostazioni internazionali** su:

   `en_US - English (United States)`

1. Apri la scheda **Risorse** .
1. **** Carica il seguente file  **multimediale-ZIP**:

   [Ottieni file](/help/sites-deploying/assets/geometrixx-outdoors-images.zip)

1. Fare clic su **Start** per importare i file specificati. La scheda **Risultato** mostrerà tutte le voci di registro.

1. Fai clic su **Fine** per chiudere la finestra di importazione.

1. Dalla barra laterale selezionare **Sistema**, quindi **Strumenti**, quindi **Importa**.

1. **** Carica il seguente file  **di importazione**:

   [Ottieni file](/help/sites-deploying/assets/base-store.csv)

   Per hybris 5.7, utilizzare quanto segue:

   [Ottieni file](/help/sites-deploying/assets/base-store-5_7.csv)

1. Imposta le **impostazioni internazionali** su:

   `en_US - English (United States)`

1. Fare clic su **Start** per importare i file specificati. La scheda **Risultato** mostrerà tutte le voci di registro.

1. Fai clic su **Fine** per chiudere la finestra di importazione.

1. È ora possibile utilizzare il cockpit prodotto per visualizzare i cataloghi e i prodotti importati:

   [http://localhost:9002/productcockpit](http://localhost:9002/productcockpit)
