---
title: Intestazioni HTTP personalizzate
description: Configurazione delle intestazioni HTTP personalizzate
exl-id: 834aadac-c3be-4e7a-a3cb-349608810b40
source-git-commit: a467009851937c4a10b165a3d253c47bf990bbc5
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 5%

---

# Intestazioni HTTP personalizzate {#custom-http-headers}

## Panoramica {#overview}

Per ottenere un maggiore controllo sul backend, gli autori possono configurare intestazioni HTTP personalizzate da inviare al motore di e-commerce, insieme a quelle già inviate da CIF. I casi d’uso comuni includono impostazioni multi-store in cui puoi utilizzare le intestazioni HTTP per controllare la risposta del back-end di Commerce.

>[!NOTE]
>
>Gli sviluppatori possono sempre configurare intestazioni HTTP personalizzate utilizzando la configurazione client di GraphQL.

## Configurazione {#configuration}

Per configurare le intestazioni HTTP personalizzate, è necessario prima definirle. Le intestazioni HTTP personalizzate devono prima essere definite aggiungendole al `com.adobe.cq.cif.http.internal.HttpHeadersConfigProviderImpl` configurazione del servizio tramite una configurazione OSGi.

Puoi configurare i valori delle intestazioni HTTP nella pagina Configurazione Cloud Service per il progetto:

1. Vai alla pagina di configurazione del Cloud Service in Strumenti -> Cloud Services -> Configurazione CIF
1. Apri una configurazione esistente o creane una nuova
1. Vai alla scheda &quot;Avanzate&quot; e trova il multicampo &quot;Intestazioni HTTP personalizzate&quot;. Puoi selezionare le intestazioni definite in precedenza e assegnarvi dei valori.

I componenti che utilizzano la configurazione del servizio cloud precedente invieranno queste intestazioni HTTP a ogni richiesta di GraphQL.

## Restrizioni {#restrictions}

Anche se il servizio consente di definire qualsiasi nome di intestazione, inclusi quelli standard, non saranno disponibili per la configurazione. In altre parole, non puoi sovrascrivere le intestazioni HTTP standard con questa funzione. È possibile trovare un elenco di nomi di intestazione con restrizioni [qui](https://developer.mozilla.org/it-IT/docs/Web/HTTP/Headers). Oltre a queste, ci sono altre due intestazioni che non possono essere utilizzate:

* &quot;Store&quot;: utilizzato da CIF per identificare lo store di Adobe Commerce
* &quot;Preview-Version&quot;: utilizzato da CIF per recuperare i prodotti in staging
