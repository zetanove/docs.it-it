---
title: "Estensione dell&#39;hosting tramite ServiceHostFactory | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: bcc5ae1b-21ce-4e0e-a184-17fad74a441e
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# Estensione dell&#39;hosting tramite ServiceHostFactory
L'API <xref:System.ServiceModel.ServiceHost> standard per i servizi di hosting in [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] è un punto di estendibilità nell'architettura [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  Gli utenti possono derivare proprie classi host da <xref:System.ServiceModel.ServiceHost>, in genere per eseguire l'override di <xref:System.ServiceModel.Channels.CommunicationObject.OnOpening>, per usare <xref:System.ServiceModel.Description.ServiceDescription> al fine di aggiungere endpoint predefiniti in modo imperativo o modificare comportamenti, prima di aprire il servizio.  
  
 Nell'ambiente di self\-hosting, non è necessario creare una classe <xref:System.ServiceModel.ServiceHost> personalizzata, perché si scrive il codice che crea un'istanza dell'host e quindi si chiama <xref:System.ServiceModel.ICommunicationObject.Open> sull'host dopo averne creato l'istanza.  Tra questi due passaggi è possibile eseguire tutte le operazioni che si desidera.  È ad esempio possibile aggiungere una nuova classe <xref:System.ServiceModel.Description.IServiceBehavior>:  
  
```  
public static void Main()  
{  
   ServiceHost host = new ServiceHost( typeof( MyService ) );  
   host.Description.Add( new MyServiceBehavior() );  
   host.Open();  
  
   ...  
}  
  
```  
  
 Questo approccio non è riutilizzabile.  Il codice che modifica la descrizione è inserito nel programma host, in questo caso, la funzione Main\(\), ed è quindi difficile riutilizzare la logica in questione in altri contesti.  Esistono altri modi di aggiungere una classe <xref:System.ServiceModel.Description.IServiceBehavior> che non richiedono codice imperativo.  È possibile derivare un attributo da <xref:System.ServiceModel.ServiceBehaviorAttribute> e inserirlo sul tipo di implementazione del servizio o è possibile rendere configurabile un comportamento personalizzato e comporlo dinamicamente usando la configurazione.  
  
 Tuttavia, per risolvere il problema, è possibile usare anche una leggera variazione dell'esempio.  Un approccio consiste nello spostare il codice che aggiunge ServiceBehavior fuori da `Main()` e inserirlo nel metodo <xref:System.ServiceModel.Channels.CommunicationObject.OnOpening%2A> di un derivato personalizzato di <xref:System.ServiceModel.ServiceHost>:  
  
```  
public class DerivedHost : ServiceHost  
{  
   public DerivedHost( Type t, params Uri baseAddresses ) :  
      base( t, baseAddresses ) {}  
  
   public override void OnOpening()  
   {  
  this.Description.Add( new MyServiceBehavior() );  
   }  
}  
```  
  
 All'interno di `Main()` è quindi possibile usare:  
  
```  
public static void Main()  
{  
   ServiceHost host = new DerivedHost( typeof( MyService ) );  
   host.Open();  
  
   ...  
}  
```  
  
 Ora è stata incapsulata la logica personalizzata in un'astrazione pulita, facilmente riutilizzabile su molti eseguibili host diversi.  
  
 Non è immediatamente ovvio come usare questa classe <xref:System.ServiceModel.ServiceHost> personalizzata da Internet Information Services \(IIS\) o dal servizio di attivazione dei processi di Windows \(WAS\).  Questi ambienti sono diversi dall'ambiente di self\-hosting, perché l'ambiente host è quello che crea l'istanza di <xref:System.ServiceModel.ServiceHost> per conto dell'applicazione.  L'infrastruttura di hosting di IIS e WAS non conosce assolutamente il derivato <xref:System.ServiceModel.ServiceHost> personalizzato.  
  
 La classe <xref:System.ServiceModel.Activation.ServiceHostFactory> è stata progettata per risolvere questo problema di accesso alla classe <xref:System.ServiceModel.ServiceHost> personalizzata da IIS o WAS.  Poiché un host personalizzato derivato da <xref:System.ServiceModel.ServiceHost> viene configurato dinamicamente ed è potenzialmente di vario tipo, l'ambiente host non ne crea mai un'istanza in modo diretto.  Invece, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] usa un modello di factory per fornire un livello di riferimento indiretto tra l'ambiente host e il tipo concreto del servizio.  Se non diversamente detto, usa un'implementazione predefinita di <xref:System.ServiceModel.Activation.ServiceHostFactory> che restituisce un'istanza di <xref:System.ServiceModel.ServiceHost>.  È però possibile fornire anche una propria factory che restituisca l'host derivato specificando il nome del tipo CLR dell'implementazione della factory nella direttiva @ServiceHost.  
  
 Nei casi di base, l'implementazione di una propria factory dovrebbe essere un esercizio semplice.  Di seguito è ad esempio riportata una classe <xref:System.ServiceModel.Activation.ServiceHostFactory> personalizzata che restituisce una classe <xref:System.ServiceModel.ServiceHost> derivata:  
  
```  
public class DerivedFactory : ServiceHostFactory  
{  
   public override ServiceHost CreateServiceHost( Type t, Uri[] baseAddresses )  
   {  
      return new DerivedHost( t, baseAddresses )  
   }  
}  
  
```  
  
 Per usare questa factory al posto di quella predefinita, fornire il nome del tipo nella direttiva @ServiceHost, come illustrato di seguito:  
  
```  
<% @ServiceHost Factory=”DerivedFactory” Service=”MyService” %>  
```  
  
 Sebbene non ci siano limiti tecnici a ciò che è possibile fare alla classe <xref:System.ServiceModel.ServiceHost> restituita da <xref:System.ServiceModel.Activation.ServiceHostFactory.CreateServiceHost%2A>, è consigliabile mantenere l'implementazione della factory quanto più semplice è possibile.  Se si usa un'elevata quantità di logica personalizzata, è preferibile inserire tale logica all'interno dell'host invece che all'interno della factory, in modo che possa essere riutilizzata.  
  
 Esiste un ulteriore livello dell'API di hosting che dovrebbe essere qui citato.  [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] dispone anche di <xref:System.ServiceModel.ServiceHostBase> e <xref:System.ServiceModel.Activation.ServiceHostFactoryBase>, da cui derivano rispettivamente <xref:System.ServiceModel.ServiceHost> e <xref:System.ServiceModel.Activation.ServiceHostFactory>.  Queste classi sono destinate a scenari più avanzati, in cui è necessario scambiare ampie parti del sistema dei metadati con proprie creazioni personalizzate.