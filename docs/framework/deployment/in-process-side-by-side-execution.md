---
title: "Esecuzione side-by-side in-process | Microsoft Docs"
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
  - "esecuzione affiancata in-process"
  - "esecuzione affiancata, in-process"
ms.assetid: 18019342-a810-4986-8ec2-b933a17c2267
caps.latest.revision: 25
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 25
---
# Esecuzione side-by-side in-process
A partire da [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)], è possibile utilizzare l'hosting side\-by\-side in\-process per eseguire più versioni di Common Language Runtime \(CLR\) in un unico processo.  Per impostazione predefinita, i componenti COM gestiti vengono eseguiti con la versione di .NET Framework con la quale sono stati compilati, indipendentemente dalla versione caricata per il processo.  
  
## Background  
 Da sempre .NET Framework fornisce l'hosting side\-by\-side per le applicazioni di codice gestito; prima di [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)], però, questa funzionalità non era disponibile per i componenti COM gestiti.  In passato, i componenti COM gestiti caricati in un processo venivano eseguiti con la versione del runtime già caricata o con l'ultima versione di .NET Framework installata.  Se la versione non fosse stata compatibile con il componente COM, questo avrebbe dato esito negativo.  
  
 Il nuovo approccio all'hosting side\-by\-side fornito in [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] assicura quanto segue:  
  
-   L'installazione di una nuova versione di .NET Framework non influisce sulle applicazioni esistenti.  
  
-   Le applicazioni vengono eseguite con la versione di .NET Framework con la quale sono state compilate.  Salvo esplicita indicazione, non viene utilizzata la nuova versione di .NET Framework.  Tuttavia, per le applicazioni è più facile passare all'utilizzo di una nuova versione di .NET Framework.  
  
## Effetti sugli utenti e gli sviluppatori  
  
-   **Utenti finali e amministratori di sistema**.  Questi utenti possono ora confidare maggiormente nel fatto che, quando installano una nuova versione del runtime, che sia in modo indipendente o con un'applicazione, essa non avrà alcun impatto sui computer in uso.  Le applicazioni esistenti continueranno a essere eseguite come in precedenza.  
  
-   **Sviluppatori di applicazioni**.  L'hosting side\-by\-side non ha pressoché alcun effetto sugli sviluppatori di applicazioni.  Per impostazione predefinita, le applicazioni vengono sempre eseguite con la versione di .NET Framework con la quale sono state compilate; questo aspetto non è cambiato.  Tuttavia, gli sviluppatori possono eseguire l'override di questo comportamento e fare in modo che l'applicazione venga eseguita con una versione più recente di .NET Framework \(vedere lo [scenario 2](#scenarios)\).  
  
-   **Sviluppatori di librerie e consumer**.  L'hosting side\-by\-side non risolve i problemi di compatibilità che gli sviluppatori di librerie devono affrontare.  Una libreria direttamente caricata da un'applicazione, che sia tramite un riferimento diretto o una chiamata a <xref:System.Reflection.Assembly.Load%2A?displayProperty=fullName>, continua a utilizzare il runtime dell'oggetto <xref:System.AppDomain> nel quale è caricata.  È necessario eseguire un test delle librerie con tutte le versioni di .NET Framework che si desidera supportare.  Se un'applicazione viene compilata utilizzando il runtime di [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] ma include una libreria compilata con un runtime precedente, anche quella libreria utilizzerà il runtime di [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)].  Tuttavia, se si ha un'applicazione compilata utilizzando un runtime precedente e una libreria compilata con [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)], è necessario forzare l'applicazione affinché utilizzi anch'essa [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] \(vedere lo [scenario 3](#scenarios)\).  
  
-   **Sviluppatori di componenti COM gestiti**.  In passato, i componenti COM gestiti venivano eseguiti automaticamente utilizzando la versione del runtime più recente installata nel computer.  Ora è possibile eseguire i componenti COM con la versione del runtime con la quale sono stati compilati.  
  
     Come illustrato nella seguente tabella, i componenti compilati con .NET Framework versione 1.1 possono essere eseguiti side\-by\-side con componenti compilati con la versione 4; non possono però essere eseguiti con componenti compilati con la versione 2.0, 3.0 o 3.5, poiché l'hosting side\-by\-side non è disponibile per tali versioni.  
  
    |Versione di .NET Framework|1.1|2.0 \- 3.5|4|  
    |--------------------------------|---------|----------------|-------|  
    |1.1|Non applicabile|No|Yes|  
    |2.0 \- 3.5|No|Non applicabile|Yes|  
    |4|Yes|Yes|Non applicabile|  
  
> [!NOTE]
>  Le versioni 3.0 e 3.5 di .NET Framework si basano in modo incrementale sulla versione 2.0 e non richiedono l'esecuzione side\-by\-side.  Intrinsecamente, si tratta della stessa versione.  
  
<a name="scenarios"></a>   
## Scenari comuni di hosting side\-by\-side  
  
-   **Scenario 1:** applicazione nativa che utilizza componenti COM compilati con versioni di .NET Framework precedenti.  
  
     Versioni di .NET Framework installate: [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] e tutte le altre versioni di .NET Framework utilizzate dai componenti COM.  
  
     Cosa fare: in questo scenario non occorre fare nulla.  I componenti COM verranno eseguiti con la versione di .NET Framework con la quale sono stati registrati.  
  
-   **Scenario 2**: applicazione gestita compilata con [!INCLUDE[net_v20SP1_short](../../../includes/net-v20sp1-short-md.md)], da eseguire preferibilmente con [!INCLUDE[dnprdnext](../../../includes/dnprdnext-md.md)], oppure con [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] se la versione 2.0 non è presente.  
  
     Versioni di .NET Framework installate: una versione di .NET Framework precedente e [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)].  
  
     Cosa fare: nel [file di configurazione dell'applicazione](../../../docs/framework/configure-apps/index.md) contenuto nella directory dell'applicazione, utilizzare l'[elemento \<startup\>](../../../docs/framework/configure-apps/file-schema/startup/startup-element.md) e l'[elemento \<supportedRuntime\>](../../../docs/framework/configure-apps/file-schema/startup/supportedruntime-element.md) impostati come segue:  
  
    ```  
    <configuration>  
      <startup >  
        <supportedRuntime version="v2.0.50727" />  
        <supportedRuntime version="v4.0" />  
      </startup>  
    </configuration>  
    ```  
  
-   **Scenario 3:** applicazione nativa che utilizza componenti COM compilati con versioni di .NET Framework precedenti, da eseguire con [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)].  
  
     Versioni di .NET Framework installate: [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)].  
  
     Cosa fare: nel file di configurazione dell'applicazione contenuto nella directory dell'applicazione, utilizzare l'elemento `<startup>` con l'attributo `useLegacyV2RuntimeActivationPolicy` impostato su `true` e l'elemento `<supportedRuntime>` impostato come segue:  
  
    ```  
    <configuration>  
      <startup useLegacyV2RuntimeActivationPolicy="true">  
        <supportedRuntime version="v4.0" />  
      </startup>  
    </configuration>  
    ```  
  
## Esempio  
 Nell'esempio seguente viene illustrato un host COM non gestito che esegue un componente COM gestito con la versione di .NET Framework per il cui utilizzo il componente è stato compilato.  
  
 Per eseguire l'esempio, compilare e registrare il seguente componente COM gestito utilizzando [!INCLUDE[net_v35_long](../../../includes/net-v35-long-md.md)].  Per registrare il componente, nel menu **Progetto**, scegliere **Proprietà**, cliccare sulla scheda **Compilazione** quindi selezionare la casella di controllo **Registra per interoperabilità COM**.  
  
```  
using System;  
using System.Collections.Generic;  
using System.Linq;  
using System.Text;  
using System.Runtime.InteropServices;  
  
namespace BasicComObject  
{  
    [ComVisible(true), Guid("9C99C4B5-CA54-4c58-8988-49B6811BA53B")]  
    public class MyObject : SimpleObjectModel.IPrintInfo  
    {  
        public MyObject()  
        {  
        }  
        public void PrintInfo()  
        {  
            Console.WriteLine("MyObject was activated in {0} runtime in:\n\tAppDomain {1}:{2}", System.Runtime.InteropServices.RuntimeEnvironment.GetSystemVersion(), AppDomain.CurrentDomain.Id, AppDomain.CurrentDomain.FriendlyName);  
        }  
    }  
}  
```  
  
 Compilare la seguente applicazione C\+\+ non gestita, la quale attiva l'oggetto COM creato con l'esempio precedente.  
  
```  
#include "stdafx.h"  
#include <string>  
#include <iostream>  
#include <objbase.h>  
#include <string.h>  
#include <process.h>  
  
using namespace std;  
  
int _tmain(int argc, _TCHAR* argv[])  
{  
    char input;  
    CoInitialize(NULL) ;  
    CLSID clsid;  
    HRESULT hr;  
    HRESULT clsidhr = CLSIDFromString(L"{9C99C4B5-CA54-4c58-8988-49B6811BA53B}",&clsid);  
    hr = -1;  
    if (FAILED(clsidhr))  
    {  
        printf("Failed to construct CLSID from String\n");  
    }  
    UUID id = __uuidof(IUnknown);  
    IUnknown * pUnk = NULL;  
    hr = ::CoCreateInstance(clsid,NULL,CLSCTX_INPROC_SERVER,id,(void **) &pUnk);  
    if (FAILED(hr))  
    {  
        printf("Failed CoCreateInstance\n");  
    }else  
    {  
        pUnk->AddRef();  
        printf("Succeeded\n");  
    }  
  
    DISPID dispid;  
    IDispatch* pPrintInfo;  
    pUnk->QueryInterface(IID_IDispatch, (void**)&pPrintInfo);  
    OLECHAR FAR* szMethod[1];  
    szMethod[0]=OLESTR("PrintInfo");   
    hr = pPrintInfo->GetIDsOfNames(IID_NULL,szMethod, 1, LOCALE_SYSTEM_DEFAULT, &dispid);  
    DISPPARAMS dispparams;  
    dispparams.cNamedArgs = 0;  
    dispparams.cArgs = 0;  
    VARIANTARG* pvarg = NULL;  
    EXCEPINFO * pexcepinfo = NULL;  
    WORD wFlags = DISPATCH_METHOD ;  
;  
    LPVARIANT pvRet = NULL;  
    UINT * pnArgErr = NULL;  
    hr = pPrintInfo->Invoke(dispid,IID_NULL, LOCALE_USER_DEFAULT, wFlags,  
        &dispparams, pvRet, pexcepinfo, pnArgErr);  
    printf("Press Enter to exit");  
    scanf_s("%c",&input);  
    CoUninitialize();  
    return 0;  
}  
  
```  
  
## Vedere anche  
 [Elemento \<startup\>](../../../docs/framework/configure-apps/file-schema/startup/startup-element.md)   
 [Elemento \<supportedRuntime\>](../../../docs/framework/configure-apps/file-schema/startup/supportedruntime-element.md)