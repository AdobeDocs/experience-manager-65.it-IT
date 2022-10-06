---
title: Configurazione dei calendari aziendali
seo-title: Configuring Business Calendars
description: I calendari aziendali definiscono i giorni lavorativi e non lavorativi dell'organizzazione. Scopri come configurare i calendari aziendali.
seo-description: Business calendars define business and non-business days for your organization. Learn how to configure the business calendars.
uuid: 0ba610b8-72a8-480c-8783-70d98cbe890a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7a85e13d-4800-47c4-812a-5c6e2355298a
exl-id: 4282718a-41f1-411a-9cd7-8c470005107d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1908'
ht-degree: 0%

---

# Configurazione dei calendari aziendali {#configuring-business-calendars}

*Calendari aziendali* definisci i giorni lavorativi e non lavorativi (ad esempio, festività legali, fine settimana e giorni di chiusura dell’azienda) per la tua organizzazione. Quando si utilizzano calendari aziendali, i moduli AEM ignorano i giorni non lavorativi durante l&#39;esecuzione di determinati calcoli di data. In Workbench è possibile specificare se utilizzare i calendari aziendali per eventi associati all&#39;utente, ad esempio promemoria, scadenze e escalation delle attività, oppure per azioni non associate agli utenti, come Eventi con timer e Servizio di attesa.

Ad esempio, un promemoria attività è configurato in modo che si verifichi tre giorni lavorativi dopo l’assegnazione dell’attività a un utente. Il compito è assegnato giovedì. Tuttavia, i tre giorni seguenti non sono giorni lavorativi perché il venerdì è una festa nazionale e i due giorni successivi sono giorni feriali. Il sollecito è pertanto inviato mercoledì della settimana successiva.

>[!NOTE]
>
>Quando si calcolano le date e gli orari utilizzando i calendari aziendali, i moduli AEM utilizzano la data e l’ora del server in cui sono in esecuzione e non si adeguano alla differenza tra i fusi orari. Ad esempio, se un promemoria attività è pianificato alle 10.00 su un server in esecuzione a Londra, ma l&#39;utente che riceve il promemoria si trova a New York City, l&#39;utente riceverà il promemoria alle 5.00 ora locale.

## Utilizzo del calendario aziendale predefinito {#using-the-default-business-calendar}

AEM forms fornisce un calendario aziendale predefinito (denominato *Calendario incorporato*) che designa il sabato e la domenica come giorni non lavorativi. Se tutti gli utenti dell&#39;organizzazione hanno gli stessi giorni non lavorativi, è possibile aggiornare il calendario aziendale predefinito in base all&#39;organizzazione. Quando si utilizza solo il calendario aziendale predefinito, non è necessario abilitare i calendari aziendali in Gestione utente o fornire alcuna mappatura. Se non vengono definiti altri calendari aziendali, AEM moduli utilizza il calendario aziendale predefinito.

## Impostazione di più calendari aziendali {#setting-up-multiple-business-calendars}

Se alcuni degli utenti della tua organizzazione hanno giorni non lavorativi diversi, puoi definire più calendari aziendali e configurare mappature che consentono una risoluzione in fase di esecuzione di un calendario aziendale per un utente.

### Definire più calendari aziendali {#define-multiple-business-calendars}

1. Decidi come associare il calendario aziendale appropriato a un utente. Esistono due modi per associare un calendario aziendale a un utente:

   **Iscrizione al gruppo:** È possibile assegnare un calendario aziendale a un utente in base all’appartenenza al gruppo dell’utente. In questo caso, ogni utente del gruppo utilizzerà lo stesso calendario aziendale.

   Se un utente è membro di due gruppi diversi e tali gruppi sono mappati su due calendari aziendali diversi, AEM moduli utilizzeranno il primo calendario trovato nei risultati della ricerca. In questo caso, è consigliabile utilizzare le chiavi del calendario aziendale per associare gli utenti ai calendari aziendali.

   **Chiavi del calendario aziendale:** È possibile assegnare un calendario aziendale a un utente in base a una chiave del calendario aziendale, un&#39;impostazione specificata in Gestione utente. È quindi possibile mappare la chiave del calendario aziendale su un calendario aziendale nel flusso di lavoro dei moduli.

   Il modo in cui si assegnano le chiavi del calendario aziendale agli utenti dipende dal fatto che si utilizzi un dominio enterprise, locale o ibrido. Per maggiori dettagli sulla configurazione dei domini, vedi [Aggiunta di domini](/help/forms/using/admin-help/adding-domains.md#adding-domains).

   Se si utilizza un dominio locale o ibrido, le informazioni sugli utenti vengono memorizzate solo nel database User Management. Per impostare la chiave del calendario aziendale per questi utenti, immettere una stringa nel campo Chiave calendario aziendale quando si aggiunge o si modifica un utente in Gestione utente. (Vedi [Aggiunta e configurazione di utenti](/help/forms/using/admin-help/adding-configuring-users.md#adding-and-configuring-users).) È quindi possibile mappare le chiavi del calendario aziendale (le stringhe) ai calendari aziendali nel flusso di lavoro dei moduli. (Vedi [Mappatura di utenti e gruppi su un calendario aziendale](configuring-business-calendars.md#mapping-users-and-groups-to-a-business-calendar).)

   Se utilizzi un dominio enterprise, le informazioni sugli utenti risiedono in un sistema di storage di terze parti, ad esempio una directory LDAP, sincronizzata da User Management con il database User Management. Questo consente di mappare una chiave del calendario aziendale su un campo nella directory LDAP. Ad esempio, se ogni record utente nella directory contiene un campo &quot;paese&quot; e si desidera assegnare calendari aziendali in base al paese in cui si trova l&#39;utente, specificare il nome del campo &quot;paese&quot; nel campo Chiave calendario aziendale quando si specificano le impostazioni utente per la directory. (Vedi [Configurazione delle directory](/help/forms/using/admin-help/configuring-directories.md#configuring-directories).) È quindi possibile mappare le chiavi del calendario aziendale (i valori definiti per il campo &quot;paese&quot; nella directory LDAP) ai calendari aziendali nel flusso di lavoro dei moduli. (Vedi [Mappatura di utenti e gruppi su un calendario aziendale](configuring-business-calendars.md#mapping-users-and-groups-to-a-business-calendar).)

1. Nel flusso di lavoro dei moduli, definisci un calendario per ciascun set di utenti che condividono gli stessi giorni non lavorativi. (Vedi [Crea o aggiorna un calendario aziendale](configuring-business-calendars.md#create-or-update-a-business-calendar).)
1. Nel flusso di lavoro dei moduli, mappa le chiavi del calendario aziendale o le appartenenze al gruppo per ciascun calendario. (Vedi [Mappatura di utenti e gruppi su un calendario aziendale](configuring-business-calendars.md#mapping-users-and-groups-to-a-business-calendar).)
1. In Workbench, lo sviluppatore del processo sceglie se utilizzare i calendari aziendali per promemoria, scadenze e escalation. (Vedi [Guida di Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

   Se lo sviluppatore del processo sceglie di utilizzare i calendari aziendali, AEM moduli selezionerà in modo dinamico il calendario aziendale appropriato in base all’impostazione Gestione utente e alle mappature del calendario aziendale definite in Admin Console oppure, se non esistono mappature, utilizzerà il calendario predefinito.

   Se lo sviluppatore del processo non utilizza calendari aziendali, il calcolo della data per l’evento considera ogni giorno come un giorno lavorativo. Ad esempio, la scadenza di un&#39;attività viene configurata per essere eseguita tre giorni dopo l&#39;assegnazione dell&#39;attività a un utente. Il compito è assegnato giovedì. La scadenza del compito si verifica domenica, anche se è un fine settimana.

## Crea o aggiorna un calendario aziendale {#create-or-update-a-business-calendar}

Se l&#39;organizzazione contiene diversi set di utenti con giorni non lavorativi diversi, è possibile definire più calendari aziendali. È inoltre possibile modificare i calendari esistenti, compreso il calendario predefinito fornito con i moduli AEM.

>[!NOTE]
>
>Se non si crea un nuovo calendario aziendale, verrà utilizzato quello predefinito.

1. Nella console di amministrazione, fare clic su Servizi > Flusso di lavoro Forms > Calendari aziendali.
1. Per aggiungere un nuovo calendario aziendale, fare clic su ![bus_cal_plus](assets/bus_cal_plus.png). Testo *Nuovo calendario* nell’elenco a discesa. Selezionare il testo e digitare un altro nome per il calendario.

   Per modificare un calendario aziendale esistente, selezionarlo dall&#39;elenco a discesa.

1. In Giorni non lavorativi predefiniti, seleziona i giorni non lavorativi settimanali, ad esempio i fine settimana.
1. [Facoltativo] Selezionare Usa ore aziendali e specificare gli orari di inizio e di fine per i giorni lavorativi.

   Se si seleziona questa opzione, un evento che si verifica prima dell&#39;intervallo di tempo specificato viene spostato all&#39;inizio dell&#39;intervallo di tempo e un evento che si verifica dopo l&#39;intervallo di tempo viene spostato all&#39;ora di inizio del giorno lavorativo successivo.

   Ad esempio, si consideri una situazione in cui a un utente viene assegnata un’attività alle 02:00 di un martedì e il promemoria per tale attività è impostato su due giorni lavorativi. Senza l&#39;orario di lavoro, il promemoria si sarebbe verificato alle 2:00 di giovedì. Se l&#39;orario di lavoro è impostato alle 8:00 alle 17:00, il promemoria verrà inviato alle 8:00 di giovedì. Senza l&#39;orario di lavoro, se un evento di promemoria è stato creato alle 18:00 di martedì, il promemoria si verifica dopo l&#39;orario di lavoro di giovedì. Con l&#39;orario di lavoro impostato alle 8:00 alle 17:00, il promemoria si verificherà alle 8:00 del mattino del venerdì.

1. Nel calendario a sinistra, fai doppio clic su qualsiasi altro giorno non lavorativo, ad esempio festività. Non è possibile selezionare giorni nel passato. I giorni non lavorativi selezionati vengono visualizzati in un elenco a destra, con la data che appare due volte su una sola riga. Selezionare la data a sinistra per digitare il nome o la descrizione del giorno non lavorativo.

   Per rimuovere un giorno non lavorativo dall&#39;elenco, fare clic su ![bus_cal_spazzatura](assets/bus_cal_trash.png) accanto alla giornata.

1. [Facoltativo] Se il calendario deve essere quello predefinito, selezionare Calendario predefinito. Il calendario predefinito viene utilizzato quando non esiste alcuna altra mappatura del calendario per gli eventi associati all&#39;utente o non viene specificato alcun calendario aziendale per l&#39;evento Timer o per il servizio Attendi. Non è possibile eliminare il calendario predefinito.
1. Al termine della definizione dei giorni non lavorativi, selezionare Calendario abilitato per renderlo attivo, quindi fare clic su Salva.

   Se si aggiorna un calendario esistente, la nuova versione ha effetto immediato e viene utilizzata per tutti i calcoli del calendario aziendale, incluse le attività già in esecuzione.

   >[!NOTE]
   >
   >Se non si abilita il calendario, verrà utilizzato il calendario predefinito.

## Mappatura di utenti e gruppi su un calendario aziendale {#mapping-users-and-groups-to-a-business-calendar}

Esistono due metodi che è possibile utilizzare per associare un calendario aziendale a un utente. È possibile assegnare calendari aziendali agli utenti in base a una chiave di calendario aziendale o in base al gruppo di directory a cui appartiene l&#39;utente. Utilizzare la scheda Mappatura per specificare il metodo utilizzato AEM moduli e per mappare le chiavi e i gruppi del calendario aziendale ai calendari aziendali. Per informazioni dettagliate sull&#39;associazione delle chiavi del calendario aziendale con gli utenti, vedi [Impostazione di più calendari aziendali](configuring-business-calendars.md#setting-up-multiple-business-calendars).

### Associare i calendari aziendali agli utenti in base alle chiavi del calendario aziendale {#associate-business-calendars-with-users-based-on-business-calendar-keys}

1. In Admin Console, fai clic su Servizi > flusso di lavoro moduli > Calendari aziendali, quindi fai clic sulla scheda Mappatura .
1. Nell&#39;elenco System Will Use (Sistema utilizzerà), selezionare User Manager Business Calendar Key Resolution.
1. Selezionare Visualizza la chiave del calendario aziendale di User Manager. Viene visualizzato un elenco contenente un set univoco di chiavi del calendario aziendale definite in Gestione utente.

   Per i domini locali e ibridi, l&#39;elenco visualizza i valori immessi nel campo Chiave calendario aziendale in Gestione utente. Per i domini enterprise (LDAP), l&#39;elenco visualizza il set univoco restituito dal campo LDAP (ad esempio, &quot;country&quot;) configurato nelle impostazioni del dominio LDAP.

   Se l&#39;amministratore di User Management non ha definito alcuna chiave del calendario aziendale, l&#39;elenco sarà vuoto.

1. Per ogni elemento nell&#39;elenco delle chiavi del calendario aziendale di messaggistica unificata, selezionare un Calendario.
1. Fai clic su Salva.

### Associare i calendari aziendali a utenti e gruppi in base ai gruppi di servizi di directory {#associate-business-calendars-with-users-and-groups-based-on-directory-service-groups}

1. In Admin Console, fai clic su Servizi > flusso di lavoro moduli > Calendari aziendali, quindi fai clic sulla scheda Mappatura .
1. Selezionare Gruppi definiti dal server di directory nell&#39;elenco Verrà utilizzato.
1. Nella scheda Mappatura, selezionare Visualizza gruppi del servizio directory. Viene visualizzato un elenco contenente i gruppi definiti in Gestione utente. (Vedi [Impostazioni directory](/help/forms/using/admin-help/configuring-directories.md#directory-settings).)

   >[!NOTE]
   >
   >In Workbench, se è stato configurato un servizio utente per l’utilizzo di calendari aziendali e il servizio è assegnato a un gruppo, AEM forms utilizza le mappature dei gruppi qui specificate per risolvere il calendario del gruppo. AEM forms utilizza sempre le mappature dei gruppi per risolvere il calendario dei gruppi, anche quando si utilizzano le chiavi del calendario aziendale per risolvere il calendario per gli utenti. Se non viene trovata alcuna mappatura di gruppo, verrà utilizzato il calendario aziendale predefinito.

1. Selezionare un Calendario per ogni elemento dell&#39;elenco Gruppo servizi directory.
1. Fai clic su Salva.

## Esportazione e importazione di calendari aziendali {#exporting-and-importing-business-calendars}

I moduli AEM consentono di esportare e importare i calendari aziendali come file XML. È possibile utilizzare questa funzione per spostare i calendari da un sistema di gestione temporanea a un sistema di produzione.

>[!NOTE]
>
>Questa funzione esporta e importa tutti i calendari aziendali definiti, compreso il calendario aziendale predefinito fornito dai moduli AEM. Un calendario aziendale importato con lo stesso nome di un calendario esistente sovrascrive il calendario esistente.

### Esportare i calendari aziendali {#export-business-calendars}

1. Nella console di amministrazione, fare clic su Servizi > flusso di lavoro moduli > Calendari aziendali.
1. Fare clic su Esporta e salvare il file XML.

### Importa calendari aziendali {#import-business-calendars}

1. Nella console di amministrazione, fare clic su Servizi > flusso di lavoro moduli > Calendari aziendali.
1. Fai clic su Importa.
1. Selezionare il file XML contenente i calendari aziendali esportati e fare clic su Apri.

## Eliminare un calendario aziendale {#delete-a-business-calendar}

È possibile rimuovere i calendari aziendali non più necessari per la propria organizzazione. Se si elimina un calendario aziendale ancora mappato a utenti e gruppi, verrà utilizzato il calendario predefinito.

1. Nella console di amministrazione, fare clic su Servizi > Flusso di lavoro Forms > Calendari aziendali.
1. Selezionare il calendario.
1. Fai clic su Elimina.
