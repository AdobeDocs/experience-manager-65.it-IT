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
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# Configurare l’ambiente per l’app AEM Forms{#set-up-environment-for-aem-forms-app}

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
* Se l&#39;ADT è installato in un&#39;altra posizione in Mac o se l&#39;ambiente è configurato in un sistema Windows, il percorso dell&#39;SDK ADT deve essere aggiornato nel file `local.properties`. Il file è disponibile nella cartella `src\android` dell&#39;archivio di origine `mobileworkspace-src.zip` estratto. In questo file, puntare la variabile `sdk.dir` alla posizione SDK ADT sul desktop.

>[!NOTE]
>
>Adobe-lc-mobileworkspace-src.zip contiene l&#39;SDK PhoneGap 5.0. Assicurati che PhoneGap SDK non sia preinstallato.
