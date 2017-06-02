---
title: "Configurazione del servizio di condivisione delle porte Net.TCP | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b6dd81fa-68b7-4e1b-868e-88e5901b7ea0
caps.latest.revision: 20
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 20
---
# Configurazione del servizio di condivisione delle porte Net.TCP
I servizi indipendenti che usano il trasporto Net.TCP possono controllare diverse impostazioni avanzate, quali esempio `ListenBacklog` e `MaxPendingAccepts`, che regolano il comportamento del socket TCP sottostante usato per la comunicazione di rete.  Tuttavia, queste impostazioni per ogni socket si applicano solo al livello di associazione, se l'associazione del trasporto ha disattivato la condivisione delle porte, che è attivata per impostazione predefinita.  
  
 Quando un'associazione net.tcp attiva la condivisione delle porte, impostando `portSharingEnabled =true` sull'elemento di associazione del trasporto, consente implicitamente a un processo esterno, ovvero SMSvcHost.exe, che ospita il servizio di condivisione delle porte Net.TCP, di gestire il socket TCP per suo conto.  Ad esempio, quando si usa TCP, specificare:  
  
```  
    <tcpTransport   
        portSharingEnabled="true"  
/>  
```  
  
 Se configurate in questo modo, le impostazioni socket specificate sull'elemento di associazione del trasporto del servizio vengono ignorate a vantaggio delle impostazioni socket specificate da SMSvcHost.exe.  
  
 Per configurare SMSvcHost.exe, creare un file di configurazione XML denominato SmSvcHost.exe.config e posizionarlo nella stessa directory fisica dell'eseguibile SMSvcHost.exe, ad esempio C:\\Windows\\Microsoft.NET\\Framework\\v4.5.  
  
 Di seguito viene illustrato un file SMSvcHost.exe.config di esempio, con le impostazioni predefinite per tutti i valori configurabili dichiarate in modo esplicito.  
  
```  
<configuration>  
   <system.serviceModel.activation>  
       <net.tcp listenBacklog="16" <!—16 * # of processors -->  
          maxPendingAccepts="4"<!— 4 * # of processors -->  
          maxPendingConnections="100"  
          receiveTimeout="00:00:30" <!—30 seconds -->  
          teredoEnabled="false">  
          <allowAccounts>  
             <!-- LocalSystem account -->  
             <add securityIdentifier="S-1-5-18"/>  
             <!-- LocalService account -->  
             <add securityIdentifier="S-1-5-19"/>  
             <!-- Administrators account -->  
             <add securityIdentifier="S-1-5-20"/>  
             <!-- Network Service account -->  
             <add securityIdentifier="S-1-5-32-544" />  
             <!-- IIS_IUSRS account (Vista only) -->  
             <add securityIdentifier="S-1-5-32-568"/>  
           </allowAccounts>  
       </net.tcp>  
</configuration>  
```  
  
## Quando modificare SMSvcHost.exe.config  
 In generale, quando si modifica il contenuto del file SMSvcHost.exe.config è necessario fare attenzione, poiché qualsiasi impostazione di configurazione in esso specificata influenza tutti i servizi presenti in un computer che usa il servizio di condivisione delle porte Net.TCP.  Sono incluse le applicazioni su [!INCLUDE[wv](../../../../includes/wv-md.md)] che usano le funzionalità di attivazione TCP del servizio di attivazione dei processi di Windows \(WAS\).  
  
 Talvolta può però essere necessario modificare la configurazione predefinita del servizio di condivisione delle porte Net.TCP.  Ad esempio, il valore predefinito per `maxPendingAccepts` è 4 volte il numero di processori.  Nei server che ospitano un gran numero di servizi che usano la condivisione delle porte potrebbe essere necessario aumentare questo valore per raggiungere la velocità effettiva massima.  Il valore predefinito di `maxPendingConnections` è 100.  Considerare la possibilità di aumentare questo valore se sono presenti più client simultanei che chiamano il servizio e quest'ultimo sta rimuovendo connessioni client.  
  
 SMSvcHost.exe.config contiene inoltre informazioni sulle identità dei processi che potrebbero usare il servizio di condivisione delle porte.  Quando un processo si connette al servizio di condivisione delle porte per usare una porta TCP condivisa, l'identità del processo di connessione viene controllata a fronte di un elenco delle identità autorizzate a usare il servizio di condivisione delle porte.  Queste identità sono specificate come ID di sicurezza \(SID\) nella sezione \<allowAccounts\> del file SMSvcHost.exe.config.  Per impostazione predefinita, l'autorizzazione a usare il servizio di condivisione delle porte viene concessa agli account di sistema \(LocalService, LocalSystem e NetworkService\) così come ai membri del gruppo Administrators.  Le applicazioni che consentono l'esecuzione di un processo con un'altra identità, ad esempio un'identità utente, per connettersi al servizio di condivisione delle porte, devono aggiungere in modo esplicito il SID appropriato al file SMSvcHost.exe.config. Queste modifiche non vengono applicate fino a quando il processo SMSvc.exe non viene riavviato.  
  
> [!NOTE]
>  Nei sistemi [!INCLUDE[wv](../../../../includes/wv-md.md)] con il controllo dell'account utente attivato, gli utenti locali necessitano di autorizzazioni elevate anche se il proprio account è un membro del gruppo Administrators.  Per consentire a questi utenti di usare il servizio di condivisione delle porte senza l'elevazione dei privilegi, è necessario aggiungere in modo esplicito il SID dell'utente, o di un gruppo di cui l'utente è membro, alla sezione \<allowAccounts\> del file SMSvcHost.exe.config.  
  
> [!WARNING]
>  Il file SMSvcHost.exe.config predefinito specifica un elemento `etwProviderId` personalizzato per impedire che la traccia di SMSvcHost.exe interferisca con le tracce del servizio.  
  
## Vedere anche  
 [\<net.tcp\>](../../../../docs/framework/configure-apps/file-schema/wcf/net-tcp.md)