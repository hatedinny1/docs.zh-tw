---
title: "使用 XslCompiledTransform 類別 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
ms.assetid: f9b074f6-d6f4-49dd-a093-df510bf0cf7b
caps.latest.revision: 3
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 3
---
# 使用 XslCompiledTransform 類別
<xref:System.Xml.Xsl.XslCompiledTransform> 類別為 Microsoft .NET Framework XSLT 處理器。  此類別用於編譯樣式表，並執行 XSLT 轉換。  
  
> [!NOTE]
>  雖然 <xref:System.Xml.Xsl.XslCompiledTransform> 類別的整體效能優於 <xref:System.Xml.Xsl.XslTransform> 類別，但是在轉換時第一次呼叫 <xref:System.Xml.Xsl.XslCompiledTransform> 類別的 <xref:System.Xml.Xsl.XslCompiledTransform.Load%2A> 方法之執行速度可能會比 <xref:System.Xml.Xsl.XslTransform> 類別的 <xref:System.Xml.Xsl.XslTransform.Load%2A> 方法慢許多。  這是因為在載入之前必須先編譯 XSLT 檔案。  如需詳細資訊，請參閱下列：[XslCompiledTransform 比 XslTransform 還慢嗎？](http://go.microsoft.com/fwlink/?LinkId=130590)  
  
## 在本節中  
 [XslCompiledTransform 類別的輸入](../../../../docs/standard/data/xml/inputs-to-the-xslcompiledtransform-class.md)  
 說明可用的 XSLT 輸入選項。  
  
 [XslCompiledTransform 類別的輸出選項](../../../../docs/standard/data/xml/output-options-on-the-xslcompiledtransform-class.md)  
 說明可用的 XSLT 輸出選項。  
  
 [XSLT 處理期間解析外部資源](../../../../docs/standard/data/xml/resolving-external-resources-during-xslt-processing.md)  
 討論如何使用 <xref:System.Xml.XmlResolver> 類別解析外部資源。  
  
 [延伸 XSLT 樣式表](../../../../docs/standard/data/xml/extending-xslt-style-sheets.md)  
 討論如何支援 XSLT 擴充。  
  
|||  
|-|-|  
|[可復原的 XSLT 錯誤](../../../../docs/standard/data/xml/recoverable-xslt-errors.md)|列出全球資訊網協會 \(W3C\) XSLT 1.0 版建議事項所允許的判別行為，以及說明 <xref:System.Xml.Xsl.XslCompiledTransform> 類別如何處理這些行為。|  
|[HOW TO：轉換節點片段](../../../../docs/standard/data/xml/how-to-transform-a-node-fragment.md)|描述如何轉換節點片段。|  
  
## 相關章節  
 [從 XslTransform 類別移轉](../../../../docs/standard/data/xml/migrating-from-the-xsltransform-class.md)  
 討論如何從 <xref:System.Xml.Xsl.XslTransform> 類別移轉程式碼  
  
## 請參閱  
 <xref:System.Xml.Xsl.XsltSettings>   
 <xref:System.Xml.Xsl.XsltMessageEncounteredEventArgs>