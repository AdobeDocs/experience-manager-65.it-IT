---
title: Scelta di un tipo di persistenza per un'installazione di AEM Forms
seo-title: Scelta di un tipo di persistenza per un'installazione di AEM Forms
description: Scegliete un tipo di persistenza con cognizione di causa. Consente di creare un ambiente AEM Forms efficiente e scalabile.
seo-description: Scegliete un tipo di persistenza con cognizione di causa. Consente di creare un ambiente AEM Forms efficiente e scalabile.
uuid: 1c692502-5039-4757-9358-1772772b3904
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: a972fb35-38a7-4b83-99bd-6a6dddf8043b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Scelta di un tipo di persistenza per un&#39;installazione di AEM Forms {#choosing-a-persistence-type-for-an-aem-forms-installation}

Scegliete un tipo di persistenza con cognizione di causa. Consente di creare un ambiente AEM Forms efficiente e scalabile.

La persistenza è il metodo per memorizzare il contenuto negli archivi fisici. Definisce la struttura dati e il meccanismo di memorizzazione effettivi per i dati. I microkernel agiscono come persistence manager in AEM Forms. AEM Forms supporta la persistenza (MicroKernals) di tipo TarMK, MongoMK e RDBMK. È possibile scegliere un tipo di persistenza per AEM Forms a seconda dello scopo e del tipo di distribuzione (Server singolo, Fattoria o Cluster) di un&#39;istanza di AEM Forms.

>[!NOTE]
>
>LiveCycle ES4 SP1 utilizza la persistenza TarPM per memorizzare il contenuto.

Nella tabella seguente sono elencati tutti i tipi di persistenza supportati insieme a vari parametri per facilitare la scelta di un tipo di persistenza per l’ambiente:

<table>
 <tbody>
  <tr>
   <th><strong>Tipo di installazione / Costo</strong></th>
   <th><strong>TarMK</strong></th>
   <th><strong>MongoMk</strong></th>
   <th><strong>RDBMK</strong></th>
  </tr>
  <tr>
   <th><strong>Configurazione indipendente</strong></th>
   <td>Supportato<br /> </td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <th><strong>Configurazione cluster</strong></th>
   <td>Non supportato</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <th><strong>Costo licenza</strong></th>
   <td>Incluso in AEM </td>
   <td>Licenza separata richiesta</td>
   <td>Licenza separata richiesta</td>
  </tr>
 </tbody>
</table>

TarMK è progettato per le prestazioni, mentre MongoMK e RDBMK sono progettati per la scalabilità. Adobe consiglia vivamente TarMK come tecnologia di persistenza predefinita per tutti gli scenari di distribuzione di AEM Forms, sia per le istanze Author che per le istanze Publish, fatta eccezione per i casi di utilizzo descritti nella sezione [Scelta di Mongo o di un Microkernel di database relazionale su TarMK](#p-choosing-mongo-or-a-relational-database-microkernel-over-tarmk-p).

Per un elenco dei microkernel supportati, consultate [AEM Forms on OSGi Technical Requirements](/help/sites-deploying/technical-requirements.md) o [AEM Forms on JEE supported platform Combinations](/help/forms/using/aem-forms-jee-supported-platforms.md) articles (Moduli AEM su piattaforme supportate da JEE).

## Scelta di Mongo o di un microkernel di database relazionale su TarMK {#choosing-mongo-or-a-relational-database-microkernel-over-tarmk}

Un ambiente AEM Forms scalabile (cluster) è un insieme di due o più istanze di autori attivi configurate orizzontalmente. È possibile scegliere di eseguire più istanze di autore se un singolo server, che supporta tutte le attività di authoring simultanee, non è più sostenibile.

Solo i tipi di persistenza MongoMK e RDBMK sono supportati per un ambiente AEM Forms scalabile (cluster) in JEE. Il numero di server o le dimensioni dell&#39;ambiente scalabile variano per ogni installazione. Per un elenco di considerazioni ed esempi, consultate l&#39;articolo [consigliati Implementazioni](/help/sites-deploying/recommended-deploys.md) e/o topologie di [architettura e distribuzione per AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md) . È inoltre possibile contattare il supporto AEM Forms per informazioni dettagliate sulla pianificazione della capacità per AEM Forms con RDBMK e TarMK.
