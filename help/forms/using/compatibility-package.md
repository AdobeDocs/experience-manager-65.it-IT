---
title: Pacchetto di compatibilità
description: L’installazione del pacchetto di compatibilità su AEM Forms 6.5 consente di utilizzare le risorse di Gestione della corrispondenza di AEM Forms 6.4 e versioni precedenti e i modelli e le pagine obsoleti dei moduli adattivi
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management, installing
geptopics: SG_AEMFORMS/categories/jee
docset: aem65
role: Admin
exl-id: bb16017c-a1bf-40d8-a78d-827c05b7ee2e
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 2%

---

# Pacchetto di compatibilità{#compatibility-package}

## Panoramica {#overview}

La comunicazione interattiva è l’approccio predefinito e consigliato per creare comunicazioni con i clienti in AEM Forms 6.5. Per continuare a utilizzare le lettere in AEM Forms 6.5, devi installare la più recente [Pacchetto di compatibilità per AEMFD](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html).

Il pacchetto di compatibilità AEMFD consente inoltre di: [utilizza le seguenti risorse di AEM Forms 6.4, 6.3 e 6.2 in AEM Forms 6.5:](../../forms/using/compatibility-package.md#add-support-for-aem-forms-and-assets-in-aem-forms)

* Frammenti di documenti
* Lettere
* Dizionari dati
* Moduli adattivi: modelli e pagine obsoleti

Per ulteriori informazioni, consulta [Risorse rese compatibili con AEM Forms 6.5 installando il pacchetto Compatibilità](../../forms/using/compatibility-package.md#assetsmadecompatible).

## Aggiunta del supporto per risorse AEM Forms 6.4, 6.3 e 6.2 in AEM Forms 6.5 {#add-support-for-aem-forms-and-assets-in-aem-forms}

Dopo aver eseguito un aggiornamento, effettua le seguenti operazioni per installare il pacchetto di compatibilità AEMFD e rendere le risorse compatibili con la versione 6.5:

Assicurati di avere [Pacchetto di compatibilità AEM](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) pre-installato.

1. Installare la versione 6.5 più recente [Pacchetto di compatibilità](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html).

   Per ulteriori informazioni sul caricamento e l’installazione del pacchetto, consulta [Come lavorare con i pacchetti](/help/sites-administering/package-manager.md).

1. Una volta stabilizzati i registri, riavviare il server.
1. Utilizza l’utility di migrazione per rendere le risorse compatibili con la versione 6.5.

   Per ulteriori informazioni, consulta [utilità di migrazione](../../forms/using/migration-utility.md).

## Risorse rese compatibili con AEM Forms 6.5 installando il pacchetto Compatibilità {#assetsmadecompatible}

Installando il pacchetto di compatibilità, puoi rendere compatibili con AEM Forms 6.5 le risorse e i modelli seguenti:

* Risorse di gestione della corrispondenza dell’AEM 6.4 e versioni precedenti:

   * [Lettere](../../forms/using/create-letter.md)
   * [Dizionari dati](/help/forms/using/data-dictionary.md)
   * Frammenti del documento

* Modelli obsoleti per moduli adattivi:

   * /libs/fd/af/templates/blankTemplate2
   * /libs/fd/af/templates/simpleEnrollmentTemplate
   * /libs/fd/af/templates/simpleEnrollmentTemplate2
   * /libs/fd/af/templates/surveyTemplate
   * /libs/fd/af/templates/surveyTemplate2
   * /libs/fd/af/templates/tabbedEnrollmentTemplate
   * /libs/fd/af/templates/tabbedEnrollmentTemplate2
   * /libs/fd/afaddon/templates/advancedEnrollmentTemplate
   * /libs/fd/afaddon/templates/advancedEnrollmentTemplate2

* Pagine obsolete dei moduli adattivi:

   * /libs/fd/af/components/page/survey
   * /libs/fd/af/components/page/tabbedenrollment
   * /libs/fd/afaddon/components/page/advancedenrollment
