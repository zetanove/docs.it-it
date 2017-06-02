---
title: "Download del pacchetto del gestore del token Web JSON | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d12b3f5b-f1f1-4a9d-a159-0c13e5976c90
caps.latest.revision: 3
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 3
---
# Download del pacchetto del gestore del token Web JSON
In questo argomento viene descritto come scaricare e utilizzare il gestore di token Web JSON nel progetto.  
  
## Download del gestore dei token Web JSON  
 L'estensione Gestore dei token Web JSON è disponibile come pacchetto NuGet, che consente di aggiungere gli assembly e i riferimenti necessari al progetto.  Se NuGet non è già installato, andare su [nuget.org](http://nuget.org) per installarlo.  È possibile visualizzare la cronologia di controllo delle versioni per l'estensione visitando la pagina relativa in NuGet: [Gestore token Web JSON in NuGet](http://www.nuget.org/packages/System.IdentityModel.Tokens.Jwt/)  
  
#### Download del gestore dei token Web JSON tramite la console di gestione del pacchetto utilizzando la GUI di Gestione pacchetti  
  
1.  In Visual Studio fare clic con il pulsante destro del mouse sul progetto in **Esplora soluzioni**, quindi selezionare **Gestisci pacchetti NuGet**.  
  
2.  Nella finestra **Gestisci pacchetti NuGet**, fare clic sulla casella di ricerca e immettere `JWT Token Handler`, quindi scegliere **Invio**.  
  
3.  Dal riquadro Risultati, fare clic sul pulsante **Installa** per il primo risultato.  
  
4.  Verrà avviato il download del pacchetto.  Prima che venga aggiunto al progetto, verrà visualizzata la finestra di dialogo di conferma della licenza.  Se si accettano i termini di licenza, fare clic su **Accetto**.  
  
5.  Gli assembly del Gestore dei token Web JSON più recenti verranno scaricati e aggiunti al progetto.  
  
#### Download del gestore dei token Web JSON tramite la console di Gestione pacchetti  
  
1.  In Visual Studio, fare clic su **Strumenti**, **Gestione pacchetti di librerie**, quindi **Console di gestione pacchetti**.  
  
2.  Verrà aperta la **Console di gestione del pacchetto**.  Immettere il testo seguente e premere **INVIO**:  
  
    ```powershell  
    Install-Package System.IdentityModel.Tokens.Jwt  
    ```  
  
3.  Gli assembly del Gestore dei token Web JSON più recenti verranno scaricati e aggiunti al progetto.