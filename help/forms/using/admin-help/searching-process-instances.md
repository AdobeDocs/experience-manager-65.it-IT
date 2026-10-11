---
title: Ricerca di istanze di processo
description: Utilizza la pagina Ricerca dei processi per inserire i criteri di ricerca e identificare un’istanza di processo.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 35f9acbf-7a82-43b1-9e17-9be4de666212
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 100%
---
# Ricerca di istanze di processo{#searching-for-process-instances}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Utilizza la pagina Ricerca dei processi per inserire i criteri di ricerca e identificare un’istanza di processo. Puoi accedere alla pagina Ricerca dei processi dalla pagina Flusso di lavoro di Forms oppure facendo clic su Cerca nella pagina Istanza di processo.

Puoi inserire i criteri di base per eseguire una ricerca generale, attributi specifici per eseguire una ricerca dettagliata oppure una combinazione di criteri di base e attributi specifici per eseguire una ricerca combinata.

## Eseguire una ricerca generale {#perform-a-general-search}

Una ricerca generale di un processo è più appropriata se conosci l’ID processo dell’istanza del processo, se cerchi un gruppo di istanze di processo correlate o se sono in esecuzione solo alcune istanze di processo.

Immetti i criteri di base per eseguire una ricerca generale. Se immetti più criteri, la ricerca viene eseguita con una condizione AND implicita.

1. Nella console di amministrazione, fai clic su Servizi > Flusso di lavoro di Forms > Ricerca dei processi.
1. Nella pagina Ricerca dei processi, in Ricerca generale, specifica i criteri riportati di seguito:

   * **ID processo:** il numero intero positivo che identifica ogni istanza di processo univoca.
   * **Stato processo:** seleziona uno stato dall’elenco.
   * **Applicazione:** seleziona un’applicazione dall’elenco. Vengono visualizzate solo le applicazioni distribuite.
   * **Nome processo - Versione:** seleziona un nome di processo dal menu. Vengono visualizzati solo i processi distribuiti.

1. Fai clic su Ricerca. Viene visualizzata la pagina Istanza del processo, in cui sono elencate le istanze trovate.

## Eseguire una ricerca dettagliata di un processo {#perform-a-detailed-search-for-a-process}

Puoi immettere attributi specifici per eseguire una ricerca dettagliata. Una ricerca dettagliata è più appropriata se sono in esecuzione molte istanze di processo e devi restringere i possibili risultati in base a determinati criteri.

1. Nella console di amministrazione, fai clic su Servizi > Flusso di lavoro di Forms > Ricerca dei processi.
1. Nella pagina Ricerca dei processi, in Ricerca dettagliata, specifica il primo set di criteri:

   * Nell’elenco Attributo, seleziona un attributo.
   * Nell’elenco Filtro, seleziona un operatore.
   * Nella casella Valore, digita un valore appropriato per l’attributo selezionato.

1. Per aggiungere un’altra riga, seleziona Altri filtri. Viene visualizzato un altro insieme di elenchi Attributo, Filtro e Valore e un elenco Condizione.
1. In Condizione, seleziona AND oppure OR. Ripeti i passaggi da 1 a 3, se necessario, per limitare ulteriormente la ricerca.
1. Per aggiungere o rimuovere righe, fai clic su Altri filtri o su Meno filtri. Puoi avere da una a quattro righe.
1. Fai clic su Ricerca. Viene visualizzata la pagina Istanza del processo, in cui sono elencate le istanze trovate.

[Informazioni sugli stati delle istanze di processo](/help/forms/using/admin-help/processes.md#about-process-instance-statuses)

## Eseguire una ricerca combinata di un processo {#perform-a-combined-search-for-a-process}

Per creare una ricerca basata sia su una ricerca generale sia su una ricerca dettagliata, con un AND implicito tra le aree, immetti i criteri di ricerca sia nelle aree Ricerca generale e sia in quelle Ricerca dettagliata nella pagina Ricerca dei processi.

Se la ricerca è troppo limitata, non verrà trovata alcuna istanza.
