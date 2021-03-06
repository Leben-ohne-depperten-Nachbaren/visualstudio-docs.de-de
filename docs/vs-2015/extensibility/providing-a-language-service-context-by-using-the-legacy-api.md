---
title: Einen Dienstkontext für die Sprache bereitstellt, mit der Legacy-API | Microsoft-Dokumentation
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - language service context
ms.assetid: daa2df22-9181-4bad-b007-a7d40302bce1
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 4471b71b612008ba7d0733c92286415cd3c3f6b3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2019
ms.locfileid: "68193867"
---
# <a name="providing-a-language-service-context-by-using-the-legacy-api"></a>Bereitstellen eines Sprachdienstkontexts mithilfe der Legacy-API
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Es gibt zwei Optionen für einen Sprachdienst zu Benutzer-Kontext verwenden die [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] -Kern-Editor: Text Markers Kontext bereitzustellen, oder geben Sie alle Benutzerkontext. Hier werden die Unterschiede zwischen den einzelnen beschrieben.  
  
 Weitere Informationen zum Bereitstellen von Kontext für einen Sprachdienst an, die mit Ihren eigenen Editor verbunden ist, finden Sie unter [Vorgehensweise: Bereitstellen von Kontext für Editoren](../extensibility/how-to-provide-context-for-editors.md).  
  
## <a name="provide-text-marker-context-to-the-editor"></a>Geben Sie Text Markers Kontext in den Editor  
 Compilerfehler durch Textmarker im angegebenen Kontext bereit die [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Kern-Editor, implementieren Sie die <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerContextProvider> Schnittstelle. In diesem Szenario stellt der Sprachdienst nur, wenn der Cursor für eine textmarkierung ist Kontext bereit. Dadurch wird der Editor das Schlüsselwort an der Cursorposition zum Bereitstellen der **dynamische Hilfe** Fenster keine Attribute.  
  
## <a name="provide-all-user-context-to-the-editor"></a>Geben Sie alle Benutzerkontext auf dem Editor  
 Wenn Sie einen Sprachdienst erstellen und Verwenden der [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Kern-Editor, und Sie implementieren können, die <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageContextProvider> Schnittstelle, um Kontext für den Sprachdienst bereitzustellen.  
  
 Für die Implementierung von `IVsLanguageContextProvider`, eine Kontextsammlung (Auflistung) angefügt ist, um den Editor für die Aktualisierung der kontextauflistung verantwortlich ist. Wenn die **dynamische Hilfe** Fenster Aufrufe der <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.Update%2A> Schnittstelle auf diesem kontextbehälter während der Leerlaufzeit den kontextbehälter fragt den Editor für ein Update. Der Editor benachrichtigt dann dem Sprachdienst, sollte den Editor zu aktualisieren und übergibt einen Zeiger auf den kontextbehälter. Dies erfolgt durch Aufrufen der <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageContextProvider.UpdateLanguageContext%2A> Methode aus dem Editor auf den Sprachdienst. Verwenden den Zeiger auf die Kontextsammlung, kann der Sprachdienst jetzt hinzufügen und entfernen Attribute und Schlüsselwörter. Weitere Informationen finden Sie unter <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageContextProvider>.  
  
 Es gibt zwei Möglichkeiten zum Implementieren `IVsLanguageContextProvider`:  
  
- Geben Sie ein Schlüsselwort, durch den kontextbehälter  
  
   Wenn der Editor aufgerufen wird, um den kontextbehälter zu aktualisieren, übergeben Sie die geeignete Schlüsselwörter und Attribute und wieder `S_OK`. Dieser Rückgabewert weist der Editor beibehalten Ihres Kontexts-Schlüsselwort und Attribut, anstatt das Schlüsselwort an der Cursorposition auf die Kontextsammlung.  
  
- Das Schlüsselwort aus das Schlüsselwort an der Cursorposition zu erhalten.  
  
   Wenn der Editor aufgerufen wird, um den kontextbehälter zu aktualisieren, übergeben Sie die entsprechenden Attribute und wieder `E_FAIL`. Dieser Rückgabewert wird angewiesen, Ihre Attribute in den kontextbehälter beibehalten, aber den kontextbehälter zu aktualisieren, mit dem Schlüsselwort an der Cursorposition im Editor.  
  
  Das folgende Diagramm veranschaulicht, wie der Kontext für einen Sprachdienst bereitgestellt wird, die implementiert `IVsLanguageContextProvider`.  
  
  ![LangServiceImplementation2-Grafik](../extensibility/media/vslanguageservice2.gif "vsLanguageService2")  
  Kontext für einen Sprachdienst  
  
  Wie Sie im Diagramm sehen die [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] kerntext-Editor verfügt über eine Kontextsammlung angefügt ist. Diese kontextbehälter verweist auf drei separaten unterkontextbehälter: Sprachdienst, Standard-Editor und textmarkierung. Der Language-Dienst und Text Marker unterkontextbehälter enthalten Attribute und Schlüsselwörter für den Sprachdienst, wenn die <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageContextProvider> Schnittstelle implementiert wird, und Textmarkierungen Wenn die <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerContextProvider> Schnittstelle wird implementiert. Wenn Sie nicht eine der folgenden Schnittstellen implementieren, stellt der Editor Kontext für das Schlüsselwort an der Cursorposition in den unterkontextbehälter für Standard-Editor bereit.  
  
## <a name="context-guidelines-for-editors-and-designers"></a>Kontext-Richtlinien für die Editoren und Designern  
 Designer und Editoren müssen ein allgemeines Schlüsselwort für den Editor oder Designer-Fenster bereitstellen. Dies erfolgt, damit ein Hilfethema generischen, jedoch erforderlich, für den Designer oder Editor angezeigt werden, wenn ein Benutzer F1 drückt. Ein Editor muss darüber hinaus geben Sie das aktuelle Schlüsselwort an der Cursorposition oder stellen Sie eine wesentliche Begriffe, die basierend auf der aktuellen Auswahl. Dies erfolgt, um sicherzustellen, dass ein Hilfethema für den Text oder ein Element der Benutzeroberfläche auf den verwiesen wird, oder zeigt ausgewählt, wenn der Benutzer F1 drückt. Ein Designer stellt Kontext für ein Element in einem Designer, z. B. eine Schaltfläche in einem Formular ausgewählt. Editoren und Designern müssen auch eine Verbindung herstellen, die ein Sprachdienst wie unter [Legacy-Sprache von Dienstzusammenfassungen](../extensibility/internals/legacy-language-service-essentials.md).
