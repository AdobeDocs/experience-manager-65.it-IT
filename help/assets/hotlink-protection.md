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
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# Attivare la protezione hotlinking in Dynamic Medie {#activating-hotlink-protection-in-dynamic-media}

Il collegamento rapido si verifica quando un sito web di terze parti utilizza un codice HTML per visualizzare un’immagine dal sito web. Utilizzano la larghezza di banda ogni volta che l&#39;immagine viene richiesta, perché il browser del visitatore vi accede direttamente dal server. Hotlink *protezione* è un metodo per impedire ad altri siti Web di collegarsi direttamente a immagini, CSS o JavaScript nelle pagine Web. Questo tipo di schermatura contribuisce a ridurre l’utilizzo di larghezza di banda non necessaria con il tuo account Dynamic Medie.

[L&#39;Assistenza clienti Experience Manager](https://experienceleague.adobe.com/it?support-solution=Experience+Manager&lang=it#support) può configurare un filtro referente a livello di rete CDN (Content Delivery Network) in modo che il contenuto Dynamic Medie venga distribuito solo ai siti Web inclusi nell&#39;elenco dei siti Web consentiti per il dominio.

>[!NOTE]
>
>Questa funzione richiede l’utilizzo della rete CDN preconfigurata fornita in bundle con Adobe Experience Manager Dynamic Medie. Qualsiasi altra rete CDN personalizzata non è supportata con questa funzione. Per attivare la protezione tramite collegamento rapido, un amministratore deve creare un ticket di supporto tecnico Adobe per richiedere la modifica della configurazione dell’account Dynamic Medie. L&#39;attivazione della protezione hotlink non comporta costi aggiuntivi.
