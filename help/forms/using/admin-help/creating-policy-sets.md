---
title: Creare e gestire set di criteri
description: I set di criteri vengono utilizzati per raggruppare i criteri che hanno uno scopo aziendale comune. È possibile creare, modificare ed eliminare i criteri in un set di criteri.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
exl-id: 736926af-ae41-4da3-b181-444de72407bd
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '1309'
ht-degree: 100%

---

# Creare e gestire set di criteri {#creating-and-managing-policy-sets}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

I set di criteri vengono utilizzati per raggruppare i criteri che hanno uno scopo aziendale comune. I set di criteri possono essere resi disponibili a un sottoinsieme di utenti nel sistema.

A ogni set di criteri è associato almeno un coordinatore di set di criteri. Il *coordinatore di set di criteri* è un amministratore o un utente che dispone di autorizzazioni aggiuntive. Il coordinatore di set di criteri è in genere uno specialista dell’organizzazione che può creare in modo ottimale i criteri in un determinato set di criteri.

I coordinatori dei set di criteri possono eseguire le seguenti attività:

* Creare nuovi criteri
* Modificare ed eliminare qualsiasi criterio nel set di criteri
* Modificare impostazioni del set di criteri
* Aggiungere e rimuovere coordinatori per il set di criteri
* Visualizzare eventi relativi a criteri e documenti per qualsiasi criterio o documento all’interno del set di criteri
* Revocare l’accesso ai documenti
* Cambiare i criteri per il documento

I set di criteri vengono creati ed eliminati nell’interfaccia di amministrazione di protezione dei documenti dagli utenti con privilegi avanzati e dai coordinatori dei set di criteri che dispongono delle autorizzazioni necessarie.

Quando elimini un set di criteri, i criteri che facevano parte del set non possono essere applicati ai nuovi documenti. Tuttavia, è possibile visualizzare le informazioni sui criteri sia nella console di amministrazione che nelle pagine web dell’utente finale per i criteri ancora in uso. È possibile visualizzare le informazioni sul criterio dalla pagina dei dettagli del documento per qualsiasi documento protetto dallo stesso. È possibile modificare i criteri ancora in uso.

Il coordinatore di utenti con privilegi avanzati o set di criteri aggiunge i domini creati in Gestione utenti all’utente e al gruppo visibili per ogni set di criteri. Questo elenco è visibile al coordinatore del set di criteri e viene utilizzato per definire i limiti sui domini che il coordinatore del set di criteri può esplorare quando sceglie gli utenti da aggiungere ai criteri.

Quando crei i set di criteri, assegni agli utenti il ruolo di autore del documento. L’*autore del documento* è l’utente che protegge il documento con un criterio. Per impostazione predefinita, questo utente è sempre incluso in un criterio con diritti di accesso completi, incluse le funzionalità di revoca e cambio di criterio. Tuttavia, gli amministratori possono modificare i diritti di accesso dell’autore del documento per i criteri condivisi. Ad esempio, l’amministratore può disabilitare il diritto dell’autore di documenti di revocare l’accesso ai documenti o cambiare il criterio. Se un amministratore cambia il criterio associato al documento, il nome del server di pubblicazione verrà aggiornato in base al nome del proprietario dell’ultimo criterio applicato al documento.

Al momento dell’installazione della protezione dei documenti, viene creato un set di criteri predefinito denominato *Set di criteri globale*. Questo set di criteri viene gestito dall’amministratore che ha installato il software o dal coordinatore del set di criteri designato per il set di criteri.

## Creare un set di criteri {#create-a-policy-set}

Il set di criteri globale è l’unico set di criteri predefinito creato al momento dell’installazione. È possibile creare set di criteri aggiuntivi e aggiungere criteri, utenti, coordinatori di set di criteri e autori di documenti. Dopo aver creato un set di criteri, puoi creare criteri all’interno del set.

Durante la creazione del set di criteri, puoi utilizzare il pulsante Indietro per tornare alla schermata precedente e il pulsante Salva per salvare il set di criteri in qualsiasi momento.

1. Nella pagina di protezione dei documenti fai clic su Criteri, seleziona la scheda Set di criteri e quindi fai clic su Nuovo.
1. Nella casella Nome digita un nome per il set di criteri, se desideri digita una Descrizione e quindi fai clic su Avanti. Il nome non può contenere i due punti **:**.

   >[!NOTE]
   >
   >È possibile creare un nome di set di criteri che contenga caratteri estesi; tuttavia, quando effetui un confronto tra due stringhe, i caratteri accentati e non accentati come &quot;e&quot; ed &quot;è&quot; vengono considerati uguali. Quandocrei un set di criteri, viene eseguito un confronto per verificare se esiste già un set con lo stesso nome. Il confronto non è in grado di distinguere tra nomi che sono uguali se si eccettuano i caratteri accentati. Si presume che il set di criteri sia già stato aggiunto al database e che il nuovo non venga aggiunto.

1. (Facoltativo) Per impostare i domini visibili agli editori di documenti quando aggiungono utenti a un criterio, fai clic su Aggiungi domini, seleziona i domini da rendere ricercabili, fai clic su Aggiungi e quindi su OK.
1. Nella pagina Aggiungi utenti e gruppi visibili fai clic su Avanti.
1. (Facoltativo) Per aggiungere un coordinatore di set di criteri, fai clic su Aggiungi utenti e gruppi nella pagina Aggiungi coordinatori di set di criteri (passaggio 3 di 4) ed esegui le operazioni seguenti:

   * Nella casella Trova digita il nome o l’indirizzo di posta elettronica.
   * Nell’elenco Utilizzo seleziona l’opzione appropriata.
   * Nell’elenco Tipo seleziona Utente e nell’elenco In seleziona un dominio in cui eseguire la ricerca.
   * Nell’elenco Visualizza seleziona il numero di risultati da visualizzare per pagina e quindi fai clic su Trova.
   * Seleziona la casella di controllo relativa all’utente o al gruppo da aggiungere e fai clic su Avanti.
   * Seleziona le autorizzazioni del coordinatore del set di criteri e fai clic su Aggiungi. Puoi impostare le seguenti autorizzazioni:

      * Visualizzazione degli eventi
      * Gestisci i documenti (revoca e ripristina l’accesso ai documenti e cambia i criteri sui documenti)
      * Gestisci i criteri (crea, modifica ed elimina i criteri)
      * Gestione degli editori di documenti (aggiunta e rimozione di editori di documenti)
      * Delega (aggiungi e rimuovi i coordinatori del set di criteri)

1. Ripeti il passaggio 5 per aggiungere altri coordinatori del set di criteri.
1. Rivedi le impostazioni del coordinatore del set di criteri e fai clic su Avanti.
1. Fai clic su Aggiungi utenti e gruppi per aggiungere autori di documenti che possono utilizzare i criteri del set di criteri per proteggere i documenti.
1. Nella pagina Aggiungi editori di documenti esegui le operazioni seguenti:

   * Nella casella Trova digita il nome o l’indirizzo di posta elettronica.
   * Nell’elenco Utilizzo seleziona l’opzione appropriata.
   * Nell’elenco Tipo seleziona Utente e nell’elenco In seleziona un dominio in cui eseguire la ricerca.
   * Nell’elenco Visualizza seleziona il numero di risultati da visualizzare per pagina e quindi fai clic su Trova.
   * Seleziona le caselle di controllo relative agli utenti e ai gruppi da aggiungere, fai clic su Aggiungi e quindi su OK.

1. Fai clic su Salva.

Ora puoi aggiungere i criteri al set di criteri. Consulta [Creazione e modifica dei criteri](/help/forms/using/admin-help/creating-policies.md#creating-and-editing-policies).

## Modificare un set di criteri {#edit-a-policy-set}

1. Nella pagina di protezione dei documenti, fai clic su Criteri, quindi sulla scheda Set di criteri e infine sul set di criteri da modificare.
1. Fai clic sulla scheda appropriata e modifica come richiesto:

   * **Dettagli:** modifica il nome e la descrizione del set di criteri.
   * **Criteri:** crea, abilita, modifica ed elimina i criteri all’interno del set di criteri.
   * **Utenti e gruppi visibili:** aggiungi e rimuovi utenti e gruppi visibili che possono essere inclusi in un criterio.
   * **Coordinatori dei set di criteri:** aggiungi, rimuovi e modifica le autorizzazioni per i coordinatori.
   * **Editori dei documenti:** aggiungi e rimuovi gli utenti che possono pubblicare documenti utilizzando i criteri del set.

1. Per eliminare un utente o un gruppo visibile, un coordinatore dei set di criteri o un editore dei documenti, fai clic sulla scheda appropriata, seleziona la casella di controllo relativa alla voce, fai clic su Elimina e quindi su OK.
1. Per aggiungere utenti o gruppi visibili, coordinatori dei set di criteri o editori dei documenti, fai clic sulla scheda appropriata, fai clic su Aggiungi utenti o gruppi, cerca l’utente o il gruppo da aggiungere, seleziona la voce, fai clic su Aggiungi e quindi su OK.
1. Nella scheda Criteri cerca i criteri da aggiungere al set di criteri e creane di nuovi:

   * Per cercare un criterio, seleziona ID criterio o Nome criterio, digita il valore corrispondente, seleziona il numero di elementi da visualizzare e fai clic su Trova.
   * Per informazioni dettagliate sulla creazione di un criterio, consulta [Creazione e modifica di criteri](/help/forms/using/admin-help/creating-policies.md#creating-and-editing-policies).

## Elimina un set di criteri {#delete-a-policy-set}

Quando elimini un set di criteri, i criteri che facevano parte del set non possono essere applicati ai nuovi documenti. Tuttavia, puoi visualizzare le informazioni sui criteri sia nella console di amministrazione che nelle pagine web dell’utente finale per i criteri ancora in uso. È possibile visualizzare le informazioni sul criterio dalla pagina dei dettagli del documento per qualsiasi documento protetto dallo stesso. È possibile modificare i criteri ancora in uso.

1. Fai clic su Criteri e quindi sulla scheda Set di criteri.
1. Seleziona la casella di controllo relativa al set di criteri da eliminare.
1. Fai clic su Elimina e quindi su OK.
