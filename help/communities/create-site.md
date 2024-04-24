---
title: Creare un sito community
description: Scopri come creare un sito di Adobe Experience Manager Communities.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: d4c1895f-421c-4146-b94a-8d11065ef9e3
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1556'
ht-degree: 0%

---

# Creare un sito community{#author-a-new-community-site}

## Creare un sito community {#create-a-community-site}

Utilizza l’istanza di authoring per creare un sito community. Sull’istanza dell’autore AEM:

1. Accedi con privilegi di amministratore.
1. Dalla navigazione globale, vai a **[!UICONTROL Community]** > **[!UICONTROL Sites]**.

La console Siti di Communities offre una procedura guidata per illustrare i passaggi necessari per la creazione di un sito di community. È possibile passare alla `Next` passaggio o `Back` al passaggio precedente prima di eseguire il commit del sito nel passaggio finale.

Per iniziare a creare un sito community:

* Seleziona la `Create` pulsante.

![createcommunity site](assets/createcommunitysite.png)

### Passaggio 1: modello del sito {#step-site-template}

![modello per creare il sito](assets/create-site.png)

Il giorno [Passaggio modello sito](/help/communities/sites-console.md#step2013asitetemplate), immettere un titolo, una descrizione, il nome dell&#39;URL e selezionare un modello di sito community, ad esempio:

* **Titolo sito community**: `Getting Started Tutorial`
* **Descrizione del sito community**: `A site for engaging with the community.`
* **Directory principale sito community**: (lascia vuoto per impostare la directory principale predefinita) `/content/sites`)
* **Configurazioni cloud**: (lascia vuoto se non è specificata alcuna configurazione cloud) specifica il percorso delle configurazioni cloud specificate.
* **Lingua base del sito community**: (non toccare per una singola lingua: inglese) utilizza l’elenco a discesa per sceglierne uno *o più* lingue di base delle lingue disponibili: tedesco, italiano, francese, giapponese, spagnolo, portoghese (Brasile), cinese (tradizionale) e cinese (semplificato). Viene creato un sito community per ogni lingua aggiunta ed esiste nella stessa cartella del sito seguendo la best practice descritta in [Traduzione di contenuti per siti multilingue](/help/sites-administering/translation.md). La pagina principale di ciascun sito contiene una pagina figlia denominata con il codice della lingua di una delle lingue selezionate, ad esempio &#39;en&#39; per l&#39;inglese o &#39;fr&#39; per il francese.

* **Nome sito community**: interagire

   * Ricontrolla il nome poiché non è più facile modificarlo dopo la creazione del sito
   * L&#39;URL iniziale viene visualizzato sotto il nome del sito community
   * Per un URL valido, aggiungi un codice della lingua di base + &quot;.html&quot;
   * *Ad esempio*, https://localhost:4502/content/sites/ `engage/en.html`

* **Modello**: seleziona per scegliere `Reference Site`

* Seleziona **Avanti**.

### Passaggio 2: Progettazione {#step-design}

Il passaggio Progettazione è presentato in due sezioni per la selezione del tema e del banner di branding:

#### TEMA DEL SITO COMMUNITY {#community-site-theme}

Seleziona lo stile desiderato da applicare al modello. Quando è selezionata, il tema viene sovrapposto con un segno di spunta.

#### MARCHIO PER SITO COMMUNITY {#community-site-branding}

(Facoltativo) Carica un&#39;immagine del banner da visualizzare nelle pagine del sito. Il banner è fissato al bordo sinistro del browser, tra l&#39;intestazione del sito community e i collegamenti di navigazione. L&#39;altezza del banner viene ridotta a 120 pixel. Il banner non viene ridimensionato in base alla larghezza del browser e all&#39;altezza di 120 pixel.

![community-site-branding](assets/community-site-branding.png)

![upload-image-site](assets/upload-image-site.png)

Seleziona **Avanti**.

### Passaggio 3: Impostazioni {#step-settings}

Nel passaggio Impostazioni, prima di selezionare `Next`, ci sono sette sezioni che forniscono accesso a configurazioni che coinvolgono la gestione degli utenti, l’assegnazione di tag, la moderazione, la gestione dei gruppi, le analisi e la traduzione.

#### User Management {#user-management}

Seleziona tutte le caselle di controllo per [Gestione utente](/help/communities/sites-console.md#user-management)

* Per consentire ai visitatori del sito di registrarsi autonomamente
* Per consentire ai visitatori del sito di visualizzare il sito senza effettuare l&#39;accesso
* Per consentire ai membri di inviare e ricevere messaggi da altri membri della community
* Per consentire l’accesso con Facebook anziché registrare e creare un profilo
* Per consentire l&#39;accesso con il Twitter invece di registrare e creare un profilo

>[!NOTE]
>
>Per un ambiente di produzione, è necessario creare applicazioni Facebook e di Twitter personalizzate. Consulta [Accesso social network con Facebook e Twitter](/help/communities/social-login.md).

![impostazioni del sito community](assets/site-settings.png)

#### ASSEGNAZIONE TAG {#tagging}

I tag applicati al contenuto della community sono controllati selezionando gli spazi dei nomi AEM precedentemente definiti tramite [Console per assegnazione tag](/help/sites-administering/tags.md#tagging-console) (ad esempio [Spazio dei nomi dell’esercitazione](/help/communities/setup.md#create-tutorial-tags)).

Trovare gli spazi dei nomi è facile con la ricerca del tipo-ahead. Ad esempio:

* Tipo `tut`
* Seleziona `Tutorial`

![assegnazione tag](assets/tagging.png)

#### RUOLI {#roles}

[Ruoli dei membri della community](/help/communities/users.md) vengono assegnati tramite le impostazioni nella sezione Ruoli.

Per consentire a un membro della community (o a un gruppo di membri) di utilizzare il sito come manager della community, utilizzare la ricerca di completamento automatico e selezionare il nome del membro o del gruppo tra le opzioni disponibili nel menu a discesa.

Ad esempio:

* Tipo `q`
* Seleziona Quinn Harper

>[!NOTE]
>
>[Servizio tunnel](https://helpx.adobe.com/experience-manager/6-3/help/communities/deploy-communities.html#tunnel-service-on-author) consente di selezionare i membri e i gruppi esistenti solo nell&#39;ambiente di pubblicazione.

![ruoli utente nel nuovo sito](assets/site-admin-1.png)

#### MODERAZIONE {#moderation}

Accetta le impostazioni globali predefinite per [moderazione](/help/communities/sites-console.md#moderation) contenuti generati dall&#39;utente (UGC, user-generated content).

![moderazione](assets/moderation1.png)

#### ANALISI {#analytics}

Se Adobe Analytics è concesso in licenza e sono stati configurati un servizio e un framework di Analytics Cloud, è possibile abilitare Analytics e selezionare il framework.

Consulta [Configurazione di Analytics per le funzioni di Communities](/help/communities/analytics.md).

![analisi](assets/analytics.png)

#### TRADUZIONE {#translation}

Il [Impostazioni di traduzione](/help/communities/sites-console.md#translation) specifica la lingua di base per il sito, se il linguaggio UGC può essere tradotto e in quale lingua.

* Verifica **Consenti traduzione automatica**
* Lascia le lingue predefinite selezionate per la traduzione dal servizio di traduzione automatica predefinito
* Lascia provider di traduzione e configurazione predefiniti
* Non è necessario uno store globale perché non sono presenti copie in lingua
* Seleziona **Traduci intera pagina**
* Lascia opzione di persistenza predefinita

![translation-settings](assets/translation-settings.png)

### Passaggio 4: creare il sito community {#step-create-communities-site}

Seleziona **Crea.**

![create-site](assets/create-site2.png)

Al termine del processo, la cartella per il nuovo sito viene visualizzata nella console Community - Sites.

![communitiesconsole](assets/communitiessitesconsole.png)

## Pubblica il sito community {#publish-the-community-site}

Il sito creato deve essere gestito dalla console Community - Sites, la stessa da cui è possibile creare nuovi siti.

Dopo aver selezionato la cartella del sito community per aprirla, passa il puntatore sull&#39;icona del sito in modo da visualizzare quattro icone di azione:

![siteactionicons-1](assets/siteactionicons-1.png)

Quando selezioni la quarta icona con i puntini di sospensione (Altre azioni), vengono visualizzate le opzioni Esporta sito ed Elimina sito.

![siteactionsnew-1](assets/siteactionsnew-1.png)

Da sinistra a destra:

* **Apri sito**

  Selezionando l’icona a forma di matita si apre il sito community in modalità di modifica Creazione, dove è possibile aggiungere o configurare i componenti della pagina.

* **Modifica sito**

  Selezionando l&#39;icona delle proprietà si apre il sito community per modificare le proprietà, ad esempio il titolo o il tema.

* **Pubblica sito**

  Se si seleziona l&#39;icona mondo, il sito community verrà pubblicato (ad esempio, se il server di pubblicazione è in esecuzione sul computer locale, su localhost:4503 per impostazione predefinita).

* **Esporta sito**

  Selezionando l&#39;icona di esportazione viene creato un pacchetto del sito community memorizzato in [Gestione pacchetti](/help/sites-administering/package-manager.md) e scaricato. UGC non incluso nel pacchetto del sito.

* **Elimina sito**

  Se si seleziona l&#39;icona Elimina, il sito community verrà eliminato da **[!UICONTROL Community > Console Sites]**. Questa azione rimuove tutti gli elementi associati al sito, ad esempio UGC, gruppi di utenti, risorse e record di database.

![siteactions](assets/siteactions.png)

>[!NOTE]
>
>Se non utilizzi la porta predefinita 4503 per l’istanza Publish, modifica l’agente di replica predefinito per impostare il numero della porta sul valore corretto.
>
>Nell’istanza di authoring, dal menu principale:
>
>1. Accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Replica]** menu.
>1. Seleziona **[!UICONTROL Agenti per creazione]**.
>1. Seleziona **[!UICONTROL Agente predefinito (pubblicazione)]**.
>1. Accanto a **[!UICONTROL Impostazioni]**, seleziona **[!UICONTROL Modifica]**.
>1. Nella finestra di dialogo a comparsa per Impostazioni agente, seleziona **[!UICONTROL Trasporto]** scheda.
>1. In URI, modificare il numero di porta, 4503, nel numero di porta desiderato. Ad esempio, per utilizzare la porta 6103: https://localhost:6103/bin/receive?sling:authRequestLogin=1
>1. Seleziona **[!UICONTROL OK]**.
>1. (Facoltativo) Seleziona **[!UICONTROL Cancella]** o **[!UICONTROL Forza nuovo tentativo]** per reimpostare la coda di replica.

### Seleziona pubblicazione {#select-publish}

Dopo aver verificato che il server di pubblicazione sia in esecuzione, seleziona l’icona mondo per pubblicare il sito community.

![publish-site](assets/publish-site.png)

Dopo la pubblicazione del sito community, viene visualizzato brevemente il messaggio Sito pubblicato.

### Nuovi gruppi di utenti della community {#new-community-user-groups}

Insieme al nuovo sito della community, vengono creati nuovi gruppi di utenti che dispongono delle autorizzazioni appropriate impostate per diverse funzioni amministrative. Per ulteriori informazioni, visitare il sito [Gruppi di utenti per i siti community](/help/communities/users.md#usergroupsforcommunitysites).

Per questo nuovo sito community, dato il nome del sito &quot;coinvolgimento&quot; nel passaggio 1, i quattro nuovi gruppi di utenti possono essere visualizzati dalla sezione [Console Gruppi](/help/communities/members.md) (navigazione globale: Community, Gruppi):

* Community Engage manager
* Amministratori del gruppo Community Engage
* Membri del coinvolgimento community
* Moderatori del coinvolgimento della community
* Membri con privilegi di coinvolgimento community
* Gestione contenuti del sito community Engage

[Aaron McDonald](/help/communities/tutorials.md#demo-users) è un membro di

* Community Engage manager
* Moderatori del coinvolgimento della community
* Membri del coinvolgimento della community (indirettamente come membro del gruppo Moderatori)

![user-group](assets/user-group.png)

#### https://localhost:4503/content/sites/engage/en.html {#http-localhost-content-sites-engage-en-html}

![coinvolgere](assets/engage.png)

## Errore di configurazione per l’autenticazione {#configure-for-authentication-error}

Una volta configurato il sito e inviato per la pubblicazione, [configurare la mappatura di accesso](/help/communities/sites-console.md#configure-for-authentication-error) ( `Adobe Granite Login Selector Authentication Handler`) sull&#39;istanza Publish. Il vantaggio è che quando le credenziali di accesso non vengono immesse correttamente, l&#39;errore di autenticazione visualizza nuovamente la pagina di accesso del sito community con un messaggio di errore.

Aggiungi un `Login Page Mapping` as

* `/content/sites/engage/en/signin:/content/sites/engage/en`

## Passaggi facoltativi {#optional-steps}

### Modificare la home page predefinita {#change-the-default-home-page}

Quando si lavora con il sito pubblicato a scopo dimostrativo, potrebbe essere utile impostare la home page predefinita sul nuovo sito.

Per farlo è necessario utilizzare [CRXDE](https://localhost:4503/crx/de) Lite per modificare il [mappatura delle risorse](/help/sites-deploying/resource-mapping.md) tabella sulla pubblicazione.

Per iniziare:

1. Nell’istanza di pubblicazione, accedi con privilegi di amministratore.
1. Sfoglia per [https://localhost:4503/crx/de](https://localhost:4503/crx/de).
1. Nel browser del progetto, espandi `/etc/map.`
1. Seleziona la `http` nodo:

   * Seleziona **Crea nodo:**

      * **Nome** localhost.4503 (do *non* usa &#39;:&#39;)

      * **Tipo** [sling:mappatura](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)

1. Con nuova creazione `localhost.4503` nodo selezionato:

   * Aggiungi proprietà:

   * **Nome** sling:match
      * **Tipo** Stringa
      * **Valore** localhost.4503/$ (deve terminare con &#39;$&#39; char)

   * Aggiungi proprietà:

      * **Nome** sling:internalRedirect
      * **Tipo** Stringa
      * **Valore** /content/sites/engage/en.html

1. Seleziona **Salva tutto.**
1. (Facoltativo) Elimina la cronologia esplorazioni.
1. Passa a https://localhost:4503/.

   * Arrivare a https://localhost:4503/content/sites/engage/en.html

>[!NOTE]
>
>Per disattivare, utilizza il prefisso `sling:match` valore della proprietà con una &quot;x&quot; - `xlocalhost.4503/$` - e **Salva tutto**.

![optional-steps](assets/optional-steps.png)

#### Risoluzione dei problemi: errore durante il salvataggio della mappa {#troubleshooting-error-saving-map}

Se non è possibile salvare le modifiche, assicurati che il nome del nodo sia `localhost.4503`, con un separatore di &#39;punto&#39; e non `localhost:4503` con un separatore &quot;due punti&quot;, come `localhost`non è un prefisso valido per lo spazio dei nomi.

![error-message](assets/error-message.png)

#### Risoluzione dei problemi: impossibile reindirizzare {#troubleshooting-fail-to-redirect}

L&#39;&#39;**$**&#39; alla fine dell&#39;espressione regolare `sling:match`è fondamentale, in modo che solo `https://localhost:4503/` è mappato, altrimenti il valore di reindirizzamento viene anteposto a qualsiasi percorso che potrebbe esistere dopo server:porta nell’URL. Pertanto, quando l’AEM tenta di reindirizzare alla pagina di accesso, questo non riesce.

### Modificare il sito {#modify-the-site}

Dopo la creazione iniziale del sito, gli autori possono utilizzare [Icona Apri sito](/help/communities/sites-console.md#authoring-site-content) eseguire le attività standard di creazione AEM.

Inoltre, gli amministratori possono utilizzare [Icona Modifica sito](/help/communities/sites-console.md#modifying-site-properties) per modificare le proprietà del sito, ad esempio il titolo.

Dopo eventuali modifiche, ricorda di: **Salva** e re-mail **Pubblica** il sito.

>[!NOTE]
>
>Se non conosci l’AEM, consulta la documentazione su [operazioni di base](/help/sites-authoring/basic-handling.md) e un [guida rapida all’authoring delle pagine](/help/sites-authoring/qg-page-authoring.md).
