---
title: "How to: Access Members of an Object (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
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
  - "members, accessing"
  - "object variables, accessing members"
ms.assetid: a0072514-6a79-4dd6-8d03-ca8c13e61ddc
caps.latest.revision: 20
caps.handback.revision: 20
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# How to: Access Members of an Object (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Quando si utilizza una variabile oggetto che fa riferimento a un oggetto, è spesso necessario accedere ai membri di tale oggetto, ad esempio metodi, proprietà, campi ed eventi.  Ad esempio, dopo aver creato un nuovo oggetto <xref:System.Windows.Forms.Form>, può essere necessario impostarne la proprietà <xref:System.Windows.Forms.Control.Text%2A> o chiamare il metodo <xref:System.Windows.Forms.Control.Focus%2A>.  
  
## Accesso ai membri  
 Per accedere ai membri di un oggetto è necessario utilizzare la variabile che fa riferimento all'oggetto.  
  
#### Per accedere ai membri di un oggetto  
  
-   Utilizzare l'operatore di accesso ai membri \(`.`\) tra il nome della variabile oggetto e il nome del membro.  
  
    ```  
    currentText = newForm.Text  
    ```  
  
     Se il membro è [Shared](../../../../visual-basic/language-reference/modifiers/shared.md), non è necessario utilizzare una variabile per accedere al membro.  
  
## Accesso ai membri di un oggetto di tipo conosciuto  
 Se il tipo di un oggetto è noto in fase di compilazione, è possibile utilizzare l'*associazione anticipata* per una variabile che fa riferimento a tale oggetto.  
  
#### Per accedere ai membri di un oggetto di cui si conosce il tipo in fase di compilazione  
  
1.  Dichiarare la variabile oggetto con lo stesso tipo dell'oggetto che si intende assegnare alla variabile.  
  
    ```  
    Dim extraForm As System.Windows.Forms.Form   
    ```  
  
     Con `Option Strict On` è possibile assegnare soltanto oggetti <xref:System.Windows.Forms.Form> \(oppure oggetti di un tipo derivato da <xref:System.Windows.Forms.Form>\) a `extraForm`.  Se è stata definita una classe o una struttura con una conversione `CType` di ampliamento in <xref:System.Windows.Forms.Form>, è anche possibile assegnare la classe o la struttura a `extraForm`.  
  
2.  Utilizzare l'operatore di accesso ai membri \(`.`\) tra il nome della variabile oggetto e il nome del membro.  
  
    ```  
    extraForm.Show()  
    ```  
  
     È possibile accedere a tutti i metodi e le proprietà specifici della classe <xref:System.Windows.Forms.Form>, indipendentemente dall'impostazione di `Option Strict`.  
  
## Accesso ai membri di un oggetto di tipo sconosciuto  
 Se il tipo di un oggetto non è noto in fase di compilazione, è necessario utilizzare l'*associazione tardiva* per qualsiasi variabile che fa riferimento a tale oggetto.  
  
#### Per accedere ai membri di un oggetto di cui non si conosce il tipo in fase di compilazione  
  
1.  Dichiarare la variabile oggetto con il [Object Data Type](../../../../visual-basic/language-reference/data-types/object-data-type.md).  La dichiarazione di una variabile come `Object` equivale alla dichiarazione della variabile come <xref:System.Object?displayProperty=fullName>.  
  
    ```  
    Dim someControl As Object   
    ```  
  
     Con `Option Strict On` è possibile accedere soltanto ai membri definiti sulla classe <xref:System.Object>.  
  
2.  Utilizzare l'operatore di accesso ai membri \(`.`\) tra il nome della variabile oggetto e il nome del membro.  
  
    ```  
    someControl.GetType()  
    ```  
  
     Per poter accedere ai membri di qualsiasi oggetto assegnato alla variabile oggetto, è necessario impostare `Option Strict Off`.  In questo caso, il compilatore non può garantire che un dato membro sia esposto dall'oggetto assegnato alla variabile.  Se l'oggetto non espone un membro a cui si tenta di accedere, si verificherà un'eccezione <xref:System.MemberAccessException>.  
  
## Vedere anche  
 <xref:System.Object>   
 <xref:System.Windows.Forms.Form>   
 <xref:System.MemberAccessException>   
 [Object Variables](../../../../visual-basic/programming-guide/language-features/variables/object-variables.md)   
 [Object Variable Declaration](../../../../visual-basic/programming-guide/language-features/variables/object-variable-declaration.md)   
 [Object Data Type](../../../../visual-basic/language-reference/data-types/object-data-type.md)   
 [Option Strict Statement](../../../../visual-basic/language-reference/statements/option-strict-statement.md)