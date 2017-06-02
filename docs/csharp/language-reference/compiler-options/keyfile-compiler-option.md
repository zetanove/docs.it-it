---
title: -keyfile (opzioni del compilatore C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- /keyfile
dev_langs:
- CSharp
helpviewer_keywords:
- /keyfile compiler option [C#]
- -keyfile compiler option [C#]
- keyfile compiler option [C#]
ms.assetid: 0815f9de-ace4-4e98-b4c6-13c55dea40c2
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
ms.sourcegitcommit: fe32676f0e39ed109a68f39584cf41aec5f5ce90
ms.openlocfilehash: 4f9ccbfe7126aac3214ccf08015353eec0490cd4
ms.contentlocale: it-it
ms.lasthandoff: 05/10/2017

---
# <a name="keyfile-c-compiler-options"></a>/keyfile (opzioni del compilatore C#)
Specifica il nome file contenente la chiave crittografica.  
  
## <a name="syntax"></a>Sintassi  
  
```console  
/keyfile:file  
```  
  
## <a name="arguments"></a>Argomenti  
  
|Termine|Definizione|  
|----------|----------------|  
|`file`|Nome del file che contiene la chiave con nome sicuro.|  
  
## <a name="remarks"></a>Note  
 Se si usa questa opzione, il compilatore inserisce la chiave pubblica dal file specificato nel manifesto dell'assembly e quindi firma l'assembly finale con la chiave privata. Per generare un file di chiave, digitare sn -k `file` nella riga di comando.  
  
 Se si esegue la compilazione con **/target: module**, il nome del file di chiave verrà mantenuto nel modulo e incorporato nell'assembly creato quando si compila un assembly con [/addmodule](../../../csharp/language-reference/compiler-options/addmodule-compiler-option.md).  
  
 È possibile passare al compilatore le informazioni di crittografia anche tramite [/keycontainer](../../../csharp/language-reference/compiler-options/keycontainer-compiler-option.md). Usare [/delaysign](../../../csharp/language-reference/compiler-options/delaysign-compiler-option.md) se si vuole che l'assembly abbia una firma parziale.  
  
 Se nella stessa compilazione vengono specificate sia /keyfile che /keycontainer (tramite opzione della riga di comando o attributo personalizzato), verrà tentato prima il contenitore di chiavi. Se l'operazione riesce, l'assembly viene firmato con le informazioni incluse nel contenitore di chiavi. Se invece il compilatore non trova il contenitore di chiavi, effettua un tentativo con il file specificato in /keyfile. Se l'operazione riesce, l'assembly verrà firmato con le informazioni contenute nel file di chiave e le informazioni sulla chiave verranno installate nel contenitore di chiavi (in modo analogo a sn -i) in modo che nella compilazione successiva il contenitore di chiavi sia valido.  
  
 Si noti che un file di chiave può contenere solo la chiave pubblica.  
  
 Per altre informazioni, vedere [Creazione e uso degli assembly con nome sicuro](https://msdn.microsoft.com/library/xwb8f617) e [Ritardo della firma di un assembly](../../../framework/app-domains/delay-sign-assembly.md).  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Per impostare l'opzione del compilatore nell'ambiente di sviluppo di Visual Studio  
  
1.  Aprire la pagina **Proprietà** del progetto.  
  
2.  Fare clic sulla pagina della proprietà **Firma**.  
  
3.  Modificare la proprietà **Scegli un file chiave con nome sicuro**.  
  
 È possibile accedere a questa opzione del compilatore a livello di codice con <xref:VSLangProj.ProjectProperties.AssemblyOriginatorKeyFile%2A>.  
  
## <a name="see-also"></a>Vedere anche  
 [C# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)  (Opzioni del compilatore C#)  
 [NIB Procedura: Modificare le proprietà e le impostazioni di configurazione dei progetti](http://msdn.microsoft.com/en-us/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)
