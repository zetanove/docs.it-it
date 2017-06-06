---
title: "Assembly su più file | Microsoft Docs"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-bcl
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- assemblies [.NET Framework], multifile
- entry point for assembly
- compiling assemblies
- command-line compilers
- assembly manifest, multifile assemblies
- code modules
- multifile assemblies
ms.assetid: 13509e73-db77-4645-8165-aad8dfaedff6
caps.latest.revision: 9
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: Machine Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 0521e3bcfc7ed4e58434bacf36b43840647ddf50
ms.contentlocale: it-it
ms.lasthandoff: 06/02/2017

---
# <a name="multifile-assemblies"></a>Assembly su più file
È possibile creare assembly su più file usando i compilatori da riga di comando o [!INCLUDE[vsprvslong](../../../includes/vsprvslong-md.md)] con Visual C++. Un file all'interno dell'assembly deve contenere il manifesto dell'assembly. Un assembly che avvia un'applicazione deve inoltre contenere un punto di ingresso, ad esempio un metodo Main o WinMain.  
  
 Ad esempio, si supponga di avere un'applicazione contenente due moduli di codice, Client.cs e Stringer.cs. Stringer.cs crea lo spazio dei nomi `myStringer` a cui fa riferimento il codice in Client.cs. Client.cs contiene il metodo `Main`, che è il punto di ingresso dell'applicazione. In questo esempio vengono compilati i due moduli di codice e quindi viene creato un terzo file contenente il manifesto dell'assembly che avvia l'applicazione. Il manifesto dell'assembly fa riferimento a entrambi i moduli `Client` e `Stringer`.  
  
> [!NOTE]
>  Negli assembly su più file può essere presente un solo punto di ingresso, anche se l'assembly include più moduli di codice.  
  
 La scelta di creare un assembly su più file può essere consigliabile per varie ragioni:  
  
-   Per combinare moduli scritti in linguaggi diversi. Questo è il motivo più comune per la creazione di un assembly su più file.  
  
-   Per ottimizzare il download di un'applicazione inserendo i tipi usati raramente in un modulo che verrà scaricato solo quando necessario.  
  
    > [!NOTE]
    >  Se si creano applicazioni che verranno scaricate usando il tag `<object>` con Microsoft Internet Explorer, è importante creare assembly su più file. In questo scenario occorrerà creare un file separato dai moduli di codice che contenga solo il manifesto dell'assembly. Internet Explorer scarica prima il manifesto dell'assembly e quindi crea i thread di lavoro per scaricare altri moduli o assembly eventualmente necessari. Durante il download del file che contiene il manifesto dell'assembly, Internet Explorer non risponde all'input dell'utente. Tanto minori saranno le dimensioni del file contenente il manifesto dell'assembly, tanto più breve sarà il tempo in cui Internet Explorer non risponderà.  
  
-   Per combinare moduli di codice scritti da più sviluppatori. Sebbene ogni sviluppatore possa compilare ogni modulo di codice in un assembly, questa operazione può forzare l'esposizione pubblica di alcuni tipi che non sarebbero esposti se tutti i moduli venissero inclusi in un assembly su più file.  
  
 Dopo aver creato l'assembly, è possibile firmare il file che contiene il manifesto dell'assembly (e quindi l'assembly) oppure è possibile assegnare un nome sicuro al file (e all'assembly) e inserirlo nella Global Assembly Cache.  
  
## <a name="see-also"></a>Vedere anche  
 [Procedura: Compilare un assembly su più file](../../../docs/framework/app-domains/how-to-build-a-multifile-assembly.md)   
 [Programmazione con gli assembly](../../../docs/framework/app-domains/programming-with-assemblies.md)
