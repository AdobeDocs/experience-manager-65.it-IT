---
title: Installazione e configurazione di Designer
seo-title: Installing and configuring Designer
description: 'Designer è disponibile come programma di installazione autonomo e fornito in bundle con Workbench. Scopri come installare Designer autonomo.  '
seo-description: Designer is available as a stand-alone installer and is also bundled with Workbench. Learn how to install stand-alone Designer.
uuid: c5b779d1-cb6a-48f4-87d6-48464753e516
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: designer
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: f3a5b5ce-2262-4d5d-a8ae-d59a3a4229e7
docset: aem65
role: Admin
exl-id: 90503d29-e079-43f4-a5dc-ce90ed7844c6
source-git-commit: a3cf926bde4a4b3a0810058e84ac01012a4a3a57
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 30%

---

# Installazione e configurazione di Designer{#installing-and-configuring-designer}

## Prerequisiti {#pre-requisites}

Il programma di installazione di AEM Forms Designer richiede la versione a 32 bit di [Pacchetto runtime ridistribuibile di Visual C++ 2012](https://support.microsoft.com/en-us/topic/the-latest-supported-visual-c-downloads-2647da03-1eea-4433-9aff-95f26a218cc0) e [Pacchetto runtime ridistribuibile di Visual C++ 2013](https://support.microsoft.com/it-it/help/3179560/update-for-visual-c-2013-and-visual-c-redistributable-package). Prima di avviare l&#39;installazione, verificare che i pacchetti di runtime ridistribuibili di cui sopra siano installati.

Per installare o disinstallare Designer sono necessari i diritti di amministratore.

## Installare Designer {#install-designer}

Designer è disponibile come programma di installazione autonomo ed è fornito in bundle con WorkBench. Se si utilizza un programma di installazione autonomo per Designer, effettuare le seguenti operazioni:

1. Scarica Designer dall’Adobe [Sito Web delle licenze](https://licensing.adobe.com/).

   >[!NOTE]
   >
   >Se si dispone di una versione precedente di Designer installata, disinstallare la versione precedente prima di procedere.

1. Avviare il programma di installazione di Designer facendo doppio clic su setup.exe.
1. Fornire i propri dettagli e il numero di serie nella schermata di personalizzazione.
1. Se si accetta il contratto di licenza, fare clic su Successivo per procedere.
1. (Facoltativo) Se si desidera installare Designer in una posizione di propria scelta, cambiare il percorso di installazione predefinito. Fai clic su Avanti.
1. Fare clic su Indietro per modificare le preferenze. Per installare Designer, fare clic su Installa.
1. Al completamento dell’installazione, fare clic su Fine.

In alternativa, è possibile installare Designer tramite la riga di comando utilizzando la modalità passiva o silenziosa.

* Installazione passiva da riga di comando: Il programma di installazione visualizza una barra di avanzamento che indica che l&#39;installazione è in corso ma non vengono visualizzati prompt o messaggi di errore. Una volta avviato, non è possibile annullare l&#39;installazione.

```shell
msiexec /i "<absolute path>\Designer.msi" /passive SERIALNUMBER=****-****-****-****-****-****
```

* Installazione automatica da riga di comando: Il programma di installazione esegue l&#39;installazione senza visualizzare un&#39;interfaccia utente. Non vengono visualizzati prompt, messaggi o finestre di dialogo. Una volta avviato, non è possibile annullare l&#39;installazione.

```shell
msiexec /i "<absolute path>\Designer.msi" /quiet SERIALNUMBER=****-****-****-****-****-****
```


