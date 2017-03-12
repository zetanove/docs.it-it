---
title: "/baseaddress (C# Compiler Options) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "/dllbase"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "baseaddress compiler option [C#]"
  - "/baseaddress compiler option [C#]"
  - "-baseaddress compiler option [C#]"
ms.assetid: ce13c965-dfe4-4433-94f5-63b476e3a608
caps.latest.revision: 18
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 18
---
# /baseaddress (C# Compiler Options)
L'opzione **\/baseaddress** consente di specificare l'indirizzo di base preferenziale per il caricamento di una DLL.  Per ulteriori informazioni su quando e perché utilizzare questa opzione, vedere [Miglioramento del tempo di avvio dell'applicazione](http://go.microsoft.com/fwlink/?LinkId=107043) ed [WebLog di Larry Osterman](http://go.microsoft.com/fwlink/?LinkId=107044).  
  
## Sintassi  
  
```  
/baseaddress:address  
```  
  
## Argomenti  
 `address`  
 Indirizzo di base della DLL.  È possibile specificare questo indirizzo sotto forma di numero decimale, esadecimale o ottale.  
  
## Note  
 L'indirizzo di base predefinito di una DLL viene impostato automaticamente nel Common Language Runtime di .NET Framework.  
  
 Tenere presente che, in questo indirizzo, l'elemento meno significativo verrà arrotondato.  Se ad esempio si specifica 0x11110001, verrà automaticamente effettuato l'arrotondamento a 0x11110000.  
  
 Per completare il processo di firma di una DLL, utilizzare SN.EXE con l'opzione \-R.  
  
### Per impostare l'opzione del compilatore nell'ambiente di sviluppo di Visual Studio  
  
1.  Aprire la pagina **Proprietà** del progetto.  
  
2.  Fare clic sulla pagina delle proprietà **Compila**.  
  
3.  Fare clic sul pulsante **Avanzate**.  
  
4.  Modificare la proprietà **Indirizzo di base DLL**.  
  
     Per impostare l'opzione del compilatore a livello di codice, vedere <xref:VSLangProj80.CSharpProjectConfigurationProperties3.BaseAddress%2A>.  
  
## Vedere anche  
 <xref:System.Diagnostics.ProcessModule.BaseAddress%2A?displayProperty=fullName>   
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [Procedura: modificare le proprietà e le impostazioni di configurazione dei progetti](http://msdn.microsoft.com/it-it/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)