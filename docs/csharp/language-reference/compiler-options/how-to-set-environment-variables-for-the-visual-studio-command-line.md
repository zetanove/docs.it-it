---
title: 'Procedura: Impostare le variabili di ambiente per la riga di comando di Visual Studio | Microsoft Docs'
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- cs.build.commandline
dev_langs:
- CSharp
helpviewer_keywords:
- csc.exe, command-line builds
- Visual C#, command-line builds
- command-line compilers, Visual C#
- Vsvars32.bat
- builds [C#], command-line
- compilers, invoking from command line
- Vcvars32.bat file
- command line [C#], building from
- Visual C# compiler, enabling
- compiling source code, from command line
ms.assetid: 7ec09480-5612-4f6a-8d00-ad90ea9bca5d
caps.latest.revision: 15
author: BillWagner
ms.author: wiwagn
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
ms.translationtype: Human Translation
ms.sourcegitcommit: a780a11d8dd238187eb82933359bbb151bb3c333
ms.openlocfilehash: e2cc644bb3b2c51615fe763224505b07e113ad62
ms.contentlocale: it-it
ms.lasthandoff: 05/22/2017

---
# <a name="how-to-set-environment-variables-for-the-visual-studio-command-line"></a>Procedura: Impostare le variabili di ambiente per la riga di comando di Visual Studio
Il file vsvars32.bat imposta le variabili di ambiente necessarie per abilitare le compilazioni da riga di comando. Per altre informazioni su vsvars32.bat, vedere l[articolo della Knowledge Base Q248802](http://go.microsoft.com/fwlink/?LinkId=225042).  
  
 Se la versione corrente di Visual Studio è installata in un computer che include anche la versione precedente di Visual Studio, non eseguire vsvars32.bat o vcvars32.bat da diverse versioni nella stessa finestra del prompt dei comandi.  
  
### <a name="to-run-vsvars32bat"></a>Per eseguire VSVARS32.BAT  
  
1.  Dal menu **Start** aprire il **Prompt dei comandi per gli sviluppatori per VS2012**.  
  
2.  Passare alla sottodirectory di installazione Programmi\Microsoft Visual Studio *Version*\Common7\Tools o Programmi (x86)\Microsoft Visual Studio *Version*\Common7\Tools.  
  
3.  Eseguire VSVARS32.bat digitando **VSVARS32**.  
  
    > [!CAUTION]
    >  Il file VSVARS32.bat può variare da computer a computer. Non sostituire un file VSVARS32.bat mancante o danneggiato con un file VSVARS32.bat da un altro computer. Rieseguire invece l'installazione per sostituire il file mancante.  
  
## <a name="see-also"></a>Vedere anche  
 [Compilazione dalla riga di comando con csc.exe](../../../csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md)
