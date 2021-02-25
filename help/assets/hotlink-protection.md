---
title: Attivazione della protezione tramite collegamento caldo in Dynamic Media
description: Informazioni su come attivare la protezione tramite collegamento caldo in Dynamic Media.
uuid: 5f93bc27-5edd-4143-8701-87896c52f0af
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: a70aa448-0f58-4ed2-9381-afcc76fa827f
translation-type: tm+mt
source-git-commit: 787f3b4cf5835b7e9b03e3f4e6f6597084adec8c
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---


# Attivazione della protezione tramite collegamento caldo in Dynamic Media {#activating-hotlink-protection-in-dynamic-media}

Il collegamento a caldo si verifica quando un sito Web di terze parti utilizza il codice HTML per visualizzare un’immagine dal sito Web. Usano la larghezza di banda ogni volta che l&#39;immagine viene richiesta, perché il browser del visitatore vi accede direttamente dal server. Hotlink *protected* è un metodo per impedire ad altri siti Web di collegarsi direttamente a immagini, css o JavaScript nelle pagine Web. Questo tipo di schermo consente di ridurre l&#39;utilizzo non necessario della larghezza di banda nell&#39;account Dynamic Media.

[ Adobe ](https://helpx.adobe.com/support.html) Supportatore può configurare un filtro di riferimento a livello CDN (Content Delivery Network), in modo che il contenuto Dynamic Media venga distribuito solo ai siti Web inclusi nell’elenco dei siti Web consentiti per il dominio.

>[!NOTE]
>
>Questa funzione richiede l’utilizzo del CDN fornito con Adobe Experience Manager Dynamic Media. Qualsiasi altra CDN personalizzata non è supportata con questa funzione. Per attivare la protezione tramite collegamento caldo, un amministratore deve creare un ticket di assistenza clienti  Adobe per richiedere la modifica alla configurazione dell&#39;account Dynamic Media. Non sono previsti costi aggiuntivi per l&#39;attivazione della protezione tramite collegamento a caldo.
