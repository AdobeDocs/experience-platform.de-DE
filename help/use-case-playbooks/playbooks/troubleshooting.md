---
solution: Experience Platform
title: Bekannte Einschränkungen und Fehlerbehebung bei Problemen mit Playbooks
description: Erfahren Sie mehr über bekannte Probleme und häufige Probleme mit Playbooks und wie Sie diese beheben können.
role: User, Developer, Admin
exl-id: 2604ce26-bcf9-46e1-bc10-30252a113159
source-git-commit: 0faf3187c0b32e0be70033e501939412ade37d7e
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---


# Fehlerbehebung {#troubleshooting}

Anzeigen von Empfehlungen zur Fehlerbehebung bei häufigen Fehlern beim Arbeiten mit Anwendungsfallbüchern

## Nicht konfigurierte Adobe Journey Optimizer-Oberflächen {#surfaces-not-configured}

Beim Erstellen einer Instanz eines Playbooks wird möglicherweise die folgende Meldung angezeigt.

![Fehlerbehebung](/help/use-case-playbooks/assets/playbooks/troubleshooting/troubleshooting-ajo.png)

Dies liegt daran, dass Journey Optimizer-Playbooks Nachrichten für E-Mail-, Push- und SMS-Kanäle erstellen. Lesen Sie die [Erste Schritte](/help/use-case-playbooks/playbooks/get-started.md#configure-sandbox-and-channel-surfaces-in-journey-optimizer) Anleitung zur Konfiguration der verschiedenen Oberflächen.

## Status *failed* beim Erstellen einer neuen Instanz {#status-failed}

Wenn beim Erstellen einer Instanz eine Fehlermeldung angezeigt wird, liegt dies möglicherweise daran, dass Ihnen Ihr Administrator nicht die erforderlichen Benutzerberechtigungen erteilt hat. Ein Playbook enthält viele verschiedene Assets und Ihr Benutzer benötigt Berechtigungen, um diese Assets zu erstellen, damit er die Instanz des Playbooks erfolgreich erstellen kann. Siehe [Berechtigungen](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions) Abschnitt dieses Handbuchs zum Einrichten von Berechtigungen.

## Import-Fehler {#import-failure}

Kunden arbeiten in verschiedenen Testumgebungen. Gelegentlich kann es bei einem Import einer Instanz aus ihrer Umgebung in die Adobe-Sandbox zu Fehlern kommen. Um den Status dieser Importe anzuzeigen, wählen Sie im linken Navigationsbereich Sandbox und dann Aufträge aus. Hier können Sie alle Details der importierten Dateien anzeigen. Wählen Sie eine Datei mit dem Status &quot;Fehlgeschlagen&quot;und dann Auftragsdetails anzeigen aus. Ein Modal wird angezeigt. Wählen Sie JSON-Datei anzeigen aus, scrollen Sie nach unten und kopieren Sie die Fehlermeldung, die unter &quot;Nachrichten&quot;angezeigt wird. Es ist durchaus möglich, dass mehrere Fehlermeldungen angezeigt werden. Stellen Sie daher sicher, dass Sie alle Nachrichten kopieren. Senden Sie diese an Ihr Adobe-Team, während Sie versuchen, ein Bug-Ticket zu protokollieren. Dadurch wird der Auflösungsprozess beschleunigt und Ihr Team erhält mehr Kontext zu den Geschehnissen.
