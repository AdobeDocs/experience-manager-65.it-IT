---
title: Utilizzo di Social Graph
description: Scopri come aggiungere un componente Segue a una pagina che consente ai membri della community con accesso effettuato di seguire o seguire le attività.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 2cd1436b-3727-4757-b28e-70756be78a4e
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 1%

---

# Utilizzo di Social Graph {#using-social-graph}

## Introduzione {#introduction}

Possibilità per un membro della community di seguire [attività](activities.md) e l’essere seguiti si stabilisce attraverso due componenti: `Follow` e `Following`.

Il `Follow` il componente deve essere associato a un&#39;altra risorsa e questa associazione è già stata stabilita per i membri e le funzionalità della community.

Il `Following` Il componente elenca semplicemente i membri che seguono il membro corrente o che sono seguiti dal membro corrente. Questo grafico social network delle relazioni tra i membri è incluso nel profilo utente stabilito per un [sito community](overview.md#communitiessites).

## Aggiunta di quanto segue a una pagina {#adding-following-to-a-page}

Se si desidera aggiungere un `Following` a una pagina in modalità di authoring, individua il componente `Communities / Following` e trascinarlo nella posizione in cui dovrebbe apparire il grafico social.

Per informazioni necessarie, visitare il sito [Nozioni di base sui componenti community](basics.md).

Quando [librerie lato client richieste](essentials-socialgraph.md#essentials-for-client-side) sono inclusi, è così che `Following` viene visualizzato il componente:

![segue](assets/following.png)

## Configurazione dei seguenti elementi {#configuring-following}

Attualmente, è necessario impostare la proprietà per determinare se il componente visualizza `follows` relazione o `following` relazione.

## Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili sul sito [Nozioni di base sui grafici social](essentials-socialgraph.md) pagina per sviluppatori.
