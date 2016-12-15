---
title: "&lt;proceduresignature1&gt; is not CLS-compliant because it overloads &lt;proceduresignature2&gt; which differs from it only by array of array parameter types or by the rank of the array parameter types | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vbc40035"
  - "bc40035"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC40035"
ms.assetid: 50a66dbe-2c1e-41bf-96bc-369301c891ac
caps.latest.revision: 11
caps.handback.revision: 11
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# &lt;proceduresignature1&gt; is not CLS-compliant because it overloads &lt;proceduresignature2&gt; which differs from it only by array of array parameter types or by the rank of the array parameter types
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Una routine o proprietà è contrassegnata come `<CLSCompliant(True)>` quando esegue l'override di un'altra routine o proprietà e l'unica differenza tra gli elenchi dei parametri sta nel livello di annidamento di una matrice irregolare o nel numero di dimensioni di una matrice.  
  
 Nel seguente elenco, l'errore viene generato dalla seconda e dalla terza dichiarazione.  
  
 `Overloads Sub processArray(ByVal arrayParam() As Integer)`  
  
 `Overloads Sub processArray(ByVal arrayParam()() As Integer)`  
  
 `Overloads Sub processArray(ByVal arrayParam(,) As Integer)`  
  
 La seconda dichiarazione modifica il parametro unidimensionale originario `arrayParam` in una matrice di matrici.  La terza dichiarazione modifica `arrayParam` in una matrice bidimensionale \(2 dimensioni\).  Mentre Visual Basic consente che la differenza tra overload consista solo in una di queste modifiche, questo tipo di overload non è conforme con CLS \([Indipendenza del linguaggio e componenti indipendenti dal linguaggio](../Topic/Language%20Independence%20and%20Language-Independent%20Components.md)\).  
  
 Quando si applica l'<xref:System.CLSCompliantAttribute> a un elemento di programmazione, il parametro `isCompliant` dell'attributo viene impostato su `True` o `False` per indicare la compatibilità o la non compatibilità.  L'impostazione predefinita per questo parametro non è disponibile, è necessario quindi specificare un valore.  
  
 Se <xref:System.CLSCompliantAttribute> non viene applicato a un elemento, l'elemento non sarà considerato conforme.  
  
 Per impostazione predefinita, si tratta di un messaggio di avviso.  Per informazioni su come nascondere gli avvisi o considerarli come errori, vedere [Configurazione degli avvisi in Visual Basic](/visual-studio/ide/configuring-warnings-in-visual-basic).  
  
 **ID errore:** BC40035  
  
### Per correggere l'errore  
  
-   Se si desidera la conformità con CLS, definire tra gli overload altre differenze rispetto a quelle elencate in questa pagina della Guida.  
  
-   Se si desidera che le differenze tra gli overload consistano solo nelle modifiche elencate in questa pagina della Guida, rimuovere l'oggetto <xref:System.CLSCompliantAttribute> dalle definizioni o contrassegnare gli overload come `<CLSCompliant(False)>`.  
  
## Vedere anche  
 [\<PAVE OVER\> Writing CLS\-Compliant Code](http://msdn.microsoft.com/it-it/4c705105-69a2-4e5e-b24e-0633bc32c7f3)   
 [Procedure Overloading](../../../visual-basic/programming-guide/language-features/procedures/procedure-overloading.md)   
 [Overloads](../../../visual-basic/language-reference/modifiers/overloads.md)