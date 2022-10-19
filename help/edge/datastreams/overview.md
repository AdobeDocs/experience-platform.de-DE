---
title: Übersicht über Datenströme
description: Verbinden Sie Ihre Client-seitige Experience Platform SDK-Integration mit Adobe-Produkten und Zielen von Drittanbietern.
keywords: Konfiguration;Datenströme;datastreamId;edge;datastream id;Umgebungseinstellungen;edgeConfigId;identity;id sync enabled;ID Sync Container ID;Sandbox;Streaming Inlet;Ereignis-Datensatz;Target;Client-Code;Eigenschafts-Token;Target-Umgebungs-ID;Cookie-Ziele;URL-Ziele;Analytics Settings Blockreport suite id;Datenvorbereitung für Datenerfassung;Data Prep;Mapper;XDM Mapper;Mapper in Edge;
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: 2cec87d3f45b1b774925a9b669b53a958e65e57a
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 21%

---

# Übersicht über Datenströme

Ein Datenstrom stellt die Server-seitige Konfiguration bei der Implementierung der Adobe Experience Platform Web- und Mobile-SDKs dar. Während mit dem [configure-Befehl](../fundamentals/configuring-the-sdk.md) im SDK Elemente kontrolliert werden, die auf dem Client verarbeitet werden müssen (z. B. die `edgeDomain`), handhaben Datenströme alle anderen Konfigurationen für das SDK. Wenn eine Anfrage an das Adobe Experience Platform Edge Network gesendet wird, wird die `edgeConfigId` verwendet, um auf den Datenstrom zu verweisen. Auf diese Weise können Sie die Server-seitige Konfiguration aktualisieren, ohne Code-Änderungen auf Ihrer Website vornehmen zu müssen.

Sie können Datenspeicher erstellen und verwalten, indem Sie **[!UICONTROL Datenspeicher]** im linken Navigationsbereich der Benutzeroberfläche von Adobe Experience Platform oder der Datenerfassungs-Benutzeroberfläche.

![Registerkarte „Datenströme“ in der Benutzeroberfläche](../assets/datastreams/overview/datastreams-tab.png)

Weitere Informationen zum Konfigurieren eines Datastreams in der Benutzeroberfläche finden Sie unter [Konfigurationshandbuch](./configure.md).

## Umgang mit sensiblen Daten in Datastreams {#sensitive}

>[!IMPORTANT]
>
>Der Inhalt dieses Dokuments ist keine Rechtsberatung und soll keine Rechtsberatung ersetzen. Wenden Sie sich an die Rechtsabteilung Ihres Unternehmens, um Ratschläge zur Verarbeitung sensibler Daten zu erhalten.

Richtlinien zur Unternehmensdatenverwaltung und rechtliche Anforderungen der Unternehmen beschränken zunehmend, wie vertrauliche Kundendaten erfasst, verarbeitet und verwendet werden können. Dazu gehören die Erhebung, Verarbeitung und Nutzung geschützter Gesundheitsdaten (PHI), die Vorschriften wie dem Health Insurance Portability and Accounability Act (HIPAA) unterliegen.

Datastreams bietet drei Methoden, die Sie bei der sicheren Verarbeitung vertraulicher Daten unterstützen:

* [Verbesserte Verschlüsselung](#encryption)
* [Data Governance](#governance)
* [Auditprotokolle](#audit-logs)

### Verbesserte Verschlüsselung {#encryption}

Alle Daten, die durch das Edge-Netzwerk übertragen werden, werden über sichere, verschlüsselte Verbindungen mit [HTTPS TLS 1.2](https://datatracker.ietf.org/doc/html/rfc5246). Wenn der Datastream Daten in die Experience Platform einbringt, werden die Daten im Data Lake der Experience Platform im Ruhezustand verschlüsselt. Siehe Dokument unter [Datenverschlüsselung in Experience Platform](../../landing/governance-privacy-security/encryption.md) für weitere Informationen.

### Data Governance {#governance}

Datastreams nutzt die integrierten Data Governance-Funktionen von Experience Platform, um zu verhindern, dass sensible Daten an nicht HIPAA-fähige Dienste gesendet werden. Durch die Beschriftung bestimmter Felder, die sensible Daten in Ihren Datenasterschemas enthalten, können Sie präzise steuern, welche Datenfelder für bestimmte Zwecke verwendet werden können.

Das folgende Video bietet einen kurzen Überblick darüber, wie Datennutzungsbeschränkungen für Datenspeicher in der Benutzeroberfläche konfiguriert und durchgesetzt werden:

>[!VIDEO](https://video.tv.adobe.com/v/3409588/?quality=12&learn=on&speedcontrol=on)

In Experience Platform können Sie [Nutzungsbezeichnungen für vertrauliche Daten](../../data-governance/labels/reference.md#sensitive) zu Schemata und Feldern, die Daten enthalten, die Ihre Organisation für vertraulich hält. Beispiel: die `RHD` Der Titel wird verwendet, um geschützte Gesundheitsinformationen (PHI) zu kennzeichnen, und die `S1` label stellt Geolocation-Daten dar.

>[!NOTE]
>
>Weitere Informationen zum Anwenden von Datennutzungsbezeichnungen in der [!UICONTROL Schemas] Registerkarte in der Experience Platform-Benutzeroberfläche oder der Datenerfassungs-Benutzeroberfläche finden Sie im Abschnitt [Tutorial zur Schemakennung](../../xdm/tutorials/labels.md).

Wenn beim Erstellen eines neuen Datastreams das ausgewählte Schema vertrauliche Datennutzungsbezeichnungen enthält, kann der Datastream nur so konfiguriert werden, dass diese Daten an HIPAA-bereite Ziele gesendet werden. Derzeit ist Adobe Experience Platform das einzige HIPAA-bereite Ziel, das von Datastreams unterstützt wird. Andere Zieldienste wie Adobe Target, Adobe Analytics, Adobe Audience Manager, Ereignisweiterleitung und Edge-Ziele sind für Datenspeicher mit sensiblen Datennutzungsbezeichnungen deaktiviert.

Wenn ein Schema in einem vorhandenen Datastream mit nicht HIPAA-fähigen Diensten verwendet wird, führt der Versuch, dem Schema eine Beschriftung zur sensiblen Datennutzung hinzuzufügen, zu einer Richtlinienverletzungsmeldung und die Aktion wird verhindert. Die Meldung gibt an, welcher Datastream den Verstoß ausgelöst hat, und schlägt vor, alle nicht HIPAA-fähigen Dienste aus dem Datastream zu entfernen, um das Problem zu beheben.

### Auditprotokolle

In Experience Platform können Datastream-Aktivitäten in Form von Prüfprotokollen überwacht werden. Ein Auditprotokoll teilt **who** ausgeführt **what** Aktion und **when**, zusammen mit anderen Kontextdaten, die Ihnen bei der Fehlerbehebung von Problemen im Zusammenhang mit Datastreams helfen können, damit Ihr Unternehmen die Richtlinien zur Unternehmensdatenverwaltung und die gesetzlichen Vorschriften einhalten kann.

Jedes Mal, wenn ein Benutzer einen Datastream erstellt, aktualisiert oder löscht, wird ein Auditprotokoll erstellt, um die Aktion aufzuzeichnen. Dasselbe tritt auf, wenn ein Benutzer eine Zuordnung erstellt, aktualisiert oder löscht über [Datenvorbereitung für die Datenerfassung](./data-prep.md). Unabhängig davon, ob es sich um einen Datastream oder eine Zuordnung handelt, die aktualisiert wurde, wird das resultierende Auditprotokoll unter der Kategorie [!UICONTROL Datenspeicher] Ressourcentyp.

Weitere Informationen finden Sie in der Dokumentation unter [Auditprotokolle](../../landing/governance-privacy-security/audit-logs/overview.md) Weitere Informationen zur Interpretation von Protokollen aus Datenspeichern und anderen unterstützten Diensten.

## Nächste Schritte

Dieses Handbuch bietet einen allgemeinen Überblick über Datenspeicher und deren Verwendung bei der Datenerfassung und der Verarbeitung sensibler Daten. Anweisungen zum Einrichten eines neuen Datastreams finden Sie in der [Konfigurationsleitfaden für Datenspeicher](./configure.md).
