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

È possibile configurare manualmente il file FontManagerResources.properties per associare i tipi di carattere predefiniti di AEM forms al fallback (o alla sostituzione) se i tipi di carattere predefiniti non sono disponibili sul server. Questo file di proprietà si trova nel file adobe-fontmanager.jar.

>[!NOTE]
>
>La configurazione del font di fallback si applica anche al servizio Assembler.

1. Passa ad adobe-livecycle-*`[appserver]`* file .ear nella *`[aem-forms root]`*/configurationManager/export, creare una copia di backup e rimuovere il pacchetto originale.
1. Individua il file adobe-fontmanager.jar e decomprimi il file.
1. Individuare il file FontManagerResources.properties e aprirlo in un editor di testo.
1. Modificate le posizioni e i nomi dei caratteri generici e di fallback in base alle esigenze, quindi salvate il file.

   Le voci relative ai tipi di carattere nel file FontManagerResources.properties sono relative al *`[aem-forms root]`* directory /fonts. Se si specificano tipi di carattere diversi da quelli predefiniti per i moduli AEM, è necessario installare tali tipi di carattere all&#39;interno di questa struttura di directory (all&#39;interno di una directory esistente o in una directory appena creata).

   >[!NOTE]
   >
   >Se il tipo di carattere specificato o il tipo di carattere predefinito non contiene un carattere Unicode specifico o non è disponibile, il carattere viene preso da un tipo di carattere di fallback in base alla seguente priorità:

   * Font specifico per le impostazioni internazionali
   * Font ROOT se non è impostata la lingua
   * Font generico, ricerca per set di ordini nella tabella di fallback

1. Riconfeziona il file adobe-fontmanager.jar.
1. Riconfezionare il ciclo di vita di Adobe *`[appserver]`* file .ear e quindi distribuirlo manualmente o eseguendo Configuration Manager.

>[!NOTE]
>
>Non utilizzare Configuration Manager per creare un nuovo pacchetto di adobe-livecycle-`[appserver]`file .ear perché sovrascriverà le modifiche con i valori predefiniti di AEM forms.
