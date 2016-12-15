---
title: "Visual Basic Compiler Options Listed by Category | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
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
  - "Visual Basic compiler, options"
ms.assetid: fbe36f7a-7cfa-4f77-a8d4-2be5958568e3
caps.latest.revision: 24
caps.handback.revision: 24
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Visual Basic Compiler Options Listed by Category
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Il compilatore da riga di comando [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] fornisce un'alternativa alla compilazione dei programmi dall'interno dell'ambiente di sviluppo integrato \(IDE\) di [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)].  Di seguito è riportato un elenco delle opzioni del compilatore da riga di comando [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] ordinate in base alla categoria funzionale.  
  
## Output del compilatore  
  
|||  
|-|-|  
|Opzione|Scopo|  
|[\/nologo](../../../visual-basic/reference/command-line-compiler/nologo.md)|Elimina i messaggi informativi del compilatore.|  
|[\/utf8output](../../../visual-basic/reference/command-line-compiler/utf8output.md)|Visualizza l'output del compilatore usando la codifica UTF\-8.|  
|[\/verbose](../../../visual-basic/reference/command-line-compiler/verbose.md)|Restituisce informazioni supplementari durante la compilazione.|  
|`/modulename:<string>`|Specificare il nome del modulo di origine|  
|[\/preferreduilang](../../../csharp/language-reference/compiler-options/preferreduilang-compiler-option.md)|Specificare una lingua per l'output del compilatore.|  
  
## Ottimizzazione  
  
|||  
|-|-|  
|Opzione|Scopo|  
|[\/filealign](../../../visual-basic/reference/command-line-compiler/filealign.md)|Specifica la posizione di allineamento per le sezioni del file di output.|  
|[\/optimize](../../../visual-basic/reference/command-line-compiler/optimize.md)|Abilita\/disabilita le ottimizzazioni.|  
  
## File di output  
  
|||  
|-|-|  
|Opzione|Scopo|  
|[\/doc](../../../visual-basic/reference/command-line-compiler/doc.md)|Elabora commenti per la documentazione in un file XML.|  
|[\/netcf](../../../visual-basic/reference/command-line-compiler/netcf.md)|Imposta il compilatore in modo che punti a [!INCLUDE[Compact](../../../visual-basic/reference/command-line-compiler/includes/compact_md.md)].|  
|[\/out](../../../visual-basic/reference/command-line-compiler/out.md)|Specifica un file di output.|  
|[\/target](../../../visual-basic/reference/command-line-compiler/target.md)|Specifica il formato dell'output.|  
  
## Assembly .NET  
  
|||  
|-|-|  
|Opzione|Scopo|  
|[\/addmodule](../../../visual-basic/reference/command-line-compiler/addmodule.md)|Fa sì che il compilatore renda disponibili per il progetto in compilazione tutte le informazioni sui tipi presenti nei file specificati.|  
|[\/delaysign](../../../visual-basic/reference/command-line-compiler/delaysign.md)|Specifica se l'assembly avrà firma completa o parziale.|  
|[\/imports](../../../visual-basic/reference/command-line-compiler/imports.md)|Importa uno spazio dei nomi dall'assembly specificato.|  
|[\/keycontainer](../../../visual-basic/reference/command-line-compiler/keycontainer.md)|Specifica il nome di un contenitore di chiavi per una coppia di chiavi allo scopo di assegnare a un assembly un nome sicuro.|  
|[\/keyfile](../../../visual-basic/reference/command-line-compiler/keyfile.md)|Specifica un file contenente una chiave o una coppia di chiavi allo scopo di assegnare a un assembly un nome sicuro.|  
|[\/libpath](../../../visual-basic/reference/command-line-compiler/libpath.md)|Specifica la posizione degli assembly a cui fa riferimento l'opzione [\/reference](../../../visual-basic/reference/command-line-compiler/reference.md).|  
|[\/reference](../../../visual-basic/reference/command-line-compiler/reference.md)|Importa metadati da un assembly.|  
|[\/moduleassemblyname](../../../visual-basic/reference/command-line-compiler/moduleassemblyname.md)|Specifica il nome dell'assembly che conterrà un modulo.|  
|`/analyzer`|Esegue gli analizzatori da questo assembly \(forma breve: \/a\)|  
|`/additionalfile`|Assegna un nome ad altri file che non influiscono direttamente sulla generazione del codice, ma possono essere usati dagli analizzatori per produrre errori o avvisi.|  
  
## Debug\/Controllo errori  
  
|||  
|-|-|  
|Opzione|Scopo|  
|[\/bugreport](../../../visual-basic/reference/command-line-compiler/bugreport.md)|Crea un file contenente informazioni che rendono più semplice segnalare un bug.|  
|[\/debug](../../../visual-basic/reference/command-line-compiler/debug.md)|Crea informazioni di debug.|  
|[\/nowarn](../../../visual-basic/reference/command-line-compiler/nowarn.md)|Inibisce la capacità del compilatore di generare avvisi.|  
|[\/quiet](../../../visual-basic/reference/command-line-compiler/quiet.md)|Impedisce al compilatore di visualizzare codice per avvisi ed errori relativi alla sintassi.|  
|[\/removeintchecks](../../../visual-basic/reference/command-line-compiler/removeintchecks.md)|Disabilita il controllo dell'overflow di Integer.|  
|[\/warnaserror](../../../visual-basic/reference/command-line-compiler/warnaserror.md)|Alza il livello degli avvisi a errori.|  
|`/ruleset:<file>`|Specificare un file di set di regole che disabilita la diagnostica specifica.|  
  
## ?  
  
|||  
|-|-|  
|Opzione|Scopo|  
|[\/?](../../../visual-basic/reference/command-line-compiler/help.md)|Visualizza le opzioni del compilatore.  Questo comando ha la stessa funzione dell'opzione `/help`.  Non viene effettuata alcuna compilazione.|  
|[\/help](../../../visual-basic/reference/command-line-compiler/help.md)|Visualizza le opzioni del compilatore.  Questo comando ha la stessa funzione dell'opzione `/?`.  Non viene effettuata alcuna compilazione.|  
  
## Linguaggio  
  
|||  
|-|-|  
|Opzione|Scopo|  
|[\/langversion](../../../visual-basic/reference/command-line-compiler/langversion.md)|Specificare la versione del linguaggio: 9&#124;9.0&#124;10&#124;10.0&#124;11&#124;11.0.|  
|[\/optionexplicit](../../../visual-basic/reference/command-line-compiler/optionexplicit.md)|Richiede la dichiarazione esplicita delle variabili.|  
|[\/optionstrict](../../../visual-basic/reference/command-line-compiler/optionstrict.md)|Attiva la semantica dei tipi rigorosa.|  
|[\/optioncompare](../../../visual-basic/reference/command-line-compiler/optioncompare.md)|Specifica se il confronto si verifica tra stringhe di tipo binario oppure se usare una semantica basata sul testo specifica delle impostazioni locali definite.|  
|[\/optioninfer](../../../visual-basic/reference/command-line-compiler/optioninfer.md)|Consente di usare l'inferenza del tipo di variabile locale nelle dichiarazioni di variabile.|  
  
## Preprocessore  
  
|||  
|-|-|  
|Opzione|Scopo|  
|[\/define](../../../visual-basic/reference/command-line-compiler/define.md)|Definisce simboli per la compilazione condizionale.|  
  
## Risorse  
  
|||  
|-|-|  
|Opzione|Scopo|  
|[\/linkresource](../../../visual-basic/reference/command-line-compiler/linkresource.md)|Crea un collegamento a una risorsa gestita.|  
|[\/resource](../../../visual-basic/reference/command-line-compiler/resource.md)|Incorpora una risorsa gestita in un assembly.|  
|[\/win32icon](../../../visual-basic/reference/command-line-compiler/win32icon.md)|Inserisce un file ico nel file di output.|  
|[\/win32resource](../../../visual-basic/reference/command-line-compiler/win32resource.md)|Inserisce una risorsa Win32 nel file di output.|  
  
## Varie  
  
|||  
|-|-|  
|Opzione|Scopo|  
|[@ \(specifica di un file di risposta\)](../../../visual-basic/reference/command-line-compiler/specify-response-file.md)|Specifica un file di risposta.|  
|[\/baseaddress](../../../visual-basic/reference/command-line-compiler/baseaddress.md)|Specifica l'indirizzo di base di una DLL.|  
|[\/codepage](../../../visual-basic/reference/command-line-compiler/codepage.md)|Specifica la tabella codici da usare per tutti i file del codice sorgente nella compilazione.|  
|[\/errorreport](../../../visual-basic/reference/command-line-compiler/errorreport.md)|Specifica la modalità di segnalazione degli errori interni del compilatore [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].|  
|[\/highentropyva](../../../visual-basic/reference/command-line-compiler/highentropyva.md)|Indica al kernel di Windows se un particolare eseguibile supporta ASLR \(Address Space Layout Randomization\) a entropia elevata.|  
|[\/main](../../../visual-basic/reference/command-line-compiler/main.md)|Specifica la classe che contiene la routine `Sub``Main` da usare all'avvio.|  
|[\/noconfig](../../../visual-basic/reference/command-line-compiler/noconfig.md)|La compilazione non viene eseguita con Vbc.rsp|  
|[\/nostdlib](../../../visual-basic/reference/command-line-compiler/nostdlib.md)|Indica al compilatore di non fare riferimento alle librerie standard.|  
|[\/nowin32manifest](../../../visual-basic/reference/command-line-compiler/nowin32manifest.md)|Indica al compilatore di non incorporare un manifesto dell'applicazione nel file eseguibile.|  
|[\/platform](../../../visual-basic/reference/command-line-compiler/platform.md)|Specifica la piattaforma del processore da impostare come destinazione del file di output.|  
|[\/recurse](../../../visual-basic/reference/command-line-compiler/recurse.md)|Cerca nelle sottodirectory i file di origine da compilare.|  
|[\/rootnamespace](../../../visual-basic/reference/command-line-compiler/rootnamespace.md)|Specifica uno spazio dei nomi per tutte le dichiarazioni di tipo.|  
|[\/sdkpath](../../../visual-basic/reference/command-line-compiler/sdkpath.md)|Specifica il percorso dei file Mscorlib.dll e Microsoft.VisualBasic.dll.|  
|[\/vbruntime](../../../visual-basic/reference/command-line-compiler/vbruntime.md)|Indica che il compilatore deve compilare senza un riferimento alla libreria di runtime di Visual Basic oppure con un riferimento a una libreria di runtime specifica.|  
|[\/win32manifest](../../../visual-basic/reference/command-line-compiler/win32manifest.md)|Identifica un file manifesto dell'applicazione Win32 definito dall'utente da incorporare nel file eseguibile di tipo PE di un progetto.|  
|`/parallel[+&#124;-]`|Specifica se usare la compilazione simultanea \(\+\).|  
|`/checksumalgorithm:<alg>`|Specificare l'algoritmo per il calcolo del checksum del file di origine archiviato nel file PDB.  I valori supportati sono: SHA1 \(predefinito\) o SHA256.|  
  
## Vedere anche  
 [Visual Basic Compiler Options Listed Alphabetically](../../../visual-basic/reference/command-line-compiler/compiler-options-listed-alphabetically.md)   
 [Introduction to the Project Designer](http://msdn.microsoft.com/it-it/898dd854-c98d-430c-ba1b-a913ce3c73d7)   
 [C\# Compiler Options Listed Alphabetically](../../../csharp/language-reference/compiler-options/listed-alphabetically.md)   
 [C\# Compiler Options Listed by Category](../../../csharp/language-reference/compiler-options/listed-by-category.md)