---
title: Esecuzione di moduli AEM in modalità manutenzione
description: La modalità di manutenzione è utile quando si eseguono attività quali l’applicazione di patch a un DSC, l’aggiornamento dei moduli AEM o l’applicazione di un service pack. Ulteriori informazioni sull’esecuzione dei moduli AEM in modalità di manutenzione.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 6f5ce18b-26b4-4c31-b48a-43ccbb3912f6
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# Esecuzione di moduli AEM in modalità manutenzione {#running-aem-forms-in-maintenance-mode}

La modalità di manutenzione è utile quando si eseguono attività quali l’applicazione di patch a un DSC, l’aggiornamento dei moduli AEM o l’applicazione di un service pack.

Evita di richiamare i processi mentre il server è in modalità di manutenzione. Questo è ciò che accade se un processo viene richiamato mentre il server è in modalità di manutenzione:

* Se il processo è di lunga durata, viene aggiunto al database dei processi, ma non viene avviato. Quando si esce dalla modalità di manutenzione, i moduli AEM elaborano i processi di lunga durata presenti nella coda, anche se il server è stato riavviato in modalità di manutenzione.
* Se il processo è di breve durata, viene elaborato immediatamente.

**Mettere i moduli AEM in modalità di manutenzione**

1. In un browser web, immetti:

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=pause&user=[administrator username]&password=[password]`

   Nella finestra del browser viene visualizzato il messaggio &quot;ora in pausa&quot;.

   >[!NOTE]
   >
   >Se si arresta il server mentre è in modalità di manutenzione, al riavvio il server è ancora in modalità di manutenzione. Disattivare la modalità di manutenzione al termine delle attività di manutenzione.

**Verifica se i moduli AEM sono in esecuzione in modalità di manutenzione**

1. In un browser web, immetti:

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=isPaused&user=[administrator username]&password=[password]`

   Lo stato viene visualizzato nella finestra del browser. Lo stato &quot;true&quot; indica che il server è in esecuzione in modalità di manutenzione, mentre &quot;false&quot; indica che il server non è in modalità di manutenzione.

**Disattiva modalità di manutenzione**

1. In un browser web, immetti:

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=resume&user=[administrator username]&password=[password]`

   Nella finestra del browser viene visualizzato il messaggio &quot;in esecuzione&quot;.
