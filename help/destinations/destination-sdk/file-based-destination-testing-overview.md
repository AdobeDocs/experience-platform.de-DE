---
description: Die dateibasierte Ziel-Test-API ist eine Sammlung von Endpunkten, mit denen Sie die Konfiguration Ihrer dateibasierten Ziele überprüfen können, die über die Destination SDK erstellt wurden.
title: Dateibasierte Ziel-Test-API
exl-id: 2733fd00-af08-4763-a30e-a53ee56c0a19
source-git-commit: 44e056407f5089c927752f00cc6bf173d7640b83
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# Dateibasierte Ziel-Test-API

## Übersicht {#overview}

Die dateibasierte Ziel-Test-API ist ein Satz von Endpunkten, mit denen Sie die Konfiguration Ihrer dateibasierten Ziele überprüfen können, die über die Destination SDK erstellt wurden.

Es wird empfohlen, diese Tools zu verwenden, um Ihre Konfiguration vor [submit](submit-destination.md) Ihr Ziel zur Überprüfung an Adobe.

Für die besten Testergebnisse empfehlen wir die Verwendung dieser API basierend auf dem unten stehenden Flussdiagramm.

![Diagramm mit dem empfohlenen Zieltestfluss](assets/file-based-testing-flow.png)

In den folgenden Abschnitten finden Sie einen kurzen Überblick darüber, was jeder Endpunkt tun kann.

## Beispielprofile generieren {#generate-sample-profiles}

Verwenden Sie die `/sample-profiles` API-Endpunkt zum Generieren von Beispielprofilen basierend auf Ihrem vorhandenen Quellschema.

Beispielprofile können Ihnen dabei helfen, die JSON-Struktur eines Profils zu verstehen. Darüber hinaus erhalten Sie eine Standardeinstellung, die Sie mit Ihren eigenen Profildaten anpassen können, um weitere Zieltests durchzuführen.

Siehe [dedizierte Dokumentation](file-based-sample-profile-generation-api.md) , um zu erfahren, wie Sie Beispielprofile generieren.

## Testzielkonfiguration {#test-destination-configuration}

Verwenden Sie die `/testing/destinationInstance` API-Endpunkt, um zu testen, ob Ihr dateibasiertes Ziel richtig konfiguriert ist, und um die Integrität der Datenflüsse zu Ihrem konfigurierten Ziel zu überprüfen.

Sie können Anforderungen an den Test-Endpunkt mit oder ohne Hinzufügen von [Beispielprofile](file-based-sample-profile-generation-api.md) an den -Aufruf. Wenn Sie bei der Anfrage keine Profile senden, generiert die API automatisch ein Beispielprofil und fügt es der Anfrage hinzu.

Siehe [dedizierte Dokumentation](file-based-destination-testing-api.md) , um zu erfahren, wie Sie Ihre Zielkonfiguration mit Beispielprofilen testen können.

## Detaillierte Aktivierungsergebnisse anzeigen {#view-detailed-activation-results}

Verwenden Sie die `/testing/destinationInstance` API-Endpunkt, an dem Sie die vollständigen Details Ihrer dateibasierten Zieltestergebnisse anzeigen können.

Dieser API-Endpunkt gibt dasselbe Ergebnis zurück, das Sie bei Verwendung von [Flussdienst-API](../api/update-destination-dataflows.md) zur Überwachung von Datenflüssen.

Siehe [dedizierte Dokumentation](file-based-destination-results-api.md) um zu erfahren, wie Sie detaillierte Aktivierungsergebnisse anzeigen können.

## Rendern von Kundendatenfeldern {#render-customer-data-fields}

Verwenden Sie die `/authoring/testing/template/render` API-Endpunkt zur Visualisierung der Vorlagenerstellung [Kundendatenfelder](file-based-destination-configuration.md#customer-data-fields) in Ihrer Zielkonfiguration definiert wurde, würde so aussehen.

Der API-Endpunkt generiert zufällige Werte für Ihre Kundendatenfelder und gibt sie in der Antwort zurück. Auf diese Weise können Sie die semantische Struktur von Kundendatenfeldern wie Behälternamen oder Ordnerpfaden überprüfen.

Siehe [dedizierte Dokumentation](file-based-render-template-api.md) , um zu erfahren, wie Sie Werte für Ihre Kundendatenfelder generieren und visualisieren können.
