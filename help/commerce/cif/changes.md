---
title: Modifiche di rilievo del componente aggiuntivo Commerce Integration Framework (CIF)
description: Modifiche di rilievo del componente aggiuntivo Commerce Integration Framework (CIF) rispetto alle versioni CIF precedenti.
exl-id: 41dee21a-9ae2-4067-a32a-2d4633323fc4
source-git-commit: a2ababa9dd9115e963b91a7271d204d287557c40
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 1%

---

# Modifiche di rilievo apportate al componente aggiuntivo Commerce Integration Framework (CIF){#notable-changes}

In questo documento vengono evidenziate le differenze importanti tra il componente aggiuntivo Commerce Integration Framework (CIF) e le versioni precedenti di CIF, note principalmente come CIF Classic (Quickstart) e CIF Open-source.

## Installazione e aggiornamenti

Il pacchetto del componente aggiuntivo AEM CIF viene installato e aggiornato con Gestione pacchetti AEM.

**Versioni CIF precedenti**

* CIF Classic: non è necessaria alcuna installazione, CIF faceva parte di Quickstart. Gli aggiornamenti CIF facevano parte dei normali aggiornamenti AEM o service pack
* CIF Open-source: installazione tramite GitHub. Gli aggiornamenti facevano parte del lavoro di aggiornamento/manutenzione manuale.

## Configurazione endpoint

L’endpoint viene configurato tramite la console OSGi.

**Versioni CIF precedenti**

* CIF Classic: tramite configurazione OSGi in AEM
* CIF Open-source: tramite browser di configurazione CIF

## Implementazione del progetto CIF Venia

Progetto disponibile il [Guide AEM GitHub - Progetto CIF Venia](https://github.com/adobe/aem-cif-guides-venia) e l’implementazione vengono eseguite tramite Gestione pacchetti AEM.

**Versioni CIF precedenti**

* CIF Classic: tramite installazione pacchetto AEM

## Dati catalogo prodotti

I dati del catalogo dei prodotti vengono richiesti on-demand tramite chiamate in tempo reale a un endpoint esterno che supporta le API GraphQL richieste. Queste API supportano l’accesso a dati live o in staging in qualsiasi data. Nessuna replica necessaria.

**Versioni CIF precedenti**

* CIF Classic: i dati di prodotto live e in staging vengono importati e mantenuti in JCR su AEM Author tramite l’importazione di prodotti completa o delta. I dati dei prodotti live vengono replicati in AEM Publish.

## Esperienze nel catalogo dei prodotti con rendering AEM

L’AEM esegue il rendering istantaneo delle esperienze del catalogo dei prodotti utilizzando i modelli di catalogo AEM assegnati a prodotti e categorie. Nessuna replica necessaria.

**Versioni CIF precedenti**

* CIF Classic: AEM Author crea una pagina AEM per ogni categoria/prodotto utilizzando lo strumento blueprint del catalogo. Queste pagine vengono replicate in AEM Publish.

>[!NOTE]
>
>Per ulteriore documentazione su come utilizzare CIF con AEM Managed Service o AEM On-Premise, consulta [Framework di integrazione Commerce](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)
