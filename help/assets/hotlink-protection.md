---
title: Attivazione della protezione hot link in Dynamic Media
description: Informazioni su come attivare la protezione hot link in Dynamic Media.
uuid: 5f93bc27-5edd-4143-8701-87896c52f0af
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: a70aa448-0f58-4ed2-9381-afcc76fa827f
role: User, Admin
exl-id: 698e8bdb-9b31-49ab-8560-26b05109bb23
feature: Configuration
source-git-commit: 65af6e33ae3897519491952f4d3a6832700f77b2
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# Attivare la protezione hot link in Dynamic Media {#activating-hotlink-protection-in-dynamic-media}

Il collegamento rapido si verifica quando un sito web di terze parti utilizza codice HTML per visualizzare un’immagine dal sito web. Utilizzano la larghezza di banda ogni volta che l&#39;immagine viene richiesta perché il browser del visitatore vi accede direttamente dal server. Hotlink *protection* è un metodo per impedire ad altri siti web di collegarsi direttamente a immagini, CSS o JavaScript sulle tue pagine web. Questo tipo di schermo aiuta a ridurre l&#39;utilizzo di larghezza di banda inutile sotto il tuo account Dynamic Media.

[Ad Experience Manager, il ](https://experienceleague.adobe.com/?support-solution=Experience+Manager#support) supporto clienti può configurare un filtro referente a livello CDN (Content Delivery Network) in modo che i contenuti Dynamic Media vengano serviti solo ai siti web nell’elenco dei siti web consentiti per il dominio.

>[!NOTE]
>
>Questa funzione richiede l’utilizzo della rete CDN preconfigurata fornita con Adobe Experience Manager Dynamic Media. Qualsiasi altra CDN personalizzata non è supportata con questa funzione. Per attivare la protezione hot link, un amministratore deve creare un ticket di supporto clienti Adobe per richiedere la modifica della configurazione al tuo account Dynamic Media. Non vi sono costi aggiuntivi per attivare la protezione hot link.
