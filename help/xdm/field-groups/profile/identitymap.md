---
keywords: Experience Platform;Startseite;beliebte Themen;Schema;Schema;XDM;individuelles Profil;Felder;Schemas;Schemata;identityMap;identität zuordnen;Identität zuordnen;Schema-Design;map;Map;Vereinigungsschema;Vereinigung
title: Schemafeldgruppe für IdentityMap
description: Dieses Dokument bietet einen Überblick über die Klasse „XDM Individual Profile“.
exl-id: c9928e85-ef1e-4739-ba1d-80505a9e60c3
source-git-commit: 43b3b79a4d24fd92c7afbf9ca9c83b0cbf80e2c2
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 81%

---

# Schemafeldgruppe für [!UICONTROL IdentityMap] 

>[!NOTE]
>
>Die Namen mehrerer Schemafeldgruppen wurden geändert. Weitere Informationen finden Sie im Dokument zu den [Namensaktualisierungen für Feldgruppen](../name-updates.md).

[!UICONTROL IdentityMap] ist eine standardmäßige Schemafeldgruppe für die [[!DNL XDM Individual Profile] Klasse](../../classes/individual-profile.md). Die Feldergruppe stellt ein einzelnes Zuordnungsfeld bereit, das eine Reihe von Benutzeridentitäten enthält, die vom Namespace angegeben wurden.

![Ein Diagramm des [!UICONTROL IdentityMap] Schemafeldgruppe](../../images/field-groups/identitymap.png)

Siehe den Abschnitt zu Identitätszuordnungen in [Grundlagen der Schemakomposition](../../schema/composition.md#identityMap) für weitere Informationen zu ihrem Anwendungsfall, einschließlich der Vor- und Nachteile.

**Beispiel**

```JSON
{
    "identityMap":{
        "ECID":[
            {
                "id":"83238819066235616291057085344313877718",
                "authenticatedState":"ambiguous",
                "primary":true
            }
        ]
    }
}
```

Weiterführende Informationen zur Feldergruppe finden Sie im Abschnitt [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/identitymap.schema.json) im öffentlichen XDM-Repository.
