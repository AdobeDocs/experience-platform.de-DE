---
title: Entfernen von Ressourcen aus einer Bibliothek
description: Erfahren Sie, wie Sie Ressourcen aus einer Tag-Bibliothek entfernen.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 92%

---

# Entfernen von Ressourcen aus einer Bibliothek

>[!NOTE]
>
>Adobe Experience Platform Launch wird als eine Suite von Datenerfassungstechnologien in Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Wenn eine Ressource keine Auswirkungen mehr innerhalb eines Builds haben soll, müssen Sie sie aus der Bibliothek entfernen, die diese Ressource enthält, und einen neuen Build erstellen.

>[!IMPORTANT]
>
>Ressourcen in Bibliotheken sind voneinander abhängig. Wenn Sie eine Ressource aus einem Build entfernen, kann sich das Verhalten anderer Ressourcen im Build ändern.

Der Löschvorgang funktioniert unterschiedlich, je nachdem, welchen Status die Bibliothek aufweist.

## Entwicklungsbibliotheken

Ressourcen in Entwicklungsbibliotheken können direkt bearbeitet werden.

1. Öffnen Sie die Bibliothek.
1. Entfernen Sie die Ressource.
1. Speichern Sie die Bibliothek.
1. Erstellen Sie die Bibliothek.

## Gesendete und genehmigte Bibliotheken

Ressourcen in gesendeten oder genehmigten Bibliotheken können nicht direkt bearbeitet werden. Sie müssen die Bibliothek zurück in den Entwicklungsstatus versetzen.

1. Lehnen Sie die Bibliothek ab (verschiebt sie zurück in die Entwicklung).
1. Führen Sie die unter „Entwicklungsbibliotheken“ aufgeführten Schritte aus, um Ressourcen aus Entwicklungsbibliotheken zu entfernen.

## Produktionsbibliotheken

Das Entfernen von Ressourcen aus einer Produktionsbibliothek ist der komplexeste Fall. Sie können die Bibliotheksressourcen in diesem Status nicht bearbeiten, und Sie können diese Bibliotheken nicht wieder in den Entwicklungsstatus zurückversetzen.

Stattdessen müssen Sie die Ressource deaktivieren. Die Deaktivierung ist eine Änderung, die Sie daraufhin wie jede andere Änderung einer Entwicklungsbibliothek hinzufügen können. Sobald diese Änderung in der Produktion vorgenommen wurde, wird die Ressource aus Ihrer Produktionsbibliothek verschoben.

1. Deaktivieren Sie die Ressource.
   1. Wählen Sie die Ressource aus der Listenansicht aus.
   1. Wählen Sie **[!UICONTROL Deaktivieren]**.
1. Erstellen Sie eine neue Entwicklungsbibliothek.
1. Fügen Sie die Version „`latest`“ der deaktivierten Ressource hinzu.
1. Speichern Sie die Eingaben und erstellen Sie den Build.
1. Folgen Sie Ihrem normalen Prozess, um Bibliotheken zur Produktion zu verschieben.
1. Veröffentlichen Sie die Bibliothek in der Produktion, um die Ressource zu entfernen.
