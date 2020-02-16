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
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Funzione blog{#blog-feature}

## Introduzione {#introduction}

La funzione blog di AEM Communities si è trasformata da attività di authoring a una vera e propria attività della community che si svolge nell’ambiente di pubblicazione.

La funzione blog supporta la fornitura di informazioni sulla community in un formato di pubblicazione. Le voci di blog vengono inserite nell’ambiente di pubblicazione da membri autorizzati (utenti registrati e con accesso).

La funzione blog fornisce:

* Creazione lato pubblicazione di articoli e commenti di blog
* Modifica RTF
* Immagini in linea (con supporto per trascinamento)
* Contenuto di social networking incorporato (supporto[oEmbed](/help/communities/blog-developer-basics.md#allowing-rich-media))
* Modalità Bozza
* Pubblicazione pianificata
* Componi per conto (un membro [](/help/communities/users.md#privileged-members-group) privilegiato può creare contenuti per conto di un membro della comunità diverso)
* [Moderazione](/help/communities/moderate-ugc.md) contestuale e collettiva degli articoli e dei commenti dei blog

Questa sezione della documentazione descrive

* aggiunta della funzione blog a un sito AEM
* impostazioni di configurazione per i componenti blog

>[!NOTE]
>
>I componenti `Journal`e `Journal Sidebar` sono denominati `Blog` e `Blog Sidebar`.
>
>La funzione blog disponibile in AEM 6.0 e nelle versioni precedenti è stata rimossa. Era basato su un modello e consentiva solo agli autori di creare contenuti nell’ambiente di authoring.

## Aggiunta di componenti blog a una pagina {#adding-blog-components-to-a-page}

Se desiderate aggiungere un blog a una pagina in modalità di creazione, usate il browser dei componenti per individuare

* `Communities / Blog`
* `Communities / Blog Sidebar`

trascinateli nella stessa posizione di una pagina in cui dovrebbe comparire il blog.

Per le informazioni necessarie, visita [Community Components Basics](/help/communities/basics.md).

Quando sono incluse le librerie [lato client](/help/communities/blog-developer-basics.md#essentials-for-client-side) richieste, viene visualizzato il `Blog`componente:

![chlimage_1-229](assets/chlimage_1-229.png)

E come `Blog Sidebar` apparirà:

![chlimage_1-230](assets/chlimage_1-230.png)

### Configurazione del blog {#configuring-blog}

Selezionate il `Blog` componente inserito a cui accedere e selezionate l’ `Configure` icona che apre la finestra di dialogo di modifica.

![chlimage_1-231](assets/chlimage_1-231.png) Impostazioni ![blog](assets/blog-configure.png)

#### scheda Impostazioni {#settings-tab}

Nella scheda **Impostazioni** , specificate le funzioni di base del blog:

* **Consenti miniatura** allegato Se questa opzione è selezionata, viene creata una miniatura dell&#39;immagine allegata.

* **Dimensione** massima miniatura allegato DimensioneDimensione massima (in pixel) dell’immagine della miniatura dell’allegato. Il valore predefinito è 800 x 800.
* **Dimensione minima immagine per miniatura** Dimensione minima (in byte) dell&#39;immagine per la generazione della miniatura per le immagini in linea. Il valore predefinito è 100000 byte (100 kb).
* **Dimensione** massima miniatura DimensioneMassima (in pixel) della miniatura per l’immagine in linea. Il valore predefinito è 800 x 800.
* **Consenti membri** privilegiati Se questa opzione è selezionata, solo i membri privilegiati possono creare contenuto.
* **Membri** privilegiati consentitiAggiungi i membri privilegiati autorizzati a creare contenuto.
* **Blocca contenuto generato dall&#39;utente in modalità** Modifica autore Se attivato, blocca il contenuto generato dall&#39;utente durante la modifica in modalità Autore.

* **Titolo** giornale di registrazione Titolo del blog da visualizzare sulla pagina.

>[!NOTE]
>
>Il Titolo diario viene utilizzato per creare automaticamente l&#39;URL del blog.
>Per creare l&#39;URL per il blog vengono utilizzati al massimo 50 caratteri (con 5 caratteri aggiuntivi per l&#39;univocità) dal titolo del giornale specificato qui.

* **Descrizione diario**La descrizione del blog.
* **Argomenti per pagina** Definisce il numero di post/commenti del blog visualizzati per pagina. Il valore predefinito è 10.

* **Moderato** Se selezionato, l&#39;invio di post di blog e commenti deve essere approvato prima che vengano visualizzati su un sito pubblicato. Il valore predefinito è deselezionato.

* **Chiuso** Se selezionato, il blog viene chiuso a nuovi post e commenti del blog. Il valore predefinito è deselezionato.

* **Editor** Rich Text Se questa opzione è selezionata, è possibile immettere commenti e post di blog con la marcatura. Il valore predefinito è selezionato.

* **Consenti tag** Se questa opzione è selezionata, consentire ai membri di aggiungere etichette di tag al proprio post (consultate la scheda Campo **** tag). Il valore predefinito è deselezionato.

* **Consenti caricamenti** file Se questa opzione è selezionata, consenti l&#39;aggiunta di allegati a un post di blog o a un commento. Il valore predefinito è deselezionato.

* **Dimensione** massima file pertinente solo se `Allow File Uploads` è selezionata. Questo campo limita la dimensione (in byte) di un file caricato. Il valore predefinito è 104857600 (10 Mb).

* **Tipi** di file consentiti Pertinenti solo se `Allow File Uploads` è selezionata. Un elenco separato da virgole di estensioni di file con il separatore &quot;punto&quot;. Ad esempio: .jpg, .jpeg, .png, .doc, .docx, .pdf. Se vengono specificati dei tipi di file, non sarà possibile caricarli. Il valore predefinito non è specificato in modo che** **tutti i tipi di file siano consentiti.

* **Dimensione** massima file immagine pertinente solo se l&#39;opzione Consenti caricamenti file è selezionata. Numero massimo di byte di cui può disporre un file immagine caricato. Il valore predefinito è 2097152****(2 Mb).

* **Consenti risposte** Se questa opzione è selezionata, consenti risposte ai commenti inviati al post di blog. Il valore predefinito è deselezionato.

* **Consenti votazione** Se questa opzione è selezionata, includete la funzione di voto con un post di blog. Il valore predefinito è deselezionato.

* **Consenti agli utenti di eliminare commenti e argomenti** Se questa opzione è selezionata, consente ai membri di eliminare i commenti e i post di blog che hanno pubblicato. Il valore predefinito è** **non selezionato.

* **Consenti** se questa opzione è selezionata, includete la seguente funzione per gli articoli di blog, che consente ai membri di ricevere [notifiche](/help/communities/notifications.md) per i nuovi post. Il valore predefinito è deselezionato.

* **Consenti iscrizioni** e-mail Se questa opzione è selezionata, consente ai membri di ricevere notifiche sui nuovi post tramite e-mail ([iscrizione](/help/communities/subscriptions.md)). Richiede `Allow Following` di essere selezionato e configurato [l’](/help/communities/email.md)e-mail. Il valore predefinito è deselezionato.

* **Visualizza Badge** Se questa opzione è selezionata, visualizza [i simboli](/help/communities/implementing-scoring.md) guadagnati e assegnati con il post di blog di un membro. Il valore predefinito è deselezionato.

* **Non ottenere risposte sulla pagina di elenco**
* **Consenti contenuti** contenuti contenuti contenuti [contenuti se questa opzione è selezionata, l’idea può essere identificata come contenuto](/help/communities/featured.md)disponibile. Il valore predefinito è deselezionato.

* **Abilita menzioni** Se abilitata, consente agli utenti della community registrati di identificare altri membri registrati (utilizzando nome, cognome, nome utente) e di assegnare loro un tag utilizzando la sintassi comune @user-name. Gli utenti con tag ricevono notifiche sulle proprie menzioni.

* **N. max menzioni** Limita il numero massimo di menzioni consentite in un post. Il valore predefinito è 10.

* **Pattern** di menzione dell&#39;interfaccia utente Specificate la stringa di pattern consentita per assegnare un tag (@reference) all&#39;utente registrato in un post. Ad esempio ~{{familyName}}{{givenName}}.

#### Scheda Moderazione utente {#user-moderation-tab}

Nella scheda Moderazione **** utente, specificate le impostazioni di moderazione:

* **Rifiuta post** Se questa opzione è selezionata, i moderatori di membri attendibili potranno negare i post e impedire che vengano visualizzati nel forum pubblico. Il valore predefinito è deselezionato.

* **Chiudi/Riapri argomenti** Se questa opzione è selezionata, i moderatori di membri attendibili potrebbero chiudere un argomento per ulteriori modifiche e commenti e riaprire un argomento. Il valore predefinito è deselezionato.

* **Contrassegna post** Se questa opzione è selezionata, consentire ai membri di contrassegnare gli argomenti o i commenti di altri utenti in modo inappropriato. Il valore predefinito è deselezionato**.**

* **Elenco** motivi contrassegno Se questa opzione è selezionata, consente ai membri di scegliere, da un elenco a discesa, il motivo per cui l&#39;argomento o il commento vengono contrassegnati come non appropriati. Il valore predefinito è deselezionato.

* **Motivo** contrassegno personalizzato Se questa opzione è selezionata, consentire ai membri di inserire il proprio motivo per cui l&#39;argomento o il commento è contrassegnato come inappropriato. Il valore predefinito è deselezionato**.**

* **Soglia moderazione** Immettere il numero di volte in cui un argomento o un commento deve essere contrassegnato dai membri prima che i moderatori ricevano una notifica. Il valore predefinito è 1 (una volta).

* **Limite** contrassegno Consente di specificare quante volte un argomento o un commento deve essere contrassegnato prima che venga nascosto dalla visualizzazione pubblica. Se è impostato su -1, l&#39;argomento o il commento contrassegnato non viene mai nascosto dalla visualizzazione pubblica. In caso contrario, questo numero deve essere maggiore o uguale alla soglia di moderazione. Il valore predefinito è 5.

#### Scheda Campo tag {#tag-field-tab}

Nella scheda Campo **** tag, specificate i tag che possono essere applicati se nella scheda **Impostazioni** è selezionata l’opzione **Consenti tag** :

* **Spazi dei nomi consentiti** Pertinenti se `Allow Tagging` è selezionato nella scheda **Settings **(Impostazioni). I tag che possono essere applicati sono limitati a quelli all&#39;interno delle categorie dello spazio nomi selezionate. L&#39;elenco degli spazi dei nomi include &quot;Tag standard&quot; (lo spazio dei nomi predefinito) e &quot;Includi tutti i tag&quot;. Il valore predefinito non è selezionato, ovvero tutti gli spazi dei nomi sono consentiti.

* **Limite** suggerimenti Consente di specificare il numero di tag da visualizzare come suggerimento al membro che invia il messaggio al forum. Un valore pari a -1 non indica alcun limite. Il valore predefinito è 0.

### Configurazione della barra laterale del blog {#configuring-blog-sidebar}

Quando si fa doppio clic sul `Blog Sidebar` componente, si apre una finestra di dialogo di modifica.

Nella scheda Impostazioni **barra laterale** giornale, specificare il formato della data per gli archivi e il tipo di voci da visualizzare nella barra laterale:

![blog-component-sidebar](assets/blog-component-sidebar.png)

* **Formato** data Il formato utilizzato per visualizzare gli archivi dei post di blog. Il formato utilizza dei segnaposto secondo la convenzione Java.

   * yyyy: anno intero, come &#39;2015&#39;
   * yy: anno breve, come &#39;15&#39;
   * MMMMM : mese intero, come giugno
   * MMM : mese breve, come Jun
   * MM : numero del mese, come 06
   Il valore predefinito è &quot;yyyy MMMMM&quot; che mostrerebbe, ad esempio, &quot;2015 June&quot;

* **Tipo** di visualizzazione Titolo e tipo di post di blog da visualizzare nella barra laterale. La scelta è tra

   * Autori
   * Categorie
   * Archivi

* **Percorso componente Blopg**
   *(Facoltativo)* Il percorso della risorsa del blog da cui devono essere elencati gli articoli del blog. Se lasciato vuoto, verrà utilizzato il componente resourceType `social/journal/components/hbs/journal` che viene visualizzato sulla stessa pagina.

   * for example, `/content/sites/engage/en/blog/jcr:content/content/primary/blog`

* **Limite** suggerimenti Il numero di articoli di blog da visualizzare. Un valore pari a -1 non indica alcun limite. Il valore predefinito è -1.

## Esperienza dei visitatori del sito {#site-visitor-experience}

Nell&#39;ambiente di pubblicazione, la funzione blog mostrerà l&#39;articolo di blog più recente seguito da articoli di blog meno recenti in ordine decrescente. Le barre laterali dei blog consentono ai visitatori del sito di applicare filtri per limitare la selezione degli articoli del blog visualizzati.

L&#39;articolo del blog è seguito da un collegamento per pubblicare o visualizzare commenti.

Quando è selezionato un articolo di blog, vengono visualizzati l&#39;articolo e i commenti del blog (se abilitati).

Altre capacità dipendono dal fatto che il visitatore del sito sia un moderatore, un amministratore, un membro della community, un membro privilegiato o un anonimo.

### Utilizzo degli articoli {#working-with-articles}

Quando create un nuovo articolo di blog, potete scegliere di:

1. Pubblica immediatamente
1. Pubblicare una bozza
1. Pubblicare a una data e un&#39;ora pianificate

Gli articoli del blog verranno visualizzati nella scheda appropriata (Pubblicato, Bozze o Pianificato) ai membri in grado di eseguire l&#39;authoring al momento della pubblicazione.

#### Moderatori e amministratori {#moderators-and-administrators}

Quando l&#39;utente che ha effettuato l&#39;accesso dispone di privilegi di moderatore o amministratore, può eseguire attività [di](/help/communities/moderate-ugc.md) moderazione (come consentito dalla configurazione del componente) su tutti gli articoli di blog e i commenti inviati a un blog.

![chlimage_1-232](assets/chlimage_1-232.png)

#### Membri {#members}

Quando l&#39;utente che ha effettuato l&#39;accesso è un membro della community o un membro [](/help/communities/users.md#privileged-members-group) privilegiato (a seconda della configurazione), può selezionare `New Article` di creare e pubblicare un nuovo articolo del blog.

In particolare, possono

* create un nuovo articolo blog
* pubblicare un nuovo articolo di blog per conto di un altro membro
* pubblicare un commento su un articolo di blog
* modificare il proprio articolo o commento di blog
* eliminare un proprio articolo o commento blog
* contrassegnare gli articoli o i commenti di altri blog

![chlimage_1-233](assets/chlimage_1-233.png) ![chlimage_1-234](assets/chlimage_1-234.png)

#### Anonimo {#anonymous}

I visitatori del sito che non hanno effettuato l&#39;accesso possono solo leggere articoli e commenti di blog postati, tradurli se supportati, ma non possono aggiungere un articolo o un commento di blog né contrassegnare gli articoli o i commenti di altri utenti.

![chlimage_1-235](assets/chlimage_1-235.png)

## Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili nella pagina [Blog Essentials](/help/communities/blog-developer-basics.md) per gli sviluppatori.

Per la moderazione di post e commenti di blog, consultate [Moderazione del contenuto](/help/communities/moderate-ugc.md)generato dall&#39;utente.

Per assegnare tag a post e commenti di blog, consultate [Assegnazione di tag ai contenuti](/help/communities/tag-ugc.md)generati dall&#39;utente.

Per la traduzione di post e commenti del blog, consultate [Traduzione di contenuti](/help/communities/translate-ugc.md)generati dagli utenti.
