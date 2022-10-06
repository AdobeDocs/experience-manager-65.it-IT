---
title: Classificazioni Adobe
seo-title: Adobe Classifications
description: Scopri le classificazioni di Adobe.
seo-description: Learn about Adobe Classifications.
uuid: 57fb59f4-da90-4fe7-a5b1-c3bd51159a16
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 6787511a-2ce0-421a-bcfb-90d5f32ad35e
exl-id: 0e675ce8-ba3b-481d-949e-0c85c97054d2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 7%

---

# Classificazioni Adobe{#adobe-classifications}

Adobe Classificazioni esporta dati di classificazione in [Adobe Analytics](/help/sites-administering/adobeanalytics.md) in modo programmato. L&#39;esportatore è l&#39;attuazione di un **com.adobe.cq.scheduled.export.Exporter**.

Per configurare quanto segue:

1. Utilizzo **Navigazione**, seleziona **Strumenti**, **Cloud Services**, quindi **Cloud Services legacy**.
1. Scorri fino a **Adobe Analytics** e seleziona **Mostra configurazioni**.
1. Fai clic sul pulsante **[+]** link accanto alla tua configurazione Adobe Analytics.

1. In **Crea framework** finestra di dialogo:

   * Specificare un **Titolo**.
   * Facoltativamente, puoi specificare la **Nome**, per il nodo che memorizza i dettagli del framework nell&#39;archivio.
   * Seleziona **Classificazioni Adobe Analytics**

   E fai clic su **Crea**.

   ![Finestra di dialogo Crea framework](assets/aa-25.png)

1. La **Impostazioni delle classificazioni** viene visualizzata la finestra di dialogo per la modifica.

   ![Finestra di dialogo Impostazioni classificazioni](assets/aa-classifications-settings.png)

   Le proprietà includono quanto segue:

   | **Campo** | **Descrizione** |
   |---|---|
   | Abilitato | Seleziona **Sì** per abilitare le impostazioni Adobe Classificazioni . |
   | Sovrascrivi in caso di conflitto | Seleziona **Sì** per sovrascrivere eventuali conflitti di dati. Per impostazione predefinita, è impostata su **No**. |
   | Elimina elementi elaborati | Se impostato su **Sì**, elimina i nodi elaborati dopo l’esportazione. Il valore predefinito è **False**. |
   | Descrizione processo esportazione | Immettere una descrizione per il processo Classificazioni Adobe. |
   | E-mail di notifica | Immetti un indirizzo e-mail per la notifica Classificazioni Adobe. |
   | Suite di rapporti | Immetti la suite di rapporti per la quale eseguire il processo di importazione. |
   | Set di dati | Immetti l’ID della relazione del set di dati per cui eseguire il processo di importazione. |
   | Trasformazione | Dal menu a discesa, seleziona un’implementazione di trasformazione. |
   | Sorgente dati | Passa al percorso del contenitore di dati. |
   | Esporta pianificazione | Selezionare la pianificazione per l&#39;esportazione. Il valore predefinito è ogni 30 minuti. |

1. Fai clic su **OK** per salvare le impostazioni.

## Modifica delle dimensioni della pagina {#modifying-page-size}

I record vengono elaborati nelle pagine. Per impostazione predefinita, in Classificazioni Adobe vengono create pagine con una dimensione di pagina pari a 1000.

Una pagina può avere una dimensione massima di 25000, per definizione nelle classificazioni di Adobe, e può essere modificata dalla console Felix. Durante l’esportazione, Classificazioni Adobe blocca il nodo di origine per evitare modifiche simultanee. Il nodo viene sbloccato dopo l’esportazione, per errore o quando la sessione viene chiusa.

Per modificare le dimensioni della pagina:

1. Passa alla console OSGI all’indirizzo **https://&lt;host>:&lt;port>/system/console/configMgr** e seleziona **Esportatore di classificazioni AEM Adobe**.

   ![aa-26](assets/aa-26.png)

1. Aggiorna **Esporta dimensioni pagina** in base alle esigenze, quindi fai clic su **Salva**.

## SAINTDefaultTransformer {#saintdefaulttransformer}

>[!NOTE]
>
>Classificazioni Adobe era precedentemente noto come Esportatore SAINT.

Un esportatore può utilizzare un trasformatore per trasformare i dati di esportazione in un formato specifico. Ad Adobe Classificazioni, una sottointerfaccia `SAINTTransformer<String[]>` è stata fornita l&#39;implementazione dell&#39;interfaccia di trasformazione. Questa interfaccia viene utilizzata per limitare il tipo di dati a `String[]` , utilizzato dall’API di SAINT e dotato di un’interfaccia marker per la ricerca di tali servizi da selezionare.

Nell&#39;implementazione predefinita SAINTDefaultTransformer, le risorse figlio dell&#39;origine dell&#39;esportatore vengono trattate come record con nomi di proprietà come chiavi e valori di proprietà come valori. La **Chiave** viene aggiunta automaticamente come prima colonna; il relativo valore sarà il nome del nodo. Proprietà con namespace (contenenti `:`) non vengono prese in considerazione.

*Struttura del nodo:*

* classificazione id `nt:unstructured`

   * 1 `nt:unstructured`

      * Product = My Product Name (Stringa)
      * Prezzo = 120,90 (Stringa)
      * Dimensione = M (Stringa)
      * Colore = nero (Stringa)
      * Colore^Codice = 101 (Stringa)

**Intestazione e record di SAINT:**

| **Chiave** | **Prodotto** | **Prezzo** | **Dimensione** | **Colore** | **Colore^Codice** |
|---|---|---|---|---|---|
| 1 | Nome del prodotto | 120,90 | M | black | 101 |

Le proprietà includono quanto segue:

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
   <td>Flag per sovrascrivere i conflitti tra dati. Il valore predefinito è <strong>false</strong>.</td>
  </tr>
  <tr>
   <td>divisioni</td>
   <td>Flag per verificare la compatibilità delle suite di rapporti. Il valore predefinito è <strong>true</strong>.</td>
  </tr>
  <tr>
   <td>cancella</td>
   <td>Flag per eliminare i nodi elaborati dopo l’esportazione. Il valore predefinito è <strong>false</strong>.</td>
  </tr>
 </tbody>
</table>

## Automazione dell’esportazione delle classificazioni di Adobe {#automating-adobe-classifications-export}

Puoi creare un flusso di lavoro personalizzato, in modo che qualsiasi nuova importazione avvii il flusso di lavoro per creare i dati appropriati e strutturati correttamente in **/var/export/** in modo che possa essere esportato in Classificazioni Adobi.
