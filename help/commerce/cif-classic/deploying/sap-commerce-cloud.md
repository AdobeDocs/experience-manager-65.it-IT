---
title: Distribuzione di eCommerce con SAP Commerce Cloud
description: Scopri come implementare Adobe Experience Manager eCommerce con SAP Commerce Cloud.
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
exl-id: ecbd0097-c407-4581-bab2-4729a71df4a3
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 1%

---

# COMMERCE CLOUD SAP{#sap-commerce-cloud}

>[!NOTE]
>
>Questa pagina contiene collegamenti al sito web hybris. Per alcune pagine, è necessario un account per accedere.

## Implementazione di eCommerce con SAP Commerce Cloud {#deploying-ecommerce-with-sap-commerce-cloud}

>[!NOTE]
>
>Le procedure seguenti utilizzano il seguente catalogo di dimostrazione per illustrare la distribuzione:
>
>`Geometrixx Outdoors Site English (US)`

La distribuzione dei [pacchetti eCommerce necessari](#packages-needed-for-ecommerce-with-hybris) fornisce tutte le funzionalità del framework eCommerce, insieme a un&#39;implementazione di riferimento della funzionalità eCommerce fornita con un&#39;implementazione ibrida (incluso un catalogo dimostrativo)

È disponibile nel ramo inglese (Stati Uniti) ( `/content/geometrixx-outdoors/en_US`) del sito Geometrixx Outdoors:

* [Informazioni sul prodotto](#productinformationwithcolorvariants) (con varianti di colore se appropriate)

* [Panoramica del contenuto del carrello](#shoppingcartcontentoverview)
* [Registrazione cliente](#customersignup) e [Accesso cliente](#customersignin)

* [Accesso alla console di gestione Hybris](#accesstothehybrismanagementconsole)

### Requisiti tecnici - Hybris Server {#technical-requirements-hybris-server}

L&#39;estensione hybris di eCommerce Integration Framework è stata aggiornata per supportare Hybris 5 (come impostazione predefinita), mantenendo al contempo la compatibilità con le versioni precedenti di [Hybris 4](/help/commerce/cif-classic/developing/sap-commerce-cloud.md#developing-for-hybris).

>[!NOTE]
>
>* Supporta le versioni 18.11 e successive.
>* È necessario Java™ 7 per eseguire il server [hybris 5.](https://www.sap.com/products/crm.html)
>* Il componente aggiuntivo Hybris, [Telco Accelerator](https://www.sap.com/products/crm.html), non è supportato dall&#39;estensione AEM.
>

### Pacchetti necessari per l’e-commerce con ibridi {#packages-needed-for-ecommerce-with-hybris}

Per installare la funzionalità eCommerce, è necessario:

* Il server ibrido
* Quadro per l’eCommerce dell’AEM:

   * fa parte di un impianto AEM standard

* Pacchetto Geometrixx AEM:

   * `cq-geometrixx-all-pkg`

* Pacchetti di contenuti AEM-hybris:

   * `cq-hybris-content-6.3.2`
   * implementazione API specifica per hybris
   * `cq-geometrixx-hybris-content-6.3.2`
   * implementazione di riferimento per illustrare l&#39;utilizzo di hybris ( `geometrixx-outdoors/en_US`)

### Installazione di eCommerce con hybris {#installation-of-ecommerce-with-hybris}

Per installare una configurazione completa (utilizzando il catalogo dimostrativo, i Geometrixx Outdoors), i passaggi di base sono i seguenti:

1. [Installa AEM](/help/sites-deploying/deploy.md).
1. Installare il pacchetto Geometrixx-all

   1. ` [cq-geometrixx-all-pkg](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq60/product/cq-geometrixx-all-pkg)`

1. Installa i pacchetti di contenuti dimostrativi utilizzando [Gestione pacchetti](/help/sites-administering/package-manager.md):

   1. ` [cq-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-hybris-content)`
   1. ` [cq-geometrixx-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-geometrixx-hybris-content)`

1. [Scarica e crea il tuo server ibrido](#download-and-build-your-hybris-server).
1. Crea il catalogo nel motore di eCommerce:

   1. [Configura l&#39;archivio Geometrixx Outdoor](#setup-the-geometrixx-outdoors-store).

1. [Autore](/help/sites-authoring/qg-page-authoring.md) delle pagine supplementari necessarie per l&#39;AEM.

>[!CAUTION]
>
>L’utilizzo del server ibrido richiede una licenza ibrida separata.

>[!NOTE]
>
>Per gli sviluppatori, è disponibile anche la [documentazione API](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation).

### Scarica e crea il server ibrido {#download-and-build-your-hybris-server}

I passaggi descritti in questa procedura consentono di scaricare e generare il server ibrido. Vengono inoltre effettuate le configurazioni iniziali necessarie per le connessioni tra hybris e cq. L’estensione è quindi utilizzabile con le impostazioni predefinite.

>[!CAUTION]
>
>Le versioni Hybris precedenti alla 5.5.1 non sono supportate.

>[!NOTE]
>
>Per completare l&#39;operazione, è necessario installare [Groovy](https://groovy-lang.org/) nel sistema.

1. Scarica la distribuzione **hybris Commerce Suite** dal sito di download hybris.

   >[!CAUTION]
   >
   >Per accedervi è necessario un account (da hybris).

1. Decomprimi il file di distribuzione nel percorso richiesto (indicato come &lt;hybris-root-directory>).
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
   >Premere `Return` quando richiesto.

1. Scarica i seguenti file nella cartella principale della distribuzione ibrida estratta,

   ```
       <hybris-root-directory>
   ```


[Ottieni file](/help/sites-deploying/assets/setup.groovy)

   >[!NOTE]
   >
   >Per hybris 5.6.0 e versioni successive, utilizzare il seguente file setup.groovy.

   5.6.0 e versioni successive

[Ottieni file](/help/sites-deploying/assets/setup-1.groovy)

1. Dalla riga di comando, eseguire le operazioni seguenti:

   * aggiorna la configurazione del server hybris (come richiesto dall’estensione)
   * rigenera il server hybris con la configurazione modificata
   * avviare il server

   ```shell
   groovy setup.groovy
   cd bin/platform
   ant clean all
   sh hybrisserver.sh
   ```

   >[!NOTE]
   >
   >A seconda del sistema in uso, il completamento di alcuni di questi passaggi potrebbe richiedere alcuni minuti.

1. Nel browser, accedi alla **console di amministrazione Hybris** all&#39;indirizzo:

   [http://localhost:9002](http://localhost:9002)

1. Fare clic su **Inizializza** e quindi confermare l&#39;azione di inizializzazione, poiché elimina i dati esistenti.

   L&#39;avanzamento viene visualizzato nella console, con `FINISHED` che indica il completamento.

   >[!NOTE]
   >
   >A seconda del sistema, il completamento dell&#39;operazione potrebbe richiedere alcuni minuti.

### Configurare l’archivio Geometrixx Outdoors {#setup-the-geometrixx-outdoors-store}

Questa procedura consente di caricare e configurare il negozio di dimostrazione - Geometrixx Online.

1. Avvia l’istanza ibrida. Dalla riga di comando, eseguire le operazioni seguenti:

   ```shell
   cd <hybris-root-directory>/bin/platform
   sh hybrisserver.sh
   ```

1. Nel browser, accedi alla **console di gestione Hybris** all&#39;indirizzo:

   [https://localhost:9002/backoffice](https://localhost:9002/backoffice)

   Usa queste credenziali:
   * nome utente: admin
   * password: nimda

1. Dalla navigazione della barra laterale, espandi **Sistema** e **Strumenti**. Quindi seleziona **Importa** per aprire la finestra **Procedura guidata: Importazione CSV**.
1. Nella scheda **Configurazione**, **Carica** il seguente **File di importazione**:

[Ottieni file](/help/sites-deploying/assets/geometrixx-outdoors-export.csv)

1. Impostare **Impostazioni internazionali** su:

   `en_US - English (United States)`

1. Apri la scheda **Risorse**.
1. **Carica** i seguenti **File-ZIP**:

[Ottieni file](/help/sites-deploying/assets/geometrixx-outdoors-images.zip)

1. Fare clic su **Inizio** per importare i file specificati. La scheda **Risultato** mostra tutte le voci di registro.

1. Fai clic su **Fine** per chiudere la finestra di importazione.

1. Dalla barra laterale, seleziona **Sistema**, quindi **Strumenti**, quindi **Importa**.

1. **Carica** il seguente **file di importazione**:

[Ottieni file](/help/sites-deploying/assets/base-store.csv)

   Per hybris 5.7, utilizzare quanto segue:

[Ottieni file](/help/sites-deploying/assets/base-store-5_7.csv)

1. Impostare **Impostazioni internazionali** su:

   `en_US - English (United States)`

1. Fare clic su **Inizio** per importare i file specificati. La scheda **Risultato** mostra tutte le voci di registro.

1. Fai clic su **Fine** per chiudere la finestra di importazione.

1. Ora puoi utilizzare la cabina di comando del prodotto per visualizzare i cataloghi e i prodotti importati:

   [http://localhost:9002/productcockpit](http://localhost:9002/productcockpit)
