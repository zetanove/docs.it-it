---
title: "/keyfile (C# Compiler Options) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "/keyfile"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "/keyfile compiler option [C#]"
  - "-keyfile compiler option [C#]"
  - "keyfile compiler option [C#]"
ms.assetid: 0815f9de-ace4-4e98-b4c6-13c55dea40c2
caps.latest.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 15
---
# /keyfile (C# Compiler Options)
Specifica il nome del file che contiene la chiave di crittografia.  
  
## Sintassi  
  
```  
/keyfile:file  
```  
  
## Argomenti  
  
|Termine|Definizione|  
|-------------|-----------------|  
|`file`|Nome del file che contiene la chiave con nome sicuro.|  
  
## Note  
 Quando viene utilizzata questa opzione, il compilatore inserisce la chiave pubblica dal file specificato nel manifesto dell'assembly, quindi firma l'assembly finale con la chiave privata.  Per generare un file di chiave, immettere sn \-k `file` sulla riga di comando.  
  
 Se si esegue la compilazione con l'opzione **\/target:module**, il nome del file di chiave verrà conservato nel modulo e incorporato nell'assembly che viene creato quando si compila un assembly con l'opzione [\/addmodule](../../../csharp/language-reference/compiler-options/addmodule-compiler-option.md).  
  
 È possibile passare al compilatore le informazioni di crittografia anche mediante [\/keycontainer](../../../csharp/language-reference/compiler-options/keycontainer-compiler-option.md).  Utilizzare [\/delaysign](../../../csharp/language-reference/compiler-options/delaysign-compiler-option.md) per ottenere un assembly parzialmente firmato.  
  
 Qualora nella stessa compilazione vengano specificate sia \/keyfile che \/keycontainer \(tramite opzione della riga di comando o attributo personalizzato\), verrà tentato prima il contenitore di chiavi.  Se questa operazione viene eseguita correttamente, l'assembly viene firmato con le informazioni incluse nel contenitore di chiavi.  Se il compilatore non trova il contenitore di chiavi, verrà effettuato un tentativo con il file specificato con l'opzione \/keyfile.  In caso di esito positivo, l'assembly viene firmato con le informazioni presenti nel file di chiave e le informazioni sulla chiave verranno installate nel contenitore di chiavi, analogamente a sn \-i, in modo che alla successiva compilazione il contenitore di chiavi sarà valido.  
  
 Si noti che un file di chiave può contenere solo la chiave pubblica.  
  
 Per ulteriori informazioni, vedere [Creazione e utilizzo degli assembly con nome sicuro](../Topic/Creating%20and%20Using%20Strong-Named%20Assemblies.md) e [Ritardo della firma di un assembly](../Topic/Delay%20Signing%20an%20Assembly.md).  
  
### Per impostare l'opzione del compilatore nell'ambiente di sviluppo di Visual Studio  
  
1.  Aprire la pagina **Proprietà** del progetto.  
  
2.  Fare clic sulla pagina delle proprietà **Firma**.  
  
3.  Modificare la proprietà **Scegli un file chiave con nome sicuro**.  
  
 È possibile accedere a questa opzione del compilatore a livello di codice con <xref:VSLangProj.ProjectProperties.AssemblyOriginatorKeyFile%2A>.  
  
## Vedere anche  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [Procedura: modificare le proprietà e le impostazioni di configurazione dei progetti](http://msdn.microsoft.com/it-it/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)