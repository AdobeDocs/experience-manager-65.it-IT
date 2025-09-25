---
title: Esecuzione di AEM Forms in modalità manutenzione
description: La modalità manutenzione è utile quando esegui attività quali l’applicazione di patch a un DSC, l’aggiornamento di AEM Forms o l’applicazione di un service pack. Ulteriori informazioni sull’esecuzione di AEM Forms in modalità manutenzione.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 6f5ce18b-26b4-4c31-b48a-43ccbb3912f6
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: ht
source-wordcount: '256'
ht-degree: 100%

---

# Esecuzione di AEM Forms in modalità manutenzione {#running-aem-forms-in-maintenance-mode}

La modalità manutenzione è utile quando esegui attività quali l’applicazione di patch a un DSC, l’aggiornamento di AEM Forms o l’applicazione di un service pack.

Evita di richiamare i processi mentre il server è in modalità manutenzione. Questo è ciò che accade se richiami un processo mentre il server è in modalità manutenzione:

* Se il processo è di lunga durata, viene aggiunto al database dei processi, ma non viene avviato. Quando esci dalla modalità manutenzione, AEM Forms elabora i processi di lunga durata presenti nella coda, anche se il server è stato riavviato in modalità manutenzione.
* Se il processo è di breve durata, viene elaborato immediatamente.

**Mettere AEM Forms in modalità manutenzione**

1. In un browser web immetti:

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=pause&user=[administrator username]&password=[password]`

   Nella finestra del browser viene visualizzato il messaggio “in pausa”.

   >[!NOTE]
   >
   >Se arresti il server mentre è in modalità manutenzione, al riavvio il server è ancora in modalità manutenzione. Disattiva la modalità manutenzione al termine delle attività di manutenzione.

**Verificare se AEM Forms è in esecuzione in modalità manutenzione**

1. In un browser web immetti:

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=isPaused&user=[administrator username]&password=[password]`

   Lo stato viene visualizzato nella finestra del browser. Lo stato “vero” indica che il server è in esecuzione in modalità manutenzione, mentre “falso” indica che il server non è in modalità manutenzione.

**Disattivare la modalità manutenzione**

1. In un browser web immetti:

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=resume&user=[administrator username]&password=[password]`

   Nella finestra del browser viene visualizzato il messaggio “in esecuzione”.
