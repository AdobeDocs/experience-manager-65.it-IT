---
title: Intestazioni HTTP personalizzate
description: Scopri come configurare le intestazioni HTTP personalizzate in Adobe Experience Manager Commerce.
exl-id: 834aadac-c3be-4e7a-a3cb-349608810b40
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: f30decf0e32a520dcda04b89c5c1f5b67ab6e028
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 3%

---

# Intestazioni HTTP personalizzate {#custom-http-headers}

## Panoramica {#overview}

Per ottenere un maggiore controllo sul backend, gli autori possono configurare intestazioni HTTP personalizzate da inviare al motore di e-commerce, insieme a quelle già inviate dall’CIF. I casi d’uso comuni includono impostazioni multi-store in cui puoi utilizzare le intestazioni HTTP per controllare la risposta del back-end di Commerce.

>[!NOTE]
>
>Gli sviluppatori possono sempre configurare intestazioni HTTP personalizzate utilizzando la configurazione client di GraphQL.
>

## Configurazione {#configuration}

Per configurare le intestazioni HTTP personalizzate, devi prima definirle. Le intestazioni HTTP personalizzate devono prima essere definite aggiungendole alla configurazione del servizio `com.adobe.cq.cif.http.internal.HttpHeadersConfigProviderImpl` tramite una configurazione OSGi.

Puoi configurare i valori delle intestazioni HTTP nella pagina Configurazione Cloud Service per il progetto:

1. Vai alla pagina di configurazione del Cloud Service in Strumenti > Cloud Services > Configurazione CIF.
1. Apri una configurazione esistente o creane una.
1. Vai alla scheda &quot;Avanzate&quot; e trova il multicampo &quot;Intestazioni HTTP personalizzate&quot;. Puoi selezionare le intestazioni definite in precedenza e assegnarvi dei valori.

I componenti che utilizzano la configurazione del servizio cloud precedente inviano queste intestazioni HTTP a ogni richiesta di GraphQL.

## Restrizioni {#restrictions}

Anche se il servizio consente di definire qualsiasi nome di intestazione, inclusi quelli standard, non sono disponibili per la configurazione. In altre parole, non puoi sovrascrivere le intestazioni HTTP standard con questa funzione. Un elenco di nomi di intestazione con restrizioni si trova in [documenti Web MDN - intestazioni HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers). Oltre a queste, ci sono altre due intestazioni che non possono essere utilizzate:

* &quot;Store&quot;: utilizzato dall’CIF per identificare il negozio Adobe Commerce
* &quot;Preview-Version&quot;: utilizzato dall&#39;CIF per recuperare i prodotti in staging
