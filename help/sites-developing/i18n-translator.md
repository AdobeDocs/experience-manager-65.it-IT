---
title: Utilizzo di Translator per gestire i dizionari
seo-title: Using Translator to Manage Dictionaries
description: AEM fornisce una console per la gestione delle varie traduzioni di testi utilizzati nell’interfaccia utente dei componenti
seo-description: AEM provides a console for managing the various translations of texts used in component UI
uuid: 4eea3110-e958-473e-8d22-c84fa435edbd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
discoiquuid: adf3364c-11f1-45c6-b41d-2c7d48b626f9
exl-id: a8d50c09-72d0-406e-874e-50a985227a56
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2325'
ht-degree: 1%

---

# Utilizzo di Translator per gestire i dizionari{#using-translator-to-manage-dictionaries}

AEM fornisce una console per la gestione delle varie traduzioni di testi utilizzati nell’interfaccia utente dei componenti. Questa console è disponibile in

`https://<hostname>:<port-number>/libs/cq/i18n/translator.html`

Utilizza lo strumento di traduzione per gestire le stringhe inglesi e le loro traduzioni. I dizionari vengono creati nell’archivio, ad esempio /apps/myproject/i18n.

Lo strumento Traduttore e i dizionari gestiti consentono di presentare l’interfaccia utente dei componenti in lingue diverse. Per tradurre la pagina o il contenuto generato dall’utente, consulta [Traduzione di contenuti per siti multilingue](/help/sites-administering/translation.md) e [Traduzione di contenuti generati dagli utenti](/help/communities/translate-ugc.md).

>[!CAUTION]
>
>Modifica solo i dizionari creati per il progetto e che risiedono in `/apps`.
>
>AEM dizionari di sistema sono disponibili anche in questo strumento. Non modificare i dizionari di sistema AEM in quanto questo può causare problemi con l’interfaccia utente AEM. Inoltre, le modifiche possono andare perse dopo l&#39;aggiornamento. I dizionari di sistema AEM si trovano in `/libs`.

>[!NOTE]
>
>Sebbene lo strumento di traduzione abbia un’interfaccia classica, viene utilizzato per la traduzione di frasi indipendentemente dall’interfaccia in cui tali frasi vengono trovate.

Il traduttore elenca insieme i testi utilizzati in AEM con le varie traduzioni linguistiche:

![chlimage_1-205](assets/chlimage_1-205.png)

È possibile cercare, filtrare e modificare l&#39;inglese e i testi tradotti. Puoi anche esportare i dizionari in formato XLIFF per la traduzione, quindi importare di nuovo le traduzioni nei dizionari.

È anche possibile aggiungere i dizionari i18n a un progetto di traduzione da questa console. Puoi crearne uno nuovo o aggiungerlo a un progetto esistente.

1. Fai clic su **Traduci dizionario**.

   ![chlimage_1-206](assets/chlimage_1-206.png)

1. Seleziona l’opzione Crea o Aggiungi a seconda delle tue esigenze. Viene visualizzata una finestra di dialogo.

   ![chlimage_1-207](assets/chlimage_1-207.png)

1. Compila i campi come richiesto e fai clic su OK. ![chlimage_1-208](assets/chlimage_1-208.png)

1. Ora puoi fare clic su **OK** oppure consulta il Dizionario di Target .

   >[!NOTE]
   >
   >Per ulteriori informazioni sui progetti di traduzione, consulta [Gestione dei progetti di traduzione](/help/sites-administering/tc-manage.md).

## Creazione di un dizionario {#creating-a-dictionary}

Crea un dizionario per la gestione delle stringhe di interfaccia utente localizzate. Dopo aver creato un dizionario è possibile utilizzare lo strumento di traduzione per gestirlo.

1. Utilizzando CRXDE Lite, aggiungi il nodo principale ( `sling:Folder`) per il nuovo dizionario come struttura per le definizioni delle lingue:

   ` /apps/<projectName>/i18n`

   Esempio, `/apps/myProject/i18n`

1. Aggiungi la struttura della lingua richiesta sotto questa radice. Esempio:

   ```shell
   /apps/myProject/i18n [sling:Folder]
       - de.json [nt:file] [mix:language]
           + jcr:language = de
       - fr.json [nt:file] [mix:language]
           + jcr:language = fr
   ```

   >[!NOTE]
   >
   >Questa è la struttura dal [Modulo Sling i18n](https://sling.apache.org/site/internationalization-support.html).

1. Ricarica il traduttore e il percorso del dizionario (ad es. `/apps/myProject/i18n`) sarà disponibile nel selettore a discesa nella barra degli strumenti. Seleziona questa opzione per iniziare ad aggiungere stringhe e relative traduzioni.

   >[!NOTE]
   >
   >Il traduttore salverà solo le traduzioni per le lingue che sono effettivamente presenti sotto il percorso (ad es. `/apps/myProject/i18n`).
   >
   >Assicurati che corrispondano alle lingue mostrate nella griglia.

## Gestione delle stringhe del dizionario {#managing-dictionary-strings}

Utilizza lo strumento di traduzione per gestire le stringhe nei dizionari. È possibile aggiungere, modificare e rimuovere stringhe in lingua inglese, nonché fornire stringhe tradotte.

>[!CAUTION]
>
>Modifica solo i dizionari creati per il progetto e che risiedono in `/apps`.
>
>Non modificare i dizionari di sistema AEM in quanto questo può causare problemi con l’interfaccia utente AEM. Inoltre, le modifiche possono andare perse dopo l&#39;aggiornamento. I dizionari di sistema AEM si trovano in `/libs`.

### Aggiunta, modifica e rimozione di stringhe {#adding-changing-and-removing-strings}

Aggiungi stringhe in inglese a un dizionario internazionalizzato dal componente. Aggiungi solo stringhe internazionalizzate in modo da non sprecare risorse traducendo stringhe non utilizzate.

Le stringhe aggiunte a un dizionario devono corrispondere esattamente alla stringa specificata nel codice. Se la stringa inglese predefinita utilizzata nel codice non corrisponde alla stringa inglese in un dizionario, la stringa tradotta non viene visualizzata nell&#39;interfaccia utente quando necessario. Le stringhe distinguono tra maiuscole e minuscole.

**Fornire suggerimenti di traduzione**

Utilizzare la proprietà Commento della stringa dizionario per fornire informazioni al traduttore per chiarire il significato della stringa. In genere, l’interfaccia utente aiuta gli utenti a determinare il significato di parole ambigue. Tuttavia, il traduttore non visualizza la stringa nel contesto dell&#39;interfaccia utente. Il suggerimento di traduzione rimuove l&#39;ambiguità. Ad esempio, un commento aiuta il traduttore a capire che la parola inglese Request viene utilizzata come sostantivo anziché come verbo.

I suggerimenti di traduzione distinguono anche le stringhe che sono identiche e hanno significati diversi. Ad esempio, la parola Ricerca può essere un sostantivo o un verbo, che richiede due voci &quot;Cerca&quot; nel dizionario con due diversi suggerimenti di traduzione. Il codice che richiede la stringa include anche l&#39;hint di traduzione in modo che la stringa corretta venga utilizzata nell&#39;interfaccia utente.

**Inclusione di variabili indicizzate**

Includi le variabili nella stringa localizzata per creare un significato contestuale in una frase. Ad esempio, dopo aver effettuato l&#39;accesso a un&#39;applicazione Web, nella home page viene visualizzato il messaggio &quot;Bentornato Amministratore. Hai 2 messaggi nella tua casella in entrata.&quot; Il contesto della pagina determina il nome utente e il numero di messaggi.

Per includere le variabili nella stringa localizzata, posiziona gli indici tra parentesi nella posizione delle variabili nel primo argomento del metodo get. Utilizza il suggerimento di localizzazione per descrivere i valori. Il traduttore deve capire il significato delle variabili perché le diverse lingue utilizzano strutture di frase diverse.

Tieni presente che [il codice che richiede la stringa tradotta](/help/sites-developing/i18n-dev.md#including-variables-in-localized-sentences) fornisce valori per le variabili indicizzate in base al contesto.

Ad esempio, la stringa seguente viene visualizzata quando un utente accede a un sito Web e viene inclusa nel dizionario:

`Welcome back {0}. You have {1} messages.`

Il commento seguente descrive le variabili:

`{0} = the user name, {1} = the number of items in the user's inbox`

**Modifica delle stringhe**

Modifica o rimuovi le stringhe inglesi mano a mano che vengono modificate o rimosse nel codice. Quando si modifica una stringa, la stringa originale viene mantenuta e viene creata una nuova stringa che riflette la modifica. Prima di rimuovere una stringa, accertati che nessun codice la utilizzi.

Per aggiungere una stringa, attenersi alla procedura descritta di seguito.

1. Nel menu a discesa Dizionari , seleziona il dizionario al quale si sta aggiungendo una stringa. Nel menu a discesa, i dizionari sono rappresentati dal loro percorso nel repository.
1. Sopra la tabella Stringhe e traduzioni fare clic su Aggiungi.

   ![chlimage_1-209](assets/chlimage_1-209.png)

1. Nella casella Stringa della finestra di dialogo Aggiungi stringa digitare la stringa inglese. Nella casella Commento digitare un suggerimento di traduzione per il traduttore, se necessario.
1. Fai clic su OK.
1. Fai clic su Salva.

   ![chlimage_1-210](assets/chlimage_1-210.png)

Per modificare una stringa in un dizionario, attenersi alla procedura descritta di seguito.

1. Nel menu a discesa Dizionari , seleziona il dizionario contenente la stringa da modificare.
1. Fare doppio clic sulla stringa da modificare.
1. Nella finestra di dialogo Modifica stringa, selezionare Modifica stringa o commento (crea una copia).

   ![chlimage_1-211](assets/chlimage_1-211.png)

1. Modificare la stringa o il commento e fare clic su OK.
1. Fai clic su Salva.

   ![chlimage_1-212](assets/chlimage_1-212.png)

Per rimuovere una stringa da un dizionario, attenersi alla procedura descritta di seguito.

1. Nel menu a discesa Dizionari selezionare il dizionario da cui si sta rimuovendo una stringa.
1. Fai clic su Rimuovi.

   ![chlimage_1-213](assets/chlimage_1-213.png)

1. Fai clic su Salva.

   ![chlimage_1-214](assets/chlimage_1-214.png)

### Ricerca di stringhe {#searching-for-strings}

La barra di ricerca nella parte inferiore dello strumento Traduttore fornisce le opzioni di selezione delle stringhe:

* **Filtra per testo:** Pattern da abbinare alla stringa, al commento o alle traduzioni in inglese. Nella tabella vengono visualizzati solo gli elementi che corrispondono interamente o in parte al pattern.
* **Modifiche: Qualsiasi, Modificato, Nuovo, Eliminato:** Mostra gli elementi modificati e non salvati.

   * Qualsiasi: Mostra gli elementi modificati, aggiunti o rimossi.
   * Modificato: Mostra gli elementi modificati.
   * Novità: Mostra gli elementi aggiunti.
   * Eliminato: Mostra gli elementi da rimuovere.
   * Selezioni multiple: Mostra elementi con tutte le proprietà selezionate.

* **Con commento**: Mostra gli elementi che contengono commenti per i traduttori.
* **Traduzioni mancanti:** Mostra gli elementi in cui almeno una lingua non ha una traduzione.

![chlimage_1-215](assets/chlimage_1-215.png)

1. Nella barra di ricerca, seleziona le opzioni di filtro.
1. Per filtrare utilizzando le opzioni, fare clic su Filtro.
1. Per rimuovere i filtri e visualizzare tutti gli elementi nel dizionario, fare clic su Cancella.

### Modifica di stringhe tradotte {#editing-translated-strings}

Dopo aver aggiunto la stringa inglese a un dizionario, puoi aggiungere traduzioni della stringa. È inoltre possibile [esportare il dizionario](/help/sites-developing/i18n-translator.md#exporting-a-dictionary) affinché sia tradotto da terzi.

1. Seleziona [dizionario specifico per il progetto](#creating-a-dictionary) come specifica il percorso nell&#39;archivio contenente le traduzioni. Ad esempio, seleziona **Dizionari** come:

   `/apps/myProject/i18n`

   >[!CAUTION]
   >
   >Modifica solo i dizionari creati per il progetto e che risiedono in `/apps`.
   >
   >AEM dizionari di sistema sono disponibili anche in questo strumento. Non modificare i dizionari di sistema AEM in quanto questo può causare problemi con l’interfaccia utente AEM. Inoltre, le modifiche possono andare perse dopo l&#39;aggiornamento. I dizionari di sistema AEM si trovano in `/libs`.

1. Per modificare i testi tradotti per una delle stringhe è possibile:

   * Fare doppio clic sulla lingua appropriata per la stringa richiesta per modificare il testo singolo:

   ![chlimage_1-216](assets/chlimage_1-216.png)

   * Fai doppio clic sul pulsante **Stringa** o **Commento** campi per la stringa richiesta per aprire il **Modifica stringa** finestra di dialogo, modifica le traduzioni in base alle esigenze, quindi fai clic su **OK** per chiudere la finestra di dialogo:

   ![chlimage_1-217](assets/chlimage_1-217.png)

1. Fai clic su **Salva** nella barra degli strumenti per eseguire il commit delle modifiche.

   >[!NOTE]
   >
   >Clic su **Reimposta e aggiorna** (anziché **Salva**) ripristina le modifiche apportate ai testi precedenti.

## Utilizzo di traduttori di terze parti {#using-third-party-translators}

Per supportare l’utilizzo di servizi di traduzione di terze parti, lo strumento di traduzione consente di esportare e importare dizionari.

### Esportazione di un dizionario {#exporting-a-dictionary}

Esporta un dizionario in un file XLIFF in modo che un servizio di terze parti possa tradurre le stringhe del dizionario.

* Esportare un dizionario e includere l&#39;inglese e i termini tradotti per una lingua.
* Esporta alcune o tutte le stringhe inglesi.

Quando si esporta un file XLIFF e si include una lingua, la struttura del nodo del dizionario nell&#39;archivio deve includere tale lingua. Se la lingua non è inclusa, si verificano degli errori. Ad esempio, per esportare il file XLIFF francese, la cartella del dizionario deve includere il `mix:language` nodo figlio denominato `fr`. (Vedi [Creazione di un dizionario](/help/sites-developing/i18n-translator.md#creating-a-dictionary).)

Segui la procedura seguente per esportare un file XLIFF per una lingua specifica.

1. Apri lo strumento di traduzione `http://<host>:<port>/libs/cq/i18n/translator.html`
1. Utilizza il menu a discesa Dizionari per selezionare il dizionario da esportare.
1. Fai clic su Esporta > Esporta completo *XX* Opzioni Xliff, dove *XX* è il codice della lingua a due lettere, ad esempio DE o FR.

   Il file XLIFF si apre in una nuova scheda o finestra.

1. Utilizzare i comandi del browser Web per salvare la pagina come file nel file system, ad esempio File > Salva pagina con nome.

Utilizzare la procedura seguente per esportare tutte o alcune delle stringhe inglesi.

1. Apri lo strumento Traduzione . `http://<host>:<port>/libs/cq/i18n/translator.html`
1. Utilizza il menu a discesa Dizionari per selezionare il dizionario da esportare.
1. Se stai esportando un sottoinsieme di stringhe, seleziona gli elementi nel dizionario da esportare. Selezionando nessun articolo vengono esportati tutti gli articoli.
1. Fai Clic Su Esporta > Esporta Selezione Come Xliff (Solo Stringhe).
1. Nella finestra di dialogo visualizzata, copiare il testo e incollarlo in un file di testo.

### Importazione di un dizionario {#importing-a-dictionary}

Importa un file XLIFF in un dizionario per compilare il dizionario. Quando il dizionario include una traduzione per una stringa inglese e il file XLIFF contiene una traduzione diversa per la stessa stringa, la traduzione del dizionario viene sostituita.

1. Apri lo strumento di traduzione `http://<host>:<port>/libs/cq/i18n/translator.html`
1. Fai clic su Importa > Traduzioni XLIFF.
1. Selezionare il file da importare e fare clic su OK.

## Gestione delle lingue supportate {#managing-supported-lanuages}

Aggiungi o rimuovi le lingue supportate dallo strumento di traduzione e fornite agli utenti delle tue pagine web.

### Modifica delle lingue elencate nella tabella del dizionario {#changing-languages-listed-in-the-dictionary-table}

Lo strumento Traduttore include le seguenti lingue nella tabella del dizionario:

* de - tedesco
* fr - Francese
* it - Italiano
* es - Spagnolo
* ja - Giapponese
* pt-br - Portoghese brasiliano
* zh-cn - Cinese semplificato
* zh-tw - Cinese tradizionale (supporto limitato)
* ko-kr - Coreano

Per aggiungere o rimuovere le lingue, attenersi alla procedura descritta di seguito.

1. Utilizzando CRXDE Lite, crea un nuovo nodo:

   `/etc/languages`

1. In questo nodo, crea una proprietà:

   * **Nome**: `languages`
   * **Tipo**: `Multi-String`
   * **Valore**: elenco delle lingue che si desidera visualizzare. Esempio:

      * fr
      * es

   >[!NOTE]
   >
   >I codici della lingua devono essere minuscoli.

1. Fai clic su **Salva tutto** in CRXDE Lite e ricarica il traduttore. La griglia viene aggiornata per mostrare le lingue definite.

   >[!NOTE]
   >
   >Il traduttore salverà solo le traduzioni per le lingue che sono in realtà [presente nel dizionario](#creating-a-dictionary) (ovvero sotto il percorso del dizionario, come `/apps/myProject/i18n`).
   >
   >Assicurati che corrispondano alle lingue mostrate nella griglia.

### Rendere le lingue disponibili agli autori {#making-languages-available-to-authors}

Dopo aver definito un dizionario per una lingua nuova nell’istanza AEM, devi renderlo disponibile per la selezione da parte degli autori (ad esempio, per l’utilizzo in **Preferenze**):

1. Per modificare l’elenco delle lingue disponibili in **Preferenze** del **Sicurezza** console:

   1. Crea una sovrapposizione nel codice dell&#39;applicazione per:

      ```
              /libs/cq/security/widgets/source/widgets/security/Preferences.js
       and update as required.
      ```

1. Per rendere disponibile la lingua in **Preferenze** dal **Siti Web** console è necessario apportare le seguenti modifiche all’interno dell’applicazione:

   1. Crea una sovrapposizione per la struttura in:

      `/libs/cq/security/content/tools/userProperties`

   1. All’interno della sovrapposizione aggiorna l’elenco delle lingue sotto:

      `items/common/items /lang/options`

1. Salva tutto e ricarica la console appropriata.

### Modifica dei nomi delle lingue e dei paesi predefiniti {#changing-language-names-and-default-countries}

Diversi paesi utilizzano la stessa lingua, ad esempio gli Stati Uniti, il Regno Unito e l&#39;Australia utilizzano tutti l&#39;inglese. Questo codice indica sia la lingua che il paese come `en_US`, `en_GB` e `en_AU`.

I paesi predefiniti vengono utilizzati quando vengono visualizzati dei flag (ad esempio nella finestra di dialogo copia lingua), per risolvere il paese in caso di codice lingua.

>[!NOTE]
>
>Per le localizzazioni gestite dal traduttore sopra, funziona solo la lingua esatta. Se il menu a discesa delle preferenze della lingua utilizza `en_uk`, deve esserci un `en_uk` dizionario nella directory archivio.

Per modificare le definizioni predefinite:

1. Un elenco delle lingue è memorizzato in:

   `/libs/wcm/core/resources/languages`

   Sovrapponi copiandolo in:

   `/apps/wcm/core/resources/languages`

   Quindi modificare o estendere l&#39;elenco. La proprietà `defaultCountry` su un nodo linguistico (ad es. `ja`) deve contenere il codice completo, ad esempio `ja_jp`, che definirebbe `jp` come paese predefinito per la lingua `ja`.

1. Aggiorna **Gestione lingua di CQ WCM**.

   * **Elenco lingua**:

      Percorso dell’elenco delle lingue nell’archivio. Impostalo sulla posizione utilizzata per sovrapporre:

      ```
             /apps/wcm/core/resources/languages
      ```
   Puoi eseguire questa operazione utilizzando la console Web OSGi:

   ```shell
   https://<hostname>:<port-number>/system/console/configMgr/com.day.cq.wcm.core.impl.LanguageManagerImpl
   ```

## Pubblicazione dei dizionari {#publishing-dictionaries}

Incorpora i dizionari nel processo di gestione delle versioni delle applicazioni AEM. Ad esempio, includi il dizionario nel pacchetto di contenuto dell’applicazione per la distribuzione nell’istanza di pubblicazione. Questa strategia offre i seguenti vantaggi:

* I dizionari sono disponibili per i componenti nel loro ambiente di pubblicazione.
* Le modifiche alle stringhe dell’interfaccia utente del componente vengono distribuite insieme alle traduzioni aggiornate.

Allo stesso modo, il test delle stringhe del dizionario deve essere eseguito come parte del normale ciclo di vita dello sviluppo software.

>[!NOTE]
>
>La funzionalità di pubblicazione regolare, o replica, non deve essere utilizzata per i dizionari. I dizionari devono essere trattati allo stesso modo del codice e della configurazione. Ciò include l&#39;utilizzo del controllo del codice sorgente per tenere traccia delle modifiche e l&#39;utilizzo dei pacchetti di contenuti per applicare le modifiche all&#39;autore e alla pubblicazione.

>[!NOTE]
>
>Quando utilizzi Dispatcher, devi [annullare la validità delle pagine memorizzate nella cache](https://helpx.adobe.com/experience-manager/dispatcher/using/page-invalidate.html) per includere nuove stringhe di dizionario nelle stringhe di componenti renderizzate.
