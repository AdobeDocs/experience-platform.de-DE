---
title: CMK-Referenz zur Warnhinweisauflösung
description: Identifizieren, beheben und beheben Sie häufige Warnhinweise, die durch Fehlkonfigurationen von kundenverwalteten Schlüsseln (CMK) in Adobe Experience Platform ausgelöst werden. Verwenden Sie dieses Handbuch, um klare, schrittweise Anweisungen zu befolgen und den sicheren Schlüsselzugriff wiederherzustellen.
exl-id: ffe2eadc-dfb5-418b-a201-2c20dcc9cfe4
source-git-commit: e8cfed9ebd50cf50f03e232755eddef1cb8c0d3b
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 1%

---

# CMK-Referenz zur Warnhinweisauflösung

Verwenden Sie dieses Handbuch, um eine Fehlerbehebung bei Warnhinweisen durchzuführen, die durch falsch konfigurierte CMK-Einstellungen (Customer Managed Key) in Adobe Experience Platform ausgelöst werden. Dies hilft Systemadministratoren und Implementierungsspezialisten, Ursachen zu identifizieren und Lösungen anzuwenden, um den sicheren Zugriff wiederherzustellen.

## Warnhinweiskategorien {#categories}

In den folgenden Abschnitten werden die Arten von Warnhinweisen beschrieben, die durch Probleme mit kundenverwalteten Schlüsseln (CMK) in Adobe Experience Platform ausgelöst werden können:

- [Schlüsselzugriff deaktiviert](#key-access-disabled)
- [Schlüsselzugriff fehlgeschlagen](#key-access-failure)
- [Benachrichtigung bei Warnhinweisen](#alert-notification)

## Schlüsselzugriff deaktiviert {#key-access-disabled}

Dieser Warnhinweis zeigt an, dass Adobe Experience Platform nicht auf das konfigurierte CMK zugreifen kann, da der Schlüssel aufgrund der Konfiguration deaktiviert ist oder nicht zugänglich ist. In solchen Fällen behandelt das System die Bedingung als eine absichtliche Entfernung des Schlüsselzugriffs.

### Wenn er auftritt

Dieser Warnhinweis wird ausgelöst, wenn sich der Verschlüsselungsschlüssel im Azure-Schlüsseltresor in einem deaktivierten Zustand befindet, gelöscht oder falsch konfiguriert ist, sodass der Zugriff während Platform-Vorgängen verhindert wird.

### Mögliche Ursachen

Die folgenden häufigen Gründe können für diesen Warnhinweis auftreten:

- Der Schlüssel wurde manuell deaktiviert.
- Schlüsseloperationen (wrapKey/unwrapKey) wurden entfernt.
- Das Aktivierungsdatum des Schlüssels liegt in der Zukunft.
- Das Gültigkeitsdatum des Schlüssels liegt in der Vergangenheit.
- Der Schlüssel wurde gelöscht.
- Die Berechtigungen für die Multi-Mandanten-App wurden entfernt oder geändert.
- Die MultiMandant-App wurde gelöscht.
- Die Eigenschaften der Multi-Mandanten-App wurden geändert.
- Der Schlüsseltresor wurde gelöscht oder ist nicht mehr zugänglich.

### Auflösung

+++Wenn der Schlüssel deaktiviert ist

1. Navigieren Sie zum [Azure-Schlüsseltresor](https://portal.azure.com/), der das CMK enthält.
2. Wählen Sie den Schlüssel aus, der mit Adobe Experience Platform verknüpft ist.
3. Stellen Sie sicher, dass der Status des Schlüssels auf (**)**.
4. Wenn der Schlüssel deaktiviert ist, aktivieren Sie ihn über das Azure-Portal oder die CLI-`az keyvault key enable`.

>[!NOTE]
>
>Passen Sie diesen Befehl für Ihre Azure-Umgebung an.

+++

+++Wenn Schlüsselfunktionen geändert wurden

1. Fügen Sie die `wrapKey` und `unwrapKey` Berechtigungen erneut zum Schlüssel hinzu.

>[!NOTE]
>
>Alle Einstellungen des Schlüssels - einschließlich der Aktivierungs- und Ablaufdaten - müssen gültig sein, damit der Schlüssel funktioniert.

+++

+++Wenn das Aktivierungs- oder Ablaufdatum falsch konfiguriert ist

1. Legen Sie das Aktivierungsdatum auf die Vergangenheit oder Gegenwart fest.
2. Legen Sie das Ablaufdatum auf ein Datum in der Zukunft fest.

+++

+++Wenn der Schlüssel gelöscht wurde

1. Stellen Sie sicher, dass „Soft Delete“ im Azure-Schlüsseltresor aktiviert ist.
2. Navigieren Sie im Azure-Portal oder in der CLI zu „Gelöschte Schlüssel verwalten“.
3. Wählen Sie den gelöschten Schlüssel aus der Liste der vorläufig gelöschten Elemente aus.
4. Klicken Sie **Wiederherstellen**, um den Schlüssel wiederherzustellen.

+++

+++Wenn die Berechtigungen für die Multi-Mandanten-App entfernt oder geändert wurden

1. Stellen Sie die richtigen Berechtigungen für die MultiMandant-App wieder her.
2. Stellen Sie sicher, dass die folgende Berechtigung erteilt wird: `Key Vault Crypto Service Encryption User`

+++

+++Wenn die MultiTenant-App gelöscht wurde

Dies ist eine grundlegende Veränderung. Sie müssen sich an Adobe wenden, um die Multi-Mandanten-App wiederherzustellen oder neu zu generieren.

+++

+++Wenn die Einstellungen für die Multi-Mandanten-App geändert wurden

1. Machen Sie die Änderungen an den Eigenschaften rückgängig, die mit der MultiTenant-App verknüpft sind.

+++

+++Wenn der Schlüsseltresor gelöscht wurde

1. Vergewissern Sie sich, dass die Soft-Delete-Funktion in Azure aktiviert ist.
2. Navigieren Sie im Portal oder in der CLI zu „Gelöschte Tresore verwalten“.
3. Wiederherstellen des gelöschten Tresors innerhalb Ihrer Aufbewahrungsfrist (7-90 Tage).
4. Wenn der Bereinigungsschutz deaktiviert ist, können Sie den Tresor möglicherweise dennoch wiederherstellen.

>[!NOTE]
>
>Wenn der Soft-Delete- oder Purge-Schutz nicht korrekt konfiguriert ist, kann der Schlüssel oder Tresor möglicherweise nicht wiederhergestellt werden.

+++

## Schlüsselzugriff fehlgeschlagen {#key-access-failure}

Dieser Warnhinweis zeigt an, dass Adobe Experience Platform aufgrund einer Zugriffsverweigerung auf Netzwerkebene oder einer konfigurationsbasierten Instanz nicht auf CMK zugegriffen hat.

>[!IMPORTANT]
>
>Dies wird als behebbarer Fehler behandelt. Daten **in diesem Fall** unter SLA gelöscht.

### Wenn er auftritt

Dieser Warnhinweis wird normalerweise ausgelöst, wenn die Key Vault-Firewall nicht so konfiguriert ist, dass sie den CMK-Zugriff von Adobe zulässt, oder wenn der identitätsbasierte Zugriff fehlschlägt.

### Mögliche Ursachen

- Die Key Vault-Firewall blockiert die statische IP von Adobe (`20.88.123.53`)
- Der Schlüssel existiert nicht mehr am erwarteten Speicherort
- Für die Adobe-Multi-Mandanten-App fehlen Berechtigungen
- Der Schlüsseltresor wurde gelöscht oder falsch konfiguriert
- Die Objekt-ID der Multi-Mandanten-App hat sich geändert

### Auflösung

+++Wenn der Schlüsseltresor oder der Schlüssel nicht mehr vorhanden ist

1. Stellen Sie sicher, dass der Schlüsseltresor und der Verschlüsselungsschlüssel noch vorhanden sind.
2. Wenn der Schlüssel gelöscht wurde, führen Sie die Wiederherstellungsschritte für Soft-Delete unter „Schlüsselzugriff deaktiviert“ aus.

+++

+++Wenn Berechtigungen für die Multi-Mandanten-App fehlen oder geändert werden

1. Vergewissern Sie sich, dass die Adobe-Multi-Mandant-App über die folgenden Berechtigungen verfügt:
   - `get`, `wrapKey` und `unwrapKey` auf dem -Schlüssel.
2. Überprüfen Sie, ob die Objekt-ID für die Multi-Mandanten-App korrekt ist. Wenn sie sich geändert hat, wenden Sie die Berechtigungen erneut an.

+++

+++Wenn die Firewall Adobe blockiert

1. Überprüfen Sie die Firewall-Regeln im Azure-Schlüsseltresor.
2. Stellen Sie sicher, dass sie den Zugriff über die statische IP-Adresse von Adobe zulassen: `20.88.123.53`.

>[!NOTE]
>
>Selbst mit den richtigen Berechtigungen verhindert eine blockierte IP den Schlüsselzugriff.

+++

## Benachrichtigung bei Warnhinweisen {#alert-notification}

Dieser Warnhinweis dient als allgemeine Benachrichtigung für CMK-Konfigurationen oder Zugriffsanomalien, die nicht mit einem bekannten Fehlertyp übereinstimmen.

>[!NOTE]
>
>Dieser Warnhinweis kann einen internen Fehler, eine neuartige Fehlkonfiguration oder eine unerwartete Bedingung widerspiegeln.

### Wenn er auftritt

Dieser Warnhinweis wird angezeigt, wenn Adobe CMK beim Schlüsselzugriff oder der Überwachung ein unbekanntes, nicht unterstütztes oder neuartiges Problem erkennt.

### Mögliche Ursachen

- Unerwartete Firewall-/Netzwerkbedingungen
- Schlüssel- oder Vault-Änderungen, die nicht von vordefinierten Warnhinweistypen abgedeckt werden
- Interne Adobe-Netzwerkstörungen
- Fehlerhafte Konfiguration, die Adobe noch nie gesehen hat

### Auflösung

+++Wenn die Ursache unbekannt oder mehrdeutig ist

1. Überprüfen Sie die Warnmeldung auf kontextuelle Details.
2. Überprüfen Sie die Firewall-, Vault- und Schlüsseleinstellungen auf die letzten Änderungen.
3. Wenn keine eindeutige Ursache gefunden wird, wenden Sie sich an den Adobe-Support.
4. Überwachen Sie Protokolle und Systemverhalten, um Muster zu identifizieren.

+++

## Nächste Schritte

Informationen zum Auslösen von Warnhinweisen und zum Konfigurieren der IP-Zulassungsauflistung für [!DNL Azure] CMK finden Sie im Handbuch [Konfigurieren von Warnhinweisen und IP-Zulassungsliste für Azure CMK](./azure/alerts-and-ip-access.md) .
