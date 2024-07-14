---
title: Funzione forum
description: Scopri come aggiungere e configurare la funzione forum che fornisce un’area per i membri della community con accesso esterno per creare, visualizzare, seguire, cercare o rispondere ad argomenti.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 2b1a4917-9db6-436a-a5fd-c102fe41fb9d
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1233'
ht-degree: 1%

---

# Funzione forum{#forum-feature}

## Introduzione {#introduction}

La funzione forum fornisce un’area per i visitatori del sito connessi (membri della community) nell’ambiente Publish per:

* Crea argomenti
* Visualizza e rispondi agli argomenti
* Segui un argomento
* Cerca in un forum
* Contribuisci a moderare il contenuto del forum
* Spostare gli argomenti dei forum da una pagina a un&#39;altra

Questa sezione della documentazione descrive:

* Aggiunta della funzione forum a un sito AEM.
* Impostazioni di configurazione per il componente `Forum`.

### Aggiunta di un forum a una pagina {#adding-a-forum-to-a-page}

Per aggiungere un componente `Forum` a una pagina in modalità di creazione, utilizza il browser componenti per individuare

* `Communities / Forum`

e trascinarlo in una pagina in cui dovrebbe apparire il forum.

Per informazioni necessarie, visitare [Nozioni di base sui componenti delle community](/help/communities/basics.md).

Quando sono incluse le [librerie lato client richieste](/help/communities/essentials-forum.md#essentials-for-client-side), il componente `Forum` viene visualizzato in questo modo:

![componente forum](assets/forum-component.png)

### Configurazione di un forum {#configuring-a-forum}

Selezionare il componente `Forum` inserito in modo da poter accedere e selezionare l&#39;icona `Configure` che apre la finestra di dialogo per modifica.

![configura-nuovo](assets/configure-new.png)

![forum-config](assets/forum-config.png)

#### Scheda Impostazioni {#settings-tab}

Nella scheda **Impostazioni**, specifica le impostazioni per gli argomenti e le risposte:

* **Consenti miniatura allegato**

  Se questa opzione è selezionata, viene creata una miniatura dell&#39;immagine allegata.

* **Dimensione massima miniatura allegato**

  Dimensione massima (in pixel) dell&#39;immagine miniatura dell&#39;allegato. Il valore predefinito è 800 x 800.

* **Dimensioni minime immagine per miniatura**
* **Dimensione massima miniatura**

  Dimensione massima (in pixel) dell’immagine miniatura per l’immagine in linea. Il valore predefinito è 800 x 800.

* **Argomenti per pagina**

  Definisce il numero di topic/post mostrati per pagina. Impostazione predefinita: 10.

* **Moderato**

  Se questa opzione è selezionata, è necessario approvare la pubblicazione di argomenti e commenti prima di visualizzarli in un sito pubblicato. L&#39;impostazione predefinita è deselezionata.

* **Chiuso**

  Se questa opzione è selezionata, il forum verrà chiuso con nuovi argomenti e commenti. L&#39;impostazione predefinita è deselezionata.

* **Editor Rich Text**

  Se questa opzione è selezionata, è possibile immettere argomenti e commenti con il markup. L&#39;impostazione predefinita è deselezionata.

* **Consenti assegnazione tag**

  Se questa opzione è selezionata, consentire ai membri di aggiungere etichette tag ai propri post (vedere la scheda **Campo tag**). L&#39;impostazione predefinita è deselezionata.

* **Consenti caricamenti file**

  Se questa opzione è selezionata, consenti l&#39;aggiunta di file allegati all&#39;argomento o al commento. L&#39;impostazione predefinita è deselezionata.

* **Consenti Segui**

  Se questa opzione è selezionata, includere la funzionalità seguente per i post dei forum, che consente ai membri di ricevere [notifica](/help/communities/notifications.md) dei nuovi post. L&#39;impostazione predefinita è deselezionata.

* **Consenti blocco**

  Se questa opzione è selezionata, gli argomenti del forum possono essere bloccati nella parte superiore dell&#39;elenco. L&#39;impostazione predefinita è deselezionata.

* **Consenti contenuto in primo piano**

  Se questa opzione è selezionata, l&#39;idea è identificabile come [contenuto in primo piano](/help/communities/featured.md). L&#39;impostazione predefinita è deselezionata.

* **Consenti iscrizioni e-mail**

  Se questa opzione è selezionata, consenti ai membri di ricevere notifiche sui nuovi post tramite e-mail ([abbonamento](/help/communities/subscriptions.md)). Richiede `Allow Following` per essere controllato e [configurato](/help/communities/email.md). L&#39;impostazione predefinita è deselezionata.

* **Dimensione massima file**

  Rilevante solo se è selezionato `Allow File Uploads`. Questo campo limita la dimensione (in byte) di un file caricato. Il valore predefinito è 104857600 (10 Mb).

* **Tipi di file consentiti**

  Rilevante solo se è selezionato `Allow File Uploads`. Un elenco separato da virgole di estensioni di file con il separatore &quot;punto&quot;. Ad esempio, .jpg, .jpeg, .png, .doc, .docx, .pdf. Se sono specificati dei tipi di file, non è possibile caricare quelli non specificati. Il valore predefinito è none specificato, pertanto tutti i tipi di file sono consentiti.

* **Dimensione massima file immagine allegato**
Rilevante solo se è selezionata l’opzione Consenti caricamenti file. Numero massimo di byte consentito per un file di immagine caricato. Il valore predefinito è 2097152 (2 Mb).

* **Consenti risposte concatenate**

  Se questa opzione è selezionata, consenti le risposte ai commenti inviati all&#39;argomento. L&#39;impostazione predefinita è deselezionata.

* **Consenti votazione**

  Se questa opzione è selezionata, includere la funzionalità Votazione con un argomento. L&#39;impostazione predefinita è deselezionata.

* **Consenti agli utenti di eliminare commenti e argomenti**

  Se questa opzione è selezionata, consentire ai membri di eliminare i commenti e gli argomenti pubblicati. L&#39;impostazione predefinita è deselezionata.

* **Mostra breadcrumb**

  Se questa opzione è selezionata, mostra le breadcrumb di navigazione nelle pagine degli argomenti. Il valore predefinito è selezionato.

* **Distintivi visualizzati**

  Se selezionato, visualizza i [distintivi](/help/communities/implementing-scoring.md) ottenuti e assegnati con il post di blog di un membro. L&#39;impostazione predefinita è deselezionata.

* **Consenti membri privilegiati**

  Se questa opzione è selezionata, solo i membri con privilegi possono creare contenuto.

* **Membri privilegiati consentiti**

  Aggiungere i membri con privilegi autorizzati a creare il contenuto.

* **Blocca contenuto generato dall&#39;utente in modalità Modifica autore**

  Se questa opzione è abilitata, blocca i contenuti generati dagli utenti durante la modifica in modalità Creazione.

* **Abilita menzione**

  Se questa opzione è attivata, consente agli utenti registrati della community di identificare altri membri registrati (tramite nome, cognome, nome utente) e di assegnare loro tag utilizzando la sintassi @user-name comune. Gli utenti taggati ricevono notifiche sulle loro menzioni.

* **Max menzioni**

  Limita il numero massimo di menzioni consentite in un post. Il valore predefinito è 10.

* **Pattern menzioni interfaccia utente**

  Specifica la stringa di pattern consentita per assegnare tag (@mention) all’utente registrato in un post. Esempio: `~{{familyName}}{{givenName}}`.

>[!NOTE]
>
>Potrebbe essere necessario controllare sia `AllowThreaded Replies` che `Allow users to Delete Comments and Topics` per abilitare i commenti su un argomento.

#### Scheda Moderazione utente {#user-moderation-tab}

Nella scheda **Moderazione utente**, specifica come vengono gestiti gli argomenti e le risposte inviati (contenuti generati dall&#39;utente). Per ulteriori informazioni, vedere [Moderazione del contenuto generato dall&#39;utente](/help/communities/moderate-ugc.md).

* **Rifiuta post**

  Se questa opzione è selezionata, i moderatori membri di fiducia possono negare i post e impedirne la visualizzazione nel forum pubblico. L&#39;impostazione predefinita è deselezionata.

* **Chiudi/Riapri argomenti**

  Se questa opzione è selezionata, i moderatori membri attendibili possono chiudere un argomento per ulteriori modifiche e commenti e riaprire un argomento. L&#39;impostazione predefinita è deselezionata.

* **Sposta argomenti**

  Se questa opzione è selezionata, consenti ai moderatori sul lato pubblicazione di spostare gli argomenti. Il valore predefinito è selezionato.

* **Contrassegna post**

  Se questa opzione è selezionata, consentire ai membri di contrassegnare gli argomenti o i commenti di altri utenti come non appropriati. L&#39;impostazione predefinita è deselezionata.

* **Elenco motivi contrassegno**

  Se questa opzione è selezionata, consentire ai membri di scegliere, da un elenco a discesa, il motivo per cui contrassegnare un argomento o un commento come non appropriato. L&#39;impostazione predefinita è deselezionata.

* **Motivo contrassegno personalizzato**

  Se questa opzione è selezionata, consentire ai membri di immettere un motivo specifico per contrassegnare un argomento o un commento come non appropriato. L&#39;impostazione predefinita è deselezionata.

* **Soglia moderazione**

  Immettere il numero di volte in cui un argomento o un commento deve essere segnalato dai membri prima che il moderatore riceva una notifica. Il valore predefinito è 1 (una tantum).

* **Limite di segnalazione**

  Immettere il numero di volte in cui un argomento o un commento deve essere contrassegnato prima di essere nascosto dalla visualizzazione pubblica. Se è impostato su -1, l&#39;argomento o il commento contrassegnato non viene mai nascosto. Altrimenti, questo numero deve essere maggiore o uguale alla soglia di moderazione. Il valore predefinito è 5.

#### Scheda Campo tag {#tag-field-tab}

Nella scheda **Campo tag**, i tag che possono essere applicati, se consentiti nella scheda **Impostazioni**, sono limitati in base agli spazi dei nomi scelti.

* **Spazi dei nomi consentiti**

  Rilevante se `Allow Tagging` è selezionato nella scheda **Impostazioni**. I tag che possono essere applicati sono limitati a quelli all’interno delle categorie dello spazio dei nomi selezionate. L’elenco degli spazi dei nomi include &quot;Tag standard&quot; (lo spazio dei nomi predefinito) e &quot;Includi tutti i tag&quot;. L’impostazione predefinita non è selezionata, il che significa che tutti gli spazi dei nomi sono consentiti.

* **Limite suggerimenti**

  Immettere il numero di tag da visualizzare come suggerimento per la pubblicazione del membro nel forum. Il valore predefinito è **-**1 (nessun limite).

#### Scheda Traduzione {#translation-tab}

Nella scheda **Traduzione**, se la traduzione è abilitata per il sito community, è possibile impostare la traduzione per tradurre l&#39;intero argomento o i post selezionati.

* **Traduci tutto**

  Se questa opzione è selezionata, il thread del forum viene tradotto nella lingua preferita dell’utente. L&#39;impostazione predefinita è deselezionata.

#### Scheda Impostazioni ordinamento {#sort-settings-tab}

Nella scheda **Impostazioni ordinamento**, specifica l&#39;ordinamento dei commenti inviati quando vengono visualizzati.

* **Ordina per**

  Controllare tutte le selezioni di ordinamento consentite: `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. Il valore predefinito è `Newest, Oldest, Last Updated`.

* **Imposta come predefinito**

  Tirare verso il basso per selezionare una delle opzioni di ordinamento selezionate da visualizzare come impostazione predefinita. Il valore predefinito è `Newest`.

* **Selezionare le opzioni di tempo per l&#39;ordinamento di Analytics**

  Premere verso il basso per selezionare una delle opzioni seguenti: `All, Last 24 Hours, Last 7 Days, Last 30 Days`.

  Il valore predefinito è `All`.

### Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili nella pagina [Forum Essentials](/help/communities/essentials-forum.md) per sviluppatori.

Per la moderazione degli argomenti e dei commenti pubblicati, vedere [Moderazione dei contenuti generati dagli utenti](/help/communities/moderate-ugc.md).

Per assegnare tag agli argomenti e ai commenti pubblicati, vedere [Assegnazione di tag ai contenuti generati dagli utenti](/help/communities/tag-ugc.md).

Per la traduzione degli argomenti e dei commenti pubblicati, vedere [Traduzione di contenuti generati dall&#39;utente](/help/communities/translate-ugc.md).
