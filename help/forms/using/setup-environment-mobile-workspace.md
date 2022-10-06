---
title: Configurare l’ambiente per l’app AEM Forms
seo-title: Set up environment for AEM Forms app
description: Hardware, software e licenze per la creazione e l’implementazione dell’app AEM Forms.
seo-description: Hardware, software, and licenses to build and deploy the AEM Forms app.
uuid: 4123a6b7-5766-476c-9afb-f57029b148ad
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: e6b01ade-7ea3-42a7-872d-cc35a3d2782a
docset: aem65
exl-id: 1d1f9db2-83cf-4612-ac8c-d2638c3bbaea
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---

# Configurare l’ambiente per l’app AEM Forms{#set-up-environment-for-aem-forms-app}

Per creare e distribuire l’app AEM Forms sono necessari i seguenti hardware, software e licenze:

## Per dispositivi Windows {#for-windows-devices}

* Microsoft Windows 10
* Microsoft Visual Studio 2015
* Strumenti di Microsoft Visual Studio per Apache Cordova

## Per dispositivi iOS {#for-ios-devices}

* Apple Mac basato su Intel con Mac OS X 10.9.5 o superiore
* SDK iOS 8.4 o successivo
* Versione Xcode: Xcode 6.4 per OS X o versioni successive
* Iscrizione al programma iOS Developer Enterprise
* Certificato Enterprise per la distribuzione di app iOS interne
* Apple iPad con iOS 8.4 o versione successiva

## Per dispositivi Android {#for-android-devices}

* Android Development Toolkit (bundle ADT) che può essere scaricato da [https://developer.android.com/sdk/index.html](https://developer.android.com/sdk/index.html)
* Se l&#39;ambiente è configurato in un sistema MAC, l&#39;ADT deve essere installato nella cartella Applicazioni.
* Se ADT è installato in un altro percorso in MAC o se l&#39;ambiente è configurato in un sistema Windows, è necessario aggiornare il percorso SDK ADT in `local.properties` file disponibile in `src\android` cartella nell&#39;archivio sorgente estratto `mobileworkspace-src.zip`. In questo file, seleziona `sdk.dir` alla posizione ADT SDK sul desktop.

>[!NOTE]
>
>adobe-lc-mobileworkspace-src.zip contiene PhoneGap SDK 5.0. Assicurati che PhoneGap SDK non sia preinstallato.
