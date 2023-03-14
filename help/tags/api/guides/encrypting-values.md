---
title: Verschlüsseln von Werten
description: Hier erfahren Sie, wie Sie bei Verwendung der Reactor-API sensible Werte verschlüsseln können.
exl-id: d89e7f43-3bdb-40a5-a302-bad6fd1f4596
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 100%

---

# Verschlüsseln von Werten

Bei der Verwendung von Tags in Adobe Experience Platform erfordern einige Workflows die Bereitstellung sensibler Werte (z. B. das Angeben eines privaten Schlüssels bei der Bereitstellung von Bibliotheken an Umgebungen über Hosts). Die Vertraulichkeit dieser Zugangsdaten erfordert
sichere Übertragung und Speicherung.

In diesem Dokument wird beschrieben, wie vertrauliche Werte mit [GnuPG-Verschlüsselung](https://www.gnupg.org/gph/en/manual/x110.html) (auch als GPG bezeichnet) verschlüsselt werden können, sodass nur das Tag-System sie lesen kann.

## Abrufen des öffentlichen GPG-Schlüssels und der Prüfsumme

Nachdem Sie die neueste Version von GPG [heruntergeladen](https://gnupg.org/download/) und installiert haben, müssen Sie den öffentlichen GPG-Schlüssel für die Produktionsumgebung der Tags abrufen:

* [GPG-Schlüssel](https://github.com/adobe/reactor-developer-docs/blob/master/files/launch%40adobe.com_pub.gpg)
* [Prüfsumme](https://github.com/adobe/reactor-developer-docs/blob/master/files/launch%40adobe.com_pub.gpg.sum)

## Importieren des Schlüssels in Ihren Schlüsselbund

Wenn Sie den Schlüssel auf Ihrem Computer gespeichert haben, besteht der nächste Schritt darin, ihn zu Ihrem GPG-Schlüsselbund hinzuzufügen.

**Syntax**

```shell
gpg --import {KEY_NAME}
```

| Parameter | Beschreibung |
| --- | --- |
| `{KEY_NAME}` | Der Name der öffentlichen Schlüsseldatei. |

{style="table-layout:auto"}

**Beispiel**

```shell
gpg --import launch@adobe.com_pub.gpg
```

## Verschlüsseln von Werten

Nachdem Sie den Schlüssel zu Ihrem Schlüsselbund hinzugefügt haben, können Sie mit der Verschlüsselung von Werten mit dem Flag `--encrypt` beginnen. Das folgende Skript zeigt, wie dieser Befehl funktioniert:

```shell
echo -n 'Example value' | gpg --armor --encrypt -r "Tags Data Encryption <launch@adobe.com>"
```

Dieser Befehl kann wie folgt aufgeschlüsselt werden:

* Die Eingabe wird dem Befehl `gpg` bereitgestellt.
* `--armor` erstellt eine ASCII-armierte Ausgabe statt einer binären. Dies vereinfacht die Übertragung des Wertes über JSON.
* `--encrypt` weist GPG an, die Daten zu verschlüsseln.
* `-r` legt den Empfänger für die Daten fest. Nur der Empfänger (der Inhaber des privaten Schlüssels, der dem öffentlichen Schlüssel entspricht) kann die Daten entschlüsseln. Der Empfängername des gewünschten Schlüssels kann durch die Überprüfung der Ausgabe von `gpg --list-keys` gefunden werden.

Der obige Befehl verwendet den öffentlichen Schlüssel für `Tags Data Encryption <launch@adobe.com>`, um den Wert `Example value` im ASCII-armierten Format zu verschlüsseln.

Die Ausgabe des Befehls würde in etwa wie folgt aussehen:

```shell
-----BEGIN PGP MESSAGE-----

hQIMAxJHCI6fydT/ARAAwQ0Y0k7eSAbd0T9seoaWX75G70O2gxAF20KY5FWiZ9/m
/RkgJwhJusZyEdazC/CmAdfXi9bsVxQT0i06ErUxXfQF0VtweRlcyRBsxzLz6Hr+
BpYGnq+cCCzGAT73Gg1CM4UWmaPKLLyWKGkXtDBAqVBRAIQT/8JhnkbyWIohHkWV
I/Uf7NrPXuaSmrqZ1SZQgwjIM3qNMR02qtqg59dncKoCQBji8Oeb8lqRLskRT0Jq
gVgbJYwSe2n6KpJkELJ6QtF9lCRl1+yU4mvM4jBHgkM1+vb1WmbFRIR40dDpg85N
0J9hVj4bg//eLRDfAdEC9kgq9Atph0WqJ5EpehdS7yVO9lO8mpbpqZ4BCGjTi/VS
isEPr6eZ2mxRbk8f9Z4csRZnkErY8ep5+cqC5CZVdmguWvC9PKzXqEsPFd0PSYk3
Qp3UIW2/JMf16E5CKmntm+gKdl6kggZOOvNQuyJYa9yNbzySPerHXsknTOxV+QP/
WXwrAL52g5+gpMib7Ve/KBz5/OViDhDqkmHzlGad73W74d+CYjf0AnuXuWRRlUMT
s8ORw1eplInldhXk2mgkGPZS/gWDs3zpKUu4GSO9AaeWldynLG/Bgh78XhumQ58h
ekGD+p3PyyvxjfS5G/wf9HQZ085+mnjpKFa7fuFBQPbg4WpBadhWrhobthC+hN3S
SAE9yWU11Y3xpoxqg4y7iYZ6rnX+qP2oUNYxC2/hdhsFbbZtUh4s51qaoLbe0iWB
OUoIPf4KxTaboHZOEy32ZBng5heVrn4i9w==
=jrfE
-----END PGP MESSAGE-----
```

Diese Ausgabe kann nur von Systemen entschlüsselt werden, die über den privaten Schlüssel verfügen, der dem öffentlichen Schlüssel `Tags Data Encryption <launch@adobe.com>` entspricht.

Diese Ausgabe ist der Wert, der bereitgestellt werden muss, wenn Daten an die Reactor-API gesendet werden. Das System speichert diese verschlüsselte Ausgabe und entschlüsselt sie vorübergehend nach Bedarf. Beispielsweise entschlüsselt das System Host-Anmeldeinformationen lange genug, um eine Verbindung zum Server herzustellen, und entfernt dann sofort alle Spuren des entschlüsselten Werts.

>[!NOTE]
>
>Das Format des armierten, verschlüsselten Werts ist wichtig. Stellen Sie sicher, dass Zeilenumbrüche in dem in der Anfrage angegebenen Wert ordnungsgemäß umbrochen sind.
