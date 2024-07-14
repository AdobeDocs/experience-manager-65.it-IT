---
title: Creazione e gestione di set di criteri
description: I set di criteri vengono utilizzati per raggruppare i criteri che hanno uno scopo aziendale comune. È possibile creare, modificare ed eliminare i criteri in un set di criteri.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
exl-id: 736926af-ae41-4da3-b181-444de72407bd
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1297'
ht-degree: 0%

---

# Creazione e gestione di set di criteri {#creating-and-managing-policy-sets}

I set di criteri vengono utilizzati per raggruppare i criteri che hanno uno scopo aziendale comune. I set di criteri possono essere resi disponibili a un sottoinsieme di utenti nel sistema.

A ogni set di criteri è associato almeno un coordinatore di set di criteri. Il *coordinatore set di criteri* è un amministratore o un utente che dispone di autorizzazioni aggiuntive. Il coordinatore del set di criteri è in genere uno specialista dell’organizzazione che può creare in modo ottimale i criteri in un determinato set di criteri.

I coordinatori dei set di criteri possono eseguire le seguenti attività:

* Creare nuovi criteri
* Modificare ed eliminare qualsiasi criterio nel set di criteri
* Modifica impostazioni set di criteri
* Aggiunta e rimozione di coordinatori per il set di criteri
* Visualizzare eventi relativi a criteri e documenti per qualsiasi criterio o documento all&#39;interno del set di criteri
* Revoca dell&#39;accesso ai documenti
* Cambia criteri per il documento

I set di criteri vengono creati ed eliminati nell’interfaccia di amministrazione di document security dagli utenti con privilegi avanzati e dai coordinatori dei set di criteri che dispongono delle autorizzazioni necessarie.

Quando si elimina un set di criteri, i criteri che facevano parte del set non possono essere applicati ai nuovi documenti. Tuttavia, è possibile visualizzare le informazioni sui criteri sia nella console di amministrazione che nelle pagine Web dell&#39;utente finale per i criteri ancora in uso. È possibile visualizzare le informazioni sulla policy dalla pagina dei dettagli del documento per qualsiasi documento protetto dalla policy. È possibile modificare i criteri ancora in uso.

Il coordinatore di utenti con privilegi avanzati o set di criteri aggiunge i domini creati in Gestione utenti all&#39;utente e al gruppo visibili per ogni set di criteri. Questo elenco è visibile al coordinatore del set di criteri e viene utilizzato per definire i limiti sui domini che il coordinatore può esplorare quando sceglie gli utenti da aggiungere ai criteri.

Quando si creano i set di criteri, si assegna agli utenti il ruolo di autore del documento. L&#39;*editore di documenti* è l&#39;utente che protegge il documento con un criterio. Per impostazione predefinita, questo utente è sempre incluso in un criterio con diritti di accesso completi, incluse le funzionalità di revoca e cambio di criterio. Tuttavia, gli amministratori possono modificare i diritti di accesso dell’editore del documento per i criteri condivisi. Ad esempio, l’amministratore può disabilitare il diritto dell’editore di documenti di revocare l’accesso ai documenti o cambiare la policy. Se un amministratore cambia il criterio associato al documento, il nome del server di pubblicazione verrà aggiornato in base al nome del proprietario dell&#39;ultimo criterio applicato al documento.

Al momento dell&#39;installazione di Document Security, viene creato un set di criteri predefinito denominato *Set di criteri globale*. Questo set di criteri viene gestito dall&#39;amministratore che ha installato il software o dal coordinatore del set di criteri designato per il set di criteri.

## Creare un set di criteri {#create-a-policy-set}

Il set di criteri globale è l&#39;unico set di criteri predefinito creato al momento dell&#39;installazione. È possibile creare set di criteri aggiuntivi e aggiungere criteri, utenti, coordinatori di set di criteri e autori di documenti. Dopo aver creato un set di criteri, è possibile creare criteri all&#39;interno del set.

Durante la creazione del set di criteri, è possibile utilizzare il pulsante Indietro per tornare alla schermata precedente e il pulsante Salva per salvare il set di criteri in qualsiasi momento.

1. Nella pagina di protezione dei documenti fare clic su Criteri, selezionare la scheda Set di criteri e quindi fare clic su Nuovo.
1. Nella casella Nome digitare un nome per il set di criteri, facoltativamente digitare una Descrizione e quindi fare clic su Avanti. Il nome non può contenere i due punti **:**.

   >[!NOTE]
   >
   >È possibile creare un nome di set di criteri che contenga caratteri estesi; tuttavia, quando si effettua un confronto tra due stringhe, i caratteri accentati e non accentati come &quot;e&quot; ed &quot;é&quot; vengono considerati uguali. Quando si crea un set di criteri, viene eseguito un confronto per verificare se esiste già un set con lo stesso nome. Il confronto non è in grado di distinguere tra nomi uguali, ad eccezione dei caratteri accentati. Si presume che il set di criteri sia già stato aggiunto al database e che il nuovo non venga aggiunto.

1. (Facoltativo) Per impostare i domini visibili agli editori di documenti quando aggiungono utenti a una policy, fai clic su Aggiungi domini, seleziona i domini da rendere ricercabili, fai clic su Aggiungi e quindi su OK.
1. Nella pagina Aggiungi utenti e gruppi visibili fare clic su Avanti.
1. (Facoltativo) Per aggiungere un coordinatore di set di criteri, fare clic su Aggiungi utenti e gruppi nella pagina Aggiungi coordinatore/i di set di criteri (passaggio 3 di 4) ed eseguire le operazioni seguenti:

   * Nella casella Trova digitare il nome o l&#39;indirizzo di posta elettronica.
   * Nell&#39;elenco Utilizzo selezionare l&#39;opzione appropriata.
   * Nell&#39;elenco Tipo, selezionare Utente e, nell&#39;elenco In, selezionare un dominio in cui eseguire la ricerca.
   * Nell&#39;elenco Visualizzazione selezionare il numero di risultati da visualizzare per pagina e quindi fare clic su Trova.
   * Selezionare la casella di controllo relativa all&#39;utente o al gruppo da aggiungere e fare clic su Avanti.
   * Selezionare le autorizzazioni del coordinatore del set di criteri e fare clic su Aggiungi. È possibile impostare le seguenti autorizzazioni:

      * Visualizza eventi
      * Gestire i documenti (revocare e ripristinare l&#39;accesso ai documenti e cambiare le policy sui documenti)
      * Gestire i criteri (creare, modificare ed eliminare i criteri)
      * Gestione degli editori di documenti (aggiunta e rimozione di editori di documenti)
      * Delega (aggiungere e rimuovere i coordinatori del set di criteri)

1. Ripeti il passaggio 5 per aggiungere altri coordinatori del set di criteri.
1. Rivedere le impostazioni del coordinatore del set di criteri e fare clic su Avanti.
1. Fare clic su Aggiungi utenti e gruppi per aggiungere autori di documenti che possono utilizzare i criteri del set di criteri per proteggere i documenti.
1. Nella pagina Aggiungi autori documenti eseguire le operazioni seguenti:

   * Nella casella Trova digitare il nome o l&#39;indirizzo di posta elettronica.
   * Nell&#39;elenco Utilizzo selezionare l&#39;opzione appropriata.
   * Nell&#39;elenco Tipo, selezionare Utente e, nell&#39;elenco In, selezionare un dominio in cui eseguire la ricerca.
   * Nell&#39;elenco Visualizzazione selezionare il numero di risultati da visualizzare per pagina e quindi fare clic su Trova.
   * Selezionare le caselle di controllo relative agli utenti e ai gruppi da aggiungere, fare clic su Aggiungi e quindi su OK.

1. Fai clic su Salva.

Ora puoi aggiungere criteri al set di criteri. (Vedi [Creazione e modifica dei criteri](/help/forms/using/admin-help/creating-policies.md#creating-and-editing-policies).)

## Modificare un set di criteri {#edit-a-policy-set}

1. Nella pagina di protezione dei documenti, fai clic su Criteri, quindi sulla scheda Set di criteri e infine sul set di criteri da modificare.
1. Fai clic sulla scheda appropriata e modifica come richiesto:

   * **Dettagli:** Modificare il nome e la descrizione del set di criteri.
   * **Criteri:** Creare, abilitare, modificare ed eliminare i criteri all&#39;interno del set di criteri.
   * **Utenti e gruppi visibili:** Aggiungere e rimuovere utenti e gruppi visibili che possono essere inclusi in un criterio.
   * **Coordinatori set di criteri:** Aggiungere, rimuovere e modificare le autorizzazioni per i coordinatori.
   * **Autori documenti:** Aggiungere e rimuovere gli utenti che possono pubblicare documenti utilizzando i criteri del set.

1. Per eliminare un utente o un gruppo visibile, Coordinatore set di criteri o Publisher documenti, fare clic sulla scheda appropriata, selezionare la casella di controllo relativa alla voce, fare clic su Elimina e quindi su OK.
1. Per aggiungere utenti o gruppi visibili, un coordinatore di set di criteri o autori di documenti, fare clic sulla scheda appropriata, fare clic su Aggiungi utenti o gruppi, cercare l&#39;utente o il gruppo da aggiungere, selezionare la voce, fare clic su Aggiungi e quindi fare clic su OK.
1. Nella scheda Criteri cercare i criteri da aggiungere al set di criteri e creare nuovi criteri:

   * Per cercare un criterio, seleziona ID criterio o Nome criterio, digita il valore corrispondente, seleziona il numero di elementi da visualizzare e fai clic su Trova.
   * Per informazioni dettagliate sulla creazione di un criterio, vedere [Creazione e modifica di criteri](/help/forms/using/admin-help/creating-policies.md#creating-and-editing-policies).

## Eliminare un set di criteri {#delete-a-policy-set}

Quando si elimina un set di criteri, i criteri che facevano parte del set non possono essere applicati ai nuovi documenti. Tuttavia, è possibile visualizzare le informazioni sui criteri sia nella console di amministrazione che nelle pagine Web dell&#39;utente finale per i criteri ancora in uso. È possibile visualizzare le informazioni sulla policy dalla pagina dei dettagli del documento per qualsiasi documento protetto dalla policy. È possibile modificare i criteri ancora in uso.

1. Fai clic su Criteri e quindi sulla scheda Set di criteri.
1. Selezionare la casella di controllo relativa al set di criteri da eliminare.
1. Fare clic su Elimina e quindi su OK.
