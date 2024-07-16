---
title: Verwenden des letzten XDM-Attributs für die Qualifikationszeit in den neuen Beta-Cloud-Speicher-Zielen
description: Erfahren Sie, wie Sie das XDM-Attribut für die letzte Qualifikationszeit in den neuen Beta-Cloud-Speicher-Zielen verwenden
badgeBeta: label="Beta" type="Informative"
exl-id: d077ea10-5ff2-4acc-8ee6-78ea6cd752d1
source-git-commit: 7130ac46a7768ea6e71bf73eb970bf2890323d0f
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 10%

---

# Verwenden des letzten XDM-Attributs für die Qualifikationszeit in den neuen Beta-Cloud-Speicher-Zielen {#last-qualification-time}

>[!IMPORTANT]
> 
>Auf dieser Seite wird die Funktionalität der Beta-Version beschrieben. Die Funktionalität und Dokumentation können sich ändern. Wenden Sie sich an den Adobe-Support-Mitarbeiter oder die Kundenunterstützung, wenn Sie Zugang zu diesem Beta-Programm erhalten möchten.

## Voraussetzungen {#prerequisites}

Um das XDM-Attribut für die letzte Qualifikationszeit (`lastQualificationTime`) zu verwenden, müssen Sie Daten an eines der sechs unten aufgeführten Cloud-Speicher-Ziele exportieren:

* [[!DNL ADLS Gen 2]](/help/destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md)
* [[!DNL Azure Blob]](/help/destinations/catalog/cloud-storage/azure-blob.md)
* [[!DNL Data Landing Zon]e](/help/destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL Google Cloud Storage]](/help/destinations/catalog/cloud-storage/google-cloud-storage.md)
* [SFTP](/help/destinations/catalog/cloud-storage/sftp.md)

## Verwendung des XDM-Attributs für die letzte Qualifikationszeit {#how-to-use}

Wenn Sie einen der sechs oben aufgeführten Cloud-Speicher-Connectoren verwenden, können Sie das XDM-Attribut für die letzte Qualifizierungszeit im Schritt [Zuordnen](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) des Aktivierungs-Workflows verwenden, um eine Spalte in der exportierten Datei mit dem neuesten Zeitstempel zu erstellen, von der aus ein Profil für ein Segment qualifiziert wurde. Dies kann Ihnen bei bestimmten Mess- oder Analytics-Anwendungsfällen helfen und Ihnen eine bessere Vorstellung davon vermitteln, wann bestimmte Zielgruppen aktiviert werden.

Beachten Sie, dass Sie zum Hinzufügen von `lastQualificationTime` zu Ihren Dateiexporten derzeit den Wert `xdm: segmentMembership.ups.seg_id.lastQualificationTime` manuell in das Quellfeld einfügen müssen, wie unten dargestellt. Sie können das Zielfeld auch in &quot;`lastQualificationTime`&quot;oder einen anderen Wert bearbeiten, den Sie dieser Spalte nennen möchten. Da es sich um eine Beta-Funktion handelt, kann sich die Syntax des `xdm: segmentMembership.ups.seg_id.lastQualificationTime` -Werts in Zukunft ändern.

![Bildschirmaufzeichnung mit der letzten Qualifikationszeit, zu der das XDM-Attribut in den Zuordnungsschritt eingefügt wurde](/help/destinations/ui/last-qualification-time.gif)

## Weitere Informationen {#more-information}

Ausführliche Informationen zum Aktivieren von Daten für dateibasierte Ziele, einschließlich aller Schritte im Workflow und der erforderlichen Berechtigungen, finden Sie im Tutorial [Dateibasierte Ziele aktivieren](/help/destinations/ui/activate-batch-profile-destinations.md).
