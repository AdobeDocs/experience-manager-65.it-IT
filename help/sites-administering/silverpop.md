---
title: Integrazione con Silverpop Engage
seo-title: Integrating with Silverpop Engage
description: Scopri come integrare AEM con Silverpop Engage
seo-description: Learn how to integrate AEM with Silverpop Engage
uuid: e17deeb6-5339-4ead-9086-cbe2167cdec6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 01029a80-f80e-450c-9c73-16d0662af26d
docset: aem65
exl-id: 6c4b8aaa-bda0-4066-a3fc-d91a5ab1621c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 2%

---

# Integrazione con Silverpop Engage{#integrating-with-silverpop-engage}

>[!NOTE]
>
>L&#39;integrazione Silverpop è **not** disponibile in dotazione. È necessario scaricare il [Pacchetto di integrazione Silverpop](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/aem620/product/cq-mcm-integrations-silverpop-content) da Condivisione pacchetti e installalo nell&#39;istanza. Dopo aver installato il pacchetto, puoi configurarlo come descritto in questo documento.

L’integrazione di AEM con Silverpop Engage consente di gestire e inviare e-mail create in AEM tramite Silverpop. Consente inoltre di utilizzare le funzioni di gestione dei lead di Silverpop tramite moduli AEM su pagine AEM.

L’integrazione offre le seguenti funzionalità:

* La possibilità di creare e-mail in AEM e pubblicarle su Silverpop per la distribuzione.
* Possibilità di impostare l’azione di un modulo AEM per creare un utente con sottoscrizione Silverpop.

Dopo la configurazione di Silverpop Engage, puoi pubblicare newsletter o e-mail su Silverpop Engage.

## Creazione di una configurazione Silverpop {#creating-a-silverpop-configuration}

Le configurazioni Silverpop possono essere aggiunte tramite **Servizi cloud**, **Strumenti** oppure **Endpoint API**. Tutti i metodi sono descritti in questa sezione.

### Configurazione di Silverpop tramite Cloudservices {#configuring-silverpop-via-cloudservices}

Per creare una configurazione Silverpop nei Cloud Services:

1. In AEM, tocca o fai clic su **Strumenti** > **Distribuzione** > **Cloud Services**. (o direttamente all&#39;indirizzo `https://<hostname>:<port>/etc/cloudservices.html`.)
1. In Servizi di terze parti, fai clic su **Interazione Silverop** e poi **Configura**. Viene visualizzata la finestra di configurazione Silverpop.

   >[!NOTE]
   >
   >Silverpop Engage non è disponibile come opzione nei servizi di terze parti a meno che tu non scarichi il pacchetto da Package Share.

1. Inserisci un titolo e, facoltativamente, un nome e fai clic su **Crea**. Viene visualizzata la finestra di configurazione** Silverpop Settings**.
1. Immetti nome utente e password e seleziona un endpoint API dall’elenco a discesa.
1. Fai clic su **Connettiti a Silverpop.** Una volta effettuata la connessione, viene visualizzata una finestra di dialogo di successo. Fai clic su **OK** per uscire dalla finestra. Per passare a Silverpop fai clic su **Vai a Silverpop Engage**.
1. Silverpop è stato configurato. Per modificare la configurazione, fai clic su **Modifica**.
1. Inoltre, il framework Silverpop Engage può essere configurato per azioni personalizzate fornendo titolo e nome (facoltativo). Fai clic su Crea per creare correttamente il framework per la connessione Silverpop già configurata.

   Le colonne di estensione dei dati importate possono essere utilizzate in un secondo momento tramite il componente AEM - **Testo e personalizzazione**.

### Configurazione di Silverpop tramite Strumenti {#configuring-silverpop-via-tools}

Per creare una configurazione Silverpop in Strumenti:

1. In AEM, tocca o fai clic su **Strumenti** > **Distribuzione** > **Cloud Services**. Oppure puoi navigare direttamente da `https://<hostname>:<port>/misadmin#/etc`.
1. Seleziona **Strumenti**, quindi **Configurazioni Cloud Services,** then **Silverpop Engage**.
1. Fai clic su **Nuovo** per aprire la finestra **Crea pagina**.

   ![chlimage_1-6](assets/chlimage_1-6.jpeg)

1. Inserisci il **Titolo** e facoltativamente **Nome** e fai clic su **Crea**.
1. Immettere le informazioni di configurazione descritte al punto 4 della procedura precedente. Segui questa procedura per completare la configurazione di Silverpop.

### Aggiunta di più configurazioni {#adding-multiple-configurations}

Per aggiungere più configurazioni:

1. Nella pagina di benvenuto, fai clic su **Cloud Services** e fai clic su **Silverpop Engage**. Fai clic su **Mostra configurazioni** che appare se sono disponibili una o più configurazioni Silverpop. Sono elencate tutte le configurazioni disponibili.
1. Fai clic sul pulsante **+** Accedi a Configurazioni disponibili. Viene aperta la **Creare configurazioni** finestra. Segui la procedura di configurazione precedente per creare una nuova configurazione.

### Configurazione dei punti finali API per la connessione a Silverpop {#configuring-api-end-points-for-connecting-to-silverpop}

Attualmente, AEM ha sei punti finali non sicuri (da 1 a 6). Silverpop ora fornisce due nuovi punti finali e punti finali di connessione modificati per quelli esistenti.

Per configurare gli endpoint API:

1. Vai a `/libs/mcm/silverpop/components/silverpoppage/dialog/items/general/items/apiendpoint/options node` su `https://<hostname>:<port>/crxde.`
1. Fai clic con il pulsante destro del mouse e seleziona **Crea**, quindi **Crea nodo**.
1. Inserisci il **Nome** come `sp-e0` e scegli **Tipo** come `cq:Widget`.
1. Aggiungi due proprietà al nodo appena aggiunto:

   1. **Nome**: `text`, **Tipo**: `String`, **Valore**: `Engage 0`
   1. **Nome**: `value`, **Tipo**: `String`, **Valore**: `https://api0.silverpop.com`

   ![chlimage_1-42](assets/chlimage_1-42.png)

   Fai clic sul pulsante &quot;Salva tutto&quot;.

1. Crea un altro nodo con **Nome** come `sp-e7` e **Tipo** come `cq:Widget`.

   Aggiungi due proprietà al nodo appena aggiunto:

   1. **Nome**: `text`, **Tipo**: `String`, **Valore**: `Pilot`
   1. **Nome**: `value`, **Tipo**: `String`, **Valore**: `https://apipilot.silverpop.com/XMLAPI`

1. Per modificare i punti finali dell’API esistenti (da 1 a 6), fai clic su ciascuno di essi uno per uno e sostituisci i valori come segue:

   | **Nome nodo** | **Valore del punto finale esistente** | **Nuovo valore del punto finale** |
   |---|---|---|
   | sp-e1 | https://api.engage1.silverpop.com/XMLAPI | https://api1.silverpop.com |
   | sp-e2 | https://api.engage2.silverpop.com/XMLAPI | https://api2.silverpop.com |
   | sp-e3 | https://api.engage3.silverpop.com/XMLAPI | https://api3.silverpop.com |
   | sp-e4 | https://api.engage4.silverpop.com/XMLAPI | https://api4.silverpop.com |
   | sp-e5 | https://api.engage5.silverpop.com/XMLAPI | https://api5.silverpop.com |
   | sp-e6 | https://api.pilot.silverpop.com/XMLAPI | https://api6.silverpop.com |

1. Fai clic su **Salva tutto**. AEM è ora pronto per il collegamento a Silverpop su punti finali protetti.

   ![chlimage_1-7](assets/chlimage_1-7.jpeg)
