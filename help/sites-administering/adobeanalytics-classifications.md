---
title: Classificazioni Adobe
description: Scopri come utilizzare le classificazioni Adobe per esportare i dati delle classificazioni in Adobe Analytics.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: 0e675ce8-ba3b-481d-949e-0c85c97054d2
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 5%

---

# Classificazioni Adobe{#adobe-classifications}

Adobe Classificazioni esporta i dati delle classificazioni in [Adobe Analytics](/help/sites-administering/adobeanalytics.md) in modo programmato. L&#39;esportatore è l&#39;attuazione di un **com.adobe.cq.scheduled.exporter.Exporter**.

Per configurarlo:

1. Utilizzo di **Navigazione**, seleziona **Strumenti**, **Cloud Service**, quindi **Cloud Service legacy**.
1. Scorri fino a **Adobe Analytics** e seleziona **Mostra configurazioni**.
1. Fai clic su **[+]** accanto alla configurazione di Adobe Analytics.

1. In **Crea framework** finestra di dialogo:

   * Specificare un **Titolo**.
   * Facoltativamente, puoi specificare **Nome**, per il nodo che memorizza i dettagli del framework nell’archivio.
   * Seleziona **Classificazioni Adobe Analytics**

   E fai clic su **Crea**.

   ![Finestra di dialogo Crea framework](assets/aa-25.png)

1. Il **Impostazioni classificazioni** viene visualizzata una finestra di dialogo per la modifica.

   ![Finestra di dialogo Impostazioni classificazioni](assets/aa-classifications-settings.png)

   Le proprietà includono:

   | **Campo** | **Descrizione** |
   |---|---|
   | Abilitato | Seleziona **Sì** per abilitare le impostazioni Adobe Classificazioni. |
   | Sovrascrivi in caso di conflitto | Seleziona **Sì** per sovrascrivere eventuali conflitti di dati. Per impostazione predefinita, è impostato su **No**. |
   | Elimina elementi elaborati | Se impostato su **Sì**, elimina i nodi elaborati dopo l&#39;esportazione. Il valore predefinito è **Falso**. |
   | Descrizione processo esportazione | Immettere una descrizione per il job Classificazioni di Adobe. |
   | E-mail di notifica | Immetti un indirizzo e-mail per la notifica Classificazioni di Adobe. |
   | Suite per report | Immetti la suite di rapporti per la quale eseguire il processo di importazione. |
   | Set di dati | Immetti l’ID di relazione del set di dati per cui eseguire il processo di importazione. |
   | Trasformazione | Dal menu a discesa, seleziona un’implementazione di trasformatore. |
   | Origine dati | Passa al percorso del contenitore dati. |
   | Esporta pianificazione | Seleziona la pianificazione per l’esportazione. Il valore predefinito è ogni 30 minuti. |

1. Clic **OK** per salvare le impostazioni.

## Modifica delle dimensioni di pagina {#modifying-page-size}

I record vengono elaborati nelle pagine. Per impostazione predefinita, Classificazioni di Adobe crea pagine con dimensioni pari a 1000.

Una pagina può avere dimensioni 25000 al massimo, per definizione in Classificazioni di Adobe e può essere modificata dalla console Felix. Durante l’esportazione, Adobe Classifications blocca il nodo di origine per impedire modifiche simultanee. Il nodo viene sbloccato dopo l’esportazione, in caso di errore o quando la sessione viene chiusa.

Per modificare le dimensioni della pagina:

1. Passa alla console OSGI all’indirizzo **https://&lt;host>:&lt;port>/system/console/configMgr** e seleziona **Adobe Esportatore classificazioni AEM**.

   ![aa-26](assets/aa-26.png)

1. Aggiornare il **Esporta dimensioni pagina** come richiesto, quindi fai clic su **Salva**.

## SAINTDefaultTransformer {#saintdefaulttransformer}

>[!NOTE]
>
>Adobe Classifications era precedentemente noto come SAINT Exporter.

Un esportatore può utilizzare un trasformatore per trasformare i dati di esportazione in un formato specifico. Ad Adobe Classificazioni, una sottointerfaccia `SAINTTransformer<String[]>` È stata fornita l’implementazione dell’interfaccia del trasformatore. Questa interfaccia viene utilizzata per limitare il tipo di dati a `String[]` che viene utilizzato dall’API SAINT e che dispone di un’interfaccia marker per trovare tali servizi da selezionare.

Nell&#39;implementazione predefinita di SAINTDefaultTransformer, le risorse figlie dell&#39;origine di esportazione vengono considerate come record con nomi di proprietà come chiavi e valori di proprietà come valori. Il **Chiave** viene aggiunta automaticamente come prima colonna; il suo valore sarà il nome del nodo. Proprietà con namespace (contenenti `:`) vengono ignorati.

*Struttura nodo:*

* id-classification `nt:unstructured`

   * 1 `nt:unstructured`

      * Product = My Product Name (String)
      * Prezzo = 120,90 (stringa)
      * Dimensione = M (Stringa)
      * Colore = nero (stringa)
      * Colore^Codice = 101 (stringa)

**Intestazione e registrazione SAINT:**

| **Chiave** | **Prodotto** | **Prezzo** | **Dimensione** | **Colore** | **Colore^Codice** |
|---|---|---|---|---|---|
| 1 | Nome prodotto | 120,90 | M | black | 101 |

Le proprietà includono:

<table>
 <tbody>
  <tr>
   <td><strong>Percorso proprietà</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>trasformatore</td>
   <td>Nome di classe di un'implementazione di SAINTTransformer</td>
  </tr>
  <tr>
   <td>e-mail</td>
   <td>Indirizzo e-mail di notifica.</td>
  </tr>
  <tr>
   <td>suite di rapporti</td>
   <td>ID suite di rapporti per cui eseguire il processo di importazione. </td>
  </tr>
  <tr>
   <td>set di dati</td>
   <td>ID relazione set di dati per cui eseguire il processo di importazione. </td>
  </tr>
  <tr>
   <td>descrizione</td>
   <td>Descrizione del processo. <br /> </td>
  </tr>
  <tr>
   <td>sovrascrivi</td>
   <td>Contrassegno flag per sovrascrivere i conflitti di dati. Il valore predefinito è <strong>false</strong>.</td>
  </tr>
  <tr>
   <td>divisioni di controllo</td>
   <td>Contrassegno flag per verificare la compatibilità delle suite di rapporti. Il valore predefinito è <strong>true</strong>.</td>
  </tr>
  <tr>
   <td>deleteprocessed</td>
   <td>Flag per eliminare i nodi elaborati dopo l’esportazione. Il valore predefinito è <strong>false</strong>.</td>
  </tr>
 </tbody>
</table>

## Automazione dell’esportazione di classificazioni di Adobi {#automating-adobe-classifications-export}

Puoi creare un flusso di lavoro personalizzato in modo che tutte le nuove importazioni avviino il flusso di lavoro per creare i dati appropriati e correttamente strutturati in **/var/export/** in modo che possa essere esportato in Classificazioni Adobe.
