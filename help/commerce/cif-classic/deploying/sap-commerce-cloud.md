---
title: Distribuzione di eCommerce con SAP Commerce Cloud
description: Scopri come implementare Adobe Experience Manager eCommerce con SAP Commerce Cloud.
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
exl-id: ecbd0097-c407-4581-bab2-4729a71df4a3
source-git-commit: eaffc71c23c18d26ec5cbb2bbb7524790c4826fe
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 2%

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

Distribuzione di [pacchetti eCommerce necessari](#packages-needed-for-ecommerce-with-hybris) fornisce la piena funzionalità del framework eCommerce, insieme a un’implementazione di riferimento della funzionalità eCommerce fornita con un’implementazione ibrida (incluso un catalogo dimostrativo)

È disponibile presso la filiale inglese (USA) ( `/content/geometrixx-outdoors/en_US`) del sito Geometrixx Outdoors:

* [Informazioni prodotto](#productinformationwithcolorvariants) (con varianti di colore, se necessario)

* [Panoramica del contenuto del carrello](#shoppingcartcontentoverview)
* [Registrazione cliente](#customersignup) e [Accesso del cliente](#customersignin)

* [Accesso alla console di gestione Hybris](#accesstothehybrismanagementconsole)

### Requisiti tecnici - Hybris Server {#technical-requirements-hybris-server}

L’estensione hybris di eCommerce Integration Framework è stata aggiornata per supportare Hybris 5 (come impostazione predefinita), mantenendo al contempo la compatibilità con le versioni precedenti di [Hybris 4](/help/commerce/cif-classic/developing/sap-commerce-cloud.md#developing-for-hybris).

>[!NOTE]
>
>* Supporta le versioni 18.11 e successive.
>* È necessario Java™ 7 per eseguire [server hybris 5.](https://www.sap.com/products/crm.html)
* Il componente aggiuntivo hybris, il [Acceleratore Telco](https://www.sap.com/products/crm.html), non è supportato dall’estensione AEM.
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
   * un&#39;implementazione di riferimento per illustrare l&#39;uso di hybris ( `geometrixx-outdoors/en_US`)

### Installazione di eCommerce con hybris {#installation-of-ecommerce-with-hybris}

Per installare una configurazione completa (utilizzando il catalogo dimostrativo, i Geometrixx Outdoors), i passaggi di base sono i seguenti:

1. [Installare AEM](/help/sites-deploying/deploy.md).
1. Installare il pacchetto Geometrixx-all

   1. ` [cq-geometrixx-all-pkg](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq60/product/cq-geometrixx-all-pkg)`

1. Installare i pacchetti di contenuti dimostrativi utilizzando [Gestione pacchetti](/help/sites-administering/package-manager.md):

   1. ` [cq-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-hybris-content)`
   1. ` [cq-geometrixx-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-geometrixx-hybris-content)`

1. [Scarica e crea il tuo server ibrido](#download-and-build-your-hybris-server).
1. Crea il catalogo nel motore di eCommerce:

   1. [Configurare il negozio Geometrixx Outdoor](#setup-the-geometrixx-outdoors-store).

1. [Autore](/help/sites-authoring/qg-page-authoring.md) eventuali pagine supplementari necessarie per l’AEM.

>[!CAUTION]
>
L’utilizzo del server ibrido richiede una licenza ibrida separata.

>[!NOTE]
>
Per sviluppatori, [Documentazione API](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation) è disponibile anche per il download.

### Scarica e crea il server ibrido {#download-and-build-your-hybris-server}

I passaggi descritti in questa procedura consentono di scaricare e generare il server ibrido. Vengono inoltre effettuate le configurazioni iniziali necessarie per le connessioni tra hybris e cq. L’estensione è quindi utilizzabile con le impostazioni predefinite.

>[!CAUTION]
>
Le versioni Hybris precedenti alla 5.5.1 non sono supportate.

>[!NOTE]
>
Per completare l&#39;operazione, è necessario [Scanalatura](https://groovy-lang.org/) installato nel sistema.

1. Scarica il file **hybris Commerce Suite** distribuzione dal sito di download hybris.

   >[!CAUTION]
   >
   Per accedervi è necessario un account (da hybris).

1. Decomprimi il file di distribuzione nella posizione desiderata (nota come &lt;hybris-root-directory>).
1. Dalla riga di comando, eseguire le operazioni seguenti:

   ```shell
   cd <hybris-root-directory>/bin/platform
   . ./setantenv.sh
   ant clean all
   cd ../..
   ```

   >[!NOTE]
   >
   Durante l&#39;esecuzione:
   >
   `ant clean all`
   >
   Premi `Return` quando richiesto.

1. Scarica i seguenti file nella cartella principale della distribuzione ibrida estratta,

   ```
       <hybris-root-directory>
   ```


[Ottieni file](/help/sites-deploying/assets/setup.groovy)

   >[!NOTE]
   >
   Per hybris 5.6.0 e versioni successive, utilizzare il seguente file setup.groovy.

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
   A seconda del sistema in uso, il completamento di alcuni di questi passaggi potrebbe richiedere alcuni minuti.

1. Nel browser, accedi al **console di amministrazione di hybris** a:

   [Http://localhost:9002](Http://localhost:9002)

1. Clic **Inizializza** e quindi confermare l&#39;azione di inizializzazione (in quanto elimina i dati esistenti).

   L’avanzamento viene visualizzato nella console, con `FINISHED` che indica il completamento.

   >[!NOTE]
   >
   A seconda del sistema, il completamento dell&#39;operazione potrebbe richiedere alcuni minuti.

### Configurare l’archivio Geometrixx Outdoors {#setup-the-geometrixx-outdoors-store}

Questa procedura consente di caricare e configurare il negozio di dimostrazione - Geometrixx Online.

1. Avvia l’istanza ibrida. Dalla riga di comando, eseguire le operazioni seguenti:

   ```shell
   cd <hybris-root-directory>/bin/platform
   sh hybrisserver.sh
   ```

1. Nel browser, accedi al **console di gestione hybris** a:

   [https://localhost:9002/backoffice](https://localhost:9002/backoffice)

   Usa queste credenziali:
   * nome utente: admin
   * password: nimda

1. Dalla navigazione della barra laterale, espandi **Sistema** e **Strumenti**. Quindi seleziona **Importa** per aprire **Procedura guidata: Importazione CSV** finestra.
1. In **Configurazione** scheda, **Carica** i seguenti **Importa file**:

[Ottieni file](/help/sites-deploying/assets/geometrixx-outdoors-export.csv)

1. Imposta il **Impostazioni internazionali** a:

   `en_US - English (United States)`

1. Apri **Risorse** scheda.
1. **Carica** i seguenti **Media-Zip**:

[Ottieni file](/help/sites-deploying/assets/geometrixx-outdoors-images.zip)

1. Clic **Inizio** per importare i file specificati. Il **Risultato** mostra tutte le voci di registro.

1. Clic **Fine** per chiudere la finestra di importazione.

1. Dalla barra laterale, seleziona **Sistema**, quindi **Strumenti**, quindi **Importa**.

1. **Carica** i seguenti **Importa file**:

[Ottieni file](/help/sites-deploying/assets/base-store.csv)

   Per hybris 5.7, utilizzare quanto segue:

[Ottieni file](/help/sites-deploying/assets/base-store-5_7.csv)

1. Imposta il **Impostazioni internazionali** a:

   `en_US - English (United States)`

1. Clic **Inizio** per importare i file specificati. Il **Risultato** mostra tutte le voci di registro.

1. Clic **Fine** per chiudere la finestra di importazione.

1. Ora puoi utilizzare la cabina di comando del prodotto per visualizzare i cataloghi e i prodotti importati:

   [http://localhost:9002/productcockpit](http://localhost:9002/productcockpit)
