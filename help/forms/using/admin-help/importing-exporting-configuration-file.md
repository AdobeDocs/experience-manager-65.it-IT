---
title: Importazione ed esportazione del file di configurazione
seo-title: Importazione ed esportazione del file di configurazione
description: Scoprite come importare ed esportare il file di configurazione per modificare le preferenze del server o configurare un'altra istanza di prodotto AEM moduli.
seo-description: Scoprite come importare ed esportare il file di configurazione per modificare le preferenze del server o configurare un'altra istanza di prodotto AEM moduli.
uuid: 32e8a709-2d7c-4740-9533-d53aa751bc58
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c1636537-f7dc-48d8-a3f0-9052bcd28b62
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---


# Importazione ed esportazione del file di configurazione {#importing-and-exporting-the-configuration-file}

Utilizzare la pagina Configurazione manuale per scaricare una copia delle impostazioni di configurazione in formato XML. Le impostazioni di questo file controllano tutte le preferenze del server. Potete quindi modificare il file e caricarlo nuovamente sul server. È inoltre possibile utilizzare il file per configurare un&#39;altra istanza di prodotto AEM moduli.

Per evitare rischi legati alla sicurezza, il valore della password di binding per il server di directory non è incluso in un file di configurazione esportato. Aggiornare la password nel file XML prima di importare il file in un nuovo sistema.

>[!NOTE]
>
>L&#39;importazione del file di configurazione consente di riconfigurare AEM moduli in base alle informazioni contenute nel file. Solo un amministratore di sistema o un consulente di servizi professionali che abbia familiarità con il prodotto AEM dei moduli e con XML deve considerare la possibilità di modificare il file di configurazione. Potrebbero dover modificare il file di configurazione, ad esempio per riconfigurare un&#39;impostazione danneggiata.

**Esportare le informazioni di configurazione**

1. In Admin Console, fai clic su Settings (Impostazioni) > User Management (Gestione utente) > Configuration (Configurazione) > Import And Export Configuration Files (Importa ed esporta file di configurazione).
1. Fate clic su Esporta. Se si utilizza Microsoft Internet Explorer, viene richiesto di specificare un percorso in cui salvare il file. Se utilizzate Firefox, il file viene salvato sul desktop.

**Importare le informazioni di configurazione**

1. In Admin Console, fai clic su Settings (Impostazioni) > User Management (Gestione utente) > Configuration (Configurazione) > Import And Export Configuration Files (Importa ed esporta file di configurazione).
1. Fate clic su Sfoglia per trovare il file di configurazione, fate clic su Importa, quindi fate clic su OK.

