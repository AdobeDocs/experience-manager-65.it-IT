---
title: Modifiche di rilievo del componente aggiuntivo Commerce Integration Framework (CIF)
description: Modifiche di rilievo del componente aggiuntivo Commerce Integration Framework (CIF) rispetto alle versioni CIF precedenti.
exl-id: 5a526960-96a1-421e-9fb0-0825e7df8f32,c136763f-56aa-450e-8796-bc84bf6c205d
translation-type: tm+mt
source-git-commit: a8dba82029168660b84b085ab46d0406b19961ef
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 1%

---

# Modifiche di rilievo apportate al componente aggiuntivo Commerce Integration Framework (CIF){#notable-changes}

Questo documento evidenzia le importanti differenze tra il componente aggiuntivo Commerce Integration Framework (CIF) e le vecchie versioni CIF, note principalmente come CIF Classic (Quickstart) e CIF Open-source.

## Installazione e aggiornamenti

Il pacchetto aggiuntivo CIF AEM viene installato e aggiornato con AEM gestore di pacchetti.

**Versioni CIF precedenti**

* CIF Classic: Non è necessaria alcuna installazione, CIF faceva parte di Quickstart. Gli aggiornamenti CIF facevano parte degli aggiornamenti AEM o service pack regolari
* CIF Open source: Installazione tramite GitHub. Gli aggiornamenti facevano parte del lavoro di aggiornamento/manutenzione manuale.

## Configurazione endpoint

L’endpoint viene configurato tramite la console OSGi.

**Versioni CIF precedenti**

* CIF Classic: Configurazione tramite OSGi in AEM
* CIF Open source: Browser di configurazione CIF

## Implementazione del progetto CIF Venia

Progetto disponibile su [Guide AEM GitHub - CIF Venia Project](https://github.com/adobe/aem-cif-guides-venia) e distribuzione eseguita tramite package AEM manager

**Versioni CIF precedenti**

* CIF Classic: Tramite installazione del pacchetto AEM

## Dati catalogo prodotti

I dati del catalogo dei prodotti vengono richiesti on-demand tramite chiamate in tempo reale a un endpoint esterno che supporta le API GraphQL richieste. Queste API supportano l’accesso a dati live o in staging in qualsiasi data. Nessuna replica necessaria.

**Versioni CIF precedenti**

* CIF Classic: I dati dei prodotti live e in staging vengono importati e mantenuti in JCR su AEM Author tramite l’importazione completa o delta del prodotto. I dati dei prodotti live vengono replicati in AEM Publish.

## Esperienze del catalogo dei prodotti con rendering AEM

AEM esegue il rendering immediato delle esperienze di catalogo di prodotti utilizzando AEM modelli di catalogo assegnati a prodotti e categorie. Nessuna replica necessaria.

**Versioni CIF precedenti**

* CIF Classic: AEM Author crea una pagina AEM per ogni categoria/prodotto utilizzando lo strumento di blueprint del catalogo. Queste pagine vengono replicate in AEM Publish.

>[!NOTE]
>
>Per ulteriore documentazione su come utilizzare CIF con AEM Managed Service o AEM on-premise, consulta [Commerce Integration Framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)
