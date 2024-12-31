---
title: Übersicht über Datenströme
description: Erfahren Sie, wie Datenströme Ihnen dabei helfen, Ihre Client-seitige Experience Platform SDK-Integration mit Adobe-Produkten und Drittanbieterzielen zu verbinden.
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: e3768a3f695abeedc9a3ce2fef591c6ecae9a897
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 70%

---

# Übersicht über Datenströme

Ein Datenstrom stellt die Server-seitige Konfiguration für die Adobe Experience Platform Web- und Mobile-SDKs dar. Während Client-seitige Einstellungen (z. B. die `edgeDomain`) mit dem [`configure`](/help/web-sdk/commands/configure/overview.md)-Befehl in der SDK verarbeitet werden, verwalten Datenströme alle anderen Konfigurationen.

Wenn Sie eine Anfrage an das Edge Network senden, verweist die `datastreamId` auf den Datenstrom, an den die Daten gesendet werden. Auf diese Weise können Sie die Server-seitige Konfiguration aktualisieren, ohne den Code Ihrer Website zu ändern.

Sie können Datenströme erstellen und verwalten, indem Sie **[!UICONTROL Datenströme]** in der linken Navigation innerhalb der Adobe Experience Platform-Benutzeroberfläche oder der Datenerfassungs-Benutzeroberfläche auswählen.

![Registerkarte „Datenströme“ in der Benutzeroberfläche](assets/overview/datastreams-tab.png)

Weitere Informationen zum Konfigurieren eines Datenstroms in der Benutzeroberfläche finden Sie im [Konfigurationshandbuch](./configure.md).

## Handhabung sensibler Daten in Datenströmen {#sensitive}

>[!IMPORTANT]
>
>Der Inhalt dieses Dokuments ist keine Rechtsberatung und soll keine Rechtsberatung ersetzen. Wenden Sie sich an die Rechtsabteilung Ihres Unternehmens, um sich über den Umgang mit sensiblen Daten zu beraten.

Unternehmensrichtlinien zur Datenverwaltung und gesetzliche Vorschriften schränken die Erfassung, Verarbeitung und Nutzung sensibler Kundendaten zunehmend ein. Dazu gehören die Erfassung, Verarbeitung und Verwendung geschützter Gesundheitsdaten (PHI), die Vorschriften wie dem Health Insurance Portability and Accountability Act (HIPAA) unterliegen.

Datenströme bieten drei Methoden, mit denen Sie Ihre sensiblen Daten sicher verarbeiten können:

* [Verbesserte Verschlüsselung](#encryption)
* [Data Governance](#governance)
* [Audit-Protokolle](#audit-logs)

### Verbesserte Verschlüsselung {#encryption}

Alle Daten, die durch das Edge-Netzwerk übertragen werden, werden über sichere, verschlüsselte Verbindungen mit [HTTPS TLS 1.2](https://datatracker.ietf.org/doc/html/rfc5246) übertragen. Wenn der Datenstrom Daten in Experience Platform einbringt, werden die Daten im Ruhezustand im Experience Platform Data Lake verschlüsselt. Weitere Informationen finden Sie im Dokument über [Datenverschlüsselung in Experience Platform](../landing/governance-privacy-security/encryption.md).

### Data Governance {#governance}

Datenströme verwenden die integrierten Data Governance-Funktionen von Experience Platform, um zu verhindern, dass sensible Daten an nicht HIPAA-fähige Services gesendet werden. Durch die Kennzeichnung bestimmter Felder, die sensible Daten in Ihren Datenstromschemata enthalten, können Sie genau steuern, welche Datenfelder für bestimmte Zwecke verwendet werden können.

Das folgende Video bietet einen kurzen Überblick darüber, wie Datennutzungsbeschränkungen für Datenspeicher in der Benutzeroberfläche konfiguriert und durchgesetzt werden:

>[!VIDEO](https://video.tv.adobe.com/v/3409588/?quality=12&learn=on&speedcontrol=on)

In Experience Platform können Sie [sensible Datennutzungskennzeichnungen](../data-governance/labels/reference.md#sensitive) auf Schemata und Felder anwenden, die Daten enthalten, welche Ihr Unternehmen als sensibel einstuft. So wird beispielsweise die Kennzeichnung `RHD` für geschützte Gesundheitsinformationen (PHI) verwendet, und die Kennzeichnung `S1` steht für Geolokalisierungsdaten.

>[!NOTE]
>
>Details zum Anwenden von Datennutzungskennzeichnungen auf der Registerkarte [!UICONTROL Schemata] in der Experience Platform-Benutzeroberfläche oder der Datenerfassungs-Benutzeroberfläche finden Sie im [Tutorial zur Schemakennzeichnung](../xdm/tutorials/labels.md).

Wenn Sie beim Erstellen eines Datenstroms das ausgewählte Schema vertrauliche Datennutzungskennzeichnungen enthält, können Sie den Datenstrom nur so konfigurieren, dass diese Daten an HIPAA-fähige Ziele gesendet werden. Derzeit ist Adobe Experience Platform das einzige HIPAA-fähige Ziel, das von Datenströmen unterstützt wird. Andere Zieldienste wie Adobe Target, Adobe Analytics, Adobe Audience Manager, Ereignisweiterleitung und Edge-Ziele sind für Datenströme mit sensiblen Datennutzungskennzeichnungen deaktiviert.

Wenn ein Schema in einem vorhandenen Datenstrom mit nicht HIPAA-fähigen Diensten verwendet wird, führt der Versuch, dem Schema eine sensible Datennutzungskennzeichnung hinzuzufügen, zu einer Richtlinienverletzungsmeldung und die Aktion wird verhindert. Die Meldung gibt an, welcher Datenstrom die Verletzung ausgelöst hat, und schlägt vor, alle nicht HIPAA-fähigen Services aus dem Datenstrom zu entfernen, um das Problem zu beheben.

### Audit-Protokolle

In Experience Platform können Datenstrom-Aktivitäten in Form von Administratorprotokollen überwacht werden. Audit-Protokolle geben an **wer** welche **ausgeführt** und **wann** sowie andere kontextuelle Daten, mit denen Sie Probleme im Zusammenhang mit Datenströmen beheben können, damit Ihr Unternehmen die Richtlinien zur Unternehmensdatenverwaltung und die gesetzlichen Anforderungen erfüllen kann.

Jedes Mal, wenn eine Benutzerin oder ein Benutzer einen Datenstrom erstellt, aktualisiert oder löscht, wird ein Administratorprotokoll erstellt, um die Aktion aufzuzeichnen. Dasselbe erfolgt, wenn jemand über die [Datenvorbereitung für die Datenerfassung](./data-prep.md) eine Zuordnung erstellt, aktualisiert oder löscht. Unabhängig davon, ob es sich um einen Datenstrom oder eine Zuordnung handelt, die aktualisiert wurde, wird das resultierende Administratorprotokoll unter dem Ressourcentyp [!UICONTROL Datenströme] kategorisiert.

Weitere Informationen zur Interpretation von Protokollen aus Datenströmen und anderen unterstützten Diensten finden Sie in der Dokumentation zu [Administratorprotokollen](../landing/governance-privacy-security/audit-logs/overview.md).

## Nächste Schritte

Dieses Handbuch bietet einen allgemeinen Überblick über Datenströme und deren Verwendung bei der Datenerfassung und der Verarbeitung sensibler Daten. Wie Sie einen neuen Datenstrom einrichten, erfahren Sie im [Handbuch zur Konfiguration von Datenströmen](./configure.md).
