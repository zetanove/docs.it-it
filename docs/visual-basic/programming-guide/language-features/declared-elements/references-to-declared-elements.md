---
title: Riferimenti a elementi dichiarati (Visual Basic) | Documenti di Microsoft
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
- declared elements
- references, declared elements
- qualified names
ms.assetid: d6301709-f4cc-4b7a-b8ba-80898f14ab46
caps.latest.revision: 19
author: stevehoag
ms.author: shoag
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
ms.openlocfilehash: 48a04f81075accc073b0d1f5b7a61006bef807ae
ms.lasthandoff: 03/13/2017

---
# <a name="references-to-declared-elements-visual-basic"></a>Riferimenti a elementi dichiarati (Visual Basic)
Quando il codice fa riferimento a un elemento dichiarato, il [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] compilatore corrisponde al nome nel riferimento alla dichiarazione corretta di tale nome. Se più di un elemento viene dichiarato con lo stesso nome, è possibile controllare quale di questi elementi viene riferimento *qualificazione* il relativo nome.  
  
 Il compilatore tenta di ottenere un riferimento a una dichiarazione del nome e il *nell'ambito più ristretto*. Ciò significa inizia con il codice di riferimento e spostandosi verso l'esterno per i livelli successivi di che contiene elementi.  
  
 Nell'esempio seguente vengono visualizzati i riferimenti a due variabili con lo stesso nome. Nell'esempio vengono dichiarate due variabili, ciascuna denominata `totalCount`, con diversi livelli di ambito nel modulo `container`. Quando la procedura `showCount` Visualizza `totalCount` senza qualifica, il [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] compilatore risolve il riferimento alla dichiarazione con l'ambito più ristretto, ovvero la dichiarazione locale all'interno di `showCount`. Quando è qualificato `totalCount` con il modulo contenente `container`, il compilatore risolve il riferimento alla dichiarazione con l'ambito più ampio.  
  
```vb  
' Assume these two modules are both in the same assembly.  
Module container  
    Public totalCount As Integer = 1  
    Public Sub showCount()  
        Dim totalCount As Integer = 6000  
        ' The following statement displays the local totalCount (6000).  
        MsgBox("Unqualified totalCount is " & CStr(totalCount))  
        ' The following statement displays the module's totalCount (1).  
        MsgBox("container.totalCount is " & CStr(container.totalCount))  
    End Sub  
End Module  
Module callingModule  
    Public Sub displayCount()  
        container.showCount()  
        ' The following statement displays the containing module's totalCount (1).  
        MsgBox("container.totalCount is " & CStr(container.totalCount))  
    End Sub  
End Module  
```  
  
## <a name="qualifying-an-element-name"></a>Nome di un elemento di qualificazione  
 Se si desidera eseguire l'override di questo processo di ricerca e specificare un nome dichiarato in un ambito più ampio, è necessario *qualificare* il nome con l'elemento contenitore dell'ambito più ampio. In alcuni casi, potrebbe anche essere necessario qualificare l'elemento contenitore.  
  
 Qualificare un nome significa farlo precedere, nell'istruzione del codice sorgente con le informazioni che identificano in cui è definito l'elemento di destinazione. Queste informazioni vengono definite una *stringa di qualificazione*. Può includere uno o più spazi dei nomi e un modulo, classe o struttura.  
  
 La stringa di qualificazione deve specificare in modo univoco il modulo, classe o struttura che contiene l'elemento di destinazione. Il contenitore a sua volta potrebbe trovarsi in un altro elemento contenitore, in genere uno spazio dei nomi. Potrebbe essere necessario includere diversi elementi che contiene la stringa di qualificazione.  
  
#### <a name="to-access-a-declared-element-by-qualifying-its-name"></a>Per accedere a un elemento dichiarato qualificando il nome  
  
1.  Determinare il percorso in cui è stato definito l'elemento. Può includere uno spazio dei nomi o anche una gerarchia di spazi dei nomi. Nello spazio dei nomi di livello più basso, l'elemento deve essere incluso in un modulo, classe o struttura.  
  
    ```vb  
    ' Assume the following hierarchy exists outside your code.  
    Namespace outerSpace  
        Namespace innerSpace  
            Module holdsTotals  
                Public Structure totals  
                    Public thisTotal As Integer  
                    Public Shared grandTotal As Long  
                End Structure  
            End Module  
        End Namespace  
    End Namespace  
    ```  
  
2.  Determinare il percorso di qualificazione in base alla posizione dell'elemento di destinazione. Iniziare con lo spazio dei nomi di livello più alto, procedere con lo spazio dei nomi di livello più basso e terminare con il modulo, classe o struttura che contiene l'elemento di destinazione. Ogni elemento del percorso deve contenere l'elemento che lo segue.  
  
     `outerSpace` → `innerSpace` → `holdsTotals` → `totals`  
  
3.  Preparare la stringa di qualificazione per l'elemento di destinazione. Inserire un punto (`.`) dopo ogni elemento nel percorso. L'applicazione deve poter accedere a ogni elemento nella stringa di qualificazione.  
  
    ```vb  
    outerSpace.innerSpace.holdsTotals.totals.  
    ```  
  
4.  Scrivere l'espressione o istruzione di assegnazione, che fa riferimento all'elemento di destinazione in modo normale.  
  
    ```vb  
    grandTotal = 9000  
    ```  
  
5.  Anteporre al nome di elemento di destinazione con la stringa di qualificazione. Il nome deve seguire immediatamente il periodo (`.`) che segue il modulo, classe o struttura che contiene l'elemento.  
  
    ```vb  
    ' Assume the following module is part of your code.  
    Module accessGrandTotal  
        Public Sub setGrandTotal()  
            outerSpace.innerSpace.holdsTotals.totals.grandTotal = 9000  
        End Sub  
    End Module  
    ```  
  
6.  Il compilatore utilizza la stringa di qualificazione per trovare una dichiarazione di non crittografata e non ambigua a cui può trovare il riferimento all'elemento di destinazione.  
  
 Inoltre, è necessario qualificare un riferimento al nome, se l'applicazione ha accesso a più di un elemento di programmazione che ha lo stesso nome. Ad esempio, il <xref:System.Windows.Forms>e <xref:System.Web.UI.WebControls>due spazi dei nomi contengono un `Label` (classe) (<xref:System.Windows.Forms.Label?displayProperty=fullName> e <xref:System.Web.UI.WebControls.Label?displayProperty=fullName>).</xref:System.Web.UI.WebControls.Label?displayProperty=fullName> </xref:System.Windows.Forms.Label?displayProperty=fullName> </xref:System.Web.UI.WebControls> </xref:System.Windows.Forms> Se l'applicazione utilizza entrambi, o se definisce il proprio `Label` (classe), è necessario distinguere i diversi `Label` oggetti. Includere l'alias dello spazio dei nomi o importazione nella dichiarazione di variabile. Nell'esempio seguente viene utilizzato l'alias di importazione.  
  
```vb  
' The following statement must precede all your declarations.  
Imports win = System.Windows.Forms, web = System.Web.UI.WebControls  
' The following statement references the Windows.Forms.Label class.  
Dim winLabel As New win.Label()  
```  
  
## <a name="members-of-other-containing-elements"></a>Membri di altri elementi contenitore  
 Quando si utilizza un membro non condiviso di un'altra classe o struttura, è innanzitutto necessario qualificare il nome del membro con una variabile o espressione che punta a un'istanza della classe o struttura. Nell'esempio seguente, `demoClass` è un'istanza di una classe denominata `class1`.  
  
```vb  
Dim demoClass As class1 = New class1()  
demoClass.someSub[(argumentlist)]  
```  
  
 È possibile utilizzare il nome della classe per qualificare un membro che non è [Shared](../../../../visual-basic/language-reference/modifiers/shared.md). È innanzitutto necessario creare un'istanza in una variabile oggetto (in questo caso `demoClass`) e quindi farvi riferimento tramite il nome della variabile.  
  
 Se una classe o struttura ha un `Shared` membro, è possibile qualificare tale membro con il nome di classe o struttura o con una variabile o espressione che punta a un'istanza.  
  
 Un modulo dispone di alcuna istanza separata e tutti i relativi membri sono `Shared` per impostazione predefinita. Pertanto, qualificare un membro del modulo con il nome del modulo.  
  
 L'esempio seguente mostra riferimenti qualificati a procedure di membri di modulo. Nell'esempio vengono dichiarati due `Sub` procedure, sia denominato `perform`, in moduli diversi in un progetto. Ognuno di essi può essere specificato senza qualifica all'interno del relativo modulo ma deve essere qualificato a cui fa riferimento da qualsiasi altra posizione. Poiché l'ultimo riferimento `module3` non soddisfa i requisiti `perform`, il compilatore non può risolvere il riferimento.  
  
```vb  
' Assume these three modules are all in the same assembly.  
Module module1  
    Public Sub perform()  
        MsgBox("module1.perform() now returning")  
    End Sub  
End Module  
Module module2  
    Public Sub perform()  
        MsgBox("module2.perform() now returning")  
    End Sub  
    Public Sub doSomething()  
        ' The following statement calls perform in module2, the active module.  
        perform()  
        ' The following statement calls perform in module1.  
        module1.perform()  
    End Sub  
End Module  
Module module3  
    Public Sub callPerform()  
        ' The following statement calls perform in module1.  
        module1.perform()  
        ' The following statement makes an unresolvable name reference  
        ' and therefore generates a COMPILER ERROR.  
        perform() ' INVALID statement  
    End Sub  
End Module  
```  
  
## <a name="references-to-projects"></a>Riferimenti a progetti  
 Utilizzare [pubblica](../../../../visual-basic/language-reference/modifiers/public.md) elementi definiti in un altro progetto, è innanzitutto necessario impostare un *riferimento* alla raccolta di assembly o un tipo di progetto. Per impostare un riferimento, fare clic su **Aggiungi riferimento** sul **progetto** menu o utilizzare il [/reference (Visual Basic)](../../../../visual-basic/reference/command-line-compiler/reference.md) l'opzione del compilatore da riga di comando.  
  
 Ad esempio, è possibile utilizzare il modello a oggetti XML di [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)]. Se si imposta un riferimento il <xref:System.Xml>dello spazio dei nomi, è possibile dichiarare e utilizzare una delle relative classi, ad esempio <xref:System.Xml.XmlDocument>.</xref:System.Xml.XmlDocument> </xref:System.Xml> L'esempio seguente usa <xref:System.Xml.XmlDocument>.</xref:System.Xml.XmlDocument>  
  
```vb  
' Assume this project has a reference to System.Xml  
' The following statement creates xDoc as an XML document object.  
Dim xDoc As System.Xml.XmlDocument  
```  
  
## <a name="importing-containing-elements"></a>Importazione di elementi contenitore  
 È possibile utilizzare il [istruzione Imports (tipo e Namespace .NET)](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md) a *importare* gli spazi dei nomi che contengono i moduli o le classi che si desiderano utilizzare. In questo modo è possibile fare riferimento agli elementi definiti in uno spazio dei nomi importato senza i relativi nomi completi. Nell'esempio seguente viene riscritto l'esempio precedente per importare il <xref:System.Xml>dello spazio dei nomi.</xref:System.Xml>  
  
```vb  
' Assume this project has a reference to System.Xml  
' The following statement must precede all your declarations.  
Imports System.Xml  
' The following statement creates xDoc as an XML document object.  
Dim xDoc As XmlDocument  
```  
  
 Inoltre, il `Imports` istruzione è possibile definire un *alias di importazione* per ogni spazio dei nomi importato. Ciò può rendere il codice sorgente più breve e facile da leggere. Nell'esempio seguente viene riscritto l'esempio precedente per utilizzare `xD` come alias per il <xref:System.Xml>dello spazio dei nomi.</xref:System.Xml>  
  
```vb  
' Assume this project has a reference to System.Xml  
' The following statement must precede all your declarations.  
Imports xD = System.Xml  
' The following statement creates xDoc as an XML document object.  
Dim xDoc As xD.XmlDocument  
```  
  
 Il `Imports` istruzione non rende gli elementi da altri progetti disponibili per l'applicazione. Vale a dire non sostituisce l'impostazione di un riferimento. L'importazione di uno spazio dei nomi appena Elimina la necessità di qualificare i nomi definiti nello spazio dei nomi.  
  
 È inoltre possibile utilizzare il `Imports` per importare moduli, classi, strutture ed enumerazioni. È quindi possibile utilizzare i membri di tali elementi importati senza qualifica. Tuttavia, è necessario qualificare sempre membri non condivisi di classi e strutture con una variabile o espressione che restituisce un'istanza della classe o struttura.  
  
## <a name="naming-guidelines"></a>Convenzioni di denominazione  
 Quando si definiscono due o più elementi di programmazione che hanno lo stesso nome, un *nome ambiguità* possono verificarsi quando il compilatore tenta di risolvere un riferimento a tale nome. Se più di una definizione nell'ambito, o se non è una definizione nell'ambito, il riferimento è non risolvibile. Per un esempio, vedere "Esempio di riferimento qualificato" in questa pagina della Guida in linea.  
  
 È possibile evitare ambiguità, assegnando a tutti gli elementi di nomi univoci. Quindi è possibile creare riferimento a qualsiasi elemento senza la necessità di qualificare il nome con un spazio dei nomi, modulo o classe. È anche possibile ridurre le probabilità di accidentalmente fare riferimento a un elemento non corretto.  
  
## <a name="shadowing"></a>Shadowing  
 Quando due elementi di programmazione condividono lo stesso nome, è possibile nascondere una di esse, o *shadow*, l'altro. Un elemento nascosto non è disponibile per riferimento; al contrario, quando il codice utilizza il nome dell'elemento nascosto, il [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] compilatore risolve tale nome nell'elemento di shadowing. Per una spiegazione più dettagliata con esempi, vedere [Shadowing in Visual Basic](../../../../visual-basic/programming-guide/language-features/declared-elements/shadowing.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Nomi elementi dichiarati](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)   
 [Caratteristiche di elementi dichiarati](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-characteristics.md)   
 [NIB procedura: modificare le proprietà del progetto e le impostazioni di configurazione](http://msdn.microsoft.com/en-us/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)   
 [Variabili](../../../../visual-basic/programming-guide/language-features/variables/index.md)   
 [Istruzione Imports (tipo e spazio dei nomi .NET)](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)   
 [Operatore new](../../../../visual-basic/language-reference/operators/new-operator.md)   
 [Public](../../../../visual-basic/language-reference/modifiers/public.md)
