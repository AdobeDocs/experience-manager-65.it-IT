---
title: Importazione ed esportazione del file di configurazione
description: Scopri come importare ed esportare il file di configurazione per modificare le preferenze del server o configurare un’altra istanza di prodotto di AEM forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 225dbeb5-a21c-4338-98c7-e10c32973721
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '252'
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
