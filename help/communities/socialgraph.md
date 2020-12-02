---
title: Utilizzo di Social Graph
seo-title: Utilizzo di Social Graph
description: Aggiunta di un componente seguente a una pagina
seo-description: Aggiunta di un componente seguente a una pagina
uuid: 8be6334b-e6c9-40bc-90a8-750b98419470
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 0ce57ab1-e4c6-4c38-963d-556eef8757f2
translation-type: tm+mt
source-git-commit: 1429a099288f038510cb0a194fb55632297ef371
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 1%

---


# Utilizzo di Social Graph {#using-social-graph}

## Introduzione {#introduction}

La capacità di un membro della comunità di seguire [le attività](activities.md) così come di essere seguito è stabilita tramite due componenti: `Follow` e `Following`.

Il componente `Follow` deve essere associato a un&#39;altra risorsa, e questa associazione è già stabilita per i membri della community e le funzioni.

Il componente `Following` elenca semplicemente i membri che seguono il membro corrente o che sono seguiti dal membro corrente. Questo grafico social delle relazioni tra i membri è incluso nel profilo utente stabilito per un [sito community](overview.md#communitiessites).

## Aggiunta di seguito a una pagina {#adding-following-to-a-page}

Se desiderate aggiungere un componente `Following` a una pagina in modalità di creazione, individuate il componente `Communities / Following` e trascinatelo nella posizione desiderata su una pagina in cui dovrebbe essere visualizzato il grafico social.

Per le informazioni necessarie, visitare [Community Components Basics](basics.md).

Quando vengono incluse le [librerie lato client ](essentials-socialgraph.md#essentials-for-client-side), viene visualizzato il componente `Following`:

![seguente](assets/following.png)

## Configurazione di {#configuring-following}

Attualmente è necessario impostare la proprietà per determinare se il componente visualizza la relazione `follows` o la relazione `following`.

## Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili nella pagina [Social Graph Essentials](essentials-socialgraph.md) per gli sviluppatori.
