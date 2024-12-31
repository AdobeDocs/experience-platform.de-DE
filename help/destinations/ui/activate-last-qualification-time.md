---
title: Verwenden des XDM-Attributs für die letzte Qualifikationszeit in den neuen Beta-Cloud-Speicherzielen
description: Erfahren Sie, wie Sie das XDM-Attribut der letzten Qualifikationszeit in den neuen Beta-Cloud-Speicherzielen verwenden
badgeBeta: label="Beta" type="Informative"
exl-id: d077ea10-5ff2-4acc-8ee6-78ea6cd752d1
source-git-commit: 7130ac46a7768ea6e71bf73eb970bf2890323d0f
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 10%

---

# Verwenden des XDM-Attributs für die letzte Qualifikationszeit in den neuen Beta-Cloud-Speicherzielen {#last-qualification-time}

>[!IMPORTANT]
> 
>Auf dieser Seite werden Funktionen beschrieben, die sich in der Beta-Phase befinden. Die Funktionalität und Dokumentation können sich ändern. Wenden Sie sich an den Adobe-Support-Mitarbeiter oder die Kundenunterstützung, wenn Sie Zugang zu diesem Beta-Programm erhalten möchten.

## Voraussetzungen {#prerequisites}

Um das XDM-Attribut Letzte Qualifikationszeit (`lastQualificationTime`) verwenden zu können, müssen Sie Daten an eines der sechs unten aufgeführten Cloud-Speicher-Ziele exportieren:

* [[!DNL ADLS Gen 2]](/help/destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md)
* [[!DNL Azure Blob]](/help/destinations/catalog/cloud-storage/azure-blob.md)
* [[!DNL Data Landing Zon]e](/help/destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL Google Cloud Storage]](/help/destinations/catalog/cloud-storage/google-cloud-storage.md)
* [SFTP](/help/destinations/catalog/cloud-storage/sftp.md)

## Verwenden des XDM-Attributs für die letzte Qualifikationszeit {#how-to-use}

Wenn Sie einen der sechs oben aufgeführten Cloud-Speicher-Connectoren verwenden, können Sie das XDM-Attribut für die letzte Qualifikationszeit im [Zuordnungsschritt](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) des Aktivierungs-Workflows verwenden, um eine Spalte in der exportierten Datei mit dem neuesten Zeitstempel zu erstellen, der angibt, wann sich ein Profil für ein Segment qualifiziert hat. Dies kann Ihnen bei bestimmten Anwendungsfällen für Messungen oder Analysen helfen und Ihnen eine bessere Vorstellung davon vermitteln, wann bestimmte Zielgruppen aktiviert werden sollten.

Beachten Sie, dass Sie, um `lastQualificationTime` zu Ihren Dateiexporten hinzuzufügen, derzeit den `xdm: segmentMembership.ups.seg_id.lastQualificationTime` Wert manuell in das Quellfeld einfügen müssen, wie unten dargestellt. Sie können auch das Zielfeld so bearbeiten, dass oder ein beliebiger anderer Wert `lastQualificationTime` wird, den Sie dieser Spalte einen Namen geben möchten. Da es sich um eine Beta-Funktion handelt, kann sich die Syntax des `xdm: segmentMembership.ups.seg_id.lastQualificationTime` in Zukunft ändern.

![Bildschirmaufzeichnung, die die letzte Qualifikationszeit anzeigt, in die das XDM-Attribut im Zuordnungsschritt eingefügt wurde](/help/destinations/ui/last-qualification-time.gif)

## Weitere Informationen {#more-information}

Ausführliche Informationen zum Aktivieren von Daten für dateibasierte Ziele, einschließlich aller Schritte im Workflow und der erforderlichen Berechtigungen, finden Sie im [Tutorial zum Aktivieren dateibasierter Ziele](/help/destinations/ui/activate-batch-profile-destinations.md).
