---
title: Attivazione della protezione hotlinking in Dynamic Media
description: Informazioni su come attivare la protezione hotlink in Dynamic Media.
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
role: User, Admin
exl-id: 698e8bdb-9b31-49ab-8560-26b05109bb23
feature: Configuration
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: da0dfbce-df02-4f8b-b32d-a4e3b1d05085
    internal-label: Configuration
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 3%
---
# Attivare la protezione hotlinking in Dynamic Media {#activating-hotlink-protection-in-dynamic-media}

Il collegamento rapido si verifica quando un sito web di terze parti utilizza il codice HTML per visualizzare un’immagine dal sito web. Utilizzano la larghezza di banda ogni volta che l&#39;immagine viene richiesta, perché il browser del visitatore vi accede direttamente dal server. Hotlink *protezione* è un metodo per impedire ad altri siti Web di collegarsi direttamente a immagini, CSS o JavaScript nelle pagine Web. Questo tipo di schermatura consente di ridurre l’utilizzo di larghezza di banda non necessaria nell’account Dynamic Media.

[L&#39;Assistenza clienti Experience Manager](https://experienceleague.adobe.com/?support-solution=Experience+Manager&lang=it#support) può configurare un filtro referente a livello CDN (Content Delivery Network) in modo che il contenuto di Dynamic Media venga distribuito solo ai siti Web inclusi nell&#39;elenco dei siti Web consentiti per il dominio.

>[!NOTE]
>
>Questa funzione richiede l’utilizzo della rete CDN preconfigurata inclusa in Adobe Experience Manager Dynamic Media. Qualsiasi altra rete CDN personalizzata non è supportata con questa funzione. Per attivare la protezione hotlink, un amministratore deve creare un ticket all’Assistenza clienti di Adobe per richiedere la modifica della configurazione dell’account Dynamic Media. L&#39;attivazione della protezione hotlink non comporta costi aggiuntivi.
