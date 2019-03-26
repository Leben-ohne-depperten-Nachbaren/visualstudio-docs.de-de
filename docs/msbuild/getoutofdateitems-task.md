---
title: GetOutOfDateItems-Aufgabe | Microsoft-Dokumentation
ms.date: 03/10/2019
ms.topic: reference
f1_keywords:
- vc.task.getoutofdateitems
dev_langs:
- VB
- CSharp
- C++
- jsharp
- C++
helpviewer_keywords:
- MSBuild (Visual C++), GetOutOfDateItems task
- GetOutOfDateItems task (MSBuild (Visual C++))
author: mikeblome
ms.author: Michael.Blome
ms.workload:
- multiple
ms.openlocfilehash: 668dddcd0854869c9ede7bf96c092d415f41dd17
ms.sourcegitcommit: 4ffb7be5384ad566ce46538032bf8561754c61a4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/15/2019
ms.locfileid: "58070408"
---
# <a name="getoutofdateitems-task"></a>GetOutOfDateItems-Aufgabe

Hilfsaufgabe zum Lesen alter Nachverfolgungsprotokolle, Schreiben neuer Nachverfolgungsprotokolle und Zurückgeben von Elementen, die nicht auf dem neuesten Stand sind.

## <a name="parameters"></a>Parameter

In der folgenden Tabelle werden die Parameter der **GetOutOfDateItems-Aufgabe** beschrieben.

|Parameter|Beschreibung|
|---------------|-----------------|
|**CheckForInterdependencies**|Optionaler **bool**-Parameter|
|**CommandMetadataName**|Optionaler **string**-Parameter|
|**DependenciesMetadataName**|Optionaler **string**-Parameter|
|**HasInterdependencies**|Optionaler **bool**-Ausgabeparameter|
|**OutOfDateSources**|Optionaler **ITaskItem[]**-Ausgabeparameter.|
|**OutputsMetadataName**|Erforderlicher **String**-Parameter.|
|**Sources**|Optionaler **ITaskItem[]**-Parameter.|
|**TLogDirectory**|Erforderlicher **String**-Parameter.|
|**TLogNamePrefix**|Erforderlicher **String**-Parameter.|

## <a name="see-also"></a>Siehe auch

[Referenz zu MSBuild-Tasks](../msbuild/msbuild-task-reference.md)