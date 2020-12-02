---
title: Funzione calendario
seo-title: Funzione calendario
description: Fornisce informazioni sull'evento community in un formato calendario
seo-description: Fornisce informazioni sull'evento community in un formato calendario
uuid: 262f6afa-d8aa-4815-8440-a8ed5668c76d
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 70fa0b9c-cb98-45c4-9c94-bef4a9f3741e
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1170'
ht-degree: 7%

---


# Funzione calendario {#calendar-feature}

## Introduzione {#introduction}

La funzione di calendario supporta la fornitura di informazioni sull&#39;evento community in formato calendario a tutti i visitatori del sito o solo ai visitatori del sito (membri della community), mentre solo i membri autorizzati possono aggiungere eventi.

Questa sezione della documentazione descrive

* Aggiunta della funzione calendario a un sito AEM
* Impostazioni di configurazione per i componenti `Calendar`

## Aggiunta di un calendario a una pagina {#adding-a-calendar-to-a-page}

Per aggiungere un componente `Calendar` a una pagina in modalità di creazione, usate il browser componenti per individuare

* `Communities / Calendar`

e trascinarlo nella posizione desiderata su una pagina, ad esempio una posizione relativa alla funzione che gli utenti potranno rivedere.

Per le informazioni necessarie, visitare [Community Components Basics](/help/communities/basics.md).

Quando vengono incluse le [librerie lato client ](/help/communities/calendar-basics-for-developers.md#essentials-for-client-side), viene visualizzato il componente `Calendar`.

![calendario-componente](assets/calendar-component.png)

### Configurazione del calendario {#configuring-calendar}

Selezionare il componente `Calendar` inserito a cui accedere e selezionare l&#39;icona `Configure` che apre la finestra di dialogo di modifica.

![configure](assets/configure-new.png)

![configure-Calendar](assets/configure-calendar1.png)

#### Scheda Impostazioni {#settings-tab}

Nella scheda **Impostazioni**, specificare se consentire o meno l&#39;applicazione dei tag alle voci del calendario.

* **Eventi per pagina**

   Definisce il numero di eventi visualizzati per pagina. Il valore predefinito è 10.

* **Moderato**

   Se questa opzione è attivata, gli eventi di calendario e i commenti devono essere approvati prima che vengano visualizzati su un sito di pubblicazione. Il valore predefinito è deselezionato.

* **Chiuso**

   Se questa opzione è attivata, il calendario viene chiuso alle nuove voci e ai commenti dell&#39;evento. Il valore predefinito è deselezionato.

* **Editor Rich Text**

   Se questa opzione è attivata, è possibile inserire eventi e commenti del calendario con la marcatura. Il valore predefinito è selezionato.

* **Consenti assegnazione tag**

   Se questa opzione è selezionata, consentire ai membri di aggiungere etichette di tag agli eventi inseriti (vedere la scheda **Campo tag**). Il valore predefinito è selezionato.

* **Consenti caricamenti file**

   Se questa opzione è selezionata, consentire l&#39;aggiunta di allegati a un evento o commento del calendario. Il valore predefinito è selezionato.

* **Consenti Segui**

   Se questa opzione è selezionata, consentire ai membri di seguire gli eventi inviati al calendario. Il valore predefinito è selezionato.

* **Dimensione file massima**

   Rilevante solo se è selezionato `Allow File Uploads`. Questo campo limita la dimensione (in byte) di un file caricato. Il valore predefinito è 104857600 (10 Mb).

* **Tipi di file consentiti**

   Rilevante solo se è selezionato `Allow File Uploads`. Un elenco separato da virgole di estensioni di file con il separatore &quot;punto&quot;. Ad esempio: .jpg, .jpeg, .png, .doc, .docx, .pdf. Se vengono specificati dei tipi di file, non sarà possibile caricare quelli non specificati. Il valore predefinito non è specificato, pertanto tutti i tipi di file sono consentiti.

* **Dimensione massima per file immagine allegato**

   Pertinente solo se l&#39;opzione Consenti caricamenti file è selezionata. Numero massimo di byte di cui può disporre un file immagine caricato. Il valore predefinito è 2097152****(2 Mb).

* **Tipi di immagine di copertina consentiti**

   Elenco separato da virgole di estensioni di file immagine con il separatore &quot;punto&quot;. Il valore predefinito è `.jpg,.jpeg,.png,.gif,.bmp`.

* **Consenti risposte concatenate**

   Se questa opzione è selezionata, consentire le risposte ai commenti inviati all&#39;evento del calendario. Il valore predefinito è selezionato.

* **Consenti agli utenti di eliminare commenti ed eventi**

   Se questa opzione è selezionata, consentire ai membri di eliminare i commenti e gli eventi di calendario da essi inviati. Il valore predefinito è** **selezionato.

* **Consenti votazione**

   Se questa opzione è selezionata, includete la funzione di votazione con un evento del calendario. Il valore predefinito è selezionato.

* **Mostra breadcrumb**

   Mostra breadcrumb su pagina eventi. Il valore predefinito è selezionato.

* **Filtro intervallo di date**

   Definisce il numero di giorni aggiunti alla data corrente al fine di calcolare il valore &quot;A&quot; del filtro della pagina di elenco eventi del calendario. Il numero predefinito è 30.

* **Consenti contenuto in primo piano**

   Se questa opzione è selezionata, l&#39;idea può essere identificata come [contenuto in evidenza](/help/communities/featured.md). Il valore predefinito è deselezionato.

Nella scheda **Moderazione utente**, specificare la modalità di gestione degli argomenti e delle risposte inviati (contenuto generato dall&#39;utente). Per ulteriori informazioni, vedere [Moderazione dei contenuti generati dall&#39;utente](/help/communities/moderate-ugc.md).

#### Scheda Moderazione utente {#user-moderation-tab}

* **Rifiuta post**

   Se questa opzione è attivata, i moderatori di membri attendibili potranno negare i post e impedirne la visualizzazione nel forum pubblico. Il valore predefinito è selezionato.

* **Chiudi/Riapri eventi**

   Se questa opzione è attivata, i moderatori dei membri attendibili possono chiudere un evento per apportare ulteriori modifiche e commenti e riaprire un evento. Il valore predefinito è selezionato.

* **Segnala post**

   Se questa opzione è selezionata, consentire ai membri di contrassegnare eventi o commenti di altri utenti come inappropriati. Il valore predefinito è selezionato.

* **Elenco di motivi per segnalazione**

   Se questa opzione è selezionata, consentite ai membri di scegliere, da un elenco a discesa, il motivo per cui l&#39;evento è contrassegnato o il commento è inappropriato. Il valore predefinito è deselezionato.

* **Motivo per segnalazione personalizzato**

   Se questa opzione è selezionata, consentite ai membri di inserire il proprio motivo per cui un evento o un commento è contrassegnato come inappropriato. Il valore predefinito è deselezionato.

* **Soglia moderazione**

   Immettete il numero di volte in cui un evento o un commento deve essere contrassegnato dai membri prima che i moderatori siano informati. Il valore predefinito è 1 (una volta).

* **Limite segnalazione**

   Immettete il numero di volte in cui un evento o un commento deve essere contrassegnato prima che venga nascosto dalla visualizzazione pubblica. Se è impostato su -1, l&#39;argomento o il commento contrassegnato non viene mai nascosto dalla visualizzazione pubblica. In caso contrario, questo numero deve essere maggiore o uguale alla soglia di moderazione. Il valore predefinito è 5.

#### Scheda Campo tag {#tag-field-tab}

Nella scheda **Tag field** (Campo tag), i tag che possono essere applicati, se consentiti nella scheda **Settings** (Impostazioni), sono limitati in base agli spazi dei nomi scelti.

* **Namespace consentiti**

   Pertinente se `Allow Tagging` è selezionato nella scheda **Settings**. I tag che possono essere applicati sono limitati a quelli all&#39;interno delle categorie dello spazio nomi selezionate. L’elenco degli spazi dei nomi include &quot;Tag standard&quot; (lo spazio dei nomi predefinito) e &quot;Includi tutti i tag&quot;. Il valore predefinito non è selezionato, il che significa che tutti gli spazi dei nomi sono consentiti.

* **Limite di suggerimenti**

   Immettete il numero di tag da visualizzare come suggerimento al membro che invia il messaggio al forum. Il valore predefinito è **-**1 (nessun limite).

>[!NOTE]
>
>Per informazioni su come aggiungere un nuovo spazio nomi tag (tassonomia), visitare [Administering Tags](/help/sites-administering/tags.md).

#### Scheda Traduzione {#translation-tab}

Nella scheda **Translation**, se la traduzione è abilitata per il sito della community, è possibile impostare la traduzione in modo da tradurre l&#39;intero thread (evento e commenti) invece di post specifici.

* **Traduci tutto**

   Se questa opzione è attivata, l&#39;evento e i commenti vengono tradotti nella lingua preferita dell&#39;utente. Il valore predefinito è selezionato.

## Esperienza visitatori del sito {#site-visitor-experience}

Nell&#39;ambiente di pubblicazione, la funzione calendario visualizzerà un campo di ricerca con un intervallo di date predefinito, nonché tutti gli eventi di calendario che rientrano in tale intervallo.

Quando viene selezionato un evento del calendario, vengono visualizzati i dettagli, la descrizione e i commenti dell&#39;evento del calendario.

Altre capacità dipendono dal fatto che il visitatore del sito sia un moderatore, un amministratore, un membro della community, un membro privilegiato o un utente anonimo.

### Moderatori e amministratori {#moderators-and-administrators}

Quando l&#39;utente che ha effettuato l&#39;accesso dispone di privilegi di moderatore o amministratore, può eseguire [attività di moderazione](/help/communities/moderate-ugc.md) (come consentito dalla configurazione del componente) su tutti gli eventi del calendario e i commenti pubblicati su un evento.

![moderatori-vista](assets/moderators-view.png)

#### Membri {#members}

Quando l&#39;utente che ha effettuato l&#39;accesso è un membro della community o un membro [privilegiato](/help/communities/users.md#privileged-members-group) (a seconda della configurazione), è in grado di selezionare `New Event` per creare e pubblicare un nuovo evento del calendario.

In particolare, essi possono:

* Creazione di un nuovo evento del calendario
* Pubblicare un commento su un evento del calendario
* Modifica di un proprio evento o commento calendario
* Elimina un proprio evento o commento calendario
* Contrassegnare eventi o commenti di calendario di altri utenti

![create-event](assets/configure-calendar2.png)

![event-post](assets/configure-calendar3.png)

#### Anonimo {#anonymous}

I visitatori del sito che non hanno effettuato l&#39;accesso possono solo leggere gli eventi del calendario postati, tradurli se supportati, ma non possono aggiungere un evento o un commento né contrassegnare eventi o commenti di altri utenti.

![visualizzazione utente anonima](assets/anonymous-user-view1.png)

## Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili nella pagina [Calendar Essentials](/help/communities/calendar-basics-for-developers.md) per gli sviluppatori.

Per la moderazione degli eventi del calendario e dei commenti, vedere [Moderazione dei contenuti generati dall&#39;utente](/help/communities/moderate-ugc.md).

Per assegnare tag agli eventi del calendario e ai commenti, vedere [Assegnazione tag a contenuti generati dall&#39;utente](/help/communities/tag-ugc.md).

Per la traduzione di eventi e commenti del calendario, vedere [Traduzione di contenuti generati dall&#39;utente](/help/communities/translate-ugc.md).
