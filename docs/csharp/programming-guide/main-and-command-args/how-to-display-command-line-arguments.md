---
title: "Procedura: visualizzare gli argomenti della riga di comando (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "argomenti della riga di comando [C#], visualizzazione"
ms.assetid: b8479f2d-9e05-4d38-82da-2e61246e5437
caps.latest.revision: 19
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 19
---
# Procedura: visualizzare gli argomenti della riga di comando (Guida per programmatori C#)
Gli argomenti forniti per un file eseguibile sulla riga di comando sono accessibili tramite un parametro facoltativo a `Main`.  Gli argomenti vengono forniti sotto forma di una matrice di stringhe.  Ogni elemento della matrice contiene un solo argomento.  Gli spazi tra gli argomenti vengono rimossi.  Si considerino ad esempio le seguenti chiamate della riga di comando di un file eseguibile fittizio:  
  
|Input sulla riga di comando|Matrice di stringhe passate a Main|  
|---------------------------------|----------------------------------------|  
|**executable.exe a b c**|"a"<br /><br /> "b"<br /><br /> "c"|  
|**executable.exe one two**|"one"<br /><br /> "two"|  
|**executable.exe "one two" three**|"one two"<br /><br /> "three"|  
  
> [!NOTE]
>  Quando si esegue un'applicazione in Visual Studio, è possibile specificare gli argomenti della riga di comando nella [Pagina Debug, Progettazione progetti](/visual-studio/ide/reference/debug-page-project-designer).  
  
## Esempio  
 In questo esempio vengono visualizzati gli argomenti della riga di comando passati a un'applicazione della riga di comando.  L'output illustrato è relativo alla prima voce della tabella precedente.  
  
 [!code-cs[csProgGuideMain#9](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/how-to-display-command-line-arguments_1.cs)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Command\-line Building With csc.exe](../../../csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md)   
 [Main\(\) e argomenti della riga di comando](../../../csharp/programming-guide/main-and-command-args/main-and-command-line-arguments.md)   
 [Procedura: accedere agli argomenti della riga di comando utilizzando foreach](../../../csharp/programming-guide/main-and-command-args/how-to-access-command-line-arguments-using-foreach.md)   
 [Valori restituiti da Main\(\)](../../../csharp/programming-guide/main-and-command-args/main-return-values.md)