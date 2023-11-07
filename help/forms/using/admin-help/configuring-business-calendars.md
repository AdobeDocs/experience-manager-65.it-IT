---
title: Configurazione dei calendari aziendali
description: I calendari aziendali definiscono i giorni lavorativi e non lavorativi per l'organizzazione. Scopri come configurare i calendari aziendali.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 4282718a-41f1-411a-9cd7-8c470005107d
source-git-commit: fc2f26a69c208947c14e8c6036825bb217901481
workflow-type: tm+mt
source-wordcount: '1898'
ht-degree: 0%

---

# Configurazione dei calendari aziendali {#configuring-business-calendars}

*Calendari aziendali* definisci i giorni lavorativi e non lavorativi (ad esempio, festività legali, fine settimana e giorni di chiusura della società) per la tua organizzazione. Quando si utilizzano i calendari aziendali, i moduli AEM saltano i giorni non lavorativi durante l’esecuzione di determinati calcoli di date. In Workbench è possibile specificare se utilizzare i calendari aziendali per gli eventi associati all&#39;utente, ad esempio promemoria di attività, scadenze e inoltri per livelli di priorità, oppure per le azioni non associate agli utenti, ad esempio Eventi timer e Servizio di attesa.

Ad esempio, un promemoria dell’attività è configurato per essere visualizzato tre giorni lavorativi dopo l’assegnazione dell’attività a un utente. L&#39;attività viene assegnata giovedì. Tuttavia, i tre giorni successivi non sono giorni lavorativi perché il venerdì è una festa nazionale e i due giorni successivi sono giorni festivi. Il promemoria è quindi inviato il mercoledì della prossima settimana.

>[!NOTE]
>
>Quando si calcolano le date e le ore utilizzando i calendari commerciali, i moduli AEM utilizzano la data e l&#39;ora del server in cui è in esecuzione e non si adeguano alla differenza tra i fusi orari. Ad esempio, se un promemoria attività è pianificato per le 10:00 su un server in esecuzione a Londra, ma l’utente che riceve il promemoria si trova a New York, riceverà il promemoria alle 5:00 ora locale.

## Utilizzo del calendario aziendale predefinito {#using-the-default-business-calendar}

I moduli AEM forniscono un calendario aziendale predefinito (denominato *Calendario incorporato*) che indica sabato e domenica come giorni non lavorativi. Se tutti gli utenti dell&#39;organizzazione hanno gli stessi giorni non lavorativi, è possibile aggiornare il calendario aziendale predefinito in base alle esigenze dell&#39;organizzazione. Quando si utilizza solo il calendario aziendale predefinito, non è necessario abilitare i calendari aziendali in Gestione utenti o fornire mapping. Quando non vengono definiti altri calendari aziendali, i moduli AEM utilizzano il calendario aziendale predefinito.

## Impostazione di più calendari aziendali {#setting-up-multiple-business-calendars}

Se alcuni utenti dell&#39;organizzazione dispongono di giorni non lavorativi diversi, è possibile definire più calendari aziendali e configurare mapping che consentano la risoluzione in fase di esecuzione di un calendario aziendale per un utente.

### Definizione di più calendari aziendali {#define-multiple-business-calendars}

1. Decidere come associare il calendario aziendale appropriato a un utente. Esistono due modi per associare un calendario aziendale a un utente:

   **Appartenenza al gruppo:** È possibile assegnare un calendario aziendale a un utente in base all&#39;appartenenza al gruppo dell&#39;utente. In questo caso, ogni utente del gruppo utilizzerà lo stesso calendario aziendale.

   Se un utente è membro di due gruppi diversi e tali gruppi sono mappati a due calendari aziendali diversi, i moduli AEM utilizzeranno il primo calendario individuato nei risultati di ricerca. In questo caso, è consigliabile utilizzare le chiavi del calendario aziendale per associare gli utenti ai calendari aziendali.

   **Chiavi calendario aziendale:** È possibile assegnare un calendario aziendale a un utente in base a una chiave del calendario aziendale, che è un&#39;impostazione specificata in Gestione utente. È quindi possibile mappare la chiave del calendario aziendale a un calendario aziendale nel flusso di lavoro di Forms.

   Il modo in cui si assegnano le chiavi del calendario aziendale agli utenti dipende dal fatto che si utilizzi un dominio enterprise, locale o ibrido. Per informazioni dettagliate sulla configurazione dei domini, consulta [Aggiunta di domini](/help/forms/using/admin-help/adding-domains.md#adding-domains).

   Se si utilizza un dominio locale o ibrido, le informazioni relative agli utenti vengono memorizzate solo nel database Gestione utenti. Per impostare la chiave del calendario aziendale per questi utenti, immettere una stringa nel campo Chiave del calendario aziendale quando si aggiunge o si modifica un utente in Gestione utente. (vedere [Aggiunta e configurazione di utenti](/help/forms/using/admin-help/adding-configuring-users.md#adding-and-configuring-users).) È quindi possibile mappare le chiavi del calendario aziendale (le stringhe) ai calendari aziendali nel flusso di lavoro dei moduli. (vedere [Mappatura di utenti e gruppi a un calendario aziendale](configuring-business-calendars.md#mapping-users-and-groups-to-a-business-calendar).)

   Se si utilizza un dominio enterprise, le informazioni sugli utenti risiedono in un sistema di storage di terze parti, ad esempio una directory LDAP, che User Management sincronizza con il database User Management. Questo consente di mappare una chiave del calendario aziendale a un campo nella directory LDAP. Ad esempio, se ogni record utente della directory contiene un campo &quot;paese&quot; e si desidera assegnare calendari aziendali in base al paese in cui si trova l&#39;utente, specificare il nome del campo &quot;paese&quot; nel campo Chiave calendario aziendale quando si specificano le impostazioni utente per la directory. (vedere [Configurazione delle directory](/help/forms/using/admin-help/configuring-directories.md#configuring-directories).) È quindi possibile mappare le chiavi del calendario aziendale (i valori definiti per il campo &quot;paese&quot; nella directory LDAP) ai calendari aziendali nel flusso di lavoro dei moduli. (vedere [Mappatura di utenti e gruppi a un calendario aziendale](configuring-business-calendars.md#mapping-users-and-groups-to-a-business-calendar).)

1. Nei flussi di lavoro dei moduli, definisci un calendario per ogni set di utenti che condividono gli stessi giorni non lavorativi. (vedere [Creare o aggiornare un calendario aziendale](configuring-business-calendars.md#create-or-update-a-business-calendar).)
1. Nel flusso di lavoro dei moduli, mappa le chiavi del calendario aziendale o le appartenenze ai gruppi per ogni calendario. (vedere [Mappatura di utenti e gruppi a un calendario aziendale](configuring-business-calendars.md#mapping-users-and-groups-to-a-business-calendar).)
1. In Workbench, lo sviluppatore del processo sceglie se utilizzare i calendari aziendali per promemoria, scadenze e riassegnazione. (vedere [Guida di Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

   Se lo sviluppatore del processo sceglie di utilizzare i calendari aziendali, i moduli AEM selezioneranno dinamicamente il calendario aziendale appropriato in base all&#39;impostazione Gestione utente e ai mapping del calendario aziendale definiti in Administration Console oppure, se non esistono mapping, utilizzeranno il calendario predefinito.

   Se lo sviluppatore del processo non utilizza calendari aziendali, il calcolo della data per l&#39;evento considera ogni giorno come giorno lavorativo. Ad esempio, la scadenza di un’attività è configurata in modo che sia tre giorni dopo che l’attività è stata assegnata a un utente. L&#39;attività viene assegnata giovedì. La scadenza dell’attività è domenica, anche se si tratta di un fine settimana.

## Creare o aggiornare un calendario aziendale {#create-or-update-a-business-calendar}

Se l&#39;organizzazione contiene diversi gruppi di utenti che hanno giorni non lavorativi diversi, è possibile definire più calendari aziendali. È inoltre possibile modificare i calendari esistenti, incluso il calendario predefinito fornito con i moduli AEM.

>[!NOTE]
>
>Se non si crea un calendario aziendale, verrà utilizzato il calendario predefinito.

1. Nella console di amministrazione, fai clic su Servizi > Flusso di lavoro di Forms > Calendari aziendali.
1. Per aggiungere un nuovo calendario aziendale, fare clic su ![bus_cal_plus](assets/bus_cal_plus.png). Il testo *Nuovo calendario* nell&#39;elenco a discesa. Selezionare il testo e digitare un altro nome per il calendario.

   Per modificare un calendario aziendale esistente, selezionarlo dall&#39;elenco a discesa.

1. In Giorni non lavorativi predefiniti selezionare qualsiasi giorno non lavorativo settimanale, ad esempio i fine settimana.
1. [Facoltativo] Selezionare Usa l&#39;orario di ufficio e specificare l&#39;orario di inizio e di fine per i giorni lavorativi.

   Se si seleziona questa opzione, un evento che si verifica prima dell&#39;intervallo di tempo specificato viene spostato all&#39;inizio dell&#39;intervallo di tempo e un evento che si verifica dopo l&#39;intervallo di tempo viene spostato all&#39;ora di inizio del giorno lavorativo successivo.

   Consideriamo ad esempio la situazione in cui a un utente viene assegnata un’attività alle 02:00 del martedì e il promemoria per tale attività è impostato su due giorni lavorativi. Senza l’orario di lavoro, il promemoria verrà visualizzato alle 02:00 del giovedì. Se l’orario di lavoro è impostato sulle 8:00 alle 17:00, il promemoria verrà inviato alle 8:00 del giovedì. Senza orario di lavoro, se un evento di promemoria è stato creato alle 18:00 di martedì, il promemoria si verificherà dopo l’orario di lavoro di giovedì. Con l’orario di lavoro impostato sulle 08:00 alle 17:00, il promemoria verrà visualizzato alle 08:00 del venerdì.

1. Nel calendario a sinistra fare doppio clic su qualsiasi altro giorno non lavorativo, ad esempio festività. Non è possibile selezionare i giorni passati. I giorni non lavorativi selezionati vengono visualizzati in un elenco a destra, con la data visualizzata due volte su una riga. Selezionare la data a sinistra per digitare il nome o la descrizione del giorno non lavorativo.

   Per rimuovere un giorno non lavorativo dall&#39;elenco, fare clic su ![bus_cal_trash](assets/bus_cal_trash.png) accanto al giorno.

1. [Facoltativo] Se questo calendario deve essere quello predefinito, selezionare Calendario predefinito. Il calendario predefinito viene utilizzato quando non esiste alcun altro mapping di calendario per gli eventi associati all&#39;utente o non è specificato alcun calendario aziendale per l&#39;evento timer o il servizio di attesa. Impossibile eliminare il calendario predefinito.
1. Dopo aver definito i giorni non lavorativi, selezionare Calendario abilitato per attivarlo e quindi fare clic su Salva.

   Se si aggiorna un calendario esistente, la nuova versione viene applicata immediatamente e viene utilizzata per tutti i calcoli del calendario aziendale, inclusi i task già in esecuzione.

   >[!NOTE]
   >
   >Se non si abilita il calendario, verrà utilizzato il calendario predefinito.

## Mappatura di utenti e gruppi a un calendario aziendale {#mapping-users-and-groups-to-a-business-calendar}

Per associare un calendario aziendale a un utente è possibile utilizzare due metodi. È possibile assegnare calendari aziendali agli utenti in base a una chiave del calendario aziendale o in base al gruppo di directory a cui appartiene l&#39;utente. La scheda Mapping consente di specificare il metodo che i moduli AEM utilizzeranno e di mappare le chiavi e i gruppi del calendario aziendale ai calendari aziendali. Per informazioni dettagliate sull&#39;associazione delle chiavi del calendario aziendale agli utenti, vedere [Impostazione di più calendari aziendali](configuring-business-calendars.md#setting-up-multiple-business-calendars).

### Associa calendari aziendali a utenti in base alle chiavi del calendario aziendale {#associate-business-calendars-with-users-based-on-business-calendar-keys}

1. Nella console di amministrazione, fare clic su Servizi > Flusso di lavoro moduli > Calendari aziendali, quindi fare clic sulla scheda Mappatura.
1. Nell&#39;elenco Sistema utilizzerà selezionare User Manager Business Calendar Key Resolution.
1. Selezionare Visualizza chiave calendario aziendale di User Manager. Viene visualizzato un elenco contenente un set univoco di chiavi del calendario aziendale definite in Gestione utente.

   Per i domini locali e ibridi, l&#39;elenco visualizza i valori immessi nel campo Chiave calendario aziendale in Gestione utente. Per i domini enterprise (LDAP), l&#39;elenco mostra il set univoco restituito dal campo LDAP (ad esempio, &quot;paese&quot;) configurato nelle impostazioni del dominio LDAP.

   Se l&#39;amministratore di User Management non ha definito alcuna chiave del calendario aziendale, l&#39;elenco sarà vuoto.

1. Per ogni elemento nell&#39;elenco Chiave calendario aziendale di messaggistica unificata, selezionare un calendario.
1. Fai clic su Salva.

### Associa calendari aziendali a utenti e gruppi in base ai gruppi di servizi di elenchi in linea {#associate-business-calendars-with-users-and-groups-based-on-directory-service-groups}

1. Nella console di amministrazione, fare clic su Servizi > Flusso di lavoro moduli > Calendari aziendali, quindi fare clic sulla scheda Mappatura.
1. Nell&#39;elenco System Will Use selezionare Groups Defined By The Directory Server (Gruppi definiti dal server delle directory).
1. Nella scheda Mapping selezionare Visualizza gruppi di servizi directory. Viene visualizzato un elenco contenente i gruppi definiti in Gestione utente. (vedere [Impostazioni directory](/help/forms/using/admin-help/configuring-directories.md#directory-settings).)

   >[!NOTE]
   >
   >In Workbench, se è stato configurato un servizio utente per l&#39;utilizzo dei calendari aziendali e il servizio è assegnato a un gruppo, i moduli AEM utilizzano i mapping dei gruppi qui specificati per risolvere il calendario del gruppo. I moduli AEM utilizzano sempre i mapping dei gruppi per risolvere il calendario dei gruppi, anche quando si utilizzano le chiavi del calendario aziendale per risolvere il calendario degli utenti. Se non viene trovato alcun mapping di gruppo, viene utilizzato il calendario aziendale predefinito.

1. Per ogni elemento nell&#39;elenco Gruppo di servizi directory, selezionare un Calendario.
1. Fai clic su Salva.

## Esportazione e importazione di calendari commerciali {#exporting-and-importing-business-calendars}

I moduli AEM consentono di esportare e importare i calendari aziendali come file XML. È possibile utilizzare questa funzione per spostare i calendari da un sistema di gestione temporanea a un sistema di produzione.

>[!NOTE]
>
>Questa funzione esporta e importa tutti i calendari aziendali definiti, incluso il calendario aziendale predefinito fornito dai moduli AEM. Un calendario aziendale importato con lo stesso nome di un calendario esistente sovrascrive il calendario esistente.

### Esporta calendari commerciali {#export-business-calendars}

1. Nella console di amministrazione, fare clic su Servizi > Flusso di lavoro moduli > Calendari aziendali.
1. Fare clic su Esporta e salvare il file XML.

### Importa calendari commerciali {#import-business-calendars}

1. Nella console di amministrazione, fare clic su Servizi > Flusso di lavoro moduli > Calendari aziendali.
1. Fai clic su Importa.
1. Selezionare il file XML contenente i calendari aziendali esportati e fare clic su Apri.

## Eliminare un calendario aziendale {#delete-a-business-calendar}

È possibile rimuovere i calendari aziendali non più necessari per l&#39;organizzazione. Se si elimina un calendario aziendale ancora mappato a utenti e gruppi, viene utilizzato il calendario predefinito.

1. Nella console di amministrazione, fai clic su Servizi > Flusso di lavoro di Forms > Calendari aziendali.
1. Seleziona il calendario.
1. Fai clic su Elimina.
