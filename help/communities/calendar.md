---
title: Funzione calendario
description: Scopri in che modo la funzione Calendario fornisce le informazioni sugli eventi community in formato calendario.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: c9b34b00-525d-4ca3-bd18-11bb7ce66787
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '1148'
ht-degree: 7%

---

# Funzione calendario {#calendar-feature}

## Introduzione {#introduction}

La funzione calendario supporta la possibilità di fornire informazioni sugli eventi community in formato calendario a tutti i visitatori del sito o solo ai visitatori del sito (membri della community), mentre solo i membri autorizzati possono aggiungere eventi.

Questa sezione della documentazione descrive

* Aggiunta della funzione calendario a un sito AEM
* Impostazioni di configurazione per `Calendar` componenti

## Aggiunta di un calendario a una pagina {#adding-a-calendar-to-a-page}

Per aggiungere una `Calendar` a una pagina in modalità di authoring, utilizza il browser Componenti per individuare

* `Communities / Calendar`

Trascinarlo nella posizione desiderata su una pagina, ad esempio una posizione relativa alla caratteristica da rivedere.

Per informazioni necessarie, visitare il sito [Nozioni di base sui componenti community](/help/communities/basics.md).

Quando [librerie lato client richieste](/help/communities/calendar-basics-for-developers.md#essentials-for-client-side) sono inclusi, è così che `Calendar` viene visualizzato.

![calendar-component](assets/calendar-component.png)

### Configurazione del calendario {#configuring-calendar}

Seleziona la inserita `Calendar` in modo da poter accedere e selezionare `Configure` che apre la finestra di dialogo per modifica.

![configura](assets/configure-new.png)

![configure-calendar](assets/configure-calendar1.png)

#### Scheda Impostazioni {#settings-tab}

Sotto **Impostazioni** , specificare se consentire l&#39;applicazione di tag alle voci del calendario.

* **Eventi per pagina**

  Definisce il numero di eventi visualizzati per pagina. Il valore predefinito è 10.

* **Moderato**

  Se questa opzione è selezionata, la pubblicazione di eventi e commenti del calendario deve essere approvata prima che vengano visualizzati in un sito pubblicato. L&#39;impostazione predefinita è deselezionata.

* **Chiuso**

  Se questa opzione è selezionata, il calendario viene chiuso alle nuove voci evento e ai nuovi commenti. L&#39;impostazione predefinita è deselezionata.

* **Editor Rich Text**

  Se questa opzione è selezionata, è possibile immettere eventi e commenti del calendario con il markup. Il valore predefinito è selezionato.

* **Consenti assegnazione tag**

  Se questa opzione è selezionata, consentire ai membri di aggiungere etichette tag agli eventi inseriti (vedere **Campo tag** ). Il valore predefinito è selezionato.

* **Consenti caricamenti file**

  Se questa opzione è selezionata, consenti l&#39;aggiunta di file allegati a un evento o a un commento del calendario. Il valore predefinito è selezionato.

* **Consenti Segui**

  Se questa opzione è selezionata, consentire ai membri di seguire gli eventi pubblicati nel calendario. Il valore predefinito è selezionato.

* **Dimensione file massima**

  Rilevante solo se `Allow File Uploads` è selezionato. Questo campo limita la dimensione (in byte) di un file caricato. Il valore predefinito è 104857600 (10 Mb).

* **Tipi di file consentiti**

  Rilevante solo se `Allow File Uploads` è selezionato. Un elenco separato da virgole di estensioni di file con il separatore &quot;punto&quot;. Ad esempio, .jpg, .jpeg, .png, .doc, .docx, .pdf. Se sono specificati dei tipi di file, non è possibile caricare quelli non specificati. Il valore predefinito è none specificato, pertanto tutti i tipi di file sono consentiti.

* **Dimensione massima per file immagine allegato**

  Rilevante solo se è selezionata l’opzione Consenti caricamenti file. Numero massimo di byte consentito per un file di immagine caricato. Il valore predefinito è 2097152** **(2 Mb).

* **Tipi di immagine di copertina consentiti**

  Elenco separato da virgole di estensioni di file immagine con il separatore &quot;punto&quot;. Il valore predefinito è `.jpg,.jpeg,.png,.gif,.bmp`.

* **Consenti risposte concatenate**

  Se questa opzione è selezionata, consenti le risposte ai commenti inviati all’evento calendario. Il valore predefinito è selezionato.

* **Consenti agli utenti di eliminare commenti ed eventi**

  Se questa opzione è selezionata, consentire ai membri di eliminare i commenti e gli eventi del calendario pubblicati. Il valore predefinito è selezionato.

* **Consenti votazione**

  Se questa opzione è selezionata, includere la funzionalità Votazione con un evento calendario. Il valore predefinito è selezionato.

* **Mostra breadcrumb**

  Mostra breadcrumb su pagina eventi. Il valore predefinito è selezionato.

* **Filtro intervallo di date**

  Definisce il numero di giorni aggiunti alla data corrente per calcolare il valore &quot;A&quot; del filtro della pagina di elenco degli eventi del calendario. Il numero predefinito è 30.

* **Consenti contenuto in primo piano**

  Se questa opzione è selezionata, l’idea è identificabile come [contenuto in primo piano](/help/communities/featured.md). L&#39;impostazione predefinita è deselezionata.

Sotto **Moderazione utenti** , specificare la modalità di gestione degli argomenti e delle risposte inviati (contenuto generato dall&#39;utente). Per ulteriori informazioni, consulta [Moderazione dei contenuti generati dagli utenti](/help/communities/moderate-ugc.md).

#### Scheda Moderazione utente {#user-moderation-tab}

* **Rifiuta post**

  Se questa opzione è selezionata, i moderatori membri di fiducia possono negare i post e impedirne la visualizzazione nel forum pubblico. Il valore predefinito è selezionato.

* **Chiudi/Riapri eventi**

  Se questa opzione è selezionata, i moderatori membri attendibili possono chiudere un evento per ulteriori modifiche e commenti e riaprire un evento. Il valore predefinito è selezionato.

* **Segnala post**

  Se questa opzione è selezionata, consentire ai membri di contrassegnare eventi o commenti di altri utenti come non appropriati. Il valore predefinito è selezionato.

* **Elenco di motivi per segnalazione**

  Se questa opzione è selezionata, consentire ai membri di scegliere, da un elenco a discesa, il motivo per cui contrassegnare un evento o un commento come non appropriato. L&#39;impostazione predefinita è deselezionata.

* **Motivo per segnalazione personalizzato**

  Se questa opzione è selezionata, consentire ai membri di immettere il proprio motivo per contrassegnare un evento o un commento come non appropriato. L&#39;impostazione predefinita è deselezionata.

* **Soglia moderazione**

  Immetti il numero di volte in cui un evento o un commento deve essere segnalato dai membri prima che il moderatore riceva una notifica. Il valore predefinito è 1 (una tantum).

* **Limite segnalazione**

  Immettere il numero di volte in cui un evento o un commento deve essere contrassegnato prima di essere nascosto dalla visualizzazione pubblica. Se è impostato su -1, l&#39;argomento o il commento contrassegnato non viene mai nascosto. Altrimenti, questo numero deve essere maggiore o uguale alla soglia di moderazione. Il valore predefinito è 5.

#### Scheda Campo tag {#tag-field-tab}

Sotto **Campo tag** , i tag che possono essere applicati, se consentito dalla scheda **Impostazioni** , sono limitati in base agli spazi dei nomi scelti.

* **Namespace consentiti**

  Pertinente se `Allow Tagging` è controllato nella sezione **Impostazioni** scheda. I tag che possono essere applicati sono limitati a quelli all’interno delle categorie dello spazio dei nomi selezionate. L’elenco degli spazi dei nomi include &quot;Tag standard&quot; (lo spazio dei nomi predefinito) e &quot;Includi tutti i tag&quot;. L’impostazione predefinita non è selezionata, il che significa che tutti gli spazi dei nomi sono consentiti.

* **Limite di suggerimenti**

  Immettere il numero di tag da visualizzare come suggerimento per la pubblicazione del membro nel forum. Il valore predefinito è **-**1 (nessun limite).

>[!NOTE]
>
>Visita [Amministrazione dei tag](/help/sites-administering/tags.md) dove puoi scoprire come aggiungere uno spazio dei nomi tag (tassonomia).

#### Scheda Traduzione {#translation-tab}

Sotto **Traduzione** Se è abilitata la traduzione per il sito community, la traduzione può essere impostata in modo da tradurre l’intero thread (evento e commenti) invece di post specifici.

* **Traduci tutto**

  Se questa opzione è selezionata, l’evento e i commenti vengono tradotti nella lingua preferita dell’utente. Il valore predefinito è selezionato.

## Esperienza visitatore del sito {#site-visitor-experience}

Nell’ambiente di pubblicazione, la funzione calendario visualizza un campo di ricerca con un intervallo di date predefinito ed eventuali eventi di calendario che rientrano in tale intervallo.

Quando viene selezionato un evento calendario, vengono visualizzati i dettagli, la descrizione e i commenti relativi all&#39;evento.

Altre funzionalità dipendono dal fatto che il visitatore del sito sia un moderatore, un amministratore, un membro della community, un membro con privilegi o un anonimo.

### Moderatori e amministratori {#moderators-and-administrators}

Quando l&#39;utente connesso dispone dei privilegi di moderatore o amministratore, è in grado di eseguire [attività di moderazione](/help/communities/moderate-ugc.md) (come consentito dalla configurazione del componente) su tutti gli eventi del calendario e i commenti pubblicati su un evento.

![moderators-view](assets/moderators-view.png)

#### Membri {#members}

Quando l&#39;utente connesso è un membro della community o [membro privilegiato](/help/communities/users.md#privileged-members-group) (a seconda della configurazione), è possibile selezionare `New Event` per creare e pubblicare un nuovo evento calendario.

In particolare, essi possono:

* Creare un evento calendario
* Pubblicare un commento in un evento calendario
* Modifica il proprio evento calendario o commento
* Eliminare il proprio evento calendario o commento
* Contrassegna eventi o commenti del calendario di altri utenti

![create-event](assets/configure-calendar2.png)

![post-evento](assets/configure-calendar3.png)

#### Anonimo {#anonymous}

I visitatori del sito che non hanno effettuato l&#39;accesso possono solo leggere gli eventi di calendario pubblicati, tradurli se supportati, ma non possono aggiungere un evento o un commento né contrassegnare eventi o commenti di altri utenti.

![anonymous-user-view](assets/anonymous-user-view1.png)

## Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili sul sito [Elementi di base di Calendar](/help/communities/calendar-basics-for-developers.md) pagina per sviluppatori.

Per la moderazione degli eventi e dei commenti del calendario, vedere [Moderazione dei contenuti generati dagli utenti](/help/communities/moderate-ugc.md).

Per assegnare tag agli eventi e ai commenti del calendario, vedere [Assegnazione di tag ai contenuti generati dagli utenti](/help/communities/tag-ugc.md).

Per la traduzione degli eventi e dei commenti del calendario, vedere [Traduzione dei contenuti generati dagli utenti](/help/communities/translate-ugc.md).
