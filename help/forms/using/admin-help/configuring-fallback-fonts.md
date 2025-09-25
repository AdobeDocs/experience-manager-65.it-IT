---
title: Configurazione dei font di fallback
description: Scopri come configurare i font di fallback per AEM Forms. Puoi utilizzare il file FontManagerResources.properties per associare manualmente i tipi di font predefiniti ai tipi di font di fallback.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
exl-id: 76dd2b0c-9f16-47bf-a565-99277be750fb
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '264'
ht-degree: 100%

---

# Configurazione dei font di fallback {#configuring-fallback-fonts}

Puoi configurare manualmente il file FontManagerResources.properties per associare i tipi di font predefiniti di AEM Forms al fallback (o alla sostituzione) se i tipi di font predefiniti non sono disponibili sul server. Questo file di proprietà si trova nel file adobe-fontmanager.jar.

>[!NOTE]
>
>La configurazione del font di fallback si applica anche al servizio Assembler.

1. Passa al file adobe-livecycle-*`[appserver]`*.ear nella directory *`[aem-forms root]`*/configurationManager/export, crea una copia di backup e decomprimi il pacchetto originale.
1. Individua il file adobe-fontmanager.jar e decomprimi il file.
1. Individua il file FontManagerResources.properties e aprilo in un editor di testo.
1. Modifica le posizioni e i nomi dei font generici e di fallback in base alle esigenze, quindi salva il file.

   Le voci dei font nel file FontManagerResources.properties sono relative alla directory *`[aem-forms root]`*/font. Se specifichi i font diversi da quelli predefiniti di AEM Forms, devi installare tali tipi di font all’interno di questa struttura di directory (all’interno di una directory esistente o di una directory nuova).

   >[!NOTE]
   >
   >Se il font specificato o quello predefinito non contiene un carattere Unicode specifico o non è disponibile, il carattere viene preso da un font di fallback in base alla seguente priorità:

   * Font specifico per lingua
   * Font principale se non è impostata la lingua
   * Font generico, ricerca per set di ordini nella tabella di fallback

1. Ricomprimi il file adobe-fontmanager.jar.
1. Ricomprimi il file adobe-livecycle-*`[appserver]`*.ear e quindi ridistribuiscilo manualmente o eseguendo Configuration Manager.

>[!NOTE]
>
>Non utilizzare Configuration Manager per comprimere nuovamente il pacchetto del file adobe-livecycle-`[appserver]`.ear perché sovrascriverà le modifiche con i valori predefiniti di AEM Forms.
