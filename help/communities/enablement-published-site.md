---
title: Scopri il sito pubblicato
seo-title: Scopri il sito pubblicato
description: Individuazione di un sito pubblicato per l'abilitazione
seo-description: Individuazione di un sito pubblicato per l'abilitazione
uuid: 1bfefa8a-fd9c-4ca8-b2ff-add79776c8ae
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 26715b94-e2ea-4da7-a0e2-3e5a367ac1cd
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1239'
ht-degree: 2%

---



# Esperienza con il sito pubblicato {#experience-the-published-site}


**[⇐ creare e assegnare risorse di abilitazione](resource.md)**

## Passa a nuovo sito in Pubblica {#browse-to-new-site-on-publish}

Ora che è stato pubblicato il sito della community appena creato e le relative risorse di abilitazione e il percorso di apprendimento, è possibile utilizzare il sito di Enablement Tutorial.

Per iniziare, andate all’URL visualizzato al momento della creazione del sito, ma sul server di pubblicazione, ad esempio

* URL autore = [http://localhost:4502/content/sites/enable/en.html](http://localhost:4502/content/sites/enable/en.html)
* URL pubblicazione = [http://localhost:4503/content/sites/enable/en.html](http://localhost:4503/content/sites/enable/en.html)

Se la pagina principale [predefinita è stata impostata](enablement-create-site.md#changethedefaulthomepage), è sufficiente accedere a [http://localhost:4503/](Http://localhost:4503/) per avviare il sito.

Al primo arrivo sul sito pubblicato, il visitatore del sito in genere non avrebbe già effettuato l’accesso e sarebbe anonimo.

**http://localhost:4503/content/sites/enable/en.html**

![enablement-login](assets/enablement-login.png)

## Visitatore anonimo del sito {#anonymous-site-visitor}

A un visitatore del sito anonimo viene immediatamente presentata la pagina di login per questo sito della community di abilitazione privata. Notate che non è disponibile l&#39;opzione di autoregistrazione né di accesso con Facebook o Twitter.

Questa home page include quattro voci di menu: `Assignments, Ski Catalog, What's New` e `Discussions`, ma è possibile che non venga raggiunto alcun risultato senza effettuare l&#39;accesso.

>[!NOTE]
>
>È possibile concedere l&#39;accesso anonimo a un sito di abilitazione senza consentire ai visitatori del sito di registrarsi autonomamente.
>
>Se una risorsa di abilitazione è impostata su `show in catalog` e `allow anonymous access`, i visitatori anonimi del sito potranno visualizzare le risorse nel catalogo.

### Impedisci l&#39;accesso anonimo su JCR {#prevent-anonymous-access-on-jcr}

Una limitazione nota espone il contenuto del sito community ai visitatori anonimi attraverso contenuti jcr e json, anche se **[!UICONTROL consenti l&#39;accesso anonimo]** è disabilitato per il contenuto del sito. Tuttavia, questo comportamento può essere controllato utilizzando Limitazioni Sling come soluzione alternativa.

Per proteggere i contenuti del sito della community dall&#39;accesso di utenti anonimi tramite contenuti jcr e json, procedi come segue:

1. AEM’istanza di creazione, andate a https://&lt;host>:&lt;porta>/editor.html/content/site/&lt;nome sito>.html.

   >[!NOTE]
   >
   >Non andate al sito localizzato.

1. Vai a **[!UICONTROL Proprietà pagina]**.

   ![page-properties](assets/page-properties.png)

1. Vai alla scheda **[!UICONTROL Avanzate]**.
1. Abilita **[!UICONTROL Autenticazione richiesta]**.

   ![autenticazione del sito](assets/site-authentication.png)

1. Aggiungete il percorso della pagina di login. Esempio, `/content/......./GetStarted`.
1. Pubblicate la pagina.

## Membro iscritto {#enrolled-member}

Questa esperienza si basa sugli utenti `Riley Taylor` e `Sidney Croft` creati[e [ assegnati](resource.md#settings) al percorso di apprendimento *Lezioni di sci* attraverso la loro appartenenza al gruppo *Community Ski Class*.](enablement-setup.md#publishcreateenablementmembers)

Accedi con

* `Username: riley`
* `Password: password`

Se il profilo utente non è stato creato mediante autoregistrazione, la prima volta che un membro effettua l’accesso viene visualizzata la relativa pagina Profilo in modo che possa verificarla e modificarla come necessario.

Al successivo accesso del membro, viene visualizzata la pagina principale, identificata dalla prima voce di menu.

![chlimage_1-434](assets/chlimage_1-434.png)

### Assegnazioni {#assignments}

Nella pagina Assegnazioni viene visualizzato il membro di tutti i percorsi di apprendimento e le risorse di abilitazione assegnate specificatamente a tale utente.

Ogni assegnazione fornisce informazioni di base su:

* Tipo di assegnazione
* Indica se si tratta di una nuova assegnazione
* Nome
* Dettagli relativi al tipo di assegnazione
* Contatto assegnazione, esperto e autore (se fornito)

Il tipo di assegnazione è indicato da un&#39;icona nell&#39;angolo superiore sinistro della scheda. L&#39;immagine di una strada è per un percorso di apprendimento con il numero di risorse di abilitazione incluse.

![chlimage_1-435](assets/chlimage_1-435.png)

Selezionando *Lezioni di sci* verranno visualizzate le due risorse di abilitazione a cui fa riferimento il percorso di apprendimento.

![chlimage_1-436](assets/chlimage_1-436.png)

Selezionando *Lezione sci 1* si aprirà la pagina dei dettagli della risorsa di abilitazione.

Dalla pagina dei dettagli, il membro è in grado di apprendere, [valutare](rating.md) la lezione e aggiungere [commenti](comments.md). Qualsiasi attività dei membri verrà riflessa nella sezione Novità del sito.

Le interazioni con la risorsa di abilitazione saranno riportate nella sezione Rapporto accessibile nell’ambiente di authoring.

![chlimage_1-437](assets/chlimage_1-437.png)

### Catalogo sci {#ski-catalog}

La pagina Catalogo sci è il catalogo di risorse di abilitazione con tag dallo spazio dei nomi `Tutorial`. Alle due risorse *Lezione sci* viene assegnato il tag `Skiing`, in modo che se sono selezionati tag diversi da `All` o `Tutorial: Sports / Skiing` non venga visualizzato nulla.

Se a un membro non sono state assegnate risorse di abilitazione, direttamente o attraverso un percorso di apprendimento, è possibile interagire con le risorse di abilitazione presenti in un catalogo e fornire feedback attraverso commenti e valutazioni.

![chlimage_1-438](assets/chlimage_1-438.png)

### Discussioni {#discussions}

Oltre a classificare e commentare le risorse di abilitazione ([se attivato](enablement-create-site.md#step33asettings)), il modello di sito community da cui è stato creato `Enablement Tutorial` include la funzione [forum](functions.md#forum-function) (il titolo è `Discussions)`).

Selezionate il collegamento `Discussions`e pubblicate un argomento.

Disconnettetevi ed effettuate l&#39;accesso come Sidney Croft (sidney / password) e rispondete alla domanda, oltre a seguire l&#39;argomento.

Notate che, oltre alla moderazione in linea, ci sono opzioni per condividere l&#39;argomento sui social media o per inviare l&#39;argomento via e-mail.

![chlimage_1-439](assets/chlimage_1-439.png)

### Novità {#what-s-new}

La voce di menu `What's New` è il titolo dato dalla [funzione di flusso di attività](functions.md#activity-stream-function) nella struttura del sito community.

Sempre con accesso come Sidney, selezionate il collegamento `What's New` per mostrare l&#39;attività.

![chlimage_1-440](assets/chlimage_1-440.png)

## Membro della community trusted {#trusted-community-member}

Questa esperienza presuppone che ` [Quinn Harper](enablement-setup.md#publishcreateenablementmembers)` sia stato assegnato il ruolo di [moderatore](enablement-create-site.md#moderation) e [contatto risorse](resource.md#settings).

Accedi con

* `Username: quinn`
* `Password: password`

Una volta effettuato l&#39;accesso, viene visualizzata una nuova voce di menu, `Administration`, in quanto al membro è stato assegnato il ruolo di moderatore.

![chlimage_1-441](assets/chlimage_1-441.png)

La pagina principale è identificata dalla prima voce di menu, Assegnazioni. Quinn è il contatto con le risorse di moderatore e abilitazione e non è stato registrato in alcuna risorsa di abilitazione o percorsi di apprendimento, pertanto non c&#39;è nulla da visualizzare.

### Amministrazione {#administration}

Ciò che esiste è l&#39;attività dei due studenti, `Riley Taylor` e `Sidney Croft`. Selezionando il collegamento `Administration` per accedere alla console di moderazione, Quinn può utilizzare la [console di moderazione di massa](moderation.md) per moderare i propri post.

Selezionando l&#39;icona del pannello laterale si aprono i filtri utilizzati per la ricerca di contenuti per le community.

Passando il puntatore su una scheda di commento vengono visualizzate le azioni di moderazione.

![chlimage_1-442](assets/chlimage_1-442.png)

## Report sull&#39;autore {#reports-on-author}

Esistono due modi per accedere ai rapporti sugli studenti e alle risorse di abilitazione.

Per l&#39;autore, andate alla **console Community, [Risorse](resources.md)**, in cui vengono gestite le risorse di abilitazione, e dopo aver selezionato un sito community, è possibile generare rapporti per

* Tutte le risorse di abilitazione e i percorsi di apprendimento
* Una risorsa di abilitazione o un percorso di apprendimento specifico

Andate alla **console Community, [Report](reports.md)** e generate i rapporti in base a:

* Assegnazioni per abilitare risorse e percorsi di apprendimento
* Post a un sito community su un periodo specifico
* Viste (visite al sito) di un sito community in un determinato periodo

* I post e le viste possono essere per tutto il contenuto o per contenuto specifico:

   * Forum
   * Topic forum
   * D/R
   * Domanda d/r
   * Blog
   * Articolo di blog
   * Calendario
   * Evento calendario

### Console risorse {#resources-console}

Con una piccola attività e un’interazione con le risorse durante la pubblicazione, la visualizzazione dei rapporti sull’autore merita un’occhiata.

* Per l’autore, effettuate l’accesso con privilegi amministrativi.
* Dal menu principale, passare a **[!UICONTROL Communities]** > **[!UICONTROL Resources]**.
* Selezionare il sito `Enablement Tutorial`.
* Selezionate l&#39;icona `Report` per un riepilogo di tutte le risorse.
* Selezionare una risorsa, quindi l&#39;icona `Report` per il rapporto su tale risorsa.

Notare che è probabile che troppo presto per visualizzare i dati da  Adobe Analytics, che può richiedere da 1 a 12 ore di visualizzazione. Tuttavia, il reporting SCORM di base è già disponibile.

#### Rapporto sulle risorse delle lezioni di sci {#ski-lessons-resource-report}

![chlimage_1-443](assets/chlimage_1-443.png)

#### Rapporto utente sulle lezioni di sci {#ski-lessons-user-report}

* Selezionare **[!UICONTROL Communities > Resources]**

* Open card `Enablement Tutorial`
* Open card `Ski Lessons`
* Seleziona `Report > User Report`

![chlimage_1-444](assets/chlimage_1-444.png)

### Console Rapporti {#reports-console}

La console Rapporti consente la generazione di rapporti su

* **Assegnazioni** per qualsiasi sito di abilitazione community
* **** Visualizzazioni per qualsiasi sito community
* **** Post per qualsiasi sito community

Per i rapporti sulle assegnazioni:

* Per l’autore, effettuate l’accesso con privilegi amministrativi.
* Andate a **[!UICONTROL Communities]** > **[!UICONTROL Reports]** > **[!UICONTROL Assignments Report]** (Rapporto assegnazioni).
* Selezionare un **[!UICONTROL sito]** dal menu a discesa (selezionare `Enablement Tutorial`).

* Selezionare **[!UICONTROL Group]** (selezionare `Community Ski Class`)

* Selezionare una **[!UICONTROL assegnazione]** (selezionare `Ski Lessons`)

* Selezionare **[!UICONTROL Generate]**

![chlimage_1-445](assets/chlimage_1-445.png)

Per i rapporti sulle visualizzazioni:

* Per l’autore, effettuate l’accesso con privilegi amministrativi.
* Andate a **[!UICONTROL Communities]** > **[!UICONTROL Reports]** > **[!UICONTROL Views Report]**.
* Selezionare un **sito** dal menu a discesa (selezionare `Enablement Tutorial`).

* Selezionare **[!UICONTROL Tipo di contenuto]** (selezionare `all`).

* Selezionare un **[!UICONTROL intervallo di date]** (selezionare `Last 7 days`).

* Selezionare **[!UICONTROL Generate]**.

![chlimage_1-446](assets/chlimage_1-446.png)

**[⇐ creare e assegnare risorse di abilitazione](resource.md)**
