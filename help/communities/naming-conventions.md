---
title: Convenzioni di denominazione
seo-title: Convenzioni di denominazione
description: Trattini nel nome del pacchetto Java
seo-description: Trattini nel nome del pacchetto Java
uuid: 48086e6c-c35b-4ffc-b216-d01feca7bf9a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 5271feb9-70c6-4c82-8ac7-34a63d80e3aa
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Naming Conventions {#naming-conventions}

## Trattini nel nome del pacchetto Java {#hyphens-in-java-package-name}

Quando create un percorso per una classe Java, tenete presente che il nome del pacchetto deve corrispondere a quello del percorso della cartella dell&#39;archivio, con eventuali trattini inclusi nel percorso con la corretta escape.

Anche se l&#39;uso dei trattini nei nomi degli elementi del repository è una pratica consigliata nello sviluppo di AEM, i trattini non sono consentiti nei nomi dei pacchetti Java.

La piattaforma CRX sottostante deve essere in grado di distinguere tra un carattere di sottolineatura effettivo &#39;_&#39; e un trattino &#39;-&#39;. Pertanto, in JCR, il trattino deve essere sostituito con il suo valore unicode (u002d) ed eseguito con escape con un carattere di sottolineatura &#39;_&#39;.

Ad esempio, se il percorso del repository è **/apps/my-example/component/info/Info.java**, il nome del pacchetto deve essere `java package apps.my_002dexample.component.info;`

Tenere presente che un carattere di sottolineatura deve essere anch&#39;esso evitato, in modo che `_` diventi `_005f`.
