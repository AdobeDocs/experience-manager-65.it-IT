---
title: Traduzione di contenuti generati dall'utente
seo-title: Traduzione di contenuti generati dall'utente
description: Funzionamento della funzione di traduzione
seo-description: Funzionamento della funzione di traduzione
uuid: 7ee3242c-2aca-4787-a60d-b807161401ad
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: bfaf80c5-448b-47fb-9f22-57ee0eb169b2
translation-type: tm+mt
source-git-commit: b29945dc73e85504cd42102eafb9e2bf6198c9cc
workflow-type: tm+mt
source-wordcount: '1117'
ht-degree: 1%

---


# Traduzione di contenuti generati dall&#39;utente {#translating-user-generated-content}

La funzione di traduzione per  AEM Communities estende il concetto di [traduzione di contenuti di pagina](../../help/sites-administering/translation.md) ai contenuti generati dall&#39;utente (UGC) inviati a siti community tramite [social component framework (SCF) components](scf.md).

La traduzione di UGC consente ai visitatori e ai membri del sito di sperimentare una comunità globale rimuovendo le barriere linguistiche.

Ad esempio, supponete:

* Un membro francese ha pubblicato una ricetta in francese nel forum della comunità di un sito web di cucina multinazionale.
* Un altro membro del Giappone utilizza la funzione di traduzione per attivare la traduzione della ricetta dal francese al giapponese.
* Dopo aver letto la ricetta in giapponese, il membro giapponese ha poi pubblicato un commento in giapponese.
* Il membro francese utilizza la funzione di traduzione per tradurre il commento giapponese in francese.
* Comunicazione globale.

## Panoramica {#overview}

Questa sezione della documentazione descrive in modo specifico come il servizio di traduzione funziona con UGC, supponendo che sia chiaro come connettersi AEM a un [provider di servizi di traduzione](../../help/sites-administering/translation.md#connectingtoatranslationserviceprovider) e integrare tale servizio in un sito Web configurando un [framework di integrazione di traduzione](../../help/sites-administering/tc-tic.md).

Quando un provider di servizi di traduzione è associato al sito, ogni copia della lingua del sito mantiene i propri thread di UGC pubblicati tramite componenti SCF, come commenti.

Quando un framework di integrazione della traduzione è configurato in aggiunta al provider di servizi di traduzione, è possibile per ogni copia del sito condividere un singolo thread di UGC, fornendo così la comunicazione globale tra le copie della lingua. Invece di un thread di discussione segregato per lingua, l&#39; [archivio condiviso globale configurato](#global-translation-of-ugc) consente all&#39;intero thread di essere visibile indipendentemente dalla lingua in cui viene visualizzato. Inoltre, è possibile configurare più configurazioni di integrazione delle traduzioni specificando diversi store condivisi globali per un gruppo logico di partecipanti globali, ad esempio per regioni.

## Servizio di traduzione predefinito {#the-default-translation-service}

 AEM Communities include una [licenza di prova](../../help/sites-administering/tc-msconf.md#microsoft-translator-trial-license) per un [servizio di traduzione predefinito](../../help/sites-administering/tc-msconf.md) abilitato per diverse lingue.

Quando [si crea un sito community](sites-console.md), il servizio di traduzione predefinito viene attivato quando `Allow Machine Translation` viene selezionato dal sottopannello [TRANSLATION](sites-console.md#translation).

>[!CAUTION]
>
>Il servizio di traduzione predefinito è solo per la dimostrazione.
>
>Per un sistema di produzione, è necessario un servizio di traduzione con licenza. In caso contrario, il servizio di traduzione predefinito deve essere [disattivato](../../help/sites-administering/tc-msconf.md#microsoft-translator-trial-license-geometrixx-outdoors).

## Traduzione globale di UGC {#global-translation-of-ugc}

Quando un sito Web contiene più copie [della lingua](../../help/sites-administering/tc-prep.md), il servizio di traduzione predefinito non riconosce che l&#39;UGC immesso in un sito può essere correlato all&#39;UGC immesso in un altro sito, come quando l&#39;UGC viene, essenzialmente, generato dallo stesso componente (la copia della lingua della pagina contenente il componente).

È simile a gruppi di persone che discutono di un argomento ignaro dei commenti fatti in gruppi diversi dal proprio, rispetto a tutti in un grande gruppo che partecipa a una conversazione.

Se si desidera &quot;una conversazione di gruppo&quot;, è possibile abilitare la traduzione globale in un sito Web con più copie in lingua, in modo che l’intero thread sia visibile indipendentemente dalla copia in lingua visualizzata.

Ad esempio, se un forum è stato creato sul sito di base, le copie della lingua create e la traduzione globale è stata attivata, un argomento pubblicato nel forum creato in una copia della lingua verrà visualizzato in tutte le copie della lingua. Lo stesso vale per tutte le risposte, indipendentemente dalla lingua in cui è stata inserita la copia della risposta. Il risultato sarebbe che l&#39;argomento e l&#39;intero thread di risposte sarebbero visibili, indipendentemente dalla lingua in cui l&#39;argomento viene visualizzato nella copia dell&#39;argomento.

>[!CAUTION]
>
>Qualsiasi UGC esistente prima della traduzione globale non è più visibile.
>
>Sebbene l&#39;UGC sia ancora nello [store comune](working-with-srp.md), si trova nel percorso UGC specifico per la lingua, mentre il nuovo contenuto, aggiunto dopo la configurazione della traduzione globale, viene recuperato dal percorso dello store condiviso globale.
>
>Non è disponibile uno strumento di migrazione per spostare o unire contenuto specifico della lingua nello store condiviso globale.

### Configurazione integrazione traduzione {#translation-integration-configuration}

Per creare una nuova integrazione della traduzione, che integra un connettore del servizio di traduzione con il sito Web nell&#39;istanza di creazione:

* Accesso come amministratore
* Dal [menu principale](Http://localhost:4502/)
* Selezionare **[!UICONTROL Strumenti]**
* Selezionare **[!UICONTROL Operazioni]**
* Selezionare **[!UICONTROL Cloud]**
* Selezionare **[!UICONTROL Cloud Services]**
* Scorri verso il basso fino a **[!UICONTROL Integrazione traduzione]**

   ![traduzione-integrazione](assets/translation-integration.png)

* Selezionare **[!UICONTROL Mostra configurazioni]**

   ![show-configuration](assets/translation-integration1.png)

* Seleziona l&#39;icona `[+]` accanto a **[!UICONTROL Configurazioni disponibili]** per creare una nuova configurazione

#### Finestra di dialogo Crea configurazione {#create-configuration-dialog}

![create-configuration](assets/translation-integration2.png)

* **[!UICONTROL Configurazione elemento padre]**

   (Obbligatorio) In genere lasciate impostato il valore predefinito. Il valore predefinito è `/etc/cloudservices/translation`.

* **[!UICONTROL Titolo]**

   (Obbligatorio) Immettete un titolo di visualizzazione di vostra scelta. Nessun valore predefinito.

* **[!UICONTROL Nome]**

   (Facoltativo) Immettete un nome per la configurazione. Il valore predefinito è un nome di nodo basato sul titolo.

* Seleziona **[!UICONTROL Crea]**

#### Finestra di dialogo Configurazione traduzione {#translation-config-dialog}

![configuration-dialog](assets/translation-integration3.png)

Per istruzioni dettagliate, vedere [Creazione di una configurazione di integrazione della traduzione](../../help/sites-administering/tc-tic.md#creating-a-translation-integration-configuration)

* **** Sitestab: può essere lasciato come predefinito.

* **** Comuni:
   * **[!UICONTROL Provider]**
di traduzione: selezionate il provider di traduzione dall&#39;elenco a discesa. Il valore predefinito è 
`microsoft`, il servizio di prova.

   * **[!UICONTROL Contenuto]**
Categoria: selezionate una categoria che descrive il contenuto da convertire. Il valore predefinito è 
`General.`

   * **[!UICONTROL Scegliere Un&#39;Impostazione Internazionale...]**
(Facoltativo) Selezionando una lingua per la memorizzazione UGC, i post di tutte le copie della lingua verranno visualizzati in un&#39;unica conversazione globale. Per convenzione, scegliete le impostazioni internazionali per la [lingua di base](sites-console.md#translation) del sito Web. Se si sceglie `No Common Store`, la traduzione globale verrà disabilitata. Per impostazione predefinita, la traduzione globale è disabilitata.

* **** Assetstab: può essere lasciato come predefinito.
* Selezionare **[!UICONTROL OK]**

#### Attivazione {#activation}

Il nuovo servizio cloud per l’integrazione della traduzione dovrà essere attivato nell’ambiente di pubblicazione. Se associato a un sito Web, se non ancora attivato, il flusso di lavoro di attivazione richiederà di pubblicare la configurazione del servizio cloud quando la pagina a cui è associato viene pubblicata.

## Gestione delle impostazioni di traduzione {#managing-translation-settings}

>[!NOTE]
>
>**Lingua preferita**
>
>Al fine di rilevare se il post si trova in una lingua diversa da quella preferita, è necessario stabilire la lingua preferita del visitatore del sito.
>
>La lingua preferita è la preferenza della lingua impostata nel profilo di un utente, quando il visitatore del sito ha effettuato l’accesso e ha specificato una preferenza per la lingua.
>
>Quando il visitatore del sito è anonimo o non ha specificato una preferenza di lingua nel suo profilo, la lingua preferita è la lingua di base del modello di pagina.

### Preferenze utente {#user-preference}

#### Profilo utente {#user-profile}

Tutti i siti community forniscono un profilo utente che può essere modificato per identificarsi nella community e impostarne le preferenze.

Un&#39;impostazione di questo tipo consiste nel decidere se visualizzare o meno sempre il contenuto della community nella lingua preferita. Per impostazione predefinita, l&#39;impostazione non è impostata e viene impostata per impostazione predefinita sull&#39;impostazione del sistema. L&#39;utente può modificare l&#39;impostazione su Attivato o Disattivato, ignorando l&#39;impostazione del sistema.

Quando le pagine vengono tradotte automaticamente nella lingua preferita dall’utente, l’interfaccia utente per la visualizzazione del testo originale e il miglioramento della traduzione è ancora disponibile.

![user-profile](assets/translation-integration4.png)

### Impostazione sito community {#community-site-setting}

Quando viene creato un sito community, l&#39;opzione di traduzione può essere abilitata e configurata. L&#39;impostazione di traduzione è attiva per il contenuto che i visitatori anonimi del sito possono visualizzare, ma viene ignorata dalle impostazioni del profilo dell&#39;utente.
