---
title: Erweiterungskonfiguration
description: Erfahren Sie, wie Sie eine Tag-Erweiterung konfigurieren, um globale Einstellungen von einem Benutzer in der Adobe Experience Platform-Benutzeroberfläche oder der Datenerfassungs-Benutzeroberfläche zu erfassen.
exl-id: 2bf33617-1398-499f-8325-3849dbdb1f97
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 91%

---

# Erweiterungskonfiguration

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../term-updates.md).

Über die Erweiterungskonfiguration erfasst eine Erweiterung globale Einstellungen von einem Benutzer. Betrachten Sie beispielsweise eine Erweiterung, die es dem Benutzer ermöglicht, ein Beacon mit der Aktion „Beacon senden“ zu senden, wobei das Beacon immer eine Konto-ID enthalten muss. Wir möchten den Benutzern ersparen, dass sie jedes Mal, wenn sie eine Aktion „Beacon senden“ konfigurieren, zur Eingabe der Konto-ID aufgefordert werden. Stattdessen sollte die Erweiterung die Konto-ID einmal in der Erweiterungskonfigurationsansicht abfragen. Jedes Mal, wenn ein Beacon gesendet werden soll, kann das Bibliotheksmodul für die Aktion „Beacon senden“ die Konto-ID aus der Erweiterungskonfiguration abrufen und dem Beacon hinzufügen.

Wenn Benutzer eine Erweiterung für eine Tag-Eigenschaft in Adobe Experience Platform installieren, wird ihnen die Erweiterungskonfigurationsansicht angezeigt, die Ihre Erweiterung bereitstellt. Sie können die Installation der Erweiterung erst abschließen, nachdem sie die Erweiterungskonfiguration abgeschlossen haben. Informationen zum Erstellen einer Ansicht für die Erweiterungskonfiguration finden Sie im Dokument [Ansichten](./web/views.md).

Nachdem die Einstellungen aus einer Erweiterungskonfigurationsansicht gespeichert wurden, werden sie in der Tag-Laufzeitbibliothek ausgegeben. Sie können dann über Module der Erweiterungsbibliothek auf diese Einstellungen zugreifen, indem Sie [`turbine.getExtensionSettings()`](./turbine.md#get-extension-settings) aufrufen.

Die Erweiterungskonfiguration ist eine optionale Funktion, die Sie möglicherweise gar nicht verwenden möchten.
