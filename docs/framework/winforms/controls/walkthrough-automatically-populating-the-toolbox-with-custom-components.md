---
title: "Procedura dettagliata: compilare automaticamente la casella degli strumenti con componenti personalizzati | Microsoft Docs"
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
  - "componenti personalizzati, aggiunta alla Casella degli strumenti"
  - "IToolboxService (interfaccia)"
  - "casella degli strumenti [Windows Form], compilazione"
ms.assetid: 2fa1e3e8-6b9f-42b2-97c0-2be57444dba4
caps.latest.revision: 22
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 22
---
# Procedura dettagliata: compilare automaticamente la casella degli strumenti con componenti personalizzati
Se i componenti sono definiti da un progetto nella soluzione corrente, verranno automaticamente inclusi nella **Casella degli strumenti**, senza la necessità di altre azioni.  È anche possibile inserire manualmente i componenti personalizzati nella **Casella degli strumenti** utilizzando [Choose Toolbox Items Dialog Box \(Visual Studio\)](http://msdn.microsoft.com/it-it/bd07835f-18a8-433e-bccc-7141f65263bb), ma la **Casella degli strumenti** tiene conto degli elementi presenti negli output di compilazione della soluzione con tutte le seguenti caratteristiche:  
  
-   Implementa <xref:System.ComponentModel.IComponent>.  
  
-   Non dispone di <xref:System.ComponentModel.ToolboxItemAttribute> impostato su `false`.  
  
-   Non dispone di <xref:System.ComponentModel.DesignTimeVisibleAttribute> impostato su `false`.  
  
> [!NOTE]
>  La **Casella degli strumenti** non segue le catene dei riferimenti e quindi non visualizzerà gli elementi che non vengono compilati da un progetto nella soluzione.  
  
 In questa procedura dettagliata viene descritto come impostare la visualizzazione automatica di un componente personalizzato nella **Casella degli strumenti** successivamente alla compilazione del componente.  Di seguito vengono elencate le attività illustrate nella procedura dettagliata:  
  
-   Creazione di un progetto Windows Form  
  
-   Creazione di un componente personalizzato.  
  
-   Creazione di un'istanza di un componente personalizzato.  
  
-   Scaricamento e nuovo caricamento di un componente personalizzato.  
  
 Al termine, si potrà notare che nella **Casella degli strumenti** è incluso il componente creato.  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
## Creazione del progetto  
 Il primo passaggio indica come creare il progetto e impostare il form.  
  
#### Per creare il progetto  
  
1.  Creare un progetto di applicazione basata su Windows chiamato `ToolboxExample`.  
  
     Per ulteriori informazioni, vedere [How to: Create a Windows Application Project](http://msdn.microsoft.com/it-it/b2f93fed-c635-4705-8d0e-cf079a264efa).  
  
2.  Aggiungere un nuovo componente al progetto.  Chiamarlo `DemoComponent`.  
  
     Per ulteriori informazioni, vedere [NIB:How to: Add New Project Items](http://msdn.microsoft.com/it-it/63d3e16b-de6e-4bb5-a0e3-ecec762201ce).  
  
3.  Compilare il progetto.  
  
4.  Scegliere **Opzioni** dal menu **Strumenti**.  Scegliere **su Generale** in **Progettazione Windows Form** e verificare che l'opzione **AutoToolboxPopulate** sia impostata su **True**.  
  
## Creazione di un'istanza di un componente personalizzato  
 Il passaggio successivo consiste nella creazione di un'istanza del componente personalizzato nel form.  Dal momento che la **Casella degli strumenti** automaticamente tiene conto del nuovo componente, la creazione risulterà semplice al pari di altri componenti o controlli.  
  
#### Per creare un'istanza di un componente personalizzato  
  
1.  Aprire il form del progetto in **Progettazione Windows Form**.  
  
2.  Nella **Casella degli strumenti** fare clic sulla nuova scheda denominata **Componenti ToolboxExample**.  
  
     Dopo aver selezionato la scheda, verrà visualizzato **DemoComponent**.  
  
    > [!NOTE]
    >  Per non compromettere le prestazioni, i componenti presenti nell'area compilata automaticamente della **Casella degli strumenti** non vengono visualizzate le bitmap personalizzate e <xref:System.Drawing.ToolboxBitmapAttribute> non è supportato.  Per visualizzare un'icona per un componente personalizzato nella **Casella degli strumenti**, caricare il componente nella finestra di dialogo **Scegli elementi della Casella degli strumenti**.  
  
3.  Trascinare il componente nel form.  
  
     Un'istanza del componente viene creata e aggiunta nella **Barra dei componenti**.  
  
## Scaricamento e nuovo caricamento di un componente personalizzato  
 La **Casella degli strumenti** tiene conto dei componenti di ogni progetto caricato e quando un progetto viene scaricato, rimuove i riferimenti ai componenti del progetto.  
  
#### Per valutare l'effetto nella Casella degli strumenti dello scaricamento e nuovo caricamento dei componenti  
  
1.  Scaricare il progetto dalla soluzione.  
  
     Per ulteriori informazioni sullo scaricamento dei progetti, vedere [NIB:How to: Unload and Reload Projects](http://msdn.microsoft.com/it-it/abc0155b-8fcb-4ffc-95b6-698518a7100b).  Se viene chiesto di salvare, scegliere **Sì**.  
  
2.  Aggiungere alla soluzione un nuovo progetto **Applicazione Windows**.  Aprire il form nella **finestra di progettazione**.  
  
     La scheda **Componenti ToolboxExample** del progetto precedente è stata rimossa.  
  
3.  Ricaricare il progetto `ToolboxExample`.  
  
     La scheda **Componenti ToolboxExample** viene ora di nuovo visualizzata.  
  
## Passaggi successivi  
 In questa procedura dettagliata viene spiegato che la **Casella degli strumenti** tiene conto dei componenti di un progetto e anche dei controlli.  Provare con i controlli personalizzati aggiungendo e rimuovendo i progetti dei controlli dalla soluzione.  
  
## Vedere anche  
 [General, Windows Forms Designer, Options Dialog Box](http://msdn.microsoft.com/it-it/8dd170af-72f0-4212-b04b-034ceee92834)   
 [How to: Manipulate Toolbox Tabs](http://msdn.microsoft.com/it-it/21285050-cadd-455a-b1f5-a2289a89c4db)   
 [Choose Toolbox Items Dialog Box \(Visual Studio\)](http://msdn.microsoft.com/it-it/bd07835f-18a8-433e-bccc-7141f65263bb)   
 [Inserimento di controlli in Windows Form](../../../../docs/framework/winforms/controls/putting-controls-on-windows-forms.md)