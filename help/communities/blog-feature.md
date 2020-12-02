---
title: Funzione blog
seo-title: Funzione blog
description: Informazioni della community in un formato di registrazione
seo-description: Informazioni della community in un formato di registrazione
uuid: 7323063f-81e8-45c3-9035-bf7df6124830
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: cf8b3d72-30ba-40ca-ae48-b61abbb28802
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1676'
ht-degree: 7%

---


# Funzione blog {#blog-feature}

## Introduzione {#introduction}

La funzione blog di  AEM Communities è stata trasformata da attività di authoring a vera e propria attività della community che si svolge nell’ambiente di pubblicazione.

La funzione blog supporta la fornitura di informazioni sulla community in un formato di pubblicazione. Le voci di blog vengono inserite nell’ambiente di pubblicazione da membri autorizzati (utenti registrati e con accesso).

La funzione blog fornisce:

* Creazione lato pubblicazione di articoli e commenti di blog
* Modifica RTF
* Immagini in linea (con supporto per trascinamento)
* Contenuto di social networking incorporato ([Supporto per incorporamento](/help/communities/blog-developer-basics.md#allowing-rich-media))
* Modalità Bozza
* Pubblicazione pianificata
* Componi per conto (un [membro privilegiato](/help/communities/users.md#privileged-members-group) può creare contenuto per conto di un membro della comunità diverso)
* [Contesto e ](/help/communities/moderate-ugc.md) moderazione in blocco di articoli e commenti di blog

Questa sezione della documentazione descrive quanto segue:

* Aggiunta della funzione blog a un sito AEM
* Impostazioni di configurazione per i componenti blog

>[!NOTE]
>
>I componenti `Journal` e `Journal Sidebar` sono denominati `Blog` e `Blog Sidebar`.
>
>La funzione blog di AEM 6.0 e versioni precedenti è stata rimossa. Era basato su un modello e consentiva solo agli autori di creare contenuti nell’ambiente di authoring.

## Aggiunta di componenti di blog a una pagina {#adding-blog-components-to-a-page}

Se desiderate aggiungere un blog a una pagina in modalità di creazione, usate il browser dei componenti per individuare

* `Communities / Blog`
* `Communities / Blog Sidebar`

trascinateli nella stessa posizione di una pagina in cui dovrebbe comparire il blog.

Per le informazioni necessarie, visitare [Community Components Basics](/help/communities/basics.md).

Quando vengono incluse le [librerie lato client ](/help/communities/blog-developer-basics.md#essentials-for-client-side), viene visualizzato il componente `Blog`:

![add-blog-component](assets/add-blog-component.png)

### Configurazione del blog {#configuring-blog}

Selezionare il componente `Blog` inserito a cui accedere e selezionare l&#39;icona `Configure` che apre la finestra di dialogo di modifica.

![configure](assets/configure-new.png)

![Impostazioni blog](assets/blog-configure.png)

#### Scheda Impostazioni {#settings-tab}

Nella scheda **Impostazioni**, specificate le funzioni di base del blog:

* **Consenti miniatura allegato**

   Se questa opzione è attivata, viene creata una miniatura dell’immagine allegata.

* **Dimensione max miniatura allegato**

   Dimensione massima (in pixel) dell’immagine della miniatura dell’allegato. Il valore predefinito è 800 x 800.

* **Dimensioni minime immagine per miniatura**

   Dimensione minima (in byte) dell&#39;immagine per la generazione della miniatura per le immagini in linea. Il valore predefinito è 100000 byte (100 kb).

* **Dimensione massima miniatura**

   Dimensione massima (in pixel) dell’immagine in miniatura per l’immagine in linea. Il valore predefinito è 800 x 800.

* **Consenti membri privilegiati**

   Se questa opzione è selezionata, solo i membri con privilegi possono creare contenuto.

* **Membri privilegiati consentiti**

   Aggiungete i membri privilegiati autorizzati a creare contenuto.

* **Blocca i contenuti generati dagli utenti in modalità di modifica Creazione**

   Se attivato, blocca il contenuto generato dall&#39;utente durante la modifica in modalità Autore.

* **Titolo diario**

   Titolo del blog da visualizzare sulla pagina.

>[!NOTE]
>
>Il Titolo diario viene utilizzato per creare automaticamente l&#39;URL del blog.
>
>Per creare l&#39;URL per il blog vengono utilizzati al massimo 50 caratteri (con 5 caratteri aggiuntivi per l&#39;univocità) dal titolo del giornale specificato qui.

* **Descrizione diario**

   Descrizione del blog.

* **Topic per pagina**

   Definisce il numero di post/commenti del blog visualizzati per pagina. Il valore predefinito è 10.

* **Moderato**

   Se questa opzione è attivata, i post di post di blog e i commenti devono essere approvati prima che vengano visualizzati su un sito pubblicato. Il valore predefinito è deselezionato.

* **Chiuso**

   Se questa opzione è attivata, il blog è chiuso a nuovi post e commenti del blog. Il valore predefinito è deselezionato.

* **Editor Rich Text**

   Se questa opzione è selezionata, è possibile inserire commenti e post di blog con tag. Il valore predefinito è selezionato.

* **Consenti assegnazione tag**

   Se questa opzione è selezionata, consentire ai membri di aggiungere etichette di tag al proprio post (vedere la scheda **Campo tag**). Il valore predefinito è deselezionato.

* **Consenti caricamenti file**

   Se questa opzione è selezionata, consentite l&#39;aggiunta di allegati a un post di blog o a un commento. Il valore predefinito è deselezionato.

* **Dimensione file massima**

   Rilevante solo se è selezionato `Allow File Uploads`. Questo campo limita la dimensione (in byte) di un file caricato. Il valore predefinito è 104857600 (10 Mb).

* **Tipi di file consentiti**

   Rilevante solo se è selezionato `Allow File Uploads`. Un elenco separato da virgole di estensioni di file con il separatore &quot;punto&quot;. Ad esempio: .jpg, .jpeg, .png, .doc, .docx, .pdf. Se vengono specificati dei tipi di file, non sarà possibile caricare quelli non specificati. Il valore predefinito non è specificato, pertanto tutti i tipi di file sono consentiti.

* **Dimensione massima per file immagine allegato**

   Pertinente solo se l&#39;opzione Consenti caricamenti file è selezionata. Numero massimo di byte di cui può disporre un file immagine caricato. Il valore predefinito è 2097152 (2 Mb).

* **Consenti risposte**

   Se questa opzione è attivata, consentite le risposte ai commenti inviati al post di blog. Il valore predefinito è deselezionato.

* **Consenti votazione**

   Se questa opzione è selezionata, includete la funzione di voto con un post di blog. Il valore predefinito è deselezionato.

* **Consenti agli utenti di eliminare commenti e argomenti**

   Se questa opzione è selezionata, consentire ai membri di eliminare i commenti e i post di blog che hanno pubblicato. Il valore predefinito è deselezionato.

* **Consenti Segui**

   Se questa opzione è attivata, includete la seguente funzione per gli articoli di blog, che consente ai membri di ricevere [notifiche](/help/communities/notifications.md) di nuovi post. Il valore predefinito è deselezionato.

* **Consenti iscrizioni e-mail**

   Se questa opzione è attivata, consentire ai membri di ricevere notifiche sui nuovi post via e-mail ([subscription](/help/communities/subscriptions.md)). È necessario che `Allow Following` sia selezionato e che [e-mail sia configurato](/help/communities/email.md). Il valore predefinito è deselezionato.

* **Visualizza badge**

   Se questa opzione è attivata, vengono visualizzati i simboli guadagnati e assegnati [con il post di blog di un membro. ](/help/communities/implementing-scoring.md) Il valore predefinito è deselezionato.

* **Non ottenere risposte sulla pagina di elenco**

* **Consenti contenuto in primo piano**

   Se questa opzione è selezionata, l&#39;idea può essere identificata come [contenuto in evidenza](/help/communities/featured.md). Il valore predefinito è deselezionato.

* **Abilita menzione**

   Se abilitata, consente agli utenti della community registrati di identificare altri membri registrati (utilizzando nome, cognome, nome utente) e di assegnare loro un tag utilizzando la sintassi comune @user-name. Gli utenti con tag ricevono notifiche sulle proprie menzioni.

* **Max menzioni**

   Limita il numero massimo di menzioni consentite in un post. Il valore predefinito è 10.

* **Pattern menzioni interfaccia**

   Specificare la stringa di pattern consentita per assegnare un tag (@reference) all&#39;utente registrato in un post. Ad esempio ~{{familyName}}{{givenName}}.

#### Scheda Moderazione utente {#user-moderation-tab}

Nella scheda **Moderazione utente**, specificare le impostazioni di moderazione:

* **Rifiuta post**

   Se questa opzione è attivata, i moderatori di membri attendibili potranno negare i post e impedirne la visualizzazione nel forum pubblico. Il valore predefinito è deselezionato.

* **Chiudi/Riapri argomenti**

   Se questa opzione è attivata, i moderatori di membri attendibili potrebbero chiudere un argomento per ulteriori modifiche e commenti e riaprire un argomento. Il valore predefinito è deselezionato.

* **Segnala post**

   Se questa opzione è selezionata, consentire ai membri di contrassegnare gli argomenti o i commenti di altri utenti in modo inappropriato. Il valore predefinito è deselezionato.

* **Elenco di motivi per segnalazione**

   Se questa opzione è selezionata, consentire ai membri di scegliere, da un elenco a discesa, il motivo per cui segnalano un argomento o un commento come inappropriato. Il valore predefinito è deselezionato.

* **Motivo per segnalazione personalizzato**

   Se questa opzione è selezionata, consentire ai membri di inserire il proprio motivo per cui un argomento o un commento viene contrassegnato come inappropriato. Il valore predefinito è deselezionato.

* **Soglia moderazione**

   Immettere il numero di volte in cui un argomento o un commento deve essere contrassegnato dai membri prima che i moderatori ricevano una notifica. Il valore predefinito è 1 (una volta).

* **Limite segnalazione**

   Immettete il numero di volte in cui un argomento o un commento deve essere contrassegnato prima che venga nascosto dalla visualizzazione pubblica. Se è impostato su -1, l&#39;argomento o il commento contrassegnato non viene mai nascosto dalla visualizzazione pubblica. In caso contrario, questo numero deve essere maggiore o uguale alla soglia di moderazione. Il valore predefinito è 5.

#### Scheda Campo tag {#tag-field-tab}

Nella scheda **Tag field** (Campo tag), specificare i tag che possono essere applicati se l&#39;opzione **Consenti tag** è selezionata nella scheda **Settings** (Impostazioni):

* **Namespace consentiti**

   Pertinente se `Allow Tagging` è selezionato nella scheda **Settings**. I tag che possono essere applicati sono limitati a quelli all&#39;interno delle categorie dello spazio nomi selezionate. L’elenco degli spazi dei nomi include &quot;Tag standard&quot; (lo spazio dei nomi predefinito) e &quot;Includi tutti i tag&quot;. Il valore predefinito non è selezionato, il che significa che tutti gli spazi dei nomi sono consentiti.

* **Limite di suggerimenti**

   Immettete il numero di tag da visualizzare come suggerimento al membro che invia il messaggio al forum. Un valore pari a -1 non indica alcun limite. Il valore predefinito è 0.

### Configurazione della barra laterale del blog {#configuring-blog-sidebar}

Quando si fa doppio clic sul componente `Blog Sidebar`, si apre una finestra di dialogo di modifica.

Nella scheda **Impostazioni barra laterale giornale**, specificare il formato della data per gli archivi e il tipo di voci da visualizzare nella barra laterale:

![blog-component-sidebar](assets/blog-component-sidebar.png)

* **Formato data**

   Il formato utilizzato per visualizzare gli archivi dei post di blog. Il formato utilizza dei segnaposto secondo la convenzione Java.

   * yyyy: anno intero, come &#39;2015&#39;
   * yy: anno breve, come &#39;15&#39;
   * MMMMM : mese intero, come giugno
   * MMM : mese breve, come Jun
   * MM : numero del mese, come 06

   Il valore predefinito è &quot;yyyy MMMMM&quot; che mostrerebbe, ad esempio, &quot;2015 June&quot;

* **Tipo di visualizzazione**

   Titolo e tipo di post di blog da visualizzare nella barra laterale. La scelta è tra

   * Autori
   * Categorie
   * Archivi

* **Percorso componente Blopg**

   *(Facoltativo)* La posizione della risorsa del blog da cui devono essere elencati gli articoli del blog. Se lasciato vuoto, utilizzerà il componente di resourceType `social/journal/components/hbs/journal` che viene visualizzato sulla stessa pagina.

   * Esempio, `/content/sites/engage/en/blog/jcr:content/content/primary/blog`

* **Limite di suggerimenti**

   Il numero di articoli di blog da visualizzare. Un valore pari a -1 non indica alcun limite. Il valore predefinito è -1.

## Esperienza visitatori del sito {#site-visitor-experience}

Nell&#39;ambiente di pubblicazione, la funzione blog mostrerà l&#39;articolo di blog più recente seguito da articoli di blog meno recenti in ordine decrescente. Le barre laterali dei blog consentono ai visitatori del sito di applicare filtri per limitare la selezione degli articoli del blog visualizzati.

L&#39;articolo del blog è seguito da un collegamento per pubblicare o visualizzare commenti.

Quando è selezionato un articolo di blog, vengono visualizzati l&#39;articolo e i commenti del blog (se abilitati).

Altre capacità dipendono dal fatto che il visitatore del sito sia un moderatore, un amministratore, un membro della community, un membro privilegiato o un utente anonimo.

### Utilizzo degli articoli {#working-with-articles}

Quando create un nuovo articolo di blog, potete scegliere di:

1. Pubblica immediatamente
1. Pubblicare una bozza
1. Pubblicare a una data e un&#39;ora pianificate

Gli articoli del blog verranno visualizzati nella scheda appropriata (Pubblicato, Bozze o Pianificato) ai membri in grado di eseguire l&#39;authoring al momento della pubblicazione.

#### Moderatori e amministratori {#moderators-and-administrators}

Quando l&#39;utente che ha effettuato l&#39;accesso dispone di privilegi di moderatore o amministratore, può eseguire [attività di moderazione](/help/communities/moderate-ugc.md) (come consentito dalla configurazione del componente) su tutti gli articoli di blog e i commenti inviati a un blog.

![moderatore-homepage](assets/moderator-homepage.png)

#### Membri {#members}

Quando l&#39;utente che ha effettuato l&#39;accesso è un membro della community o un membro [privilegiato](/help/communities/users.md#privileged-members-group) (a seconda della configurazione), è in grado di selezionare `New Article` per creare e pubblicare un nuovo articolo del blog.

In particolare, essi possono:

* Creare un nuovo articolo di blog
* Pubblica un nuovo articolo di blog per conto di un altro membro
* Pubblicare un commento su un articolo di blog
* Modificare un proprio articolo o commento di blog
* Eliminare un proprio articolo o commento di blog
* Contrassegnare gli articoli o i commenti di altri blog

![home page](assets/member-homepage.png)

![create-blog](assets/create-blog.png)

#### Anonimo {#anonymous}

I visitatori del sito che non hanno effettuato l&#39;accesso possono solo leggere articoli e commenti di blog postati, tradurli se supportati, ma non possono aggiungere un articolo o un commento di blog né contrassegnare gli articoli o i commenti di altri utenti.

![visualizzazione utente anonima](assets/anonymous-user-view.png)

## Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili nella pagina [Blog Essentials](/help/communities/blog-developer-basics.md) dedicata agli sviluppatori.

Per la moderazione di post e commenti di blog, vedere [Moderazione di contenuti generati dall&#39;utente](/help/communities/moderate-ugc.md).

Per assegnare tag a post e commenti di blog, consultate [Tagging User Generated Content](/help/communities/tag-ugc.md).

Per la traduzione di post e commenti del blog, vedere [Traduzione di contenuti generati dall&#39;utente](/help/communities/translate-ugc.md).
