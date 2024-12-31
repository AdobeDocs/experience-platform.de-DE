---
solution: Experience Platform
title: Bekannte Einschränkungen und Fehlerbehebung bei Problemen mit Playbooks
description: Erfahren Sie mehr über bekannte Probleme und häufige Probleme mit Playbooks und deren Fehlerbehebung
role: User, Developer, Admin
exl-id: 2604ce26-bcf9-46e1-bc10-30252a113159
source-git-commit: 0faf3187c0b32e0be70033e501939412ade37d7e
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---


# Fehlerbehebung {#troubleshooting}

Hier finden Sie Vorschläge zur Fehlerbehebung bei häufigen Fehlern bei der Arbeit mit Playbooks für Anwendungsfälle

## Adobe Journey Optimizer-Oberflächen nicht konfiguriert {#surfaces-not-configured}

Beim Erstellen einer Instanz eines Playbooks wird möglicherweise die unten stehende Meldung angezeigt.

![Fehlerbehebung](/help/use-case-playbooks/assets/playbooks/troubleshooting/troubleshooting-ajo.png)

Dies liegt daran, dass Journey Optimizer-Playbooks Nachrichten für E-Mail-, Push- und SMS-Kanäle erstellen. Lesen Sie das [Erste Schritte](/help/use-case-playbooks/playbooks/get-started.md#configure-sandbox-and-channel-surfaces-in-journey-optimizer)-Handbuch, um die verschiedenen Oberflächen zu konfigurieren.

## Status *fehlgeschlagen* beim Erstellen einer neuen Instanz {#status-failed}

Wenn beim Erstellen einer Instanz eine Fehlermeldung angezeigt wird, liegt dies möglicherweise daran, dass Ihnen der Administrator die erforderlichen Benutzerberechtigungen nicht erteilt hat. Ein Playbook enthält viele verschiedene Assets, und Ihr Benutzer benötigt die Berechtigungen zum Erstellen dieser Assets, um die Instanz des Playbooks erfolgreich erstellen zu können. Informationen [ Einrichten von Berechtigungen finden ](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions) im Abschnitt „Berechtigungen“ in diesem Handbuch.

## Importfehler {#import-failure}

Kunden arbeiten in verschiedenen Testumgebungen und gelegentlich schlägt der Import einer Instanz aus ihrer Umgebung in die Adobe-Sandbox fehl. Um den Status dieser Importe anzuzeigen, wählen Sie im linken Navigationsbereich Sandbox und dann Aufträge aus. Hier können Sie alle Details der importierten Dateien anzeigen. Wählen Sie eine Datei mit dem Status Fehlgeschlagen und dann Auftragsdetails anzeigen aus. Ein modales Fenster wird angezeigt. Wählen Sie JSON-Datei anzeigen aus, blättern Sie nach unten und kopieren Sie die Fehlermeldung, die unter „Nachrichten“ angezeigt wird. Es ist durchaus möglich, dass mehrere Fehlermeldungen angezeigt werden. Achten Sie daher darauf, alle zu kopieren. Schicken Sie diese an Ihr Adobe-Team, während Sie versuchen, ein Bug-Ticket zu erstellen. Dies beschleunigt den Auflösungsprozess und gibt Ihrem Team mehr Kontext darüber, was passiert.
