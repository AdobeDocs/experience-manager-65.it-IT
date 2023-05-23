---
title: Importazione ed esportazione del file di configurazione
seo-title: Importing and exporting the configuration file
description: Scopri come importare ed esportare il file di configurazione per modificare le preferenze del server o configurare un’altra istanza di prodotto di AEM forms.
seo-description: Learn how to import and export the configuration file in order to edit server preferences or configure another AEM forms product instance.
uuid: 32e8a709-2d7c-4740-9533-d53aa751bc58
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c1636537-f7dc-48d8-a3f0-9052bcd28b62
exl-id: 225dbeb5-a21c-4338-98c7-e10c32973721
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# Importazione ed esportazione del file di configurazione {#importing-and-exporting-the-configuration-file}

Utilizzare la pagina Configurazione manuale per scaricare una copia delle impostazioni di configurazione in formato XML. Le impostazioni di questo file controllano tutte le preferenze del server. Puoi quindi modificare il file e caricarlo nuovamente sul server. Puoi anche utilizzare il file per configurare un’altra istanza del prodotto AEM forms.

Per evitare rischi di protezione, il valore della password di associazione per il server delle directory non viene incluso in un file di configurazione esportato. Aggiornare la password nel file XML prima di importare il file in un nuovo sistema.

>[!NOTE]
>
>L’importazione del file di configurazione riconfigura i moduli AEM in base alle informazioni contenute nel file. Solo un amministratore di sistema o un consulente di servizi professionali che ha familiarità con il prodotto moduli AEM e con XML deve considerare la modifica del file di configurazione. Potrebbe essere necessario modificare il file di configurazione, ad esempio, per riconfigurare un&#39;impostazione danneggiata.

**Esportare le informazioni di configurazione**

1. In Administration Console, fare clic su Impostazioni > Gestione utente > Configurazione > Importa ed esporta file di configurazione.
1. Fai clic su Esporta. Se si utilizza Microsoft Internet Explorer, viene richiesto di specificare il percorso in cui salvare il file. Se utilizzi Firefox, il file viene salvato sul desktop.

**Importare le informazioni di configurazione**

1. In Administration Console, fare clic su Impostazioni > Gestione utente > Configurazione > Importa ed esporta file di configurazione.
1. Fare clic su Sfoglia per trovare il file di configurazione, su Importa e quindi su OK.
