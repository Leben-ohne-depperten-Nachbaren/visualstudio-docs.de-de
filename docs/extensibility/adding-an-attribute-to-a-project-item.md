---
title: Hinzufügen eines Attributs zu einem Projektelement | Microsoft-Dokumentation
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- attributes [Visual Studio], adding to a project item
ms.assetid: 404a71d5-cce5-44e7-9eaf-d747c794fedb
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8524ebc866d92cfe39a19dc79165da7c38025628
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/29/2019
ms.locfileid: "66352379"
---
# <a name="add-an-attribute-to-a-project-item"></a>Hinzufügen eines Attributs zu einem Projektelement
Die Methoden <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.GetItemAttribute%2A> und <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.SetItemAttribute%2A> abrufen und Festlegen des Werts der Attribute eines Projektelements. SetItemAttribute erstellt das Attribut, wenn es nicht bereits vorhanden ist, die Elementmetadaten Projekt hinzugefügt.

## <a name="add-an-attribute-to-a-project-item"></a>Hinzufügen eines Attributs zu einem Projektelement

- Der folgende code verwendet die <xref:EnvDTE.DTE> Automatisierungsobjekt und <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.SetItemAttribute%2A> Methode, um ein Attribut auf ein Projektelement hinzuzufügen. Die Projekt-ID wird aus dem Projekt Element namens "program.cs" abgerufen. Das Attribut "MyAttribute" ist zu diesem Projektelement hinzugefügt und den Wert "MyValue".

    ```csharp
    EnvDTE.DTE dte = (EnvDTE.DTE)Package.GetGlobalService(typeof(EnvDTE.DTE));
    EnvDTE.Project project = dte.Solution.Projects.Item(1);

    string uniqueName = project.UniqueName;
    IVsSolution solution = (IVsSolution)Package.GetGlobalService(typeof(SVsSolution));
    IVsHierarchy hierarchy;
    solution.GetProjectOfUniqueName(uniqueName, out hierarchy);
    IVsBuildPropertyStorage buildPropertyStorage = hierarchy as IVsBuildPropertyStorage;
    if (buildPropertyStorage != null)
    {
        uint itemId;
        string fullPath = (string)project.ProjectItems.Item("Program.cs").Properties.Item("FullPath").Value;
        hierarchy.ParseCanonicalName(fullPath, out itemId);
        buildPropertyStorage.SetItemAttribute(itemId, "MyAttribute", "MyValue");
    }

    ```

## <a name="see-also"></a>Siehe auch
- [Beibehalten von Daten in der MSBuild-Projektdatei](../extensibility/internals/persisting-data-in-the-msbuild-project-file.md)
