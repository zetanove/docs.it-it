---
title: 'Procedura: fare riferimento agli oggetti COM da Visual Basic | Documenti di Microsoft'
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- COM interop, referencing COM objects
- referencing objects, COM objects from Visual Basic
- objects [Visual Basic], referencing
- COM objects, referencing
- interop assemblies
ms.assetid: 9c518fb4-27d9-4112-9e6a-5a7d0210af6f
caps.latest.revision: 13
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 97c132bcbd36ba7810acadb2aebddc5e84f0b44d
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-reference-com-objects-from-visual-basic"></a>Procedura: fare riferimento a oggetti COM da Visual Basic
In [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)], aggiunta di riferimenti a oggetti COM che dispongono di librerie richiede la creazione di un assembly di interoperabilità per la libreria COM. Riferimenti ai membri dell'oggetto COM vengono indirizzati all'assembly di interoperabilità e quindi inoltrati all'oggetto COM effettivo. Le risposte dall'oggetto COM vengono indirizzate all'assembly di interoperabilità e inoltrate al [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] dell'applicazione.  
  
 È possibile fare riferimento a un oggetto COM senza utilizzare un assembly di interoperabilità incorporando le informazioni sul tipo per l'oggetto COM in un assembly .NET. Per incorporare informazioni sul tipo, impostare il `Embed Interop Types` proprietà `True` per il riferimento all'oggetto COM. Se esegue la compilazione tramite il compilatore della riga di comando, utilizzare il `/link` opzione per fare riferimento alla libreria COM. Per ulteriori informazioni, vedere [/link (Visual Basic)](../../../visual-basic/reference/command-line-compiler/link.md).  
  
 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]Crea automaticamente gli assembly di interoperabilità quando si aggiunge un riferimento a una libreria dei tipi dall'ambiente di sviluppo integrato (IDE). Quando si utilizza dalla riga di comando, è possibile utilizzare l'utilità Tlbimp per creare manualmente gli assembly di interoperabilità.  
  
### <a name="to-add-references-to-com-objects"></a>Per aggiungere riferimenti a oggetti COM  
  
1.  Nel **progetto** menu, scegliere **Aggiungi riferimento** e quindi fare clic su di **COM** scheda nella finestra di dialogo.  
  
2.  Selezionare il componente che si desidera utilizzare dall'elenco di oggetti COM.  
  
3.  Per semplificare l'accesso all'assembly di interoperabilità, aggiungere un `Imports` all'inizio della classe o del modulo in cui verrà utilizzato l'oggetto COM. Ad esempio, nell'esempio seguente importa lo spazio dei nomi `INKEDLib` per gli oggetti a cui fa riferimento il `Microsoft InkEdit Control 1.0` libreria.  
  
     [!code-vb[&#40; VbVbalrInterop](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/how-to-reference-com-objects_1.vb)]  
  
### <a name="to-create-an-interop-assembly-using-tlbimp"></a>Per creare un assembly di interoperabilità tramite Tlbimp  
  
1.  Aggiungere il percorso di Tlbimp al percorso di ricerca, se non è già parte del percorso di ricerca e non è attualmente la directory in cui si trova.  
  
2.  Tlbimp chiamata da un prompt dei comandi, fornendo le informazioni seguenti:  
  
    -   Nome e il percorso della DLL che contiene la libreria dei tipi  
  
    -   Nome e il percorso dello spazio dei nomi in cui inserire le informazioni  
  
    -   Nome e percorso dell'assembly di interoperabilità.  
  
     Nel codice seguente ne viene illustrato un esempio:  
  
    ```  
    Tlbimp test3.dll /out:NameSpace1 /out:Interop1.dll  
    ```  
  
     È possibile utilizzare Tlbimp per creare assembly di interoperabilità per librerie dei tipi, anche per gli oggetti COM non registrati. Tuttavia, gli oggetti COM a cui fa riferimento l'assembly di interoperabilità devono essere registrati correttamente nel computer in cui essi devono essere utilizzati. È possibile registrare un oggetto COM tramite l'utilità Regsvr32 incluso con il sistema operativo Windows.  
  
## <a name="see-also"></a>Vedere anche  
 [Interoperabilità COM](../../../visual-basic/programming-guide/com-interop/index.md)   
 [Tlbimp.exe (Type Library Importer)](http://msdn.microsoft.com/library/ec0a8d63-11b3-4acd-b398-da1e37e97382)   
 [Tlbexp.exe (Type Library Exporter)](http://msdn.microsoft.com/library/a487d61b-d166-467b-a7ca-d8b52fbff42d)   
 [Procedura dettagliata: Implementazione dell'ereditarietà con gli oggetti COM](../../../visual-basic/programming-guide/com-interop/walkthrough-implementing-inheritance-with-com-objects.md)   
 [Risoluzione dei problemi di interoperabilità](../../../visual-basic/programming-guide/com-interop/troubleshooting-interoperability.md)   
 [Istruzione Imports (tipo e spazio dei nomi .NET)](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)
