---
title: Configurare il servizio Adobe Mobile Services Cloud
seo-title: Configurare il servizio Adobe Mobile Services Cloud
description: Segui questa pagina per configurare il servizio Adobe Mobile Services Cloud Service.
seo-description: Segui questa pagina per configurare il servizio Adobe Mobile Services Cloud Service.
uuid: 21fe5b24-dc4d-4ee4-9e7f-ed4783baf276
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 962e9e98-a303-435b-a938-31319282e022
legacypath: /content/docs/en/aem/6-1/develop/mobile-apps/apps/managing-aem-mobile-apps/configure-your-adobe-phonegap-build-cloud-service1
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configurare il servizio Adobe Mobile Services Cloud {#configure-your-adobe-mobile-services-cloud-service}

>[!NOTE]
>
>Adobe consiglia di utilizzare SPA Editor per i progetti che richiedono il rendering lato client basato sul framework dell&#39;applicazione a pagina singola (ad es. React). [Per saperne di più](/help/sites-developing/spa-overview.md).

La sezione Metriche **mobili** del centro comandi fornisce analisi in tempo reale per l’applicazione mobile.

L’SDK di [Adobe Mobile Analytics](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) è disponibile tramite un plug-in PhoneGap. Le metriche vengono raccolte e memorizzate nella cache del dispositivo fino a quando il dispositivo non è connesso. In tal caso, i dati vengono inviati ad Adobe Mobile Services Cloud per attività di reporting e analisi.

L’SDK di Adobe Mobile Analytics fornisce le seguenti informazioni:

1. **Raccolta di dati per i canali** mobili: raccolta di dati completi per i siti Web e le app mobili su tutti i principali sistemi operativi.
1. **Analisi** del coinvolgimento dei dispositivi mobili - Comprendi il coinvolgimento degli utenti all’interno dell’app mobile, del sito Web o del video, inclusa la frequenza con cui i consumatori avviano il canale, sia che effettuino acquisti da esso, e molto altro.
1. **Dashboard e rapporti** delle app per dispositivi mobili: ottieni rapporti sull&#39;utilizzo che includono metriche del ciclo di vita per le tue app e metriche dell&#39;app store; visualizza le tendenze per utenti, avvii, lunghezza di sessione media, durata di conservazione e arresti anomali.
1. **Analisi** delle campagne per dispositivi mobili - Consente di quantificare l&#39;efficacia delle campagne per dispositivi mobili, come SMS, annunci di ricerca per dispositivi mobili, annunci display per dispositivi mobili e codici QR.
1. **Analisi** della geolocalizzazione - Scopri dove gli utenti dell&#39;app avviano e interagiscono con le tue esperienze mobili in base alla posizione GPS o ai punti di interesse.
1. **Analisi** dei percorsi - Scopri in che modo gli utenti si spostano all&#39;interno dell&#39;app per determinare quali schermate ed elementi dell&#39;interfaccia utente coinvolgono gli utenti e quali causano il loro rilascio.

>[!CAUTION]
>
>La sezione Metriche **di** analisi viene visualizzata nel dashboard solo se avete configurato i servizi cloud.

![chlimage_1-22](assets/chlimage_1-22.png)

Sezione Metriche del centro di comando AEM

## Configurazione del servizio Cloud {#configuring-the-cloud-service}

Per sfruttare Adobe Mobile Services Analytics, devi configurare il servizio AEM Mobile Analytics Cloud Service con le informazioni dell&#39;account Adobe Analytics.

1. Fai clic sull&#39;icona in alto a destra per aggiungere o modificare i Servizi cloud dalla sezione **Gestisci servizi** cloud dal dashboard dell&#39;app.

   ![chlimage_1-23](assets/chlimage_1-23.png)

1. Viene visualizzata la schermata **Aggiungi o Modifica servizi** cloud. Seleziona **Adobe Mobile Services** e fai clic su **Avanti**.

   ![chlimage_1-24](assets/chlimage_1-24.png)

1. Scegli una configurazione esistente da **Mobile Services** o scegli **Crea configurazione** per crearne una nuova.

   Per una nuova configurazione, immetti le proprietà di **Mobile Services** e fai clic su **Verifica.**

   ![chlimage_1-25](assets/chlimage_1-25.png)

   Se le credenziali vengono verificate, il pulsante **Verifica** diventa **Verificato**. Puoi scegliere un&#39;app di servizi mobili da **Seleziona un servizio** app mobile.

   Fate clic su **Invia** per configurare la configurazione.

   ![chlimage_1-26](assets/chlimage_1-26.png)

1. Una volta impostata la configurazione cloud, potete visualizzare la stessa visualizzazione nel dashboard.

   ![chlimage_1-27](assets/chlimage_1-27.png)

   >[!NOTE]
   >
   >Una volta impostata la configurazione cloud, puoi visualizzare la sezione **Analisi metriche** nel dashboard dell&#39;app.

   ![chlimage_1-28](assets/chlimage_1-28.png)

