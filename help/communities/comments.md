---
title: Utilizzo dei commenti
seo-title: Utilizzo dei commenti
description: La funzione Commenti consente ai visitatori del sito che hanno effettuato l’accesso di condividere le proprie opinioni e conoscenze
seo-description: La funzione Commenti consente ai visitatori del sito che hanno effettuato l’accesso di condividere le proprie opinioni e conoscenze
uuid: 40acd962-846c-483c-b789-aab3a7d2b31b
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 216cfb3e-777e-4773-afba-749debdca000
docset: aem65
translation-type: tm+mt
source-git-commit: 6be0aa7c3f6b21ad26221289a6cca2b4615ed3f4
workflow-type: tm+mt
source-wordcount: '994'
ht-degree: 6%

---


# Utilizzo dei commenti {#using-comments}

## Introduzione {#introduction}

La funzione commenti consente ai visitatori del sito che hanno effettuato l’accesso (membri) di condividere le proprie opinioni e conoscenze in merito ai contenuti del sito. Questa funzione è spesso già presente in altre funzioni, ma può essere aggiunta a qualsiasi sito Web.

Il documento descrive:

* Aggiunta `Comments` a una pagina.
* Impostazioni di configurazione per il `Comments` componente.

>[!NOTE]
>
>L&#39;invio anonimo di un commento non è supportato. I visitatori del sito devono registrarsi (diventare membri) ed effettuare l’accesso per partecipare.


### Aggiunta di commenti a una pagina {#adding-comments-to-a-page}

Per aggiungere un `Comments` componente a una pagina in modalità di creazione, usate il browser dei componenti per individuare

* `Communities / Comments`

trascinatelo nella posizione desiderata su una pagina, ad esempio una posizione relativa alla funzione in cui gli utenti possono inserire commenti oppure semplicemente nella parte inferiore della pagina.

Per le informazioni necessarie, consulta [Community Components Basics](/help/communities/basics.md).

Quando sono incluse le librerie [lato client](/help/communities/essentials-comments.md#essentials-for-client-side) richieste, viene visualizzato così il `Comments` componente.

![comments-component](assets/comments-component.png)

>[!NOTE]
>
>Su una pagina può esistere un solo `Comments` componente. Alcune funzioni di Communities includono già commenti, ad esempio blog, calendario, forum, QnA e recensioni.


### Configurazione dei commenti {#configuring-comments}

Selezionate il `Comments` componente inserito a cui accedere e selezionate l’ `Configure` icona che apre la finestra di dialogo di modifica.

![icona di configurazione](assets/configure.png)

![commenti, impostazioni](assets/commentssettings.png)

#### Scheda Commenti {#comments-tab}

Nella scheda **Commenti** , specificare il modo in cui i visitatori inseriscono i commenti.

* **Consenti risposte**

   Se questa opzione è selezionata, consente ai membri di rispondere ai commenti esistenti. Il valore predefinito è deselezionato.

* **Commenti per pagina**

   Limita il numero di commenti visualizzati per pagina e il numero di risposte visualizzate. Il valore predefinito è 10.

* **Consenti caricamenti file**

   Se questa opzione è selezionata, l&#39;opzione per caricare un file viene visualizzata con la casella di immissione testo. Il valore predefinito è deselezionato.

* **Dimensione file massima**

   Pertinente solo se l&#39;opzione Consenti caricamenti file è selezionata. Questo valore limita le dimensioni del file caricato. Il limite predefinito è 10 MB.

* **Lunghezza massima messaggio**

   Numero massimo di caratteri che possono essere immessi nella casella di testo. Il valore predefinito è 4096 caratteri.

* **Tipi di file consentiti**

   Pertinente solo se l&#39;opzione Consenti caricamenti file è selezionata. Un elenco separato da virgole di estensioni di nomi di file con il separatore &quot;punto&quot;. Ad esempio: .jpg, .jpeg, .png, .doc, .docx, .pdf. Se vengono specificati dei tipi di file, quelli non specificati non sono consentiti. Il valore predefinito non è specificato, pertanto tutti i tipi di file sono consentiti.

* **Editor Rich Text**

   Se questa opzione è selezionata, i commenti vengono inseriti con la marcatura. Il valore predefinito è deselezionato.

* **Consenti votazione**

   Se questa opzione è selezionata, l&#39;opzione per votare verso l&#39;alto o il basso viene visualizzata con la casella di immissione testo. Il valore predefinito è deselezionato.

* **Consenti Segui**

   Se questa opzione è selezionata, consentire ai membri di seguire i commenti. Il valore predefinito è deselezionato.

* **Visualizza badge**

   Se questa opzione è selezionata, è possibile visualizzare i simboli acquisiti e assegnati. Il valore predefinito è deselezionato.

#### Scheda Moderazione utente {#user-moderation-tab}

Nella scheda Moderazione **** utente, specificate le modalità di gestione dei commenti inviati. Per ulteriori informazioni, consultate [Moderazione del contenuto](/help/communities/moderate-ugc.md)generato dall&#39;utente.

* **Premoderazione**

   Se questa opzione è attivata, i commenti devono essere approvati prima di essere visualizzati su un sito di pubblicazione. Il valore predefinito è deselezionato.

* **Elimina commenti**

   Se questa opzione è attivata, al membro che ha pubblicato il commento viene fornita la possibilità di eliminarlo. Il valore predefinito è deselezionato.

* **Rifiuta commenti**

   Se questa opzione è selezionata, consentire ai moderatori di negare i commenti. Il valore predefinito è deselezionato.

* **Chiudi/Riapri commenti**

   Se questa opzione è selezionata, consentire ai moderatori di chiudere e riaprire i commenti. Il valore predefinito è deselezionato.

* **Segnala commenti**

   Se questa opzione è selezionata, consentire ai membri di contrassegnare i commenti come non appropriati. Il valore predefinito è deselezionato.

* **Elenco di motivi per segnalazione**

   Se questa opzione è selezionata, consentire ai membri di scegliere, da un elenco a discesa, il motivo per cui contrassegnare un commento come non appropriato. Il valore predefinito è deselezionato.

* **Motivo per segnalazione personalizzato**

   Se questa opzione è selezionata, consentire ai membri di inserire il proprio motivo per il quale è stato segnalato un commento come inappropriato. Il valore predefinito è deselezionato.

* **Soglia moderazione**

   Immettete il numero di volte in cui un commento deve essere contrassegnato dai membri prima che i moderatori vengano informati. Il valore predefinito è una tantum (1).

* **Limite segnalazione**

   Specificate quante volte un commento deve essere contrassegnato prima che venga nascosto dalla visualizzazione pubblica. Questo numero deve essere maggiore o uguale alla soglia di **moderazione**. Il valore predefinito è 5.

#### Scheda Impostazioni ordinamento {#sort-settings-tab}

Nella scheda **Impostazioni** ordinamento, specificare in che modo i commenti inviati vengono ordinati quando vengono visualizzati.

* **Campo di ordinamento**

   Per selezionare uno dei `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed`, o `Most Liked`.

* **Ordinamento**

   Per selezionare una delle `Ascending` opzioni o `Descending`, trascinate verso il basso.

### Passaggio a un tipo di commento personalizzato {#changing-to-a-custom-comment-type}

Modificando il Tipo risorsa commento, il sistema di commenti non genera più un&#39;istanza di commento utilizzando l&#39;impostazione predefinita, ma piuttosto un&#39;istanza che è stata personalizzata (estesa) dagli sviluppatori.

Una volta noti i tipi di risorse personalizzati, immettete la modalità [](/help/sites-authoring/default-components-designmode.md) Progettazione e fate doppio clic sul `Comments` componente inserito per aprire una finestra di dialogo con una scheda aggiuntiva.

Nella scheda Tipi **di** risorse, specificare il resourceType personalizzato per le nuove istanze dei `Comments or Voting` componenti:

![resource-type](assets/resource-type.png)

* **Tipo risorsa commento**

   Passa a resourceType di un `comment` componente esteso (commento singolo) in /apps. Esempio, `/apps/social/commons/components/hbs/comments/comment`

   Questa risorsa identifica il resourceType dell&#39;UGC creato quando un visitatore inserisce un commento.

* **Tipo di risorsa per votazione**

   Passa a resourceType di un `voting` componente esteso in /apps. Esempio, `/apps/social/components/hbs/voting`

   Questa risorsa identifica il tipo di risorsa dell&#39;UGC creato quando un visitatore pubblica un voto.

* **Tipo risorsa sistema commenti**

   Passa a resourceType di un `comments`componente esteso (sistema di commenti) in /apps. Lasciate vuoto, a meno che il modello di pagina includa [](/help/communities/scf.md#add-or-include-a-communities-component) dinamicamente il sistema di commenti nello script sottostante, anziché essere aggiunto alla pagina come risorsa (nodo commenti). Ulteriori informazioni leggendo l&#39;helper [](/help/communities/handlebars-helpers.md#include){{include}}.

### Esperienza dei visitatori del sito {#site-visitor-experience}

#### Moderatori e amministratori {#moderators-and-administrators}

Quando l’utente che ha effettuato l’accesso dispone di privilegi di moderatore o amministratore, può eseguire le attività di moderazione consentite dalla configurazione del componente, indipendentemente da chi ha creato il commento.

#### Membri {#members}

Quando il visitatore del sito ha effettuato l&#39;accesso, a seconda della configurazione, può

* Pubblicare un nuovo commento
* Modificare il proprio commento
* Elimina il proprio commento
* Contrassegnare altri commenti

#### Anonimo {#anonymous}

I visitatori del sito che non hanno effettuato l&#39;accesso possono solo leggere i commenti pubblicati, tradurli se supportati, ma non aggiungere commenti o contrassegnare i commenti di altri utenti.

### Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili nella pagina [Comments Essentials](/help/communities/essentials-comments.md) per gli sviluppatori.

Per la moderazione dei commenti pubblicati, vedere [Moderazione del contenuto](/help/communities/moderate-ugc.md)generato dall&#39;utente.

Per la traduzione dei commenti postati, vedere [Traduzione del contenuto](/help/communities/translate-ugc.md)generato dall&#39;utente.
