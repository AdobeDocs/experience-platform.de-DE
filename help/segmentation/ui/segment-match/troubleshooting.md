---
keywords: Experience Platform; Startseite; beliebte Themen; Segmentierung; Segmentierung; Segmentübereinstimmung; Segmentübereinstimmung
solution: Experience Platform
title: Häufig gestellte Fragen zur Segmentübereinstimmung
description: Segmentabgleich ist ein Dienst zur Segmentfreigabe in Adobe Experience Platform, mit dem zwei oder mehr Platform-Benutzer Segmentdaten auf sichere, gesteuerte und datenschutzfreundliche Weise austauschen können.
exl-id: cfa9db16-0bc3-4d25-914d-0d923eccb5a3
source-git-commit: 823eb549e5514a3201ba68ed395c69e202cb747f
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---

# [!DNL Segment Match] häufig gestellte Fragen

Dieses Handbuch enthält Antworten auf Datenschutz- und Rechtsfragen, die häufig zur Adobe Experience Platform-Segmentübereinstimmung gestellt werden.

## Welche Daten werden während der Überschneidungen mit den Schätzungen freigegeben und wie kann Adobe sicherstellen, dass diese Metriken sicher erhalten werden?

![lap-report.png](./images/overlap-report.png)

Es werden keine Kunden- oder Segmentdaten über Sandboxes hinweg verschoben, um diese Überschneidungsschätzmetriken zu erhalten. Die vom Kunden ausgewählten, vorab gehashten anwendbaren Identitäten in einer beliebigen Sandbox werden einer probabilistischen Datenstruktur hinzugefügt, in der die IDs selbst in einem Hash-Format dargestellt werden.

Dies ist ein unidirektionaler Prozess, d. h. die ursprünglichen vorab gehashten Kennungen werden nicht offen gelegt und können nicht rückwärts bearbeitet werden.

Diese Datenstrukturen verfügen über eindeutige Eigenschaften, die es dem Engineering ermöglichen, Vereinigungs- und Schnittstellenvorgänge zwischen ihnen durchzuführen, selbst wenn die kodierten Informationen stark komprimiert oder gehasht sind. Diese Vorgänge ermöglichen [!DNL Segment Match] um die geschätzte Schnittmenge aus zwei Datenstrukturen abzurufen, die aus IDs aus zwei verschiedenen Sandboxes bestehen, ohne die tatsächlichen Werte vergleichen zu müssen. Seit [!DNL Segment Match] verwendet nur die Datenstrukturen, verlassen die IDs die Profilspeicher ihrer IMS-Organisationen nie für Schätzzwecke. Dies ermöglicht es der Adobe, die Datenschutz- und Sicherheitsanforderungen der Kunden zu erfüllen und gleichzeitig hochgenaue Schätzwerkzeuge zur Anleitung von Vereinbarungen über die Datenzusammenarbeit anzubieten.

## Was ist der Prozess hinter der Angabe, welche Identitäten die freigegebenen Segment-IDs erhalten?

[!DNL Segment Match] bietet Kunden die Möglichkeit, zu konfigurieren, welche Namespaces im Dienst verwendet werden sollen. Diese Auswahl wird sowohl auf den in der vorherigen Frage beschriebenen Schätzungsprozess als auch auf den Datenübertragungsprozess angewendet, wenn der Kunde beschließt, den Feed in einer Partner-Sandbox zu veröffentlichen.

Der Datenübertragungsprozess zwischen den verschlüsselten Identitäten zweier verschiedener Organisationen wird in einer neutralen Compute-Umgebung durchgeführt. Der Datenübertragungsauftrag wird von der Adobe übernommen. Die an der Partnerschaft beteiligten Organisationen haben keinen Zugriff auf diese Umgebung und sie erhalten auch keinen Zugriff auf Protokolle, die aus dem Datenübertragungsauftrag hervorgehen können.

Nur die Segmentzugehörigkeit wird in die überlappenden Profilfragmente der IMS-Organisation des Empfängers aufgenommen und keine zusätzliche Identität wird von der IMS-Organisation des Absenders an die IMS-Organisation des Empfängers übertragen. Es werden keine personenbezogenen Daten (PII) im Klartext vom Datenübertragungsauftrag gelesen, da [!DNL Segment Match] ermöglicht Überschneidungen nur bei SHA256-verschlüsselten Namespaces (E-Mail/Telefon) bei PII-Daten. Ergebnisse werden nie in der Compute-Umgebung gespeichert.
