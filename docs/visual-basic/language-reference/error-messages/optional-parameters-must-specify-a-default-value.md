---
title: "Optional parameters must specify a default value | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vbc30812"
  - "bc30812"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30812"
ms.assetid: 5091a250-be66-413b-98a3-2a9974c4d600
caps.latest.revision: 10
caps.handback.revision: 10
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Optional parameters must specify a default value
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

I parametri facoltativi devono fornire valori predefiniti da utilizzare se la routine che effettua la chiamata non specifica alcun parametro.  
  
 **ID errore:** BC30812  
  
### Per correggere l'errore  
  
-   Specificare valori predefiniti per i parametri facoltativi, come nell'esempio seguente:  
  
    ```  
    Sub Proc1(ByVal X As Integer,   
          Optional ByVal Y As String = "Default Value")  
       MsgBox("Default argument is: " & Y)  
    End Sub  
    ```  
  
## Vedere anche  
 [Optional](../../../visual-basic/language-reference/modifiers/optional.md)