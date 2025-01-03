---
title: Ricerca di istanze di processo
description: Utilizzare la pagina Ricerca processo per inserire i criteri di ricerca per trovare un'istanza di processo.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 35f9acbf-7a82-43b1-9e17-9be4de666212
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 0%

---

# Ricerca di istanze di processo{#searching-for-process-instances}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Utilizzare la pagina Ricerca processo per inserire i criteri di ricerca per trovare un&#39;istanza di processo. È possibile accedere alla pagina Ricerca processo dalla pagina Flusso di lavoro moduli oppure facendo clic su Cerca nella pagina Istanza processo.

È possibile inserire i criteri di base per eseguire una ricerca generale, attributi specifici per eseguire una ricerca dettagliata oppure una combinazione di criteri di base e attributi specifici per eseguire una ricerca combinata.

## Eseguire una ricerca generale {#perform-a-general-search}

Una ricerca generale di un processo è più appropriata se si conosce l&#39;ID processo dell&#39;istanza del processo, se si cerca un gruppo di istanze di processo correlate o se sono in esecuzione solo alcune istanze di processo.

Immettere i criteri di base per eseguire una ricerca generale. Se si immettono più criteri, la ricerca viene eseguita con una condizione AND implicita.

1. Nella console di amministrazione, fai clic su Servizi > Flusso di lavoro di Forms > Ricerca processi.
1. Nella sezione Ricerca generale della pagina Ricerca processo specificare i criteri riportati di seguito.

   * **ID processo:** Il numero intero positivo che identifica ogni istanza di processo univoca.
   * **Stato processo:** Selezionare uno stato dall&#39;elenco.
   * **Applicazione:** Selezionare un&#39;applicazione dall&#39;elenco. Vengono visualizzate solo le applicazioni distribuite.
   * **Nome processo - Versione:** Selezionare un nome di processo dal menu. Vengono visualizzati solo i processi distribuiti.

1. Fai clic su Cerca. Viene visualizzata la pagina Istanza processo, in cui sono elencate le istanze trovate.

## Eseguire una ricerca dettagliata di un processo {#perform-a-detailed-search-for-a-process}

È possibile immettere attributi specifici per eseguire una ricerca dettagliata. Una ricerca dettagliata è più appropriata se sono in esecuzione molte istanze di processo e devi restringere i possibili risultati in base a determinati criteri.

1. Nella console di amministrazione, fai clic su Servizi > Flusso di lavoro di Forms > Ricerca processi.
1. Nella pagina Ricerca processo, in Ricerca dettagliata, specifica il primo set di criteri:

   * Nell&#39;elenco Attributo selezionare un attributo.
   * Nell&#39;elenco Filtro selezionare un operatore.
   * Nella casella Valore digitare un valore appropriato per l&#39;attributo selezionato.

1. Per aggiungere un’altra riga, seleziona Altri filtri. Viene visualizzato un altro insieme di elenchi Attributo, Filtro e Valore e un elenco Condizione.
1. In Condizione, seleziona AND o OR. Ripetere i passaggi da 1 a 3 per limitare ulteriormente la ricerca.
1. Per aggiungere o rimuovere righe, fare clic su Altri filtri o su Meno filtri. Puoi avere da una a quattro righe.
1. Fai clic su Cerca. Viene visualizzata la pagina Istanza processo, in cui sono elencate le istanze trovate.

[Informazioni sugli stati delle istanze di processo](/help/forms/using/admin-help/processes.md#about-process-instance-statuses)

## Eseguire una ricerca combinata di un processo {#perform-a-combined-search-for-a-process}

Per creare una ricerca basata sia su una ricerca generale che su una ricerca dettagliata, con un AND implicito tra le aree, immettere i criteri di ricerca nelle aree Ricerca generale e Ricerca dettagliata nella pagina Ricerca processo.

Se la ricerca è troppo limitata, non verrà trovata alcuna istanza.
