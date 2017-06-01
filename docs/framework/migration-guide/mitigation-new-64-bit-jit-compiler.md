---
title: 'Mitigazione: Nuovo compilatore JIT a 64 bit | Documenti di Microsoft'
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
helpviewer_keywords:
- JIT compiler, 64-bit
- JIT compilation, 64-bit
- RyuJIT compiler
ms.assetid: 0332dabc-72c5-4bdc-8975-20d717802b17
caps.latest.revision: 6
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: Human Translation
ms.sourcegitcommit: 407b31c8b5825093d9ba6bab6329aaf8dd821572
ms.openlocfilehash: f5bab95cc5a4ff49a0ff81e209f0a71c78914976
ms.contentlocale: it-it
ms.lasthandoff: 05/22/2017

---
# <a name="mitigation-new-64-bit-jit-compiler"></a>Mitigazione: Nuovo compilatore JIT a 64 bit
A partire da .NET Framework 4.6, il runtime include un nuovo compilatore JIT a 64 bit per la compilazione JIT. Questa modifica non riguarda il compilatore JIT a 32 bit.  
  
## <a name="unexpected-behavior-or-exceptions"></a>Comportamento imprevisto o eccezioni  
 In alcuni casi, la compilazione con il nuovo compilatore JIT a 64 bit comporta un'eccezione di runtime o un comportamento che non viene osservato durante l'esecuzione di codice compilato dal compilatore JIT a 64 bit precedente. Le differenze note includono quanto segue:  
  
> [!IMPORTANT]
>  Tutti questi problemi noti sono stati risolti nel nuovo compilatore a 64 bit rilasciato con .NET Framework 4.6.2. La maggior parte dei problemi è stata inoltre risolta nelle service release di .NET Framework 4.6 e 4.6.1 incluse con Windows Update. È possibile evitare questi problemi assicurandosi che la versione di Windows sia aggiornata o eseguendo l'aggiornamento a .NET Framework 4.6.2.  
  
-   In determinate condizioni, un'operazione di conversione unboxing può generare <xref:System.NullReferenceException> nelle build di rilascio con l'ottimizzazione attivata.  
  
-   In alcuni casi l'esecuzione del codice di produzione in un corpo del metodo di grandi dimensioni può generare <xref:System.StackOverflowException>.  
  
-   In determinate condizioni, le strutture passate a un metodo vengono considerate come tipi di riferimento piuttosto che tipi di valore nelle build di rilascio. Una delle manifestazioni di questo problema è che i singoli elementi in una raccolta vengono visualizzati in un ordine imprevisto.  
  
-   In determinate condizioni, il confronto dei valori di <xref:System.UInt16> con il set di bit elevato non è corretto se l'ottimizzazione è abilitata.  
  
-   In determinate condizioni, in particolare durante l'inizializzazione dei valori della matrice, è possibile che l'inizializzazione della memoria con l'istruzione IL <xref:System.Reflection.Emit.OpCodes.Initblk?displayProperty=fullName> venga eseguita con un valore non corretto. Ciò può generare un'eccezione non gestita o un output non corretto.  
  
-   In alcuni casi rari, un test condizionale dei bit può restituire il valore <xref:System.Boolean> non corretto o generare un'eccezione se sono abilitate le ottimizzazioni del compilatore.  
  
-   In determinate condizioni, se un'istruzione `if` viene usata per testare una condizione prima di immettere un blocco `try` e in uscita dal blocco `try`, e la stessa condizione viene valutata nel blocco `catch` o `finally`, il nuovo compilatore JIT a 64 bit rimuove la condizione `if` dal blocco `catch` o `finally` quando ottimizza il codice. Di conseguenza, il codice contenuto nell'istruzione `if` nel blocco `catch` o `finally` viene eseguita in modo non condizionale.  
  
<a name="General"></a>   
## <a name="mitigation-of-known-issues"></a>Mitigazione dei problemi noti  
 Se si verificano i problemi elencati in precedenza, è possibile risolverli effettuando una delle operazioni seguenti:  
  
-   Eseguire l'aggiornamento a .NET Framework 4.6.2. Il nuovo compilatore a 64 bit incluso in .NET Framework 4.6.2 risolve tutti questi problemi noti.  
  
-   Assicurarsi che la versione di Windows venga aggiornata tramite l'esecuzione di Windows Update. Gli aggiornamenti dei servizi per .NET Framework 4.6 e 4.6.1 risolvono tutti questi problemi, ad eccezione di <xref:System.NullReferenceException> in un'operazione di conversione unboxing.  
  
-   Eseguire la compilazione con la versione precedente del compilatore JIT a 64 bit. Vedere la sezione [Mitigazione di altri problemi](#Other) per altre informazioni su come eseguire questa operazione.  
  
<a name="Other"></a>   
## <a name="mitigation-of-other-issues"></a>Mitigazione di altri problemi  
 Nel caso di qualsiasi altra differenza nel comportamento tra il codice compilato con la versione precedente del compilatore a 64 bit e quello compilato con la versione nuova, oppure tra le versioni di debug e rilascio dell'app compilate entrambe con il nuovo compilatore JIT a 64 bit, è possibile eseguire le operazioni seguenti per compilare l'app con la versione precedente del compilatore JIT a 64 bit:  
  
-   In base all'applicazione, è possibile aggiungere l'elemento [\<useLegacyJit>](../../../docs/framework/configure-apps/file-schema/runtime/uselegacyjit-element.md) al file di configurazione dell'applicazione. Le operazioni seguenti consentono di disattivare la compilazione con il nuovo compilatore JIT a 64 bit e usare invece il compilatore JIT a 64 bit legacy.  
  
    ```xml  
    <?xml version ="1.0"?>  
    <configuration>  
        <runtime>  
           <useLegacyJit enabled="1" />  
        </runtime>  
    </configuration>  
    ```  
  
-   Per ogni utente è possibile aggiungere un valore `REG_DWORD` denominato `useLegacyJit` per la chiave `HKEY_CURRENT_USER\SOFTWARE\Microsoft\.NETFramework` del Registro di sistema. Il valore 1 abilita il compilatore JIT a 64 bit legacy, mentre il valore 0 lo disattiva e consente di abilitare il nuovo compilatore JIT a 64 bit.  
  
-   Per ogni macchina è possibile aggiungere un valore `REG_DWORD` denominato `useLegacyJit` per la chiave `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework` del Registro di sistema. Il valore 1 abilita il compilatore JIT a 64 bit legacy, mentre il valore 0 lo disattiva e consente di abilitare il nuovo compilatore JIT a 64 bit.  
  
 È possibile inoltre inviare i dettagli sul problema segnalando un bug in [Microsoft Connect](https://connect.microsoft.com/VisualStudio).  
  
## <a name="see-also"></a>Vedere anche  
 [Modifiche al runtime](../../../docs/framework/migration-guide/runtime-changes-in-the-net-framework-4-6.md)   
 [\<useLegacyJit> Element](../../../docs/framework/configure-apps/file-schema/runtime/uselegacyjit-element.md) (Elemento useLegacyJit>)

