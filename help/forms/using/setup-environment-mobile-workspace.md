---
title: Configurare l'ambiente per 'app AEM Forms
seo-title: Configurare l'ambiente per 'app AEM Forms
description: Hardware, software e licenze per creare e distribuire l'app AEM Forms .
seo-description: Hardware, software e licenze per creare e distribuire l'app AEM Forms .
uuid: 4123a6b7-5766-476c-9afb-f57029b148ad
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: e6b01ade-7ea3-42a7-872d-cc35a3d2782a
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---


# Configurare l&#39;ambiente per &#39;app AEM Forms{#set-up-environment-for-aem-forms-app}

Per creare e distribuire l&#39;app AEM Forms  sono necessari hardware, software e licenze seguenti:

## Per dispositivi Windows {#for-windows-devices}

* Microsoft Windows 10
* Microsoft Visual Studio 2015
* Microsoft Visual Studio Tools per Apache Cordova

## Per dispositivi iOS {#for-ios-devices}

* Apple Mac basato su Intel con Mac OS X 10.9.5 o versione successiva
* iOS SDK 8.4 o successivo
* Versione Xcode: Xcode 6.4 per OS X o versione successiva
* Iscrizione al programma iOS Developer Enterprise
* Certificato Enterprise per la distribuzione di app iOS interne
* Apple iPad con iOS 8.4 o versione successiva

## Per dispositivi Android {#for-android-devices}

* Android Development Toolkit (bundle ADT) scaricabile da [https://developer.android.com/sdk/index.html](https://developer.android.com/sdk/index.html)
* Se l&#39;ambiente è impostato su un sistema MAC, ADT deve essere installato nella cartella Applicazioni.
* Se ADT è installato in un altro percorso in MAC o se l&#39;ambiente è configurato in un sistema Windows, il percorso ADT SDK deve essere aggiornato in `local.properties` file disponibile nella cartella `src\android` nell&#39;archivio di origine estratto `mobileworkspace-src.zip`. In questo file, indicate la variabile `sdk.dir` per il percorso ADT SDK sul desktop.

>[!NOTE]
>
>adobe-lc-mobileworkspace-src.zip contiene PhoneGap SDK 5.0. Accertatevi che PhoneGap SDK non sia preinstallato.
