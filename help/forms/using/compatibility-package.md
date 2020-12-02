---
title: Pacchetto di compatibilità
seo-title: Pacchetto di compatibilità
description: L'installazione del pacchetto Compatibilità su  AEM Forms 6.5 consente di utilizzare le risorse Gestione corrispondenza di  AEM Forms 6.4 e versioni precedenti e modelli e pagine di moduli adattivi obsoleti
seo-description: L'installazione del pacchetto di compatibilità su  AEM Forms 6.4 consente di utilizzare le risorse Gestione corrispondenza da  AEM Forms 6.4 e da pagine e modelli di moduli adattivi obsoleti
uuid: b49633d6-2cb3-422c-a314-25f3b8a37b7f
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management, installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: 73e8ccc6-f857-493e-b6e3-878f93e2a356
docset: aem65
translation-type: tm+mt
source-git-commit: a929252a13f66da8ac3e52aea0655b12bdd1425f
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 6%

---


# Pacchetto compatibilità{#compatibility-package}

## Panoramica {#overview}

La comunicazione interattiva è l&#39;approccio predefinito e consigliato per creare comunicazioni con i clienti in  AEM Forms 6.5. Per continuare a utilizzare le lettere in  AEM Forms 6.5, è necessario installare l&#39;ultimo [pacchetto di compatibilità AEMFD](https://helpx.adobe.com/it/aem-forms/kb/aem-forms-releases.html).

Il pacchetto di compatibilità AEMFD consente inoltre di [utilizzare le risorse seguenti da  AEM Forms 6.4, 6.3 e 6.2 su  AEM Forms 6.5:](../../forms/using/compatibility-package.md#add-support-for-aem-forms-and-assets-in-aem-forms)

* Frammenti di documenti
* Lettere
* Dizionari dati
* Moduli adattivi modelli e pagine obsoleti

Per ulteriori informazioni, consultate [Risorse rese compatibili con  AEM Forms 6.5 installando il pacchetto di compatibilità](../../forms/using/compatibility-package.md#assetsmadecompatible).

## Supporto  risorse AEM Forms 6.4, 6.3 e 6.2 in  AEM Forms 6.5 {#add-support-for-aem-forms-and-assets-in-aem-forms}

Dopo aver effettuato l’aggiornamento, effettuate le seguenti operazioni per installare il pacchetto di compatibilità AEMFD e rendere le risorse compatibili con la versione 6.5:

Assicurarsi di avere [AEM pacchetto di compatibilità](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) pre-installato.

1. Installate la versione più recente del pacchetto di compatibilità [6.5](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html).

   Per ulteriori informazioni sul caricamento e l&#39;installazione del pacchetto, consultate [Come lavorare con i pacchetti](/help/sites-administering/package-manager.md).

1. Dopo aver stabilizzato i registri, riavviate il server.
1. Utilizzate l’utility di migrazione per rendere le risorse compatibili con la versione 6.5.

   Per ulteriori informazioni, vedere [utility di migrazione](../../forms/using/migration-utility.md).

## Risorse rese compatibili con  AEM Forms 6.5 installando il pacchetto di compatibilità {#assetsmadecompatible}

Installando il pacchetto Compatibilità, potete rendere le risorse e i modelli seguenti compatibili con  AEM Forms 6.5:

* Risorse per la gestione della corrispondenza dal AEM 6.4 e versioni precedenti:

   * [Lettere](../../forms/using/create-letter.md)
   * [Dizionari dati](/help/forms/using/data-dictionary.md)
   * Frammenti del documento

* Modelli per moduli adattivi obsoleti:

   * /libs/fd/af/templates/blankTemplate2
   * /libs/fd/af/templates/simpleEnrollmentTemplate
   * /libs/fd/af/templates/simpleEnrollmentTemplate2
   * /libs/fd/af/templates/surveyTemplate
   * /libs/fd/af/templates/surveyTemplate2
   * /libs/fd/af/templates/taccollEnrollmentTemplate
   * /libs/fd/af/templates/taccollEnrollmentTemplate2
   * /libs/fd/afaddon/templates/advancedEnrollmentTemplate
   * /libs/fd/afaddon/templates/advancedEnrollmentTemplate2

* Moduli adattivi: pagine obsolete:

   * /libs/fd/af/components/page/survey
   * /libs/fd/af/components/page/tabbedenrollment
   * /libs/fd/afaddon/components/page/advancedenrollment

