---
title: Übersicht über Datenströme
description: Verbinden Sie Ihre Client-seitige Experience Platform SDK-Integration mit Adobe-Produkten und Zielen von Drittanbietern.
keywords: Konfiguration;Datenströme;datastreamId;edge;datastream id;Umgebungseinstellungen;edgeConfigId;identity;id sync enabled;ID Sync Container ID;Sandbox;Streaming Inlet;Ereignis-Datensatz;Target;Client-Code;Eigenschafts-Token;Target-Umgebungs-ID;Cookie-Ziele;URL-Ziele;Analytics Settings Blockreport suite id;Datenvorbereitung für Datenerfassung;Data Prep;Mapper;XDM Mapper;Mapper in Edge;
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: 5f2358c2e102c66a13746004ad73e2766e933705
workflow-type: ht
source-wordcount: '780'
ht-degree: 100%

---


# Übersicht über Datenströme

Ein Datenstrom stellt die Server-seitige Konfiguration bei der Implementierung der Adobe Experience Platform Web- und Mobile-SDKs dar. Während mit dem [configure-Befehl](../edge/fundamentals/configuring-the-sdk.md) im SDK Elemente kontrolliert werden, die auf dem Client verarbeitet werden müssen (z. B. die `edgeDomain`), handhaben Datenströme alle anderen Konfigurationen für das SDK. Wenn eine Anfrage an das Adobe Experience Platform Edge Network gesendet wird, wird die `edgeConfigId` verwendet, um auf den Datenstrom zu verweisen. Auf diese Weise können Sie die Server-seitige Konfiguration aktualisieren, ohne Code-Änderungen auf Ihrer Website vornehmen zu müssen.

Sie können Datenströme erstellen und verwalten, indem Sie **[!UICONTROL Datenströme]** in der linken Navigation innerhalb der Adobe Experience Platform-Benutzeroberfläche oder der Datenerfassungs-Benutzeroberfläche auswählen.

![Registerkarte „Datenströme“ in der Benutzeroberfläche](assets/overview/datastreams-tab.png)

Weitere Informationen zum Konfigurieren eines Datenstroms in der Benutzeroberfläche finden Sie im [Konfigurationshandbuch](./configure.md).

## Handhabung sensibler Daten in Datenströmen {#sensitive}

>[!IMPORTANT]
>
>Der Inhalt dieses Dokuments ist keine Rechtsberatung und soll keine Rechtsberatung ersetzen. Wenden Sie sich an die Rechtsabteilung Ihres Unternehmens, um Ratschläge zur Verarbeitung sensibler Daten zu erhalten.

Unternehmensrichtlinien zur Datenverwaltung und gesetzliche Vorschriften schränken die Erfassung, Verarbeitung und Nutzung sensibler Kundendaten zunehmend ein. Dazu gehören die Erfassung, Verarbeitung und Verwendung geschützter Gesundheitsdaten (PHI), die Vorschriften wie dem Health Insurance Portability and Accountability Act (HIPAA) unterliegen.

Datenströme bietet drei Methoden, um Sie bei der sicheren Handhabung Ihrer sensiblen Daten zu unterstützen:

* [Verbesserte Verschlüsselung](#encryption)
* [Data Governance](#governance)
* [Audit-Protokolle](#audit-logs)

### Verbesserte Verschlüsselung {#encryption}

Alle Daten, die durch das Edge-Netzwerk übertragen werden, werden über sichere, verschlüsselte Verbindungen mit [HTTPS TLS 1.2](https://datatracker.ietf.org/doc/html/rfc5246) übertragen. Wenn der Datenstrom Daten in Experience Platform einbringt, werden die Daten im Ruhezustand im Experience Platform Data Lake verschlüsselt. Weitere Informationen finden Sie im Dokument über [Datenverschlüsselung in Experience Platform](../landing/governance-privacy-security/encryption.md).

### Data Governance {#governance}

Datenströme nutzen die integrierten Data Governance-Funktionen von Experience Platform, um zu verhindern, dass sensible Daten an nicht HIPAA-fähige Dienste gesendet werden. Durch die Kennzeichnung bestimmter Felder, die sensible Daten in Ihren Datenstromschemata enthalten, können Sie genau steuern, welche Datenfelder für bestimmte Zwecke verwendet werden können.

Das folgende Video bietet einen kurzen Überblick darüber, wie Datennutzungsbeschränkungen für Datenspeicher in der Benutzeroberfläche konfiguriert und durchgesetzt werden:

>[!VIDEO](https://video.tv.adobe.com/v/3409588/?quality=12&learn=on&speedcontrol=on)

In Experience Platform können Sie [sensible Datennutzungskennzeichnungen](../data-governance/labels/reference.md#sensitive) auf Schemata und Felder anwenden, die Daten enthalten, welche Ihr Unternehmen als sensibel einstuft. So wird beispielsweise die Kennzeichnung `RHD` für geschützte Gesundheitsinformationen (PHI) verwendet, und die Kennzeichnung `S1` steht für Geolokalisierungsdaten.

>[!NOTE]
>
>Details zum Anwenden von Datennutzungskennzeichnungen auf der Registerkarte [!UICONTROL Schemata] in der Experience Platform-Benutzeroberfläche oder der Datenerfassungs-Benutzeroberfläche finden Sie im [Tutorial zur Schemakennzeichnung](../xdm/tutorials/labels.md).

Wenn beim Erstellen eines neuen Datenstroms das ausgewählte Schema vertrauliche Datennutzungskennzeichnungen enthält, kann der Datenstrom nur so konfiguriert werden, dass diese Daten an HIPAA-fähige Ziele gesendet werden. Derzeit ist Adobe Experience Platform das einzige HIPAA-fähige Ziel, das von Datenströmen unterstützt wird. Andere Zieldienste wie Adobe Target, Adobe Analytics, Adobe Audience Manager, Ereignisweiterleitung und Edge-Ziele sind für Datenströme mit sensiblen Datennutzungskennzeichnungen deaktiviert.

Wenn ein Schema in einem vorhandenen Datenstrom mit nicht HIPAA-fähigen Diensten verwendet wird, führt der Versuch, dem Schema eine sensible Datennutzungskennzeichnung hinzuzufügen, zu einer Richtlinienverletzungsmeldung und die Aktion wird verhindert. Die Meldung gibt an, welcher Datenstrom den Verstoß ausgelöst hat, und schlägt vor, alle nicht HIPAA-fähigen Dienste aus dem Datenstrom zu entfernen, um das Problem zu beheben.

### Audit-Protokolle

In Experience Platform können Datenstrom-Aktivitäten in Form von Administratorprotokollen überwacht werden. Ein Administratorprotokoll gibt Aufschluss darüber, **wer** **welche** Aktion **wann** ausgeführt hat; sowie über andere kontextbezogene Daten, die Ihnen helfen können, Probleme im Zusammenhang mit Datenströmen zu beheben, um Ihr Unternehmen bei der Einhaltung der Unternehmensrichtlinien für die Datenverwaltung und der gesetzlichen Vorschriften zu unterstützen.

Jedes Mal, wenn eine Benutzerin oder ein Benutzer einen Datenstrom erstellt, aktualisiert oder löscht, wird ein Administratorprotokoll erstellt, um die Aktion aufzuzeichnen. Dasselbe erfolgt, wenn jemand über die [Datenvorbereitung für die Datenerfassung](./data-prep.md) eine Zuordnung erstellt, aktualisiert oder löscht. Unabhängig davon, ob es sich um einen Datenstrom oder eine Zuordnung handelt, die aktualisiert wurde, wird das resultierende Administratorprotokoll unter dem Ressourcentyp [!UICONTROL Datenströme] kategorisiert.

Weitere Informationen zur Interpretation von Protokollen aus Datenströmen und anderen unterstützten Diensten finden Sie in der Dokumentation zu [Administratorprotokollen](../landing/governance-privacy-security/audit-logs/overview.md).

## Nächste Schritte

Dieses Handbuch bietet einen allgemeinen Überblick über Datenströme und deren Verwendung bei der Datenerfassung und der Verarbeitung sensibler Daten. Wie Sie einen neuen Datenstrom einrichten, erfahren Sie im [Handbuch zur Konfiguration von Datenströmen](./configure.md).
