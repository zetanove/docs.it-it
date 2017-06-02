---
title: "How to: Compile Conditionally with Trace and Debug | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "trace compiler options"
  - "trace statements"
  - "compiling source code, trace statements"
  - "tracing [.NET Framework], enabling or disabling"
  - "tracing [.NET Framework], compiling conditionally"
  - "TRACE directive"
  - "conditional compilation, tracing code"
ms.assetid: 56d051c3-012c-42c1-9a58-7270edc624aa
caps.latest.revision: 11
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 11
---
# How to: Compile Conditionally with Trace and Debug
Quando si sottopone a debug l'applicazione durante la fase di sviluppo, sia l'output di tracciatura che l'output di debug vengono inviati alla finestra di output in Visual Studio.  Tuttavia, per includere funzionalità di tracciatura in un'applicazione distribuita, è necessario compilare le applicazioni instrumentate con la direttiva del compilatore **TRACE** attivata.  In questo modo è possibile tracciare il codice da compilare nella versione di rilascio dell'applicazione.  Se non si attiva la direttiva **TRACE**, tutto il codice di tracciatura verrà ignorato durante la compilazione e non sarà incluso nel codice eseguibile da distribuire.  
  
 Sia i metodi di debug che di tracciatura sono dotati di attributi condizionali associati.  Se, ad esempio, l'attributo condizionale per la tracciatura è **true**, tutte le istruzioni di traccia verranno incluse all'interno di un assembly, cioè un file EXE o DLL compilato. Se l'attributo condizionale **Trace** è **false**, le istruzioni di traccia non verranno incluse.  
  
 In una build è possibile attivare uno degli attributi condizionali **Trace** o **Debug**, entrambi gli attributi o nessuno.  Esistono quindi quattro tipi di build: **Debug**, **Trace**, entrambi o nessuno.  Alcune build di rilascio per la distribuzione della produzione non contengono alcun attributo.  
  
 Le impostazioni del compilatore per l'applicazione possono essere specificate in diversi modi:  
  
-   Pagine delle proprietà  
  
-   Riga di comando  
  
-   **\#CONST** \(per Visual Basic\) e **\#define** \(per C\#\)  
  
### Per modificare le impostazioni di compilazione dalla finestra di dialogo delle pagine delle proprietà  
  
1.  Fare clic con il pulsante destro del mouse sul nodo progetto in **Esplora soluzioni**.  
  
2.  Scegliere **Proprietà** dal menu di scelta rapida.  
  
    -   In Visual Basic fare clic sulla scheda **Compila** nel riquadro sinistro della pagina delle proprietà, quindi fare clic sul pulsante **Opzioni di compilazione avanzate** per visualizzare la finestra di dialogo **Impostazioni del compilatore avanzate**.  Selezionare le caselle di controllo per le impostazioni del compilatore che si vogliono attivare.  Deselezionare le caselle di controllo per le impostazioni che si vogliono disabilitare.  
  
    -   In C\# fare clic sulla scheda **Compila** nel riquadro sinistro della pagina delle proprietà, quindi selezionare le caselle di controllo per le impostazioni del compilatore che si vogliono attivare.  Deselezionare le caselle di controllo per le impostazioni che si vogliono disabilitare.  
  
### Per compilare il codice instrumentato usando la riga di comando  
  
1.  Impostare un'opzione del compilatore condizionale sulla riga di comando.  Il compilatore includerà il codice di traccia o di debug nell'eseguibile.  
  
     Ad esempio, l'istruzione del compilatore che segue, immessa sulla riga di comando, includerà il codice di tracciatura in un eseguibile compilato:  
  
     Per Visual Basic: **vbc \/r:System.dll \/d:TRACE\=TRUE \/d:DEBUG\=FALSE MyApplication.vb**  
  
     Per C\#: **csc \/r:System.dll \/d:TRACE \/d:DEBUG\=FALSE MyApplication.cs**  
  
    > [!TIP]
    >  Per compilare più file dell'applicazione, lasciare uno spazio vuoto tra i nomi dei file, ad esempio: **MyApplication1.vb MyApplication2.vb MyApplication3.vb** o **MyApplication1.cs MyApplication2.cs MyApplication3.cs**.  
  
     Il significato delle direttive di compilazione condizionale usate nell'esempio precedente è riportato di seguito:  
  
    |Direttiva|Significato|  
    |---------------|-----------------|  
    |`vbc`|Visual Basic \(compilatore\)|  
    |`csc`|Compilatore C\#|  
    |`/r:`|Riferimenti a un assembly esterno \(EXE o DLL\)|  
    |`/d:`|Definizione di un simbolo di compilazione condizionale|  
  
    > [!NOTE]
    >  È necessario scrivere TRACE o DEBUG con le lettere maiuscole.  Per altre informazioni sui comandi di compilazione condizionale, immettere `vbc /?` \(per Visual Basic\) o `csc /?` \(per C\#\) al prompt dei comandi.  Per altre informazioni, vedere [Compilazione dalla riga di comando](../Topic/How%20to:%20Set%20Environment%20Variables%20for%20the%20Visual%20Studio%20Command%20Line.md) \(C\#\) o [Utilizzo del compilatore dalla riga di comando](../Topic/How%20to:%20Invoke%20the%20Command-Line%20Compiler%20\(Visual%20Basic\).md) \(Visual Basic\).  
  
### Per eseguire la compilazione condizionale con \#CONST o \#define  
  
1.  Digitare l'istruzione adatta per il linguaggio di programmazione usato all'inizio del file di codice sorgente.  
  
    |Linguaggio|Istruzione|Risultato|  
    |----------------|----------------|---------------|  
    |**Visual Basic**|**\#CONST TRACE \= true**|Abilita la traccia|  
    ||**\#CONST TRACE \= false**|Disabilita la traccia|  
    ||**\#CONST DEBUG \= true**|Attiva il debug|  
    ||**\#CONST DEBUG \= false**|Disabilita il debug|  
    |**C\#**|**\#define TRACE**|Abilita la traccia|  
    ||**\#undef TRACE**|Disabilita la traccia|  
    ||**\#define DEBUG**|Attiva il debug|  
    ||**\#undef DEBUG**|Disabilita il debug|  
  
### Per disabilitare la traccia o il debug  
  
1.  Eliminare la direttiva del compilatore dal codice sorgente.  
  
     \-oppure\-  
  
2.  Impostare come commento la direttiva del compilatore.  
  
    > [!NOTE]
    >  Al momento di avviare la compilazione è possibile scegliere **Compila** dal menu **Compila** o usare il metodo della riga di comando senza digitare **d:** per definire i simboli di compilazione condizionale.  
  
## Vedere anche  
 [Tracing and Instrumenting Applications](../../../docs/framework/debug-trace-profile/tracing-and-instrumenting-applications.md)   
 [How to: Create, Initialize and Configure Trace Switches](../../../docs/framework/debug-trace-profile/how-to-create-initialize-and-configure-trace-switches.md)   
 [Trace Switches](../../../docs/framework/debug-trace-profile/trace-switches.md)   
 [Trace Listeners](../../../docs/framework/debug-trace-profile/trace-listeners.md)   
 [How to: Add Trace Statements to Application Code](../../../docs/framework/debug-trace-profile/how-to-add-trace-statements-to-application-code.md)   
 [How to: Set Environment Variables for the Visual Studio Command Line](../Topic/How%20to:%20Set%20Environment%20Variables%20for%20the%20Visual%20Studio%20Command%20Line.md)   
 [How to: Invoke the Command\-Line Compiler](../Topic/How%20to:%20Invoke%20the%20Command-Line%20Compiler%20\(Visual%20Basic\).md)