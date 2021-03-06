---
title: 'Exemplarische Vorgehensweise: Erstellen eines Webparts für SharePoint | Microsoft-Dokumentation'
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Web Parts [SharePoint development in Visual Studio], developing
- Web Parts [SharePoint development in Visual Studio], creating
- Web Parts [SharePoint development in Visual Studio], designing
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 3cbc4b9a2eecd6eb9853c515eb5358009c32843a
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/19/2019
ms.locfileid: "72655911"
---
# <a name="walkthrough-create-a-web-part-for-sharepoint"></a>Exemplarische Vorgehensweise: Erstellen eines Webparts für SharePoint

Mithilfe von Webparts können Benutzer Inhalt, Darstellung und Verhalten der Seiten einer SharePoint-Website direkt im Browser ändern. In dieser exemplarischen Vorgehensweise wird veranschaulicht, wie ein Webpart mithilfe der Element Vorlage **Webpart** in Visual Studio 2010 erstellt wird.

Das Webpart zeigt Mitarbeiter in einem Datenraster an. Der Benutzer gibt den Speicherort der Datei an, die die Mitarbeiterdaten enthält. Außerdem kann der Benutzer das Datenraster filtern, damit nur Mitarbeiter, die Manager sind, in der Liste angezeigt werden.

In dieser exemplarischen Vorgehensweise werden die folgenden Aufgaben veranschaulicht:

- Erstellen eines Webparts mithilfe der Element Vorlage von Visual Studio- **Webpart** .

- Erstellen einer Eigenschaft, die vom Benutzer des Webparts festgelegt werden kann. Diese Eigenschaft gibt den Speicherort der Mitarbeiterdatendatei an.

- Rendern von Inhalt in einem Webpart durch Hinzufügen von Steuerelementen zur Webpart-Steuerelementauflistung.

- Erstellen eines neuen Menü Elements (als *Verb* bezeichnet), das im Verbenmenü des gerenderten Webparts angezeigt wird. Verben ermöglichen es dem Benutzer, die im Webpart angezeigten Daten zu ändern.

- Testen des Webparts in SharePoint.

    > [!NOTE]
    > Auf Ihrem Computer werden möglicherweise andere Namen oder Speicherorte für die Benutzeroberflächenelemente von Visual Studio angezeigt als die in den folgenden Anweisungen aufgeführten. Diese Elemente sind von der jeweiligen Visual Studio-Version und den verwendeten Einstellungen abhängig. Weitere Informationen finden Sie unter [Personalisieren von Visual Studio-IDE](../ide/personalizing-the-visual-studio-ide.md).

## <a name="prerequisites"></a>Erforderliche Voraussetzungen

- Unterstützte Editionen von Microsoft Windows und SharePoint.

- Visual Studio 2017 oder Azure DevOps Services.

## <a name="create-an-empty-sharepoint-project"></a>Erstellen Sie ein leeres SharePoint-Projekt.

Erstellen Sie zunächst ein leeres SharePoint-Projekt. Später fügen Sie dem Projekt ein Webpart hinzu, indem Sie die Element Vorlage für das **Webpart** verwenden.

1. Starten Sie [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)], indem Sie die Option **als Administrator ausführen** verwenden.

2. Wählen Sie auf der Leiste "Männer" die Option **Datei**  > **neue**  > **Projekt**aus.

3. Erweitern Sie im Dialogfeld **Neues Projekt** den Knoten **SharePoint** unter der Sprache, die Sie verwenden möchten, und wählen Sie dann den Knoten **2010** aus.

4. Wählen Sie im Bereich **Vorlagen** die Option **SharePoint 2010-Projekt**aus, und klicken Sie dann auf die Schaltfläche **OK** .

     Der Assistent zum Anpassen von **SharePoint** wird angezeigt. Mit diesem Assistenten können Sie die Website, die Sie zum Debuggen des Projekts verwenden, sowie die Vertrauensebene der Projektmappe auswählen.

5. Wählen Sie das Optionsfeld **als Farm Lösung** bereitstellen, und klicken Sie dann auf die Schaltfläche **Fertig** stellen, um die standardmäßige lokale SharePoint-Website zu akzeptieren.

## <a name="add-a-web-part-to-the-project"></a>Fügen Sie dem Projekt ein Webpart hinzu.

Fügen Sie dem Projekt ein **Webpartelement** hinzu. Das **Webpartelement** fügt die Codedatei für das Webpart hinzu. Später fügen Sie der Codedatei für das Webpart Code hinzu, um den Inhalt des Webparts zu rendern.

1. Wählen Sie in der Menüleiste **Projekt** > **Neues Element hinzufügen** aus.

2. Erweitern Sie im Dialogfeld **Neues Element hinzufügen** im Bereich **installierte Vorlagen** den Knoten **SharePoint** , und wählen Sie dann den Knoten **2010** aus.

3. Wählen Sie in der Liste der SharePoint-Vorlagen die Vorlage **Webpart** aus, und klicken Sie dann auf die Schaltfläche **Hinzufügen** .

     Das Element **Webpart** wird in **Projektmappen-Explorer**angezeigt.

## <a name="rendering-content-in-the-web-part"></a>Rendern von Inhalt im Webpart

Sie können angeben, welche Steuerelemente im Webpart angezeigt werden, indem Sie diese der Steuerelementauflistung der Webpartklasse hinzufügen.

1. ÖffnenSie in Projektmappen-Explorer *WebPart1. vb* (in Visual Basic) oder *WebPart1.cs* (in C#).

     Die Codedatei für das Webpart wird im Code-Editor geöffnet.

2. Fügen Sie am Anfang der Codedatei für das Webpart die folgenden-Direktiven hinzu.

     [!code-csharp[SP_WebPart#1](../sharepoint/codesnippet/CSharp/spext_webpart/webpart1/webpart1.cs#1)]
     [!code-vb[SP_WebPart#1](../sharepoint/codesnippet/VisualBasic/spext_webpart/webpart1/webpart1.vb#1)]

3. Fügen Sie der `WebPart1` -Klasse folgenden Code hinzu. Mit diesem Code werden die folgenden Felder deklariert:

   - Ein Datenraster, um Mitarbeiter im Webpart anzuzeigen.

   - Text, der auf dem Steuerelement angezeigt wird, das zum Filtern des Datenrasters verwendet wird.

   - Eine Bezeichnung, die einen Fehler anzeigt, wenn das Datenraster keine Daten anzeigen kann.

   - Eine Zeichenfolge, die den Pfad zur Mitarbeiterdatendatei enthält.

     [!code-csharp[SP_WebPart#2](../sharepoint/codesnippet/CSharp/spext_webpart/webpart1/webpart1.cs#2)]
     [!code-vb[SP_WebPart#2](../sharepoint/codesnippet/VisualBasic/spext_webpart/webpart1/webpart1.vb#2)]

4. Fügen Sie der `WebPart1` -Klasse folgenden Code hinzu. In diesem Code wird dem Webpart eine benutzerdefinierte Eigenschaft mit dem Namen `DataFilePath` hinzugefügt. Eine benutzerdefinierte Eigenschaft ist eine Eigenschaft, die vom Benutzer in SharePoint festgelegt werden kann. Diese Eigenschaft ruft den Speicherort einer XML-Datendatei ab, die zum Auffüllen des Datenrasters verwendet wird, und legt diesen Speicherort fest.

     [!code-csharp[SP_WebPart#3](../sharepoint/codesnippet/CSharp/spext_webpart/webpart1/webpart1.cs#3)]
     [!code-vb[SP_WebPart#3](../sharepoint/codesnippet/VisualBasic/spext_webpart/webpart1/webpart1.vb#3)]

5. Ersetzen Sie die `CreateChildControls` -Methode durch folgenden Code: Mit diesem Code werden die folgenden Aufgaben ausgeführt:

   - Fügt das Datenraster und die Bezeichnung hinzu, die Sie im vorherigen Schritt deklariert haben.

   - Bindet das Datenraster an eine XML-Datei, die Mitarbeiterdaten enthält.

     [!code-csharp[SP_WebPart#4](../sharepoint/codesnippet/CSharp/spext_webpart/webpart1/webpart1.cs#4)]
     [!code-vb[SP_WebPart#4](../sharepoint/codesnippet/VisualBasic/spext_webpart/webpart1/webpart1.vb#4)]

6. Fügen Sie der `WebPart1` -Klasse die folgende Methode hinzu. Mit diesem Code werden die folgenden Aufgaben ausgeführt:

   - Erstellt ein Verb, das im Verbmenü des gerenderten Webparts angezeigt wird.

   - Behandelt das Ereignis, das ausgelöst wird, wenn der Benutzer im Verbmenü das Verb auswählt. In diesem Code wird die Liste der Mitarbeiter gefiltert, die im Datenraster angezeigt wird.

     [!code-csharp[SP_WebPart#5](../sharepoint/codesnippet/CSharp/spext_webpart/webpart1/webpart1.cs#5)]
     [!code-vb[SP_WebPart#5](../sharepoint/codesnippet/VisualBasic/spext_webpart/webpart1/webpart1.vb#5)]

## <a name="test-the-web-part"></a>Testen des Webparts

Wenn Sie das Projekt ausführen, wird die SharePoint-Website geöffnet. Das Webpart wird automatisch dem Webpartkatalog in SharePoint hinzugefügt. Sie können das Webpart jeder Webpartseite hinzufügen.

1. Fügen Sie folgendes XML in eine Editor-Datei ein. Diese XML-Datei enthält die Beispieldaten, die im Webpart angezeigt werden.

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
        <employees xmlns="http://schemas.microsoft.com/vsto/samples">
           <employee>
               <name>David Hamilton</name>
               <hireDate>2001-05-11</hireDate>
               <title>Sales Associate</title>
           </employee>
           <employee>
               <name>Karina Leal</name>
               <hireDate>1999-04-01</hireDate>
               <title>Manager</title>
           </employee>
           <employee>
               <name>Nancy Davolio</name>
               <hireDate>1992-05-01</hireDate>
               <title>Sales Associate</title>
           </employee>
           <employee>
               <name>Steven Buchanan</name>
               <hireDate>1955-03-04</hireDate>
               <title>Manager</title>
           </employee>
           <employee>
               <name>Suyama Michael</name>
               <hireDate>1963-07-02</hireDate>
               <title>Sales Associate</title>
           </employee>
        </employees>
    ```

2. Wählen Sie im Editor in der Menüleiste **Datei**  > **Speichern**unter aus.

3. Wählen Sie im Dialogfeld **Speichern** unter in der Liste **Dateityp** die Option **alle Dateien**aus.

4. Geben Sie im Feld **Dateiname** den Text **Data. XML**ein.

5. Wählen Sie mithilfe der Schaltfläche **Ordner durchsuchen** einen beliebigen Ordner aus, und klicken Sie dann auf die Schaltfläche **Speichern** .

6. Wählen Sie in Visual Studio die Taste **F5** aus.

     Die SharePoint-Website wird geöffnet.

7. Wählen Sie im Menü **Website Aktionen** die **Option Weitere Optionen**aus.

8. Wählen Sie auf der Seite **Erstellen** den Typ der **Webpartseite** aus, und klicken Sie dann auf die Schaltfläche **Erstellen** .

9. Benennen Sie auf der Seite **neue Webpartseite** die Seite **SampleWebPartPage. aspx**, und wählen Sie dann die Schaltfläche **Erstellen** aus.

     Die Webpartseite wird angezeigt.

10. Wählen Sie eine Zone auf der Webpartseite aus.

11. Wählen Sie am oberen Rand der Seite die Registerkarte **Einfügen** aus, und klicken Sie dann auf die Schaltfläche **Webpart** .

12. Wählen Sie im Bereich **Kategorien** den Ordner **Benutzer** definiert aus, wählen Sie das **WebPart1** -Webpart aus, und klicken Sie dann auf die Schaltfläche **Hinzufügen** .

     Das Webpart wird auf der Seite angezeigt.

## <a name="test-the-custom-property"></a>Testen der benutzerdefinierten Eigenschaft

Um das im Webpart angezeigte Datenraster aufzufüllen, geben Sie den Pfad der XML-Datei an, die Daten zu jedem Mitarbeiter enthält.

1. Wählen Sie den Pfeil aus, der auf der rechten Seite des Webparts angezeigt wird, und wählen Sie dann im angezeigten Menü **Webpart bearbeiten** aus.

     Ein Bereich, der Eigenschaften für das Webpart enthält, wird auf der rechten Seite der Seite angezeigt.

2. Erweitern Sie im Bereich den Knoten **Verschiedenes** , geben Sie den Pfad der XML-Datei ein, die Sie zuvor erstellt haben, wählen Sie **die Schaltfläche** übernehmen aus, und klicken Sie dann auf die Schaltfläche **OK** .

     Überprüfen Sie, ob eine Liste von Mitarbeitern im Webpart angezeigt wird.

## <a name="test-the-web-part-verb"></a>Testen des webpartverbs

Zeigen Sie Mitarbeiter an, die keine Manager sind, und blenden Sie diese aus, indem Sie auf ein Element klicken, das im Verbmenü des Webparts angezeigt wird.

1. Wählen Sie den Pfeil aus, der auf der rechten Seite des Webparts angezeigt wird, und wählen Sie dann im angezeigten Menü **nur Manager anzeigen** aus.

     Nur Mitarbeiter, die Manager sind, werden im Webpart angezeigt.

2. Wählen Sie den Pfeil erneut aus, und wählen Sie dann im angezeigten Menü **alle Mitarbeiter anzeigen** aus.

     Alle Mitarbeiter werden im Webpart angezeigt.

## <a name="see-also"></a>Siehe auch

[Erstellen von Webparts für SharePoint](../sharepoint/creating-web-parts-for-sharepoint.md) 
 Gewusst[wie: Erstellen eines SharePoint-Webparts](../sharepoint/how-to-create-a-sharepoint-web-part.md) 
 Gewusst[wie: Erstellen eines SharePoint-Webparts mithilfe eines Designers](../sharepoint/how-to-create-a-sharepoint-web-part-by-using-a-designer.md) 
 Exemplarische Vorgehensweise[: Erstellen eines Webparts für SharePoint mithilfe eines Designers](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint-by-using-a-designer.md)
