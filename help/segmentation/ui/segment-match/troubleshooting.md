---
keywords: Experience Platform;Startseite;beliebte Themen;segmentierung;Segmentierung;Segment Match;segment match
solution: Experience Platform
title: Häufig gestellte Fragen zu Segment Match
description: Segment Match ist ein Service zur Segmentfreigabe in Adobe Experience Platform, mit dem zwei oder mehr Platform-Benutzende Segmentdaten auf sichere, geregelte und datenschutzsensible Weise austauschen können.
exl-id: cfa9db16-0bc3-4d25-914d-0d923eccb5a3
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 100%

---

# Häufig gestellte Fragen zu [!DNL Segment Match]

Dieses Handbuch enthält Antworten auf Datenschutz- und Rechtsfragen, die häufig zu Adobe Experience Platform Segment Match gestellt werden.

## Welche Daten werden während der geschätzten Überschneidungen freigegeben und wie kann Adobe sicherstellen, dass diese Metriken sicher abgerufen werden?

![overlap-report.png](./images/overlap-report.png)

Es werden keine Kunden- oder Segmentdaten über Sandboxes hinweg verschoben, um diese Metriken für geschätzte Überschneidungen abzurufen. Die der Kundin oder dem Kunden ausgewählten, vorab gehashten anwendbaren Identitäten in einer beliebigen Sandbox werden einer probabilistischen Datenstruktur hinzugefügt, in der die IDs selbst in einem Hash-Format dargestellt werden.

Dies ist ein unidirektionaler Prozess, d. h., die ursprünglichen, vorab gehashten Kennungen werden weder offengelegt noch kann für sie ein Reverse Engineering durchgeführt werden.

Diese Datenstrukturen verfügen über eindeutige Eigenschaften, die es dem Engineering ermöglichen, Vereinigungs- und Schnittstellenvorgänge zwischen ihnen durchzuführen, selbst wenn die codierten Informationen stark komprimiert oder gehasht sind. Durch diese Vorgänge kann [!DNL Segment Match] die geschätzte Schnittmenge aus zwei Datenstrukturen abrufen, die aus IDs aus zwei verschiedenen Sandboxes bestehen, ohne die tatsächlichen Werte vergleichen zu müssen. Da [!DNL Segment Match] nur die Datenstrukturen verwendet, verlassen die IDs nie die Profilspeicher ihrer jeweiligen Organisationen für Schätzzwecke. Dies ermöglicht es Adobe, die Datenschutz- und Sicherheitsanforderungen der Kundinnen und Kunden zu erfüllen und gleichzeitig hochgenaue Schätzwerkzeuge als Grundlage von Vereinbarungen über die Datenzusammenarbeit anzubieten.

## Welcher Prozess bildet die Grundlage zur Angabe der Identitäten, die die freigegebenen Segment-IDs erhalten?

Mit [!DNL Segment Match] können Kundinnen und Kunden konfigurieren, welche Namespaces im Service verwendet werden sollen. Diese Auswahl wird sowohl auf den in der vorherigen Frage beschriebenen Schätzungsprozess als auch auf den Datenübertragungsprozess angewendet, wenn die Kundin bzw. der Kunde beschließt, den Feed in einer Partner-Sandbox zu veröffentlichen.

Der Datenübertragungsprozess zwischen den verschlüsselten Identitäten zweier verschiedener Organisationen wird in einer neutralen Rechenumgebung durchgeführt. Für den Datenübertragungsvorgang ist Adobe verantwortlich. Die an der Partnerschaft beteiligten Organisationen haben keinen Zugriff auf diese Umgebung und sie erhalten auch keinen Zugriff auf Protokolle, die möglicherweise aus dem Datenübertragungsvorgang hervorgehen.

Nur die Segmentzugehörigkeit wird in die sich überschneidenden Profilfragmente einer Empfängerorganisation aufgenommen, und es wird keine zusätzliche Identität von der Absenderorganisation an die Empfängerorganisation übertragen. Im Zuge des Datenübertragungsvorgangs werden keine personenbezogenen Daten (Personally Identifiable Information, PII) als Klartext gelesen, da [!DNL Segment Match] im Falle von PII-Daten Überschneidungen nur bei SHA256-verschlüsselten Namespaces (E-Mail/Telefon) ermöglicht. Ergebnisse werden niemals in der Rechenumgebung gespeichert.
