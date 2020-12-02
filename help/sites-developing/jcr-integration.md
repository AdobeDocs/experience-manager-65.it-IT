---
title: Integrazione JCR
seo-title: Integrazione JCR
description: Suggerimenti per l’integrazione a livello JCR
seo-description: Suggerimenti per l’integrazione a livello JCR
uuid: 11518baf-521e-471d-ad4f-2baa76075cfa
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: e6647a11-a36e-4808-bb61-29b2895c6b1d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---


# Integrazione JCR{#jcr-integration}

## Preferisci Sling Resource API all&#39;API JCR {#prefer-the-sling-resource-api-to-jcr-api}

L&#39;API Sling funziona a un livello più alto e astratto rispetto all&#39;API JCR. Questo consente al codice di essere più riutilizzabile e indipendente dallo storage sottostante. Ciò semplifica l&#39;inclusione di dati virtuali esterni tramite il meccanismo ResourceProvider, se necessario.

## Evitare query dove possibile {#avoid-queries-wherever-possible}

È sempre più veloce navigare nella directory archivio per recuperare i dati rispetto all&#39;esecuzione di una query. In alcuni casi saranno necessarie query, ad esempio una query per l&#39;utente finale o la necessità di trovare contenuto strutturato dall&#39;intero repository, ma per tutti gli altri casi è preferibile passare ai nodi necessari. Le query devono sempre essere evitate nella logica di rendering, ad esempio componenti di navigazione, un &quot;elenco di elementi recenti&quot;, un conteggio di elementi e così via. In questi casi, è meglio spostarsi nella gerarchia o prememorizzare il risultato nella cache in modo che possa essere utilizzato direttamente durante il rendering.

## Limitare l&#39;ambito dell&#39;osservazione JCR {#restrict-the-scope-of-jcr-observation}

Quando si ascoltano gli eventi nella directory archivio, è importante restringere il più possibile l&#39;ambito. Ad esempio, è molto meglio ascoltare un evento in `/etc/mycompany` piuttosto che ascoltare `/etc`. Non ascoltare mai gli eventi nella directory principale del repository. Inoltre, accertatevi che i metodi di callback vengano eseguiti il più rapidamente possibile quando non è possibile eseguire alcuna operazione.

## Eliminazione dell&#39;utilizzo dell&#39;accesso dell&#39;amministratore JCR {#eliminate-use-of-jcr-admin-access}

A partire dal AEM 6, l&#39;account di accesso Administrative è stato dichiarato obsoleto, così come una sessione amministrativa di ResourceResolverFactory. È invece necessario creare account di servizio per le operazioni back office che richiedono questo tipo di accesso e ResourceResolverFactory può essere utilizzato per ottenere un ResourceResolver per questo account.
