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

La capacità di un membro della comunità di seguire e seguire [le attività](activities.md) è stabilita attraverso due componenti: `Follow` e `Following`.

Il `Follow` componente deve essere associato a un&#39;altra risorsa e questa associazione è già definita per i membri e le caratteristiche della community.

Il `Following` componente elenca semplicemente i membri che seguono il membro corrente o che sono seguiti dal membro corrente. Questo grafico social delle relazioni tra i membri è incluso nel profilo utente stabilito per un sito [](overview.md#communitiessites)community.

## Aggiunta di seguito a una pagina {#adding-following-to-a-page}

Se desiderate aggiungere un `Following` componente a una pagina in modalità di creazione, individuate il componente `Communities / Following` e trascinatelo nella posizione desiderata su una pagina in cui dovrebbe comparire il grafico social.

Per le informazioni necessarie, consulta [Community Components Basics](basics.md).

Quando sono incluse le librerie [lato client](essentials-socialgraph.md#essentials-for-client-side) richieste, verrà visualizzato il `Following` componente:

![seguente](assets/following.png)

## Configurazione di quanto segue {#configuring-following}

Al momento è necessario impostare la proprietà per determinare se il componente visualizza la `follows` relazione o la `following` relazione.

## Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili nella pagina [Social Graph Essentials](essentials-socialgraph.md) per gli sviluppatori.
