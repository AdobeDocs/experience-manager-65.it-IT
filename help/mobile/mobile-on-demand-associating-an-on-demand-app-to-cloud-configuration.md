---
title: Configurazione cloud
seo-title: Cloud Configuration
description: L’associazione di un’app on-demand a una configurazione cloud consente ad Adobe Experience Manager (AEM) di comunicare direttamente con un progetto ospitato da Mobile On-Demand creando un collegamento in due modi. Segui questa pagina per ulteriori informazioni.
seo-description: Associating an On-Demand App to a Cloud Configuration allows Adobe Experience Manager (AEM) to communicate directly with a Mobile On-Demand hosted project by establishing a two way link. Follow this page to learn more.
uuid: f377f2af-864b-43df-9d42-4a5fd6cd70d5
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: d0d29b99-53d4-4b0d-947b-39d91b381de7
exl-id: 37428543-c310-4712-a4ec-1f482579fb4b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 3%

---

# Configurazione cloud{#cloud-configuration}

>[!NOTE]
>
>Adobe consiglia di utilizzare l’editor di SPA per i progetti che richiedono il rendering lato client basato sul framework di un’applicazione a pagina singola (ad esempio, React). [Per saperne di più](/help/sites-developing/spa-overview.md).

L’associazione di un’app on-demand a una configurazione cloud consente ad Adobe Experience Manager (AEM) di comunicare direttamente con un progetto ospitato da Mobile On-Demand creando un collegamento in due modi. Collegando l’app a un progetto Mobile On-Demand, potrai eseguire la creazione di contenuti, come articoli, banner e raccolte all’interno di AEM, ma anche servire tali contenuti a Mobile On-Demand.

Da lì è possibile pubblicare, visualizzare in anteprima e gestire i contenuti. È inoltre possibile importare i contenuti Mobile On-Demand esistenti in AEM ed eseguire la modifica dei contenuti.

## Configurazione di Cloud Configuration {#setting-up-cloud-configuration}

>[!CAUTION]
>
>Prima di iniziare a configurare la configurazione cloud per l’app on-demand, devi avere già familiarità con il provisioning AEM Mobile e la configurazione del client AEM Mobile On-demand Services.
>
>Per ulteriori informazioni, consulta [Configurazione di AEM Mobile On-demand Services](/help/mobile/aem-mobile-setup.md) nella sezione Amministrazione .

Per configurare i Cloud Services Mobile On-Demand, fai clic sull’ingranaggio superiore nell’angolo in alto a destra del **Gestisci connessione** dal dashboard dell&#39;app.

Acquisisci familiarità con il dashboard dell’app e i riquadri disponibili. Vedi [Dashboard dell&#39;applicazione AEM Mobile](/help/mobile/mobile-apps-ondemand-application-dashboard.md) per ulteriori dettagli.

### Configurazione del collegamento alla configurazione cloud {#setting-up-link-to-cloud-configuration}

>[!CAUTION]
>
>Verifica di disporre di una configurazione client on-demand e cloud esistente.
>
>Per ulteriori informazioni, consulta [Configurazione di AEM Mobile On-demand Services](/help/mobile/aem-mobile-setup.md) nella sezione Amministrazione .

I passaggi seguenti descrivono la configurazione del collegamento alla configurazione cloud:

1. Da **Mobile**, scegli **App** e quindi la tua app Mobile On-Demand dal catalogo.
1. Fai clic sull’icona a forma di ingranaggio nella **Gestisci connessione** piastrelle.

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. Immetti la configurazione già esistente o creane una nuova immettendo la **Titolo della configurazione**, **ID dispositivo** e **Token del dispositivo**.

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. Una volta che **ID dispositivo** e **Token del dispositivo** vengono verificati, scegli il progetto on-demand dall’elenco.

   Fai clic su **Invia**.

   ![chlimage_1-67](assets/chlimage_1-67.png)

   La **Gestisci connessione** mostra la configurazione cloud.

   ![chlimage_1-68](assets/chlimage_1-68.png)

   >[!CAUTION]
   >
   >Se tenti di modificare il progetto a cui è associata questa app, cambiando progetto nel dashboard, riceverai un avviso per i problemi di integrità del contenuto, come illustrato nella figura seguente:

   ![chlimage_1-69](assets/chlimage_1-69.png)

### Passaggi successivi {#the-next-steps}

Dopo aver configurato la configurazione cloud per l’app, consulta le seguenti risorse per la gestione del contenuto:

* [Gestione degli articoli](/help/mobile/mobile-on-demand-managing-articles.md)
* [Gestione dei banner](/help/mobile/mobile-on-demand-managing-banners.md)
* [Gestione delle raccolte](/help/mobile/mobile-on-demand-managing-collections.md)
* [Caricamento delle risorse condivise](/help/mobile/mobile-on-demand-shared-resources.md)
* [Pubblicazione/annullamento della pubblicazione del contenuto](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [Anteprima con Preflight](/help/mobile/aem-mobile-manage-ondemand-services.md)
