---
title: "How to: Specify the Security Context for Services | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Windows Service applications, security"
  - "security [Visual Studio], contexts"
  - "contexts, Visual Studio security"
  - "security [Visual Studio], service applications"
  - "ServiceProcessInstaller class, security context"
  - "services, security"
  - "ServiceInstaller class, security context"
ms.assetid: 02187c7b-dbf2-45f2-96c2-e11010225a22
caps.latest.revision: 10
author: "ghogen"
ms.author: "ghogen"
manager: "douge"
caps.handback.revision: 10
---
# How to: Specify the Security Context for Services
In base all'impostazione predefinita, i servizi vengono eseguiti in un contesto di sicurezza diverso rispetto a quello dell'utente connesso.  Il contesto è quello dell'account di sistema predefinito, `LocalSystem`, che fornisce ai servizi privilegi di accesso alle risorse di sistema diversi da quelli dell'utente.  È possibile modificare questo comportamento per specificare un account utente diverso in base al quale eseguire il servizio.  
  
 Impostare il contesto di sicurezza modificando la proprietà <xref:System.ServiceProcess.ServiceProcessInstaller.Account%2A> per il processo nel quale viene eseguito il servizio.  Tale proprietà consente di assegnare al servizio uno dei quattro tipi di account seguenti:  
  
-   `User`, che genera la richiesta del sistema di immettere un nome utente e una password validi al momento dell'installazione del servizio e comporta l'esecuzione del servizio nel contesto di un account specificato da un singolo utente della rete.  
  
-   `LocalService`, che comporta l'esecuzione del servizio nel contesto di un account che opera come utente non privilegiato nel computer locale e presenta credenziali anonime a tutti i server remoti.  
  
-   `LocalSystem`, che viene eseguita nel contesto di un account che sono associati privilegi locali e presenta le credenziali del computer a tutti i server remoti,  
  
-   `NetworkService`, che comporta l'esecuzione del servizio nel contesto di un account che opera come utente non privilegiato nel computer locale e presenta le credenziali del computer a tutti i server remoti.  
  
 Per ulteriori informazioni, vedere l'enumerazione <xref:System.ServiceProcess.ServiceAccount>.  
  
### Per specificare il contesto di sicurezza per un servizio  
  
1.  Dopo aver creato il servizio, aggiungere i programmi di installazione necessari.  Per ulteriori informazioni, vedere [How to: Add Installers to Your Service Application](../../../docs/framework/windows-services/how-to-add-installers-to-your-service-application.md).  
  
2.  Nella finestra di progettazione accedere alla classe `ProjectInstaller`, quindi fare clic sul programma di installazione del processo del servizio utilizzato.  
  
    > [!NOTE]
    >  Per ciascuna applicazione di servizio, nella classe `ProjectInstaller` esistono almeno due componenti di installazione, ossia un componente per installare i processi per tutti i servizi del progetto e un programma di installazione per ciascun servizio contenuto nell'applicazione.  In questo caso, selezionare <xref:System.ServiceProcess.ServiceProcessInstaller>.  
  
3.  Nella finestra **Proprietà** impostare <xref:System.ServiceProcess.ServiceProcessInstaller.Account%2A> sul valore appropriato.  
  
## Vedere anche  
 [Introduction to Windows Service Applications](../../../docs/framework/windows-services/introduction-to-windows-service-applications.md)   
 [How to: Add Installers to Your Service Application](../../../docs/framework/windows-services/how-to-add-installers-to-your-service-application.md)   
 [How to: Create Windows Services](../../../docs/framework/windows-services/how-to-create-windows-services.md)