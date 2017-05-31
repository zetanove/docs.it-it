---
title: Opzioni del compilatore C# in ordine alfabetico (C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- compiler options [C#], listed alpabetically
- C# language, compiler options listed alphabitically
- Visual C# compiler, options listed alphabetically
- Visual C#, compiler options listed alphabetically
ms.assetid: 43535ea0-ca47-4a15-b528-615087a86092
caps.latest.revision: 25
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
ms.sourcegitcommit: fe32676f0e39ed109a68f39584cf41aec5f5ce90
ms.openlocfilehash: 91582d214c2f8a72d383a0ac17e409167fda5065
ms.contentlocale: it-it
ms.lasthandoff: 05/10/2017

---
# <a name="c-compiler-options-listed-alphabetically"></a>Opzioni del compilatore C# in ordine alfabetico
Le seguenti opzioni del compilatore sono ordinate alfabeticamente. Per un elenco organizzato per categorie, vedere [Opzioni del compilatore C# elencate per categoria](../../../csharp/language-reference/compiler-options/listed-by-category.md).  
  
|Opzione|Scopo|  
|------------|-------------|  
|[@](../../../csharp/language-reference/compiler-options/response-file-compiler-option.md)|Legge un file di risposta per altre opzioni|  
|[/?](../../../csharp/language-reference/compiler-options/help-compiler-option.md)|Visualizza un messaggio relativo all'utilizzo in stdout.|  
|`/additionalfile`|Assegna un nome ad altri file che non influiscono direttamente sulla generazione del codice, ma possono essere usati dagli analizzatori per produrre errori o avvisi.|  
|[/addmodule](../../../csharp/language-reference/compiler-options/addmodule-compiler-option.md)|Collega i moduli specificati nell'assembly|  
|`/analyzer`|Esegue gli analizzatori da questo assembly (forma breve: /a)|  
|[/appconfig](../../../csharp/language-reference/compiler-options/appconfig-compiler-option.md)|Specifica il percorso del file app.config in fase di associazione di assembly.|  
|[/baseaddress](../../../csharp/language-reference/compiler-options/baseaddress-compiler-option.md)|Specifica l'indirizzo di base della libreria da compilare.|  
|[/bugreport](../../../csharp/language-reference/compiler-options/bugreport-compiler-option.md)|Crea un file di report sui bug. Questo file verrà inviato con le informazioni sull'arresto anomalo se viene usato con **/errorreport:prompt** o **/errorreport:send**.|  
|[/checked](../../../csharp/language-reference/compiler-options/checked-compiler-option.md)|Fa generare al compilatore i controlli dell'overflow.|  
|`/checksumalgorithm:<alg>`|Specificare l'algoritmo per il calcolo del checksum del file di origine archiviato nel file PDB.  I valori supportati sono: SHA1 (predefinito) o SHA256.|  
|[/codepage](../../../csharp/language-reference/compiler-options/codepage-compiler-option.md)|Specifica la tabella di codici da utilizzare per l'apertura dei file di origine.|  
|[/debug](../../../csharp/language-reference/compiler-options/debug-compiler-option.md)|Crea informazioni di debug.|  
|[/define](../../../csharp/language-reference/compiler-options/define-compiler-option.md)|Definisce i simboli di compilazione condizionale.|  
|[/delaysign](../../../csharp/language-reference/compiler-options/delaysign-compiler-option.md)|Ritarda la firma dell'assembly usando solo la parte pubblica della chiave con nome sicuro.|  
|[/doc](../../../csharp/language-reference/compiler-options/doc-compiler-option.md)|Specifica un file XML della documentazione da generare.|  
|[/errorreport](../../../csharp/language-reference/compiler-options/errorreport-compiler-option.md)|Specifica come gestire gli errori interni del compilatore: prompt, send o none. Il valore predefinito è none.|  
|[/filealign](../../../csharp/language-reference/compiler-options/filealign-compiler-option.md)|Specifica l'allineamento usato per le sezioni del file di output.|  
|[/fullpaths](../../../csharp/language-reference/compiler-options/fullpaths-compiler-option.md)|Fa generare al compilatore percorsi completi.|  
|[/help](../../../csharp/language-reference/compiler-options/help-compiler-option.md)|Visualizza un messaggio relativo all'utilizzo in stdout.|  
|[/highentropyva](../../../csharp/language-reference/compiler-options/highentropyva-compiler-option.md)|Specifica che è supportata la funzionalità ASLR a entropia elevata.|  
|**/incremental**|Abilita la compilazione incrementale [obsoleto]|  
|[/keycontainer](../../../csharp/language-reference/compiler-options/keycontainer-compiler-option.md)|Specifica un contenitore di chiavi con nome sicuro.|  
|[/keyfile](../../../csharp/language-reference/compiler-options/keyfile-compiler-option.md)|Specifica un file di chiave con nome sicuro.|  
|[/langversion:\<string >](../../../csharp/language-reference/compiler-options/langversion-compiler-option.md)|Specifica la modalità della versione del linguaggio: ISO-1, ISO-2, 3, 4, 5, 6 o Default|  
|[/lib](../../../csharp/language-reference/compiler-options/lib-compiler-option.md)|Specifica directory aggiuntive in cui cercare i riferimenti.|  
|[/link](../../../csharp/language-reference/compiler-options/link-compiler-option.md)|Rende disponibili per il progetto le informazioni sui tipi COM negli assembly specificati.|  
|[/linkresource](../../../csharp/language-reference/compiler-options/linkresource-compiler-option.md)|Collega la risorsa specificata all'assembly.|  
|[/main](../../../csharp/language-reference/compiler-options/main-compiler-option.md)|Specifica il tipo che contiene il punto di ingresso, ignorando tutti gli altri punti di ingresso possibili.|  
|[/moduleassemblyname](../../../csharp/language-reference/compiler-options/moduleassemblyname-compiler-option.md)|Specifica l'assembly i cui tipi non pubblici sono accessibili da un file con estensione NETMODULE.|  
|`/modulename:<string>`|Specificare il nome del modulo di origine|  
|[/noconfig](../../../csharp/language-reference/compiler-options/noconfig-compiler-option.md)|Indica al compilatore di non includere automaticamente il file CSC.RSP.|  
|[/nologo](../../../csharp/language-reference/compiler-options/nologo-compiler-option.md)|Impedisce la visualizzazione del messaggio di copyright del compilatore.|  
|[/nostdlib](../../../csharp/language-reference/compiler-options/nostdlib-compiler-option.md)|Indica al compilatore non di non fare riferimento alla libreria standard (mscorlib.dll).|  
|[/nowarn](../../../csharp/language-reference/compiler-options/nowarn-compiler-option.md)|Disabilita messaggi di avviso specifici|  
|[/nowin32manifest](../../../csharp/language-reference/compiler-options/nowin32manifest-compiler-option.md)|Indica il compilatore di non incorporare un manifesto dell'applicazione nel file eseguibile.|  
|[/optimize](../../../csharp/language-reference/compiler-options/optimize-compiler-option.md)|Abilita/disabilita le ottimizzazioni.|  
|[/out](../../../csharp/language-reference/compiler-options/out-compiler-option.md)|Specifica il nome del file di output (impostazione predefinita: nome base del file con la classe principale o il primo file).|  
|`/parallel[+&#124;-]`|Specifica se usare la compilazione simultanea (+).|  
|[/pdb](../../../csharp/language-reference/compiler-options/pdb-compiler-option.md)|Specifica il nome file e il percorso del file pdb.|  
|[/platform](../../../csharp/language-reference/compiler-options/platform-compiler-option.md)|Limita le piattaforme in cui è possibile eseguire il codice: x86, Itanium, x64, anycpu o anycpu32bitpreferred. Il valore predefinito è anycpu.|  
|[/preferreduilang](../../../csharp/language-reference/compiler-options/preferreduilang-compiler-option.md)|Specifica la lingua da utilizzare per l'output del compilatore.|  
|[/recurse](../../../csharp/language-reference/compiler-options/recurse-compiler-option.md)|Include tutti i file presenti nella directory corrente e nelle relative sottodirectory in base alle specifiche dei caratteri jolly.|  
|[/reference](../../../csharp/language-reference/compiler-options/reference-compiler-option.md)|Fa riferimento ai metadati dei file di assembly specificati.|  
|[/resource](../../../csharp/language-reference/compiler-options/resource-compiler-option.md)|Incorpora la risorsa specificata.|  
|`/ruleset:<file>`|Specificare un file di set di regole che disabilita la diagnostica specifica.|  
|[/subsystemversion](../../../csharp/language-reference/compiler-options/subsystemversion-compiler-option.md)|Specifica la versione minima del sottosistema che può essere utilizzata dal file eseguibile.|  
|[/target](../../../csharp/language-reference/compiler-options/target-compiler-option.md)|Specifica il formato del file di output tramite una delle opzioni seguenti:[/target:appcontainerexe](../../../csharp/language-reference/compiler-options/target-appcontainerexe-compiler-option.md), [/target:exe](../../../csharp/language-reference/compiler-options/target-exe-compiler-option.md), [/target:library](../../../csharp/language-reference/compiler-options/target-library-compiler-option.md), [/target:module](../../../csharp/language-reference/compiler-options/target-module-compiler-option.md), [/target:winexe](../../../csharp/language-reference/compiler-options/target-winexe-compiler-option.md), [/target:winmdobj](../../../csharp/language-reference/compiler-options/target-winmdobj-compiler-option.md).|  
|[/unsafe](../../../csharp/language-reference/compiler-options/unsafe-compiler-option.md)|Consente codice [unsafe](../../../csharp/language-reference/keywords/unsafe.md).|  
|[/utf8output](../../../csharp/language-reference/compiler-options/utf8output-compiler-option.md)|Restituisce i messaggi del compilatore usando la codifica UTF-8.|  
|[/warn](../../../csharp/language-reference/compiler-options/warn-compiler-option.md)|Imposta il livello degli avvisi (0-4).|  
|[/warnaserror](../../../csharp/language-reference/compiler-options/warnaserror-compiler-option.md)|Segnala determinati avvisi come errori.|  
|[/win32icon](../../../csharp/language-reference/compiler-options/win32icon-compiler-option.md)|Usa questa icona per l'output.|  
|[/win32manifest](../../../csharp/language-reference/compiler-options/win32manifest-compiler-option.md)|Specifica un file manifesto win32 personalizzato.|  
|[/win32res](../../../csharp/language-reference/compiler-options/win32res-compiler-option.md)|Specifica il file di risorse win32 (res).|  
  
## <a name="see-also"></a>Vedere anche  
 [C# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)  (Opzioni del compilatore C#)  
 [Opzioni del compilatore C# elencate per categoria](../../../csharp/language-reference/compiler-options/listed-by-category.md)   
 [Procedura: Impostare le variabili di ambiente per la riga di comando di Visual Studio](../../../csharp/language-reference/compiler-options/how-to-set-environment-variables-for-the-visual-studio-command-line.md)   
 [\<compiler> Element](../../../framework/configure-apps/file-schema/compiler/compiler-element.md) (Elemento <compiler>)
