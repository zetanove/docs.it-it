---
title: "How to: Reference COM Objects from Visual Basic | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "COM interop, referencing COM objects"
  - "referencing objects, COM objects from Visual Basic"
  - "objects [Visual Basic], referencing"
  - "COM objects, referencing"
  - "interop assemblies"
ms.assetid: 9c518fb4-27d9-4112-9e6a-5a7d0210af6f
caps.latest.revision: 13
caps.handback.revision: 13
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# How to: Reference COM Objects from Visual Basic
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

In [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] la procedura per l'aggiunta di riferimenti agli oggetti COM che dispongono di librerie dei tipi richiede la creazione di un assembly di interoperabilità per la libreria COM.  I riferimenti ai membri dell'oggetto COM sono inviati all'assembly di interoperabilità e quindi inoltrati all'oggetto COM.  Le risposte provenienti dall'oggetto COM vengono instradate all'assembly di interoperabilità e inoltrate all'applicazione [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] in uso.  
  
 È possibile fare riferimento a un oggetto COM senza utilizzare un assembly di interoperabilità incorporando le informazioni sul tipo per l'oggetto COM in un assembly .NET.  Per incorporare le informazioni sul tipo, impostare la proprietà `Embed Interop Types` su `True` in relazione al riferimento all'oggetto COM.  Se la compilazione viene eseguita tramite il compilatore della riga di comando, utilizzare l'opzione `/link` per fare riferimento alla libreria COM.  Per ulteriori informazioni, vedere [\/link](../../../visual-basic/reference/command-line-compiler/link.md).  
  
 In [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] vengono creati automaticamente assembly di interoperabilità quando si aggiunge un riferimento a una libreria dei tipi dall'ambiente di sviluppo integrato \(IDE, Integrated Development Environment\).  Dalla riga di comando è possibile utilizzare l'utilità Tlbimp per creare manualmente assembly di interoperabilità.  
  
### Per aggiungere riferimenti a oggetti COM  
  
1.  Scegliere **Aggiungi riferimento** dal menu **Progetto**, quindi fare clic sulla scheda **COM** nella finestra di dialogo.  
  
2.  Nell'elenco di oggetti COM selezionare il componente da utilizzare.  
  
3.  Per semplificare l'accesso all'assembly di interoperabilità, aggiungere un'istruzione `Imports` all'inizio della classe o del modulo in cui verrà utilizzato l'oggetto COM.  Nell'esempio di codice riportato di seguito viene importato `INKEDLib` dello spazio dei nomi per oggetti a cui è fatto riferimento nella libreria `Microsoft InkEdit Control 1.0`.  
  
     [!code-vb[VbVbalrInterop#40](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/how-to-reference-com-objects_1.vb)]  
  
### Per creare un assembly di interoperabilità utilizzando l'utilità Tlbimp  
  
1.  Aggiungere il percorso dell'utilità Tlbimp al percorso di ricerca, se non è già incluso e se la directory corrente non corrisponde a quella in cui è installata l'utilità.  
  
2.  Chiamare l'utilità Tlbimp da un prompt dei comandi, fornendo le seguenti informazioni:  
  
    -   Nome e posizione della DLL che contiene la libreria dei tipi.  
  
    -   Nome e posizione dello spazio dei nomi in cui devono essere inserite le informazioni.  
  
    -   Nome e posizione dell'assembly di interoperabilità.  
  
     Nel codice che segue ne viene illustrato un esempio.  
  
    ```  
    Tlbimp test3.dll /out:NameSpace1 /out:Interop1.dll  
    ```  
  
     È possibile utilizzare l'utilità Tlbimp per creare assembly di interoperabilità per librerie dei tipi, anche nel caso di oggetti COM non registrati.  Tuttavia, gli oggetti COM a cui si fa riferimento tramite gli assembly di interoperabilità devono essere registrati correttamente nel computer in cui verranno utilizzati.  È possibile registrare un oggetto COM utilizzando l'utilità Regsvr32 inclusa nel sistema operativo Windows.  
  
## Vedere anche  
 [COM Interop](../../../visual-basic/programming-guide/com-interop/index.md)   
 [Tlbimp.exe \(Type Library Importer\)](../Topic/Tlbimp.exe%20\(Type%20Library%20Importer\).md)   
 [Tlbexp.exe \(Type Library Exporter\)](../Topic/Tlbexp.exe%20\(Type%20Library%20Exporter\).md)   
 [Walkthrough: Implementing Inheritance with COM Objects](../../../visual-basic/programming-guide/com-interop/walkthrough-implementing-inheritance-with-com-objects.md)   
 [Troubleshooting Interoperability](../../../visual-basic/programming-guide/com-interop/troubleshooting-interoperability.md)   
 [Imports Statement \(.NET Namespace and Type\)](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)