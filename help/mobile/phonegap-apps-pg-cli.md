---
title: Sviluppo di app con PhoneGap CLI
description: Scopri come sviluppare app per dispositivi mobili con PhoneGap CLI utilizzando un ambiente di sviluppo con avvio automatico.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: fbeceb70-b199-478b-907b-253ed212ff99
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 2%

---

# Sviluppo di app con PhoneGap CLI{#developing-apps-with-phonegap-cli}

>[!NOTE]
>
>L’Adobe consiglia di utilizzare l’Editor SPA per i progetti che richiedono il rendering lato client basato su framework di applicazione a pagina singola (ad esempio, React). [Ulteriori informazioni](/help/sites-developing/spa-overview.md).

In qualsiasi momento, come sviluppatore puoi eseguire l’app su un dispositivo o all’interno di un emulatore, purché sia stato configurato l’ambiente di sviluppo.

Per eseguire gli esempi seguenti, è necessario un sistema che esegua macOS X con Xcode oppure un sistema Mac/Win/Linux con l&#39;SDK Android™ installato.

## Bootstrap l’ambiente di sviluppo {#bootstrap-your-development-environment}

Configura CLI PhoneGap (`https://docs.phonegap.com/en/4.0.0/guide_cli_index.md.html#The%20Command-Line%20Interface`)

Per iOS: per sviluppare per iPhone e iPad, è necessario Apple Xcode IDE.

* Scaricala gratuitamente [qui](https://idmsa.apple.com/IDMSWebAuth/signin?appIdKey=891bd3417a7776362562d2197f89480a8547b108fd934911bcbea0110d07f757&amp;path=%2Fdownload%2F&amp;rv=1).
* Guida alla piattaforma PhoneGap iOS (`https://docs.phonegap.com/en/4.0.0/guide_platforms_ios_index.md.html#iOS%20Platform%20Guide`)

Per Android™: per sviluppare per iPhone e iPad, è necessario Google Android™ Studio IDE.

* Scaricala gratuitamente [qui](https://developer.android.com/studio).
* Guida alla piattaforma PhoneGap Android™ (`https://docs.phonegap.com/en/4.0.0/guide_platforms_android_index.md.html#Android%20Platform%20Guide`)

## Scarica l’origine {#download-the-source}

Dopo aver avviato correttamente l’ambiente di sviluppo, scarica l’origine dal riquadro di build dell’app AEM:

* Fai clic sulla freccia a discesa del riquadro PhoneGap Build.

![chlimage_1-45](assets/chlimage_1-45.png)

* Fai clic su Scarica origine.
* Seleziona l’origine desiderata dal modale Scarica origine.

![chlimage_1-46](assets/chlimage_1-46.png)

>[!NOTE]
>
>L’origine di sviluppo contiene lo stato più recente dell’app, comprese le modifiche non di staging. Utilizza l’origine Staging per creare le versioni candidate per l’invio ai fornitori degli app store.
>
>Se non esegui mai l’app in staging, quando selezioni Staging viene attivato il flusso di lavoro di staging (suggerimento: viene visualizzato come app di staging nell’app del visualizzatore Enterprise di PhoneGap disponibile in AppStore e Google PlayStore).

* Fai clic su Scarica e salva il file ZIP sul computer.
* Estrai il file zip scaricato nell’area di lavoro.

## Creare e caricare l’app (dall’origine) {#build-and-load-the-app-from-source}

PhoneGap CLI può creare un progetto di piattaforma, compilare l’origine e distribuire l’app in un unico comando.

>[!NOTE]
>
>Puoi eseguire tutti questi passaggi separatamente, vedi i documenti CLI di PhoneGap (`https://phonegap.com/blog/2014/11/13/phonegap-cli-3-6-3/`).

1. Verifica di aver installato PhoneGap CLI, vedi sopra.
1. In una finestra della console (o del terminale), passa alla directory principale della sorgente estratta.
1. Immetti il comando seguente:

```xml
phonegap run android

// -- or -- //

phonegap run ios
```

>[!NOTE]
>
>In caso di problemi, torna alle nozioni di base per la risoluzione dei problemi -
>
>1. Creare una cartella (test mkdir)
>1. Passa a questa nuova cartella (test cd)
>1. Esegui `phonegap create helloWorld`
>1. Navigare in helloWorld (cd helloWorld)
>1. Esegui `phonegap run android` (o sostituisci Android™ con iOS come sopra).
>1. L’emulatore apre l’esecuzione dell’app PhoneGap appena creata, indicando &quot;Device Ready&quot; (Pronto per il dispositivo) se JavaScript Bridge to native è operativo.
>
>Questa risoluzione dei problemi verifica che l’ambiente di sviluppo CLI di PhoneGap funzioni correttamente.

## Eseguire il debug di JavaScript con il debug di Safari e IOS {#debug-javascripts-with-safari-and-ios-debug}

Puoi eseguire il debug del codice JavaScript dell’app utilizzando gli strumenti per sviluppatori di Safari, allo stesso modo che faresti con un’applicazione web.

## Abilitare gli strumenti per sviluppatori Safari {#enable-safari-developer-tools}

Per abilitare gli strumenti per sviluppatori:

* Apri le preferenze di Safari

   * Fai clic su Safari nella barra dei menu
   * Fai clic su Preferenze

* Fare clic su Avanzate nella finestra Preferenze

![chlimage_1-47](assets/chlimage_1-47.png)

* Seleziona &quot;Mostra menu Sviluppo nella barra dei menu&quot;
* Chiudi la finestra Preferenze

## Connettere Safari ad iOS {#connect-safari-to-ios}

È possibile collegare Safari a un dispositivo o a un emulatore iOS.

* In una finestra della console, passa alla directory principale dell&#39;origine estratta.
* Immetti il seguente comando per avviare l&#39;app sul dispositivo o sull&#39;emulatore.

```xml
phonegap run <platform> --device

// -- or -- //

phonegap run <platform> --emulator
```

* Apri Safari
* Fai clic su Sviluppo nella barra dei menu.
* Seleziona il sottomenu iOS Simulator
* Fare clic su home.html

![chlimage_1-48](assets/chlimage_1-48.png)

## Debug di JavaScript con Safari Web Inspector {#debug-javascript-with-safari-s-web-inspector}

È possibile impostare i punti di interruzione in qualsiasi punto dell&#39;origine. Quando interagisci con l’emulatore o il dispositivo, l’esecuzione dell’app si interrompe in corrispondenza di tali punti di interruzione. Puoi analizzare in dettaglio l’esecuzione e controllare i valori nelle variabili.

* Fare clic su Risorse nella finestra Controllo Web
* Navigare nella struttura di origine e fare clic sul file di origine desiderato
* Fare clic sul numero di riga accanto al punto di interruzione
* Interagire con il dispositivo o l’emulatore

![chlimage_1-49](assets/chlimage_1-49.png)

* Utilizza i pulsanti di controllo per continuare l’esecuzione, eseguire un passaggio, eseguire un passaggio e uscire dai metodi:

![Cinque diversi pulsanti di controllo funzionanti allineati in una riga orizzontale.](do-not-localize/chlimage_1-4.png)

>[!NOTE]
>
>Per visualizzare i valori delle variabili nel metodo corrente, passa il puntatore del mouse.

## Passaggi successivi {#the-next-steps}

Dopo aver appreso come sviluppare app con PhoneGap CLI, consulta [Accesso alle funzioni del dispositivo](/help/mobile/phonegap-access-device-features.md).
