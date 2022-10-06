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

La capacità di un membro della comunità di seguire [attività](activities.md) oltre a essere seguito è costituito da due componenti: `Follow` e `Following`.

La `Follow` Il componente deve essere associato a un’altra risorsa e questa associazione è già stabilita per i membri e le funzionalità della community.

La `Following` Il componente elenca semplicemente i membri che seguono il membro corrente o che sono seguiti dal membro corrente. Questo grafico social delle relazioni tra i membri è incluso nel profilo utente stabilito per un [sito della community](overview.md#communitiessites).

## Aggiunta di seguito a una pagina {#adding-following-to-a-page}

Se desideri aggiungere una `Following` in una pagina in modalità di authoring, individua il componente `Communities / Following` e trascinalo nella posizione in una pagina in cui dovrebbe essere visualizzato il grafico social.

Per le informazioni necessarie, visita [Nozioni di base sui componenti di Communities](basics.md).

Quando il [librerie lato client richieste](essentials-socialgraph.md#essentials-for-client-side) sono inclusi, è così che `Following` apparirà il componente:

![seguente](assets/following.png)

## Configurazione seguente {#configuring-following}

Attualmente, è necessario impostare la proprietà per determinare se il componente visualizza il `follows` o `following` relazione.

## Informazioni aggiuntive {#additional-information}

Per ulteriori informazioni, consulta [Nozioni di base sul grafico social](essentials-socialgraph.md) per sviluppatori.
