---
title: SAP Commerce Cloud
seo-title: SAP Commerce Cloud
description: Scopri come distribuire eCommerce con SAP Commerce Cloud.
seo-description: Scopri come distribuire eCommerce con SAP Commerce Cloud.
uuid: 26ace49c-02d2-4b49-a959-e033def89bd4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: e-commerce
content-type: reference
discoiquuid: c5dcc90a-05d2-4701-a625-2b655ad0b458
docset: aem65
pagetitle: Deploying eCommerce with hybris
translation-type: tm+mt
source-git-commit: 9e39868768d2fc70f587b18d36042e742d5fae45

---


# SAP Commerce Cloud{#sap-commerce-cloud}

>[!NOTE]
>
>Questa pagina contiene collegamenti al sito Web hybris. Per alcune pagine sarà necessario un account per accedere.

## Distribuzione di eCommerce con SAP Commerce Cloud {#deploying-ecommerce-with-sap-commerce-cloud}

>[!NOTE]
>
>Il connettore per AEM 6.5 non è pronto.

>[!NOTE]
>
>Nelle seguenti procedure viene utilizzato il seguente catalogo dimostrativo per illustrare la distribuzione:
>
>`Geometrixx Outdoors Site English (US)`

L&#39;implementazione dei pacchetti [eCommerce](#packages-needed-for-ecommerce-with-hybris) necessari fornirà la funzionalità completa del framework eCommerce, insieme a un&#39;implementazione di riferimento della funzionalità eCommerce come fornito con un&#39;implementazione ibrida (incluso un catalogo dimostrativo)

Questo è disponibile nella sezione inglese (US) del sito Geometrixx Outdoors `/content/geometrixx-outdoors/en_US`:

* [Informazioni](#productinformationwithcolorvariants) sul prodotto (con eventuali varianti di colore)

* [Sovrapposizioni di contenuti del carrello](#shoppingcartcontentoverview)
* [Iscrizione](#customersignup) del cliente e accesso [del cliente](#customersignin)

* [Accesso alla console di gestione ibrida](#accesstothehybrismanagementconsole)

### Requisiti tecnici - hybris Server {#technical-requirements-hybris-server}

L&#39;estensione hybris di eCommerce Integration Framework è stata aggiornata per supportare Hybris 5 (come impostazione predefinita), pur mantenendo la compatibilità con Hybris 4 <!--[Hybris 4](/help/sites-developing/hybris.md#developing-for-hybris). -->

>[!NOTE]
>
>* Supporta fino a hybris 6.4 con OCC versione 2.
>* Sarà necessario Java 7 per eseguire il server [hybris 5.](https://www.hybris.com/en/architecture-technology)
>* Il componente aggiuntivo hybris, [Telco Accelerator](https://www.hybris.com/en/products/telecommunication), non è supportato dall’estensione AEM.
>



### Pacchetti necessari per eCommerce con hybris {#packages-needed-for-ecommerce-with-hybris}

Per installare la funzionalità eCommerce è necessario disporre di:

* Il server hybris, disponibile da [hybris](#configureandbuildthehybrisserver).
* Framework AEM eCommerce:

   * fa parte di un’installazione standard di AEM

* Pacchetto AEM Geometrixx-all:

   * `cq-geometrixx-all-pkg`

* Pacchetti di contenuti ibridi AEM: &quot;

   * 
       &quot;
 cq-hybris-content-6.3.2     
 &quot;     
     
   
   * implementazione API specifica per hybris
   * `cq-geometrixx-hybris-content-6.3.2`
   * un&#39;implementazione di riferimento per illustrare l&#39;uso dell&#39;ibrido ( `geometrixx-outdoors/en_US`)


### Installazione di eCommerce con hybris {#installation-of-ecommerce-with-hybris}

Per installare una configurazione completa (utilizzando il catalogo dimostrativo Geometrixx Outdoors), i passaggi di base sono:

1. [Installare AEM](/help/sites-deploying/deploy.md).
1. Installare il pacchetto Geometrixx-all

   1. ` [cq-geometrixx-all-pkg](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq60/product/cq-geometrixx-all-pkg)`

1. Installate i pacchetti di contenuto dimostrativo utilizzando il gestore [](/help/sites-administering/package-manager.md)pacchetti:

   1. ` [cq-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-hybris-content)`
   1. ` [cq-geometrixx-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-geometrixx-hybris-content)`

1. [Scaricate e create il server](#download-and-build-your-hybris-server)hybris.
1. Crea il catalogo nel tuo motore eCommerce:

   1. [Impostare Geometrixx Outdoor Store](#setup-the-geometrixx-outdoors-store).

1. [Create](/help/sites-authoring/page-authoring.md) tutte le pagine supplementari necessarie in AEM.

>[!CAUTION]
>
>L&#39;utilizzo del server hybris richiede una licenza hybris separata.

>[!NOTE]
>
>Per gli sviluppatori è disponibile anche la documentazione [sulle](/help/sites-developing/ecommerce.md#api-documentation) API.

### Scaricare e creare il server hybris {#download-and-build-your-hybris-server}

I passaggi descritti in questa procedura consentono di scaricare e creare il server hybris. Inoltre, verranno effettuate le configurazioni iniziali necessarie per i collegamenti tra hybris e cq. L&#39;estensione sarà quindi utilizzabile con le impostazioni predefinite.

>[!CAUTION]
>
>Le versioni di Hybris precedenti alla 5.5.1 non sono supportate.

>[!NOTE]
>
>Per completare questo, è necessario [Groovy](https://groovy-lang.org/) installato sul sistema.

1. Scarica la distribuzione **hybris Commerce Suite **dal sito di download di hybris.

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
   >
   >`ant clean all`
   >
   >
   >Premere `Return` quando necessario.

1. Scaricate i seguenti file nella cartella principale della distribuzione degli ibridi estratti,

   ```
       <<i>hybris-root-directory</i>>
   ```

   :

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

1. Nel browser, accedete alla console **di amministrazione** ibrida all’indirizzo:

   [https://localhost:9002](https://localhost:9002)

1. Fare clic su **Inizializza** , quindi confermare l&#39;azione di inizializzazione (in quanto eliminerà i dati esistenti).

   L&#39;avanzamento verrà visualizzato nella console, con `FINISHED` indicazione del completamento.

   >[!NOTE]
   >
   >A seconda del sistema, il completamento dell&#39;operazione potrebbe richiedere alcuni minuti.

### Impostazione di Geometrixx Outdoors Store {#setup-the-geometrixx-outdoors-store}

Questa procedura consente di caricare e configurare lo store dimostrativo Geometrixx Online.

1. Avviate l’istanza hybris. Dalla riga di comando, eseguire le operazioni seguenti:

   ```shell
   cd <hybris-root-directory>/bin/platform
   sh hybrisserver.sh
   ```

1. Nel browser, accedete alla console **di gestione** ibrida all’indirizzo:

   [https://localhost:9002/hmc/hybris](https://localhost:9002/hmc/hybris)

1. Dalla navigazione della barra laterale, esplora **il sistema** e **gli strumenti**. Selezionare **Importa** per aprire la **procedura guidata: Finestra Importazione** CSV.
1. Nella scheda **Configurazione** , **Carica** il seguente file **di** importazione:

   [Ottieni file](assets/geometrixx-outdoors-export.csv)

1. Impostate l&#39;impostazione **delle impostazioni** internazionali su:

   `en_US - English (United States)`

1. Open the **Resources** tab.
1. **Caricate** il file **multimediale ZIP** seguente:

   [Ottieni file](assets/geometrixx-outdoors-images.zip)

1. Fate clic su **Avvia** per importare i file specificati. Nella scheda **Risultato** vengono visualizzate tutte le voci di registro.

1. Fate clic su **Fine** per chiudere la finestra di importazione.

1. Dalla barra laterale, selezionare **Sistema**, quindi **Strumenti**, quindi **Importa**.

1. **Caricate** il seguente file **di** importazione:

   [Ottieni file](assets/base-store.csv)per hybris 5.7, utilizza quanto segue:

   [Ottieni file](assets/base-store-5_7.csv)

1. Impostate l&#39;impostazione **delle impostazioni** internazionali su:

   `en_US - English (United States)`

1. Fate clic su **Avvia** per importare i file specificati. Nella scheda **Risultato** vengono visualizzate tutte le voci di registro.

1. Fate clic su **Fine** per chiudere la finestra di importazione.

1. È ora possibile utilizzare il cockpit prodotto per visualizzare i cataloghi e i prodotti importati:

   [https://localhost:9002/productcockpit](https://localhost:9002/productcockpit)

