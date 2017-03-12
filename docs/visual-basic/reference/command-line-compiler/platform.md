---
title: "/platform (Visual Basic) | Microsoft Docs"
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
  - "platform compiler option [Visual Basic]"
  - "/platform compiler option [Visual Basic]"
  - "-platform compiler option [Visual Basic]"
ms.assetid: f9bc61e6-e854-4ae1-87b9-d6244de23fd1
caps.latest.revision: 34
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 34
---
# /platform (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Consente di specificare la versione di Common Language Runtime \(CLR\) in grado di eseguire il file di output.  
  
## Sintassi  
  
```  
/platform:{ x86 | x64 | Itanium | arm | anycpu | anycpu32bitpreferred }  
```  
  
## Argomenti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`x86`|Compila l'assembly in modo da essere eseguito da CLR a 32 bit, compatibile con x86.|  
|`x64`|Compila l'assembly l'assemby in modo da essere eseguito da CLR a 64 bit su un computer che supporta il set di istruzioni AMD64 o EM64T.|  
|`Itanium`|Compila l'assembly in modo da essere eseguito da CLR a 64 bit su un computer dotato di processore Itanium.|  
|`arm`|Compila l'assembly in modo da essere eseguito su un computer con processore ARM \(Advanced RISC Machine\).|  
|`anycpu`|Compila l'assembly in modo da essere eseguito su qualsiasi piattaforma.  L'applicazione verrà eseguita come applicazione a 32 bit su versioni di Windows a 32 bit e come applicazione a 64 bit su versioni di Windows a 64 bit.  Questo flag è il valore predefinito.|  
|`anycpu32bitpreferred`|Compila l'assembly in modo da essere eseguito su qualsiasi piattaforma.  L'applicazione verrà eseguita come applicazione a 32 bit sia nelle versioni di Windows a 32 bit che in quelle a 64 bit.  Questo flag è valido solo per i file eseguibili \(EXE\) e richiede [!INCLUDE[net_v45](../../../csharp/language-reference/compiler-options/includes/net-v45-md.md)].|  
  
## Note  
 Per specificare il tipo di processore di destinazione del file di output, usare l'opzione `/platform`.  
  
 In genere, gli assembly .NET Framework scritti in Visual Basic vengono sempre eseguiti, indipendentemente dalla piattaforma.  L'elaborazione di alcuni elementi può tuttavia risultare influenzata dalla piattaforma in uso.  I casi più comuni sono:  
  
-   Strutture contenenti membri che cambiano dimensione in base alla piattaforma, ad esempio tutti i tipi puntatore.  
  
-   Operazioni aritmetiche che includono dimensioni costanti.  
  
-   Dichiarazioni pInvoke o COM non corrette che usano `Integer` anziché <xref:System.IntPtr> per gli handle.  
  
-   Casting di <xref:System.IntPtr> su `Integer`.  
  
-   Uso dell'interoperabilità pInvoke o COM con componenti non disponibili in tutte le piattaforme.  
  
 Specificando l'opzione **\/platform** sarà possibile limitare alcuni problemi, se si tengono presenti le premesse relative all'architettura su cui verrà eseguito il codice.  In particolare:  
  
-   Se si specifica l'opzione per una piattaforma a 64 bit e l'applicazione viene eseguita su un computer a 32 bit, il messaggio di errore verrà visualizzato con maggiore anticipo e sarà maggiormente descrittivo del problema specifico rispetto all'errore che si verifica senza usare questa opzione.  
  
-   Se si imposta il flag `x86` e successivamente si usa un computer a 64 bit per l'elaborazione dell'applicazione, questa verrà eseguita nel sottosistema WOW e non a livello nativo.  
  
 In un sistema operativo Windows a 64 bit:  
  
-   Gli assembly compilati con l'opzione `/platform:x86` potranno essere eseguiti da CLR a 32 bit in WOW64.  
  
-   Gli eseguibili compilati con l'opzione `/platform:anycpu` potranno essere eseguiti da CLR a 64 bit.  
  
-   Una DLL compilata con l'opzione `/platform:anycpu` potrà essere eseguita dallo stesso CLR del processo in cui viene caricata.  
  
-   Gli eseguibili compilati con l'opzione `/platform:anycpu32bitpreferred` potranno essere eseguiti da CLR a 32 bit.  
  
 Per altre informazioni sullo sviluppo di un'applicazione eseguibile in un sistema operativo Windows a 64 bit, vedere [Applicazioni a 64 bit](../Topic/64-bit%20Applications.md).  
  
### Per impostare \/platform nell'IDE di Visual Studio  
  
1.  Selezionare il progetto in **Esplora soluzioni** e scegliere **Proprietà** dal menu **Progetto**.  
  
     Per altre informazioni, vedere [NIB: Managing Project Properties with the Project Designer](http://msdn.microsoft.com/it-it/983f3c18-832f-4666-afec-74b716ff3e0e).  
  
2.  Nella scheda **Compila** selezionare o deselezionare la casella di controllo **Preferisci 32 bit** oppure scegliere un valore nell'elenco **CPU di destinazione**.  
  
     Per altre informazioni, vedere [Compilazione \(pagina\), Creazione progetti \(Visual Basic\)](/visual-studio/ide/reference/compile-page-project-designer-visual-basic).  
  
## Esempio  
 L'esempio seguente mostra come usare l'opzione del compilatore `/platform`.  
  
```  
vbc /platform:x86 myFile.vb  
```  
  
## Vedere anche  
 [\/target](../../../visual-basic/reference/command-line-compiler/target.md)   
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)