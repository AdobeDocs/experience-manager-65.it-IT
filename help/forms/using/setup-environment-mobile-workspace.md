---
title: Configurare l’ambiente per l’app AEM Forms
description: Hardware, software e licenze per creare e distribuire l'app AEM Forms.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: 1d1f9db2-83cf-4612-ac8c-d2638c3bbaea
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 5%
---
# Configurare l’ambiente per l’app AEM Forms{#set-up-environment-for-aem-forms-app}

>[!NOTE]
>
>L’app AEM Forms è attualmente obsoleta. Per domande o assistenza, contattare [aemformsapp-android@adobe.com](mailto:aemformsapp-android@adobe.com).

Per creare e distribuire l&#39;app AEM Forms sono necessari i seguenti componenti hardware, software e licenze:

## Per dispositivi Windows {#for-windows-devices}

* Microsoft® Windows 10
* Microsoft® Visual Studio 2015
* Strumenti Microsoft® Visual Studio per Apache Cordova

## Per dispositivi iOS {#for-ios-devices}

* Apple Mac basato su Intel con macOS X 10.9.5 o versione successiva
* iOS SDK 8.4 o versione successiva
* Versione Xcode: Xcode 6.4 per OS X o versione successiva
* Iscrizione al programma iOS Developer Enterprise
* Certificato Enterprise per la distribuzione interna di app iOS
* Apple iPad con iOS 8.4 o versione successiva

## Per dispositivi Android™ {#for-android-devices}

* Android™ Development Toolkit (bundle ADT) scaricabile da [https://developer.android.com/studio](https://developer.android.com/studio)
* Se l’ambiente è configurato su un sistema Mac, l’ADT deve essere installato nella cartella Applicazioni.
* Se ADT è installato in un&#39;altra posizione in Mac o se l&#39;ambiente è configurato in un sistema Windows, il percorso di ADT SDK deve essere aggiornato nel file `local.properties`. Il file è disponibile nella cartella `src\android` dell&#39;archivio di origine `mobileworkspace-src.zip` estratto. In questo file, puntare la variabile `sdk.dir` alla posizione ADT SDK sul desktop.

>[!NOTE]
>
>Il file adobe-lc-mobileworkspace-src.zip contiene PhoneGap SDK 5.0. Verifica che PhoneGap SDK non sia preinstallato.
