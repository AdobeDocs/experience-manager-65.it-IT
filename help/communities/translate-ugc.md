---
title: Traduzione di contenuti generati dall'utente
description: Scopri come la traduzione dei contenuti UGC consente ai visitatori e ai membri del sito di sperimentare una community globale rimuovendo le barriere linguistiche.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: ac54f06e-1545-44bb-9f8f-970f161ebb72
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1111'
ht-degree: 0%

---

# Traduzione di contenuti generati dall&#39;utente {#translating-user-generated-content}

La funzionalità di traduzione per le community Adobe Experience Manager (AEM) estende il concetto di [traduzione del contenuto della pagina](../../help/sites-administering/translation.md) ai contenuti generati dagli utenti (UGC) pubblicati nei siti della community tramite [componenti SCF (Social Component Framework)](scf.md).

La traduzione di UGC consente ai visitatori e ai membri del sito di sperimentare una community globale rimuovendo le barriere linguistiche.

Ad esempio, supponiamo che:

* Un membro francese ha pubblicato una ricetta in francese per il forum comunitario di un sito Web di cucina multinazionale.
* Un altro membro del Giappone utilizza la funzione di traduzione per attivare la traduzione della ricetta dal francese al giapponese.
* Dopo aver letto la ricetta in giapponese, il membro giapponese ha pubblicato un commento in giapponese.
* Il membro dalla Francia utilizza la funzione di traduzione per tradurre il commento giapponese in francese.
* Comunicazione globale.

## Panoramica {#overview}

Questa sezione descrive in modo specifico come funziona il servizio di traduzione con UGC. Si presuppone inoltre che tu abbia familiarità con le modalità di connessione di AEM a un [fornitore di servizi di traduzione](../../help/sites-administering/translation.md#connectingtoatranslationserviceprovider) e di integrazione di tale servizio in un sito Web configurando un [framework di integrazione della traduzione](../../help/sites-administering/tc-tic.md).

Quando un fornitore di servizi di traduzione è associato al sito, ogni copia per lingua del sito mantiene i propri thread di UGC pubblicati tramite componenti SCF come i commenti.

Quando viene configurata un’integrazione di traduzione oltre al fornitore di servizi di traduzione, è possibile che ogni copia per lingua del sito condivida un singolo thread di UGC, fornendo una comunicazione globale tra le copie per lingua. Invece di un thread di discussione separato per lingua, l&#39;[archivio condiviso globale](#global-translation-of-ugc) configurato consente di rendere visibile l&#39;intero thread indipendentemente dalla copia per lingua dalla quale viene visualizzato. Inoltre, è possibile configurare più configurazioni di integrazione della traduzione specificando diversi store condivisi globali per un raggruppamento logico di partecipanti globali, ad esempio per aree geografiche.

## Il servizio di traduzione predefinito {#the-default-translation-service}

AEM Communities include una [licenza di prova](../../help/sites-administering/tc-msconf.md#microsoft-translator-trial-license) per un [servizio di traduzione predefinito](../../help/sites-administering/tc-msconf.md) abilitato per diverse lingue.

Quando [si crea un sito community](sites-console.md), il servizio di traduzione predefinito viene attivato quando `Allow Machine Translation` viene selezionato dal pannello secondario [TRADUZIONE](sites-console.md#translation).

>[!CAUTION]
>
>Il servizio di traduzione predefinito è solo a scopo dimostrativo.
>
>Per un sistema di produzione, è necessario un servizio di traduzione concesso in licenza. Se non si dispone della licenza, il servizio di traduzione predefinito deve essere [disattivato](../../help/sites-administering/tc-msconf.md#microsoft-translator-trial-license-geometrixx-outdoors).

## Traduzione globale di UGC {#global-translation-of-ugc}

Quando un sito Web contiene più [copie per lingua](../../help/sites-administering/tc-prep.md), il servizio di traduzione predefinito non riconosce che il contenuto generato dall&#39;utente immesso in un sito possa essere correlato al contenuto generato dall&#39;utente immesso in un altro sito. Ciò si verifica quando l’UGC viene generato dallo stesso componente (la copia per lingua della pagina contenente il componente).

È simile a gruppi di persone che discutono di un argomento. Non sono a conoscenza dei commenti che vengono fatti in gruppi diversi dal proprio, rispetto a tutti in un gruppo di grandi dimensioni che partecipano a una conversazione.

Se desideri una conversazione di gruppo, puoi abilitare la traduzione globale su un sito web con più copie per lingua, in modo che l’intero thread sia visibile indipendentemente dalla copia per lingua dalla quale viene visualizzato.

Ad esempio, se un forum è stato creato sul sito base, sono state create copie per lingua e la traduzione globale è stata abilitata, un argomento pubblicato nel forum e creato in una sola lingua verrebbe visualizzato in tutte le copie per lingua. Lo stesso vale per qualsiasi risposta, indipendentemente dalla lingua dalla quale è stata immessa la copia della risposta. Il risultato è che l&#39;argomento e l&#39;intero thread di risposte saranno visibili indipendentemente dalla copia per lingua in cui viene visualizzato l&#39;argomento.

>[!CAUTION]
>
>Qualsiasi UGC che esisteva prima della traduzione globale non è più visibile.
>
>Mentre l&#39;UGC si trova ancora nell&#39;[archivio comune](working-with-srp.md), si trova nel percorso UGC specifico della lingua, mentre il nuovo contenuto, aggiunto dopo la configurazione della traduzione globale, viene recuperato dal percorso dell&#39;archivio condiviso globale.
>
>Non esiste uno strumento di migrazione per spostare o unire contenuti specifici per lingua nell’archivio condiviso globale.

### Configurazione integrazione traduzione {#translation-integration-configuration}

Per creare un’integrazione di traduzione, che integra un connettore del servizio di traduzione con il sito web nell’istanza di authoring:

* Accedi come amministratore
* Dal [menu principale](http://localhost:4502/)
* Seleziona **[!UICONTROL Strumenti]**
* Seleziona **[!UICONTROL Operazioni]**
* Seleziona **[!UICONTROL Cloud]**
* Seleziona **[!UICONTROL Cloud Service]**
* Scorri verso il basso fino a **[!UICONTROL Integrazione traduzione]**

  ![integrazione-traduzione](assets/translation-integration.png)

* Seleziona **[!UICONTROL Mostra configurazioni]**

  ![show-configuration](assets/translation-integration1.png)

* Seleziona l&#39;icona `[+]` accanto a **[!UICONTROL Configurazioni disponibili]** per creare una configurazione.

#### Finestra di dialogo Crea configurazione {#create-configuration-dialog}

![create-configuration](assets/translation-integration2.png)

* **[!UICONTROL Configurazione padre]**

  (Obbligatorio) In genere lascia come impostazione predefinita. Il valore predefinito è `/etc/cloudservices/translation`.

* **[!UICONTROL Titolo]**

  (Obbligatorio) Inserisci un titolo da visualizzare a tua scelta. Nessun valore predefinito.

* **[!UICONTROL Nome]**

  (Facoltativo) Immetti un nome per la configurazione. L&#39;impostazione predefinita è un nome di nodo basato sul titolo.

* Seleziona **[!UICONTROL Crea]**

#### Finestra di dialogo Configurazione traduzione {#translation-config-dialog}

![finestra di dialogo per configurazione](assets/translation-integration3.png)

Per istruzioni dettagliate, vedere [Creazione di una configurazione dell&#39;integrazione della traduzione](../../help/sites-administering/tc-tic.md#creating-a-translation-integration-configuration).

* Scheda **[!UICONTROL Siti]**: può lasciare come valori predefiniti.

* Scheda **[!UICONTROL Communities]**:
   * **[!UICONTROL Provider traduzione]**
Seleziona il fornitore di traduzione dall’elenco a discesa. Il valore predefinito è `microsoft`, il servizio di prova.

   * **[!UICONTROL Categoria contenuto]**
Seleziona una categoria che descrive il contenuto da tradurre. Il valore predefinito è `General.`

   * **[!UICONTROL Scegli una lingua...]**
(Facoltativo) Selezionando una lingua per l&#39;archiviazione dei contenuti generati dagli utenti (UGC), i post di tutte le copie per lingua vengono visualizzati in un&#39;unica conversazione globale. Per convenzione, scegliere le impostazioni locali per la [lingua base](sites-console.md#translation) del sito Web. La scelta di `No Common Store` disabilita la traduzione globale. Per impostazione predefinita, la traduzione globale è disabilitata.

* Scheda **[!UICONTROL Assets]**: può lasciare come valori predefiniti.
* Seleziona **[!UICONTROL OK]**

#### Attivazione {#activation}

Il nuovo servizio cloud di integrazione della traduzione deve essere attivato nell’ambiente Publish. Se associata a un sito web, se non ancora attivata, il flusso di lavoro di attivazione richiede di pubblicare questa configurazione del servizio cloud quando viene pubblicata la pagina a cui è associata.

## Gestione delle impostazioni di traduzione {#managing-translation-settings}

>[!NOTE]
>
>**Lingua preferita**
>
>Quando si rileva se il post è in una lingua diversa da quella preferita, è necessario stabilire la lingua preferita del visitatore del sito.
>
>La lingua preferita è quella impostata nel profilo di un utente quando il visitatore del sito ha effettuato l’accesso e ha specificato una preferenza per la lingua.
>
>Quando il visitatore del sito è anonimo o non ha specificato una preferenza di lingua nel suo profilo, la lingua preferita è la lingua di base del modello della pagina.

### Preferenza utente {#user-preference}

#### Profilo utente {#user-profile}

Tutti i siti community forniscono un profilo utente che i membri che hanno effettuato l&#39;accesso possono modificare per identificarsi nella community e impostare le proprie preferenze.

Ad esempio, puoi scegliere di visualizzare sempre i contenuti della community nella lingua che preferisci. Per impostazione predefinita, l&#39;impostazione non è impostata e viene utilizzata per impostazione predefinita l&#39;impostazione di sistema. L&#39;utente può modificare l&#39;impostazione su On o Off per ignorare l&#39;impostazione di sistema.

Quando le pagine vengono tradotte automaticamente nella lingua preferita dell’utente, l’interfaccia utente per la visualizzazione del testo originale e il miglioramento della traduzione rimane disponibile.

![profilo-utente](assets/translation-integration4.png)

### Impostazione sito community {#community-site-setting}

Quando si crea un sito community, è possibile abilitare e configurare l’opzione di traduzione. L’impostazione di traduzione è attiva per il contenuto che i visitatori anonimi del sito possono visualizzare, ma è bypassata dall’impostazione del profilo dell’utente.
