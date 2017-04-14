---
title: "How to: Distinguish Between Clicks and Double-Clicks | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "mouse, click"
  - "mouse, double-click"
  - "mouse clicks, single versus double"
ms.assetid: d836ac8c-85bc-4f3a-a761-8aee03dc682c
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# How to: Distinguish Between Clicks and Double-Clicks
In genere, un singolo *clic* avvia un'azione dell'interfaccia utente e un *doppio clic* estende l'azione.  Ad esempio, un solo clic consente in genere di scegliere un elemento e un doppio clic consente di modificare l'elemento selezionato.  Gli eventi Click in Windows Form, tuttavia, non si adattano facilmente a uno scenario in cui un clic e un doppio clic eseguono azioni incompatibili, perché un'azione associata all'evento <xref:System.Windows.Forms.Control.Click> o <xref:System.Windows.Forms.Control.MouseClick> viene eseguito prima dell'azione collegata all'evento <xref:System.Windows.Forms.Control.DoubleClick> o <xref:System.Windows.Forms.Control.MouseDoubleClick>.  Questo argomento illustra due soluzioni a questo problema.  Una soluzione consiste nel gestire l'evento di doppio clic e ripristinare le azioni nella gestione dell'evento Click.  In rare situazioni potrebbe essere necessario simulare un comportamento di clic e doppio clic gestendo l'evento <xref:System.Windows.Forms.Control.MouseDown> e usando le proprietà <xref:System.Windows.Forms.SystemInformation.DoubleClickTime%2A> e <xref:System.Windows.Forms.SystemInformation.DoubleClickSize%2A> della classe <xref:System.Windows.Forms.SystemInformation>.  A questo punto, si misura l'intervallo trascorso tra un clic e l'altro e, se viene eseguito un secondo clic prima che venga raggiunto il valore di <xref:System.Windows.Forms.SystemInformation.DoubleClickTime%2A> all'interno di un rettangolo definito da <xref:System.Windows.Forms.SystemInformation.DoubleClickSize%2A>, eseguire l'azione di doppio clic; in caso contrario, eseguire l'azione di clic.  
  
### Per eseguire il rollback di un'azione di clic  
  
-   Assicurarsi che il controllo con cui si lavora disponga del comportamento standard di doppio clic.  In caso contrario, abilitare il controllo con il metodo <xref:System.Windows.Forms.Control.SetStyle%2A>.  Gestire l'evento di doppio clic ed eseguire il rollback dell'azione di clic, nonché dell'azione di doppio clic.  L'esempio di codice seguente illustra come creare un pulsante personalizzato con doppio clic abilitato, nonché come eseguire il rollback dell'azione di clic nel codice di gestione dell'evento di doppio clic.  
  
     [!code-csharp[System.Windows.Forms.ButtonDoubleClick#1](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ButtonDoubleClick/CS/Form1.cs#1)]
     [!code-vb[System.Windows.Forms.ButtonDoubleClick#1](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ButtonDoubleClick/VB/Form1.vb#1)]  
  
### Per distinguere tra clic nell'evento MouseDown  
  
-   Gestire l'evento <xref:System.Windows.Forms.Control.MouseDown> e determinare la posizione e l'intervallo tra i clic usando le proprietà <xref:System.Windows.Forms.SystemInformation> appropriate e un componente <xref:System.Windows.Forms.Timer>.  Eseguire l'azione appropriata a seconda che venga eseguito un clic o un doppio clic.  Nell'esempio di codice seguente viene illustrato come procedere.  
  
     [!code-cpp[System.Windows.Forms.SingleVersusDoubleClick#0](../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.SingleVersusDoubleClick/cpp/form1.cpp#0)]
     [!code-csharp[System.Windows.Forms.SingleVersusDoubleClick#0](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.SingleVersusDoubleClick/CS/form1.cs#0)]
     [!code-vb[System.Windows.Forms.SingleVersusDoubleClick#0](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.SingleVersusDoubleClick/VB/form1.vb#0)]  
  
## Compilazione del codice  
 Gli esempi presentano i requisiti seguenti:  
  
-   Riferimenti agli assembly System, System.Drawing e System.Windows.Forms.  
  
 Per informazioni sulla compilazione di questi esempi dalla riga di comando per [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] o [!INCLUDE[csprcs](../../../includes/csprcs-md.md)], vedere [Compilazione dalla riga di comando](../Topic/Building%20from%20the%20Command%20Line%20\(Visual%20Basic\).md) o [Compilazione dalla riga di comando con csc.exe](../../../ocs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md).  È anche possibile compilare questi esempi in [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] incollando il codice in nuovi progetti.  Vedere anche [Procedura: Compilare ed eseguire un esempio di codice Windows Form completo tramite Visual Studio](http://msdn.microsoft.com/library/Bb129228\(v=vs.110\)).  
  
## Vedere anche  
 [Mouse Input in a Windows Forms Application](../../../docs/framework/winforms/mouse-input-in-a-windows-forms-application.md)