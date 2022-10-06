---
title: Ricerca di istanze del processo
seo-title: Searching for process instances
description: Utilizzare la pagina Ricerca processi per immettere i criteri di ricerca per trovare un'istanza di processo.
seo-description: Use the Process Search page to enter search criteria for finding a process instance.
uuid: 4a9c5b05-add5-4278-9c6f-d1928b6860d2
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 88b634bb-8f6c-4830-ad01-821668609615
exl-id: 35f9acbf-7a82-43b1-9e17-9be4de666212
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# Ricerca di istanze del processo{#searching-for-process-instances}

Utilizzare la pagina Ricerca processi per immettere i criteri di ricerca per trovare un&#39;istanza di processo. È possibile accedere alla pagina di ricerca del processo dalla pagina del flusso di lavoro dei moduli o facendo clic su Cerca nella pagina Istanza del processo.

È possibile immettere criteri di base per eseguire una ricerca generale, attributi specifici per eseguire una ricerca dettagliata o una combinazione di criteri di base e attributi specifici per eseguire una ricerca combinata.

## Eseguire una ricerca generale {#perform-a-general-search}

La ricerca generale di un processo è più appropriata se si conosce l&#39;ID del processo dell&#39;istanza di processo, se si cerca un gruppo di istanze di processo correlate o se sono in esecuzione solo poche istanze di processo.

Immettere i criteri di base per eseguire una ricerca generale. Se si immettono più criteri, la ricerca viene eseguita con una condizione AND implicita.

1. Nella console di amministrazione, fai clic su Servizi > Flusso di lavoro Forms > Ricerca processi.
1. Nella sezione Ricerca generale della pagina Ricerca processi specificare i seguenti criteri:

   * **ID processo:** Numero intero positivo che identifica ogni istanza di processo univoca.
   * **Stato del processo:** Selezionare uno stato dall’elenco.
   * **Applicazione:** Seleziona un&#39;applicazione dall&#39;elenco. Vengono visualizzate solo le applicazioni distribuite.
   * **Nome processo - Versione:** Selezionare un nome di processo dal menu. Vengono visualizzati solo i processi distribuiti.

1. Fare clic su Cerca. Viene visualizzata la pagina Istanza del processo, in cui sono elencate le istanze trovate.

## Eseguire una ricerca dettagliata di un processo {#perform-a-detailed-search-for-a-process}

È possibile immettere attributi specifici per eseguire una ricerca dettagliata. Una ricerca dettagliata è più appropriata se sono in esecuzione molte istanze di processo e devi limitare le possibili ricerche in base a determinati criteri.

1. Nella console di amministrazione, fai clic su Servizi > Flusso di lavoro Forms > Ricerca processi.
1. Nella pagina Ricerca processo , in Ricerca dettagliata , specifica il primo set di criteri:

   * Nell&#39;elenco Attributi, selezionare un attributo.
   * Nell’elenco Filtro, selezionare un operatore.
   * Nella casella Valore digitare un valore appropriato per l&#39;attributo selezionato.

1. Per aggiungere un’altra riga, seleziona Altri filtri. Viene visualizzato un altro set di elenchi di attributi, filtri e valori, nonché un elenco Condizione.
1. In Condizione, selezionare AND o OR. Ripetere i passaggi da 1 a 3 per restringere ulteriormente la ricerca.
1. Per aggiungere o rimuovere righe, fare clic su Altri filtri o Meno filtri. Puoi avere da una a quattro righe.
1. Fare clic su Cerca. Viene visualizzata la pagina Istanza del processo, in cui sono elencate le istanze trovate.

[Informazioni sugli stati delle istanze del processo](/help/forms/using/admin-help/processes.md#about-process-instance-statuses)

## Eseguire una ricerca combinata di un processo {#perform-a-combined-search-for-a-process}

Per creare una ricerca basata sia su una ricerca generale che su una ricerca dettagliata, con un AND implicito tra le aree, immettere i criteri di ricerca sia nelle aree Ricerca generale che Ricerca dettagliata nella pagina Ricerca processo .

Se la ricerca è troppo stretta, non verrà trovata alcuna istanza.
