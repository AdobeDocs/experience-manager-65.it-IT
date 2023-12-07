---
title: Attivazione della protezione hotlinking in Dynamic Medie
description: Informazioni su come attivare la protezione hotlink in Dynamic Medie.
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
role: User, Admin
exl-id: 698e8bdb-9b31-49ab-8560-26b05109bb23
feature: Configuration
source-git-commit: 04050f31742c926b45235595f6318929d3767bd8
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# Attivare la protezione hotlinking in Dynamic Medie {#activating-hotlink-protection-in-dynamic-media}

Il collegamento rapido si verifica quando un sito web di terze parti utilizza un codice HTML per visualizzare un’immagine dal sito web. Utilizzano la larghezza di banda ogni volta che l&#39;immagine viene richiesta, perché il browser del visitatore vi accede direttamente dal server. Hotlink *protezione* è un metodo per impedire ad altri siti web di collegarsi direttamente a immagini, CSS o JavaScript nelle pagine web. Questo tipo di schermatura contribuisce a ridurre l’utilizzo di larghezza di banda non necessaria con il tuo account Dynamic Medie.

[Assistenza clienti Experience Manager](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;lang=it#support) può configurare un filtro referente a livello di CDN (Content Delivery Network) in modo che il contenuto Dynamic Medie venga distribuito solo ai siti web inclusi nell’elenco dei siti web consentiti per il dominio.

>[!NOTE]
>
>Questa funzione richiede l’utilizzo della rete CDN preconfigurata fornita in bundle con Adobe Experience Manager Dynamic Medie. Qualsiasi altra rete CDN personalizzata non è supportata con questa funzione. Per attivare la protezione tramite collegamento rapido, un amministratore deve creare un ticket di supporto tecnico Adobe per richiedere la modifica della configurazione dell’account Dynamic Medie. L&#39;attivazione della protezione hotlink non comporta costi aggiuntivi.
