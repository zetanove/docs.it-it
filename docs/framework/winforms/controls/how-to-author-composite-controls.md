---
title: "Procedura: modificare controlli compositi | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "controlli composti, creazione"
  - "controlli utente [Windows Form], creazione"
  - "controlli utente [Windows Form], ereditare da"
  - "UserControl (classe), creazione di controlli composti"
ms.assetid: 79c9cf05-5ab6-4a18-886d-88a64748b098
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: modificare controlli compositi
I controlli compositi possono essere impiegati in vari modi.  È possibile modificarli come parte di un progetto di applicazione desktop Windows e utilizzarli solamente sui form nel progetto.  In alternativa, è possibile modificarli in un progetto di libreria di controlli Windows, compilare il progetto in un assembly e utilizzare i controlli in altri progetti.  È inoltre possibile ereditare da tali controlli e utilizzare l'ereditarietà visiva per personalizzarli rapidamente secondo scopi specifici.  
  
> [!NOTE]
>  Per modificare un controllo composito da utilizzare in Web Form, vedere [Developing Custom ASP.NET Server Controls](../Topic/Developing%20Custom%20ASP.NET%20Server%20Controls.md).  
>   
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per modificare un controllo composito  
  
1.  Aprire un nuovo progetto **Applicazione Windows** denominato `DemoControlHost`.  
  
2.  Scegliere **Aggiungi controllo utente** dalmenu **Progetto**.  
  
3.  Nella finestra di dialogo **Aggiungi nuovo elemento** assegnare al file di classe \(file VB o CS\) il nome desiderato per il controllo composito.  
  
4.  Scegliere **Aggiungi** per creare il file di classe per il controllo composito.  
  
5.  Aggiungere i controlli dalla **Casella degli strumenti** alla superficie del controllo composito.  
  
6.  Inserire il codice nelle routine evento per gestire gli eventi generati dal controllo composito o dai relativi controlli costitutivi.  
  
7.  Chiudere la finestra di progettazione per il controllo composito e salvare il file quando viene richiesto.  
  
8.  Scegliere **Compila soluzione** dal menu **Compila**.  
  
     È necessario compilare il progetto per visualizzare i controlli personalizzati nella **Casella degli strumenti**.  
  
9. Dalla scheda **DemoControlHost** della **Casella degli strumenti** aggiungere le istanze del controllo a `Form1`.  
  
### Per modificare una libreria di classi di controlli  
  
1.  Aprire un nuovo progetto **Libreria di controlli Windows**.  
  
     Per impostazione predefinita, il progetto contiene un controllo composito.  
  
2.  Aggiungere i controlli e il codice attenendosi alla procedura precedente.  
  
3.  Scegliere un controllo che si desidera non venga modificato dalle classi che ereditano e impostare la relativa proprietà **Modifiers** su **Private**.  
  
4.  Compilare la DLL.  
  
### Per ereditare da un controllo composito in una libreria di classi di controlli  
  
1.  Per aggiungere alla soluzione un nuovo progetto **Applicazione Windows**, scegliere **Aggiungi** dal menu **File**, quindi fare clic su **Nuovo progetto**.  
  
2.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse sulla cartella **Riferimenti** del nuovo progetto e scegliere **Aggiungi riferimento** per aprire la finestra di dialogo corrispondente.  
  
3.  Selezionare la scheda **Progetti** e fare doppio clic sul progetto della libreria di controlli.  
  
4.  Scegliere **Compila soluzione** dal menu **Compila**.  
  
5.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto della libreria di controlli, quindi scegliere **Aggiungi nuovo elemento** dal menu di scelta rapida.  
  
6.  Selezionare il modello **Controllo utente ereditato** dalla finestra di dialogo **Aggiungi nuovo elemento**.  
  
7.  Nella finestra di dialogo **Selezione ereditarietà** fare doppio clic sul controllo da cui ereditare.  
  
     Un nuovo controllo verrà aggiunto al progetto.  
  
8.  Aprire la finestra di progettazione grafica per il nuovo controllo e aggiungere altri controlli costitutivi.  
  
     I controlli costitutivi ereditati dal controllo composito sono visibili nella DLL ed è possibile modificare le proprietà dei controlli la cui proprietà **Modifiers** è **Public**.  Non è invece possibile cambiare le proprietà dei controlli con la proprietà **Modifiers** impostata su **Private**.  
  
## Vedere anche  
 [Procedura dettagliata: modifica di un controllo composito con Visual Basic](../../../../docs/framework/winforms/controls/walkthrough-authoring-a-composite-control-with-visual-basic.md)   
 [Procedura dettagliata: modifica di un controllo composito con Visual C\#](../../../../docs/framework/winforms/controls/walkthrough-authoring-a-composite-control-with-visual-csharp.md)   
 [Procedura dettagliata: eredità da un controllo Windows Form con Visual Basic](../../../../docs/framework/winforms/controls/walkthrough-inheriting-from-a-windows-forms-control-with-visual-basic.md)   
 [Procedura dettagliata: eredità da un controllo di Windows Form con Visual C\#](../../../../docs/framework/winforms/controls/walkthrough-inheriting-from-a-windows-forms-control-with-visual-csharp.md)   
 [Consigli sui tipi di controlli](../../../../docs/framework/winforms/controls/control-type-recommendations.md)   
 [Procedura: creare controlli per Windows Form](../../../../docs/framework/winforms/controls/how-to-author-controls-for-windows-forms.md)   
 [Tipi di controlli personalizzati](../../../../docs/framework/winforms/controls/varieties-of-custom-controls.md)