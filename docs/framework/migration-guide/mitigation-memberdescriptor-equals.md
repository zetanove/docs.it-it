---
title: 'Mitigazione: MemberDescriptor.Equals | Documenti di Microsoft'
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-bcl
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cf3735f0-0dd4-4bef-b4b0-575264e10f39
caps.latest.revision: 7
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 409f06f4dfbe7be50dd2c487e49d3d4d8a477539
ms.contentlocale: it-it
ms.lasthandoff: 04/18/2017

---
# <a name="mitigation-memberdescriptorequals"></a>Mitigazione: MemberDescriptor.Equals
A partire dalle applicazioni destinate a [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], l'implementazione del metodo <xref:System.ComponentModel.MemberDescriptor.Equals%2A?displayProperty=fullName> è stata modificata. Poiché i metodi `System.ComponentModel.EventDescriptor.Equals` e `System.ComponentModel.PropertyDescriptor.Equals` ereditano l'implementazione della classe base, la modifica interesserà anche questi metodi.  
  
 Nelle applicazioni destinate alle versioni di .NET Framework precedenti alla [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], una parte del test di uguaglianza del metodo <xref:System.ComponentModel.MemberDescriptor.Equals%2A?displayProperty=fullName> confrontava in modo inesatto la proprietà <xref:System.ComponentModel.MemberDescriptor.Category%2A?displayProperty=fullName> di un oggetto con la proprietà <xref:System.ComponentModel.MemberDescriptor.Description%2A?displayProperty=fullName> di un altro. A partire dalle applicazioni destinate a [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], il metodo <xref:System.ComponentModel.MemberDescriptor.Equals%2A?displayProperty=fullName> confronta la proprietà <xref:System.ComponentModel.MemberDescriptor.Description%2A?displayProperty=fullName> dei due oggetti.  
  
## <a name="impact"></a>Impatto  
 Questa modifica implementa correttamente il test di uguaglianza per gli oggetti <xref:System.ComponentModel.MemberDescriptor?displayProperty=fullName> e deve avere un impatto minimo.  
  
## <a name="mitigation"></a>Attenuazione  
 Sono disponibili due soluzioni alternative se le app sono destinate a [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] o a una versione successiva di .NET Framework. La scelta dipenderà dal metodo <xref:System.ComponentModel.MemberDescriptor.Equals%2A?displayProperty=fullName> che talvolta restituisce `false` quando i descrittori di membro sono equivalenti:  
  
-   È possibile rifiutare esplicitamente questa modifica senza modificare il codice sorgente aggiungendo il codice seguente alla sezione [\<runtime>](../../../docs/framework/configure-apps/file-schema/runtime/runtime-element.md) del file app.config:  
  
    ```xml  
    <runtime>  
        <AppContextSwitchOverrides value = "Switch.System.MemberDescriptorEqualsReturnsFalseIfEquivalent=true" />  
     </runtime>  
    ```  
  
-   È possibile modificare il codice sorgente per ripristinare il comportamento precedente confrontando manualmente le proprietà <xref:System.ComponentModel.MemberDescriptor.Category%2A?displayProperty=fullName> e <xref:System.ComponentModel.MemberDescriptor.Description%2A?displayProperty=fullName> dopo aver chiamato il metodo <xref:System.ComponentModel.MemberDescriptor.Equals%2A?displayProperty=fullName>, come nel seguente frammento di codice.  
  
    ```csharp  
    if (memberDescriptor1.Equals(memberDescriptor2) &   
        memberDescriptor1.Description.Equals(memberDescriptor2.Category)) {  
          // Code to execute if true.  
    }  
    else {  
          // Code to execute if false.     
    }  
    ```  
  
    ```  
    If memberDescriptor1.Equals(memberDescriptor2) And   
        memberDescriptor1.Description.Equals(memberDescriptor2.Category)  
          // Code to execute if True.  
    Else  
          // Code to execute if False.     
    End If  
    ```  
  
 Per le applicazioni destinate a [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] e versioni precedenti, è possibile abilitare questa modifica aggiungendo il valore seguente al file app.config:  
  
```xml  
<runtime>  
    <AppContextSwitchOverrides value="Switch.System.MemberDescriptorEqualsReturnsFalseIfEquivalent=true />  
</runtime>  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Modifiche di reindirizzamento](../../../docs/framework/migration-guide/retargeting-changes-in-the-net-framework-4-6-2.md)   
 [Compatibilità delle applicazioni nella versione 4.6.2](../../../docs/framework/migration-guide/application-compatibility-in-the-net-framework-4-6-2.md)

