---
title: "How to: Set Environment Variables for the Visual Studio Command Line | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "cs.build.commandline"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "csc.exe, command-line builds"
  - "Visual C#, command-line builds"
  - "command-line compilers, Visual C#"
  - "Vsvars32.bat"
  - "builds [C#], command-line"
  - "compilers, invoking from command line"
  - "Vcvars32.bat file"
  - "command line [C#], building from"
  - "Visual C# compiler, enabling"
  - "compiling source code, from command line"
ms.assetid: 7ec09480-5612-4f6a-8d00-ad90ea9bca5d
caps.latest.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 15
---
# How to: Set Environment Variables for the Visual Studio Command Line
Il file vsvars32.bat imposta le variabili di ambiente necessarie per abilitare le compilazioni da riga di comando.  Per altre informazioni su vsvars32.bat, vedere l'[articolo della Knowledge Base Q248802](http://go.microsoft.com/fwlink/?LinkId=225042).  
  
 Se la versione corrente di Visual Studio è installata in un computer che include anche la versione precedente di Visual Studio, non eseguire vsvars32.bat o vcvars32.bat da diverse versioni nella stessa finestra del prompt dei comandi.  
  
### Per eseguire VSVARS32.BAT  
  
1.  Dal menu **Start** aprire il **Prompt dei comandi per gli sviluppatori per VS2012**.  
  
2.  Passare alla sottodirectory di installazione Programmi\\Microsoft Visual Studio *Version*\\Common7\\Tools o Programmi \(x86\)\\Microsoft Visual Studio *Version*\\Common7\\Tools.  
  
3.  Eseguire VSVARS32.bat digitando VSVARS32.  
  
    > [!CAUTION]
    >  Il file VSVARS32.bat può variare da computer a computer.  Non sostituire un file VSVARS32.bat mancante o danneggiato con un file VSVARS32.bat da un altro computer.  Rieseguire invece l'installazione per sostituire il file mancante.  
  
## Vedere anche  
 [Command\-line Building With csc.exe](../../../csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md)