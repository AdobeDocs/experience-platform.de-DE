---
title: Löschen von Ressourcen
description: Erfahren Sie, wie Sie Tag-Ressourcen in Adobe Experience Platform löschen.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 81%

---

# Löschen von Ressourcen

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Das Löschen einer Ressource entfernt diese Ressource dauerhaft aus Adobe Experience Platform. Wenn die Ressource weiterhin in der Benutzeroberfläche für die Datenerfassung, aber nicht in Ihrer Tag-Bibliothek angezeigt werden soll, finden Sie weitere Informationen unter [Entfernen von Ressourcen aus einer Bibliothek](remove-resources-from-library.md).

Sie können Datenelemente, Regeln, Erweiterungen, Hosts, Umgebungen und Properties löschen. Nach der Löschung sind diese Ressourcen nicht wiederherstellbar.

Bei Ressourcen, die zu Bibliotheken hinzugefügt werden (Datenelemente, Regeln und Erweiterungen), sind beim Löschen einige spezielle Punkte zu beachten.

## Vorbereiten einer Ressource zum Löschen

Ressourcen sind in verschiedenen Status vorhanden und voneinander abhängig. Bevor Sie eine Ressource löschen, müssen Sie sicherstellen, dass sie sich in einem nicht löschbaren Status befindet.

Die Vorbereitung einer Ressource zum Löschen umfasst zwei grundlegende Schritte:

1. Aufheben von Abhängigkeiten
1. Entfernen aus Bibliotheken

### Aufheben von Abhängigkeiten

Regeln, Datenelemente und Erweiterungen sind voneinander abhängig. Deshalb kommt es bei den meisten Löschvorgängen auch zu Auswirkungen auf andere Elemente, die Sie berücksichtigen müssen.

#### Regeln

Regeln hängen von anderen Ressourcen (Erweiterungen und Datenelementen) ab, verfügen jedoch nicht über Ressourcen, die davon abhängig sind. Das Löschen einer Regel bedeutet, dass Sie sie nicht mehr in einer Bibliothek verwenden oder anzeigen können. Es bestehen jedoch keine Abhängigkeiten, um die Sie sich kümmern müssen.

#### Datenelemente

Datenelemente hängen von Erweiterungen ab. Im Gegensatz zu Regeln können Datenelemente jedoch Regeln und Erweiterungen enthalten, die davon abhängen. Wenn Sie ein Datenelement löschen, wirkt sich dies auf alle von diesem Datenelement abhängigen Regeln oder Erweiterungen aus.

Nach dem Löschen gibt das Datenelement zur Laufzeit keinen korrekten Wert mehr zurück. Entweder wird eine leere Zeichenfolge oder der Name des gelöschten Datenelements (eingeschlossen in %%) zurückgegeben. Beispiel: `%data-element-name%`. Dieses Verhalten kann in Property-Einstellungen konfiguriert werden.

Sie können diese Abhängigkeiten vor oder nach dem Löschen des Datenelements aufheben.

#### Erweiterungen

Alle anderen Ressourcen (Regeln, Regelkomponenten und Datenelemente) werden durch Erweiterungen bereitgestellt.

Regelkomponenten und Datenelemente sind hinsichtlich ihres Verhaltens, aber auch zur bloßen Anzeige in der Datenerfassungs-Benutzeroberfläche von Erweiterungen abhängig. Wenn Sie die jeweilige Erweiterung löschen, bevor Sie die Abhängigkeiten aufheben, können Sie diese verwaisten Ressourcen nicht mehr anzeigen. Entsprechende Ressourcen werden zwar in Listenansichten angezeigt, Sie erhalten jedoch eine Fehlermeldung, wenn Sie versuchen, ihre Detailansicht zu öffnen.

Aus diesem Grund sollten Sie beim Löschen von Erweiterungen sehr vorsichtig vorgehen und Abhängigkeiten aufheben, bevor Sie Elemente löschen.

### Entfernen aus Bibliotheken

Bevor Sie eine Ressource löschen können, müssen Sie sie zunächst aus allen Bibliotheken entfernen, in denen sie enthalten ist. Dieser Vorgang unterscheidet sich je nach Status der Bibliothek.

#### Entwicklung

1. Öffnen Sie die Bibliothek.
1. Entfernen Sie die Ressource.
1. Speichern Sie die Bibliothek.
1. Löschen Sie die Ressource.

#### Gesendet oder genehmigt

1. Lehnen Sie die Bibliothek ab (verschiebt sie zurück in die Entwicklung).
1. Gehen Sie wie folgt vor, um eine Ressource aus einer Entwicklungsbibliothek zu entfernen.

#### Produktion

1. Deaktivieren Sie die Ressource.
1. Veröffentlichen Sie die deaktivierte Ressource in der Produktion.
1. Löschen Sie die Ressource.

## Löschen von Ressourcen

Wählen Sie in der entsprechenden Listenansicht die Ressource aus, die Sie löschen möchten, und klicken Sie auf **[!UICONTROL Löschen]**.
