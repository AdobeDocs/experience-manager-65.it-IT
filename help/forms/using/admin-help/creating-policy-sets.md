---
title: Creazione e gestione di set di criteri
seo-title: Creazione e gestione di set di criteri
description: I set di criteri vengono utilizzati per raggruppare i criteri con uno scopo aziendale comune. Potete creare, modificare ed eliminare i criteri in un set di criteri.
seo-description: I set di criteri vengono utilizzati per raggruppare i criteri con uno scopo aziendale comune. Potete creare, modificare ed eliminare i criteri in un set di criteri.
uuid: 11faf67c-b9b7-4394-8672-d43cace131ad
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a4fb1a11-8fe3-4092-a036-1c079aea1250
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1324'
ht-degree: 0%

---


# Creazione e gestione di set di criteri {#creating-and-managing-policy-sets}

I set di criteri vengono utilizzati per raggruppare i criteri con uno scopo aziendale comune. I set di criteri possono essere resi disponibili a un sottoinsieme di utenti nel sistema.

A ciascun set di criteri è associato almeno un coordinatore set di criteri. Il *coordinatore del set di criteri* è un amministratore o un utente che dispone di autorizzazioni aggiuntive. Il coordinatore del set di criteri è in genere uno specialista dell&#39;organizzazione che può creare al meglio i criteri in un determinato set di criteri.

I coordinatori dei set di criteri possono eseguire le seguenti attività:

* Creare nuovi criteri
* Modificare ed eliminare qualsiasi criterio nel set di criteri
* Modificare le impostazioni del set di criteri
* Aggiunta e rimozione di coordinatori per il set di criteri
* Visualizzare gli eventi dei criteri e dei documenti per qualsiasi criterio o documento all&#39;interno del set di criteri
* Revoca dell&#39;accesso ai documenti
* Cambiare i criteri per il documento

I set di criteri vengono creati ed eliminati nell&#39;interfaccia dell&#39;amministratore di Document Security da super utenti e coordinatori di set di criteri che dispongono dell&#39;autorizzazione necessaria.

Quando eliminate un set di criteri, i criteri che facevano parte del set non possono essere applicati ai nuovi documenti. Tuttavia, potete visualizzare le informazioni sui criteri sia nella console di amministrazione che nelle pagine Web dell&#39;utente finale per i criteri ancora in uso. È possibile visualizzare le informazioni sui criteri dalla pagina dei dettagli del documento per qualsiasi documento protetto dal criterio. È possibile modificare i criteri ancora in uso.

Il super utente o il coordinatore del set di criteri aggiunge i domini creati in Gestione utente all&#39;utente e al gruppo visibili per ciascun set di criteri. Questo elenco è visibile al coordinatore del set di criteri e viene utilizzato per limitare i domini a cui il coordinatore del set di criteri può accedere quando sceglie gli utenti da aggiungere ai criteri.

Quando create dei set di criteri, assegnate agli utenti il ruolo di autore del documento. L&#39; *autore del documento* è l&#39;utente che protegge il documento con un criterio. Per impostazione predefinita, questo utente è sempre incluso in un criterio con diritti di accesso completi, incluse le funzionalità di revoca e di cambio di criteri. Tuttavia, gli amministratori possono modificare i diritti di accesso dell&#39;editore del documento per i criteri condivisi. Ad esempio, l&#39;amministratore può disattivare il diritto dell&#39;autore del documento di revocare l&#39;accesso al documento o cambiare il criterio. Se un amministratore cambia il criterio associato al documento, il nome dell&#39;editore verrà aggiornato al nome del proprietario del criterio applicato per l&#39;ultima volta al documento.

Dopo l&#39;installazione della protezione del documento, viene creato un set di criteri predefinito denominato *Set di criteri globali*. Questo set di criteri viene gestito dall&#39;amministratore che ha installato il software o dal coordinatore del set di criteri designato per questo set di criteri.

## Creare un set di criteri {#create-a-policy-set}

Il set di criteri globale è l&#39;unico set di criteri predefinito creato al momento dell&#39;installazione. Potete creare set di criteri aggiuntivi e aggiungere criteri, utenti, coordinatori di set di criteri e editori di documenti. Dopo aver creato un set di criteri, potete creare criteri all&#39;interno del set.

Durante la creazione del set di criteri, potete utilizzare il pulsante Indietro per tornare alla schermata precedente e il pulsante Salva per salvare il set di criteri in qualsiasi momento.

1. Nella pagina Protezione documento, fare clic su Criteri, fare clic sulla scheda Set criteri, quindi su Nuovo.
1. Nella casella Nome, digitare un nome per il set di criteri, digitare facoltativamente una Descrizione, quindi fare clic su Avanti. Il nome non può contenere due punti **:**.

   >[!NOTE]
   >
   >Potete creare un nome di set di criteri contenente caratteri estesi; tuttavia, quando si effettua un confronto tra due stringhe, i caratteri accentati e non accentati come &quot;e&quot; e &quot;é&quot; sono considerati uguali. Quando un utente crea un set di criteri, viene effettuato un confronto per verificare se esiste già un set di criteri con lo stesso nome. Il confronto non è in grado di distinguere tra nomi identici tranne che per i caratteri accentati. Si presume che il set di criteri sia già stato aggiunto al database e che il nuovo non sia stato aggiunto.

1. (Facoltativo) Per impostare i domini che sono visibili agli editori di documenti quando aggiungono utenti a un criterio, fare clic su Aggiungi domini, selezionare i domini per rendere ricercabili, fare clic su Aggiungi, quindi su OK.
1. Nella pagina Aggiungi utenti e gruppi visibili, fai clic su Avanti.
1. (Facoltativo) Per aggiungere un coordinatore del set di criteri, fate clic su Aggiungi utenti e gruppi nella pagina Aggiungi coordinatori set di criteri (Passaggio 3 di 4) ed eseguite le seguenti operazioni:

   * Nella casella Trova, digitare il nome o l&#39;indirizzo e-mail.
   * Nell&#39;elenco Uso, selezionare l&#39;opzione appropriata.
   * Nell&#39;elenco Tipo, selezionare Utente e, nell&#39;elenco In, selezionare un dominio da cercare.
   * Nell&#39;elenco Visualizza, selezionare il numero di risultati da visualizzare per pagina, quindi fare clic su Trova.
   * Selezionate la casella di controllo per l’utente o il gruppo da aggiungere e fate clic su Avanti.
   * Selezionate le autorizzazioni del coordinatore del set di criteri e fate clic su Aggiungi. È possibile impostare le seguenti autorizzazioni:

      * Visualizzare gli eventi
      * Gestire i documenti (revocare e ripristinare l&#39;accesso ai documenti e cambiare i criteri sui documenti)
      * Gestire i criteri (creare, modificare ed eliminare i criteri)
      * Gestione degli editori di documenti (aggiungere e rimuovere editori di documenti)
      * Delega (aggiungere e rimuovere Coordinatori set di criteri)

1. Ripetere il passaggio 5 per aggiungere altri coordinatori di set di criteri.
1. Esaminate le impostazioni del coordinatore del set di criteri e fate clic su Avanti.
1. Fate clic su Aggiungi utenti e gruppi per aggiungere editori di documenti che possono utilizzare i criteri all&#39;interno del set per proteggere i documenti.
1. Nella pagina Aggiungi editori di documenti, eseguite le seguenti operazioni:

   * Nella casella Trova, digitare il nome o l&#39;indirizzo e-mail.
   * Nell&#39;elenco Uso, selezionare l&#39;opzione appropriata.
   * Nell&#39;elenco Tipo, selezionare Utente e, nell&#39;elenco In, selezionare un dominio da cercare.
   * Nell&#39;elenco Visualizza, selezionare il numero di risultati da visualizzare per pagina, quindi fare clic su Trova.
   * Selezionate le caselle di controllo per gli utenti e i gruppi da aggiungere, fate clic su Aggiungi, quindi su OK.

1. Fate clic su Salva.

È ora possibile aggiungere criteri al set di criteri. (Vedere [Creazione e modifica di criteri](/help/forms/using/admin-help/creating-policies.md#creating-and-editing-policies).)

## Modificare un set di criteri {#edit-a-policy-set}

1. Nella pagina Protezione documento, fare clic su Criteri, fare clic sulla scheda Set criteri e quindi sul set di criteri da modificare.
1. Fate clic sulla scheda appropriata e modificate come necessario:

   * **Dettagli:** modificate il nome e la descrizione del set di criteri.
   * **Criteri:** creare, abilitare, modificare ed eliminare i criteri all&#39;interno del set di criteri.
   * **Utenti e gruppi visibili:** aggiungere e rimuovere utenti e gruppi visibili che possono essere inclusi in un criterio.
   * **Coordinatori set di criteri:** aggiungere, rimuovere e modificare le autorizzazioni per i coordinatori.
   * **Editori di documenti:** aggiungere e rimuovere utenti che possono pubblicare i documenti utilizzando i criteri nel set.

1. Per eliminare un utente o un gruppo visibile, Coordinatore set di criteri o Editore documenti, fare clic sulla scheda appropriata, selezionare la casella di controllo relativa alla voce, fare clic su Elimina, quindi su OK.
1. Per aggiungere utenti o gruppi visibili, un coordinatore di set di criteri o editori di documenti, fare clic sulla scheda appropriata, fare clic su Aggiungi utenti o gruppi, cercare l&#39;utente o il gruppo da aggiungere, selezionare la voce, fare clic su Aggiungi, quindi su OK.
1. Nella scheda Criteri, cercate i criteri da aggiungere al set di criteri e create nuovi criteri:

   * Per cercare un criterio, selezionate ID criterio o Nome criterio, digitate il valore corrispondente, selezionate il numero di elementi da visualizzare e fate clic su Trova.
   * Per informazioni dettagliate sulla creazione di un nuovo criterio, vedere [Creazione e modifica di criteri](/help/forms/using/admin-help/creating-policies.md#creating-and-editing-policies).

## Eliminare un set di criteri {#delete-a-policy-set}

Quando eliminate un set di criteri, i criteri che facevano parte del set non possono essere applicati ai nuovi documenti. Tuttavia, potete visualizzare le informazioni sui criteri sia nella console di amministrazione che nelle pagine Web dell&#39;utente finale per i criteri ancora in uso. È possibile visualizzare le informazioni sui criteri dalla pagina dei dettagli del documento per qualsiasi documento protetto dal criterio. È possibile modificare i criteri ancora in uso.

1. Fate clic su Criteri e quindi sulla scheda Set criteri.
1. Selezionare la casella di controllo per il set di criteri da eliminare.
1. Fate clic su Elimina, quindi su OK.

