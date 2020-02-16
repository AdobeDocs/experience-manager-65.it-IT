---
title: Classificazioni Adobe
seo-title: Classificazioni Adobe
description: Ulteriori informazioni sulle classificazioni Adobe.
seo-description: Ulteriori informazioni sulle classificazioni Adobe.
uuid: 57fb59f4-da90-4fe7-a5b1-c3bd51159a16
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 6787511a-2ce0-421a-bcfb-90d5f32ad35e
translation-type: tm+mt
source-git-commit: a833a34bbeb938c72cdb851a46b2ffd97aee9f6d

---


# Adobe Classifications{#adobe-classifications}

Adobe Classifications esporta i dati di classificazione in [Adobe Analytics](/help/sites-administering/adobeanalytics.md) in modo pianificato. L&#39;esportatore è un&#39;implementazione di un **com.adobe.cq.scheduled.export.Exporter**.

Per configurare:

1. Andate da **Strumenti, Servizi cloud** alla sezione **Adobe Analytics** .
1. Aggiungete una nuova configurazione. Vedrai che il modello di configurazione delle classificazioni **di** Adobe Analytics viene visualizzato sotto la configurazione di **Adobe Analytics Framework** . Specificate un **Titolo** e un **Nome** come richiesto:

   ![aa-25](assets/aa-25.png)

1. Fate clic su **Crea** per configurare le impostazioni.

   ![chlimage_1](assets/chlimage_1a.png)

   Le proprietà includono quanto segue:

   | **Campo** | **Descrizione** |
   |---|---|
   | Abilitato | Selezionate **Sì** per abilitare le impostazioni Classificazioni Adobe. |
   | Sovrascrivi in caso di conflitto | Selezionare **Sì** per sovrascrivere eventuali collisioni di dati. Per impostazione predefinita, è impostato su **No**. |
   | Elimina elementi elaborati | Se è impostato su **Sì**, elimina i nodi elaborati dopo l’esportazione. Il valore predefinito è **False**. |
   | Descrizione processo esportazione | Inserite una descrizione per il processo Adobe Classifications. |
   | E-mail di notifica | Immettete un indirizzo e-mail per la notifica di classificazione Adobe. |
   | Suite di rapporti | Immettere la suite di rapporti per la quale eseguire il processo di importazione. |
   | Set di dati | Immettere l&#39;ID della relazione del set di dati per cui eseguire il processo di importazione. |
   | Trasformazione | Dal menu a discesa, selezionate un&#39;implementazione del trasformatore. |
   | Sorgente dati | Individuare il percorso del contenitore di dati. |
   | Esporta pianificazione | Selezionare la pianificazione per l&#39;esportazione. Il valore predefinito è ogni 30 minuti. |

1. Click **OK** to save your settings.

## Modifica delle dimensioni di pagina {#modifying-page-size}

I record vengono elaborati nelle pagine. Per impostazione predefinita, in Adobe Classifications vengono create delle pagine con una dimensione di pagina pari a 1000.

Una pagina può avere una dimensione massima di 25000, per definizione nelle classificazioni Adobe e può essere modificata dalla console Felix. Durante l&#39;esportazione, Adobe Classifications blocca il nodo di origine per evitare modifiche simultanee. Il nodo viene sbloccato dopo l’esportazione, in caso di errore o quando la sessione viene chiusa.

Per modificare le dimensioni della pagina:

1. Andate alla console OSGI all&#39;indirizzo **https://&lt;host>:&lt;porta>/system/console/configMgr** e selezionate **Adobe AEM Classifications Exporter**.

   ![aa-26](assets/aa-26.png)

1. Aggiornate le dimensioni **di pagina** Esporta come necessario, quindi fate clic su **Salva**.

## SAINTDefaultTransformer {#saintdefaulttransformer}

>[!NOTE]
>
>Le classificazioni Adobe erano precedentemente denominate SAINT Exporter.

Un esportatore può usare un trasformatore per trasformare i dati di esportazione in un formato specifico. Per le classificazioni Adobe, è stata fornita una sottointerfaccia `SAINTTransformer<String[]>` che implementa l&#39;interfaccia Transformer. Questa interfaccia è utilizzata per limitare il tipo di dati `String[]` che viene utilizzato dall&#39;API SAINT e per avere un&#39;interfaccia di marker per la ricerca di tali servizi per la selezione.

Nell&#39;implementazione predefinita SAINTDefaultTransformer, le risorse figlio dell&#39;origine esportatore vengono trattate come record con nomi di proprietà come chiavi e valori di proprietà come valori. La colonna **Tasto** viene aggiunta automaticamente come prima colonna; il suo valore sarà il nome del nodo. Le proprietà con nome (contenenti `:`) non vengono prese in considerazione.

*Struttura nodo:*

* id-Classification `nt:unstructured`

   * 1 `nt:unstructured`

      * Prodotto = Nome Prodotto Personale (Stringa)
      * Prezzo = 120,90 (Stringa)
      * Dimensioni = M (String)
      * Colore = nero (String)
      * Color^Code = 101 (String)

**Intestazione e record SAINT:**

| **Chiave** | **Prodotto** | **Prezzo** | **Dimensione** | **Colore** | **Colore^Code** |
|---|---|---|---|---|---|
| 1 | Nome prodotto personale | 120.90 | M | black | 101 |

Le proprietà includono quanto segue:

<table>
 <tbody>
  <tr>
   <td><strong>Percorso proprietà</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>trasformatore</td>
   <td>Un nome di classe di un'implementazione SAINTTransformer</td>
  </tr>
  <tr>
   <td>e-mail</td>
   <td>Indirizzo e-mail notifica.</td>
  </tr>
  <tr>
   <td>reportsuites</td>
   <td>ID suite di rapporti per cui eseguire il processo di importazione. </td>
  </tr>
  <tr>
   <td>dataset</td>
   <td>ID relazione set di dati per cui eseguire il processo di importazione. </td>
  </tr>
  <tr>
   <td>descrizione</td>
   <td>Descrizione del processo. <br /> </td>
  </tr>
  <tr>
   <td>sovrascrivi</td>
   <td>Flag per sovrascrivere le collisioni di dati. Il valore predefinito è <strong>false</strong>.</td>
  </tr>
  <tr>
   <td>divisioni di controllo</td>
   <td>Flag per verificare la compatibilità delle suite di rapporti. Default is <strong>true</strong>.</td>
  </tr>
  <tr>
   <td>deleteprocessed</td>
   <td>Flag per eliminare i nodi elaborati dopo l'esportazione. Il valore predefinito è <strong>false</strong>.</td>
  </tr>
 </tbody>
</table>

## Automatizzazione dell&#39;esportazione delle classificazioni Adobe {#automating-adobe-classifications-export}

Potete creare un flusso di lavoro personalizzato, in modo che qualsiasi nuova importazione avvii il flusso di lavoro per creare i dati appropriati e strutturati correttamente in **/var/export/** in modo che possano essere esportati in Classificazioni Adobe.
