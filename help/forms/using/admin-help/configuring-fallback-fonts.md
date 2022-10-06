---
title: Configurazione dei font di fallback
seo-title: Configuring fallback fonts
description: Scopri come configurare i font di fallback.
seo-description: Learn how to configure fallback fonts.
uuid: 2745541c-8c6d-4bb4-aa14-ec19afd6bc35
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d997a268-a40a-462d-badd-94f0731f7ba4
feature: PDF Generator
exl-id: 76dd2b0c-9f16-47bf-a565-99277be750fb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---

# Configurazione dei font di fallback {#configuring-fallback-fonts}

È possibile configurare manualmente il file FontManagerResources.properties per mappare i font predefiniti dei moduli AEM a fallback (o sostituzione) se i font predefiniti non sono disponibili sul server. Questo file di proprietà si trova nel file adobe-fontmanager.jar .

>[!NOTE]
>
>La configurazione dei font di fallback si applica anche al servizio assembler.

1. Passa a adobe-livecycle-*`[appserver]`* file .ear nel *`[aem-forms root]`*/configurationManager/export directory, crea una copia di backup e scompone l&#39;originale.
1. Individua il file adobe-fontmanager.jar e decrea il pacchetto.
1. Individua il file FontManagerResources.properties e aprilo in un editor di testo.
1. Modifica le posizioni e i nomi dei font Generico e Fallback come richiesto e salva il file.

   Le voci di font nel file FontManagerResources.properties sono relative al *`[aem-forms root]`*/fonts directory. Se si specificano font che non sono predefiniti AEM font dei moduli, è necessario installarli all’interno di questa struttura di directory (all’interno di una directory esistente o in una directory appena creata).

   >[!NOTE]
   >
   >Se il font o il font predefinito specificato non contiene un carattere unicode specifico o se non è disponibile, il carattere viene tratto da un font di fallback in base alla seguente priorità:

   * Font specifico per le impostazioni internazionali
   * Font ROOT se le impostazioni internazionali non sono impostate
   * Font generico, ricercato per ordine impostato nella tabella di fallback

1. Ricomprimi il file adobe-fontmanager.jar.
1. Ricompila il pacchetto adobe-livecycle-*`[appserver]`*.ear e quindi ridistribuirlo manualmente o eseguendo Configuration Manager.

>[!NOTE]
>
>Non utilizzare Configuration Manager per creare un nuovo pacchetto di adobe-livecycle-`[appserver]`file .ear perché le modifiche verranno sovrascritte con i valori predefiniti dei moduli AEM.
