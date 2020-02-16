---
title: Configurazione cloud
seo-title: Configurazione cloud
description: L'associazione di un'app on-demand a una configurazione cloud consente ad Adobe Experience Manager (AEM) di comunicare direttamente con un progetto ospitato da Mobile On-Demand stabilendo un collegamento bidirezionale. Segui questa pagina per saperne di più.
seo-description: L'associazione di un'app on-demand a una configurazione cloud consente ad Adobe Experience Manager (AEM) di comunicare direttamente con un progetto ospitato da Mobile On-Demand stabilendo un collegamento bidirezionale. Segui questa pagina per saperne di più.
uuid: f377f2af-864b-43df-9d42-4a5fd6cd70d5
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: d0d29b99-53d4-4b0d-947b-39d91b381de7
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configurazione cloud{#cloud-configuration}

>[!NOTE]
>
>Adobe consiglia di utilizzare SPA Editor per i progetti che richiedono il rendering lato client basato sul framework dell&#39;applicazione a pagina singola (ad es. React). [Per saperne di più](/help/sites-developing/spa-overview.md).

L&#39;associazione di un&#39;app on-demand a una configurazione cloud consente ad Adobe Experience Manager (AEM) di comunicare direttamente con un progetto ospitato da Mobile On-Demand stabilendo un collegamento bidirezionale. Collegando l&#39;app a un progetto Mobile On-Demand, sarete in grado di eseguire la creazione di contenuto, come articoli, banner e raccolte all&#39;interno di AEM, ma anche di servire tale contenuto a Mobile On-Demand.

Da qui diventa possibile pubblicare, visualizzare in anteprima e gestire i contenuti. Potete anche importare contenuto Mobile On-Demand esistente in AEM ed eseguire la modifica dei contenuti.

## Configurazione di Cloud {#setting-up-cloud-configuration}

>[!CAUTION]
>
>Prima di iniziare a configurare la configurazione cloud per l&#39;app on-demand, dovete avere familiarità con il provisioning AEM Mobile e con la configurazione di AEM Mobile On-Demand Services Client.
>
>Per informazioni dettagliate, consultate [Configurazione di AEM Mobile On-Demand Services](/help/mobile/aem-mobile-setup.md) nella sezione Amministrazione.

Per configurare Mobile On-Demand Cloud Services, fate clic sull&#39;ingranaggio superiore nell&#39;angolo superiore destro della sezione **Gestisci connessione** dal dashboard dell&#39;app.

È necessario avere familiarità con il dashboard app e le sezioni disponibili. Per ulteriori dettagli, consultate Pannello [applicazione di](/help/mobile/mobile-apps-ondemand-application-dashboard.md) AEM Mobile.

### Configurazione del collegamento alla configurazione cloud {#setting-up-link-to-cloud-configuration}

>[!CAUTION]
>
>Accertatevi di disporre di un client on-demand e di una configurazione cloud esistenti.
>
>Per informazioni dettagliate, consultate [Configurazione di AEM Mobile On-Demand Services](/help/mobile/aem-mobile-setup.md) nella sezione Amministrazione.

Nei passaggi seguenti viene descritta la configurazione del collegamento alla configurazione cloud:

1. Da **Mobile**, scegliete **App** e quindi l&#39;app Mobile On-Demand dal catalogo.
1. Fate clic sull&#39;icona a forma di ingranaggio nella sezione **Gestisci connessione** .

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. Immettete la configurazione già esistente o createne una nuova immettendo il Titolo **** configurazione, l&#39;ID **** dispositivo e il Token **** dispositivo.

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. Dopo aver verificato l&#39;ID **** dispositivo e il token **** dispositivo, scegliete il progetto on-demand dall&#39;elenco.

   Fate clic su **Invia**.

   ![chlimage_1-67](assets/chlimage_1-67.png)

   La sezione **Gestisci connessione** mostra la configurazione cloud.

   ![chlimage_1-68](assets/chlimage_1-68.png)

   >[!CAUTION]
   >
   >Se provate a modificare il progetto a cui è associata l&#39;app, durante il passaggio al progetto nel dashboard, riceverete un avviso per i problemi di integrità del contenuto come mostrato nella figura seguente:

   ![chlimage_1-69](assets/chlimage_1-69.png)

### Passaggi successivi {#the-next-steps}

Dopo aver configurato la configurazione cloud per l&#39;app, consulta le seguenti risorse per la gestione del contenuto:

* [Gestione degli articoli](/help/mobile/mobile-on-demand-managing-articles.md)
* [Gestione dei banner](/help/mobile/mobile-on-demand-managing-banners.md)
* [Gestione delle raccolte](/help/mobile/mobile-on-demand-managing-collections.md)
* [Caricamento delle risorse condivise](/help/mobile/mobile-on-demand-shared-resources.md)
* [Pubblicazione/annullamento della pubblicazione del contenuto](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [Anteprima con verifica preliminare](/help/mobile/aem-mobile-manage-ondemand-services.md)
