---
title: Salesforce Commerce Cloud
seo-title: Salesforce Commerce Cloud / Demandware
description: Scopri come distribuire eCommerce con Salesforce Commerce Cloud / Demandware.
seo-description: Scopri come distribuire eCommerce con Salesforce Commerce Cloud / Demandware.
uuid: c0270632-bdd2-4dba-bbbe-312757ea20f4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: e-commerce
content-type: reference
discoiquuid: 52cc3162-b638-410d-854a-383399e2effb
docset: aem65
pagetitle: Deploying eCommerce with Demandware
redirecttarget: https //github.com/adobe/commerce-salesforce
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Salesforce Commerce Cloud{#salesforce-commerce-cloud}

L&#39;implementazione dei pacchetti eCommerce necessari fornirà la funzionalità completa del framework eCommerce, insieme all&#39;implementazione di riferimento della funzionalità eCommerce come fornito con un&#39;implementazione Salesforce Commerce Cloud / Demandware (incluso un catalogo dimostrativo).

## Pacchetti necessari per eCommerce con Salesforce Commerce Cloud {#packages-needed-for-ecommerce-with-salesforce-commerce-cloud}

Per installare la funzionalità eCommerce è necessario disporre di:

* Framework AEM eCommerce:

   * fa parte di un’installazione standard di AEM

* Pacchetto di contenuti AEM Demandware Commerce

   * cq-6.4.0-featurepack-10262

>[!NOTE]
>
>Questa integrazione supporta le istanze Salesforce Commerce Cloud/Demandware configurate per utilizzare OCAPI versione 17.6 o successiva.

### Installazione di eCommerce con Salesforce Commerce Cloud {#installation-of-ecommerce-with-salesforce-commerce-cloud}

Per installare AEM con una configurazione di integrazione Demandware Commerce (tramite il catalogo dimostrativo Geometrixx Outdoors), i passaggi di base sono:

1. [Installare AEM](/help/sites-deploying/deploy.md).
1. Installate il pacchetto di contenuto utilizzando il gestore [](/help/sites-administering/package-manager.md)pacchetti:
1. [Create](/help/sites-authoring/page-authoring.md) tutte le pagine supplementari necessarie in AEM.

>[!NOTE]
>
>Per scaricare i pacchetti, andate a Condivisione [](/help/sites-administering/package-manager.md#package-share)pacchetti.

È necessario configurare la connessione del server tra AEM e Demandware Sandbox. La maggior parte della configurazione è già preconfigurata per l&#39;utilizzo del pacchetto di contenuti demo SiteGenisis fornito con percorsi predefiniti, librerie e così via. Se il connettore viene utilizzato con altri siti e librerie, sarà necessario aggiornare la configurazione.

1. Andate a [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
1. Fate clic su **Demandware Client**.
1. Immettere l&#39;endpoint **di istanza ip o nomehost** come necessario.

   ![chlimage_1-5](assets/chlimage_1-5.png)

1. Fai clic su **Salva**.
1. Fate clic su Plug-in **Demandware TransportHandler per WebDAV**.
1. Impostate l&#39;utente **WebDAV e la password** utente **** WebDAV.

   ![chlimage_1-6](assets/chlimage_1-6.png)

1. Fai clic su **Salva**.

#### Replica {#replication}

La replica deve essere abilitata dopo l&#39;installazione del pacchetto, potete verificare che: [https://localhost:4502/etc/replication/agents.author/demandware.html](https://localhost:4502/etc/replication/agents.author/demandware.html)

>[!NOTE]
>
>L&#39;agente di replica è configurato per impostazione predefinita a livello di registro delle informazioni. Per avere ulteriori informazioni, è possibile impostare il livello di registro su debug.

#### OAuth {#oauth}

Il client OAuth è configurato per funzionare con un&#39;istanza di sandbox Demandware. A scopo di test, non è necessaria alcuna modifica.

Per i sistemi di staging e di produzione, i client OAuth devono essere configurati con l&#39;ID client e la password appropriati.

1. Andate a [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
1. Fate clic su **Demandware Access Token Provider**.

   ![chlimage_1-7](assets/chlimage_1-7.png)

1. Modificate i valori come richiesto e fate clic su **Salva**.

### Sandbox Salesforce Commerce Cloud {#salesforce-commerce-cloud-sandbox}

La sandbox Demandware deve essere configurata per eseguire il nuovo motore modello Velocity.

>[!NOTE]
>
>La seguente procedura guidata non fa parte del connettore AEM Demandware. Viene fornito come parte del pacchetto di contenuti demo per facilitare la configurazione rapida delle pagine demo di SiteGenesis.

1. Andate a [https://localhost:4502/etc/demandware/init.html](https://localhost:4502/etc/demandware/init.html).
1. Fai clic su **Modifica.**
1. Verificate i valori e fate clic su **OK**.
1. Fate clic su **Inizializza**.
1. Passate alla cartella WebDAV e verificate la presenza di file di modello pubblicati, ad esempio in `adobe01-tech-prtnr-na01-dw.demandware.net/on/demandware.servlet/webdav/Sites/Dynamic/SiteGenesis`.

   >[!NOTE]
   >
   >L&#39;estensione sarà `.vs`.

1. Verificate anche i file JS e CSS esportati, ad esempio in `adobe01-tech-prtnr-na01-dw.demandware.net/on/demandware.servlet/webdav/Sites/Libraries/SiteGenesisSharedLibrary`.

