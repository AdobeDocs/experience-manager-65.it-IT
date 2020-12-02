---
title: Configurazione dei font di fallback
seo-title: Configurazione dei font di fallback
description: Scoprite come configurare i font di fallback.
seo-description: Scoprite come configurare i font di fallback.
uuid: 2745541c-8c6d-4bb4-aa14-ec19afd6bc35
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d997a268-a40a-462d-badd-94f0731f7ba4
translation-type: tm+mt
source-git-commit: d3719a9ce2fbb066f99445475af8e1f1e7476f4e
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---


# Configurazione dei font di fallback {#configuring-fallback-fonts}

È possibile configurare manualmente il file FontManagerResources.properties per mappare i font AEM modulo predefiniti a fallback (o sostitutivi) se i font predefiniti non sono disponibili sul server. Questo file di proprietà si trova nel file adobe-fontmanager.jar.

>[!NOTE]
>
>La configurazione del font di fallback si applica anche al servizio assembler.

1. Andate al file adobe-livecycle-*`[appserver]`*.ear nella directory *`[aem-forms root]`*/configurationManager/export, create una copia di backup e decomprimete l&#39;originale.
1. Individuate il file adobe-fontmanager.jar e decomprimetelo.
1. Individuare il file FontManagerResources.properties e aprirlo in un editor di testo.
1. Modificate le posizioni e i nomi dei font Generici e Fallback come richiesto e salvate il file.

   Le voci dei font nel file FontManagerResources.properties sono relative alla directory *`[aem-forms root]`*/fonts. Se si specificano font che non sono font AEM modulo predefiniti, è necessario installare tali font all&#39;interno di questa struttura di directory (all&#39;interno di una directory esistente o in una nuova directory creata).

   >[!NOTE]
   >
   >Se il font o il font predefinito specificato non contiene un carattere Unicode specifico o se non è disponibile, il carattere viene tratto da un font di fallback in base alla priorità seguente:

   * Font specifico per le impostazioni internazionali
   * Carattere ROOT se le impostazioni internazionali non sono impostate
   * Font generico, ricercato per ordine impostato nella tabella di fallback

1. Reinserite il pacchetto del file adobe-fontmanager.jar.
1. Reinserite il file adobe-livecycle-*`[appserver]`*.ear e quindi ridistribuitelo manualmente o eseguendo Configuration Manager.

>[!NOTE]
>
>Non utilizzare Configuration Manager per creare nuovamente il pacchetto del file adobe-livecycle-`[appserver]`.ear perché le modifiche apportate verranno sovrascritte con i valori predefiniti dei moduli AEM.

