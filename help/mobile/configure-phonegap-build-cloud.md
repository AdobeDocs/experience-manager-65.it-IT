---
title: Configurare il Cloud Service Adobe PhoneGap Build
seo-title: Configure your Adobe PhoneGap Build Cloud Service
description: Segui questa pagina per configurare i servizi cloud e creare la tua applicazione con la build PhoneGap.
seo-description: Follow this page for configuring the cloud services and building your application with PhoneGap build.
uuid: 59aa99c3-1425-4cc5-9839-a57a6a545d45
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 3c84f4ec-d89b-4ad4-802e-ee3e2d49d916
exl-id: d91a00d1-12fa-4c84-a426-49413f61c126
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 1%

---

# Configurare il Cloud Service Adobe PhoneGap Build {#configure-your-adobe-phonegap-build-cloud-service}

>[!NOTE]
>
>Adobe consiglia di utilizzare l’editor di SPA per i progetti che richiedono il rendering lato client basato sul framework di un’applicazione a pagina singola (ad esempio, React). [Per saperne di più](/help/sites-developing/spa-overview.md).

La **PhoneGap Build** nel dashboard dell&#39;applicazione è possibile creare e distribuire l&#39;applicazione mobile PhoneGap tramite il servizio Adobe PhoneGap Build.

Tutte le piattaforme supportate definite all&#39;interno di **Gestione app** sarà costruito con PhoneGap Build quando si preme una build remota con **PhoneGap Build** Affianca.

Puoi inviare una build remota a [https://build.phonegap.com](https://build.phonegap.com) o scarica l&#39;origine con cui generare localmente [CLI di PhoneGap](https://docs.phonegap.com/references/phonegap-cli/).

![PhoneGap Build](assets/chlimage_1-60.png)

## Configurazione del Cloud Service {#configuring-the-cloud-service}

Per sfruttare le PhoneGap Build è necessario configurare il Cloud Service di PhoneGap Build AEM con le informazioni del tuo account PhoneGap Build.

Se al momento non disponi di un account, accedi a [https://build.phonegap.com](https://build.phonegap.com) e iscriviti! Se si dispone di un&#39;iscrizione a Adobe Creative Cloud, è possibile che si disponga del supporto per un massimo di 25 app private (app non open source).

Dopo aver verificato che l’account di PhoneGap Build è attivo, accedi alla console di gestione AEM Cloud, in particolare alla sezione [Cloud Service PhoneGap Build](http://localhost:4502/etc/cloudservices/phonegap-build.html) (http://localhost:4502/etc/cloudservices/phonegap-build.html).

Utilizza la **Gestire i Cloud Services** per configurare una nuova configurazione del servizio cloud.

### Utilizzo del riquadro Gestisci Cloud Services {#using-manage-cloud-services-tile}

Prima di iniziare a creare l&#39;app utilizzando **PhoneGap Build** riquadro, devi configurare i servizi cloud utilizzando **Gestire i Cloud Services** dalla dashboard di AEM Mobile.

Per configurare i servizi cloud per la tua app, segui i passaggi seguenti:

1. Fai clic sull’angolo in alto a destra del **Gestire i Cloud Services** piastrelle.

   ![chlimage_1-61](assets/chlimage_1-61.png)

1. Scegli **PhoneGap Build** dall&#39;opzione **Aggiungi o modifica Cloud Service** schermo.

   Fai clic su **Avanti**.

   ![chlimage_1-62](assets/chlimage_1-62.png)

1. Immetti le tue credenziali per creare una nuova configurazione cloud.

   Una volta verificato, fai clic su **Invia**. Questa configurazione cloud configurata viene ora visualizzata nella sezione **Gestire i Cloud Services** piastrelle.

   ![chlimage_1-63](assets/chlimage_1-63.png)

### Creazione dell&#39;applicazione con PhoneGap Build {#building-your-application-with-phonegap-build}

Dopo aver configurato i servizi cloud, puoi creare l’applicazione con **PhoneGap Build** piastrelle. Fai clic sull’angolo in alto a destra per scegliere tra **Crea remoto** o **Scarica origine** opzioni.

![chlimage_1-64](assets/chlimage_1-64.png)

Per richiamare una build remota con Adobe PhoneGap Build, fai clic su **Crea remoto**.

>[!NOTE]
>
>Se la build non riesce per qualsiasi motivo (l’icona iOS rossa qui sotto indica che la piattaforma non è riuscita), puoi passare il puntatore sull’icona per visualizzare il messaggio di errore. In alternativa, è possibile fare clic sul triplo punto, &quot;...&quot; nella parte inferiore della tessera per navigare direttamente su https://build.phonegap.com (devi eseguire l’autenticazione) e guardare e gestire direttamente la build.

### Creazione dell’applicazione con PhoneGap CLI {#building-your-application-with-phonegap-cli}

PhoneGap fornisce un&#39;interfaccia a riga di comando per creare l&#39;applicazione localmente.

Compilare l’applicazione PhoneGap sul computer utilizzando l’interfaccia CLI (PhoneGap Command Line Interface). Per includere il contenuto AEM nell’applicazione, AEM crea un file ZIP contenente il contenuto dell’app mobile, le configurazioni di sincronizzazione dei contenuti e altre risorse richieste. Scarica il file ZIP e includilo nella build.

Per sfruttare l’interfaccia a riga di comando di PhoneGap, è necessario configurare l’ambiente locale in modo da includere:

1. Platform SDK (iOS, Android, WindowsPhone, ...) e,
1. CLI di PhoneGap

Per saperne di più [qui](https://docs.phonegap.com/references/phonegap-cli/).

Dopo aver installato i prerequisiti, sottoponilo a un semplice test creando un&#39;app semplice e facendolo funzionare nel tuo simulatore o meglio ancora sul tuo dispositivo, da un terminale prova:

```xml
phonegap create myApp
cd myApp
phonegap run ios (or android, ...)
```

>[!NOTE]
>
>add —emulate alla fine di questa riga se non si desidera eseguirla sul dispositivo collegato.

Dopo aver verificato che quanto sopra funziona, utilizza il **PhoneGap Build** Affianca a **Scarica origine**. Salva e decomprimi il file nel sistema locale. Una volta fatto questo:

* passare al file salvato (cartella)
* esegui &#39;phonegap run ios&#39; (o android, ecc.)

### Risorse aggiuntive {#additional-resources}

Per scoprire i ruoli e le responsabilità di un autore e uno sviluppatore, consulta le risorse seguenti:

* [Sviluppo per Adobe PhoneGap Enterprise con AEM](/help/mobile/developing-in-phonegap.md)
* [Authoring per Adobe PhoneGap Enterprise in AEM](/help/mobile/phonegap.md)
