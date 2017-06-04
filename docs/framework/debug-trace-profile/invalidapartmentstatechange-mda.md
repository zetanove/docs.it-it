---
title: "invalidApartmentStateChange MDA | Microsoft Docs"
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
  - "MDAs (managed debugging assistants), invalid apartment state"
  - "managed debugging assistants (MDAs), invalid apartment state"
  - "InvalidApartmentStateChange MDA"
  - "invalid apartment state changes"
  - "threading [.NET Framework], apartment states"
  - "apartment states"
  - "threading [.NET Framework], managed debugging assistants"
  - "COM apartment states"
ms.assetid: e56fb9df-5286-4be7-b313-540c4d876cd7
caps.latest.revision: 12
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 12
---
# invalidApartmentStateChange MDA
L'assistente al debug gestito `invalidApartmentStateChange` viene attivato a causa di uno dei due problemi indicati di seguito.  
  
-   Viene eseguito un tentativo di modificare lo stato dell'apartment COM di un thread già inizializzato da COM in uno stato dell'apartment diverso.  
  
-   Lo stato dell'apartment COM di un thread cambia in modo imprevisto.  
  
## Sintomi  
  
-   Lo stato dell'apartment COM di un thread non corrisponde a quello richiesto.  In questo modo i proxy verranno utilizzati per i componenti COM provvisti di un modello di threading diverso da quello attuale.  Ciò può causare la generazione di una <xref:System.InvalidCastException> quando l'oggetto COM viene chiamato mediante interfacce non impostate per il marshalling tra apartment.  
  
-   Lo stato dell'apartment COM del thread è diverso da quello previsto.  Ciò può causare una <xref:System.Runtime.InteropServices.COMException> con un HRESULT RPC\_E\_WRONG\_THREAD, nonchè una <xref:System.InvalidCastException> quando vengono effettuate chiamate su un [Runtime Callable Wrapper](../../../docs/framework/interop/runtime-callable-wrapper.md) \(RCW\).  Può inoltre causare l'accesso simultaneo a componenti COM a thread singolo da parte di più thread con conseguente danneggiamento o perdita di dati.  
  
## Causa  
  
-   Il thread è stato già inizializzato a uno stato dell'apartment COM diverso.  Lo stato dell'apartment di un thread può essere impostato in modo implicito o esplicito.  Nelle operazioni esplicite sono inclusi la proprietà <xref:System.Threading.Thread.ApartmentState%2A?displayProperty=fullName> e i metodi <xref:System.Threading.Thread.SetApartmentState%2A> e <xref:System.Threading.Thread.TrySetApartmentState%2A>.  Un thread creato utilizzando il metodo <xref:System.Threading.Thread.Start%2A> viene impostato in modo implicito su <xref:System.Threading.ApartmentState>, a meno che non venga chiamato il metodo <xref:System.Threading.Thread.SetApartmentState%2A> prima dell'avvio del thread.  Anche il thread principale dell'applicazione viene inizializzato a <xref:System.Threading.ApartmentState>, a meno che nel metodo principale non venga specificato l'attributo <xref:System.STAThreadAttribute>.  
  
-   Sul thread viene chiamato il metodo `CoUninitialize` \(o il metodo `CoInitializeEx`\) con un modello di concorrenza diverso.  
  
## Risoluzione  
 Impostare lo stato dell'apartment del thread prima di avviarne l'esecuzione oppure applicare l'attributo <xref:System.STAThreadAttribute> o <xref:System.MTAThreadAttribute> al metodo principale dell'applicazione.  
  
 Per quanto riguarda la seconda causa, in teoria il codice che chiama il metodo `CoUninitialize` deve essere modificato in modo da ritardare la chiamata fino al momento in cui si approssima la terminazione del thread e in cui quest'ultimo non utilizza più gli RCW e i relativi componenti sottostanti.  Tuttavia, se non è possibile modificare il codice che chiama il metodo `CoUninitialize`, i thread non inizializzati secondo questo sistema non devono utilizzare RCW.  
  
## Effetto sul runtime  
 Questo assistente al debug gestito non produce effetti su CLR.  
  
## Output  
 Lo stato dell'apartment COM del thread attuale e lo stato che il codice ha tentato di applicare.  
  
## Configurazione  
  
```  
<mdaConfig>  
  <assistants>  
    <invalidApartmentStateChange />  
  </assistants>  
</mdaConfig>  
```  
  
## Esempio  
 Nell'esempio di codice riportato di seguito viene illustrata una situazione in cui è possibile attivare l'assistente al debug gestito di questo argomento.  
  
```  
using System.Threading;  
namespace ApartmentStateMDA  
{  
    class Program  
    {  
        static void Main(string[] args)  
        {  
            Thread.CurrentThread.SetApartmentState(ApartmentState.STA);  
        }  
    }  
}  
```  
  
## Vedere anche  
 <xref:System.Runtime.InteropServices.MarshalAsAttribute>   
 [Diagnosing Errors with Managed Debugging Assistants](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)   
 [Interop Marshaling](../../../docs/framework/interop/interop-marshaling.md)