---
title: Funzione blog
seo-title: Blog Feature
description: Informazioni della community in un formato di registrazione
seo-description: Community information in a journaling format
uuid: 7323063f-81e8-45c3-9035-bf7df6124830
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: cf8b3d72-30ba-40ca-ae48-b61abbb28802
docset: aem65
exl-id: 4650ac36-5506-4efc-be35-fac9e5a58f3d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1666'
ht-degree: 8%

---

# Funzione blog {#blog-feature}

## Introduzione {#introduction}

La funzione blog per AEM Communities si è trasformata da attività di authoring a una vera attività community che si svolge nell’ambiente di pubblicazione.

La funzione blog supporta la fornitura di informazioni sulla community in un formato di inserimento nel journal. Le voci di blog vengono effettuate nell&#39;ambiente di pubblicazione da membri autorizzati (utenti registrati e registrati).

La funzione blog fornisce :

* Creazione lato pubblicazione di articoli e commenti di blog
* Modifica RTF
* Immagini in linea (con supporto per trascinamento)
* Contenuto di social networking integrato ([Supporto oEmbed](/help/communities/blog-developer-basics.md#allowing-rich-media))
* Modalità Bozza
* Pubblicazione pianificata
* Composizione per conto terzi (a [membro privilegiato](/help/communities/users.md#privileged-members-group) può creare contenuti per conto di un membro della comunità diverso)
* [Moderazione contestuale e collettiva](/help/communities/moderate-ugc.md) articoli e commenti di blog

Questa sezione della documentazione descrive:

* Aggiunta della funzione blog a un sito AEM
* Impostazioni di configurazione per i componenti del blog

>[!NOTE]
>
>I componenti `Journal` e `Journal Sidebar` hanno titolo `Blog` e `Blog Sidebar`.
>
>La funzione blog disponibile nelle versioni AEM 6.0 e precedenti è stata rimossa. Era basato su un modello e consentiva solo agli autori di creare contenuti nell’ambiente di authoring.

## Aggiunta di componenti blog a una pagina {#adding-blog-components-to-a-page}

Se desideri aggiungere un blog a una pagina in modalità di authoring, utilizza il browser Componenti per individuare

* `Communities / Blog`
* `Communities / Blog Sidebar`

trascinateli nella posizione desiderata su una pagina in cui dovrebbe essere visualizzato il blog.

Per le informazioni necessarie, visita [Nozioni di base sui componenti di Communities](/help/communities/basics.md).

Quando il [librerie lato client richieste](/help/communities/blog-developer-basics.md#essentials-for-client-side) sono inclusi, è così che `Blog` apparirà il componente:

![componente per aggiungere un blog](assets/add-blog-component.png)

### Configurazione del blog {#configuring-blog}

Seleziona il `Blog` per accedere e selezionare il `Configure` che apre la finestra di dialogo di modifica.

![configurare](assets/configure-new.png)

![Impostazioni del blog](assets/blog-configure.png)

#### Scheda Impostazioni {#settings-tab}

Sotto la **Impostazioni** , specifica le funzioni di base del blog :

* **Consenti miniatura allegato**

   Se questa opzione è selezionata, viene creata una miniatura dell&#39;immagine allegata.

* **Dimensione max miniatura allegato**

   Dimensione massima (in pixel) dell&#39;immagine miniatura dell&#39;allegato. Il valore predefinito è 800 x 800.

* **Dimensioni minime immagine per miniatura**

   Dimensione minima (in byte) dell&#39;immagine per la generazione di miniature per le immagini in linea. Il valore predefinito è 100000 byte (100 kb).

* **Dimensione massima miniatura**

   Dimensione massima (in pixel) dell&#39;immagine in miniatura per l&#39;immagine in linea. Il valore predefinito è 800 x 800.

* **Consenti membri privilegiati**

   Se questa opzione è selezionata, solo i membri con privilegi possono creare contenuto.

* **Membri privilegiati consentiti**

   Aggiungi i membri con privilegi consentiti per creare contenuto.

* **Blocca i contenuti generati dagli utenti in modalità di modifica Creazione**

   Se attivato, blocca il contenuto generato dall’utente durante la modifica in modalità Autore.

* **Titolo diario**

   Titolo del blog da visualizzare sulla pagina.

>[!NOTE]
>
>Il Titolo del diario viene utilizzato per creare automaticamente l&#39;URL del blog.
>
>Dal titolo del giornale qui specificato viene utilizzato un massimo di 50 caratteri (con 5 caratteri aggiuntivi per l&#39;univocità) per creare l&#39;URL del blog.

* **Descrizione diario**

   Descrizione del blog.

* **Topic per pagina**

   Definisce il numero di post/commenti di blog visualizzati per pagina. Il valore predefinito è 10.

* **Moderato**

   Se questa opzione è selezionata, è necessario approvare i post e i commenti dei blog prima che vengano visualizzati su un sito pubblicato. Il valore predefinito è deselezionato.

* **Chiuso**

   Se selezionato, il blog viene chiuso a nuovi post e commenti del blog. Il valore predefinito è deselezionato.

* **Editor Rich Text**

   Se questa opzione è selezionata, è possibile inserire commenti e post di blog con tag. Il valore predefinito è selezionato.

* **Consenti assegnazione tag**

   Se questa opzione è selezionata, consenti ai membri di aggiungere etichette di tag al proprio post (consulta **Campo tag** ). Il valore predefinito è deselezionato.

* **Consenti caricamenti file**

   Se questa opzione è selezionata, consenti l&#39;aggiunta di allegati di file a un post di blog o a un commento. Il valore predefinito è deselezionato.

* **Dimensione file massima**

   Pertinente solo se `Allow File Uploads` è controllata. Questo campo limita le dimensioni (in byte) di un file caricato. Il valore predefinito è 104857600 (10 Mb).

* **Tipi di file consentiti**

   Pertinente solo se `Allow File Uploads` è controllata. Elenco di estensioni di file separate da virgola con il separatore &quot;punto&quot;. Ad esempio: .jpg, .jpeg, .png, .doc, .docx, .pdf. Se sono specificati dei tipi di file, non sarà possibile caricare quelli non specificati. Il valore predefinito non è specificato in modo che tutti i tipi di file siano consentiti.

* **Dimensione massima per file immagine allegato**

   Pertinente solo se l’opzione Consenti caricamenti file è selezionata. Numero massimo di byte di un file immagine caricato. Il valore predefinito è 2097152 (2 Mb).

* **Consenti risposte**

   Se questa opzione è selezionata, consenti risposte ai commenti pubblicati sul post di blog. Il valore predefinito è deselezionato.

* **Consenti votazione**

   Se questa opzione è selezionata, includi la funzionalità Voto con un post sul blog. Il valore predefinito è deselezionato.

* **Consenti agli utenti di eliminare commenti e argomenti**

   Se questa opzione è selezionata, consenti ai membri di eliminare i commenti e i post di blog che hanno pubblicato. Il valore predefinito è deselezionato.

* **Consenti Segui**

   Se questa opzione è selezionata, includi la seguente funzione per gli articoli di blog, che consente ai membri di essere [notificato](/help/communities/notifications.md) di nuovi posti. Il valore predefinito è deselezionato.

* **Consenti iscrizioni e-mail**

   Se questa opzione è selezionata, consente ai membri di ricevere notifiche sui nuovi post via e-mail ([abbonamento](/help/communities/subscriptions.md)). Richiede `Allow Following` da controllare e [e-mail configurata](/help/communities/email.md). Il valore predefinito è deselezionato.

* **Visualizza badge**

   Se selezionato, visualizza guadagnato e assegnato [badge](/help/communities/implementing-scoring.md) con il post di blog di un membro. Il valore predefinito è deselezionato.

* **Non ottenere risposte sulla pagina di elenco**

* **Consenti contenuto in primo piano**

   Se questa opzione è selezionata, l’idea può essere identificata come [contenuto in primo piano](/help/communities/featured.md). Il valore predefinito è deselezionato.

* **Abilita menzione**

   Se attivato, consente agli utenti della community registrata di identificare altri membri registrati (utilizzando nome, cognome, nome utente) e di assegnare loro un tag utilizzando la comune sintassi @user-name. Gli utenti con tag ricevono notifiche sulle loro menzioni.

* **Max menzioni**

   Limita il numero massimo di menzioni consentite in un post. Il valore predefinito è 10.

* **Pattern menzioni interfaccia**

   Specifica la stringa di pattern consentita per assegnare il tag (@menzione) all’utente registrato in un post. Esempio ~{{familyName}}{{givenName}}.

#### Scheda Moderazione utente {#user-moderation-tab}

Sotto la **Moderazione utente** , specifica le impostazioni di moderazione :

* **Rifiuta post**

   Se questa opzione è selezionata, ai moderatori di membri affidabili sarà consentito di negare i post e impedire che il post appaia sul forum pubblico. Il valore predefinito è deselezionato.

* **Chiudi/Riapri argomenti**

   Se questa opzione è selezionata, i moderatori di membri attendibili possono chiudere un argomento per ulteriori modifiche e commenti e riaprire un argomento. Il valore predefinito è deselezionato.

* **Segnala post**

   Se questa opzione è selezionata, consentire ai membri di contrassegnare gli argomenti o i commenti di altri come inappropriati. Il valore predefinito è deselezionato.

* **Elenco di motivi per segnalazione**

   Se questa opzione è selezionata, consenti ai membri di scegliere, da un elenco a discesa, il motivo per cui contrassegnano un argomento o un commento come inappropriato. Il valore predefinito è deselezionato.

* **Motivo per segnalazione personalizzato**

   Se questa opzione è selezionata, consenti ai membri di inserire il proprio motivo per contrassegnare un argomento o un commento come inappropriato. Il valore predefinito è deselezionato.

* **Soglia moderazione**

   Immettere il numero di volte in cui un argomento o un commento deve essere segnalato dai membri prima che i moderatori ne vengano informati. Il valore predefinito è 1 (una volta).

* **Limite segnalazione**

   Immetti il numero di volte in cui un argomento o un commento deve essere contrassegnato prima che sia nascosto dalla visualizzazione pubblica. Se è impostato su -1, l&#39;argomento o il commento contrassegnato non viene mai nascosto dalla visualizzazione pubblica. In caso contrario, questo numero deve essere maggiore o uguale alla soglia di moderazione. Il valore predefinito è 5.

#### Scheda Campo tag {#tag-field-tab}

Sotto la **Campo tag** , specifica i tag che possono essere applicati se **Consenti assegnazione tag** controlla il **Impostazioni** scheda :

* **Namespace consentiti**

   Pertinente se `Allow Tagging` è controllato sotto **Impostazioni** scheda . I tag che possono essere applicati sono limitati a quelli nelle categorie dello spazio dei nomi selezionate. L’elenco dei namespace include sia &quot;Tag standard&quot; (lo spazio dei nomi predefinito) che &quot;Includi tutti i tag&quot;. Il valore predefinito non è selezionato, il che significa che tutti i namespace sono consentiti.

* **Limite di suggerimenti**

   Immettere il numero di tag da visualizzare come suggerimento al membro che pubblica sul forum. Un valore pari a -1 non indica limiti. Il valore predefinito è 0.

### Configurazione della barra laterale del blog {#configuring-blog-sidebar}

Quando fai doppio clic sul pulsante `Blog Sidebar` viene visualizzata una finestra di dialogo di modifica.

Sotto la **Impostazioni della barra laterale del diario** , specifica il formato della data per gli archivi e il tipo di voci da visualizzare nella barra laterale :

![blog-component-sidebar](assets/blog-component-sidebar.png)

* **Formato data**

   Formato utilizzato per visualizzare gli archivi dei post di blog. Il formato utilizza segnaposto seguendo la convenzione Java.

   * yyyy : anno intero, come &#39;2015&#39;
   * yy : anno breve, come &#39;15&#39;
   * MMMM : mese intero, come giugno
   * MM : mese breve, come Jun
   * MM : numero del mese, ad esempio 06

   Il valore predefinito è &quot;aaaa MMMMM&quot; che mostrerebbe, ad esempio, &quot;2015 June&quot;

* **Tipo di visualizzazione**

   Titolo e tipo di post di blog da visualizzare nella barra laterale. La scelta è tra

   * Autori
   * Categorie
   * Archivi

* **Percorso componente Blopg**

   *(Facoltativo)* Posizione della risorsa blog da cui devono essere elencati gli articoli di blog. Se lasciato vuoto, utilizza il componente di resourceType `social/journal/components/hbs/journal` che appare sulla stessa pagina.

   * Esempio, `/content/sites/engage/en/blog/jcr:content/content/primary/blog`

* **Limite di suggerimenti**

   Numero di articoli di blog da visualizzare. Un valore pari a -1 non indica alcun limite. Il valore predefinito è -1.

## Esperienza dei visitatori del sito {#site-visitor-experience}

Nell&#39;ambiente di pubblicazione, la funzione blog mostrerà l&#39;articolo più recente seguito da articoli di blog precedenti in ordine decrescente di creazione. Le barre laterali dei blog consentono ai visitatori del sito di applicare filtri per limitare la selezione degli articoli del blog visualizzati.

L&#39;articolo del blog è seguito da un link per pubblicare o visualizzare i commenti.

Quando si seleziona un articolo di blog, vengono visualizzati l&#39;articolo e i commenti del blog (se abilitati).

Altre funzionalità dipendono dal fatto che il visitatore del sito sia un moderatore, un amministratore, un membro della community, un membro privilegiato o un anonimo.

### Utilizzo degli articoli {#working-with-articles}

Quando si crea un nuovo articolo di blog, è possibile scegliere di:

1. Pubblica immediatamente
1. Pubblicare una bozza
1. Pubblicare in una data e un’ora pianificate

Gli articoli del blog verranno visualizzati nella scheda appropriata (Pubblicato, Bozza o Pianificato) per i membri in grado di creare al momento della pubblicazione.

#### Moderatori e amministratori {#moderators-and-administrators}

Quando l&#39;utente connesso dispone di privilegi di moderatore o amministratore, può eseguire [attività di moderazione](/help/communities/moderate-ugc.md) (come consentito dalla configurazione del componente) su tutti gli articoli di blog e i commenti pubblicati su un blog.

![moderatore-homepage](assets/moderator-homepage.png)

#### Membri {#members}

Quando l&#39;utente connesso è un membro della community o [membro privilegiato](/help/communities/users.md#privileged-members-group) (a seconda della configurazione), possono selezionare `New Article` per creare e pubblicare un nuovo articolo di blog.

In particolare, possono:

* Crea un nuovo articolo di blog
* Pubblica un nuovo articolo di blog per conto di un altro membro
* Pubblica un commento a un articolo del blog
* Modifica il proprio articolo o commento di blog
* Elimina il proprio articolo o commento di blog
* Contrassegna altri articoli o commenti di blog

![home page](assets/member-homepage.png)

![create-blog](assets/create-blog.png)

#### Anonimo {#anonymous}

I visitatori del sito che non hanno effettuato l&#39;accesso possono solo leggere articoli e commenti di blog pubblicati, tradurli se supportati, ma non possono aggiungere un articolo o un commento di blog né contrassegnare gli articoli o i commenti di altri.

![visualizzazione utente anonima](assets/anonymous-user-view.png)

## Informazioni aggiuntive {#additional-information}

Per ulteriori informazioni, consulta [Blog Essentials](/help/communities/blog-developer-basics.md) per sviluppatori.

Per la moderazione di post e commenti di blog, vedi [Moderazione dei contenuti generati dagli utenti](/help/communities/moderate-ugc.md).

Per assegnare tag ai post e ai commenti dei blog, consulta [Assegnazione tag ai contenuti generati dagli utenti](/help/communities/tag-ugc.md).

Per la traduzione di post e commenti del blog, vedi [Traduzione di contenuti generati dagli utenti](/help/communities/translate-ugc.md).
