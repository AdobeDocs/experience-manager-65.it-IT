---
title: Messaggi di errore sulle API obsolete nei registri di errore
description: Messaggi di errore sulle API obsolete nei registri di errore
source-git-commit: b05666883645ca11784292e4bfb5bf9c1e35a43b
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 3%

---


# Messaggi di errore sulle API obsolete nei registri di errore {#error-messages-about-deprecated-apis-in-error-logs}

Il problema si applica alle seguenti versioni:

* Experience Manager 6.5 Forms

## Problema   {#issue}

* Nel file error.log vengono visualizzati i seguenti messaggi di errore:
  ` *WARN* [default task-36] org.apache.jackrabbit.oak.spi.security.principal.AclGroupDeprecation use of deprecated java.acl.Group-related API - this method is going to be removed in future Oak releases - see OAK-7358 for details` (NPR-38282)

## Risoluzione {#workaround}

1. Installa [Experience Manager Forms Service Pack 13 o successivo (6.5.13.0 o successivo)](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=it)
1. Utilizza il seguente collegamento per scaricare il pacchetto (file .jar con risoluzione) da Software Distribution:

   https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[...]pack/com.adobe.livecycle.dsc.externalloinmodule-4.0.8.jar

1. Apri Experience Manager Configuration Manager e installa il file com.adobe.livecycle.dsc.externalloinmodule-4.0.8.jar scaricato.

Il problema è stato risolto.