---
title: Integrazione con Silverpop Engage
seo-title: Integrazione con Silverpop Engage
description: Scopri come integrare AEM con il coinvolgimento di Silverpop
seo-description: Scopri come integrare AEM con il coinvolgimento di Silverpop
uuid: e17deeb6-5339-4ead-9086-cbe2167cdec6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 01029a80-f80e-450c-9c73-16d0662af26d
docset: aem65
translation-type: tm+mt
source-git-commit: 4e5e6ef022dc9f083859e13ab9c86b622fc3d46e

---


# Integrazione con Silverpop Engage{#integrating-with-silverpop-engage}

>[!NOTE]
>
>L&#39;integrazione Silverpop **non** è disponibile. Dovete scaricare il pacchetto [di integrazione](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/aem620/product/cq-mcm-integrations-silverpop-content) Silverpop da Package Share e installarlo nell&#39;istanza. Dopo aver installato il pacchetto, potete configurarlo come descritto in questo documento.

L’integrazione di AEM con Silverpop Engage consente di gestire e inviare e-mail create in AEM tramite Silverpop. Consente inoltre di utilizzare le funzioni di gestione dei lead di Silverpop tramite moduli AEM sulle pagine AEM.

L&#39;integrazione offre le seguenti funzionalità:

* La possibilità di creare e pubblicare e-mail in AEM e pubblicarle in Silverpop per la distribuzione.
* Possibilità di impostare l’azione di un modulo AEM per creare un utente con sottoscrizione Silverpop.

Una volta configurato Silverpop Engage, potete pubblicare newsletter o e-mail su Silverpop Engage.

## Creazione di una configurazione Silverpop {#creating-a-silverpop-configuration}

Le configurazioni Silverpop possono essere aggiunte tramite i punti **finali** Cloudservices **,** Tools **o** API. Tutti i metodi sono descritti in questa sezione.

### Configurazione di Silverpop tramite Cloudservices {#configuring-silverpop-via-cloudservices}

Per creare una configurazione Silverpop nei servizi cloud:

1. In AEM, tocca o fai clic su **Strumenti** > **Distribuzione** > Servizi **** cloud. (oppure accedere direttamente a `https://<hostname>:<port>/etc/cloudservices.html`.)
1. In Servizi di terze parti, fai clic su **Coinvolgi** Silverop e quindi su **Configura**. Viene visualizzata la finestra di configurazione Silverpop.

   >[!NOTE]
   >
   >Silverpop Engage non è disponibile come opzione in servizi di terze parti a meno che non scaricate il pacchetto da Package Share.

1. Enter a title and optionally, a name and click **Create**. Viene visualizzata la finestra di configurazione** Silverpop Settings**.
1. Immettete nome utente e password e selezionate un endpoint API dall&#39;elenco a discesa.
1. Fate clic su **Connetti a Silverpop.** Una volta stabilita la connessione, viene visualizzata una finestra di dialogo di successo. Fare clic su **OK** per uscire dalla finestra. Per accedere a Silverpop, fai clic su **Vai a Coinvolgimento** Silverpop.
1. Silverpop è stato configurato. Per modificare la configurazione, fai clic su **Modifica**.
1. Inoltre, il framework di coinvolgimento Silverpop può essere configurato per azioni personalizzate fornendo titolo e nome (facoltativo). Fate clic su Crea per creare correttamente il framework per la connessione Silverpop già configurata.

   Le colonne di estensione dei dati importate possono essere utilizzate in seguito tramite il componente AEM - **Testo e personalizzazione**.

### Configurazione di Silverpop tramite Strumenti {#configuring-silverpop-via-tools}

Per creare una configurazione Silverpop in Strumenti:

1. In AEM, tocca o fai clic su **Strumenti** > **Distribuzione** > Servizi **** cloud. Oppure andate direttamente a `https://<hostname>:<port>/misadmin#/etc`.
1. Seleziona **Strumenti**, quindi Configurazioni dei servizi **cloud,** quindi Coinvolgi **Silverpop**.
1. Fai clic su **Nuovo** per aprire la finestra **Crea pagina**.

   ![chlimage_1-6](assets/chlimage_1-6.jpeg)

1. Immettete il **Titolo** ed eventualmente il **Nome**, quindi fate clic su **Crea**.
1. Immettete le informazioni di configurazione come indicato al punto 4 della procedura precedente. Seguite questa procedura per completare la configurazione di Silverpop.

### Aggiunta di più configurazioni {#adding-multiple-configurations}

Per aggiungere più configurazioni:

1. Nella pagina di benvenuto, fai clic su **Cloud Services** e fai clic su **Silverpop Engage**. Fate clic sul pulsante **Mostra configurazioni** che viene visualizzato se sono disponibili una o più configurazioni Silverpop. Vengono elencate tutte le configurazioni disponibili.
1. Fate clic sul segno **+** accanto a Configurazioni disponibili. Viene visualizzata la finestra **Crea configurazioni** . Seguite la procedura di configurazione precedente per creare una nuova configurazione.

### Configurazione dei punti finali dell&#39;API per la connessione a Silverpop {#configuring-api-end-points-for-connecting-to-silverpop}

Attualmente, AEM ha sei punti finali non protetti (da 1 a 6). Silverpop offre ora due nuovi punti finali e due punti finali di connessione modificati per quelli esistenti.

Per configurare i punti finali dell&#39;API:

1. Vai a `/libs/mcm/silverpop/components/silverpoppage/dialog/items/general/items/apiendpoint/options node``https://<hostname>:<port>/crxde.`
1. Fai clic con il pulsante destro del mouse e seleziona **Crea**, quindi **Crea nodo**.
1. Immettete il **nome** come `sp-e0` e scegliete **Tipo** come `cq:Widget`.
1. Aggiungi due proprietà al nodo appena aggiunto:

   1. **Nome**: `text`, **Tipo**: `String`, **Valore**: `Engage 0`
   1. **Nome**: `value`, **Tipo**: `String`, **Valore**: `https://api0.silverpop.com`
   ![chlimage_1-42](assets/chlimage_1-42.png)

   Fare clic sul pulsante &quot;Salva tutto&quot;.

1. Crea un altro nodo con **Nome** come `sp-e7` e **Tipo** come `cq:Widget`.

   Aggiungi due proprietà al nodo appena aggiunto:

   1. **Nome**: `text`, **Tipo**: `String`, **Valore**: `Pilot`
   1. **Nome**: `value`, **Tipo**: `String`, **Valore**: `https://apipilot.silverpop.com/XMLAPI`

1. Per modificare i punti finali dell&#39;API (Coinvolgi da 1 a 6), fai clic su ciascuno di essi uno per uno e sostituisci i valori come segue:

   | **Nome nodo** | **Valore punto finale esistente** | **Nuovo valore punto finale** |
   |---|---|---|
   | sp-e1 | https://api.engage2.silverpop.com/XMLAPI | https://api1.silverpop.com |
   | sp-e2 | https://api.engage2.silverpop.com/XMLAPI | https://api2.silverpop.com |
   | sp-e3 | https://api.engage3.silverpop.com/XMLAPI | https://api3.silverpop.com |
   | sp-e4 | https://api.engage4.silverpop.com/XMLAPI | https://api4.silverpop.com |
   | sp-e5 | https://api.engage5.silverpop.com/XMLAPI | https://api5.silverpop.com |
   | sp-e6 | https://api.pilot.silverpop.com/XMLAPI | https://api6.silverpop.com |

1. Fate clic su **Salva tutto**. AEM è ora pronto per connettersi a Silverpop oltre i punti finali protetti.

   ![chlimage_1-7](assets/chlimage_1-7.jpeg)

