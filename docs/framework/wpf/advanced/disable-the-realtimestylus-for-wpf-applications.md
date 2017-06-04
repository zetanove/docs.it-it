---
title: "Disabilitare RealTimeStylus per le applicazioni WPF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e0525309-5ede-4782-837d-dbf6e5554859
caps.latest.revision: 3
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 3
---
# Disabilitare RealTimeStylus per le applicazioni WPF
Windows Presentation Foundation \(WPF\) dispone del supporto incorporato per l'elaborazione dell'input tocco di Windows 7. Il supporto viene fornito tramite l'input con stilo in tempo reale della piattaforma Tablet PC come eventi <xref:System.Windows.UIElement.OnStylusDown%2A>, <xref:System.Windows.UIElement.OnStylusUp%2A> e <xref:System.Windows.UIElement.OnStylusMove%2A>.  Windows 7 fornisce inoltre l'input multitocco come messaggi finestra Win32 WM\_TOUCH.  Queste due API si escludono a vicenda sullo stesso HWND.  L'abilitazione dell'input tocco tramite la piattaforma Tablet PC \(l'impostazione predefinita per le applicazioni WPF\) disabilita i messaggi WM\_TOUCH.  Di conseguenza, per utilizzare WM\_TOUCH per la ricezione dei messaggi di tocco da una finestra WPF, è necessario disabilitare il supporto dello stilo incorporato in WPF.  Queste considerazioni sono applicabili a uno scenario quale una finestra WPF in cui è ospitato un componente che utilizza WM\_TOUCH.  
  
 Per disabilitare l'ascolto di WPF dell'input con stilo, rimuovere qualsiasi supporto per Tablet PC aggiunto dalla finestra WPF.  
  
## Esempio  
 Nel codice di esempio seguente viene illustrato come rimuovere il supporto della piattaforma Tablet PC tramite reflection.  
  
```  
public static void DisableWPFTabletSupport()  
{  
    // Get a collection of the tablet devices for this window.    
    TabletDeviceCollection devices = System.Windows.Input.Tablet.TabletDevices;  
  
    if (devices.Count > 0)  
    {     
        // Get the Type of InputManager.  
        Type inputManagerType = typeof(System.Windows.Input.InputManager);  
  
        // Call the StylusLogic method on the InputManager.Current instance.  
        object stylusLogic = inputManagerType.InvokeMember("StylusLogic",  
                    BindingFlags.GetProperty | BindingFlags.Instance | BindingFlags.NonPublic,  
                    null, InputManager.Current, null);  
  
        if (stylusLogic != null)  
        {  
            //  Get the type of the stylusLogic returned from the call to StylusLogic.  
            Type stylusLogicType = stylusLogic.GetType();  
  
            // Loop until there are no more devices to remove.  
            while (devices.Count > 0)  
            {  
                // Remove the first tablet device in the devices collection.  
                stylusLogicType.InvokeMember("OnTabletRemoved",  
                        BindingFlags.InvokeMethod | BindingFlags.Instance | BindingFlags.NonPublic,  
                        null, stylusLogic, new object[] { (uint)0 });  
            }                  
        }  
  
    }  
}  
```  
  
## Vedere anche  
 [Intercettazione dell'input dello stilo](../../../../docs/framework/wpf/advanced/intercepting-input-from-the-stylus.md)