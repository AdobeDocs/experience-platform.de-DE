---
solution: Experience Platform
title: Bekannte Einschränkungen und Fehlerbehebung bei Problemen mit Playbooks
description: Erfahren Sie mehr über bekannte Probleme und häufige Probleme mit Playbooks und wie Sie diese beheben können.
exl-id: 2604ce26-bcf9-46e1-bc10-30252a113159
source-git-commit: d6be5d3e21ea924ff98c400b972709b1f60c25eb
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 2%

---


# Fehlerbehebung und bekannte Einschränkungen {#troubleshooting-known-limitations}

## Fehlerbehebung {#troubleshooting}

### Nicht konfigurierte Adobe Journey Optimizer-Oberflächen

Beim Erstellen einer Instanz eines Playbooks wird möglicherweise die folgende Meldung angezeigt.

![Fehlerbehebung](/help/use-case-playbooks/assets/playbooks/troubleshooting/troubleshooting-ajo.png)

Dies liegt daran, dass Journey Optimizer-Playbooks Nachrichten für E-Mail-, Push- und SMS-Kanäle erstellen. Lesen Sie die [Erste Schritte](/help/use-case-playbooks/playbooks/get-started.md#configure-sandbox-and-channel-surfaces-in-journey-optimizer) Anleitung zur Konfiguration der verschiedenen Oberflächen.

### Status *failed* beim Erstellen einer neuen Instanz

Wenn beim Erstellen einer Instanz eine Fehlermeldung angezeigt wird, liegt dies möglicherweise daran, dass Ihnen Ihr Administrator nicht die erforderlichen Benutzerberechtigungen erteilt hat. Ein Playbook enthält viele verschiedene Assets und Ihr Benutzer benötigt Berechtigungen, um diese Assets zu erstellen, damit er die Instanz des Playbooks erfolgreich erstellen kann. Siehe [Berechtigungen](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions) Abschnitt dieses Handbuchs zum Einrichten von Berechtigungen.

## Bekannte Einschränkungen

Beim Erstellen einer Instanz eines Playbooks und Generieren von Assets werden einige bekannte Einschränkungen angezeigt.

* Wenn bei generierten Schemata ein Schema in einer Instanz eines Playbooks generiert und Sie es bearbeiten, dann ein anderes Schema *nicht* generiert werden, wenn Sie eine andere Instanz des Playbooks aktivieren. Verwenden Sie stattdessen weiterhin das Schema, das Sie in der Instanz bearbeitet haben.

* Bei Verwendung von [Datenerfassungsfunktion](/help/use-case-playbooks/playbooks/data-awareness.md) Um das Schema von der inspirierenden Sandbox in die Entwicklungs-Sandbox zu leiten, treten möglicherweise einige Fehler auf, die in etwa wie folgt aussehen:

![schema-errors](/help/use-case-playbooks/assets/playbooks/troubleshooting/schema-errors.png)

Dies liegt daran, dass einige der aus Ihrem Schema generierten Felder nicht im Schema in der Entwicklungs-Sandbox vorhanden sind, in die Sie kopieren. Suchen Sie nach diesen Feldern. Gehen Sie dann zurück zur Entwicklungs-Sandbox, in der Sie Folgendes ausführen können:

* Erstellen Sie entweder eine neue Feldergruppe mit diesen Feldern oder
* Schließen Sie in Ihr Schema eine standardmäßige, vordefinierte Feldergruppe ein, die die fehlenden Felder enthält.

Nachdem Sie diese Felder in das Schema in die Entwicklungs-Sandbox eingefügt haben, kehren Sie zum Workflow zurück, um die Schemafelder aus der inspirierenden Sandbox in die Entwicklungs-Sandbox zu kopieren. Die Fehler sind nun vorbei.

Weitere Informationen finden Sie im folgenden Video zum Erstellen von Schemafeldgruppen.

>[!VIDEO](https://video.tv.adobe.com/v/27013/?learn=on)
