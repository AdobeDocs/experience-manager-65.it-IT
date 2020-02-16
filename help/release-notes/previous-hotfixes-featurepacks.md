---
title: Note sulla versione di AEM 6.5 Service Pack
description: Note sulla versione specifiche di Adobe Experience Manager 6.5 Service Pack 3.
uuid: c7bc3705-3d92-4e22-ad84-dc6002f6fa6c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: 25542769-84d1-459c-b33f-eabd8a535462
docset: aem65
translation-type: tm+mt
source-git-commit: 95d9ed8a0ccfa7651b83058d337511dd6b15665f

---


# Hotfix e Feature Pack inclusi nei Service Pack precedenti {#hotfixes-and-feature-packs-included-in-previous-service-packs}

## AEM 6.5.2.0

AEM 6.5.2.0 is an important release that includes performance, stability, security, and key customer fixes and enhancements released since the general availability of AEM 6.5 in **April 2019**. Può essere installato sopra AEM 6.5.

Di seguito sono elencati alcuni elementi di rilievo di questo Service Pack:

* Aggiornamento dell’archivio incorporato (Apache Jackrabbit Oak) alla versione 1.10.3.
* Aggiunta di una proprietà di configurazione per consentire l’esportazione di Frammenti esperienza direttamente in aree di lavoro definite dall’utente per Adobe Target.
* Aggiunta della funzionalità di ricerca di immagini visivamente simili per gli utenti di Assets. AEM visualizza le immagini con tag avanzati dell’archivio DAM simili a una selezionata dall’utente. Consulta la sezione sulla [ricerca visiva](../assets/search-assets.md#visualsearch).

* Miglioramento della funzionalità Risorse collegate per aggiungere il supporto per il recupero di documenti da implementazioni DAM remote. Gli autori di siti possono ora cercare e filtrare i tipi di documenti supportati in Content Finder. I documenti remoti possono essere aggiunti al componente Download nelle pagine Web. Consulta la sezione sull’[utilizzo di risorse collegate](../assets/use-assets-across-connected-assets-instances.md).

* Ottimizza i filtri di tipo Documento con più tipi MIME per supportare le opzioni multivalore.
* Introduzione di un flusso di lavoro Rielabora esterno per il supporto di più risorse.
* Ottimizzazione delle prestazioni di Dynamic Media mediante l’uso di filtri di risorse predefiniti per la replica.
* Ripristino delle opzioni di modifica di Assets relative a ritaglio/rotazione per DMS7.
* Implementazione di un’opzione per la disattivazione audio di un video durante il caricamento in VideoPlayer.
* Implementazione di una correzione per fare in modo che nella vista a colonne dell’interfaccia utente di Assets sia visualizzato solo il contenuto specifico del tenant.
* Implementazione di una correzione per consentire che le modifiche del pannello a soffietto dello stile rispecchino i risultati della ricerca.

### Assets {#assets}

**Miglioramenti apportati al prodotto**

* Miglioramento della funzionalità Risorse collegate per aggiungere il supporto per il recupero di documenti da implementazioni DAM remote. Gli autori di siti possono ora cercare e filtrare i tipi di documenti supportati in Content Finder. I documenti remoti possono essere aggiunti al componente Download nelle pagine Web. Hotfix per CQ-4270245. Consulta la sezione sull’[utilizzo di risorse collegate](/help/assets/use-assets-across-connected-assets-instances.md).

* Aggiunta della funzionalità di ricerca di immagini visivamente simili per gli utenti di Assets. AEM visualizza le immagini con tag avanzati dell’archivio DAM simili a una selezionata dall’utente. Consulta la sezione sulla [ricerca visiva](../assets/search-assets.md#visualsearch).

**Problemi risolti**

* I percorsi delle risorse negli URL e i metadati delle cartelle generati dall’API ACP non sono codificati in URL. GRANITE-26198: Hotfix per CQ-4271814
* Non è possibile utilizzare l’interfaccia di Assets per decomprimere e aprire un archivio contenente una cartella il cui nome include un segno di percentuale (%). NPR-29989: Hotfix per CQ-4270467
* Interfaccia touch: Durante la procedura guidata di gestione della pubblicazione, i riferimenti vengono aggiunti dopo la pagina nel corpo della richiesta di pubblicazione, causando la pubblicazione di tutte le risorse dopo la pagina, e quando viene eseguito il rendering della pagina, alcune risorse nell’istanza di pubblicazione vengono perdute. NPR-29985: Hotfix per CQ-4270724
* La funzione Scollega di Assets non funziona per le risorse correlate il cui nome contiene caratteri speciali (caratteri che diventano con codifica URI). NPR-30387: Hotfix per CQ-4274446
* Quando si modifica un frammento di contenuto, la versione viene creata con l’utente errato.
* Errore durante la creazione di raccolte nel sistema basato su tenant. NPR-30114: Hotfix per CQ-4272948
* La vista a colonne dell’interfaccia utente di Assets non rispetta il percorso principale DAM del tenant corrente, ma accede a tutti i percorsi DAM del tenant. NPR-30636: Hotfix per CQ-4275481
* Possibilità di attacchi che sfruttano la vulnerabilità cross-site scripting (XSS) tramite la finestra di avviso File con limitazioni, in quanto l’immagine inserita può risultare visibile. NPR-30617: Hotfix per CQ-4270133
* MultiTenant: I tenant che salvano le proprietà della cartella osservano sia il messaggio di riuscita che il messaggio di errore che descrive l&#39;azione non è riuscito, &quot;Impossibile modificare le proprietà. Autorizzazioni insufficienti.” e questo genera confusione. NPR-30545: Hotfix per CQ-4275333
* La finestra di dialogo di Selettore risorse non consente la selezione della risorsa, pertanto non è possibile aggiornare l’origine utilizzando la funzionalità di sostituzione dell’origine correlata. NPR-30502: Hotfix per CQ-4275029
* Flusso di lavoro Aggiorna risorsa DAM - Stato obsoleto durante il caricamento di file MP4 di grandi dimensioni. NPR-30480: Hotfix per CQ-4271352
* La funzionalità Crea attività di revisione non funziona a causa di un payload nullo che impedisce il completamento di tutte le azioni successive correlate all’attività di revisione. NPR-30468: Hotfix per CQ-4274263
* Problema di connettività di Tag avanzati di Adobe tramite DataPower. NPR-30026: Hotfix per CQ-4269457
* Nella vista a colonne dell’interfaccia utente di Assets viene generato un errore quando si prova ad aprire i filtri nella barra a sinistra. NPR-30501: Hotfix per CQ-4273862
* Quando si aggiungono gruppi sincronizzati da LDAP nelle proprietà di Gruppo utenti chiuso di una cartella risorse, il gruppo non viene salvato e recuperato. NPR-30615: Hotfix per CQ-4274689
* I campi di orientamento e stile per la ricerca con filtro non applicano il valore di completamento automatico alla query di ricerca. NPR-30620: Hotfix per CQ-4275724
* Con il collegamento di Condivisione risorse di una cartella il cui nome include spazi e il carattere “&amp;” vengono visualizzate schede grigie vuote per alcune risorse. NPR-30557: Hotfix per CQ-4270187
* Il modulo dello schema dei metadati della cartella non rileva automaticamente il tipo di dati e, di conseguenza, non crea l’elemento TypeHint correlato nell’invio del modulo. NPR-30599: Hotfix per CQ-4275227
* Le opzioni di modifica di Assets relative a ritaglio e rotazione vengono disabilitate dall’interfaccia utente di authoring di DMS7. NPR-30118: Hotfix per CQ-4273221
* La funzionalità Condividi collegamento non funziona sull’istanza di AEM con la configurazione DMS7. NPR-30080, NPR-30492: Hotfix per CQ-4273651
* Se si aggiunge alla pagina il componente Dynamic Media Scene7 e quindi si pubblica la pagina, la configurazione dmscene7 non viene attivata ogni volta. NPR-30641: Hotfix per CQ-4275962
* Aggiunta di un elemento IPSJobJournal in AEM per creare un solo processo IPS (Intrusion Prevention Systems) per profilo di elaborazione. NPR-30490: Hotfix per CQ-4273614
* Elemento multimediale dinamico: Sono stati aggiunti filtri predefiniti per escludere la replica delle risorse nel nodo di pubblicazione AEM. NPR-30538: Hotfix per CQ-4274678
* Introduzione di un flusso di lavoro Rielabora esterno per supportare più risorse e consentire la creazione della cartella come payload. Il flusso di lavoro prevede due passaggi: rielaborazione delle risorse senza alcun handle tramite la mappatura dei metadati al passaggio successivo e ricaricamento di tutte le risorse senza handle di risorsa a S7 in un singolo processo IPS. Per ulteriori informazioni, consulta Configurazione di Cloud Services di Dynamic Media. NPR-30489: Hotfix per CQ-4272903
* Caricamento di un CSV non corretto dopo la cancellazione del CSV corretto. Hotfix per CQ-4277694, CQ-4277814
* Icona errata specifica delle cartelle contributi da rimuovere. Hotfix per CQ-4277580
* Selezionando un utente nel selettore utenti della scheda Contributo risorse, il nome dell’utente non viene visualizzato nella tabella e nella pagina delle proprietà della finestra di dialogo Elimina utente viene visualizzato testo errato. Hotfix per CQ-4277875
* Non è possibile aggiungere collaboratori alla cartella Contributo risorse dal selettore utente selezionando l’utente e facendo clic su Aggiungi. Hotfix per CQ-4277824, CQ-4278087
* La ricerca per nome utente in minuscolo non funziona nel selettore utente. Hotfix per CQ-4277958, CQ-4277930
* Gli utenti non amministratori possono pubblicare risorse in una nuova cartella di una cartella Contributo risorse. Hotfix per CQ-4278200
* L’utente DAM (non amministratore) non può scegliere di aggiungere collaboratori alla cartella Contributo risorse. Hotfix per CQ-4278192
* Il pulsante “Crea” è visibile nella cartella Contributo risorse. Hotfix per CQ-4277560
* Se si ordinano le query di ricerca in base alla rilevanza, oltre ai modelli InDesign vengono restituiti documenti InDesign. Hotfix per CQ-4273864
* Se l’utente dispone di un ID e-mail in maiuscolo, non potrà eseguire la consegna per le risorse ritirate in precedenza. Hotfix per CQ-4276575
* L’operazione Elimina si applica solo ai predefiniti selezionati; se la schermata aggiorna automaticamente l’elenco dopo l’operazione, vengono visualizzati altri predefiniti già aggiornati. Hotfix per CQ-4261461
* Se si configura Cloud Services di Dynamic Media in modalità DMHybrid, verranno create più suite di rapporti vuote in Analytics e in AEM non verrà memorizzato alcun ID suite di rapporti, con conseguente duplicazione delle suite di rapporti. Hotfix per CQ-4249780
* L’operazione di ridenominazione di una risorsa AEM in un nome duplicato non può essere sincronizzata con Scene7. Hotfix per CQ-4276763
* I contenuti generati dall’utente non vengono visualizzati correttamente nel pannello del filtro di ricerca. Hotfix per CQ-4273875
* L’opzione Trova simile non è disponibile per le immagini TIFF. Hotfix per CQ-4278238
* Implementazione di un’opzione per disattivare l’audio dei video durante il caricamento in VideoPlayer. Hotfix per CQ-4266465
* Visualizzatori - VideoViewer: poster=none funziona in modo errato nel caso di un video esterno utilizzato. Hotfix per CQ-4265536
* L’icona di attesa è visibile durante la riproduzione video nei browser IE11 e MS Edge. Hotfix per CQ-4251539
* I file README dell’SDK 3.8 e dei visualizzatori 5.13 non vengono aggiornati e contengono informazioni provenienti da versioni precedenti. Hotfix per CQ-4273737
* Viene creata una versione del frammento di contenuto ancor prima del salvataggio delle modifiche. NPR-30616: Hotfix per CQ-4273088
* Sostituzione di Asset#getMetadata(String) con Asset#getMetadataValueFromJcr(String) nel processo miniature. NPR-30491: Hotfix per CQ-4273067
* Il caricamento di un file jpg causa l’attivazione di più istanze del messaggio: “Replica di ReplicateOnModifyWorker AGGIORNATA” per ciascuna risorsa, causando un peggioramento delle prestazioni.
* La decompressione dell’archivio ZIP mediante la funzione Estrai archivio causa problemi con le cartelle il cui nome contiene il segno di percentuale (%) nel titolo. NPR-29990: Hotfix per CQ-4270467

### Sites {#sites-6520}

* Se l&#39;ereditarietà LiveCopy è danneggiata, nelle pagine di LiveCopy vengono visualizzati i collegamenti per la copia della lingua invece dei collegamenti LiveCopy. (NPR-30980)
* Per una nuova Blueprint, Se il numero di record è superiore a 40, vengono visualizzati solo i primi 40 record. Blueprint visualizza righe vuote per il resto dei record. (NPR-31182)
* Il plug-in Editor Rich Text (RTE) del componente Testo visualizza i caratteri distorti per il testo in giapponese e coreano. (NPR-31331)
* Editor Rich Text (RTE) non consente di inserire una tabella incorporata come voce di elenco. (NPR-30879)
* L’Editor Rich Text per la creazione di ponteggi avanzati (RTE) viene applicato in linea agli elementi in modo imprevisto. (NPR-31284)
* Quando un utente si concentra sui campi della barra a sinistra e utilizza una scelta rapida da tastiera per incollare il contenuto, incolla il contenuto degli Appunti dell&#39;Editor pagina invece del contenuto copiato dai campi della barra a sinistra. (NPR-31172)
* Quando un utente aggiunge un campo Caricamento file a un campo multiplo, il percorso dell’immagine viene memorizzato nel nodo del componente invece del nodo del campo multiplo. (NPR-30882)
* L&#39;API ResponsiveGridExporter non restituisce l&#39;interfaccia com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter. Il pacchetto com.day.cq.wcm.foundation.model.impl è dichiarato come pacchetto privato. (NPR-31398)
* Quando una pagina contenente alcuni frammenti esperienza viene aperta in modalità non editor (in Author senza il `editor.html` prefisso e, `wcmmode=disabled`o in Publisher), la richiesta termina con il codice di errore dello stato HTTP 500. (NPR-30743)

### WCM - Editor pagina {#wcm-page-editor-6520}

**Miglioramenti apportati al prodotto**

* Ottimizza i filtri di tipo Documento con più tipi MIME per supportare opzioni con più valori. Hotfix per CQ-4270694

### Gestione dei frammenti di contenuto {#content-fragment-management-6520}

* La query utilizzata dall’interfaccia utente dei modelli di frammenti di contenuto è molto lenta e alla fine genera un errore. Hotfix per CQ-4270807

### Interfaccia utente - Foundation {#ui-foundation}

* Con l’attivazione dei tasti di scelta rapida l’utente non può usare i tasti m, p ed e all’interno di specifiche interfacce utente. NPR-30355: Hotfix per GRANITE-26346
* La chiusura dell’interfaccia utente di ricerca di Risorse non reimposta la barra a sinistra sulla selezione del contenuto, impedendo all’utente di aprire la barra laterale del filtro una seconda volta. NPR-30509: Hotfix per CQ-4274716
* Ambiente multi-tenant: gli elementi di navigazione nella parte superiore dell’interfaccia utente di Assets non sono disponibili e viene generato un errore JavaScript. NPR-30104: Hotfix per GRANITE-26344

### Traduzione {#translation-6520}

* Problema di traduzione - Solo alcuni componenti vengono tradotti utilizzando la traduzione automatica. NPR-30079: Hotfix per CQ-4273764

### Piattaforma {#platform-6520}

* Il mittente predefinito di AEM non è in grado di inviare messaggi a un server SMTP remoto tramite TLS v1.2. NPR-30476: Hotfix per GRANITE-26605

### Progetti {#projects-6520}

* I valori dam:folderThumbnailPaths non vengono aggiornati e vengono visualizzate miniature vecchie anche dopo l’eliminazione delle risorse nella cartella. NPR-30424: Hotfix per CQ-4273667
* Quando si completa l’opzione “Sposta”, titolo e nome della risorsa restano invariati. NPR-30647: Hotfix per CQ-4276265

### Communities {#communities-6520}

* Diagnostica sincronizzazione utenti è danneggiato e non funziona. NPR-30004, NPR-29943: Hotfix per CQ-4270287, CQ-4271348

### Sling {#sling}

* In seguito all’aggiornamento dell’istanza dalla versione 6.3.3.2 alla versione 6.5 vengono create configurazioni OSGi duplicate. NPR-30130: Hotfix per CQ-4274016

### Integrazione {#integration}

* Il contenuto personalizzato non viene visualizzato correttamente nell’istanza di pubblicazione fino al riavvio dell’istanza. NPR-30377: Hotfix per CQ-4273706
* Durante la configurazione di Launch in un sito Web, l’indirizzo della libreria è preceduto da una barra (/) e questo causa ogni volta la necessità di un intervento manuale. NPR-30694: Hotfix per CQ-4275501

### Forms {#forms-6520}

>[!NOTE]
>
>Il Service Pack di AEM non include le correzioni per AEM Forms. Tali correzioni vengono distribuite utilizzando un pacchetto separato di componenti aggiuntivi per Forms. Inoltre, viene rilasciato un programma di installazione cumulativo che include correzioni per AEM Forms su JEE. Per ulteriori informazioni, consulta [Installare il componente aggiuntivo per AEM Forms](#install-aem-forms-add-on-package) e [Installare il programma di installazione di JEE per AEM Forms](#forms-jee-installer).

Elementi di rilievo di AEM 6.5.2.0 Forms:

* Aggiunta dell’impostazione Auto a `RenderAtClient` nell’API `PDFFormRenderOptions` per la specifica OSGi di AEM Forms.

#### Pacchetto di componenti aggiuntivi per Forms {#forms-add-on-package}

**Integrazione back-end**

* Impossibile configurare il modello dati del modulo utilizzando un URL con bilanciamento del carico ospitato da AWS. NPR-30123: Hotfix per CQ-4273359
* Durante la creazione del modello dati del modulo (FDM) con il linguaggio WSDL (Web Service Definition Language), `Caused by: com.adobe.aem.dermis.exception.DermisException: java.lang.Exception: Unable to handle content type` viene restituito il messaggio di errore: NPR-30477: Hotfix per CQ-4272921

**Gestione della corrispondenza**

* &quot;Crea rappresentazione dell’interfaccia utente di corrispondenza (interfaccia utente CCR) non riesce in modo intermittente con l’errore riportato di seguito nella console:
   `- Uncaught Error: variable [object Object]is already known the letter`- NPR-30127

**Comunicazione interattiva**

* Un campo contrassegnato come obbligatorio nel modello dati del modulo viene visualizzato come obbligatorio nell’interfaccia utente di Crea corrispondenza (interfaccia utente CCR). NPR-30623: Hotfix per CQ-4274902

**Forms - Flusso di lavoro**

* Le variabili di output non mappate in cartelle esaminate causano errori di chiamata. Hotfix per CQ-4264451

**Moduli HTML5**

* Quando il codice o il progetto personalizzato viene distribuito per la seconda volta, la pagina non viene sottoposta a rendering e si verifica il seguente errore:

   `org.apache.sling.scripting.sightly.SightlyException.`

   NPR-30539: Hotfix per CQ-4272509

* Quando si utilizza l’accesso desktop non visivo in modalità Sfoglia per leggere un modulo HTML5, il browser Chrome legge l’elemento “grafico” prima di qualsiasi file SVG nella struttura del modulo. NPR-30449: Hotfix per CQ-4274732

#### Programma di installazione di JEE per Forms {#forms-jee-installer}

**Forms - Sicurezza dei documenti**

* L’applicazione di una firma con marca temporale non riesce e viene restituito l’errore: ALC-DSC-003-000: com.adobe.idp.dsc.DSCInvocationException: Errore di chiamata. NPR-30820: Hotfix per CQ-4275852

**Forms - Servizi basati su documenti**

* Se “SubmitURL” contiene una e commerciale (&amp;), nel registro sono presenti errori di analisi quando si effettua la richiesta POST al servlet renderpdf. NPR-30865: Hotfix per CQ-4278232

**Forms - JEE di base**

* Il servizio HTMLtoPDF non visualizza maxReuseCount nella console JMX. NPR-30134, NPR-30304: Hotfix per CQ-4273763
* L&#39;aggiunta o la modifica di una connessione a un servizio Web richiamando i servizi Web da AEM Forms Workbench genera un errore: ClassNotFoundException org.apache.axis.message.SOAPBodyElement. NPR-30105: Hotfix per CQ-4273217

### Feature Pack inclusi {#feature-packs-included}

>[!NOTE]
>
>Per i clienti di AEM Forms, è essenziale installare il pacchetto dei componenti aggiuntivi per AEM Forms dopo l’installazione del Service Pack, del Cumulative Fix Pack o del Feature Pack di AEM.

#### Sites {#sites-feature-packs-included}

* Aggiunta di una proprietà di configurazione per consentire l’esportazione di Frammenti esperienza direttamente in aree di lavoro definite dall’utente per Adobe Target. NPR-29189: Hotfix per CQ-4249782

#### Forms - Servizi basati su documenti {#forms-document-services-1}

* Aggiunta dell’impostazione Auto a `RenderAtClient` nell’API `PDFFormRenderOptions` per la specifica OSGi di AEM Forms. NPR-30759: Hotfix per CQ-4278193

## AEM 6.5.1.0 {#release-6510}

AEM 6.5.1.0 is an important release that includes performance, stability, security, and key customer fixes and enhancements released since the general availability of AEM 6.5 in *April 2019.* Può essere installato sopra AEM 6.5.

Di seguito sono elencati alcuni elementi di rilievo di questo Service Pack:

* Abilitazione dell’inclusione dello stato dell’interfaccia utente dinamica negli eventi di tracciamento come attributi personalizzati.
* Inclusione del supporto per la distribuzione di risorse video 360° in Scene7 di Dynamic Media.
* Enabled *Japanese Word Wrap* feature via the styles plugin of Rich Text Editor. For more information, see [Configure Japanese word wrap](/help/sites-administering/configure-rich-text-editor-plug-ins.md#jpwordwrap)

### Assets

* Aggiornamento dell’interfaccia DMGGateway di DAM per il supporto multipart di S3. NPR-29740: Hotfix per CQ-4226303
* L&#39;anteprima delle rappresentazioni genera `Only empty tenantId is currently supported` un errore dopo l&#39;aggiornamento ad AEM 6.5\. NPR-29986: Hotfix per CQ-4272353
* La finestra di dialogo Elimina non è visibile per consentire l’eliminazione di lavori. NPR-29720: Hotfix per CQ-4271074
* Dopo aver aggiunto il titolo della risorsa nella pagina delle proprietà, quando un utente prova a chiudere la pagina, AEM riapre la pagina delle proprietà. NPR-29627: Hotfix per CQ-4264929
* VersioningTimelineEventProvider deve fornire la versione principale unitamente al nodo della versione nt: del tipo. Hotfix per GRANITE-26063
* Implementazione della funzionalità per caricare e riprodurre video sferici a 360° in modalità Scene7 DM di AEM. Hotfix per CQ-4265131
* Live Copy recupera lo stato non corretto in caso di modifica dell’origine. Hotfix per CQ-4265451
* Abilitazione del supporto per l’utilità di gestione di più siti per Assets. Hotfix per CQ-4271453, CQ-4268621, CQ-4257491
* L’interfaccia di AEM deve contenere una voce aggiuntiva per la versione corrente della risorsa nella cronologia della timeline, per visualizzare l’ultimo commento di consegna fornito da Adobe Asset Link. Hotfix per CQ-4262864
* Nella timeline dei frammenti di contenuto viene visualizzato un messaggio di errore in caso di assenza di proprietà. Hotfix per CQ-4272560
* Problema relativo al lettore video di Scene7 quando viene espanso a schermo intero. Hotfix per CQ-4266700
* ZoomVerticalViewer: i pulsanti di spostamento non devono essere visualizzati se viene utilizzata una singola risorsa immagine. Hotfix per CQ-4264795
* Se si elimina un nodo figlio nella Live Copy, è necessario scollegare liveRelationship. Hotfix per CQ-4270395
* Lo schema di metadati contiene solo elementi della configurazione globale; quelli del tenant attivo non sono presenti. Il valore dell’URL di formPath viene ripristinato a quello predefinito anche se modificato. NPR-29945: Hotfix per CQ-4262898
* La pubblicazione di predefiniti per immagini su Brand Portal non riesce e viene restituito il codice di errore 500. NPR-29510: Hotfix per CQ-4268659

### Sites

* Le proprietà vuote e multiple non vengono propagate dalla blueprint durante il rollout. Il ripristino di Live Copy con la blueprint non funziona per i componenti. NPR-29253: Hotfix per CQ-4264928, CQ-4264926, CQ-4267722
* CoralUI, when used with `Multifield`, stores the `fileReferenceParameter` at the component level instead of multifield level. NPR-29537: Hotfix per CQ-4266129
* Miglioramento del componente di testo AEM e dell’editor di testo per il giapponese. NPR-29785: Hotfix per CQ-4265090
* La pagina ripristinata con Timewarp deve fare riferimento all’immagine corretta al momento del controllo delle versioni. NPR-29431: Hotfix per CQ-4262638
* Un problema relativo all&#39;ereditarietà dei nodi Style System da padre a figlio. NPR-29516: Hotfix per CQ-4270330
* Messaggio di errore durante la configurazione dell’autenticazione per il social posting su Facebook. NPR-29211: Hotfix per CQ-4266630
* La miniatura di cui è stato eseguito il rendering nel frammento di contenuto mostra la rappresentazione interna del calendario per il campo Data e ora. NPR-29531: Hotfix per CQ-4269362
* All’apertura della scheda Autorizzazioni nell’implementazione di Coral2 non viene visualizzato alcun pulsante. Hotfix per CQ-4269419

### Commerce

* ConstraintViolationException durante l’esecuzione della migrazione lenta dei contenuti per l’e-commerce. NPR-29247: Hotfix per CQ-4264383

### Gestione dei frammenti di contenuto

* Parsing error when opening a Content Fragment which has characters dollar `($)` and open brace `({)`. Hotfix per CQ-4270266

### Frammenti esperienza

* Esporta Frammenti esperienza AEM in Adobe Target. Hotfix per CQ-4265469
* L’esportazione di frammenti esperienza come destinazione non riesce con l’immagine intelligente. Hotfix per CQ-4269606

* L’utente rimane bloccato quando prova a spostare i frammenti esperienza tramite Omnisearch nella vista a schede. Hotfix per CQ-4263848

### WCM - Editor pagina

* Vulnerabilità cross-site scripting (XSS) rilevabile quando si utilizza un selettore non valido. Hotfix per CQ-4270397

### Replica

* User-provided data is not escaped on output in the `cq/replication/components/agent` component, resulting in a stored Cross-site scripting (XSS) vulnerability. Hotfix per CQ-4266263

### Flusso di lavoro

* Il campo del selettore del calendario di Partecipante finestra di dialogo è danneggiato. NPR-29727: Hotfix per CQ-4270423

### WCM - Editor SPA

* Abilitazione del recupero da un endpoint remoto di contenuti di cui è già stato eseguito il rendering. Hotfix per CQ-4270238
* Aggiunta di avvisi nei registri quando viene aperta una pagina di modello per applicazione a pagina singola di cui viene eseguito il rendering sul lato server. Hotfix per CQ-4270238

### WCM - MSM

* Con l’aggiornamento ad AEM 6.4.3 il rollout dell’utilità di gestione di più siti richiede molto tempo. Hotfix per CQ-4271410

### Integrazione

* Credenziali BrightEdge non valide ed errore di connessione. NPR-29168: Hotfix per CQ-4265872

* Viene visualizzato un messaggio di eccezione quando si prova a modificare e salvare la configurazione di avvio di AEM. NPR-29176: Hotfix per CQ-4265782/CQ-4266153

### Interfaccia utente

* Aggiunta del supporto per il tracciamento degli stati dell’interfaccia utente dinamica come attributi personalizzati durante il tracciamento di determinati eventi nell’API di tracciamento di base. Hotfix per GRANITE-26283
* Impossibile impostare la funzione di tracciamento sul pulsante di invio. Hotfix per GRANITE-26326
* La procedura guidata non riesce a impostare la funzione di tracciamento sul pulsante di invio. NPR-29995, NPR-30025: Hotfix per CQ-4264289

### Communities

* Impossibile allineare i nuovi badge nel menu a discesa sulla pagina del profilo del membro. NPR-29381: Hotfix per CQ-4267987
* Visitatori e membri, senza privilegi di moderatore, possono visualizzare i post non approvati/in sospeso incollando l’URL. NPR-29724: Hotfix per CQ-4271124, CQ-4271441
* Durante l’accesso dell’utente alla community è possibile notare un tempo di risposta elevato, fino a 40-50 secondi. NPR-29677: Hotfix per CQ-4269444

### Replica

* Il componente Agente di replica è soggetto a una vulnerabilità per cui informazioni sensibili vengono rivelate a utenti non autorizzati. NPR-29611: Hotfix per GRANITE-25070

* Falla nella sessione durante OAuth per ogni replica su Brand Portal. NPR-30001: Hotfix per GRANITE-26196

### Progetti

* La pubblicazione di risorse dalla cartella /content/dam/mac di AEM Author a Brand Portal non funziona. NPR-29819: Hotfix per CQ-4271118

### Piattaforma

* HtmlLibraryManager elimina tutti i contenuti di crx-quickstart in seguito all’annullamento della validità della cache. NPR-29863: Hotfix per GRANITE-26197

### Felix

* I dettagli sull’utilizzo della memoria non vengono visualizzati nella console del sistema quando si utilizza Java 11\. NPR-29669

### Forms

Elementi di rilievo di AEM 6.5.1.0 Forms:

* OSGi only: Added a new attribute `PAGECOUNT` in Output and Forms Service.

* Solo OSGI: È stato abilitato il supporto per la creazione di file PDF statici tramite Forms Service.
* Abilitazione delle autorizzazioni su XMLForm.exe per gli utenti amministratore e root.
* Abilitazione del supporto per ADFS v3.0 per l’integrazione On-Premise di Dynamics.

#### Pacchetto di componenti aggiuntivi per Forms

**Integrazione con il back-end**

* Errore durante il recupero del linguaggio WSDL (Web Service Definition Language) protetto. NPR-29944: Hotfix per CQ-4270777
* Quando AEM Forms è installato in IBM WebSphere, si verifica un errore nella creazione di un modello dati del modulo basato su SOAP. Hotfix per CQ-4251134
* Abilitazione del supporto per ADFS (Active Directory Federation Services) v3.0 per l’integrazione On-Premise di Microsoft Dynamics. Hotfix per CQ-4270586
* Quando si modifica il titolo di un’origine dati, il modello dati del modulo non visualizza il titolo aggiornato. Hotfix per CQ-4265599
* Se il nome di un&#39;entità o un attributo contiene trattino o spazio, le espressioni non riescono a valutare tali entità e attributi. Hotfix per CQ-4225129

* L&#39;output non è corretto quando nell&#39;output della stringa primitiva sono presenti due punti. Hotfix per CQ-4260825

* Anche quando non è previsto alcun contenuto dall’output dell’API REST, l’operazione di richiamo del modello dati del modulo genera un errore. Hotfix per CQ-4268828

**Moduli adattivi**

* Impossibile aggiungere una nuova istanza nel frammento di modulo adattivo durante il caricamento lento. NPR-29818: Hotfix per CQ-4269875
* Il componente Verifica non registra o visualizza errori per i modelli della documentazione. Hotfix per CQ-4272999
* Aggiunta del supporto per disabilitare l’editor di layout per Moduli adattivi. Hotfix per CQ-4270810
* È stato ripristinato il passaggio di verifica per i moduli adattivi in AEM 6.5\. Hotfix per CQ-4269583

* Un errore di convalida del campo Modulo adattivo interrompe l’esecuzione di Adobe Sign. Hotfix per CQ-4269463
* Se in un’istanza di AEM Forms sono presenti più di 20 frammenti di modulo adattivo e il nome di tutti i frammenti di modulo inizia con la stessa stringa, la ricerca non restituisce alcun frammento oppure restituisce solo 20 frammenti creati di recente. Hotfix per CQ-4264414, CQ-4264914

* Problemi di prestazioni quando l’app Moduli adattivi viene utilizzata con set di dati di grandi dimensioni. . Hotfix per CQ-4235310

* Se l’accesso viene effettuato tramite un account anonimo in un’istanza pubblicata, lo script GuideRuntime non viene caricato. Hotfix per CQ-4268679

**Forms - Comunicazione interattiva**

* Il modello di comunicazione interattiva non elenca i componenti intestazione e piè di pagina nell’elenco dei componenti consentiti. Hotfix per CQ-4237895
* Quando crei un modello di stampa per comunicazioni interattive contenente un campo immagine, il titolo del grafico è impostato su una stringa vuota. Hotfix per CQ-4264772
* Il colore della linea di un grafico, se eliminato, è impostato su non definito. Hotfix per CQ-4264762
* Le modifiche al livello di layout apportate al frammento del documento non vengono visualizzate quando si eseguono modifiche alla sincronizzazione. Hotfix per CQ-4266054
* L’elemento del modello dati modulo all’interno di un frammento di documento associato a un campo di testo non visualizza l’icona di ereditarietà e consente l’associazione. Hotfix per CQ-4261089
* L’API di rendering del canale di stampa non include l’opzione per passare dati come parametro nell’API. Hotfix per CQ-4263540
* Le impostazioni dell&#39;agente non sono visibili perché la casella di controllo Modificabile dall&#39;agente viene deselezionata quando il tipo di binding viene modificato da Frammento di testo a Nessuno/Oggetto modello dati per il campo/variabile Stringa. Hotfix per CQ-4261953
* Durante l&#39;invio dell&#39;interfaccia utente dell&#39;agente, il file json di dati Web risultante memorizza le informazioni per i campi non associati annullati dall&#39;ereditarietà. Hotfix per CQ-4265621

**Forms - Flusso di lavoro**

* Quando un modulo viene nuovamente inviato dalla casella in uscita dell’app Moduli adattivi, si verifica una perdita di dati. NPR-28345: Hotfix per CQ-4260929
* I documenti non vengono chiusi durante il salvataggio per i casi non variabili. Hotfix per CQ-4269784
* L&#39;app per moduli adattivi non supporta più Microsoft Windows 8.1\. Hotfix per CQ-4265274
* Quando un’immagine di dimensioni superiori a 2 MB viene associata a un modulo come allegato a livello di campo nella versione Android dell’app AEM Forms, si verifica un arresto anomalo dell’app. Hotfix per CQ-4265578

* Abilitazione delle opzioni di precompilazione per il canale di stampa delle comunicazioni interattive nell’attività Assegna. Hotfix per CQ-4265577
* Gli utenti non possono visualizzare un’attività condivisa finché non diventano membri del gruppo a cui è assegnata l’attività. Hotfix per CQ-4248733
* Il salvataggio o l’invio di applicazioni JEE nell’app Moduli adattivi è bloccato in Windows. Hotfix per CQ-4268704
* Il modello dati del modulo associato alla variabile del modello dati del modulo non è visibile. Hotfix per CQ-4266554
* Assenza del supporto per la variabile di stato della firma del documento quando viene utilizzato il supporto per le variabili. Hotfix per CQ-4266312
* Gli invii dall’area di lavoro non riescono se è presente il carattere umlaut. Hotfix per CQ-4263172
* In una configurazione aggiornata, se il flusso di lavoro viene aperto per la modifica, nell’interfaccia utente della cartella di controllo (interfaccia utente) viene visualizzato un errore invece del nome del flusso di lavoro. Hotfix per CQ-4238579

**Forms - Gestione**

* Quando viene caricata un’estensione diversa da xsd o schema.json, il caricamento non viene eseguito e non viene generato alcun messaggio di errore. Hotfix per CQ-4266716

**Forms - Gestione della corrispondenza**

* L’interfaccia utente di Crea corrispondenza (interfaccia utente CCR) per AEM 6.5 Forms non riesce ad aprire la corrispondenza creata con AEM 6.3 Forms. Hotfix per CQ-4266392
* La funzione di somma in XDP non funziona se i dati DDE sono di tipo numero. Hotfix per CQ-4227403
* La logica di annullamento validità della cache in memoria delle lettere deve essere aggiornata, perché quando viene pubblicata una risorsa, l’ora dell’ultima modifica non viene aggiornata. Hotfix per CQ-4250465
* Impossibile pubblicare il frammento di documento, DD e lettere. Hotfix per CQ-4272893

#### Programma di installazione di JEE per Forms

**PDF Generator**

* La conversione di file CAD in PDF non riesce con JDK a 64 bit. NPR-29924, NPR-29925: Hotfix per CQ-4272113
* Sostituzione del nome di PhantomJS in WebToPDF per la conversione HTMLtoPDF. NPR-29933: Hotfix per CQ-4234545
* Viene generato un errore durante la conversione del file ZIP in PDF. Hotfix per CQ-4268628

**Forms - Designer**

* Quando viene eseguito un controllo di accessibilità completo sul PDF statico creato con AEM Forms Designer, il controllo Lingua principale non riesce perché manca l’attributo della lingua. Hotfix per CQ-4272923, CQ-4271002

**Forms - Sicurezza dei documenti**

* La firma digitale con il modulo di sicurezza hardware non funziona in OSGi Linux su Java 11 e Java 8\. NPR-29838: Hotfix per CQ-4270441
* La firma digitale con il modulo di sicurezza hardware non funziona in JEE Linux e in tutti i server app supportati, ad esempio JBoss e Websphere. NPR-29839: Hotfix per CQ-4266721
* Durante la verifica delle firme in un PDF tramite l’uso di firme elettroniche avanzate PDF (PAdES) viene generata l’eccezione InvalidOperationException. NPR-29842: Hotfix per CQ-4244837
* Aggiunta del supporto per Document Security Extension per Office 2019\. Hotfix per CQ-4254369, CQ-4259764

**Forms - Servizi basati su documenti**

* La conversione del PDF in PDF/A-1b con il campo Modulo non ha il codice di aspetto. NPR-29940: Hotfix per CQ-4269618

* OSGi: Impossibile determinare il numero di pagine generate durante il rendering. NPR-28922: Hotfix per CQ-4270870
* Abilitato il supporto per i file PDF statici tramite Forms Service in AEM Forms OSGi. NPR-28572: Hotfix per CQ-4270869
* Impossibile modificare le autorizzazioni per XMLForm.exe. NPR-29828, NPR-29237: Hotfix per Q-4267080
* Il PDF statico creato dal modulo di output del server di AEM Forms non compila l’attributo/tag della lingua con la lingua del documento creato. NPR-27332: Hotfix per CQ-4271002

**Forms - JEE di base**

* Il file pdfg_srt non è disponibile negli artefatti finali e questo impedisce l’esecuzione del programma di installazione. NPR-29854: Hotfix per CQ-4270137
* LCBackupMode.sh non funziona. NPR-29840: Hotfix per CQ-4269424
* È necessario rimuovere il riferimento alla porta UDP dall’interfaccia utente per WebSphere. Hotfix per CQ-4264782

### Feature Pack inclusi

#### Assets - Incluso

* Abilitazione del supporto per l’utilità di gestione di più siti per Assets. For more information, see [Reuse assets using MSM for Assets](https://helpx.adobe.com/experience-manager/6-5/help/assets/reuse-assets-using-msm.html). NPR-29199: Hotfix per CQ-4259922

#### Siti - Inclusi

* Esporta Frammenti esperienza AEM in Adobe Target. For more details, see [The Experience Fragment Link Rewriter Provider - HTML](https://helpx.adobe.com/experience-manager/6-5/help/sites-developing/experience-fragments.html#TheExperienceFragmentLinkRewriterProviderHTML). Hotfix per CQ-4265469

#### Forms - Servizi basati su documenti - Incluso

* Solo OSGi: È stato aggiunto un nuovo attributo PAGECOUNT in Output e Forms Service. NPR-28922: Hotfix per CQ-4270870
* Solo OSGi: È stato abilitato il supporto per la creazione di file PDF statici tramite Forms Service. NPR-28572: Hotfix per CQ-4270869
* Abilitazione delle autorizzazioni su XMLForm.exe per gli utenti amministratore e root. NPR-29237: Hotfix per CQ-4267080

### Bundle OSGi e pacchetti di contenuti

Nei documenti di testo seguenti sono elencati i bundle OSGi e i pacchetti di contenuti inclusi in AEM 6.5.1.0

Elenco dei bundle OSGi inclusi in AEM 6.5.1.0

[Ottieni file](assets/6_5-bundle-list.txt)

Elenco dei pacchetti di contenuti inclusi in AEM 6.5.1.0

[Ottieni file](assets/6_5-content-package-list.txt)
