---
title: Metadati C2PA [!DNL Experience Manager Assets]
description: Scopri come [!DNL Experience Manager Assets] rileva i metadati C2PA sulle risorse caricate, li contrassegna nell'interfaccia utente e firma le rappresentazioni generate per le risorse Gen AI.
role: User, Admin, Developer
feature: Asset Management, Metadata, Renditions, Workflow, Asset Processing
solution: Experience Manager, Experience Manager Assets
source-git-commit: f47205896ed512deadb4d31acbfe0fafa18515e7
workflow-type: tm+mt
source-wordcount: '2585'
ht-degree: 6%
---

# Metadati C2PA in [!DNL Experience Manager Assets] {#c2pa-metadata}

I brand sono sempre più attenti alla trasparenza dei contenuti, la divulgazione circa l’utilizzo dell’intelligenza artificiale e la prevenzione rispetto alla manomissione delle risorse. Content Authenticity Initiative (CAI) di Adobe crea strumenti conformi allo standard tecnico [Coalition for Content Provenance and Authenticity](https://c2pa.org/specifications/specifications/2.2/specs/C2PA_Specification.html) (C2PA). I metadati C2PA, un nuovo tipo di metadati in grado di evidenziare eventuali manomissioni, aiutano gli utenti a comprendere la linea di contenuti e a garantire l’integrità delle risorse del brand. Possono includere un’ampia gamma di dati di provenienza che offrono informazioni sulla cronologia di una risorsa digitale.

Queste informazioni includono:

* **Emittente o firmatario:** informazioni sull&#39;entità o sulla società che ha emesso la firma digitale per la risorsa.
* **Data problema:** la data in cui i metadati C2PA sono stati applicati alla risorsa.
* **Processo:** record di eventuali modifiche apportate alla risorsa.
* **Dettagli dispositivo:** informazioni sull’app o sul dispositivo utilizzato per creare o modificare la risorsa.
* **Strumento di intelligenza artificiale utilizzato:** se è stata utilizzata l&#39;intelligenza artificiale generativa per modificare o creare la risorsa, viene incluso il nome del modello utilizzato.
* **Altre informazioni importanti:** dati aggiuntivi che offrono più contesto sulla cronologia di una risorsa.

Per ulteriori informazioni sulla cronologia di una risorsa, vedi [Verifica](https://contentcredentials.org/verify).

[!DNL Adobe Experience Manager Assets] rileva i metadati C2PA quando carichi o aggiorni una risorsa, contrassegna tali risorse nell&#39;interfaccia utente [!DNL Assets] e mantiene la divulgazione di IA di generazione intatta sulle rappresentazioni generate da [!DNL Experience Manager]. Ogni volta che [!DNL Experience Manager] crea o modifica una rappresentazione di una risorsa Gen AI, ad esempio una miniatura, una rappresentazione web, una copia filigranata o una trascodifica video, [!DNL Experience Manager] segnala tale rappresentazione con un nuovo metadati C2PA che fa riferimento alla risorsa originale come relativa risorsa principale. Le rappresentazioni scaricate, pubblicate o condivise mantengono la loro provenienza.

## Prerequisiti {#Prerequisites}

Il supporto per i metadati C2PA richiede [!DNL Adobe Experience Manager] 6.5 Service Pack. Nel Service Pack 6.5.25.0, installare [AEM 6.5 SP25 - C2PA GenAI compliance hotfix](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/cq-6.5.0-hotfix-ASSETS-75868-SP25-1.0.zip).

## Piattaforme e formati supportati {#supported-formats}

### Formati {#formats}

[!DNL Experience Manager] firma le rappresentazioni nei formati supportati dalla [specifica C2PA](https://c2pa.org/specifications/specifications/2.2/specs/C2PA_Specification.html) per i manifesti incorporati.

| Tipo | Formati | Tipi MIME |
|---|---|---|
| Immagine | JPEG, PNG, GIF, TIFF, DNG, WebP, JPEG XL, AVIF, HEIC/HEIF, SVG | `image/jpeg`, `image/png`, `image/gif`, `image/tiff`, `image/x-adobe-dng`, `image/webp`, `image/jxl`, `image/avif`, `image/heic`, `image/heif`, `image/svg+xml` |
| Video | MP4, MOV, AVI | `video/mp4`, `video/quicktime`, `video/x-msvideo` |
| Audio | MP3, M4A, WAV, FLAC | `audio/mpeg`, `audio/mp4`, `audio/wav`, `audio/flac` |

[!DNL Experience Manager] riconosce anche alias comuni, ad esempio `image/jpg`, `image/pjpeg`, `image/x-png` e `video/mov`. [!DNL Experience Manager] controlla ogni risorsa caricata per trovare un manifesto, indipendentemente dal formato del file. Le rappresentazioni in altri formati, ad esempio PSD o EPS, non sono firmate.

### Piattaforme {#platforms}

Il supporto per i metadati C2PA si basa su un componente C2PA nativo che viene fornito all&#39;interno del bundle `cq-dam-core`, con una build per ogni piattaforma supportata. All&#39;avvio del servizio, [!DNL Experience Manager] estrae la build per la piattaforma (`adobe_c2patool` o `adobe_c2patool.exe` su Windows) nella cartella dei dati privati del bundle, controlla il checksum SHA-256 ed esegue il servizio come processo separato. Non è necessario installare o modificare `PATH`.

| Sistema operativo | Architettura |
|---|---|
| Linux (glibc 2.28 o versione successiva, incluso Red Hat Enterprise Linux 8) | `x86_64`, `aarch64` |
| macOS | `x86_64`, `aarch64` (silicio Apple) |
| Windows | `x86_64` |

Funziona allo stesso modo per [!DNL Adobe Managed Services] e le distribuzioni locali. Assicurarsi che il processo [!DNL Experience Manager] possa avviare l&#39;eseguibile. Se si utilizzano installazioni di `noexec`, antivirus o software di protezione dell&#39;endpoint, consentire l&#39;esecuzione di `adobe_c2patool` dalla cartella `crx-quickstart`. In caso contrario, il supporto dei metadati C2PA non viene avviato.

## Funzionamento dei metadati C2PA {#how-c2pa-metadata-works}

Il supporto per i metadati C2PA è costituito da due parti: rilevamento quando una risorsa viene caricata o aggiornata e rifirma ogni volta che [!DNL Experience Manager] genera o modifica una rappresentazione.

### Configurazione del flusso di lavoro {#workflow}

Il passaggio **[!UICONTROL Rileva credenziali C2PA]** visualizzato in [Rileva metadati C2PA](#detect) fa parte del modello di flusso di lavoro predefinito **[!UICONTROL Risorsa di aggiornamento DAM]**. Se utilizzi una copia personalizzata di tale modello, aggiungi tu stesso il passaggio:

1. Nell&#39;interfaccia [!DNL Experience Manager], passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]** e apri il modello in modalità ![Icona Modifica](assets/edit.svg) **[!UICONTROL Modifica]**.
1. Aggiungere il passaggio **[!UICONTROL Rileva credenziali C2PA]** dopo **[!UICONTROL Elaboratore metadati]**, prima che venga generato il rendering.
1. Seleziona **[!UICONTROL Sincronizza]** per salvare il modello.

I passaggi della rappresentazione firmano il loro output solo se il rilevamento è già stato eseguito sulla risorsa. Se il rilevamento viene eseguito dopo di essi, le relative rappresentazioni rimangono prive di firma fino a quando il flusso di lavoro non viene eseguito nuovamente.

### Rilevare metadati C2PA {#detect}

Il flusso di lavoro **[!UICONTROL Risorsa di aggiornamento DAM]** include il passaggio **[!UICONTROL Rileva credenziali C2PA]** che viene eseguito dopo il passaggio **[!UICONTROL Elaboratore metadati]**, come illustrato nella figura seguente. Legge il binario originale della risorsa e registra il risultato nel nodo di metadati della risorsa `jcr:content/metadata`.

![Flusso di lavoro](assets/workflow.png)

Nella tabella seguente sono elencate le proprietà dei metadati chiave nel flusso di lavoro dei metadati C2PA.

| Proprietà | Tipo | Descrizione |
|---|---|---|
| `dam:hasC2PAManifest` | `boolean` | `true`, se il binario originale ha un manifesto C2PA incorporato. È sempre scritto. |
| `dam:isAiGenerated` | `boolean` | `true`, se il manifesto inserisce la risorsa nell&#39;ambito dell&#39;etichettatura Gen AI. Viene scritto solo quando è presente un manifesto. |
| `dam:c2paValidationState` | `string` | Descrive lo stato di convalida del manifesto: `TRUSTED`, `VALID`, `INVALID` o `UNKNOWN`. Viene scritto solo quando è presente un manifesto. |

Quando è presente un manifesto, [!DNL Experience Manager] lo memorizza anche come rendering `c2pa-manifest.json` (`application/json`).

Se si sostituisce la risorsa originale con un binario privo di manifesto, la successiva esecuzione del flusso di lavoro imposta `dam:hasC2PAManifest` su `false` e rimuove `dam:isAiGenerated`, `dam:c2paValidationState` e la rappresentazione `c2pa-manifest.json`.

>[!NOTE]
>
>Un errore di rilevamento non blocca mai l’acquisizione di una risorsa. Se la lettura del manifesto va in timeout o non riesce, [!DNL Experience Manager] registra l&#39;errore, lascia i metadati invariati e continua con il resto del flusso di lavoro.

### Visualizza metadati C2PA nell&#39;interfaccia utente [!DNL Assets] {#view-c2pa-metadata}

Assets che contiene metadati C2PA visualizza il badge **cr** (metadati C2PA) nell&#39;interfaccia utente [!DNL Assets]. Passa a **[!UICONTROL Assets]** > **[!UICONTROL File]** e cerca il badge nell&#39;angolo inferiore sinistro di:

* La miniatura della risorsa in **[!UICONTROL Vista a schede]**.
* La miniatura della risorsa in **[!UICONTROL Vista a colonne]**. Seleziona la risorsa per visualizzarne la miniatura.
* L’area di anteprima della pagina dei dettagli della risorsa.

Il badge **cr** mostrato nella figura seguente indica se una risorsa contiene metadati C2PA. Non mostra il manifesto stesso. Per visualizzare il manifesto completo, scarica la risorsa e aprila in [Verifica](https://contentcredentials.org/verify).

![badge cr](assets/cr.png)

[!DNL Experience Manager] memorizza il manifesto rilevato come una rappresentazione `c2pa-manifest.json` sulla risorsa. Questa rappresentazione è interna. Non viene visualizzato nel pannello **[!UICONTROL Rappresentazioni]** della pagina dei dettagli della risorsa o nel selettore delle rappresentazioni.

### Firma rappresentazioni {#sign-renditions}

Una rappresentazione è un nuovo binario, pertanto il manifesto incorporato nella risorsa originale non lo copre. Per mantenere intatta la divulgazione di Gen AI, [!DNL Experience Manager] firma ogni rappresentazione idonea come ultimo passaggio del processo che la produce. I nuovi metadati C2PA:

* Fa riferimento alla risorsa originale come componente **principale**.
* Registra il modo in cui la rappresentazione è stata derivata dalla risorsa originale, come una delle azioni C2PA `c2pa.resized`, `c2pa.transcoded` o `c2pa.edited`.
* Denomina `Adobe Experience Manager` come agente software.

[!DNL Experience Manager] firma una copia trasformata solo quando tutti i seguenti elementi sono `true`:

* La risorsa di origine ha `dam:isAiGenerated` impostato su `true`. Assets che contengono un manifesto ma non sono generati tramite IA mostra ancora il badge **cr**, ma [!DNL Experience Manager] non firma di nuovo le loro rappresentazioni.
* Il manifesto di origine è leggibile e il relativo stato di convalida non è `INVALID`. [!DNL Experience Manager] non incatena mai una nuova firma in un manifesto che non ha superato la convalida, ad esempio dopo che la risorsa è stata manomessa.
* Il formato di rendering supporta un manifesto C2PA incorporato. Per ulteriori informazioni, vedere [Formati supportati](#supported-formats). [!DNL Experience Manager] ignora i formati non supportati senza un errore.

I seguenti passaggi del flusso di lavoro **[!UICONTROL Flusso di lavoro risorsa aggiornamento DAM completato]** mostrati in [Rileva metadati C2PA](#detect) firmano l&#39;output.

| Passaggio del flusso di lavoro | Rappresentazioni firmate | Azione C2PA registrata |
|---|---|---|
| **[!UICONTROL Elabora miniature]** | Le rappresentazioni delle miniature e l’immagine abilitata per il web. | `c2pa.resized` e `c2pa.transcoded` quando il formato cambia. |
| **[!UICONTROL Miniature EPS (con tecnologia ImageMagick)]** | Output primario, miniature derivate e rappresentazioni Web. | `c2pa.resized`, `c2pa.transcoded` o `c2pa.edited` |
| **[!UICONTROL Miniature FFmpeg]** | Fotogrammi poster video e miniature. | `c2pa.resized` e `c2pa.transcoded` |
| **[!UICONTROL Trascodifica FFmpeg]** | Codifiche video. | `c2pa.transcoded` |
| **[!UICONTROL Rasterizza rappresentazione anteprima immagine PDF/AI]** | Anteprima rappresentazione. (`cqdam.preview.png`) | `c2pa.transcoded` |

Anche i seguenti processi di flusso di lavoro firmano il relativo output quando vengono utilizzati nel flusso di lavoro **[!UICONTROL Flusso di lavoro Aggiorna risorsa DAM completato]**, in un altro flusso di lavoro o in un modello di flusso di lavoro personalizzato. Selezionale nell&#39;elenco **[!UICONTROL Elabora miniature]** di un passaggio del flusso di lavoro come mostrato in [Rileva metadati C2PA](#detect).

| Processo del flusso di lavoro | Rappresentazioni firmate | Azione C2PA registrata |
|---|---|---|
| **[!UICONTROL Crea miniatura]** | Rappresentazioni delle miniature. | `c2pa.resized` e `c2pa.transcoded` quando il formato cambia. |
| **[!UICONTROL Crea immagine abilitata per il Web]** | Copie trasformate web. | `c2pa.resized` e `c2pa.transcoded` quando il formato cambia. |
| **[!UICONTROL Riga di comando]**, ad esempio, con [!DNL ImageMagick] | Output primario, miniature derivate e rappresentazioni Web. | `c2pa.resized`, `c2pa.transcoded` o `c2pa.edited` |
| **[!UICONTROL Processo filigrana immagine]** | Rendering filigrana o rappresentazione originale quando è presente la filigrana. Per ulteriori informazioni, consulta [Filigrana delle risorse](/help/assets/watermarking.md). | `c2pa.edited` |
| **[!UICONTROL Crea storyboard video]** | Frame chiave storyboard. | `c2pa.transcoded` |
| **[!UICONTROL Writeback di XMP]** | La rappresentazione originale, dopo la scrittura dei metadati. Per ulteriori informazioni, vedere [XMP writeback in rendering](/help/assets/xmp-writeback.md). | `c2pa.edited` |

### Proteggere il file binario originale durante il writeback di XMP {#xmp-writeback}

Il writeback di XMP riscrive il file binario originale, interrompendo così il manifesto incorporato. Per le risorse con `dam:hasC2PAManifest` impostato su `true`, [!DNL Experience Manager] modifica il comportamento del passaggio **[!UICONTROL Processo write-back di XMP]** del flusso di lavoro **[!UICONTROL Writeback di metadati DAM]** come segue:

* **Risorse di IA di generazione** (`dam:isAiGenerated` è `true`): [!DNL Experience Manager] scrive il XMP e quindi firma nuovamente il file binario originale, con il file binario di pre-writeback come elemento padre. Salva il writeback e la nuova firma insieme. Se la rifirma non riesce, il passaggio viene ignorato e non riesce.
* **Altre risorse con manifesto**: [!DNL Experience Manager] ignora il writeback di XMP e registra il motivo. Il binario originale e il manifesto rimangono invariati.

### Modalità di firma {#signing-mode}

[!DNL Experience Manager] firma localmente le copie trasformate nell&#39;istanza che le produce con un certificato temporaneo autofirmato generato. La firma non richiede accesso alla rete né configurazione di certificati o chiavi private.

>[!NOTE]
>
>Impossibile configurare un certificato di firma personale. Le convalide come [Verify](https://contentcredentials.org/verify) mostrano la divulgazione di Gen AI della rappresentazione e il collegamento all&#39;originale, ma non identificano la tua organizzazione come firmatario.

## Configurare i metadati C2PA {#configure}

Il supporto per i metadati C2PA è attivato per impostazione predefinita. Non è necessario installare o configurare nulla.

### Configurazione OSGi {#osgi-configuration}

Per modificare la configurazione predefinita, configura il servizio C2PA **[!UICONTROL Day CQ DAM]** (PID `com.day.cq.dam.core.impl.c2pa.C2PAServiceImpl`) in Configuration Manager alle `https://[aem_server]:[port]/system/console/configMgr`, come illustrato nella figura seguente, oppure aggiungi una configurazione OSGi al progetto. Per ulteriori informazioni, vedere [Configurare OSGi](/help/sites-deploying/configuring-osgi.md).

![Configurazione OSGi](assets/OSGi.png)

La tabella seguente elenca le proprietà nella configurazione OSGi del progetto.

| Proprietà | Nome in Configuration Manager | Predefiniti | Descrizione |
|---|---|---|---|
| `enabled` | **[!UICONTROL Abilitato]** | `true` | Attiva o disattiva il supporto dei metadati C2PA. Se è disattivato, [!DNL Experience Manager] non rileva i manifesti e non firma le rappresentazioni. |
| `timeoutMillis` | **[!UICONTROL Timeout CLI (ms)]** | `30000` | Specifica il tempo massimo, in millisecondi, di attesa di [!DNL Experience Manager] per una singola operazione di lettura o firma su un file prima di considerarlo come scaduto. Aumenta questo valore per i file video di grandi dimensioni o per i file immagine ad alta risoluzione. |

Aggiungi ad esempio una configurazione OSGi in `/apps/<your-project>/config/com.day.cq.dam.core.impl.c2pa.C2PAServiceImpl.config`.

```text
enabled=B"true"
timeoutMillis=L"60000"
```

### Disattiva supporto metadati C2PA {#disable}

Nella configurazione **[!UICONTROL Day CQ DAM C2PA Service]** mostrata nella [configurazione OSGi](#osgi-configuration), disabilita l&#39;opzione **[!UICONTROL Enabled]**, quindi salva le modifiche. La modifica entra in vigore immediatamente, senza riavviare il sistema:

* Il passaggio **[!UICONTROL Rileva credenziali C2PA]** visualizzato in [Rileva metadati C2PA](#detect) non è più operativo.
* I passaggi del flusso di lavoro creano le rappresentazioni senza firmarle.
* Assets elaborato in precedenza mantiene la proprietà `dam:hasC2PAManifest` e mostra comunque il badge **cr**.

>[!CAUTION]
>
>Dopo aver disabilitato l&#39;opzione **[!UICONTROL Enabled]**, le rappresentazioni delle risorse Gen AI non contengono metadati C2PA. Se desideri rispettare le normative di divulgazione di IA per la generazione, abilita l&#39;opzione **[!UICONTROL Abilitato]**.

## Personalizzare la pipeline di elaborazione {#customize}

Per aggiungere, rimuovere o riordinare i passaggi in **[!UICONTROL Risorsa di aggiornamento DAM]** e mantenere intatta la divulgazione di IA di generazione, attieniti alle seguenti regole:

* **Esegui prima il rilevamento.** Mantieni **[!UICONTROL Rileva credenziali C2PA]** davanti a ogni passaggio che crea o modifica le rappresentazioni.
* **Firma per ultimo.** Qualsiasi modifica apportata a un file binario dopo la firma ne invalida la firma. Non eseguire i passaggi che modificano una copia trasformata dopo il passaggio che l&#39;ha firmata.
* **Utilizzare i passaggi che firmano.** I passaggi predefiniti elencati in [Firma rappresentazioni](#sign-renditions) firmano il relativo output. I passaggi personalizzati e gli strumenti di terze parti eseguiti tramite elementi diversi dal processo **[!UICONTROL Riga di comando]** non firmano l&#39;output a meno che non venga aggiunta esplicitamente la firma. Per ulteriori informazioni, consulta [Elaborare risorse utilizzando gestori di supporti e flussi di lavoro](/help/assets/media-handlers.md).
* **Non modificare l&#39;originale sul posto** a meno che non venga nuovamente firmato dal passaggio, come avviene per **[!UICONTROL Writeback di XMP]** e **[!UICONTROL Processo filigrana immagine]**.

### Firmare le rappresentazioni da un passaggio di flusso di lavoro personalizzato {#custom-step}

I passaggi del flusso di lavoro personalizzati che producono copie trasformate possono firmarli tramite il servizio OSGi `com.day.cq.dam.api.c2pa.C2PASigner`. Applica le stesse regole di idoneità dei passaggi incorporati ma riporta il risultato come `C2PASigningOutcome`.

```java
import java.util.Collections;

import org.osgi.service.component.annotations.Reference;
import org.osgi.service.component.annotations.ReferenceCardinality;
import org.osgi.service.component.annotations.ReferencePolicy;

import com.day.cq.dam.api.Asset;
import com.day.cq.dam.api.Rendition;
import com.day.cq.dam.api.c2pa.C2PAAction;
import com.day.cq.dam.api.c2pa.C2PAConstants;
import com.day.cq.dam.api.c2pa.C2PASigner;
import com.day.cq.dam.api.c2pa.C2PASigningOutcome;

// Inside your WorkflowProcess implementation:

@Reference(cardinality = ReferenceCardinality.OPTIONAL, policy = ReferencePolicy.DYNAMIC)
private volatile C2PASigner c2paSigner;

private void signRendition(Asset asset, Rendition rendition) {
    C2PASigner signer = c2paSigner;
    if (signer == null) {
        return;
    }
    C2PASigningOutcome outcome = signer.signIfEligible(asset, rendition,
            Collections.singletonList(
                    new C2PAAction(C2PAConstants.ACTION_RESIZED, C2PAConstants.SOFTWARE_AGENT, null)));
    if (outcome == C2PASigningOutcome.FAILED) {
        // Log, retry, or alert an operator.
    }
}
```

Chiamare `signIfEligible` solo dopo che il passaggio ha completato la scrittura della rappresentazione. Il servizio OSGi fornisce i metodi elencati nella tabella seguente.

| Metodo | Utilizzala per |
|---|---|
| `signIfEligible(Asset, Rendition, List<C2PAAction>)` | Firma una nuova rappresentazione, con la risorsa di origine come risorsa principale. |
| `signIfEligible(Asset, Map<Rendition, List<C2PAAction>>)` | Firma diverse rappresentazioni derivate dalla stessa risorsa. Questo metodo legge il manifesto di origine una volta. |
| `captureResignState(Asset)` | Acquisisci un’immagine della risorsa originale prima che il passaggio la modifichi nella sua posizione. Questo metodo restituisce `null` se la risorsa non è idonea. |
| `resign(Asset, Rendition, List<C2PAAction>)` | Applica nuovamente la firma alla risorsa originale dopo una modifica diretta, con l’immagine come elemento principale. |
| `discardResignState(Rendition)` | Posiziona un&#39;immagine scattata ma non da utilizzare, ad esempio perché la modifica non è riuscita. |

I valori di `C2PASigningOutcome` sono menzionati nella tabella seguente.

| Risultato | Descrizione |
|---|---|
| `SIGNED` | [!DNL Experience Manager] ha firmato il rendering. |
| `SKIPPED_SOURCE_NOT_AI_GENERATED` | La risorsa di origine non viene contrassegnata come risorsa generata da AI. |
| `SKIPPED_FORMAT_NOT_ELIGIBLE` | Il formato di rendering non supporta il manifesto C2PA incorporato. |
| `SKIPPED_MANIFEST_UNREADABLE` | [!DNL Experience Manager] non ha trovato alcun manifesto nella risorsa di origine. |
| `SKIPPED_MANIFEST_NOT_VALID` | Convalida del manifesto di origine non riuscita. |
| `SKIPPED_SERVICE_UNAVAILABLE` | Il supporto per i metadati C2PA è disattivato o non disponibile. |
| `FAILED` | Lettura del manifesto di origine o firma della rappresentazione non riuscita. |

Per verificare l&#39;idoneità prima di generare una rappresentazione costosa, chiamare `C2PASupportedFormats.isEligible(...)`.

## Risoluzione di problemi {#troubleshooting}

Durante la risoluzione dei problemi, imposta i seguenti logger su `DEBUG` nella **[!UICONTROL configurazione del logger di registrazione di Apache Sling]**.

* `com.day.cq.dam.core.impl.c2pa`: estrazione del componente C2PA nativo, letture del manifesto e firma.
* `com.day.cq.dam.core.process.DetectC2PACredentialProcess`: rilevamento.

| Sintomo | Possibile causa | Risoluzione |
|---|---|---|
| Nessuna risorsa mostra il badge **cr**. | Il supporto per i metadati C2PA è disattivato oppure il modello di flusso di lavoro non include la fase di rilevamento. | Verifica che **[!UICONTROL Enabled]** sia abilitato nella configurazione **[!UICONTROL Day CQ DAM C2PA Service]** e che il modello **[!UICONTROL DAM Update Asset]** includa **[!UICONTROL Detect C2PA Credential]**. |
| Una risorsa che sai ha un manifesto ma non mostra alcun distintivo. | La risorsa è stata caricata prima che la funzione fosse disponibile. | Esegui di nuovo il flusso di lavoro **[!UICONTROL Risorsa di aggiornamento DAM]** sulla risorsa, ad esempio da **[!UICONTROL Timeline]** > **[!UICONTROL Avvia flusso di lavoro]**. |
| Il servizio non si avvia. Il log degli errori segnala che `adobe_c2patool` non può essere estratto o contrassegnato come eseguibile. | Non esiste alcun binario per il sistema operativo o l&#39;architettura oppure il file system blocca gli eseguibili. | Utilizza una piattaforma supportata. Consenti al processo [!DNL Experience Manager] di eseguire gli eseguibili dalla cartella `crx-quickstart`. |
| Il registro errori segnala `GLIBC_2.xx not found`. | L&#39;host Linux esegue una versione glibc precedente alla 2.28. | Aggiornare il sistema operativo host. |
| Timeout del rilevamento o della firma. | I file di grandi dimensioni richiedono più tempo del timeout predefinito di 30 secondi. | Aumentare **[!UICONTROL Timeout CLI (ms)]**. |
| Le rappresentazioni di una risorsa Gen AI non sono firmate. | Il formato non è supportato, il manifesto è `INVALID` o il rilevamento è stato eseguito dopo il passaggio della rappresentazione. | Controllare `dam:c2paValidationState` e il formato della rappresentazione. Sposta **[!UICONTROL Rileva credenziali C2PA]** prima dei passaggi della rappresentazione. |
| Il writeback di XMP non aggiorna una risorsa. | La risorsa contiene un manifesto ma non è generata tramite IA, pertanto [!DNL Experience Manager] mantiene il suo originale invariato. | Si tratta di un comportamento previsto. Per ulteriori informazioni, vedere [Proteggere l&#39;originale durante il writeback di XMP](#xmp-writeback). |

## Limitazioni {#limitations}

* L&#39;interfaccia utente [!DNL Assets] mostra solo se è presente un metadati C2PA. Non dispone di alcun pannello per i dettagli del manifesto.
* [!DNL Experience Manager] firma nuovamente le rappresentazioni solo per le risorse generate tramite IA. Le rappresentazioni di altre risorse che contengono un manifesto vengono create senza metadati C2PA.
* [!DNL Experience Manager] firma con un certificato temporaneo autofirmato. I certificati di firma personalizzati o specifici dell&#39;organizzazione non sono supportati.


>[!MORELIKETHIS]
>
>* [Metadati C2PA nella visualizzazione Assets di [!DNL Experience Manager as a Cloud Service]](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/assets/assets-view/c2pa-metadata-assets-view)
>* [Metadati C2PA in [!DNL Experience Manager Assets Essentials]](https://experienceleague.adobe.com/it/docs/experience-manager-assets-essentials/help/content-credentials)
>* [Metadati C2PA in [!DNL Dynamic Media]](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/c2pa-metadata)
>* [Writeback di XMP alle rappresentazioni](/help/assets/xmp-writeback.md)
>* [Filigrana le risorse](/help/assets/watermarking.md)
>* [Content Authenticity Initiative](https://contentauthenticity.org/)
>* [Verifica](https://contentcredentials.org/verify)
