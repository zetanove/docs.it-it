---
title: -linkresource (opzioni del compilatore C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- /linkresource
dev_langs:
- CSharp
helpviewer_keywords:
- /linkresource compiler option [C#]
- linkres compiler option [C#]
- /linkres compiler option [C#]
- -linkres compiler option [C#]
- -linkresource compiler option [C#]
- linkresource compiler option [C#]
ms.assetid: 440c26c2-77c1-4811-a0a3-57cce3f5fc96
caps.latest.revision: 17
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
ms.openlocfilehash: d9a3bc4dc4b51d6170c67f9d2f95b6805497b31c
ms.contentlocale: it-it
ms.lasthandoff: 05/10/2017

---
# <a name="linkresource-c-compiler-options"></a>/linkresource (opzioni del compilatore C#)
Crea un collegamento a una risorsa di .NET Framework nel file di output. Il file di risorse non viene aggiunto al file di output. Questa opzione è diversa dall'opzione [/resource](../../../csharp/language-reference/compiler-options/resource-compiler-option.md), che invece incorpora un file di risorse nel file di output.  
  
## <a name="syntax"></a>Sintassi  
  
```console  
/linkresource:filename[,identifier[,accessibility-modifier]]  
```  
  
## <a name="arguments"></a>Argomenti  
 `filename`  
 File di risorse .NET Framework a cui si vuole stabilire un collegamento dall'assembly.  
  
 `identifier` (facoltativo)  
 Nome logico della risorsa, usato per caricare la risorsa stessa. L'impostazione predefinita corrisponde al nome del file.  
  
 `accessibility-modifier` (facoltativo)  
 Accessibilità della risorsa: public o private. L'impostazione predefinita è public.  
  
## <a name="remarks"></a>Note  
 Per impostazione predefinita, le risorse collegate sono pubbliche nell'assembly quando vengono create con il compilatore C#. Per renderle private, specificare `private` come modificatore di accessibilità. Non è consentito alcun modificatore diverso da `public` o `private`.  
  
 Per **/linkresource** è necessaria un'opzione [/target](../../../csharp/language-reference/compiler-options/target-compiler-option.md) diversa da **/target:module**.  
  
 Se `filename` è un file di risorse .NET Framework creato ad esempio da [Resgen.exe](http://msdn.microsoft.com/library/8ef159de-b660-4bec-9213-c3fbc4d1c6f4) oppure nell'ambiente di sviluppo, è possibile accedervi tramite i membri dello spazio dei nomi <xref:System.Resources>. Per altre informazioni, vedere <xref:System.Resources.ResourceManager?displayProperty=fullName>. Per tutte le altre risorse, usare i metodi `GetManifestResource`* della classe <xref:System.Reflection.Assembly> per accedere alla risorsa in fase di runtime.  
  
 Il file specificato in `filename` può avere qualsiasi formato. Può ad esempio risultare opportuno rendere una DLL nativa parte dell'assembly in modo che possa essere installata nella Global Assembly Cache e che sia possibile accedervi dal codice gestito nell'assembly. Nel secondo degli esempi seguenti viene illustrato come effettuare questa operazione. È possibile eseguire la stessa operazione in Assembly Linker. Nel terzo degli esempi seguenti viene illustrato come effettuare questa operazione. Per altre informazioni, vedere [Al.exe (Assembly Linker)](https://msdn.microsoft.com/library/c405shex) e [Uso di assembly e della Global Assembly Cache](../../../framework/app-domains/working-with-assemblies-and-the-gac.md).  
  
 **/linkres** rappresenta la versione abbreviata di **/linkresource**.  
  
 Questa opzione del compilatore non è disponibile in Visual Studio e non può essere modificata a livello di codice.  
  
## <a name="example"></a>Esempio  
 Compilare `in.cs` e stabilire il collegamento al file di risorse `rf.resource`:  
  
```console  
csc /linkresource:rf.resource in.cs  
```  
  
## <a name="example"></a>Esempio  
 Compilare `A.cs` in una DLL, creare un collegamento a una DLL N.dll nativa e inserire l'output nella Global Assembly Cache. In questo esempio i file A.dll e N.dll verranno memorizzati entrambi nella Global Assembly Cache.  
  
```console  
csc /linkresource:N.dll /t:library A.cs  
gacutil -i A.dll  
```  
  
## <a name="example"></a>Esempio  
 In questo esempio viene eseguita la stessa operazione descritta in precedenza, ma vengono usate le opzioni di Assembly Linker.  
  
```console  
csc /t:module A.cs  
al /out:A.dll A.netmodule /link:N.dll   
gacutil -i A.dll  
```  
  
## <a name="see-also"></a>Vedere anche  
 [C# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)  (Opzioni del compilatore C#)  
 [Al.exe (Assembly Linker)](https://msdn.microsoft.com/library/c405shex)   
 [Uso di assembly e della Global Assembly Cache](../../../framework/app-domains/working-with-assemblies-and-the-gac.md)   
 [NIB Procedura: Modificare le proprietà e le impostazioni di configurazione dei progetti](http://msdn.microsoft.com/en-us/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)
