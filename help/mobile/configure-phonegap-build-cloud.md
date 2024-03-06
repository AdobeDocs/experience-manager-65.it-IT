---
title: Configurare il Cloud Service Adobe PhoneGap Build
description: Segui questa pagina per configurare i servizi cloud e creare l’applicazione con PhoneGap Build.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
exl-id: d91a00d1-12fa-4c84-a426-49413f61c126
source-git-commit: 9d497413d0ca72f22712581cf7eda1413eb8d643
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 2%

---

# Configurare il Cloud Service Adobe PhoneGap Build {#configure-your-adobe-phonegap-build-cloud-service}

>[!NOTE]
>
>L’Adobe consiglia di utilizzare l’Editor SPA per i progetti che richiedono il rendering lato client basato su framework di applicazione a pagina singola (ad esempio, React). [Ulteriori informazioni](/help/sites-developing/spa-overview.md).

Il **PhoneGap Build** sul dashboard dell’applicazione consente di generare e distribuire l’app mobile PhoneGap tramite il servizio Adobe PhoneGap Build.

Tutte le piattaforme supportate definite in **Gestisci app** sono costruite con PhoneGap Build quando si preme una build remota con **PhoneGap Build** Sezione.

Puoi inviare una build remota a `https://build.phonegap.com` o scarica l&#39;origine da generare localmente con PhoneGap CLI all&#39;indirizzo `https://docs.phonegap.com/references/phonegap-cli/`.

![PhoneGap Build](assets/chlimage_1-60.png)

## Configurazione del Cloud Service {#configuring-the-cloud-service}

Per sfruttare le PhoneGap Build, è necessario configurare il Cloud Service di PhoneGap Build AEM con le informazioni sul proprio account PhoneGap Build.

Se al momento non disponi di un account, passa a `https://build.phonegap.com` e registrati! Se hai un abbonamento a Adobe Creative Cloud, puoi avere il supporto per un massimo di 25 app private (non open source).

Dopo aver verificato che l’account PhoneGap Build è attivo, accedi alla console di gestione AEM Cloud, in particolare [Cloud Service di PhoneGap Build](http://localhost:4502/etc/cloudservices/phonegap-build.html) (http://localhost:4502/etc/cloudservices/phonegap-build.html)

Utilizza il **Gestisci Cloud Service** riquadro per configurare una nuova configurazione di cloud service.

### Utilizzo del riquadro Gestisci Cloud Service {#using-manage-cloud-services-tile}

Prima di iniziare a creare l’app utilizzando **PhoneGap Build** , è necessario configurare i servizi cloud utilizzando il **Gestisci Cloud Service** riquadro dal dashboard di AEM Mobile.

Per configurare i servizi cloud per l’app, effettua le seguenti operazioni:

1. Fai clic sull’angolo in alto a destra del **Gestisci Cloud Service** affiancare.

   ![chlimage_1-61](assets/chlimage_1-61.png)

1. Scegli **PhoneGap Build** opzione dalla **Aggiungi o modifica Cloud Service** schermo.

   Fai clic su **Avanti**.

   ![chlimage_1-62](assets/chlimage_1-62.png)

1. Immetti le credenziali per creare una configurazione cloud.

   Una volta verificata, fai clic su **Invia**. Questa configurazione cloud configurata ora viene visualizzata in **Gestisci Cloud Service** affiancare.

   ![chlimage_1-63](assets/chlimage_1-63.png)

### Creazione dell&#39;applicazione con la PhoneGap Build {#building-your-application-with-phonegap-build}

Dopo aver configurato i servizi cloud, puoi creare l’applicazione con **PhoneGap Build** affiancare. Fai clic sull’angolo in alto a destra per scegliere tra **Genera in remoto** o **Scarica origine** opzioni.

![chlimage_1-64](assets/chlimage_1-64.png)

Per richiamare una build remota con Adobe PhoneGap Build, fai clic su **Genera in remoto**.

>[!NOTE]
>
>Se la build non riesce per qualsiasi motivo (l’icona rossa di iOS riportata di seguito indica che la piattaforma non è riuscita), puoi passare il puntatore sull’icona per visualizzare il messaggio di errore. In alternativa, puoi fare clic sul triplo punto, &quot;...&quot; nella parte inferiore del riquadro per passare direttamente a `https://build.phonegap.com` (devi eseguire l’autenticazione) e guardare e gestire direttamente la build.

### Creazione dell&#39;applicazione con PhoneGap CLI {#building-your-application-with-phonegap-cli}

PhoneGap fornisce un’interfaccia a riga di comando per generare l’applicazione localmente.

Compilare l&#39;applicazione PhoneGap sul computer utilizzando l&#39;interfaccia CLI (Command-Line Interface) di PhoneGap. Per includere il contenuto dell’AEM nell’applicazione, AEM crea un file ZIP contenente il contenuto dell’app mobile, le configurazioni di sincronizzazione dei contenuti e altre risorse richieste. Scarica il file ZIP e includilo nella build.

Per sfruttare l&#39;interfaccia CLI di PhoneGap, è necessario configurare l&#39;ambiente locale in modo che includa:

1. Platform SDK (iOS, Android™, WindowsPhone, ...) e
1. CLI di PhoneGap

Per ulteriori informazioni, consulta `https://docs.phonegap.com/references/phonegap-cli/`.

Una volta installati i prerequisiti, sottoponilo a un semplice test creando una semplice app e attivandola nel simulatore o in modo migliore sul dispositivo, da un terminale, prova:

```xml
phonegap create myApp
cd myApp
phonegap run ios (or android, ...)
```

>[!NOTE]
>
>Aggiungi —emula alla fine di questa riga se non desideri eseguirla sul dispositivo connesso.

Dopo aver verificato il funzionamento di quanto sopra, utilizza **PhoneGap Build** Affianca in **Scarica origine**. Salva e decomprimi il file sul sistema locale. Una volta fatto:

* passa al file salvato (cartella)
* eseguire phonegap run ios (o android, e così via)

### Risorse aggiuntive {#additional-resources}

Per informazioni sui ruoli e sulle responsabilità di un autore e di uno sviluppatore, consulta le risorse seguenti:

* [Sviluppo per Adobe PhoneGap Enterprise con AEM](/help/mobile/developing-in-phonegap.md)
* [Authoring per Adobe PhoneGap Enterprise nell’AEM](/help/mobile/phonegap.md)
