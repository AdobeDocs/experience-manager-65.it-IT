---
title: Pacchetto di compatibilità
seo-title: Compatibility Package
description: L’installazione del pacchetto di compatibilità su AEM Forms 6.5 consente di utilizzare le risorse Gestione Corrispondenza di AEM Forms 6.4 e versioni precedenti e i modelli e le pagine dei moduli adattivi obsoleti
seo-description: Installing the Compatibility package on AEM Forms 6.4 allows you to use the Correspondence Management assets from AEM Forms 6.4 and deprecated adaptive forms templates and pages
uuid: b49633d6-2cb3-422c-a314-25f3b8a37b7f
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management, installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: 73e8ccc6-f857-493e-b6e3-878f93e2a356
docset: aem65
role: Admin
exl-id: bb16017c-a1bf-40d8-a78d-827c05b7ee2e
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 6%

---

# Pacchetto di compatibilità{#compatibility-package}

## Panoramica {#overview}

La comunicazione interattiva è l’approccio predefinito e consigliato per creare comunicazioni con i clienti in AEM Forms 6.5. Per continuare a utilizzare le lettere in AEM Forms 6.5, è necessario installare l’ultima versione [Pacchetto di compatibilità AEMFD](https://helpx.adobe.com/it/aem-forms/kb/aem-forms-releases.html).

Il pacchetto di compatibilità AEMFD consente inoltre di: [utilizza le seguenti risorse da AEM Forms 6.4, 6.3 e 6.2 su AEM Forms 6.5:](../../forms/using/compatibility-package.md#add-support-for-aem-forms-and-assets-in-aem-forms)

* Frammenti di documento
* Lettere
* Dizionari dati
* Modelli e pagine obsolete per i moduli adattivi

Per ulteriori informazioni, consulta [Risorse rese compatibili con AEM Forms 6.5 installando il pacchetto di compatibilità](../../forms/using/compatibility-package.md#assetsmadecompatible).

## Supporto per risorse AEM Forms 6.4, 6.3 e 6.2 in AEM Forms 6.5 {#add-support-for-aem-forms-and-assets-in-aem-forms}

Dopo aver eseguito un aggiornamento, procedi come segue per installare il pacchetto di compatibilità AEMFD e rendere le risorse compatibili con la versione 6.5:

Assicurati di avere [Pacchetto di compatibilità AEM](https://helpx.adobe.com/it/aem-forms/kb/aem-forms-releases.html) preinstallato.

1. Installa l&#39;ultima versione 6.5 [Pacchetto di compatibilità](https://helpx.adobe.com/it/aem-forms/kb/aem-forms-releases.html).

   Per ulteriori informazioni sul caricamento e l’installazione del pacchetto, vedi [Come lavorare con i pacchetti](/help/sites-administering/package-manager.md).

1. Dopo aver stabilizzato i registri, riavvia il server.
1. Utilizza l’utility di migrazione per rendere le risorse compatibili con la versione 6.5.

   Per ulteriori informazioni, consulta [utility di migrazione](../../forms/using/migration-utility.md).

## Risorse rese compatibili con AEM Forms 6.5 installando il pacchetto di compatibilità {#assetsmadecompatible}

Installando il pacchetto di compatibilità, puoi rendere compatibili con AEM Forms 6.5 le risorse e i modelli seguenti:

* Attività di gestione della corrispondenza dal AEM 6.4 e precedenti:

   * [Lettere](../../forms/using/create-letter.md)
   * [Dizionari dati](/help/forms/using/data-dictionary.md)
   * Frammenti del documento

* Modelli obsoleti per moduli adattivi:

   * /libs/fd/af/templates/blankTemplate2
   * /libs/fd/af/templates/simpleEnrollmentTemplate
   * /libs/fd/af/templates/simpleEnrollmentTemplate2
   * /libs/fd/af/templates/surveyTemplate
   * /libs/fd/af/templates/surveyTemplate2
   * /libs/fd/af/templates/ttabsEnrollmentTemplate
   * /libs/fd/af/templates/taggedEnrollmentTemplate2
   * /libs/fd/afaddon/templates/advancedEnrollmentTemplate
   * /libs/fd/afaddon/templates/advancedEnrollmentTemplate2

* Pagine obsolete dei moduli adattivi:

   * /libs/fd/af/components/page/survey
   * /libs/fd/af/components/page/tabbedenregistrazione
   * /libs/fd/afaddon/components/page/advancedensubscription
