---
title: "Attenuazione: Rendering di finestre WPF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 28ed6bf8-141b-4b73-a4e3-44a99fae5084
caps.latest.revision: 3
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 3
---
# Attenuazione: Rendering di finestre WPF
In [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] in esecuzione in Windows 8 e versioni successive viene eseguito il rendering dell'intera finestra senza ritaglio quando la finestra si estende al di fuori di un singolo schermo in uno scenario di utilizzo di più monitor.  
  
## Impatto  
 In generale, il rendering di un'intera finestra su più monitor senza ritaglio è il comportamento previsto.  Tuttavia, in Windows 7 e versioni precedenti le finestre WPF vengono ritagliate quando si estendono oltre un singolo schermo perché il rendering di una parte della finestra sul secondo monitor ha un impatto significativo sulle prestazioni.  
  
 L'impatto esatto del rendering di finestre WPF su più monitor in Windows 8 e versioni successive non è precisamente quantificabile poiché dipende da numerosi fattori.  In alcuni casi, potrebbe produrre un impatto indesiderato sulle prestazioni, in particolare per gli utenti che eseguono applicazioni a elevato utilizzo di grafica e hanno finestre che si estendono su più monitor.  In altri casi, si potrebbe semplicemente volere un comportamento coerente tra le versioni di .NET Framework.  
  
## Attenuazione  
 È possibile disabilitare questa modifica e ripristinare il comportamento precedente di ritaglio di una finestra WPF quando si estende oltre un singolo schermo.  Questo risultato può essere raggiunto in due modi:  
  
-   Aggiungendo l'elemento `<EnableMultiMonitorDisplayClipping>` nella sezione `<appSettings>` del file di configurazione dell'applicazione, è possibile disabilitare o abilitare questo comportamento nelle app che eseguono Windows 8 o versione successiva.  Ad esempio, la sezione di configurazione seguente disabilita il rendering senza ritaglio:  
  
    ```  
  
    <appSettings>  
        <add key="EnableMultiMonitorDisplayClipping" value="true"/>  
      </appSettings>  
  
    ```  
  
     L'impostazione di configurazione `<EnableMultiMonitorDisplayClipping>` può avere uno dei due valori seguenti:  
  
    -   `true` per consentire il ritaglio delle finestre in base ai confini del monitor durante il rendering.  
  
    -   `false` per disabilitare il ritaglio delle finestre in base ai confini del monitor durante il rendering.  
  
-   Impostando la proprietà <xref:System.Windows.CoreCompatibilityPreferences.EnableMultiMonitorDisplayClipping%2A> su `true` all'avvio dell'app.  
  
## Vedere anche  
 [Modifiche al runtime](../../../docs/framework/migration-guide/runtime-changes-in-the-net-framework-4-6.md)