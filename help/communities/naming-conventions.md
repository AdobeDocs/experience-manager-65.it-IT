---
title: Convenzioni di denominazione in Java&trade; nome pacchetto
description: Scopri le convenzioni di denominazione e l’utilizzo dei trattini nel nome del pacchetto Java&trade.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 863900c3-5fe8-41a3-a151-466d0c62eeea
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 1%

---

# Convenzioni di denominazione {#naming-conventions}

## Trattini nel nome del pacchetto Java™ {#hyphens-in-java-package-name}

Quando si crea una posizione per una classe Java™, il nome del pacchetto deve corrispondere a quello della posizione della cartella dell’archivio con eventuali trattini nel percorso correttamente preceduti da un carattere di escape.

Sebbene l’utilizzo dei trattini nei nomi degli elementi dell’archivio sia una pratica consigliata nello sviluppo AEM, i trattini non sono consentiti nei nomi dei pacchetti Java™.

La piattaforma CRX sottostante deve essere in grado di distinguere un carattere di sottolineatura effettivo `_ `e un trattino `-`. Pertanto, in JCR, il trattino deve essere sostituito con il relativo valore Unicode (u002d) ed evitato con un trattino basso `_`.

Ad esempio, se il percorso dell’archivio è **/apps/my-example/component/info/Info.java**, il nome del pacchetto deve essere `java package apps.my_002dexample.component.info;`

Si noti che un carattere di sottolineatura deve essere evitato in modo simile, tale che `_` diventa `_005f`.
