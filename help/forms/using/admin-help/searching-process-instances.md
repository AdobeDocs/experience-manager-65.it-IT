---
title: Ricerca di istanze di processo
seo-title: Ricerca di istanze di processo
description: Utilizzare la pagina Ricerca processo per inserire i criteri di ricerca per trovare un'istanza di processo.
seo-description: Utilizzare la pagina Ricerca processo per inserire i criteri di ricerca per trovare un'istanza di processo.
uuid: 4a9c5b05-add5-4278-9c6f-d1928b6860d2
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 88b634bb-8f6c-4830-ad01-821668609615
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---


# Ricerca di istanze di processo{#searching-for-process-instances}

Utilizzare la pagina Ricerca processo per inserire i criteri di ricerca per trovare un&#39;istanza di processo. È possibile accedere alla pagina di ricerca dei processi dalla pagina del flusso di lavoro dei moduli o facendo clic su Cerca nella pagina Istanza di processo.

Potete inserire criteri di base per eseguire una ricerca generale, attributi specifici per eseguire una ricerca dettagliata, oppure una combinazione di criteri di base e attributi specifici per eseguire una ricerca combinata.

## Eseguire una ricerca generale {#perform-a-general-search}

Una ricerca generale per un processo è più appropriata se si conosce l&#39;ID processo dell&#39;istanza di processo, se si sta cercando un gruppo di istanze di processo correlate o se sono in esecuzione solo alcune istanze di processo.

Immettete i criteri di base per eseguire una ricerca generale. Se immettete più criteri, la ricerca viene eseguita con una condizione AND implicita.

1. Nella console di amministrazione, fai clic su Servizi > Flusso di lavoro Forms > Process Search.
1. Nella pagina Ricerca processo, in Ricerca generale, specificate i seguenti criteri:

   * **ID processo:** il numero intero positivo che identifica ogni istanza di processo univoca.
   * **Stato processo:** selezionare uno stato dall&#39;elenco.
   * **Applicazione:** selezionare un&#39;applicazione dall&#39;elenco. Vengono visualizzate solo le applicazioni distribuite.
   * **Nome processo - Versione:** selezionate dal menu il nome di un processo. Vengono visualizzati solo i processi distribuiti.

1. Fate clic su Cerca. Viene visualizzata la pagina Istanza processo, in cui sono elencate le istanze trovate.

## Eseguire una ricerca dettagliata per un processo {#perform-a-detailed-search-for-a-process}

Potete immettere attributi specifici per eseguire una ricerca dettagliata. Una ricerca dettagliata è particolarmente appropriata se sono in esecuzione molte istanze di processo e occorre limitare le ricerche possibili in base a determinati criteri.

1. Nella console di amministrazione, fai clic su Servizi > Flusso di lavoro Forms > Process Search.
1. Nella pagina Ricerca processo, in Ricerca dettagliata, specificate il primo set di criteri:

   * Nell&#39;elenco Attributi, selezionare un attributo.
   * Nell&#39;elenco Filtro, selezionare un operatore.
   * Nella casella Valore, digitare il valore appropriato per l&#39;attributo selezionato.

1. Per aggiungere un’altra riga, selezionare Altri filtri. Viene visualizzato un altro set di elenchi Attributi, Filtro e Valore, oltre a un elenco Condizione.
1. In Condizione, selezionare AND o OR. Ripetete i passaggi da 1 a 3 per limitare ulteriormente la ricerca.
1. Per aggiungere o rimuovere righe, fare clic su Altri filtri o su Meno filtri. Puoi avere da una a quattro righe.
1. Fate clic su Cerca. Viene visualizzata la pagina Istanza processo, in cui sono elencate le istanze trovate.

[Informazioni sugli stati delle istanze di processo](/help/forms/using/admin-help/processes.md#about-process-instance-statuses)

## Eseguire una ricerca combinata per un processo {#perform-a-combined-search-for-a-process}

Per creare una ricerca basata sia su una ricerca generale che su una ricerca dettagliata, con un AND implicito tra le aree, immettete i criteri di ricerca nelle aree Ricerca generale e Ricerca dettagliata nella pagina Ricerca processo.

Se la ricerca è troppo stretta, non verrà trovata alcuna istanza.
