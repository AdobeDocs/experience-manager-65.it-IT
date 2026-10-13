---
title: Scegliere un tipo di persistenza per un’installazione di AEM Forms
description: Scegli con saggezza un tipo di persistenza. Consente di creare un ambiente AEM Forms efficiente e scalabile.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
role: Admin
exl-id: 621fe107-f4ac-42b1-8c7b-8abbcaac7380
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Foundation Components
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 7da902b6-fe94-5180-8e7c-f6d1e38d01d5
    internal-label: Foundation Components
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 6%
---
# Scegliere un tipo di persistenza per un’installazione di AEM Forms {#choosing-a-persistence-type-for-an-aem-forms-installation}

Scegli con saggezza un tipo di persistenza. Consente di creare un ambiente AEM Forms efficiente e scalabile.

La persistenza è il metodo per archiviare il contenuto negli archivi fisici. Definisce la struttura effettiva dei dati e il relativo meccanismo di archiviazione. I microKernel fungono da gestori di persistenza in AEM Forms. AEM Forms supporta la persistenza (MicroKernals) di tipo TarMK, MongoMK e RDBMK. Puoi scegliere un tipo di persistenza per AEM Forms a seconda dello scopo e del tipo di distribuzione (server singolo, farm o cluster) di un’istanza AEM Forms.

>[!NOTE]
>
>LiveCycle ES4 SP1 utilizza la persistenza TarPM per archiviare il contenuto.

La tabella seguente elenca tutti i tipi di persistenza supportati e i vari parametri che consentono di scegliere un tipo di persistenza per l’ambiente:

<table>
 <tbody>
  <tr>
   <th><strong>Tipo di installazione / Costo</strong></th>
   <th><strong>TarMK</strong></th>
   <th><strong>MongoMk</strong></th>
   <th><strong>RDBMK</strong></th>
  </tr>
  <tr>
   <th><strong>Configurazione autonoma</strong></th>
   <td>Supportato<br /> </td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <th><strong>Cluster Setup</strong></th>
   <td>Non supportato</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <th><strong>Costo licenza</strong></th>
   <td>Incluso in AEM </td>
   <td>È richiesta una licenza separata</td>
   <td>È richiesta una licenza separata</td>
  </tr>
 </tbody>
</table>

TarMK è progettato per garantire prestazioni elevate, mentre MongoMK e RDBMK sono progettati per offrire scalabilità. Adobe consiglia vivamente TarMK come tecnologia di persistenza predefinita per tutti gli scenari di distribuzione di AEM Forms, sia per le istanze Author che Publish, ad eccezione dei casi d&#39;uso descritti nella sezione [Scelta di Mongo o di un microkernel di database relazionale su TarMK](#p-choosing-mongo-or-a-relational-database-microkernel-over-tarmk-p).

Per un elenco dei microkernel supportati, consulta [AEM Forms sui requisiti tecnici OSGi](/help/sites-deploying/technical-requirements.md) o [AEM Forms sulle combinazioni di piattaforme supportate da JEE](/help/forms/using/aem-forms-jee-supported-platforms.md) articoli.

## Scelta di Mongo o di un microkernel di database relazionale su TarMK {#choosing-mongo-or-a-relational-database-microkernel-over-tarmk}

Un ambiente AEM Forms scalabile (cluster) è un set di due o più istanze di authoring attive configurate orizzontalmente. Se un singolo server, che supporta tutte le attività di authoring simultanee, non è più sostenibile, è possibile scegliere di eseguire più istanze di authoring.

Per un ambiente AEM Forms scalabile (cluster) su JEE sono supportati solo i tipi di persistenza MongoMK e RDBMK. Il numero di server o le dimensioni dell&#39;ambiente scalabile variano a seconda dell&#39;installazione. Per un elenco di considerazioni ed esempi, vedere l&#39;articolo [Distribuzioni consigliate](/help/sites-deploying/recommended-deploys.md) e/o [Architettura e topologie di distribuzione per AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md). È inoltre possibile contattare il supporto AEM Forms per informazioni dettagliate sulla pianificazione della capacità per AEM Forms con RDBMK e TarMK.
