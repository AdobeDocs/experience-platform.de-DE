---
description: Die dateibasierte Ziel-Test-API ist eine Sammlung von Endpunkten, mit denen Sie die Konfiguration Ihrer dateibasierten Ziele überprüfen können, die über die Destination SDK erstellt wurden.
title: Dateibasierte Ziel-Test-API
source-git-commit: d2d362f4b61e04fc2fa4d9cd9db70ed94a850642
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---


# Dateibasierte Ziel-Test-API

## Übersicht {#overview}

Die dateibasierte Ziel-Test-API ist ein Satz von Endpunkten, mit denen Sie die Konfiguration Ihrer dateibasierten Ziele überprüfen können, die über die Destination SDK erstellt wurden.

Es wird empfohlen, diese Tools zu verwenden, um Ihre Konfiguration vor [submit](submit-destination.md) Ihr Ziel zur Überprüfung an Adobe.

Für die besten Testergebnisse empfehlen wir die Verwendung dieser API basierend auf dem unten stehenden Flussdiagramm.

![Diagramm mit dem empfohlenen Zieltestfluss](assets/file-based-testing-flow.png)

In den folgenden Abschnitten finden Sie einen kurzen Überblick darüber, was jeder Endpunkt tun kann.

## Beispiel-Generierungsendpunkt {#sample-generation-endpoint}

Dieser Endpunkt hilft Ihnen beim Generieren von Beispielprofilen basierend auf Ihrem vorhandenen Quellschema.

Beispielprofile sollen Ihnen dabei helfen, die JSON-Struktur eines Profils zu verstehen. Darüber hinaus erhalten Sie damit ein Backbone, das Sie mit Ihren eigenen Profildaten anpassen können, um weitere Zieltests durchzuführen.

Siehe [dedizierte Dokumentation](file-based-sample-profile-generation-api.md) , um zu erfahren, wie Sie Beispielprofile generieren.

## Endpunkt zum Testen der Zielkonfiguration {#destination-configuration-testing-endpoint}

Mithilfe dieses Endpunkts können Sie testen, ob Ihr dateibasiertes Ziel richtig konfiguriert ist, und die Integrität der Datenflüsse zu Ihrem konfigurierten Ziel überprüfen.

Sie können Anforderungen an den Test-Endpunkt mit oder ohne Hinzufügen von [Beispielprofile](file-based-sample-profile-generation-api.md) an den -Aufruf. Wenn Sie bei der Anfrage keine Profile senden, generiert die API automatisch ein Beispielprofil und fügt es der Anfrage hinzu.

Siehe [dedizierte Dokumentation](file-based-destination-testing-api.md) , um zu erfahren, wie Sie Ihre Zielkonfiguration mit Beispielprofilen testen können.

## Endpunkt der Aktivierungsergebnisse {#activation-results}

Mithilfe dieses Endpunkts können Sie die vollständigen Details Ihrer dateibasierten Zieltestergebnisse anzeigen.

Dieser API-Endpunkt gibt dasselbe Ergebnis zurück, das Sie bei Verwendung von [Flussdienst-API](../api/update-destination-dataflows.md) zur Überwachung von Datenflüssen.

Siehe [dedizierte Dokumentation](file-based-destination-results-api.md) um zu erfahren, wie Sie detaillierte Aktivierungsergebnisse anzeigen können.

## Rendering-Endpunkt der Kundenfelder {#customer-fields-rendering-endpoint}

Dieser Endpunkt hilft Ihnen bei der Visualisierung der Vorlagenerstellung [Kundendatenfelder](file-based-destination-configuration.md#customer-data-fields) in Ihrer Zielkonfiguration definiert wurde, würde so aussehen.

Der Endpunkt generiert zufällige Werte für Ihre Kundendatenfelder und gibt sie in der Antwort zurück. Auf diese Weise können Sie die semantische Struktur von Kundendatenfeldern, wie z. B. Behälternamen oder Ordnerpfaden, überprüfen.

Siehe [dedizierte Dokumentation](file-based-render-template-api.md) um zu erfahren, wie Sie detaillierte Aktivierungsergebnisse anzeigen können.