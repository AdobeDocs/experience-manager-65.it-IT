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
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 1%
---
# Utilizzo di Social Graph {#using-social-graph}

## Introduzione {#introduction}

La possibilità per un membro della community di seguire [attività](activities.md) è stabilita tramite due componenti: `Follow` e `Following`.

Il componente `Follow` deve essere associato a un&#39;altra risorsa e questa associazione è già stata stabilita per i membri e le funzionalità della community.

Il componente `Following` elenca semplicemente i membri che seguono il membro corrente o che sono seguiti dal membro corrente. Questo grafico social delle relazioni tra i membri è incluso nel profilo utente stabilito per un [sito community](overview.md#communitiessites).

## Aggiunta di quanto segue a una pagina {#adding-following-to-a-page}

Se si desidera aggiungere un componente `Following` a una pagina in modalità di creazione, individuare il componente `Communities / Following` e trascinarlo in una pagina in cui dovrebbe essere visualizzato il grafico social.

Per informazioni necessarie, visitare [Nozioni di base sui componenti delle community](basics.md).

Quando sono incluse le [librerie lato client richieste](essentials-socialgraph.md#essentials-for-client-side), il componente `Following` viene visualizzato in questo modo:

![seguenti](assets/following.png)

## Configurazione dei seguenti elementi {#configuring-following}

Attualmente, è necessario impostare la proprietà per determinare se il componente visualizza la relazione `follows` o la relazione `following`.

## Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili nella pagina [Social Graph Essentials](essentials-socialgraph.md) per sviluppatori.
