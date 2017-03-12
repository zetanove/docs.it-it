---
title: "/main | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "main compiler option [Visual Basic]"
  - "/main compiler option [Visual Basic]"
  - "-main compiler option [Visual Basic]"
ms.assetid: 83fc339d-6652-415d-b205-b5133319b5b0
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# /main
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Consente di specificare la classe o il modulo che contiene la routine `Sub Main`.  
  
## Sintassi  
  
```  
/main:location  
```  
  
## Argomenti  
 `location`  
 Obbligatorio.  Nome completo della classe o del modulo che contiene la routine `Sub Main` che dovrà essere chiamata all'avvio del programma.  Può essere nel formato **\/main:module** o **\/main:namespace.module**.  
  
## Note  
 Utilizzare questa opzione per creare un file eseguibile o un programma eseguibile per Windows.  Se si omette l'opzione **\/main**, verrà ricercata una routine `Sub Main` condivisa valida in tutte le classi e i moduli pubblici.  
  
 Per informazioni sulle varie forme della routine `Main`, vedere [Main Procedure in Visual Basic](../../../visual-basic/programming-guide/program-structure/main-procedure.md).  
  
 Quando `location` è una classe che eredita da <xref:System.Windows.Forms.Form>, il compilatore fornisce una routine `Main` predefinita che avvia l'applicazione se la classe non ha la routine `Main`.  In questo modo, è possibile compilare il codice dalla  riga di comando creata nell'ambiente di sviluppo.  
  
 [!code-vb[VbVbalrCompiler#16](../../../visual-basic/reference/command-line-compiler/codesnippet/visualbasic/main_1.vb)]  
  
### Per impostare \/main nell'ambiente di sviluppo integrato di Visual Studio  
  
1.  Selezionare un progetto in **Esplora soluzioni**.  Scegliere **Proprietà** dal menu **Progetto**.  
  
     Per ulteriori informazioni, vedere [Introduction to the Project Designer](http://msdn.microsoft.com/it-it/898dd854-c98d-430c-ba1b-a913ce3c73d7).  
  
2.  Fare clic sulla scheda **Applicazione**.  
  
3.  Assicurarsi che la casella di controllo **Attiva framework applicazione** sia deselezionata.  
  
4.  Modificare il valore nella casella **Oggetto di avvio**.  
  
## Esempio  
 Nel codice seguente vengono compilati `T2.vb` e `T3.vb` e viene specificato che la routine `Sub Main` è reperibile nella classe `Test2`.  
  
```  
vbc t2.vb t3.vb /main:Test2  
```  
  
## Vedere anche  
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)   
 [\/target](../../../visual-basic/reference/command-line-compiler/target.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [NIB: Visual Basic Version of Hello, World](http://msdn.microsoft.com/it-it/9d030b60-e148-4366-a462-69532f02294c)   
 [Main Procedure in Visual Basic](../../../visual-basic/programming-guide/program-structure/main-procedure.md)