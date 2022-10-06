---
title: Sviluppo di app con PhoneGap CLI
seo-title: Developing Apps with PhoneGap CLI
description: Segui questa pagina per informazioni sullo sviluppo di app con PhoneGap CLI.
seo-description: Follow this page to learn about developing apps with PhoneGap CLI.
uuid: 9a66171d-19af-40db-9c07-f5dd9561e1b5
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 4a034e15-3394-4be3-9e8e-bc894668946a
exl-id: fbeceb70-b199-478b-907b-253ed212ff99
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 1%

---

# Sviluppo di app con PhoneGap CLI{#developing-apps-with-phonegap-cli}

>[!NOTE]
>
>Adobe consiglia di utilizzare l’editor di SPA per i progetti che richiedono il rendering lato client basato sul framework di un’applicazione a pagina singola (ad esempio, React). [Per saperne di più](/help/sites-developing/spa-overview.md).

In qualsiasi momento, in qualità di sviluppatore, puoi eseguire l’app su un dispositivo o all’interno di un emulatore, purché sia stato configurato l’ambiente di sviluppo.

Per eseguire i seguenti esempi è necessario un sistema che esegue OSx (Mac) con Xcode o un sistema Mac/Win/Linux con l&#39;SDK Android installato.

## Bootstrap dell&#39;ambiente di sviluppo {#bootstrap-your-development-environment}

[Configurazione di PhoneGap CLI](https://docs.phonegap.com/en/4.0.0/guide_cli_index.md.html#The%20Command-Line%20Interface)

Per iOS: Per sviluppare per iPhone e iPad, è necessario Apple Xcode IDE.

* Scarica gratuitamente [qui](https://developer.apple.com/xcode/downloads/).
* [Guida alla piattaforma iOS PhoneGap](https://docs.phonegap.com/en/4.0.0/guide_platforms_ios_index.md.html#iOS%20Platform%20Guide)

Per Android: Per sviluppare per iPhone e iPad, è necessario Google Android Stuido IDE.

* Scarica gratuitamente [qui](https://developer.android.com/sdk/index.html).
* [Guida alla piattaforma Android PhoneGap](https://docs.phonegap.com/en/4.0.0/guide_platforms_android_index.md.html#Android%20Platform%20Guide)

## Scarica la sorgente {#download-the-source}

Una volta avviato correttamente l’ambiente di sviluppo, scarica l’origine dal riquadro Build app AEM:

* Fai clic sulla freccia a discesa del riquadro PhoneGap Build.

![chlimage_1-45](assets/chlimage_1-45.png)

* Fai clic su Scarica origine .
* Seleziona l’origine desiderata dal modale Scarica origine .

![chlimage_1-46](assets/chlimage_1-46.png)

>[!NOTE]
>
>L&#39;origine di sviluppo contiene lo stato più recente dell&#39;app, incluse le modifiche non in staging. Utilizza l’origine Gestione temporanea per creare i candidati alle versioni da inviare ai fornitori dell’app store.
>
>Se l’app non viene mai messa in scena, la selezione dell’opzione Staging attiva il flusso di lavoro di staging (suggerimento: questo verrà visualizzato come app per staging nell’app visualizzatore PhoneGap Enterprise disponibile in AppStore e Google PlayStore).

* Fai clic su Scarica e salva il file ZIP nel computer.
* Estrai il file zip scaricato nella tua area di lavoro.

## Creare e caricare l’app (dall’origine) {#build-and-load-the-app-from-source}

PhoneGap CLI può creare un progetto di piattaforma, compilare la sorgente e distribuire l’app in un unico comando.

>[!NOTE]
>
>Puoi eseguire tutti questi passaggi separatamente, vedi [Documenti CLI di PhoneGap](https://phonegap.com/blog/2014/11/13/phonegap-cli-3-6-3/).

1. Assicurati di aver installato PhoneGap CLI, vedi sopra.
1. In una finestra della console (o terminale), accedi alla directory principale della sorgente estratta.
1. Immetti il seguente comando:

```xml
phonegap run android

// -- or -- //

phonegap run ios
```

>[!NOTE]
>
>In caso di problemi a questo punto, torna alle basi per i problemi -
>
>1. Crea una nuova cartella (test mkdir)
>1. Passa a questa nuova cartella (cd test)
>1. Esegui &#39;phonegap create helloWorld&#39;
>1. Passa a helloWorld (cd helloWorld)
>1. Esegui &#39;phonegap run android (o sostituisci android con ios come sopra).
>1. L&#39;emulatore si aprirà eseguendo l&#39;app PhoneGap appena creata, dicendo &quot;Dispositivo pronto&quot; se il ponte JavaScript a nativo è operativo.

>
>Questo verifica che l’ambiente di sviluppo PhoneGap CLI sia attivo e funzioni correttamente.

## Debug di JavaScript con il debug di Safari e IOS {#debug-javascripts-with-safari-and-ios-debug}

Puoi eseguire il debug degli JavaScript dell’app utilizzando gli strumenti per sviluppatori di Safari, come faresti con un’applicazione web.

## Abilita gli strumenti per sviluppatori di Safari {#enable-safari-developer-tools}

Per abilitare gli strumenti per sviluppatori:

* Apri le preferenze di Safari

   * Fai clic su Safari nella barra dei menu
   * Fai clic su Preferenze

* Fai clic su Avanzate nella finestra Preferenze

![chlimage_1-47](assets/chlimage_1-47.png)

* Selezionare &quot;Mostra menu di sviluppo nella barra dei menu&quot;
* Chiudi la finestra Preferenze

## Collegare Safari ad iOS {#connect-safari-to-ios}

Puoi collegare Safari a un dispositivo o a un emulatore iOS.

* In una finestra della console, accedi alla directory principale della sorgente estratta.
* Immetti il seguente comando per avviare l&#39;app sul tuo dispositivo o emulatore.

```xml
phonegap run <platform> --device

// -- or -- //

phonegap run <platform> --emulator
```

* Apri Safari
* Fai clic su Sviluppa nella barra dei menu
* Seleziona il sottomenu Simulatore di iOS
* Fai clic su home.html

![chlimage_1-48](assets/chlimage_1-48.png)

## Eseguire il debug di JavaScript con l’ispettore Web di Safari {#debug-javascript-with-safari-s-web-inspector}

Puoi impostare punti di interruzione in qualsiasi punto della sorgente. Quando interagisci con l’emulatore o il dispositivo, l’esecuzione dell’app si arresta a quei punti di interruzione. Puoi eseguire un’analisi approfondita dell’esecuzione e controllare i valori nelle variabili.

* Fare clic su Risorse nella finestra Ispettore Web
* Passa alla struttura ad albero di origine e fai clic sul file di origine desiderato
* Fai clic sul numero di riga adiacente per aggiungere un punto di interruzione
* Interagire con il dispositivo o l&#39;emulatore

![chlimage_1-49](assets/chlimage_1-49.png)

* Utilizza i pulsanti di controllo per continuare l’esecuzione, passa il cursore, entra ed esce dai metodi:

![](do-not-localize/chlimage_1-4.png)

>[!NOTE]
>
>Per visualizzare i valori delle variabili, passa il mouse nel metodo corrente.

## Passaggi successivi {#the-next-steps}

Dopo aver appreso come sviluppare app con PhoneGap CLI, consulta [Accesso alle funzioni del dispositivo](/help/mobile/phonegap-access-device-features.md).
