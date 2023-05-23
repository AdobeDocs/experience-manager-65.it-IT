---
title: Convenzioni di denominazione nel nome del pacchetto Java
description: Trattini nel nome del pacchetto Java
uuid: 48086e6c-c35b-4ffc-b216-d01feca7bf9a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 5271feb9-70c6-4c82-8ac7-34a63d80e3aa
exl-id: 863900c3-5fe8-41a3-a151-466d0c62eeea
source-git-commit: a2fd3c0c1892ac648c87ca0dec440e22144c37a2
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 1%

---

# Convenzioni di denominazione {#naming-conventions}

## Trattini nel nome del pacchetto Java {#hyphens-in-java-package-name}

Quando crei una posizione per una classe Java, tieni presente che il nome del pacchetto deve corrispondere a quello della posizione della cartella dell’archivio con eventuali trattini nel percorso correttamente preceduti da un carattere di escape.

Sebbene l’utilizzo dei trattini nei nomi degli elementi dell’archivio sia una pratica consigliata nello sviluppo dell’AEM, i trattini non sono consentiti nei nomi dei pacchetti Java.

La piattaforma CRX sottostante deve essere in grado di distinguere un carattere di sottolineatura effettivo `_ `e un trattino `-`. Pertanto, in JCR, il trattino deve essere sostituito con il relativo valore unicode (u002d) ed è possibile escape con un trattino basso `_`.

Ad esempio, se il percorso dell’archivio è **/apps/my-example/component/info/Info.java**, il nome del pacchetto deve essere `java package apps.my_002dexample.component.info;`

Si noti che un carattere di sottolineatura deve essere evitato in modo simile, tale che `_` diventa `_005f`.
