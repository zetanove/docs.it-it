---
title: "C# Compiler Options Listed by Category | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
  - "CSharp"
helpviewer_keywords: 
  - "Visual C# compiler, options listed by category"
  - "compiler options [C#], listed by category"
  - "Visual C#, compiler options listed by category"
ms.assetid: 96437ecc-6502-4cd3-b070-e9386a298e83
caps.latest.revision: 17
caps.handback.revision: 17
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# C# Compiler Options Listed by Category
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Le seguenti opzioni del compilatore sono ordinate per categoria.  Per un elenco alfabetico, vedere [Opzioni del compilatore C\# in ordine alfabetico](../../../csharp/language-reference/compiler-options/listed-alphabetically.md).  
  
### Ottimizzazione  
  
|Opzione|Scopo|  
|-------------|-----------|  
|[\/filealign](../../../csharp/language-reference/compiler-options/filealign-compiler-option.md)|Specifica le dimensioni delle sezioni nel file di output.|  
|[\/optimize](../../../csharp/language-reference/compiler-options/optimize-compiler-option.md)|Abilita\/Disabilita le ottimizzazioni.|  
  
### File di output  
  
|Opzione|Scopo|  
|-------------|-----------|  
|[\/doc](../../../csharp/language-reference/compiler-options/doc-compiler-option.md)|Specifica un file XML in cui vengono scritti i commenti sulla documentazione elaborati.|  
|[\/out](../../../csharp/language-reference/compiler-options/out-compiler-option.md)|Specifica il file di output.|  
|[\/pdb](../../../csharp/language-reference/compiler-options/pdb-compiler-option.md)|Specifica il nome file e il percorso del file pdb.|  
|[\/platform](../../../csharp/language-reference/compiler-options/platform-compiler-option.md)|Specificare la piattaforma di output.|  
|[\/preferreduilang](../../../csharp/language-reference/compiler-options/preferreduilang-compiler-option.md)|Specificare una lingua per l'output del compilatore.|  
|[\/target](../../../csharp/language-reference/compiler-options/target-compiler-option.md)|Specifica il formato del file di output mediante una delle cinque opzioni: [\/target:appcontainerexe](../../../csharp/language-reference/compiler-options/target-appcontainerexe-compiler-option.md), [\/target:exe](../../../csharp/language-reference/compiler-options/target-exe-compiler-option.md), [\/target:library](../../../csharp/language-reference/compiler-options/target-library-compiler-option.md), [\/target:module](../../../csharp/language-reference/compiler-options/target-module-compiler-option.md), [\/target:winexe](../../../csharp/language-reference/compiler-options/target-winexe-compiler-option.md) o [\/target:winmdobj](../../../csharp/language-reference/compiler-options/target-winmdobj-compiler-option.md).|  
|`/modulename:<string>`|Specificare il nome del modulo di origine|  
  
### Assembly .NET Framework  
  
|Opzione|Scopo|  
|-------------|-----------|  
|[\/addmodule](../../../csharp/language-reference/compiler-options/addmodule-compiler-option.md)|Specifica uno o più moduli che devono fare parte di questo assembly.|  
|[\/delaysign](../../../csharp/language-reference/compiler-options/delaysign-compiler-option.md)|Indica al compilatore di aggiungere la chiave pubblica e di lasciare l'assembly non firmato.|  
|[\/keycontainer](../../../csharp/language-reference/compiler-options/keycontainer-compiler-option.md)|Specifica il nome del contenitore di chiavi crittografiche.|  
|[\/keyfile](../../../csharp/language-reference/compiler-options/keyfile-compiler-option.md)|Specifica il nome file contenente la chiave crittografica.|  
|[\/lib](../../../csharp/language-reference/compiler-options/lib-compiler-option.md)|Specifica la posizione degli assembly a cui si fa riferimento tramite [\/reference](../../../csharp/language-reference/compiler-options/reference-compiler-option.md).|  
|[\/nostdlib](../../../csharp/language-reference/compiler-options/nostdlib-compiler-option.md)|Indica al compilatore non di non fare importare la libreria standard \(mscorlib.dll\).|  
|[\/reference](../../../csharp/language-reference/compiler-options/reference-compiler-option.md)|Importa i metadati da un file contenente un assembly.|  
|`/analyzer`|Esegue gli analizzatori da questo assembly \(forma breve: \/a\)|  
|`/additionalfile`|Assegna un nome ad altri file che non influiscono direttamente sulla generazione del codice, ma possono essere usati dagli analizzatori per produrre errori o avvisi.|  
  
### Debug\/Controllo errori  
  
|Opzione|Scopo|  
|-------------|-----------|  
|[\/bugreport](../../../csharp/language-reference/compiler-options/bugreport-compiler-option.md)|Crea un file contenente informazioni che rendono più semplice segnalare un bug.|  
|[\/checked](../../../csharp/language-reference/compiler-options/checked-compiler-option.md)|Specifica se il calcolo di interi che supera i limiti del tipo di dati genererà un'eccezione in fase di esecuzione.|  
|[\/debug](../../../csharp/language-reference/compiler-options/debug-compiler-option.md)|Indica al compilatore di generare informazioni di debug.|  
|[\/errorreport](../../../csharp/language-reference/compiler-options/errorreport-compiler-option.md)|Imposta il comportamento relativo alla segnalazione degli errori.|  
|[\/fullpaths](../../../csharp/language-reference/compiler-options/fullpaths-compiler-option.md)|Specifica il percorso assoluto del file nell'output del compilatore.|  
|[\/nowarn](../../../csharp/language-reference/compiler-options/nowarn-compiler-option.md)|Elimina la generazione degli avvisi specificati da parte del compilatore.|  
|[\/warn](../../../csharp/language-reference/compiler-options/warn-compiler-option.md)|Imposta il livello degli avvisi.|  
|[\/warnaserror](../../../csharp/language-reference/compiler-options/warnaserror-compiler-option.md)|Alza il livello degli avvisi a errori.|  
|`/ruleset:<file>`|Specificare un file di set di regole che disabilita la diagnostica specifica.|  
  
### Preprocessore  
  
|Opzione|Scopo|  
|-------------|-----------|  
|[\/define](../../../csharp/language-reference/compiler-options/define-compiler-option.md)|Definisce i simboli del preprocessore.|  
  
### Risorse  
  
|Opzione|Scopo|  
|-------------|-----------|  
|[\/link](../../../csharp/language-reference/compiler-options/link-compiler-option.md)|Rende disponibili per il progetto le informazioni sui tipi COM negli assembly specificati.|  
|[\/linkresource](../../../csharp/language-reference/compiler-options/linkresource-compiler-option.md)|Crea un collegamento a una risorsa gestita.|  
|[\/resource](../../../csharp/language-reference/compiler-options/resource-compiler-option.md)|Incorpora una risorsa di .NET Framework nel file di output.|  
|[\/win32icon](../../../csharp/language-reference/compiler-options/win32icon-compiler-option.md)|Specifica un file ico da inserire nel file di output.|  
|[\/win32res](../../../csharp/language-reference/compiler-options/win32res-compiler-option.md)|Specifica una risorsa Win32 da inserire nel file di output.|  
  
### Varie  
  
|Opzione|Scopo|  
|-------------|-----------|  
|[@](../../../csharp/language-reference/compiler-options/response-file-compiler-option.md)|Specifica un file di risposta.|  
|[\/?](../../../csharp/language-reference/compiler-options/help-compiler-option.md)|Elenca le opzioni del compilatore in stdout.|  
|[\/baseaddress](../../../csharp/language-reference/compiler-options/baseaddress-compiler-option.md)|Specifica l'indirizzo di base preferenziale in cui caricare una DLL.|  
|[\/codepage](../../../csharp/language-reference/compiler-options/codepage-compiler-option.md)|Specifica la tabella codici da usare per tutti i file del codice sorgente nella compilazione.|  
|[\/help](../../../csharp/language-reference/compiler-options/help-compiler-option.md)|Elenca le opzioni del compilatore in stdout.|  
|[\/highentropyva](../../../csharp/language-reference/compiler-options/highentropyva-compiler-option.md)|Specifica che il file eseguibile supporta ASLR \(Address Space Layout Randomization\).|  
|[\/langversion](../../../csharp/language-reference/compiler-options/langversion-compiler-option.md)|Specifica la modalità della versione del linguaggio: ISO\-1, ISO\-2, 3, 4, 5, 6 o Default|  
|[\/main](../../../csharp/language-reference/compiler-options/main-compiler-option.md)|Specifica il percorso del metodo **Main**.|  
|[\/noconfig](../../../csharp/language-reference/compiler-options/noconfig-compiler-option.md)|Indica al compilatore di non eseguire la compilazione con csc.rsp.|  
|[\/nologo](../../../csharp/language-reference/compiler-options/nologo-compiler-option.md)|Elimina i messaggi informativi del compilatore.|  
|[\/recurse](../../../csharp/language-reference/compiler-options/recurse-compiler-option.md)|Cerca nelle sottodirectory i file di origine da compilare.|  
|[\/subsystemversion](../../../csharp/language-reference/compiler-options/subsystemversion-compiler-option.md)|Specifica la versione minima del sottosistema che può essere utilizzata dal file eseguibile.|  
|[\/unsafe](../../../csharp/language-reference/compiler-options/unsafe-compiler-option.md)|Abilita la compilazione del codice che usa la parola chiave [unsafe](../../../csharp/language-reference/keywords/unsafe.md).|  
|[\/utf8output](../../../csharp/language-reference/compiler-options/utf8output-compiler-option.md)|Visualizza l'output del compilatore usando la codifica UTF\-8.|  
|`/parallel[+&#124;-]`|Specifica se usare la compilazione simultanea \(\+\).|  
|`/checksumalgorithm:<alg>`|Specificare l'algoritmo per il calcolo del checksum del file di origine archiviato nel file PDB.  I valori supportati sono: SHA1 \(predefinito\) o SHA256.|  
  
## Opzioni obsolete  
  
|||  
|-|-|  
|**\/incremental**|Abilita la compilazione incrementale.|  
  
## Vedere anche  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [C\# Compiler Options Listed Alphabetically](../../../csharp/language-reference/compiler-options/listed-alphabetically.md)   
 [How to: Set Environment Variables for the Visual Studio Command Line](../../../csharp/language-reference/compiler-options/how-to-set-environment-variables-for-the-visual-studio-command-line.md)