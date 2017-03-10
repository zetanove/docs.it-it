---
title: "My.Forms Object | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "My.Forms"
  - "My.MyProject.Forms"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "My.Forms object"
ms.assetid: f6bff4e6-6769-4294-956b-037aa6106d2a
caps.latest.revision: 22
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 22
---
# My.Forms Object
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Fornisce le proprietà che consentono di accedere alle istanze di ciascun form Windows dichiarato nel progetto corrente.  
  
## Note  
 L'oggetto `My.Forms` fornisce un'istanza di ciascun form nel progetto corrente.  Il nome della proprietà è uguale a quello del form a cui accede.  Per informazioni sull'aggiunta di form a un progetto, vedere [How to: Add Windows Forms to a Project](http://msdn.microsoft.com/it-it/3d7bb25f-fd90-47cf-9378-fa0d764686c1).  
  
 Per accedere ai form forniti dall'oggetto `My.Forms`, è possibile utilizzare il nome del form senza qualificazione.  Il nome della proprietà è uguale a quello del tipo di form per consentire di accedere al form come se fosse un'istanza predefinita.  Ad esempio `My.Forms.Form1.Show` è equivalente a `Form1.Show`.  
  
 L'oggetto `My.Forms` espone solo i form associati al progetto corrente  e non fornisce accesso ai form dichiarati nelle DLL di riferimento.  Per accedere a un form fornito da una DLL è necessario utilizzare il nome completo del form, ovvero *NomeDLL*. *NomeForm*.  
  
 È possibile utilizzare la proprietà <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OpenForms%2A> per ottenere una raccolta di tutti i form aperti dell'applicazione.  
  
 L'oggetto e le relative proprietà sono disponibili solo per le applicazioni Windows.  
  
## Proprietà  
 Ciascuna proprietà dell'oggetto `My.Forms` fornisce accesso a un'istanza di un form nel progetto corrente.  Il nome della proprietà è lo stesso di quello del form a cui accede e il tipo di proprietà equivale a quello del tipo di form.  
  
> [!NOTE]
>  In caso di conflitto tra nomi, il nome della proprietà per accedere al form sarà *SpazioNomiPrimoLivello*\_*SpazioNomi*\_*NomeForm*.  Si considerino ad esempio i due form denominati `Form1.`. Se uno di questi due form si trova nello spazio dei nomi di primo livello `WindowsApplication1` e nello spazio dei nomi `Namespace1`, è necessario accedere al form mediante `My.Forms.WindowsApplication1_Namespace1_Form1`.  
  
 L'oggetto `My.Forms` consente di accedere all'istanza del form principale dell'applicazione creato all'avvio.  Per tutti gli altri form, l'oggetto `My.Forms` crea una nuova istanza subito dopo l'accesso e l'archiviazione del form.  Ai successivi tentativi di accesso alla proprietà, verrà restituita tale istanza del form.  
  
 Per rimuovere un form, assegnare il valore `Nothing` alla relativa proprietà.  Il metodo di impostazione delle proprietà chiama il metodo <xref:System.Windows.Forms.Form.Close%2A> del form e assegna `Nothing` al valore archiviato.  Se alla proprietà si assegna un valore diverso da `Nothing`, il metodo per l'impostazione genera un'eccezione <xref:System.ArgumentException>.  
  
 Per verificare se una proprietà dell'oggetto `My.Forms` archivia un'istanza del form, utilizzare l'operatore `Is` o `IsNot`.  Questi operatori consentono di controllare se il valore della proprietà è `Nothing`.  
  
> [!NOTE]
>  Generalmente, l'operatore `Is` o `IsNot` deve leggere il valore della proprietà per eseguire il confronto.  Tuttavia, se il valore della proprietà è `Nothing`, la proprietà crea una nuova istanza del form e quindi la restituisce.  Il compilatore di Visual Basic considera le proprietà dell'oggetto `My.Forms` in modo speciale e consente all'operatore `Is` o `IsNot` di controllare lo stato della proprietà senza modificarne il valore.  
  
## Esempio  
 Nell'esempio viene modificato il titolo del form `SidebarMenu` predefinito.  
  
 [!code-vb[VbVbalrMyForms#2](../../../visual-basic/language-reference/objects/codesnippet/visualbasic/my-forms-object_1.vb)]  
  
 Per la corretta esecuzione dell'esempio, è necessario che il progetto contenga un modulo denominato `SidebarMenu`.  Per ulteriori informazioni, vedere [How to: Add Windows Forms to a Project](http://msdn.microsoft.com/it-it/3d7bb25f-fd90-47cf-9378-fa0d764686c1).  
  
 Questo codice può essere utilizzato solo in un progetto di un'applicazione Windows.  
  
## Requisiti  
  
### Disponibilità per tipo di progetto  
  
|||  
|-|-|  
|Tipo di progetto|Disponibile|  
|Applicazione Windows|**Sì**|  
|Libreria di classi|No|  
|Applicazione console|No|  
|Libreria di controlli Windows|No|  
|Libreria di controlli Web|No|  
|Servizio Windows|No|  
|Sito Web|No|  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OpenForms%2A>   
 <xref:System.Windows.Forms.Form>   
 <xref:System.Windows.Forms.Form.Close%2A>   
 [Objects](../../../visual-basic/language-reference/objects/index.md)   
 [How to: Add Windows Forms to a Project](http://msdn.microsoft.com/it-it/3d7bb25f-fd90-47cf-9378-fa0d764686c1)   
 [Is Operator](../../../visual-basic/language-reference/operators/is-operator.md)   
 [IsNot Operator](../../../visual-basic/language-reference/operators/isnot-operator.md)   
 [Accessing Application Forms](../../../visual-basic/developing-apps/programming/accessing-application-forms.md)