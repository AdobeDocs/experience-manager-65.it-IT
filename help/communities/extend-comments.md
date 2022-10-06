---
title: Estendi componente Commenti
seo-title: Extend Comments Component
description: Estende il componente Commenti per modificarne l’aspetto o il comportamento per usi specifici
seo-description: Extend the Comments component to alter its appearance or behavior for specific uses
uuid: 6f439097-b1d0-4e7d-afcf-01d8f43aa866
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a07a4690-0e47-4a76-84cb-96abdc70b835
exl-id: e57198cb-8fd9-43e2-b416-e40e462561c8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%

---

# Estendi componente Commenti  {#extend-comments-component}

L&#39;intenzione di [estensione](client-customize.md#extensions) un componente predefinito è quello di modificare l’aspetto o il comportamento di un componente per usi specifici.

Il percorso del componente è univoco e fa riferimento al componente predefinito come super tipo di risorsa. Il rischio è minore in quanto l’ambito di applicazione è limitato rispetto all’ambito globale di una sovrapposizione di componenti.

>[!NOTE]
>
>Estensione di un [sovrapposto](client-customize.md#overlays) componente non supportato.

## Esempio {#example}

Supponiamo che l’intestazione del componente commento debba essere visualizzata con un aspetto alternativo in un sito dell’istanza AEM, mentre appare con la visualizzazione predefinita in un altro sito. Invece di sovrapporre il commento predefinito, che cambia il componente commento per tutte le istanze, una soluzione migliore è quella di garantire che ci siano più componenti commento disponibili per l&#39;uso su vari siti.

Per implementare questa soluzione, crea un nuovo componente che estenda (sostituisce) quello esistente e modifichi lo script Handlebars. L&#39;area del sito che utilizza i nuovi commenti può utilizzare quella estesa, mentre i siti che utilizzano l&#39;aspetto predefinito rimangono invariati.

Il componente commento è in realtà uno dei due componenti che compongono il sistema di commento. Pertanto, esistono due componenti da estendere: *commenti* e *commento*. Lo script da modificare si trova nel *commento* del componente `header.hbs` , mentre il padre *commenti* Il componente (il sistema di commenti) è ciò che un autore aggiunge effettivamente alla pagina.

Per estendere i commenti è necessario:

1. [Creare i componenti](extend-create-components.md)
1. [Aggiungi commento alla pagina di esempio](extend-sample-page.md)
1. [Modificare l’aspetto](extend-alter-appearance.md)
