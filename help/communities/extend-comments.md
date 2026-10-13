---
title: Estendi componente commenti
description: Estendere il componente Commenti per modificarne l'aspetto o il comportamento per utilizzi specifici
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: e57198cb-8fd9-43e2-b416-e40e462561c8
solution: Experience Manager
feature: Communities
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%
---
# Estendi componente commenti  {#extend-comments-component}

L&#39;intenzione di [estendere](client-customize.md#extensions) un componente predefinito è di alterare l&#39;aspetto o il comportamento di un componente per usi specifici.

Il percorso del componente è univoco e fa riferimento al componente predefinito come tipo di risorsa super. Il rischio è minore in quanto l’ambito è limitato rispetto all’ambito globale di una sovrapposizione di componenti.

>[!NOTE]
>
>L&#39;estensione di un componente [sovrapposto](client-customize.md#overlays) non è supportata.

## Esempio {#example}

Supponiamo che l’intestazione del componente Commento debba essere visualizzata con un aspetto alternativo in un sito dell’istanza di AEM, mentre appare con la visualizzazione predefinita in un altro sito. Invece di sovrapporre il commento predefinito, che modifica il componente Commento per tutte le istanze, una soluzione migliore è garantire che siano disponibili più componenti di commento da utilizzare su vari siti.

Per implementare questa soluzione, crea un componente che estende (sostituisce) quello esistente e modifica lo script Handlebars. L&#39;area del sito che utilizza i nuovi commenti può utilizzare quello esteso, mentre i siti che utilizzano l&#39;aspetto predefinito rimangono invariati.

Il componente Commento è in realtà uno dei due componenti che compongono il sistema di commenti. Pertanto, sono disponibili due componenti da estendere: *commenti* e *commento*. Lo script da modificare si trova nel file `header.hbs` del componente *comment*, mentre il componente *comments* principale (il sistema di commenti) è ciò che un autore aggiunge effettivamente alla pagina.

Per estendere i commenti, è necessario:

1. [Creare i componenti](extend-create-components.md)
1. [Aggiungi commento alla pagina di esempio](extend-sample-page.md)
1. [Modificare l&#39;aspetto](extend-alter-appearance.md)
