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
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: b26425d0-6fde-5e02-bfd6-e560e2fa86c9
    internal-label: PDF Generator
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '271'
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
