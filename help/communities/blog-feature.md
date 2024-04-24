---
title: Funzione blog
description: Scopri in che modo la funzione blog supporta la fornitura di informazioni sulla community in un formato di diario. Le voci vengono effettuate nell’ambiente di pubblicazione da utenti autorizzati.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 4650ac36-5506-4efc-be35-fac9e5a58f3d
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1696'
ht-degree: 0%

---

# Funzione blog {#blog-feature}

## Introduzione {#introduction}

La funzione blog per AEM Communities si è trasformata da attività di authoring a una vera e propria attività community che ha luogo nell’ambiente di pubblicazione.

La funzione blog supporta la fornitura di informazioni sulla community in formato di diario. I post di blog vengono inseriti nell’ambiente di pubblicazione da membri autorizzati (utenti registrati e connessi).

La funzione blog fornisce:

* Creazione lato pubblicazione di articoli e commenti sui blog
* Modifica Rich Text
* Immagini in linea (con supporto per il trascinamento della selezione)
* Contenuto di social network incorporato ([Supporto per incorporamento](/help/communities/blog-developer-basics.md#allowing-rich-media))
* Modalità bozza
* Pubblicazione pianificata
* Componi per conto (a [membro privilegiato](/help/communities/users.md#privileged-members-group) può creare contenuti per conto di un altro membro della community)
* [Moderazione in contesto e in blocco](/help/communities/moderate-ugc.md) di articoli di blog e commenti

Questa sezione della documentazione descrive:

* Aggiunta della funzione blog a un sito AEM
* Impostazioni di configurazione per i componenti blog

>[!NOTE]
>
>I componenti `Journal` e `Journal Sidebar` hanno titolo `Blog` e `Blog Sidebar`.
>
>La funzione blog disponibile in AEM 6.0 e nelle versioni precedenti è stata rimossa. Era basato su un modello e consentiva solo agli autori di creare contenuti nell’ambiente di authoring.

## Aggiunta di componenti blog a una pagina {#adding-blog-components-to-a-page}

Se desiderate aggiungere un blog a una pagina in modalità di creazione, utilizzate il browser Componenti per individuare

* `Communities / Blog`
* `Communities / Blog Sidebar`

Trascinali nella posizione in cui dovrebbe apparire il blog.

Per informazioni necessarie, visitare il sito [Nozioni di base sui componenti community](/help/communities/basics.md).

Quando [librerie lato client richieste](/help/communities/blog-developer-basics.md#essentials-for-client-side) sono inclusi, `Blog` Il componente viene visualizzato come segue:

![add-blog-component](assets/add-blog-component.png)

### Configurazione del blog {#configuring-blog}

Seleziona la inserita `Blog` in modo da poter accedere e selezionare `Configure` che apre la finestra di dialogo modifica.

![configura](assets/configure-new.png)

![Impostazioni blog](assets/blog-configure.png)

#### Scheda Impostazioni {#settings-tab}

Sotto **Impostazioni** , specificare le funzioni di base del blog:

* **Consenti miniatura allegato**

  Se questa opzione è selezionata, viene creata una miniatura dell&#39;immagine allegata.

* **Dimensione massima miniatura allegato**

  Dimensione massima (in pixel) dell&#39;immagine miniatura dell&#39;allegato. Il valore predefinito è 800 x 800.

* **Dimensioni minime immagine per miniatura**

  Dimensione minima (in byte) dell&#39;immagine per la generazione della miniatura per le immagini in linea. Il valore predefinito è 100000 byte (100 kb).

* **Dimensione massima miniatura**

  Dimensione massima (in pixel) dell’immagine miniatura per l’immagine in linea. Il valore predefinito è 800 x 800.

* **Consenti membri privilegiati**

  Se questa opzione è selezionata, solo i membri con privilegi possono creare contenuto.

* **Membri privilegiati consentiti**

  Aggiungere i membri con privilegi autorizzati a creare il contenuto.

* **Blocca i contenuti generati dall&#39;utente in modalità Modifica autore**

  Se questa opzione è abilitata, blocca i contenuti generati dagli utenti durante la modifica in modalità Creazione.

* **Titolo diario**

  Titolo del blog da visualizzare nella pagina.

>[!NOTE]
>
>Il titolo del diario viene utilizzato per creare automaticamente l&#39;URL per il blog.
>
>Vengono utilizzati al massimo 50 caratteri (con 5 caratteri aggiuntivi per l&#39;univocità) dal titolo del diario specificato qui per creare l&#39;URL per il blog.

* **Descrizione diario**

  Descrizione del blog.

* **Argomenti per pagina**

  Definisce il numero di post/commenti di blog mostrati per pagina. Il valore predefinito è 10.

* **Moderato**

  Se questa opzione è selezionata, è necessario approvare la pubblicazione di post di blog e commenti prima di visualizzarli in un sito pubblicato. L&#39;impostazione predefinita è deselezionata.

* **Chiuso**

  Se questa opzione è selezionata, il blog viene chiuso ai nuovi post e commenti. L&#39;impostazione predefinita è deselezionata.

* **Editor Rich Text**

  Se questa opzione è selezionata, è possibile immettere commenti e post di blog con markup. Il valore predefinito è selezionato.

* **Consenti assegnazione tag**

  Se questa opzione è selezionata, consentire ai membri di aggiungere etichette tag ai propri post (vedere **Campo tag** ). L&#39;impostazione predefinita è deselezionata.

* **Consenti caricamenti file**

  Se questa opzione è selezionata, consenti l&#39;aggiunta di file allegati a un post di blog o a un commento. L&#39;impostazione predefinita è deselezionata.

* **Dimensione massima file**

  Rilevante solo se `Allow File Uploads` è selezionato. Questo campo limita la dimensione (in byte) di un file caricato. Il valore predefinito è 104857600 (10 Mb).

* **Tipi di file consentiti**

  Rilevante solo se `Allow File Uploads` è selezionato. Un elenco separato da virgole di estensioni di file con il separatore &quot;punto&quot;. Ad esempio: .jpg, .jpeg, .png, .doc, .docx, .pdf. Se sono specificati dei tipi di file, non è possibile caricare quelli non specificati. Il valore predefinito è none specificato, pertanto tutti i tipi di file sono consentiti.

* **Dimensione massima file immagine allegato**

  Rilevante solo se è selezionata l’opzione Consenti caricamenti file. Numero massimo di byte consentito per un file di immagine caricato. Il valore predefinito è 2097152 (2 Mb).

* **Consenti risposte**

  Se questa opzione è selezionata, consenti le risposte ai commenti inviati al post di blog. L&#39;impostazione predefinita è deselezionata.

* **Consenti votazione**

  Se questa opzione è selezionata, includete la funzione Votazione con un post di blog. L&#39;impostazione predefinita è deselezionata.

* **Consenti agli utenti di eliminare commenti e argomenti**

  Se questa opzione è selezionata, consenti ai membri di eliminare i commenti e i post di blog pubblicati. L&#39;impostazione predefinita è deselezionata.

* **Consenti Segui**

  Se questa opzione è selezionata, includi la seguente funzione per gli articoli di blog, che consente ai membri di essere [notificato](/help/communities/notifications.md) di nuovi posti. L&#39;impostazione predefinita è deselezionata.

* **Consenti iscrizioni e-mail**

  Se questa opzione è selezionata, consenti ai membri di ricevere notifiche sui nuovi post tramite e-mail ([abbonamento](/help/communities/subscriptions.md)). Richiede `Allow Following` da controllare e [e-mail configurato](/help/communities/email.md). L&#39;impostazione predefinita è deselezionata.

* **Visualizza badge**

  Se questa opzione è selezionata, vengono visualizzati i risultati ottenuti e assegnati [badge](/help/communities/implementing-scoring.md) con il post di blog di un membro. L&#39;impostazione predefinita è deselezionata.

* **Non ricevere risposte nella pagina dell&#39;elenco**

* **Consenti contenuto in primo piano**

  Se questa opzione è selezionata, l’idea viene identificata come [contenuto in primo piano](/help/communities/featured.md). L&#39;impostazione predefinita è deselezionata.

* **Abilita menzione**

  Se questa opzione è attivata, consente agli utenti registrati della community di identificare altri membri registrati (tramite nome, cognome, nome utente) e di assegnare loro tag utilizzando la sintassi @user-name comune. Gli utenti taggati ricevono notifiche sulle loro menzioni.

* **Max menzioni**

  Limita il numero massimo di menzioni consentite in un post. Il valore predefinito è 10.

* **Pattern menzioni interfaccia utente**

  Specifica la stringa di pattern consentita per assegnare tag (@mention) all’utente registrato in un post. Esempio: `~{{familyName}}{{givenName}}`.

#### Scheda Moderazione utente {#user-moderation-tab}

Sotto **Moderazione utenti** , specificare le impostazioni di moderazione:

* **Rifiuta post**

  Se questa opzione è selezionata, i moderatori membri di fiducia possono negare i post e impedirne la visualizzazione nel forum pubblico. L&#39;impostazione predefinita è deselezionata.

* **Chiudi/Riapri argomenti**

  Se questa opzione è selezionata, i moderatori membri attendibili possono chiudere un argomento per ulteriori modifiche e commenti e riaprire un argomento. L&#39;impostazione predefinita è deselezionata.

* **Contrassegna post**

  Se questa opzione è selezionata, consentire ai membri di contrassegnare gli argomenti o i commenti di altri utenti come non appropriati. L&#39;impostazione predefinita è deselezionata.

* **Elenco motivi contrassegno**

  Se questa opzione è selezionata, consentire ai membri di scegliere, da un elenco a discesa, il motivo per cui contrassegnare un argomento o un commento come non appropriato. L&#39;impostazione predefinita è deselezionata.

* **Motivo contrassegno personalizzato**

  Se questa opzione è selezionata, consentire ai membri di immettere un motivo specifico per contrassegnare un argomento o un commento come non appropriato. L&#39;impostazione predefinita è deselezionata.

* **Soglia moderazione**

  Immettere il numero di volte in cui un argomento o un commento deve essere segnalato dai membri prima che il moderatore riceva una notifica. Il valore predefinito è 1 (una tantum).

* **Limite segnalazione**

  Immettere il numero di volte in cui un argomento o un commento deve essere contrassegnato prima di essere nascosto dalla visualizzazione pubblica. Se è impostato su -1, l&#39;argomento o il commento contrassegnato non viene mai nascosto. Altrimenti, questo numero deve essere maggiore o uguale alla soglia di moderazione. Il valore predefinito è 5.

#### Scheda Campo tag {#tag-field-tab}

Sotto **Campo tag** , specificare quali tag possono essere applicati se **Consenti assegnazione tag** è controllato il **Impostazioni** scheda :

* **Namespace consentiti**

  Pertinente se `Allow Tagging` è controllato nella sezione **Impostazioni** scheda. I tag che possono essere applicati sono limitati ai tag all’interno delle categorie dello spazio dei nomi selezionate. L’elenco degli spazi dei nomi include &quot;Tag standard&quot; (lo spazio dei nomi predefinito) e &quot;Includi tutti i tag&quot;. L’impostazione predefinita non è selezionata, il che significa che tutti gli spazi dei nomi sono consentiti.

* **Limite suggerimenti**

  Immettere il numero di tag da visualizzare come suggerimento per la pubblicazione del membro nel forum. Un valore pari a -1 indica nessun limite. Il valore predefinito è 0.

### Configurazione della barra laterale blog {#configuring-blog-sidebar}

Quando si fa doppio clic su `Blog Sidebar` componente, viene visualizzata una finestra di dialogo per modifica.

Sotto **Impostazioni barra laterale diario** , specificare il formato della data per gli archivi e il tipo di voci da visualizzare nella barra laterale:

![blog-component-sidebar](assets/blog-component-sidebar.png)

* **Formato data**

  Formato utilizzato per visualizzare gli archivi dei post di blog. Il formato utilizza i segnaposto seguendo la convenzione Java™.

   * aaaa : anno intero, come &#39;2015&#39;
   * aa : anno breve, come &#39;15&#39;
   * MMMM : mese intero, come giugno
   * MMM : mese breve, come giugno
   * MM: numero mese, ad esempio 06

  Il valore predefinito è &quot;yyyy MMMM&quot;, che visualizzerebbe, ad esempio, &quot;Giugno 2015&quot;

* **Tipo di visualizzazione**

  Titolo e tipo di post di blog da visualizzare nella barra laterale. La scelta è tra

   * Autori
   * Categorie
   * Archivi

* **Percorso componente blog**

  *(Facoltativo)* Posizione della risorsa blog da cui devono essere elencati gli articoli di blog. Se non specificato, viene utilizzato il componente resourceType `social/journal/components/hbs/journal` che viene visualizzato sulla stessa pagina.

   * Ad esempio `/content/sites/engage/en/blog/jcr:content/content/primary/blog`

* **Limite suggerimenti**

  Numero di articoli di blog da visualizzare. Un valore pari a -1 indica nessun limite. Il valore predefinito è -1.

## Esperienza visitatore del sito {#site-visitor-experience}

Nell&#39;ambiente di pubblicazione, la funzione blog mostra l&#39;articolo di blog più recente seguito da articoli di blog precedenti in ordine decrescente di creazione. Le barre laterali del blog consentono ai visitatori del sito di applicare filtri per limitare la selezione degli articoli di blog visualizzati.

L&#39;articolo del blog è seguito da un link per pubblicare o visualizzare commenti.

Quando si seleziona un articolo di blog, vengono visualizzati l&#39;articolo e i commenti (se abilitati).

Altre funzionalità dipendono dal fatto che il visitatore del sito sia un moderatore, un amministratore, un membro della community, un membro con privilegi o un anonimo.

### Utilizzo degli articoli {#working-with-articles}

Quando si crea un articolo di blog, è possibile scegliere di effettuare le seguenti operazioni:

1. Pubblica immediatamente
1. Pubblicare una bozza
1. Pubblica a una data e un’ora pianificate

Gli articoli del blog vengono visualizzati nella scheda appropriata (Pubblicato, Bozze o Pianificato) per i membri in grado di creare al momento della pubblicazione.

#### Moderatori e amministratori {#moderators-and-administrators}

Quando l&#39;utente connesso dispone dei privilegi di moderatore o amministratore, è in grado di eseguire [attività di moderazione](/help/communities/moderate-ugc.md) (come consentito dalla configurazione del componente) in tutti gli articoli e i commenti di blog pubblicati in un blog.

![moderator-homepage](assets/moderator-homepage.png)

#### Membri {#members}

Quando l&#39;utente connesso è un membro della community o [membro privilegiato](/help/communities/users.md#privileged-members-group) (a seconda della configurazione), è possibile selezionare `New Article` per creare e pubblicare un nuovo articolo di blog.

In particolare, essi possono:

* Creare un articolo di blog
* Pubblica un nuovo articolo di blog per conto di un altro membro
* Pubblica un commento su un articolo di blog
* Modifica il proprio articolo o commento sul blog
* Eliminare il proprio articolo o commento del blog
* Contrassegna gli articoli o i commenti di altri blog

![member-homepage](assets/member-homepage.png)

![create-blog](assets/create-blog.png)

#### Anonimo {#anonymous}

I visitatori del sito che non hanno effettuato l&#39;accesso possono solo leggere gli articoli e i commenti del blog pubblicati, tradurli se supportati, ma non possono aggiungere un articolo o un commento del blog né contrassegnare articoli o commenti di altri utenti.

![anonymous-user-view](assets/anonymous-user-view.png)

## Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili sul sito [Nozioni di base sul blog](/help/communities/blog-developer-basics.md) pagina per sviluppatori.

Per la moderazione dei post e dei commenti di blog, consultate [Moderazione dei contenuti generati dagli utenti](/help/communities/moderate-ugc.md).

Per assegnare tag ai post e ai commenti di blog, consultate [Assegnazione di tag ai contenuti generati dagli utenti](/help/communities/tag-ugc.md).

Per la traduzione di post e commenti di blog, vedi [Traduzione di contenuti generati dall&#39;utente](/help/communities/translate-ugc.md).
