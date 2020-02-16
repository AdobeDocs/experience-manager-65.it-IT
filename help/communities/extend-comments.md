---
title: Estendi componente commenti
seo-title: Estendi componente commenti
description: Estendi il componente Commenti per modificarne l’aspetto o il comportamento per usi specifici
seo-description: Estendi il componente Commenti per modificarne l’aspetto o il comportamento per usi specifici
uuid: 6f439097-b1d0-4e7d-afcf-01d8f43aa866
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a07a4690-0e47-4a76-84cb-96abdc70b835
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Estendi componente commenti {#extend-comments-component}

L’intenzione di [estendere](client-customize.md#extensions) un componente predefinito consiste nel modificare l’aspetto o il comportamento di un componente per usi specifici.

Il percorso del componente è univoco e fa riferimento al componente predefinito come super tipo di risorsa. Il rischio è minore in quanto l’ambito è limitato rispetto all’ambito globale di una sovrapposizione di componente.

>[!NOTE]
>
>L’estensione di un componente [sovrapposto](client-customize.md#overlays) non è supportata.

## Esempio {#example}

Supponiamo che l’intestazione del componente commento debba essere visualizzata con un aspetto alternativo in un sito dell’istanza AEM, mentre viene visualizzata con la visualizzazione predefinita in un altro sito. Invece di sovrapporre il commento predefinito, che modifica il componente commento per tutte le istanze, una soluzione migliore consiste nell’assicurare che vi siano più componenti commento disponibili per l’uso in vari siti.

Per implementare questa soluzione, crea un nuovo componente che estende (sostituisce) quello esistente e modifica lo script Handlebars. L&#39;area del sito che utilizza i nuovi commenti può utilizzare quella estesa, mentre i siti che utilizzano l&#39;aspetto predefinito rimangono invariati.

Il componente commento è in realtà uno dei due componenti che compongono il sistema di commenti. Esistono quindi due componenti da estendere: *commenti* e *commenti*. Lo script da modificare si trova nel `header.hbs` file del componente *comment *e il componente *commenti* padre (il sistema di commenti) è ciò che un autore aggiunge effettivamente alla pagina.

Per estendere i commenti è necessario:

1. [Creare i componenti](extend-create-components.md)
1. [Aggiungi commento a pagina di esempio](extend-sample-page.md)
1. [Modifica dell&#39;aspetto](extend-alter-appearance.md)

