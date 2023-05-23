---
title: Utilizzo di Social Graph
seo-title: Using Social Graph
description: Aggiunta di un componente seguente a una pagina
seo-description: Adding a Following component to a page
uuid: 8be6334b-e6c9-40bc-90a8-750b98419470
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 0ce57ab1-e4c6-4c38-963d-556eef8757f2
exl-id: 2cd1436b-3727-4757-b28e-70756be78a4e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 1%

---

# Utilizzo di Social Graph {#using-social-graph}

## Introduzione {#introduction}

Possibilità per un membro della community di seguire [attività](activities.md) L’eVar viene stabilito attraverso due componenti: `Follow` e `Following`.

Il `Follow` il componente deve essere associato a un&#39;altra risorsa e questa associazione è già stata stabilita per i membri e le funzionalità della community.

Il `Following` Il componente elenca semplicemente i membri che seguono il membro corrente o che sono seguiti dal membro corrente. Questo grafico social network delle relazioni tra i membri è incluso nel profilo utente stabilito per un [sito community](overview.md#communitiessites).

## Aggiunta di quanto segue a una pagina {#adding-following-to-a-page}

Se si desidera aggiungere un `Following` a una pagina in modalità di authoring, individua il componente `Communities / Following` e trascinarlo nella posizione in cui dovrebbe apparire il grafico social.

Per informazioni necessarie, visitare il sito [Nozioni di base sui componenti community](basics.md).

Quando [librerie lato client richieste](essentials-socialgraph.md#essentials-for-client-side) sono inclusi, è così che `Following` Il componente verrà visualizzato:

![segue](assets/following.png)

## Configurazione dei seguenti elementi {#configuring-following}

Attualmente, è necessario impostare la proprietà per determinare se il componente visualizza `follows` relazione o `following` relazione.

## Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili sul sito [Nozioni di base sui grafici social](essentials-socialgraph.md) pagina per sviluppatori.
