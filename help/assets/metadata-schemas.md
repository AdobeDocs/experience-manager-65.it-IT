---
title: Schemi metadati
description: Lo schema metadati definisce il layout della pagina delle proprietà e le proprietà dei metadati visualizzate per le risorse. Scoprite come creare uno schema di metadati personalizzato, modificare lo schema di metadati e applicare lo schema di metadati alle risorse.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Schemi metadati {#metadata-schemas}

In Risorse Adobe Experience Manager (AEM), uno schema di metadati definisce il layout della pagina delle proprietà e le proprietà dei metadati visualizzate per le risorse che utilizzano lo schema specifico. Le proprietà dei metadati includono titolo, descrizione, tipi MIME, tag e così via.

È possibile utilizzare l&#39;editor Moduli schema metadati per modificare gli schemi esistenti o aggiungere schemi di metadati personalizzati.

1. Per visualizzare la pagina delle proprietà di una risorsa, toccate o fate clic sull’icona **[!UICONTROL Visualizza proprietà]** da Azioni rapide nella sezione della risorsa nella vista a schede.

   ![chlimage_1-34](assets/chlimage_1-170.png)

   In alternativa, seleziona la risorsa nell’interfaccia utente, quindi tocca o fai clic sull’icona **[!UICONTROL Proprietà]** nella barra degli strumenti.

   ![chlimage_1-35](assets/chlimage_1-171.png)

1. Modificate le varie proprietà di metadati nelle varie schede. Tuttavia, non potete modificare il tipo di risorsa nella pagina delle proprietà.

   ![chlimage_1-36](assets/chlimage_1-172.png)

   Per modificare il tipo MIME di una risorsa, utilizzate un modulo schema di metadati personalizzato o modificate un modulo esistente. Per ulteriori informazioni, consultate [Modificare i moduli](/help/assets/metadata-schemas.md#edit-metadata-schema-forms) dello schema metadati. Se modificate lo schema di metadati per un determinato tipo MIME, il layout della pagina delle proprietà per le risorse con il tipo MIME corrente e tutti i sottotipi di risorse vengono modificati. Ad esempio, modificando uno schema jpeg in `default/image` viene modificato solo il layout dei metadati (proprietà risorsa) per le risorse con tipo MIME `image/jpeg`. Tuttavia, se modificate lo schema predefinito, le modifiche apportate modificheranno il layout dei metadati per tutti i tipi di risorse.

1. Per visualizzare un elenco di moduli/modelli, fai clic sul logo AEM, quindi passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > Schemi di **[!UICONTROL metadati]**.

   ![chlimage_1-37](assets/chlimage_1-173.png)

   AEM offre i seguenti modelli:

   * **predefinito**: Modulo schema metadati di base per le risorse.
   I seguenti moduli secondari ereditano le proprietà del modulo predefinito:
i. **immagine**: Modulo schema per risorse con tipo MIME &quot;image&quot;, ad esempio `image/jpeg`, `image/png`e così via.
Il modulo &quot;immagine&quot; include i seguenti modelli di modulo figlio:a. **jpeg**: Modulo schema per risorse con sottotipo `jpeg`.
b. **tiff**: Modulo schema per le risorse con sottotipo `tiff`.

   ii) **applicazione**: Modulo schema per risorse con tipo MIME `application`, ad esempio `application/pdf`, `application/zip`e così via.
a. **pdf**: Modulo schema per risorse con sottotipo `pdf`.

   iii) **video**: Modulo schema per risorse con tipo MIME `video`, ad esempio `video/avi`, `video/mp4`e così via.

   * **insieme**: Modulo schema per le raccolte.
   * **** content fragment: Modulo schema per frammenti di contenuto.
   * **moduli**: Questo modulo schema si riferisce ad [Adobe Experience Manager Forms](/help/forms/home.md).


>[!NOTE]
>
>Per visualizzare i moduli secondari di un modulo schema, fare clic o toccare il nome del modulo schema.

## Aggiunta di uno schema di metadati {#add-a-metadata-schema-form}

1. Per aggiungere un modello personalizzato all’elenco, fate clic su **[!UICONTROL Crea]** dalla barra degli strumenti.

   >[!NOTE]
   >
   >I modelli non modificati presentano un&#39;icona a forma di lucchetto. Se personalizzate uno dei modelli, l&#39;icona Blocca prima che il modello scompaia.

1. Nella finestra di dialogo, immettere il titolo del modulo Schema, quindi fare clic su **[!UICONTROL Crea]** per completare il processo di creazione del modulo.

   ![chlimage_1-38](assets/chlimage_1-174.png)

## Modificare i moduli dello schema di metadati {#edit-metadata-schema-forms}

È possibile modificare un modulo di schema di metadati appena aggiunto o esistente. Il modulo schema metadati include quanto segue:

* Schede
* Elementi del modulo all&#39;interno delle schede.

È possibile mappare/configurare questi elementi del modulo su un campo all’interno di un nodo di metadati nell’archivio CRX.

È possibile aggiungere nuove schede o elementi modulo al modulo schema di metadati. Le schede e gli elementi del modulo derivati dall&#39;elemento padre sono nello stato bloccato. Non è possibile modificarle a livello di figlio.

1. Nella pagina Moduli schema, selezionare la casella di controllo prima di un modulo, quindi fare clic sull&#39;icona Modifica sulla barra degli strumenti.

   ![chlimage_1-39](assets/chlimage_1-175.png)

1. Nella pagina Editor **[!UICONTROL schema]** metadati, personalizza la pagina delle proprietà della risorsa trascinando uno o più componenti dall’elenco dei tipi di componenti nella scheda **[!UICONTROL Genera modulo]** alla scheda **[!UICONTROL Base]** .

   ![chlimage_1-40](assets/chlimage_1-176.png)

1. Per configurare un componente, selezionatelo e modificatene le proprietà nella scheda **Impostazioni** .

### Componenti nella scheda Genera modulo {#components-within-the-build-form-tab}

Nella scheda **[!UICONTROL Genera modulo]** sono elencati gli elementi del modulo utilizzati nel modulo schema. La scheda **[!UICONTROL Impostazioni]** fornisce gli attributi di ogni elemento selezionato nella scheda **[!UICONTROL Modulo]** di creazione. Nella tabella seguente sono elencati gli elementi del modulo disponibili nella scheda **[!UICONTROL Genera modulo]** :

| Nome componente | Descrizione |
|---|---|
| [!UICONTROL Intestazione sezione] | Aggiungere un&#39;intestazione di sezione per un elenco di componenti comuni. |
| [!UICONTROL Testo su riga singola] | Aggiungere una proprietà di testo a riga singola. È memorizzato come stringa. |
| [!UICONTROL Testo con più valori] | Aggiungete una proprietà di testo con più valori. È memorizzato come array di stringhe. |
| [!UICONTROL Numero] | Aggiungere un componente numero. |
| [!UICONTROL Data] | Aggiungere un componente data. |
| [!UICONTROL A discesa] | Aggiungere un elenco a discesa. |
| [!UICONTROL Tag standard] | Aggiungi un tag. |
| [!UICONTROL Tag avanzati] | Aggiungete nuove funzionalità di ricerca aggiungendo automaticamente tag di metadati. |
| [!UICONTROL Campo nascosto] | Aggiungere un campo nascosto. Viene inviato come parametro POST al momento del salvataggio della risorsa. |
| [!UICONTROL Risorsa con riferimento da] | Aggiungete questo componente per visualizzare l’elenco delle risorse a cui fa riferimento la risorsa. |
| [!UICONTROL Risorsa con riferimento a] | Aggiungi per visualizzare un elenco delle risorse che fanno riferimento alla risorsa. |
| [!UICONTROL Riferimenti sui prodotti] | Aggiungi per visualizzare l’elenco dei prodotti collegati alla risorsa. |
| [!UICONTROL Valutazione risorsa] | Aggiungi a opzioni di visualizzazione per la valutazione della risorsa. |
| [!UICONTROL Metadati contestuali] | Aggiungi per controllare la visualizzazione di altre schede di metadati nella pagina delle proprietà delle risorse. |

#### Modificare il componente metadati {#edit-the-metadata-component}

Per modificare le proprietà di un componente di metadati sul modulo, fate clic sul componente e modificate tutte o un sottoinsieme delle seguenti proprietà nella scheda **[!UICONTROL Impostazioni]** .

**Etichetta** campo: Nome della proprietà di metadati visualizzata nella pagina delle proprietà della risorsa.

**Mappa su proprietà**: Questa proprietà specifica il percorso/nome relativo al nodo della risorsa in cui viene salvato nell&#39;archivio CRX. Inizia con `./` perché indica che il percorso si trova sotto il nodo della risorsa.

Di seguito sono riportati i valori validi per questa proprietà:

Di seguito sono riportati i valori validi per questa proprietà:

* `./jcr:content/metadata/dc:title`: Memorizza il valore nel nodo di metadati della risorsa come proprietà `dc:title`.

* `./jcr:created`: Visualizza la proprietà JCR nel nodo della risorsa. Se configurate queste proprietà sulle proprietà di visualizzazione, è consigliabile contrassegnarle come Disattiva modifica, in quanto sono protette. In caso contrario, quando si salvano le proprietà della risorsa non è possibile modificare [!UICONTROL i risultati delle] risorse di errore.

Per garantire che il componente venga visualizzato correttamente nel modulo dello schema di metadati, il percorso della proprietà non deve includere spazi.

**Segnaposto**: Utilizzare questa proprietà per specificare il testo segnaposto relativo alla proprietà metadata.
**Obbligatorio**: Utilizzare questa proprietà per contrassegnare una proprietà di metadati come obbligatoria nella pagina delle proprietà.
**Disattiva modifica**: Utilizzare questa proprietà per rendere non modificabile una proprietà di metadati nella pagina delle proprietà.
**Mostra campo vuoto in sola**lettura: Contrassegnate questa proprietà per visualizzare una proprietà di metadati nella pagina delle proprietà anche se non ha alcun valore. Per impostazione predefinita, quando una proprietà di metadati non ha alcun valore, non viene elencata nella pagina delle proprietà.
**Mostra elenco ordinato**: Utilizzare questa proprietà per visualizzare un elenco ordinato di scelte ****: Utilizzare questa proprietà per specificare le scelte in un elenco **Descrizione** : Utilizzate questa proprietà per aggiungere una breve descrizione per il componente di metadati.
**Classe**: Classe oggetto a cui è associata la proprietà.
**Elimina**: Fare clic su questa icona per eliminare un componente dal modulo schema.

![chlimage_1-41](assets/chlimage_1-177.png)

>[!NOTE]
>
>Il componente Campo nascosto non include questi attributi. ma include proprietà quali Nome, Valore, Etichetta campo e Descrizione. I valori per il componente Campo nascosto vengono inviati come parametro POST ogni volta che la risorsa viene salvata. Non viene salvato come metadati per la risorsa.

Se selezionate l’opzione **[!UICONTROL Obbligatorio]** , potete cercare le risorse per le quali mancano i metadati obbligatori. Dal pannello **[!UICONTROL Filtri]** , espandete il predicato Convalida **** metadati e selezionate l’opzione **[!UICONTROL Non valido]** . Nei risultati della ricerca vengono visualizzate le risorse per le quali mancano i metadati obbligatori configurati tramite il modulo schema.

![chlimage_1-42](assets/chlimage_1-178.png)

Se aggiungete il componente Metadati contestuali a qualsiasi scheda di un modulo dello schema, il componente viene visualizzato come un elenco nella pagina delle proprietà delle risorse a cui è applicato lo schema specifico. L’elenco include tutte le altre schede eccetto la scheda a cui è stato applicato il componente Metadati contestuali. Attualmente, questa funzione fornisce funzionalità di base per controllare la visualizzazione dei metadati in base al contesto.

![chlimage_1-43](assets/chlimage_1-179.png)

Per includere una scheda qualsiasi nella pagina delle proprietà, oltre alla scheda in cui è applicato il componente Metadati contestuali, selezionare la scheda dall&#39;elenco. La scheda viene aggiunta alla pagina delle proprietà.

![chlimage_1-44](assets/chlimage_1-180.png)

### Specificare le proprietà nel file JSON {#specify-properties-in-json-file}

Invece di specificare le proprietà per le opzioni nella scheda **[!UICONTROL Impostazioni]** , potete definire le opzioni in un file JSON specificando le coppie chiave-valore corrispondenti. Specificate il percorso del file JSON nel campo Percorso **** JSON.

#### Aggiunta o eliminazione di una scheda nel modulo schema {#adding-deleting-a-tab-in-the-schema-form}

L&#39;editor dello schema consente di aggiungere o eliminare una scheda. Il modulo schema predefinito include per impostazione predefinita le schede **[!UICONTROL Base]**, **[!UICONTROL Avanzate]** , **[!UICONTROL IPTC]** e **[!UICONTROL IPTC Extension]** .

![chlimage_1-45](assets/chlimage_1-181.png)

Fare clic `+` per aggiungere una nuova scheda a un modulo schema. Per impostazione predefinita, la nuova scheda ha il nome `Unnamed-1`. Potete modificare il nome dalla scheda **[!UICONTROL Impostazioni]** .

Fare clic `X` per eliminare una scheda.

![chlimage_1-46](assets/chlimage_1-182.png)

## Eliminazione di moduli schema metadati {#delete-metadata-schema-forms}

AEM consente di eliminare solo i moduli schema personalizzati. Non consente di eliminare i moduli/modelli di schema predefiniti. Tuttavia, è possibile eliminare qualsiasi modifica personalizzata in questi moduli.

Per eliminare un modulo, selezionarlo e fare clic sull&#39;icona di eliminazione.

![chlimage_1-47](assets/chlimage_1-183.png)
<!--![chlimage_1-47](assets/chlimage_1-177.png) -->
>[!NOTE]
>
>Dopo aver eliminato le modifiche personalizzate a un modulo predefinito, l&#39;icona a forma di lucchetto viene visualizzata nuovamente prima di esso nell&#39;interfaccia Schema metadati per indicare che il modulo è tornato allo stato predefinito.

>[!NOTE]
>
>In Risorse AEM non è possibile eliminare i moduli di schema di metadati out-of-the-box.

## Moduli schema per tipi MIME {#schema-forms-for-mime-types}

Risorse AEM fornisce moduli predefiniti per vari tipi MIME. Tuttavia, è possibile aggiungere moduli personalizzati per risorse di vari tipi MIME.

### Aggiunta di nuovi moduli per i tipi MIME {#add-new-forms-for-mime-types}

Creare un nuovo modulo con il tipo appropriato. Ad esempio, per aggiungere un nuovo modello per il sottotipo **immagine/png** , creare il modulo sotto i moduli &quot;immagine&quot;. Il titolo del modulo schema è il nome del sottotipo. In questo caso, il titolo è &quot;png.**&quot;**

#### Utilizzare un modello di schema esistente per vari tipi MIME {#use-an-existing-schema-template-for-various-mime-types}

È possibile utilizzare un modello esistente per un tipo MIME diverso. Ad esempio, utilizzare il `image/jpeg` modulo per le risorse di tipo MIME `image/png`.

In questo caso, create un nuovo nodo `/etc/dam/metadataeditor/mimetypemappings` nell&#39;archivio CRX. Specificare un nome per il nodo e definire le seguenti proprietà:

| Nome | Descrizione | Tipo | Valore |
|---|---|---|---|
| `exposedmimetype` |  Nome del modulo esistente da mappare | `String` | `image/jpeg` |
| `mimetypes` | Elenco di tipi MIME che utilizzano il modulo definito nell&#39; `exposedmimetype` attributo | `String` | `image/png` |

Risorse AEM esegue la mappatura dei seguenti tipi MIME e moduli di schema:

| Modulo schema | Tipi MIME |
|---|---|
| image/jpeg | image/pjpeg |
| image/tiff | image/x-tiff |
| application/pdf | application/postscript |
| application/x-ImageSet | Multipart/Related; type=application/x-ImageSet |
| application/x-SpinSet | Multipart/Related; type=application/x-SpinSet |
| application/x-MixedMediaSet | Multipart/Related; type=application/x-MixedMediaSet |
| video/quicktime | video/x-quicktime |
| video/mpeg4 | video/mp4 |
| video/avi | video/avi, video/msvideo, video/x-msvideo |
| video/wmv | video/x-ms-wmv |
| video/flv | video/x-flv |

## Come concedere l’accesso agli schemi di metadati {#grant-access-to-metadata-schemas}

La funzione Schema metadati è disponibile solo per gli amministratori. Tuttavia, gli amministratori possono fornire l&#39;accesso ai non amministratori modificando alcune autorizzazioni. L’amministratore non è tenuto a creare, modificare ed eliminare le autorizzazioni nella `/conf` cartella.

## Applicare metadati specifici per le cartelle {#apply-folder-specific-metadata}

Risorse AEM consente di definire una variante di uno schema di metadati e applicarlo a una cartella specifica.

Ad esempio, potete definire una variante dello schema di metadati predefinito e applicarlo a una cartella. Quando applicate lo schema modificato, questo sostituisce lo schema di metadati predefinito originale applicato alle risorse all&#39;interno della cartella.

Solo le risorse caricate nella cartella a cui è applicato lo schema saranno conformi ai metadati modificati definiti nello schema di metadati della variante.

Le risorse in altre cartelle a cui è applicato lo schema originale continuano a essere conformi ai metadati definiti nello schema originale.

L’ereditarietà dei metadati per risorse si basa sullo schema applicato alla cartella di primo livello nella gerarchia. In altre parole, se una cartella non contiene sottocartelle, le risorse all’interno della cartella ereditano i metadati dallo schema applicato alla cartella.

Se la cartella dispone di una sottocartella, le risorse all’interno della sottocartella ereditano i metadati dallo schema applicato a livello di sottocartella se viene applicato uno schema diverso a livello di sottocartella. Tuttavia, se a livello di sottocartella non viene applicato alcuno schema o lo stesso schema, le risorse della sottocartella ereditano i metadati dallo schema applicato a livello di cartella principale.

1. Fate clic sul logo AEM, quindi selezionate **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > Schemi di **[!UICONTROL metadati]**. Viene visualizzata la pagina Moduli **[!UICONTROL schema]** metadati.
1. Selezionare la casella di controllo prima di un modulo, ad esempio il modulo di metadati predefinito, quindi fare clic o toccare l&#39;icona di copia e salvarlo come modulo personalizzato. Specificare un nome personalizzato per il modulo, ad esempio `my_default`. In alternativa, è possibile creare un modulo personalizzato.
   ![chlimage_1-184](assets/chlimage_1-184.png)

1. Nella pagina Moduli **[!UICONTROL schema]** metadati selezionare il `my_default` modulo, quindi fare clic sull&#39;icona **[!UICONTROL Modifica]** .

   ![chlimage_1-49](assets/chlimage_1-185.png)

1. Nella pagina Editor **[!UICONTROL schema]** metadati, aggiungere un campo di testo al modulo schema. Ad esempio, aggiungere un campo con l&#39;etichetta **[!UICONTROL Categoria]**.

   ![chlimage_1-50](assets/chlimage_1-186.png)

1. Fai clic su **[!UICONTROL Salva]**. Il modulo modificato è elencato nella pagina Moduli schema **[!UICONTROL metadati]** .
1. Toccate o fate clic su **[!UICONTROL Applica alle cartelle]** nella barra degli strumenti per applicare i metadati personalizzati a una cartella.

   ![chlimage_1-51](assets/chlimage_1-187.png)

1. Selezionare la cartella in cui applicare lo schema modificato, quindi fare clic o toccare **[!UICONTROL Applica]**.

   ![chlimage_1-52](assets/chlimage_1-188.png)

1. Se alla cartella è applicato un altro schema di metadati, viene visualizzato un messaggio di avviso che segnala la sovrascrittura dello schema di metadati esistente. Fate clic su **Sovrascrivi**.
1. Fate clic su **OK** per chiudere il messaggio di riuscita.
1. Andate alla cartella a cui avete applicato lo schema di metadati modificato.

## Definire i metadati obbligatori {#define-mandatory-metadata}

Potete definire i campi obbligatori a livello di cartella, che vengono applicati alle risorse caricate nella cartella. Se caricate risorse con metadati mancanti per i campi obbligatori definiti in precedenza, sulle risorse nella vista Scheda viene visualizzata un’indicazione visiva dei metadati mancanti.

>[!NOTE]
>
>Un campo di metadati può essere definito come obbligatorio in base al valore di un altro campo. Nella vista Schede, AEM non visualizza il messaggio di avviso relativo ai metadati mancanti per tali campi di metadati obbligatori.

1. Fate clic sul logo AEM, quindi selezionate **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > Schemi di **[!UICONTROL metadati]**. Viene visualizzata la pagina Moduli **[!UICONTROL schema]** metadati.
1. Salvare il modulo di metadati predefinito come modulo personalizzato. Ad esempio, salvatelo come `my_default`.

   ![chlimage_1-53](assets/chlimage_1-189.png)

1. Modificare il modulo personalizzato. Aggiungere un campo obbligatorio. Ad esempio, aggiungere un campo **[!UICONTROL Categoria]** e rendere il campo obbligatorio.

   ![chlimage_1-54](assets/chlimage_1-190.png)

1. Fai clic su **[!UICONTROL Salva]**. Il modulo modificato è elencato nella pagina Moduli schema **[!UICONTROL metadati]** . Selezionate il modulo, quindi toccate o fate clic su **[!UICONTROL Applica alle cartelle]** nella barra degli strumenti per applicare i metadati personalizzati a una cartella.

   ![chlimage_1-55](assets/chlimage_1-191.png)

1. Individuate la cartella e caricate alcune risorse con metadati mancanti per il campo obbligatorio aggiunto al modulo personalizzato. Nella vista Scheda della risorsa viene visualizzato un messaggio per i metadati mancanti per il campo obbligatorio.

   ![chlimage_1-56](assets/chlimage_1-192.png)

1. (Facoltativo) Accesso `https://[server]:[port]/system/console/components/`. Configura e abilita `com.day.cq.dam.core.impl.MissingMetadataNotificationJob` il componente disabilitato per impostazione predefinita. Impostate la frequenza con cui AEM verifica la validità dei metadati sulle risorse.

   Questa configurazione aggiunge una proprietà `hasValidMetadata` alle `jcr:content` risorse. Con questa proprietà, AEM può filtrare i risultati in una ricerca.

   >[!NOTE]
   >
   >Se una risorsa viene aggiunta dopo il controllo pianificato, non viene segnalata `hasValidMetadata` fino al controllo pianificato successivo. Le risorse non vengono visualizzate nei risultati di ricerca intermedi.

   >[!CAUTION]
   >
   >I controlli di convalida dei metadati richiedono molte risorse e possono influire sulle prestazioni del sistema. Pianificare i controlli di conseguenza. Se il server non è in grado di gestire il carico, provare a disattivare il processo.
