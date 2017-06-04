---
title: "Procedura: proteggere un servizio con un certificato X.509 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2d06c2aa-d0d7-4e5e-ad7e-77416aa1c10b
caps.latest.revision: 8
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 8
---
# Procedura: proteggere un servizio con un certificato X.509
La protezione di un servizio con un certificato X.509 è una tecnica di base utilizzata dalla maggior parte delle associazioni in [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].In questo argomento vengono illustrati i passaggi di configurazione di un servizio indipendente con un certificato X.509.  
  
 Un prerequisito è un certificato valido utilizzabile per autenticare il server.Il certificato deve essere emesso al server da un autorità di certificazione attendibile.Se il certificato non è valido, nessun client che tenti di utilizzare il servizio lo reputerà attendibile e, di conseguenza, non verrà stabilita nessuna connessione.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] utilizzo dei certificati, vedere [Utilizzo dei certificati](../../../../docs/framework/wcf/feature-details/working-with-certificates.md).  
  
### Per configurare un servizio con un certificato utilizzando codice.  
  
1.  Creare il contratto di servizio e il servizio implementato.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Progettazione e implementazione di servizi](../../../../docs/framework/wcf/designing-and-implementing-services.md).  
  
2.  Creare un'istanza della classe <xref:System.ServiceModel.WSHttpBinding> e impostarne la modalità sicura su <xref:System.ServiceModel.SecurityMode>, come illustrato nel codice seguente.  
  
     [!code-csharp[C_SecureWithCertificate#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#1)]
     [!code-vb[C_SecureWithCertificate#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#1)]  
  
3.  Creare due variabili <xref:System.Type>, una per il tipo di contratto e una per il contratto implementato, come illustrato nel codice seguente.  
  
     [!code-csharp[C_SecureWithCertificate#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#2)]
     [!code-vb[C_SecureWithCertificate#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#2)]  
  
4.  Creare un'istanza della classe <xref:System.Uri> per l'indirizzo di base del servizio.Dato che `WSHttpBinding` utilizza il trasporto HTTP, l'Uniform Resource Identifier \(URI\) deve iniziare con quello schema. In caso contrario, [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] genererà un'eccezione all'apertura del servizio.  
  
     [!code-csharp[C_SecureWithCertificate#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#3)]
     [!code-vb[C_SecureWithCertificate#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#3)]  
  
5.  Creare una nuova istanza della classe <xref:System.ServiceModel.ServiceHost> con la variabile del tipo di contratto implementato e l'URI.  
  
     [!code-csharp[C_SecureWithCertificate#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#4)]
     [!code-vb[C_SecureWithCertificate#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#4)]  
  
6.  Aggiungere un <xref:System.ServiceModel.Description.ServiceEndpoint> al servizio utilizzando il metodo <xref:System.ServiceModel.ServiceHost.AddServiceEndpoint%2A>.Passare il contratto, l'associazione e un indirizzo endpoint al costruttore, come illustrato nel codice seguente.  
  
     [!code-csharp[C_SecureWithCertificate#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#5)]
     [!code-vb[C_SecureWithCertificate#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#5)]  
  
7.  Facoltativo.Per recuperare metadati dal servizio, creare un nuovo oggetto <xref:System.ServiceModel.Description.ServiceMetadataBehavior> e impostare la proprietà <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpGetEnabled%2A> su `true`.  
  
     [!code-csharp[C_SecureWithCertificate#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#6)]
     [!code-vb[C_SecureWithCertificate#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#6)]  
  
8.  Utilizzare il metodo <xref:System.ServiceModel.Security.X509CertificateRecipientServiceCredential.SetCertificate%2A> della classe <xref:System.ServiceModel.Security.X509CertificateRecipientServiceCredential> per aggiungere il certificato valido al servizio.Il metodo può utilizzare uno di numerosi metodi per trovare un certificato.Nell'esempio viene utilizzata l'enumerazione <xref:System.Security.Cryptography.X509Certificates.X509FindType>.L'enumerazione specifica che il valore fornito è il nome dell'entità alla quale è stato emesso il certificato.  
  
     [!code-csharp[C_SecureWithCertificate#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#7)]
     [!code-vb[C_SecureWithCertificate#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#7)]  
  
9. Chiamare il metodo <xref:System.ServiceModel.Channels.CommunicationObject.Open%2A> per avviare l'ascolto del servizio.Se si sta creando un'applicazione console, chiamare il metodo <xref:System.Console.ReadLine%2A> per tenere il servizio nello stato di ascolto.  
  
     [!code-csharp[C_SecureWithCertificate#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#8)]
     [!code-vb[C_SecureWithCertificate#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#8)]  
  
## Esempio  
 Nell'esempio seguente viene utilizzato il metodo <xref:System.ServiceModel.Security.X509CertificateRecipientServiceCredential.SetCertificate%2A> per configurare un servizio con un certificato X.509.  
  
 [!code-csharp[C_SecureWithCertificate#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#9)]
 [!code-vb[C_SecureWithCertificate#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#9)]  
  
## Compilazione del codice  
 Per compilare il codice sono necessari gli spazi dei nomi seguenti:  
  
-   <xref:System>  
  
-   <xref:System.ServiceModel>  
  
-   <xref:System.ServiceModel.Channels>  
  
-   <xref:System.Web.Services.Description>  
  
-   <xref:System.Security.Cryptography.X509Certificates>  
  
-   <xref:System.Runtime.Serialization>  
  
## Vedere anche  
 [Utilizzo dei certificati](../../../../docs/framework/wcf/feature-details/working-with-certificates.md)