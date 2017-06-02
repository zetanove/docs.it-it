---
title: "Ilasm.exe (IL Assembler) | Microsoft Docs"
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
  - "MSIL generators"
  - "metadata, MSIL Assembler"
  - "MSIL Assembler"
  - "portable executable files, MSIL Assembler"
  - "PE files, MSIL Assembler"
  - "MSIL"
  - "Ilasm.exe"
  - "verifying MSIL performance"
ms.assetid: 4ca3a4f0-4400-47ce-8936-8e219961c76f
caps.latest.revision: 41
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 41
---
# Ilasm.exe (IL Assembler)
L'assembler IL genera un file eseguibile di tipo PE dal linguaggio intermedio \(IL\). Per altre informazioni su IL, vedere [Processo di esecuzione gestita](../../../docs/standard/managed-execution-process.md). È possibile eseguire il file eseguibile così ottenuto, contenente il codice IL e i metadati necessari, per determinare se il codice IL viene eseguito come previsto.  
  
 Viene installato automaticamente con Visual Studio. Per eseguire lo strumento, usare il prompt dei comandi per sviluppatori o il prompt dei comandi di Visual Studio in Windows 7. Per altre informazioni, vedere [Prompt dei comandi](../../../docs/framework/tools/developer-command-prompt-for-vs.md).  
  
 Al prompt dei comandi digitare quanto segue:  
  
## Sintassi  
  
```  
  
ilasm [options] filename [[options]filename...]  
```  
  
#### Parametri  
  
|Argomento|Descrizione|  
|---------------|-----------------|  
|*filename*|Nome del file di origine .il. Questo file è formato da direttive di dichiarazione di metadati e istruzioni IL simboliche. È possibile fornire più argomenti di file di origine per produrre un unico file PE con Ilasm.exe. **Note:**  Verificare che nell'ultima riga di codice del file di origine con estensione il sia presente uno spazio vuoto finale o un carattere di fine riga.|  
  
|Opzione|Descrizione|  
|-------------|-----------------|  
|**\/32bitpreferred**|Crea un'immagine con preferenza per i 32 bit \(PE32\).|  
|**\/alignment**\=*integer*|Imposta FileAlignment sul valore specificato da *integer* nell'intestazione NT facoltativa. Se la direttiva IL .alignment è specificata nel file, questa opzione ne esegue l'override.|  
|**\/appcontainer**|Genera un file .dll o .exe che viene eseguito nel contenitore delle app Windows, come output.|  
|**\/arm**|Specifica Advanced RISC Machine \(ARM\) come processore di destinazione.<br /><br /> Se non viene specificato il numero di bit dell'immagine, viene utilizzata l'impostazione predefinita **\/32bitpreferred**.|  
|**\/base**\=*integer*|Imposta ImageBase sul valore specificato da *integer* nell'intestazione NT facoltativa. Se la direttiva IL .imagebase è specificata nel file, questa opzione ne esegue l'override.|  
|**\/clock**|Misura e segnala i seguenti tempi di compilazione in millisecondi per il file di origine .il specificato:<br /><br /> **Total Run**: tempo totale impiegato per l'esecuzione di tutte le operazioni specifiche che seguono.<br /><br /> **Startup**: caricamento e apertura del file.<br /><br /> **Emitting MD**: emissione di metadati.<br /><br /> **Ref to Def Resolution**: risoluzione dei riferimenti nelle definizioni nel file.<br /><br /> **CEE File Generation**: generazione dell'immagine del file in memoria.<br /><br /> **PE File Writing**: scrittura dell'immagine in un file PE.|  
|**\/debug**\[\=`IMPL`&#124;`OPT`\]|Include informazioni di debug \(nomi di variabili locali e di argomenti e numeri di riga\). Crea un file PDB.<br /><br /> Se si specifica **\/debug** senza altri valori, viene disabilitata l'ottimizzazione JIT e vengono utilizzati i punti di sequenza dal file PDB.<br /><br /> **IMPL** disabilita l'ottimizzazione JIT e utilizza punti di sequenza impliciti.<br /><br /> **OPT** abilita l'ottimizzazione JIT e utilizza punti di sequenza impliciti.|  
|**\/dll**|Produce un file .dll come output.|  
|**\/enc**\=`file`|Crea file differenziali di Modifica e continuazione a partire dal file di origine specificato.<br /><br /> Questo argomento è esclusivamente per utilizzo didattico e non è supportato per un utilizzo commerciale.|  
|**\/exe**|Produce un file eseguibile come output. Questa è l'impostazione predefinita.|  
|**\/flags**\=*integer*|Imposta ImageFlags sul valore specificato da *integer* nell'intestazione Common Language Runtime. Se la direttiva IL .corflags è specificata nel file, questa opzione ne esegue l'override. Per un elenco di valori validi per *integer*, vedere CorHdr.h, COMIMAGE\_FLAGS.|  
|**\/fold**|Raggruppa corpi di metodo identici in uno solo.|  
|\/**highentropyva**|Genera in output un file eseguibile che supporta ASLR \(Address Space Layout Randomization\) a entropia elevata. Impostazione predefinita per **\/appcontainer**.|  
|**\/include**\=`includePath`|Imposta un percorso per la ricerca di file inclusi con `#include`.|  
|**\/itanium**|Specifica Intel Itanium come processore di destinazione.<br /><br /> Se non viene specificato il numero di bit dell'immagine, viene utilizzata l'impostazione predefinita **\/pe64**.|  
|**\/key:** *keyFile*|Compila *filename*con una firma sicura usando la chiave privata contenuta in *keyFile*.|  
|**\/key:@** *keySource*|Compila *filename*con una firma sicura usando la chiave privata prodotta in *keySource*.|  
|**\/listing**|Produce un file di elenco sull'output standard. Se si omette questa opzione, non verrà prodotto alcun file di elenco.<br /><br /> Questo parametro non è supportato in .NET Framework 2.0 o versione successiva.|  
|**\/mdv**\=`versionString`|Imposta la stringa di versione dei metadati.|  
|**\/msv**\=`major``.``minor`|Imposta la versione del flusso di metadati, dove `major` e `minor` sono numeri interi.|  
|**\/noautoinherit**|Disabilita l'ereditarietà predefinita da <xref:System.Object> quando non è specificata alcuna classe base.|  
|**\/nocorstub**|Elimina la generazione dello stub CORExeMain.|  
|**\/nologo**|Evita la visualizzazione del messaggio di avvio Microsoft.|  
|**\/output:** *22*|Specifica il nome e l'estensione del file di output. Per impostazione predefinita, il nome del file di output corrisponde al nome del primo file di origine. L'estensione predefinita è .exe. Se si specifica l'opzione **\/dll**, l'estensione predefinita sarà .dll. **Note:**  Se si specifica **\/output:**myfile.dll, non viene impostata l'opzione **\/dll**. Se non si specifica **\/dll**, si otterrà un file eseguibile denominato myfile.dll.|  
|**\/optimize**|Ottimizza le istruzioni long convertendole in short. Ad esempio, `br` viene convertito in `br.s`.|  
|**\/pe64**|Crea un'immagine a 64 bit \(PE32\+\).<br /><br /> Se non è specificato il processore di destinazione, l'impostazione predefinita è `/itanium`.|  
|**\/pdb**|Crea un file PDB senza abilitare la traccia delle informazioni di debug.|  
|**\/quiet**|Specifica la modalità non interattiva. Non visualizza informazioni sullo stato dell'assembly.|  
|**\/resource:** *file.res*|Include il file di risorse, specificato in formato \*.res, nel file .exe o .dll risultante. È possibile specificare un unico file .res con l'opzione **\/resource**.|  
|**\/ssver**\=`int`.`int`|Imposta il numero di versione del sottosistema nell'intestazione NT facoltativa. Per **\/appcontainer** e **\/arm** il numero minimo di versione è 6.02.|  
|**\/stack**\=`stackSize`|Imposta su `stackSize` il valore di SizeOfStackReserve nell'intestazione NT facoltativa.|  
|**\/stripreloc**|Specifica che non sono necessarie rilocazioni di base.|  
|**\/subsystem**\=*integer*|Imposta il sottosistema sul valore specificato da *integer* nell'intestazione NT facoltativa. Se la direttiva IL .subsystem è specificata nel file, questo comando ne esegue l'override. Per un elenco di valori validi per *integer*, vedere winnt.h, IMAGE\_SUBSYSTEM.|  
|**\/x64**|Specifica un processore AMD a 64 bit come processore di destinazione.<br /><br /> Se non viene specificato il numero di bit dell'immagine, viene utilizzata l'impostazione predefinita **\/pe64**.|  
|**\/?**|Visualizza la sintassi e le opzioni di comando dello strumento.|  
  
> [!NOTE]
>  Tutte le opzioni di Ilasm.exe non sono soggette alla distinzione tre maiuscole e minuscole e vengono riconosciute dalle prime tre lettere. Ad esempio, **\/lis** è equivalente a **\/listing** e **\/res:**myresfile.res è equivalente a **\/resource:**myresfile.res. Le opzioni che specificano argomenti accettano i due punti \(:\) o un segno di uguale \(\=\) come separatore tra l'opzione e l'argomento.**\/output:** *file.ext*, ad esempio, equivale a **\/output\=** *file.ext*.  
  
## Note  
 L'assembler IL consente ai fornitori di strumenti di progettare e implementare generatori IL. Grazie a Ilasm.exe, gli sviluppatori di strumenti e compilatori possono concentrarsi su IL e sulla generazione di metadati senza doversi preoccupare di emettere IL nel formato di file PE.  
  
 Analogamente ad altri compilatori destinati al runtime, quali C\# e Visual Basic, Ilasm.exe non produce file oggetto intermedi e non richiede alcuna fase di collegamento per creare un file PE.  
  
 L'assembler IL è in grado di esprimere tutte le funzionalità esistenti per IL e i metadati dei linguaggi di programmazione destinati al runtime. In questo modo il codice gestito scritto in uno qualsiasi di questi linguaggi di programmazione può essere espresso nell'assembler IL e compilato con Ilasm.exe in modo appropriato.  
  
> [!NOTE]
>  È possibile che la compilazione abbia esito negativo se nell'ultima riga di codice del file di origine con estensione il non è presente uno spazio vuoto finale o un carattere di fine riga.  
  
 È possibile utilizzare Ilasm.exe unitamente allo strumento complementare [Ildasm.exe](../../../docs/framework/tools/ildasm-exe-il-disassembler.md). Ildasm.exe accetta un file PE contenente codice IL e crea un file di testo adatto come input per Ilasm.exe. Questo è utile, ad esempio, quando si compila codice in un linguaggio di programmazione che non supporta tutti gli attributi dei metadati del runtime. Dopo aver compilato il codice ed eseguito l'output tramite Ildasm.exe, il file di testo IL ottenuto potrà essere modificato manualmente per aggiungere gli attributi mancanti. Sarà quindi possibile elaborare questo file di testo mediante Ilasm.exe per produrre un file eseguibile finale.  
  
 È inoltre possibile ricorrere a questa tecnica per produrre un unico file PE sulla base di più file PE generati da diversi compilatori.  
  
> [!NOTE]
>  Attualmente non è possibile avvalersi di questa tecnica con file PE contenenti codice nativo incorporato, ad esempio file PE prodotti da Visual C\+\+.  
  
 Per fare in modo che l'utilizzo combinato di Ildasm.exe e Ilasm.exe risulti il più accurato possibile, per impostazione predefinita l'assembler non sostituisce le codifiche short con quelle long che potrebbero essere state scritte nelle origini IL \(o che potrebbero essere state emesse da un altro compilatore\). Utilizzare l'opzione **\/optimize** per sostituire le codifiche short quando possibile.  
  
> [!NOTE]
>  Ildasm.exe opera solo su file su disco e non su file installati nella Global Assembly Cache.  
  
 Per ulteriori informazioni sulla grammatica di IL, vedere il file asmparse.grammar in [!INCLUDE[winsdklong](../../../includes/winsdklong-md.md)].  
  
## Informazioni sulla versione  
 A partire da [!INCLUDE[net_v45](../../../includes/net-v45-md.md)], è possibile associare un attributo personalizzato a un'implementazione di interfaccia utilizzando codice analogo al seguente:  
  
```  
.class interface public abstract auto ansi IMyInterface { .method public hidebysig newslot abstract virtual instance int32 method1() cil managed { } // end of method IMyInterface::method1 } // end of class IMyInterface .class public auto ansi beforefieldinit MyClass extends [mscorlib]System.Object implements IMyInterface { .interfaceimpl type IMyInterface .custom instance void [mscorlib]System.Diagnostics.DebuggerNonUserCodeAttribute::.ctor() = ( 01 00 00 00 ) …  
  
```  
  
 A partire da [!INCLUDE[net_v45](../../../includes/net-v45-md.md)], è possibile specificare un marshalling BLOB \(oggetto binario di grandi dimensioni\) arbitrario utilizzando la relativa rappresentazione binaria non elaborata, come illustrato nel codice seguente:  
  
```  
.method public hidebysig abstract virtual instance void marshal({ 38 01 02 FF }) Test(object A_1) cil managed  
  
```  
  
 Per ulteriori informazioni sulla grammatica di IL, vedere il file asmparse.grammar in [!INCLUDE[winsdklong](../../../includes/winsdklong-md.md)].  
  
## Esempi  
 Il comando che segue assembla il file IL `myTestFile.il` e produce l'eseguibile `myTestFile.exe.`  
  
```  
ilasm myTestFile  
```  
  
 Il comando che segue assembla il file IL `myTestFile.il` e produce il file .dll `myTestFile.dll`.  
  
```  
ilasm myTestFile /dll   
```  
  
 Il comando che segue assembla il file IL `myTestFile.il` e produce il file .dll `myNewTestFile.dll`.  
  
```  
ilasm myTestFile /dll /output:myNewTestFile.dll  
```  
  
 L'esempio di codice seguente illustra un'applicazione molto semplice che visualizza "Hello World\!" nella console.  È possibile compilare questo codice e quindi utilizzare lo strumento [Ildasm.exe](../../../docs/framework/tools/ildasm-exe-il-disassembler.md) per generare un file IL.  
  
```csharp  
using System; public class Hello { public static void Main(String[] args) { Console.WriteLine("Hello World!"); } }  
```  
  
 L'esempio di codice IL riportato di seguito corrisponde al precedente esempio di codice C\#.  È possibile compilare questo codice in un assembly mediante lo strumento IL Assembler.  Gli esempi di codice IL e C\# visualizzano entrambi "Hello World\!" nella console.  
  
```  
// Metadata version: v2.0.50215 .assembly extern mscorlib { .publickeytoken = (B7 7A 5C 56 19 34 E0 89 )                         // .z\V.4.. .ver 2:0:0:0 } .assembly sample { .custom instance void [mscorlib]System.Runtime.CompilerServices.CompilationRelaxationsAttribute::.ctor(int32) = ( 01 00 08 00 00 00 00 00 ) .hash algorithm 0x00008004 .ver 0:0:0:0 } .module sample.exe // MVID: {A224F460-A049-4A03-9E71-80A36DBBBCD3} .imagebase 0x00400000 .file alignment 0x00000200 .stackreserve 0x00100000 .subsystem 0x0003       // WINDOWS_CUI .corflags 0x00000001    //  ILONLY // Image base: 0x02F20000 // =============== CLASS MEMBERS DECLARATION =================== .class public auto ansi beforefieldinit Hello extends [mscorlib]System.Object { .method public hidebysig static void  Main(string[] args) cil managed { .entrypoint // Code size       13 (0xd) .maxstack  8 IL_0000:  nop IL_0001:  ldstr      "Hello World!" IL_0006:  call       void [mscorlib]System.Console::WriteLine(string) IL_000b:  nop IL_000c:  ret } // end of method Hello::Main .method public hidebysig specialname rtspecialname instance void  .ctor() cil managed { // Code size       7 (0x7) .maxstack  8 IL_0000:  ldarg.0 IL_0001:  call       instance void [mscorlib]System.Object::.ctor() IL_0006:  ret } // end of method Hello::.ctor } // end of class Hello  
```  
  
## Vedere anche  
 [Tools](../../../docs/framework/tools/index.md)   
 [Ildasm.exe \(IL Disassembler\)](../../../docs/framework/tools/ildasm-exe-il-disassembler.md)   
 [Processo di esecuzione gestita](../../../docs/standard/managed-execution-process.md)   
 [Prompt dei comandi](../../../docs/framework/tools/developer-command-prompt-for-vs.md)