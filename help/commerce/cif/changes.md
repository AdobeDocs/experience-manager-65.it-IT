---
title: Modifiche di rilievo apportate al componente aggiuntivo Commerce integration framework (CIF)
description: Modifiche di rilievo del componente aggiuntivo Commerce integration framework (CIF) rispetto alle versioni precedenti dell’CIF.
exl-id: 41dee21a-9ae2-4067-a32a-2d4633323fc4
solution: Experience Manager,Commerce
source-git-commit: 1751bfb32386685e3a159939113b9667b5e17f0e
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# Modifiche di rilievo apportate al componente aggiuntivo Commerce integration framework (CIF){#notable-changes}

Questo documento evidenzia le importanti differenze tra il componente aggiuntivo Commerce integration framework (CIF) e le versioni precedenti dell’CIF, principalmente note come CIF Classic (Quickstart) e CIF Open-source.

## Installazione e aggiornamenti

Il pacchetto del componente aggiuntivo AEM CIF viene installato e aggiornato con Gestione pacchetti AEM.

**Versioni precedenti dell’CIF**

* CIF Classic: nessuna installazione necessaria, CIF faceva parte di Quickstart. Gli aggiornamenti CIF facevano parte degli aggiornamenti regolari dell’AEM o dei service pack
* CIF Open-source: installazione tramite GitHub. Gli aggiornamenti facevano parte del lavoro di aggiornamento/manutenzione manuale.

## Configurazione endpoint

L’endpoint viene configurato tramite la console OSGi.

**Versioni precedenti dell’CIF**

* CIF Classic: tramite configurazione OSGi nell’AEM
* CIF open-source: tramite il browser configurazioni CIF

## Implementazione del progetto CIF Venia

Progetto disponibile il [Guide AEM GitHub - Progetto CIF Venia](https://github.com/adobe/aem-cif-guides-venia) e l’implementazione vengono eseguite tramite Gestione pacchetti AEM.

**Versioni precedenti dell’CIF**

* CIF Classic: tramite installazione pacchetto AEM

## Dati catalogo prodotti

I dati del catalogo dei prodotti vengono richiesti on-demand tramite chiamate in tempo reale a un endpoint esterno che supporta le API GraphQL richieste. Queste API supportano l’accesso a dati live o in staging in qualsiasi data. Nessuna replica necessaria.

**Versioni precedenti dell’CIF**

* CIF Classic: i dati di prodotto live e in staging vengono importati e mantenuti in JCR su AEM Author tramite l’importazione di prodotti completa o delta. I dati dei prodotti live vengono replicati in AEM Publish.

## Esperienze nel catalogo dei prodotti con rendering AEM

L’AEM esegue il rendering istantaneo delle esperienze del catalogo dei prodotti utilizzando i modelli di catalogo AEM assegnati a prodotti e categorie. Nessuna replica necessaria.

**Versioni precedenti dell’CIF**

* CIF Classic: l’autore AEM crea una pagina AEM per ogni categoria/prodotto utilizzando lo strumento blueprint del catalogo. Queste pagine vengono replicate in AEM Publish.

>[!NOTE]
>
>Per ulteriore documentazione su come utilizzare l’CIF con il Managed Service dell’AEM o con l’AEM on-premise, consulta [Commerce integration framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)
