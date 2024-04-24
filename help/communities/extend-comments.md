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
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---

# Estendi componente commenti  {#extend-comments-component}

L&#39;intenzione di [estensione](client-customize.md#extensions) un componente di default consiste nel modificare l&#39;aspetto o il comportamento di un componente per usi specifici.

Il percorso del componente è univoco e fa riferimento al componente predefinito come tipo di risorsa super. Il rischio è minore in quanto l’ambito è limitato rispetto all’ambito globale di una sovrapposizione di componenti.

>[!NOTE]
>
>Estensione di un [sovrapposto](client-customize.md#overlays) componente non supportato.

## Esempio {#example}

Supponiamo che l’intestazione del componente Commento debba essere visualizzata con un aspetto alternativo in un sito dell’istanza AEM, mentre appare con la visualizzazione predefinita in un altro sito. Invece di sovrapporre il commento predefinito, che modifica il componente Commento per tutte le istanze, una soluzione migliore è garantire che siano disponibili più componenti di commento da utilizzare su vari siti.

Per implementare questa soluzione, crea un componente che estende (sostituisce) quello esistente e modifica lo script Handlebars. L&#39;area del sito che utilizza i nuovi commenti può utilizzare quello esteso, mentre i siti che utilizzano l&#39;aspetto predefinito rimangono invariati.

Il componente Commento è in realtà uno dei due componenti che compongono il sistema di commenti. Pertanto, esistono due componenti da estendere: *commenti* e *commento*. Lo script da modificare si trova in *commento* del componente `header.hbs` file, mentre l&#39;elemento padre *commenti* componente (il sistema di commenti) è ciò che un autore aggiunge effettivamente alla pagina.

Per estendere i commenti, è necessario:

1. [Creare i componenti](extend-create-components.md)
1. [Aggiungi commento alla pagina di esempio](extend-sample-page.md)
1. [Modificare l&#39;aspetto](extend-alter-appearance.md)
