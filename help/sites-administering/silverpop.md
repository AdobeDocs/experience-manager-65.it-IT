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
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 1%

---

# Integrazione con Silverpop Engage{#integrating-with-silverpop-engage}

<!-- THIS ENTIRE TOPIC APPEARS OBSOLETE BECAUSE SILVERPOP NO LONGER EXISTS AND THERE ARE NO REDIRECTS FOR THE DOWNLOAD URL BELOW THAT IS 404.
>[!NOTE]
>
>Silverpop integration is **not** available out of the box. You must download the Silverpop integration package `https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/aem620/product/cq-mcm-integrations-silverpop-content` from Package Share and install it on your instance. After you have installed the package, you can configure it as described in this document. -->

L’integrazione dell’AEM con Silverpop Engage consente di gestire e inviare le e-mail create nell’AEM tramite Silverpop. Consente inoltre di utilizzare le funzioni di gestione dei lead di Silverpop tramite i moduli AEM sulle pagine AEM.

L’integrazione offre le seguenti funzioni:

* Possibilità di creare e-mail in AEM e pubblicarle su Silverpop per la distribuzione.
* Possibilità di impostare l&#39;azione di un modulo AEM per creare un abbonato Silverpop.

Dopo aver configurato Silverpop Engage, è possibile pubblicare newsletter o e-mail in Silverpop Engage.

## Creazione di una configurazione Silverpop {#creating-a-silverpop-configuration}

È possibile aggiungere configurazioni Silverpop tramite **Cloud Service**, **Strumenti**, o **Punti finali API**. Tutti i metodi sono descritti in questa sezione.

### Configurazione di Silverpop tramite Cloud Service {#configuring-silverpop-via-cloudservices}

Per creare una configurazione Silverpop in Cloud Service:

1. In AEM, tocca o fai clic su **Strumenti** > **Distribuzione** > **Cloud Service**. (oppure accedere direttamente a `https://<hostname>:<port>/etc/cloudservices.html`.)
1. In servizi di terze parti, fai clic su **Coinvolgimento Silverop** e poi **Configura**. Viene visualizzata la finestra di configurazione Silverpop.

   >[!NOTE]
   >
   >Silverpop Engage non è disponibile come opzione nei servizi di terze parti, a meno che non si scarichi il pacchetto da Condivisione pacchetti.

1. Inserisci un titolo e, facoltativamente, un nome e fai clic su **Crea**. Viene visualizzata la finestra di configurazione** Impostazioni Silverpop**.
1. Immetti il nome utente e la password, quindi seleziona un endpoint API dall’elenco a discesa.
1. Clic **Connettersi a Silverpop.** Una volta stabilita la connessione, viene visualizzata una finestra di dialogo di successo. Clic **OK** quindi si esce dalla finestra. È possibile passare a Silverpop facendo clic su **Vai a Silverpop Engage**.
1. Silverpop configurato. Puoi modificare la configurazione facendo clic su **Modifica**.
1. Inoltre, il framework Silverpop Engage può essere configurato per azioni personalizzate fornendo titolo e nome (facoltativo). Fare clic su Crea per creare il framework per la connessione Silverpop già configurata.

   Le colonne di estensione dei dati importate possono essere successivamente utilizzate tramite il componente AEM - **Testo e personalizzazione**.

### Configurazione di Silverpop tramite Strumenti {#configuring-silverpop-via-tools}

Per creare una configurazione Silverpop in Strumenti:

1. In AEM, tocca o fai clic su **Strumenti** > **Distribuzione** > **Cloud Service**. Oppure naviga direttamente da `https://<hostname>:<port>/misadmin#/etc`.
1. Seleziona **Strumenti**, quindi **Configurazioni Cloud Service,** allora **Coinvolgimento Silverpop**.
1. Clic **Nuovo**.

   ![chlimage_1-6](assets/chlimage_1-6.jpeg)

1. In **Crea pagina** finestra, inserire **Titolo** e facoltativamente **Nome** e fai clic su **Crea**.
1. Immettere le informazioni di configurazione come descritto al punto 4 della procedura precedente. Seguire questa procedura per completare la configurazione di Silverpop.

### Aggiunta di più configurazioni {#adding-multiple-configurations}

Per aggiungere più configurazioni:

1. Nella pagina di benvenuto, fai clic su **Cloud Service** e fai clic su **Coinvolgimento Silverpop**. Clic **Mostra configurazioni** che viene visualizzato se sono disponibili una o più configurazioni Silverpop. Sono elencate tutte le configurazioni disponibili.
1. Fai clic su **+** Accanto a Configurazioni disponibili. Apre il **Creare configurazioni** finestra. Segui la procedura di configurazione precedente per creare una configurazione.

### Configurazione degli endpoint API per la connessione a Silverpop {#configuring-api-end-points-for-connecting-to-silverpop}

Attualmente, l&#39;AEM ha sei endpoint non sicuri (Engage 1 - 6). Silverpop ora fornisce due nuovi punti finali e punti finali di connessione modificati per quelli esistenti.

Per configurare gli endpoint API:

1. Vai a `/libs/mcm/silverpop/components/silverpoppage/dialog/items/general/items/apiendpoint/options node` il `https://<hostname>:<port>/crxde.`
1. Fai clic con il pulsante destro del mouse e seleziona (Copia negli Appunti) **Crea**, quindi **Crea nodo**.
1. Inserisci il **Nome** as `sp-e0` e scegli **Tipo** as `cq:Widget`.
1. Aggiungi due proprietà al nuovo nodo aggiunto:

   1. **Nome**: `text`, **Tipo**: `String`, **Valore**: `Engage 0`
   1. **Nome**: `value`, **Tipo**: `String`, **Valore**: `https://api0.silverpop.com`

   ![chlimage_1-42](assets/chlimage_1-42.png)

   Fare clic su Salva tutto.

1. Crea un altro nodo con **Nome** as `sp-e7` e **Tipo** as `cq:Widget`.

   Aggiungi due proprietà al nuovo nodo aggiunto:

   1. **Nome**: `text`, **Tipo**: `String`, **Valore**: `Pilot`
   1. **Nome**: `value`, **Tipo**: `String`, **Valore**: `https://apipilot.silverpop.com/XMLAPI`

1. Per modificare gli endpoint API esistenti (Coinvolgi 1 - 6), fai clic su ciascuno di essi uno per uno e sostituisci i valori come segue:

   | **Nome nodo** | **Valore endpoint esistente** | **Nuovo valore endpoint** |
   |---|---|---|
   | sp-e1 | `https://api.engage1.silverpop.com/XMLAPI` | `https://api1.silverpop.com` |
   | sp-e2 | `https://api.engage2.silverpop.com/XMLAPI` | `https://api2.silverpop.com` |
   | sp-e3 | `https://api.engage3.silverpop.com/XMLAPI` | `https://api3.silverpop.com` |
   | sp-e4 | `https://api.engage4.silverpop.com/XMLAPI` | `https://api4.silverpop.com` |
   | sp-e5 | `https://api.engage5.silverpop.com/XMLAPI` | `https://api5.silverpop.com` |
   | sp-e6 | `https://api.pilot.silverpop.com/XMLAPI` | `https://api6.silverpop.com` |

1. Clic **Salva tutto**. L&#39;AEM è ora pronto a connettersi a Silverpop tramite endpoint protetti.

   ![chlimage_1-7](assets/chlimage_1-7.jpeg)
