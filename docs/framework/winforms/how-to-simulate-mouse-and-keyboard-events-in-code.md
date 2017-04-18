---
title: "如何：以程式碼模擬滑鼠和鍵盤事件 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "鍵盤, 事件模擬"
  - "使用者輸入, 模擬"
  - "SendKeys, 使用"
  - "按一下滑鼠, 模擬"
  - "滑鼠, 事件模擬"
ms.assetid: 6abcb67e-3766-4af2-9590-bf5dabd17e41
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 如何：以程式碼模擬滑鼠和鍵盤事件
Windows Form 提供以程式設計方式模擬滑鼠和鍵盤輸入的數個選項。 本主題提供這些選項的概觀。  
  
## 模擬滑鼠輸入  
 模擬滑鼠事件的最佳方式是呼叫 `On`*EventName* 方法，這個方法會引發您要模擬的滑鼠事件。 通常只有在自訂控制項和表單內才能使用這個選項，因為引發事件的方法會受到保護，而且無法在控制項或表單外進行存取。 例如，下列步驟說明如何以程式碼模擬按一下滑鼠右鍵的動作。  
  
#### 以程式設計方式按一下滑鼠右鍵  
  
1.  建立 <xref:System.Windows.Forms.MouseEventArgs>，並將其 <xref:System.Windows.Forms.MouseEventArgs.Button%2A> 屬性設定為 <xref:System.Windows.Forms.MouseButtons?displayProperty=fullName> 值。  
  
2.  呼叫 <xref:System.Windows.Forms.Control.OnMouseClick%2A> 方法，並以這個 <xref:System.Windows.Forms.MouseEventArgs> 做為引數。  
  
 如需自訂控制項的詳細資訊，請參閱 [在設計階段開發 Windows Form 控制項](../../../docs/framework/winforms/controls/developing-windows-forms-controls-at-design-time.md)。  
  
 還有其他方式可以模擬滑鼠輸入。 例如，您可以透過程式設計方式設定代表狀態的控制項屬性，這個狀態通常是透過滑鼠輸入來設定 \(例如 <xref:System.Windows.Forms.CheckBox> 控制項的 <xref:System.Windows.Forms.CheckBox.Checked%2A> 屬性\)，您也可以直接呼叫附加至所要模擬之事件的委派。  
  
## 模擬鍵盤輸入  
 除了可以使用上述用於滑鼠輸入的策略來模擬鍵盤輸入之外，Windows Form 還提供 <xref:System.Windows.Forms.SendKeys> 類別，以便將按鍵動作傳送至作用中應用程式。  
  
> [!CAUTION]
>  如果您的應用程式是設計成可搭配國際上現有的各種鍵盤來使用，則使用 <xref:System.Windows.Forms.SendKeys.Send%2A?displayProperty=fullName> 可能會產生無法預期的結果，應該予以避免。  
  
> [!NOTE]
>  <xref:System.Windows.Forms.SendKeys> 類別已針對 .NET Framework 3.0 進行更新，以便能夠在 Windows Vista 上執行的應用程式中使用。 Windows Vista 的增強式安全性 \(稱為使用者帳戶控制或 UAC\) 會讓之前的實作無法如預期般運作。  
>   
>  <xref:System.Windows.Forms.SendKeys> 類別容易受到時間問題的影響，某些開發人員必須解決這些問題。 更新的實作仍然容易受到時間問題的影響，但是速度會稍微快一些，而且可能需要對解決方法進行變更。<xref:System.Windows.Forms.SendKeys> 類別會先嘗試使用之前的實作；如果失敗，則使用新的實作。 因此，<xref:System.Windows.Forms.SendKeys> 類別在不同的作業系統上可能會有不同的運作方式。 此外，當 <xref:System.Windows.Forms.SendKeys> 類別使用新的實作時，<xref:System.Windows.Forms.SendKeys.SendWait%2A> 方法不會在將訊息傳送至另一個處理序時，等候處理這些訊息。  
>   
>  如果不論作業系統為何，應用程式都需要一致的行為，您可以強制 <xref:System.Windows.Forms.SendKeys> 類別使用新的實作，方式是將下列應用程式設定加入 app.config 檔中。  
>   
>  `<appSettings>`  
>   
>  `<add key="SendKeys" value="SendInput"/>`  
>   
>  `</appSettings>`  
>   
>  若要強制 <xref:System.Windows.Forms.SendKeys> 類別使用之前的實作，請改用 `"JournalHook"` 值。  
  
#### 將按鍵動作傳送至相同的應用程式  
  
1.  請呼叫 <xref:System.Windows.Forms.SendKeys> 類別的 <xref:System.Windows.Forms.SendKeys.Send%2A> 或 <xref:System.Windows.Forms.SendKeys.SendWait%2A> 方法。 應用程式的作用控制項會接收指定的按鍵動作。 下列程式碼範例使用 <xref:System.Windows.Forms.SendKeys.Send%2A> 來模擬當使用者按兩下表單介面時，按下 ENTER 鍵的動作。 這個範例假設 <xref:System.Windows.Forms.Form> 含有一個定位點索引為 0 的 <xref:System.Windows.Forms.Button> 控制項。  
  
     [!code-cpp[System.Windows.Forms.SimulateKeyPress#10](../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.SimulateKeyPress/cpp/form1.cpp#10)]
     [!code-csharp[System.Windows.Forms.SimulateKeyPress#10](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.SimulateKeyPress/CS/form1.cs#10)]
     [!code-vb[System.Windows.Forms.SimulateKeyPress#10](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.SimulateKeyPress/VB/form1.vb#10)]  
  
#### 將按鍵動作傳送至不同的應用程式  
  
1.  啟動會接收按鍵動作的應用程式視窗，然後呼叫 <xref:System.Windows.Forms.SendKeys.Send%2A> 或 <xref:System.Windows.Forms.SendKeys.SendWait%2A> 方法。 由於沒有可啟動另一個應用程式的 Managed 方法，因此您必須使用原生 Windows 方法強制將焦點放在其他應用程式上。 下列程式碼範例使用平台叫用呼叫 `FindWindow` 和 `SetForegroundWindow` 方法，以啟動 \[小算盤\] 應用程式視窗，然後再呼叫 <xref:System.Windows.Forms.SendKeys.SendWait%2A> 對 \[小算盤\] 應用程式發出一連串計算。  
  
    > [!NOTE]
    >  用於尋找 \[小算盤\] 應用程式之 `FindWindow` 呼叫的正確參數會隨您的 Windows 版本而異。  下列程式碼會尋找 [!INCLUDE[win7](../../../includes/win7-md.md)] 上的 \[小算盤\] 應用程式。 在 [!INCLUDE[windowsver](../../../includes/windowsver-md.md)] 上，將第一個參數變更為 "SciCalc"。 您可以使用 Visual Studio 隨附的 Spy\+\+ 工具來判斷正確的參數。  
  
     [!code-cpp[System.Windows.Forms.SimulateKeyPress#5](../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.SimulateKeyPress/cpp/form1.cpp#5)]
     [!code-csharp[System.Windows.Forms.SimulateKeyPress#5](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.SimulateKeyPress/CS/form1.cs#5)]
     [!code-vb[System.Windows.Forms.SimulateKeyPress#5](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.SimulateKeyPress/VB/form1.vb#5)]  
  
## 範例  
 下列程式碼範例是先前程式碼範例的完整應用。  
  
 [!code-cpp[System.Windows.Forms.SimulateKeyPress#0](../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.SimulateKeyPress/cpp/form1.cpp#0)]
 [!code-csharp[System.Windows.Forms.SimulateKeyPress#0](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.SimulateKeyPress/CS/form1.cs#0)]
 [!code-vb[System.Windows.Forms.SimulateKeyPress#0](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.SimulateKeyPress/VB/form1.vb#0)]  
  
## 編譯程式碼  
 這個範例需要：  
  
-   System、System.Drawing 和 System.Windows.Forms 組件的參考。  
  
 如需從 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] 或 [!INCLUDE[csprcs](../../../includes/csprcs-md.md)] 命令列建置這個範例的相關資訊，請參閱[從命令列建置](../Topic/Building%20from%20the%20Command%20Line%20\(Visual%20Basic\).md)或[使用 csc.exe 建置命令列](../../../ocs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md)。 您也可以將程式碼貼在新的專案中，以在 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 中建置這個範例。  另請參閱[如何：使用 Visual Studio 編譯及執行完整的 Windows Form 程式碼範例](http://msdn.microsoft.com/library/Bb129228\(v=vs.110\))。  
  
## 請參閱  
 [Windows Form 中的使用者輸入](../../../docs/framework/winforms/user-input-in-windows-forms.md)