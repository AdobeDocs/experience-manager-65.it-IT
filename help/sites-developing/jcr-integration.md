---
title: Integrazione JCR
seo-title: JCR Integration
description: Suggerimenti su quando integrare a livello JCR
seo-description: Tips for when you must integrate at the JCR level
uuid: 11518baf-521e-471d-ad4f-2baa76075cfa
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: e6647a11-a36e-4808-bb61-29b2895c6b1d
exl-id: 170474c1-c7f4-446c-bda4-84768d44a078
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---

# Integrazione JCR{#jcr-integration}

## Preferisci l’API della risorsa Sling all’API JCR {#prefer-the-sling-resource-api-to-jcr-api}

L’API Sling funziona a un livello più alto e più astratto dell’API JCR. In questo modo il codice è più riutilizzabile e indipendente dall’archiviazione sottostante. In questo modo è più semplice includere dati virtuali esterni tramite il meccanismo ResourceProvider, se necessario.

## Se possibile, evita le query {#avoid-queries-wherever-possible}

La navigazione nel repository per il recupero dei dati è sempre più rapida rispetto all&#39;esecuzione di una query. In alcuni casi saranno necessarie query, ad esempio una query dell’utente finale o la necessità di trovare contenuto strutturato dall’intero archivio, ma per tutti gli altri casi è preferibile passare ai nodi necessari. Le query devono sempre essere evitate nella logica di rendering, ad esempio nei componenti di navigazione, in un &quot;elenco di elementi recenti&quot;, nei conteggi di elementi e così via. In questi casi, è preferibile spostarsi nella gerarchia o pre-memorizzare in cache il risultato in modo che possa essere utilizzato direttamente durante il rendering.

## Limitare l’ambito dell’osservazione JCR {#restrict-the-scope-of-jcr-observation}

Quando si ascoltano gli eventi nell’archivio, è importante restringere il più possibile l’ambito. Ad esempio, è molto meglio ascoltare un evento all’indirizzo `/etc/mycompany` che per ascoltare `/etc`. Non ascoltare mai gli eventi nella directory principale dell’archivio. Inoltre, assicurati che i metodi di callback vengano eseguiti il più rapidamente possibile quando non hanno nulla da fare.

## Eliminare l’utilizzo dell’accesso come amministratore JCR {#eliminate-use-of-jcr-admin-access}

A partire da AEM 6, login Administrative è stato dichiarato obsoleto in quanto ha ottenuto una sessione amministrativa da ResourceResolverFactory. È invece necessario creare account di servizio per le operazioni di back office che richiederebbero questo tipo di accesso e utilizzare ResourceResolverFactory per ottenere un ResourceResolver per questo account.
