---
title: Esecuzione di AEM moduli in modalità di manutenzione
seo-title: Esecuzione di AEM moduli in modalità di manutenzione
description: La modalità di manutenzione è utile per eseguire attività quali l'applicazione di patch a un DSC, l'aggiornamento AEM moduli o l'applicazione di un service pack. Ulteriori informazioni sull'esecuzione AEM moduli in modalità di manutenzione.
seo-description: La modalità di manutenzione è utile per eseguire attività quali l'applicazione di patch a un DSC, l'aggiornamento AEM moduli o l'applicazione di un service pack. Ulteriori informazioni sull'esecuzione AEM moduli in modalità di manutenzione.
uuid: 9aa3be20-f17e-4384-b4ce-daaee2898c96
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 94047c12-ba3d-457a-954f-e035c7cc3ecd
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---


# Esecuzione AEM moduli in modalità di manutenzione {#running-aem-forms-in-maintenance-mode}

La modalità di manutenzione è utile per eseguire attività quali l&#39;applicazione di patch a un DSC, l&#39;aggiornamento AEM moduli o l&#39;applicazione di un service pack.

Evitare di richiamare processi mentre il server è in modalità di manutenzione. Questo è ciò che accade se un processo viene richiamato mentre il server è in modalità di manutenzione:

* Se il processo ha una durata prolungata, viene aggiunto al database dei processi, ma non viene avviato. Quando si esce dalla modalità di manutenzione, AEM moduli elabora i processi di lunga durata nella coda, anche se il server è stato riavviato in modalità manutenzione.
* Se il processo è di breve durata, viene elaborato immediatamente.

**Mettere AEM moduli in modalità di manutenzione**

1. In un browser Web, immettete:

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=pause&user=[administrator username]&password=[password]`

   Nella finestra del browser viene visualizzato un messaggio di tipo &quot;ora in pausa&quot;.

   >[!NOTE]
   >
   >Se si arresta il server mentre è in modalità di manutenzione, al successivo riavvio il server rimarrà in modalità manutenzione. È necessario disattivare la modalità di manutenzione al termine delle attività di manutenzione.

**Verificare se AEM moduli sono in esecuzione in modalità di manutenzione**

1. In un browser Web, immettete:

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=isPaused&user=[administrator username]&password=[password]`

   Lo stato viene visualizzato nella finestra del browser. Lo stato &quot;true&quot; indica che il server è in esecuzione in modalità manutenzione, mentre &quot;false&quot; indica che il server non è in modalità manutenzione.

**Disattivazione della modalità di manutenzione**

1. In un browser Web, immettete:

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=resume&user=[administrator username]&password=[password]`

   Nella finestra del browser viene visualizzato un messaggio di tipo &quot;ora in esecuzione&quot;.

