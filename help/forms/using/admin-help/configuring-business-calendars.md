---
title: Configurazione dei calendari aziendali
seo-title: Configurazione dei calendari aziendali
description: I calendari aziendali definiscono i giorni aziendali e non lavorativi per la tua organizzazione. Scoprite come configurare i calendari aziendali.
seo-description: I calendari aziendali definiscono i giorni aziendali e non lavorativi per la tua organizzazione. Scoprite come configurare i calendari aziendali.
uuid: 0ba610b8-72a8-480c-8783-70d98cbe890a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7a85e13d-4800-47c4-812a-5c6e2355298a
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d
workflow-type: tm+mt
source-wordcount: '1928'
ht-degree: 0%

---


# Configurazione dei calendari aziendali {#configuring-business-calendars}

*I* calendari aziendali definiscono i giorni lavorativi e non lavorativi (ad esempio, festività legali, fine settimana e giorni di chiusura della società) per la vostra organizzazione. Quando si utilizzano i calendari aziendali, AEM moduli ignora i giorni non lavorativi durante l&#39;esecuzione di determinati calcoli di data. In Workbench è possibile specificare se utilizzare i calendari aziendali per gli eventi associati all&#39;utente, ad esempio promemoria di attività, scadenze ed escalation o per azioni non associate a utenti, come Eventi timer e Servizio di attesa.

Ad esempio, un promemoria attività è configurato per essere eseguito tre giorni lavorativi dopo l&#39;assegnazione dell&#39;attività a un utente. Il compito è assegnato giovedì. Tuttavia, i tre giorni seguenti non sono giorni lavorativi perché il venerdì è una festa nazionale e i due giorni successivi sono giorni di fine settimana. Il promemoria viene pertanto inviato mercoledì della settimana successiva.

>[!NOTE]
>
>Quando si calcolano date e ore utilizzando i calendari aziendali, AEM moduli utilizzano la data e l&#39;ora del server in cui è in esecuzione e non si adatta alla differenza tra i fusi orari. Ad esempio, se un promemoria attività è pianificato per le 10:00 su un server in esecuzione a Londra, ma l&#39;utente che riceve il promemoria si trova a New York City, l&#39;utente riceve il promemoria alle 5:00 ora locale.

## Utilizzo del calendario aziendale predefinito {#using-the-default-business-calendar}

AEM moduli fornisce un calendario aziendale predefinito (denominato *Calendario predefinito*) che indica i sabati e le domeniche come giorni non lavorativi. Se tutti gli utenti della tua organizzazione hanno gli stessi giorni non lavorativi, puoi aggiornare il calendario aziendale predefinito in base alla tua organizzazione. Se si utilizza solo il calendario aziendale predefinito, non è necessario abilitare i calendari aziendali in Gestione utente o fornire mappature. Se non sono definiti altri calendari aziendali, AEM moduli utilizza il calendario aziendale predefinito.

## Impostazione di più calendari aziendali {#setting-up-multiple-business-calendars}

Se alcuni utenti dell&#39;organizzazione hanno giorni diversi da quelli lavorativi, è possibile definire più calendari aziendali e configurare mappature che consentano una risoluzione runtime di un calendario aziendale per un utente.

### Definire più calendari aziendali {#define-multiple-business-calendars}

1. Decidete come associare il calendario aziendale appropriato a un utente. Esistono due modi per associare un calendario aziendale a un utente:

   **iscrizione a un gruppo:** potete assegnare un calendario aziendale a un utente in base all’appartenenza a un gruppo dell’utente. In questo caso, ogni utente del gruppo utilizzerà lo stesso calendario aziendale.

   Se un utente è membro di due diversi gruppi e tali gruppi sono mappati su due calendari aziendali diversi, AEM moduli utilizzeranno il primo calendario trovato nei risultati di ricerca. In questo caso, è consigliabile utilizzare le chiavi del calendario aziendale per associare gli utenti ai calendari aziendali.

   **Chiavi del calendario aziendale:** puoi assegnare un calendario aziendale a un utente in base a una chiave del calendario aziendale, che è un&#39;impostazione specificata in Gestione utente. Quindi, mappare la chiave del calendario aziendale su un calendario aziendale nel flusso di lavoro dei moduli.

   Il modo in cui assegnate le chiavi del calendario aziendale agli utenti dipende dal dominio Enterprise, locale o ibrido utilizzato. Per informazioni dettagliate sulla configurazione dei domini, vedere [Aggiunta di domini](/help/forms/using/admin-help/adding-domains.md#adding-domains).

   Se utilizzate un dominio locale o ibrido, le informazioni sugli utenti vengono memorizzate solo nel database Gestione utente. Per impostare la chiave del calendario aziendale per questi utenti, immettete una stringa nel campo Chiave del calendario aziendale quando aggiungete o modificate un utente in Gestione utente. (Vedere [Aggiunta e configurazione di utenti](/help/forms/using/admin-help/adding-configuring-users.md#adding-and-configuring-users).) È quindi possibile mappare le chiavi del calendario aziendale (le stringhe) ai calendari aziendali nel flusso di lavoro dei moduli. (Vedere [Mappatura di utenti e gruppi in un calendario aziendale](configuring-business-calendars.md#mapping-users-and-groups-to-a-business-calendar).)

   Se utilizzate un dominio Enterprise, le informazioni sugli utenti risiedono in un sistema di storage di terze parti, come una directory LDAP, che Gestione utente sincronizza con il database Gestione utenti. Questo consente di mappare una chiave del calendario aziendale su un campo presente nella directory LDAP. Ad esempio, se ogni record utente nella directory contiene un campo &quot;paese&quot; e si desidera assegnare calendari aziendali in base al paese in cui si trova l&#39;utente, specificare il nome del campo &quot;paese&quot; nel campo Chiave calendario aziendale quando si specificano le impostazioni utente per la directory. (Vedere [Configurazione delle directory](/help/forms/using/admin-help/configuring-directories.md#configuring-directories).) È quindi possibile mappare le chiavi del calendario aziendale (i valori definiti per il campo &quot;paese&quot; nella directory LDAP) ai calendari aziendali nel flusso di lavoro dei moduli. (Vedere [Mappatura di utenti e gruppi in un calendario aziendale](configuring-business-calendars.md#mapping-users-and-groups-to-a-business-calendar).)

1. Nel flusso di lavoro dei moduli, definire un calendario per ciascun set di utenti che condividono gli stessi giorni non lavorativi. (Vedere [Creare o aggiornare un calendario aziendale](configuring-business-calendars.md#create-or-update-a-business-calendar).)
1. Nel flusso di lavoro dei moduli, mappare le chiavi del calendario aziendale o le appartenenze al gruppo per ciascun calendario. (Vedere [Mappatura di utenti e gruppi in un calendario aziendale](configuring-business-calendars.md#mapping-users-and-groups-to-a-business-calendar).)
1. In Workbench, lo sviluppatore del processo sceglie se utilizzare i calendari aziendali per promemoria, scadenze ed escalation. (Vedere [Guida di Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

   Se lo sviluppatore del processo sceglie di utilizzare i calendari aziendali, AEM moduli selezioneranno in modo dinamico il calendario aziendale appropriato in base all&#39;impostazione Gestione utente e alle mappature del calendario aziendale definite in Admin Console oppure, in assenza di mappature, utilizzerà il calendario predefinito.

   Se lo sviluppatore del processo non utilizza calendari aziendali, il calcolo della data per l&#39;evento considera ogni giorno come un giorno lavorativo. Ad esempio, una scadenza dell&#39;attività è configurata per essere eseguita tre giorni dopo l&#39;assegnazione dell&#39;attività a un utente. Il compito è assegnato giovedì. La scadenza dell&#39;attività si verifica di domenica, anche se è un fine settimana.

## Creare o aggiornare un calendario aziendale {#create-or-update-a-business-calendar}

Se la vostra organizzazione contiene diversi set di utenti che hanno giorni diversi da quelli lavorativi, potete definire più calendari aziendali. È inoltre possibile modificare i calendari esistenti, incluso il calendario predefinito fornito con AEM moduli.

>[!NOTE]
>
>Se non si crea un nuovo calendario aziendale, verrà utilizzato quello predefinito.

1. Nella console di amministrazione, fate clic su Servizi > Flusso di lavoro Forms > Calendari aziendali.
1. Per aggiungere un nuovo calendario aziendale, fare clic su ![bus_cal_plus](assets/bus_cal_plus.png). Il testo *Nuovo calendario* viene visualizzato nell&#39;elenco a discesa. Selezionare il testo e digitare un altro nome per il calendario.

   Per modificare un calendario aziendale esistente, selezionatelo dall&#39;elenco a discesa.

1. In Giorni non lavorativi predefiniti, selezionate tutti i giorni non lavorativi settimanali, ad esempio i fine settimana.
1. [] Facoltativo: selezionare Usa ore lavorative e specificare l&#39;ora iniziale e finale per i giorni lavorativi.

   Se si seleziona questa opzione, un evento che si verifica prima dell&#39;intervallo di tempo specificato viene spostato all&#39;inizio dell&#39;intervallo di tempo e un evento che si verifica dopo l&#39;intervallo di tempo viene spostato all&#39;ora di inizio del giorno lavorativo successivo.

   Ad esempio, si consideri una situazione in cui a un utente viene assegnata un&#39;attività alle 2:00 di un martedì e il promemoria per tale attività è impostato su due giorni lavorativi. Senza l&#39;orario di lavoro, il promemoria si sarebbe verificato alle 2:00 di giovedì. Se le ore di lavoro sono impostate alle 8:00-17:00, il promemoria verrà inviato alle 8:00 di giovedì. Senza l&#39;orario di lavoro, se un evento promemoria è stato creato alle 18:00 di martedì, il promemoria si verificava dopo l&#39;orario di lavoro di giovedì. Con le ore di ufficio impostate alle 8:00-17:00, il promemoria si verificherà alle 8:00 di venerdì.

1. Nel calendario a sinistra, fate doppio clic su qualsiasi altro giorno non lavorativo, ad esempio festività. Non è possibile selezionare i giorni passati. I giorni non lavorativi selezionati vengono visualizzati in un elenco a destra, con la data che appare due volte su una sola riga. Selezionare la data a sinistra per digitare il nome o la descrizione per la giornata non lavorativa.

   Per rimuovere una giornata non lavorativa dall&#39;elenco, fare clic su ![bus_cal_trash](assets/bus_cal_trash.png) accanto al giorno.

1. [] Facoltativo: se il calendario deve essere il calendario predefinito, selezionare Calendario predefinito. Il calendario predefinito viene utilizzato quando non esiste altra mappatura del calendario per gli eventi associati all&#39;utente o non viene specificato alcun calendario aziendale per l&#39;evento timer o il servizio di attesa. Non è possibile eliminare il calendario predefinito.
1. Al termine della definizione dei giorni non lavorativi, selezionare Calendario abilitato per attivarlo, quindi fare clic su Salva.

   Se si sta aggiornando un calendario esistente, la nuova versione prende effetto immediatamente e viene utilizzata per tutti i calcoli del calendario aziendale, anche per le attività già in esecuzione.

   >[!NOTE]
   >
   >Se non si abilita il calendario, verrà utilizzato il calendario predefinito.

## Mappatura di utenti e gruppi in un calendario aziendale {#mapping-users-and-groups-to-a-business-calendar}

Esistono due metodi che è possibile utilizzare per associare un calendario aziendale a un utente. È possibile assegnare calendari aziendali agli utenti in base a una chiave del calendario aziendale o in base al gruppo di directory a cui appartiene l&#39;utente. È possibile utilizzare la scheda Mapping per specificare il metodo da utilizzare AEM moduli, nonché per mappare le chiavi e i gruppi del calendario aziendale ai calendari aziendali. Per informazioni dettagliate sull&#39;associazione delle chiavi del calendario aziendale agli utenti, vedere [Impostazione di più calendari aziendali](configuring-business-calendars.md#setting-up-multiple-business-calendars).

### Associare i calendari aziendali agli utenti in base alle chiavi del calendario aziendale {#associate-business-calendars-with-users-based-on-business-calendar-keys}

1. Nella console di amministrazione, fare clic su Servizi > flusso di lavoro moduli > Calendari aziendali, quindi fare clic sulla scheda Mappatura.
1. Nell&#39;elenco System Will Use (Sistema che utilizzerà), selezionare User Manager Business Calendar Key Resolution.
1. Selezionare Visualizza chiave calendario aziendale User Manager. Viene visualizzato un elenco contenente un set univoco di chiavi del calendario aziendale definite in Gestione utente.

   Per i domini locali e ibridi, l&#39;elenco visualizza i valori immessi nel campo Chiave calendario aziendale in Gestione utente. Per i domini Enterprise (LDAP), l’elenco visualizza il set univoco restituito dal campo LDAP (ad esempio, &quot;paese&quot;) configurato nelle impostazioni del dominio LDAP.

   Se l&#39;amministratore di Gestione utenti non ha definito alcuna chiave del calendario aziendale, l&#39;elenco sarà vuoto.

1. Per ogni elemento nell&#39;elenco delle chiavi del calendario aziendale di messaggistica unificata, selezionare un calendario.
1. Fate clic su Salva.

### Associare i calendari aziendali a utenti e gruppi in base ai gruppi di servizi di directory {#associate-business-calendars-with-users-and-groups-based-on-directory-service-groups}

1. Nella console di amministrazione, fare clic su Servizi > flusso di lavoro moduli > Calendari aziendali, quindi fare clic sulla scheda Mappatura.
1. Nell&#39;elenco System Will Use (Sistema utilizzato), selezionare Groups Defined By The Directory Server (Gruppi definiti dal server di directory).
1. Nella scheda Mapping, selezionare Visualizza gruppi di servizi directory. Viene visualizzato un elenco contenente i gruppi definiti in Gestione utente. (Vedere [Impostazioni directory](/help/forms/using/admin-help/configuring-directories.md#directory-settings).)

   >[!NOTE]
   >
   >In Workbench, se è stato configurato un servizio utente per l&#39;utilizzo di calendari aziendali e il servizio è assegnato a un gruppo, AEM moduli utilizzano le mappature di gruppo specificate qui per risolvere il calendario del gruppo. AEM moduli utilizza sempre le mappature dei gruppi per risolvere il calendario per i gruppi, anche quando si utilizzano le chiavi del calendario aziendale per risolvere il calendario per gli utenti. Se non viene trovata alcuna mappatura del gruppo, verrà utilizzato il calendario aziendale predefinito.

1. Selezionare un calendario per ogni elemento nell&#39;elenco Gruppo servizi directory.
1. Fate clic su Salva.

## Esportazione e importazione di calendari aziendali {#exporting-and-importing-business-calendars}

AEM moduli consente di esportare e importare i calendari aziendali come file XML. È possibile utilizzare questa funzione per spostare i calendari da un sistema di gestione temporanea a un sistema di produzione.

>[!NOTE]
>
>Questa funzione consente di esportare e importare tutti i calendari aziendali definiti, incluso il calendario aziendale predefinito fornito dai moduli AEM. Un calendario aziendale importato con lo stesso nome di un calendario esistente sovrascriverà il calendario esistente.

### Esportare i calendari aziendali {#export-business-calendars}

1. Nella console di amministrazione, fare clic su Servizi > Flusso di lavoro moduli > Calendari aziendali.
1. Fate clic su Esporta e salvate il file XML.

### Importa calendari aziendali {#import-business-calendars}

1. Nella console di amministrazione, fare clic su Servizi > Flusso di lavoro moduli > Calendari aziendali.
1. Fai clic su Importa.
1. Selezionate il file XML che contiene i calendari commerciali esportati e fate clic su Apri.

## Eliminare un calendario aziendale {#delete-a-business-calendar}

È possibile rimuovere eventuali calendari aziendali non più richiesti dalla propria organizzazione. Se si elimina un calendario aziendale ancora mappato a utenti e gruppi, verrà utilizzato il calendario predefinito.

1. Nella console di amministrazione, fate clic su Servizi > Flusso di lavoro Forms > Calendari aziendali.
1. Selezionare il calendario.
1. Fai clic su Elimina.

