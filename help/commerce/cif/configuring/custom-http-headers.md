---
title: Intestazioni HTTP personalizzate
description: Configurazione di intestazioni HTTP personalizzate
source-git-commit: 7d174be35cb99d802e4aeff6f4d955b1b92cab74
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 1%

---


# Intestazioni HTTP personalizzate {#custom-http-headers}

## Panoramica {#overview}

Per ottenere un maggiore controllo sul back-end, gli autori possono configurare intestazioni HTTP personalizzate che verrebbero inviate al motore di e-commerce, insieme a quelle già inviate da CIF. I casi d’uso comuni includono configurazioni multi-store in cui puoi utilizzare intestazioni HTTP per controllare la risposta del back-end commerce.

>[!NOTE]
>
>Gli sviluppatori possono sempre configurare intestazioni HTTP personalizzate utilizzando la configurazione client GraphQL.


## Configurazione {#configuration}

Per configurare le intestazioni HTTP personalizzate, è innanzitutto necessario definirle. Le intestazioni HTTP personalizzate devono prima essere definite aggiungendole alla configurazione del servizio `com.adobe.cq.cif.http.internal.HttpHeadersConfigProviderImpl` utilizzando una configurazione OSGi.

Puoi configurare i valori delle intestazioni HTTP nella pagina Configurazione Cloud Service per il progetto:

1. Vai alla pagina di configurazione del Cloud Service in Strumenti -> Cloud Services -> Configurazione CIF
1. Apri una configurazione esistente o creane una nuova
1. Vai alla scheda &quot;Avanzate&quot; e trova il campo multiplo &quot;Intestazioni HTTP personalizzate&quot;. È possibile selezionare le intestazioni definite in precedenza e assegnare loro valori.

I componenti che utilizzano la configurazione del servizio cloud di cui sopra invieranno queste intestazioni HTTP con ogni richiesta GraphQL.

## Restrizioni {#restrictions}

Il servizio consente di definire i nomi di intestazione, inclusi quelli standard, ma non sarà disponibile per la configurazione. In altre parole, non è possibile ignorare le intestazioni HTTP standard utilizzando questa funzione. Un elenco di nomi di intestazione limitati è disponibile [qui](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers). Oltre a questi, ci sono altre due intestazioni che non possono essere utilizzate:

* &quot;Store&quot; - utilizzato da CIF per identificare l&#39;archivio Magenti
* &quot;Preview-Version&quot; - utilizzato da CIF per recuperare i prodotti in staging
