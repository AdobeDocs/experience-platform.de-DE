---
solution: Experience Platform
title: Datenerfassung – Übersicht
description: Erfahren Sie, wie Sie Daten an Adobe Experience Platform senden.
exl-id: 03ce5339-e68d-4adf-8c3c-82846a626dad
source-git-commit: 3d51f01d314587510d900d335dc92fedb8ac31e8
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 2%

---

# Datenerfassung – Übersicht

Adobe Experience Platform bietet eine Reihe von Technologien, mit denen Sie Kundenerlebnisdaten aus verschiedenen Quellen erfassen und an Adobe Experience Platform Edge Network senden können. Diese Daten können dann angereichert, transformiert und an Adobe- oder Nicht-Adobe-Ziele verteilt werden.

Adobe unterstützt die folgenden Codesprachen mit dedizierten Bibliotheken für die Datenerfassung:

* **JavaScript**: Für Websites und Web-basierte Anwendungen
* **Kotlin**: Für Android-Geräte
* **Swift**: Für iOS-Geräte
* **BrightScript**: Für Roku-Geräte
* **Flutter**: Für Android- und iOS-Anwendungen mit Flutter
* **React Native**: Für Android- und iOS-Anwendungen, die React Native verwenden

Die Tags-Benutzeroberfläche in der Adobe Experience Platform-Datenerfassung enthält eine Web-SDK- und eine Mobile-SDK-Erweiterung.

Wenn keines der oben genannten SDKs den Anforderungen Ihres Projekts entspricht, können Sie die [Adobe Experience Platform Edge Network-API](https://developer.adobe.com/data-collection-apis/docs/) verwenden, um Daten direkt an Adobe zu senden.

## Datenerfassungsprozess

Anstatt für jedes Adobe-Produkt separate Bibliotheken zu installieren und zu implementieren, können Sie eines der oben genannten SDKs oder Tag-Erweiterungen implementieren, um alle gewünschten Daten in einer einzigen Payload zu aggregieren. Diese Payload wird an einen [Datenstrom) &#x200B;](/help/datastreams/overview.md) Adobe Experience Platform Edge Network gesendet.

![Datenerfassungsdiagramm](assets/tags-sdks.png)

Adobe Experience Platform Edge Network ist ein global verteiltes, schnelles und zuverlässiges Netzwerk von Servern, die Daten in großem Umfang empfangen und verarbeiten können. Wenn ein Datenstrom Daten empfängt, verteilt er diese Daten an jede entsprechende Lösung, die Sie konfiguriert haben. Die Daten werden in einem Format weitergeleitet, das jedes einzelne Produkt versteht.

![Adobe-Lösungsdiagramm](assets/adobe-solutions.png)

Sie können die [Ereignisweiterleitung](/help/tags/ui/event-forwarding/overview.md) auch verwenden, um Daten mit geringer Latenz und ohne Client-seitigen Implementierungs-Code zu transformieren, anzureichern und an ein Ziel zu senden, bei dem es sich nicht um Adobe handelt.

![Diagramm zur Ereignisweiterleitung](assets/event-forwarding.png)
