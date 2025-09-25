---
title: Configurazione dei calendari aziendali
description: I calendari aziendali definiscono i giorni lavorativi e non lavorativi della tua organizzazione. Scopri come configurare i calendari aziendali.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 4282718a-41f1-411a-9cd7-8c470005107d
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '1912'
ht-degree: 100%

---

# Configurazione dei calendari aziendali {#configuring-business-calendars}

I *calendari aziendali* definiscono i giorni lavorativi e non lavorativi (ad esempio, le festività riconosciute pr legge, i fine settimana e i giorni di chiusura dell’azienda) dell’organizzazione. Quando si utilizzano i calendari aziendali, AEM Forms ignora i giorni non lavorativi durante l’esecuzione di determinati calcoli di date. In Workbench è possibile specificare se utilizzare i calendari aziendali per gli eventi associati all’utente, ad esempio promemoria di attività, scadenze ed escalation, oppure per le azioni non associate all’utente, ad esempio Eventi con timer e Servizio di attesa.

Ad esempio, un promemoria di attività è configurato per essere visualizzato tre giorni lavorativi dopo l’assegnazione dell’attività a un utente. L’attività viene assegnata giovedì. Tuttavia, i tre giorni successivi non sono giorni lavorativi perché il venerdì è festa nazionale e i due giorni successivi sono giorni festivi. Il promemoria verrà quindi inviato il mercoledì della settimana successiva.

>[!NOTE]
>
>Quando le date e le ore vengono calcolate utilizzando i calendari aziendali, AEM Forms utilizza la data e l’ora del server in cui è in esecuzione e non modifica la differenza tra i fusi orari. Ad esempio, se un promemoria dell’attività è pianificato per le ore 10:00 su un server in esecuzione a Londra, ma l’utente che deve ricevere il promemoria si trova a New York, riceverà il promemoria alle 5:00 ora locale.

## Utilizzare il calendario aziendale predefinito {#using-the-default-business-calendar}

AEM Forms fornisce un calendario aziendale predefinito (denominato *Calendario predefinito*) in cui i sabati e le domeniche sono indicati come giorni non lavorativi. Se tutti gli utenti dell’organizzazione hanno gli stessi giorni non lavorativi, puoi aggiornare il calendario aziendale predefinito in base alle esigenze dell’organizzazione. Quando utilizzi solo il calendario aziendale predefinito, non è necessario abilitare i calendari aziendali in Gestione utenti né fornire alcuna mappatura. Se non vengono definiti altri calendari aziendali, AEM Forms utilizza il calendario aziendale predefinito.

## Configurare più calendari aziendali {#setting-up-multiple-business-calendars}

Se alcuni utenti dell’organizzazione dispongono di giorni non lavorativi diversi, puoi definire più calendari aziendali e configurare delle mappature che consentano la risoluzione dell’esecuzione di un calendario aziendale per un utente.

### Definizione di più calendari aziendali {#define-multiple-business-calendars}

1. Decidi come associare il calendario aziendale appropriato a un utente. Esistono due modi per associare un calendario aziendale a un utente:

   **Iscrizione al gruppo:** puoi assegnare un calendario aziendale a un utente in base all’iscrizione al gruppo di quell’utente. In questo caso, ogni utente del gruppo utilizzerà lo stesso calendario aziendale.

   Se un utente è membro di due gruppi diversi e tali gruppi sono mappati a due calendari aziendali diversi, AEM Forms utilizzerà il primo calendario individuato nei risultati della ricerca. In questo caso, è consigliabile utilizzare le chiavi del calendario aziendale per associare gli utenti ai calendari aziendali.

   **Chiavi del calendario aziendale:** puoi assegnare un calendario aziendale a un utente in base a una chiave del calendario aziendale, che è un’impostazione specificata in Gestione utenti. Puoi eseguire la mappatura della chiave del calendario aziendale a un calendario aziendale in Forms Workflow.

   Il modo in cui assegni le chiavi del calendario aziendale agli utenti dipende dal fatto che utilizzi un dominio enterprise, locale o ibrido. Per informazioni dettagliate sulla configurazione dei domini, consulta [Aggiungere domini](/help/forms/using/admin-help/adding-domains.md#adding-domains).

   Se utilizzi un dominio locale o ibrido, le informazioni relative agli utenti vengono memorizzate solo nel database di Gestione utenti. Per impostare la chiave del calendario aziendale per questi utenti, immetti una stringa nel campo Chiave del calendario aziendale quando aggiungi o modifichi un utente in Gestione utente. (Consulta [Aggiungere e configurare utenti](/help/forms/using/admin-help/adding-configuring-users.md#adding-and-configuring-users).) Puoi quindi mappare le chiavi del calendario aziendale (le stringhe) ai calendari aziendali in Forms Workflow. (Consulta [Mappatura di utenti e gruppi a un calendario aziendale](configuring-business-calendars.md#mapping-users-and-groups-to-a-business-calendar).)

   Se utilizzi un dominio enterprise, le informazioni sugli utenti risiedono in un sistema di archiviazione di terze parti, ad esempio una directory LDAP, che Gestione utenti sincronizza con il proprio database. In questo modo potrai eseguire la mappatura di una chiave del calendario aziendale a un campo nella directory LDAP. Ad esempio, se ogni record utente della directory contiene un campo “paese” e desideri assegnare calendari aziendali in base al paese in cui si trova l’utente, specifica il nome del campo “paese” nel campo Chiave del calendario aziendale quando specifichi le impostazioni utente per la directory. (Consulta [Configurare le directory](/help/forms/using/admin-help/configuring-directories.md#configuring-directories).) Puoi eseguire la mappatura delle chiavi del calendario aziendale (i valori definiti per il campo “paese” nella directory LDAP) ai calendari aziendali in Forms Workflow. (Consulta [Mappatura di utenti e gruppi a un calendario aziendale](configuring-business-calendars.md#mapping-users-and-groups-to-a-business-calendar).)

1. In Forms Workflow, definisci un calendario per ogni gruppo di utenti che condividono gli stessi giorni non lavorativi. (Consulta [Creare o aggiornare un calendario aziendale](configuring-business-calendars.md#create-or-update-a-business-calendar).)
1. In Forms Workflow, esegui la mappatura delle chiavi del calendario aziendale o delle iscrizioni ai gruppi per ogni calendario. (Consulta [Mappatura di utenti e gruppi a un calendario aziendale](configuring-business-calendars.md#mapping-users-and-groups-to-a-business-calendar).)
1. In Workbench, lo sviluppatore del processo sceglie se utilizzare i calendari aziendali per promemoria, scadenze ed escalation. (Consulta [Guida di Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63_it).)

   Se lo sviluppatore del processo sceglie di utilizzare i calendari aziendali, AEM Forms selezionerà dinamicamente il calendario aziendale appropriato in base all’impostazione di Gestione utente e alle mappature del calendario aziendale definite nella console di amministrazione oppure, se non esiste alcuna mappatura, utilizzerà il calendario predefinito.

   Se lo sviluppatore del processo non utilizza calendari aziendali, il calcolo della data dell’evento considera ogni giorno come giorno lavorativo. Ad esempio, la scadenza di un’attività è configurata in modo che sia tre giorni dopo l’assegnazione dell’attività a un utente. L’attività viene assegnata giovedì. La scadenza dell’attività è domenica, anche se si tratta di un fine settimana.

## Creare o aggiornare un calendario aziendale {#create-or-update-a-business-calendar}

Se l’organizzazione prevede diversi gruppi di utenti con giorni non lavorativi diversi, puoi definire più calendari aziendali. Puoi inoltre modificare i calendari esistenti, incluso il calendario predefinito fornito con AEM Forms.

>[!NOTE]
>
> * Se non crei un calendario aziendale, verrà utilizzato il calendario predefinito.
> * Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.


1. Nella console di amministrazione, fai clic su Servizi > Flusso di lavoro Forms > Calendari aziendali.
2. Per aggiungere un nuovo calendario aziendale, fai clic su ![bus_cal_plus](assets/bus_cal_plus.png). Il testo *Nuovo calendario* viene visualizzato nell’elenco a discesa. Seleziona il testo e digita un altro nome per il calendario.

   Per modificare un calendario aziendale esistente, selezionalo dall’elenco a discesa.

3. In Giorni non lavorativi predefiniti seleziona qualsiasi giorno non lavorativo settimanale, ad esempio i fine settimana.
4. [Facoltativo] Seleziona Usa orario di lavoro e specificare l’orario di inizio e di fine per i giorni lavorativi.

   Se selezioni questa opzione, un evento che si verifica prima dell’intervallo di tempo specificato viene spostato all’inizio dell’intervallo di tempo e un evento che si verifica dopo l’intervallo di tempo viene spostato all’ora di inizio del giorno lavorativo successivo.

   Consideriamo ad esempio la situazione in cui a un utente viene assegnata un’attività alle 2:00:00 del mattino di martedì e il promemoria per tale attività è impostato su due giorni lavorativi. Senza l’orario di lavoro, il promemoria si verificherebbe alle 2:00:00 di giovedì. Se l’orario di lavoro è impostato dalle 8:00:00 alle 17:00:00, il promemoria verrà inviato alle 8:00:00 di giovedì. Senza orario di lavoro, se un evento di promemoria è stato creato alle 18:00 di martedì, il promemoria si verificherebbe al di fuori dell’orario lavorativo di giovedì. :00 Con l’orario di lavoro impostato dalle 8:00:00 alle 17:00:00, il promemoria si verificherà alle 8:00:00 di venerdì.

5. Nel calendario a sinistra fai doppio clic su qualsiasi altro giorno non lavorativo, ad esempio su una festività. Non è possibile selezionare date pregresse. I giorni non lavorativi selezionati vengono visualizzati in un elenco sulla destra, con la data riportata due volte su una riga. Seleziona la data a sinistra per digitare il nome o la descrizione del giorno non lavorativo.

   Per rimuovere un giorno non lavorativo dall’elenco fai clic su ![bus_cal_trash](assets/bus_cal_trash.png) accanto al giorno.

6. [Facoltativo] Se il calendario deve essere quello predefinito, seleziona Calendario predefinito. Il calendario predefinito viene utilizzato quando non esiste nessun’altra mappatura di calendario per gli eventi associati all’utente o non è specificato alcun calendario aziendale per l’evento timer o il servizio di attesa. Non è possibile eliminare il calendario predefinito.
7. Dopo aver definito i giorni non lavorativi, seleziona Calendario abilitato per attivarlo e quindi fai clic su Salva.

   Se aggiorni un calendario esistente, la nuova versione viene applicata immediatamente e viene utilizzata per tutti i calcoli del calendario aziendale, incluse le attività già in esecuzione.

   >[!NOTE]
   >
   >Se non abiliti il calendario, verrà utilizzato il calendario predefinito.

## Mappatura di utenti e gruppi a un calendario aziendale {#mapping-users-and-groups-to-a-business-calendar}

Per associare un calendario aziendale a un utente è possibile utilizzare due metodi. È possibile assegnare calendari aziendali agli utenti in base a una chiave del calendario aziendale o in base al gruppo di directory a cui appartiene l’utente. La scheda Mappatura consente di specificare il metodo che verrà utilizzato da AEM Forms e di associare le chiavi e i gruppi del calendario aziendale ai calendari aziendali. Per informazioni dettagliate sull’associazione delle chiavi del calendario aziendale agli utenti, consulta [Impostazione di più calendari aziendali](configuring-business-calendars.md#setting-up-multiple-business-calendars).

### Associare calendari aziendali a utenti in base alle chiavi del calendario aziendale {#associate-business-calendars-with-users-based-on-business-calendar-keys}

1. Nella console di amministrazione, fai clic su Servizi > Flusso di lavoro Forms > Calendari aziendali, quindi fai clic sulla scheda Mappatura.
1. Nell’elenco Il sistema utilizzerà, seleziona Gestione utente > Calendario aziendale > Risoluzione chiave.
1. In Gestione utente, seleziona Visualizza calendario aziendale chiave Viene visualizzato un elenco contenente un set univoco di chiavi del calendario aziendale definite in Gestione utente.

   Per i domini locali e ibridi, l’elenco visualizza i valori inseriti nel campo Chiave calendario aziendale in Gestione utente. Per i domini enterprise (LDAP), l’elenco mostra il set univoco restituito dal campo LDAP (ad esempio, “paese”) configurato nelle impostazioni del dominio LDAP.

   Se l’amministratore di Gestione utente non ha definito alcuna chiave del calendario aziendale, l’elenco sarà vuoto.

1. Per ogni elemento nell’elenco Chiave calendario aziendale di messaggistica unificata, seleziona un Calendario.
1. Fai clic su Salva.

### Associa i calendari aziendali agli utenti e ai gruppi in base ai gruppi del servizio di directory {#associate-business-calendars-with-users-and-groups-based-on-directory-service-groups}

1. Nella console di amministrazione, fai clic su Servizi > Flusso di lavoro Forms > Calendari aziendali, quindi fai clic sulla scheda Mappatura.
1. Nell’elenco Il sistema utilizzerà, seleziona Gruppi definiti dal server delle directory.
1. Nella scheda Mappatura, seleziona Visualizza gruppi di servizi directory. Viene visualizzato un elenco contenente i gruppi definiti nella Gestione utenti. Consulta [Impostazioni della directory](/help/forms/using/admin-help/configuring-directories.md#directory-settings).

   >[!NOTE]
   >
   >In Workbench, se hai configurato un servizio utente per l’utilizzo dei calendari aziendali e il servizio è assegnato a un gruppo, AEM Forms utilizza le mappature dei gruppi specificati per risolvere il calendario per il gruppo. AEM forms utilizza sempre le mappature dei gruppi per risolvere il calendario per i gruppi, anche quando utilizzi le chiavi del calendario aziendale per risolvere il calendario per gli utenti. Se non viene trovata alcuna mappatura dei gruppi, viene utilizzato il calendario aziendale predefinito.

1. Per ogni elemento nell’elenco Gruppo del servizio di directory, seleziona un Calendario.
1. Fai clic su Salva.

## Esportazione e importazione di calendari aziendali {#exporting-and-importing-business-calendars}

AEM Forms consente di esportare e importare i calendari aziendali come file XML. Puoi utilizzare questa funzione per spostare i calendari da un sistema di staging a un sistema di produzione.

>[!NOTE]
>
>Questa funzione consente di esportare e importare tutti i calendari aziendali definiti, incluso il calendario aziendale predefinito fornito da AEM Forms. Un calendario aziendale importato con lo stesso nome di un calendario esistente sovrascrive il calendario esistente.

### Esportare i calendari aziendali {#export-business-calendars}

1. Nella console di amministrazione, fai clic su Servizi > Flusso di lavoro Forms > Calendari aziendali.
1. Fai clic su Esporta e salva il file XML.

### Importare i calendari aziendali {#import-business-calendars}

1. Nella console di amministrazione, fai clic su Servizi > Flusso di lavoro Forms > Calendari aziendali.
1. Fai clic su Importa.
1. Seleziona il file XML contenente i calendari aziendali esportati e fai clic su Apri.

## Eliminare un calendario aziendale {#delete-a-business-calendar}

Puoi rimuovere i calendari aziendali di cui l’organizzazione non ha più bisogno. Se elimini un calendario aziendale ancora mappato a utenti e gruppi, viene utilizzato il calendario predefinito.

1. Nella console di amministrazione, fai clic su Servizi > Flusso di lavoro Forms > Calendari aziendali.
1. Seleziona il calendario.
1. Fai clic su Elimina.
