---
title: Configurazione del framework di integrazione della traduzione
seo-title: Configurazione del framework di integrazione della traduzione
description: Scopri come configurare il framework di integrazione della traduzione.
seo-description: Scopri come configurare il framework di integrazione della traduzione.
uuid: 5ecfe154-732f-4a13-96f8-92f55023c54d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 200f51ab-f9bf-4989-91af-c3904fc673e5
feature: Copia lingua
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1565'
ht-degree: 2%

---


# Configurazione di Translation Integration Framework{#configuring-the-translation-integration-framework}

Il framework di integrazione della traduzione si integra con servizi di traduzione di terze parti per orchestrare la traduzione dei contenuti AEM.

* Connettiti al provider di servizi di traduzione.
* Creare una configurazione di Translation Integration Framework.
* Associa le configurazioni cloud alle pagine.

Per una panoramica delle funzioni di traduzione dei contenuti in AEM, consulta [Traduzione di contenuti per siti multilingue](/help/sites-administering/translation.md).

## Connessione a un provider di servizi di traduzione {#connecting-to-a-translation-service-provider}

Crea una configurazione cloud che si connette AEM al provider di servizi di traduzione. AEM include la funzionalità di connessione a Microsoft Translator per impostazione predefinita.
I seguenti fornitori di traduzione forniscono un’implementazione della nuova API per i progetti di traduzione. Collegamenti per ulteriori informazioni sull’integrazione:

* [Translations.com](https://exchange.adobe.com/experiencecloud.details.90104.globallink-connect-plus-for-aem.html)  (Adobe Exchange Premier Partner)
* [Tecnologie del Tablet argilla](https://exchange.adobe.com/experiencecloud.details.90064.clay-tablet-translation-for-experience-manager.html)
* [Lionbridge](https://exchange.adobe.com/experiencecloud.details.100064.lionbridge-connector-for-experience-manager-63.html)
* [Memsource](https://exchange.adobe.com/experiencecloud.details.103166.memsource-connector-for-adobe-experience-manager.html)
* [Cloudwords](https://exchange.adobe.com/experiencecloud.details.90019.html)
* [CrossLang NV](https://exchange.adobe.com/experiencecloud.details.90049.crosslang-xtm-for-adobe-experience-manager.html)
* [Lingotek](https://exchange.adobe.com/experiencecloud.details.90088.lingotek-collaborative-translation-platform.html)
* [Smartphone](https://exchange.adobe.com/experiencecloud.details.90101.smartling-connector-for-adobe-experience-manager.html)
* [SDL](https://exchange.adobe.com/experiencecloud.details.100110.sdl-translation-management.html)
* [Sistro](https://exchange.adobe.com/experiencecloud.details.90233.systran-for-adobe-experience-manager.html)
* [Altlang](https://exchange.adobe.com/experiencecloud.details.90222.altlang.html)
* Microsoft (Microsoft Translator è preinstallato in AEM)

>[!NOTE]
>
>Per trovare l&#39;ultimo elenco di fornitori di traduzione umana e automatica, date un&#39;occhiata a queste pagine:
>
>
>* [Traduzione umana AEM](https://www.adobe.com/go/aem-human-translation-connectors)
>* [Traduzione automatica AEM](https://www.adobe.com/go/aem-machine-translation-connectors)

>



Dopo aver installato un pacchetto di connettore, puoi creare una configurazione cloud per il connettore. In genere, è necessario fornire le credenziali per l&#39;autenticazione con il servizio di traduzione. Per informazioni sull&#39;aggiunta di una configurazione cloud per il connettore Microsoft Translator, vedere [Integrazione con Microsoft Translator](/help/sites-administering/tc-msconf.md).

Se necessario, puoi creare più configurazioni cloud per lo stesso connettore. Ad esempio, crea una configurazione per ciascuno degli account o dei progetti che hai con lo stesso fornitore.

Dopo aver configurato una connessione, puoi creare la configurazione del framework di integrazione di traduzione che la utilizza.

## Creazione di una configurazione dell&#39;integrazione di traduzione {#creating-a-translation-integration-configuration}

Crea una configurazione del framework di integrazione della traduzione per specificare come tradurre il contenuto. La configurazione include le seguenti informazioni:

* Quale provider di servizi di traduzione utilizzare.
* Se la traduzione umana o automatica deve essere eseguita.
* Se tradurre altro contenuto associato a una pagina o a una risorsa, ad esempio i tag.

Dopo aver creato una configurazione di framework, associ la configurazione cloud alle pagine che desideri tradurre in base alla configurazione. Quando il processo di traduzione viene avviato, il flusso di lavoro di traduzione procede in base alla configurazione del framework associato.

Quando diverse sezioni del sito web hanno requisiti di traduzione diversi, crea di conseguenza configurazioni di framework multiple. Ad esempio, un sito web multilingue include copie in lingua inglese, spagnola e giapponese. Il proprietario del sito utilizza due diversi fornitori di servizi di traduzione per le traduzioni in spagnolo e giapponese. Pertanto, sono configurate due configurazioni del framework. Ogni configurazione utilizza un provider di servizi di traduzione diverso.

Dopo aver configurato un framework di integrazione della traduzione, è possibile [associarlo alle pagine](/help/sites-administering/tc-prep.md) che lo utilizzano.

**Nota:** per una panoramica delle funzioni di traduzione dei contenuti in AEM, consulta  [Traduzione di contenuti per siti multilingue](/help/sites-administering/translation.md).

Una singola configurazione del framework controlla come tradurre il contenuto della pagina, il contenuto della community e le risorse.
![chlimage_1-386](assets/translation-config-65.jpg)

### Proprietà di configurazione dei siti {#sites-configuration-properties}

Le proprietà Sites controllano la modalità di traduzione del contenuto della pagina.

<table>
 <tbody>
  <tr>
   <th>Proprietà</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td>Flusso di lavoro per traduzione</td>
   <td><p>Selezionare il metodo di traduzione eseguito dal framework per il contenuto del sito:</p>
    <ul>
     <li>Traduzione automatica: Il provider di traduzione esegue la traduzione utilizzando la traduzione automatica in tempo reale.</li>
     <li>Traduzione umana: Il contenuto viene inviato al provider di traduzione per essere tradotto dai traduttori. </li>
     <li>Non tradurre: Il contenuto non viene inviato per la traduzione. Questo consente di saltare alcuni rami di contenuto che non sarebbero tradotti ma che potrebbero essere aggiornati con i contenuti più recenti.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Provider traduzione</td>
   <td>Selezionare il provider di traduzione per eseguire la traduzione. Un provider viene visualizzato nell'elenco quando è installato il connettore corrispondente.</td>
  </tr>
  <tr>
   <td>Categoria contenuto</td>
   <td>(Solo traduzione automatica) Una categoria che descrive il contenuto che si sta traducendo. La categoria può influenzare la scelta della terminologia e della formulazione durante la traduzione dei contenuti.</td>
  </tr>
  <tr>
   <td>Traduci tag</td>
   <td>Seleziona per tradurre i tag associati alla pagina.</td>
  </tr>
  <tr>
   <td>Traduci risorse di pagina</td>
   <td><p>Seleziona come tradurre le risorse aggiunte ai componenti dal file system o a cui si fa riferimento da Assets:</p>
    <ul>
     <li>Non tradurre: Le risorse di pagina non sono tradotte.</li>
     <li>Utilizzo del flusso di lavoro di traduzione Sites : Le risorse vengono gestite in base alle proprietà di configurazione nella scheda Sites .</li>
     <li>Utilizzo del flusso di lavoro di traduzione di Assets: Le risorse vengono gestite in base alla configurazione delle proprietà nella scheda Risorse .</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Esegui automaticamente traduzione</td>
   <td>Selezionare questa opzione per eseguire automaticamente i processi di traduzione dopo la creazione dei progetti di traduzione. Non è possibile esaminare e ampliare il processo di traduzione quando si seleziona questa opzione.</td>
  </tr>
 </tbody>
</table>

### Proprietà di configurazione delle community {#communities-configuration-properties}

Le proprietà di Communities controllano le modalità di traduzione dei contenuti generati dall’utente. La traduzione dei contenuti generati dall’utente utilizza sempre la traduzione automatica. Per ulteriori informazioni, consulta [Traduzione di contenuti generati dagli utenti](/help/communities/translate-ugc.md).

| Proprietà | Descrizione |
|---|---|
| Provider traduzione | Selezionare il provider di traduzione per eseguire la traduzione. Il provider per il quale vengono create le configurazioni cloud viene visualizzato nell’elenco. |
| Categoria contenuto | Una categoria che descrive il contenuto che si sta traducendo. La categoria può influenzare la scelta della terminologia e della formulazione durante la traduzione dei contenuti. |
| Scegliere Un&#39;Impostazione Internazionale Da Utilizzare Come Archivio Di Condivisione Globale | (Facoltativo) Selezionando le impostazioni internazionali per la memorizzazione degli UGC, i post di tutte le copie della lingua verranno visualizzati in una conversazione globale. Per convenzione, scegli le impostazioni internazionali della [lingua di base](/help/communities/sites-console.md#translation) per il sito web. Se si sceglie Nessun archivio comune, la traduzione globale verrà disabilitata. Per impostazione predefinita, la traduzione globale è disabilitata. |

### Proprietà di configurazione delle risorse {#assets-configuration-properties}

Le proprietà delle risorse controllano come configurare le risorse. Per ulteriori informazioni sulla traduzione delle risorse, consulta [Creazione di copie per lingua per le risorse](/help/assets/translation-projects.md).

<table>
 <tbody>
  <tr>
   <th>Proprietà</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td>Flusso di lavoro per traduzione</td>
   <td><p>Seleziona il tipo di traduzione che il framework esegue per le risorse:</p>
    <ul>
     <li>Traduzione automatica: Il provider di traduzione esegue la traduzione immediatamente utilizzando la traduzione automatica.</li>
     <li>Traduzione umana: Il contenuto viene inviato automaticamente al provider di traduzione per essere tradotto manualmente. </li>
     <li>Non tradurre: Le risorse non vengono inviate per la traduzione.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Provider traduzione</td>
   <td>Selezionare il provider di traduzione per eseguire la traduzione. Un provider viene visualizzato nell'elenco quando è installato il connettore corrispondente.</td>
  </tr>
  <tr>
   <td>Categoria contenuto</td>
   <td>(Solo traduzione automatica) Una categoria che descrive il contenuto che si sta traducendo. La categoria può influenzare la scelta della terminologia e della formulazione durante la traduzione dei contenuti.</td>
  </tr>
  <tr>
   <td>Traduci risorse</td>
   <td>Seleziona per includere le risorse nel progetto di traduzione. </td>
  </tr>
  <tr>
   <td>Traduci metadati</td>
   <td>Seleziona per tradurre i metadati delle risorse.</td>
  </tr>
  <tr>
   <td>Traduci tag</td>
   <td>Seleziona per tradurre i tag associati alla risorsa.</td>
  </tr>
  <tr>
   <td>Esegui automaticamente traduzione</td>
   <td>Selezionare questa opzione per eseguire automaticamente i processi di traduzione dopo la creazione dei progetti di traduzione. Non è possibile rivedere o ampliare il processo di traduzione quando si seleziona questa opzione.</td>
  </tr>
 </tbody>
</table>

1. Nella barra laterale, tocca o fai clic su Strumenti > Operazioni > Cloud > Cloud Services.
1. Nell’area Integrazione di traduzione, se sono state create configurazioni, determina quale collegamento viene visualizzato:

   * Se non è stata creata alcuna configurazione, tocca o fai clic su Configura ora.
   * Se le configurazioni esistono già, tocca o fai clic su Mostra configurazioni, quindi tocca o fai clic sul collegamento + che appare accanto a Configurazioni disponibili.

1. Digita un nome per la configurazione e quindi tocca o fai clic su Crea .
1. Configura le proprietà nella scheda Sites, Communities e Assets , quindi tocca o fai clic su OK.

## Configurazione delle pagine per la traduzione {#configuring-pages-for-translation}

Per configurare la traduzione delle pagine sorgente in altre lingue, associa le pagine alle seguenti configurazioni cloud:

* Configurazione cloud che si connette AEM al provider di traduzione.
* Il framework di integrazione della traduzione che configura i dettagli della traduzione.

La configurazione cloud del framework di integrazione della traduzione identifica la configurazione cloud da utilizzare per la connessione al provider di servizi. Quando si associa una pagina sorgente a una configurazione cloud del framework, questa deve essere associata alla configurazione cloud del provider di servizi utilizzata dalla configurazione cloud del framework.

Quando si associa una pagina a una configurazione cloud, i discendenti della pagina ereditano l’associazione. Ad esempio, se associ la pagina /content/geometrixx/en/products a un framework di integrazione della traduzione, la pagina Prodotti e tutte le pagine sottostanti vengono tradotte in base al framework.

Se necessario, è possibile modificare l’associazione in una pagina decrescente. Ad esempio, il contenuto di un sito web riguarda principalmente l&#39;abbigliamento. Tuttavia, un ramo di pagine descrive l’azienda. La pagina principale del sito è associata a un framework di integrazione della traduzione che specifica la traduzione automatica utilizzando la categoria Abbigliamento. Il ramo che descrive l&#39;azienda utilizza un framework che esegue la traduzione automatica utilizzando la categoria Generale.

Inoltre, per tutte le community [componenti SCF](/help/communities/scf.md) sulle pagine, il contenuto generato dall’utente (UGC) includerà la possibilità per gli utenti di tradurre i contenuti. Per ulteriori informazioni, consulta [Traduzione di contenuti generati dagli utenti](/help/communities/translate-ugc.md).

### Associazione di una pagina a un provider di traduzione {#associating-a-page-with-a-translation-provider}

Associa una pagina al provider di traduzione utilizzato per tradurre la pagina e le pagine discendenti.

1. Nella console Sites, seleziona la pagina da configurare e tocca o fai clic su Visualizza proprietà .
1. Tocca o fai clic su Modifica , quindi tocca o fai clic sulla scheda Cloud Services .
1. Tocca o fai clic su Aggiungi configurazione > Integrazione di traduzione.
1. Seleziona il provider di traduzione da utilizzare, quindi tocca o fai clic su Fine.

### Associazione di pagine a un framework di integrazione della traduzione {#associating-pages-with-a-translation-integration-framework}

Associare una pagina a Translation Integration Framework che definisce come eseguire la traduzione della pagina e delle pagine discendenti.

1. Nella console Sites, seleziona la pagina da configurare e tocca o fai clic su Visualizza proprietà .
1. Tocca o fai clic su Modifica , quindi tocca o fai clic sulla scheda Cloud Services .
1. Tocca o fai clic su Aggiungi configurazione > Integrazione di traduzione.
1. Seleziona il framework di integrazione della traduzione da utilizzare, quindi tocca o fai clic su Fine.

