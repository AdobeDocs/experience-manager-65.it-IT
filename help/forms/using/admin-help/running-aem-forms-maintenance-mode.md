---
title: Esecuzione di moduli AEM in modalità di manutenzione
seo-title: Esecuzione di moduli AEM in modalità di manutenzione
description: La modalità di manutenzione è utile per eseguire attività quali l’applicazione di patch a un DSC, l’aggiornamento dei moduli AEM o l’applicazione di un service pack. Ulteriori informazioni sull'esecuzione di moduli AEM in modalità di manutenzione.
seo-description: La modalità di manutenzione è utile per eseguire attività quali l’applicazione di patch a un DSC, l’aggiornamento dei moduli AEM o l’applicazione di un service pack. Ulteriori informazioni sull'esecuzione di moduli AEM in modalità di manutenzione.
uuid: 9aa3be20-f17e-4384-b4ce-daaee2898c96
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 94047c12-ba3d-457a-954f-e035c7cc3ecd
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Esecuzione di moduli AEM in modalità di manutenzione {#running-aem-forms-in-maintenance-mode}

La modalità di manutenzione è utile per eseguire attività quali l’applicazione di patch a un DSC, l’aggiornamento dei moduli AEM o l’applicazione di un service pack.

Evitare di richiamare processi mentre il server è in modalità manutenzione. Questo è ciò che accade se un processo viene richiamato mentre il server è in modalità di manutenzione:

* Se il processo ha una durata prolungata, viene aggiunto al database dei processi, ma non viene avviato. Quando si esce dalla modalità di manutenzione, AEM Forms elabora i processi di lunga durata nella coda, anche se il server è stato riavviato in modalità manutenzione.
* Se il processo è di breve durata, viene elaborato immediatamente.

**Mettere moduli AEM in modalità di manutenzione**

1. In un browser Web, immettete:

   `https://`*[nomehost ]*`:`*[porta]* nome utente `/dsc/servlet/DSCStartupServlet?maintenanceMode=pause&user=`*[amministratore ]*`&password=`*[password]*

   Nella finestra del browser viene visualizzato un messaggio di tipo &quot;ora in pausa&quot;.

   >[!NOTE]
   >
   >Se si arresta il server mentre è in modalità di manutenzione, al successivo riavvio il server rimarrà in modalità manutenzione. È necessario disattivare la modalità di manutenzione al termine delle attività di manutenzione.

**Verificare se i moduli AEM sono in esecuzione in modalità di manutenzione**

1. In un browser Web, immettete:

   `https://`*[nomehost]:[porta ]*nome utente`/dsc/servlet/DSCStartupServlet?maintenanceMode=isPaused&user=`*[]* amministratore `&password=`*[password ]*

   Lo stato viene visualizzato nella finestra del browser. Lo stato &quot;true&quot; indica che il server è in esecuzione in modalità manutenzione, mentre &quot;false&quot; indica che il server non è in modalità manutenzione.

**Disattiva modalità manutenzione**

1. In un browser Web, immettete:

   `https://`*[nomehost]:[porta ]*nome utente`/dsc/servlet/DSCStartupServlet?maintenanceMode=resume&user=`*[]* amministratore `&password=`*[password ]*

   Nella finestra del browser viene visualizzato un messaggio di tipo &quot;ora in esecuzione&quot;.

