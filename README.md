# Telofy MCP Server

**[Telofy](https://telofy.de) ist ein KI-Telefonassistent für kleine Betriebe in Deutschland.** Telofy nimmt jeden Anruf an, führt das Gespräch, bucht Termine, nimmt Bestellungen auf und legt den fertigen Vorgang ins Kundenportal.

Über diesen MCP-Server lesen KI-Assistenten wie Claude, ChatGPT oder Cursor die Daten Ihres Telofy-Kontos direkt: Anrufe, erfasste Vorgänge und gebuchte Termine. So fragen Sie Ihren Assistenten einfach: *„Welche Termine hat Telofy heute gebucht?“* oder *„Fass mir die Anrufe von gestern zusammen.“*

- Remote-Server, nichts zu installieren: `https://api.telofy.app/mcp` (Streamable HTTP)
- Nur lesend, Zugriff ausschließlich auf das eigene Konto
- Verarbeitung in der EU, keine Tonaufzeichnungen

## Werkzeuge

| Werkzeug | Was es liefert |
|---|---|
| `list_calls` | Anrufe des Kontos, neueste zuerst (Zeit, Nummer, Dauer, Status, Ergebnis) |
| `list_outcomes` | Erfasste Vorgänge: Leads, Tickets, Termine, Auskünfte |
| `list_appointments` | Von Telofy gebuchte oder vorgemerkte Termine |

Alle Werkzeuge nehmen optional `page` (ab 1) und `limit` (1 bis 100, Standard 50).

## Einrichtung

1. Im [Telofy-Kundenportal](https://telofy.app) unter **Integrationen** einen API-Schlüssel anlegen (beginnt mit `tlfy_`).
2. Den Server in Ihrem KI-Werkzeug eintragen:

**Claude Code**

```bash
claude mcp add --transport http telofy https://api.telofy.app/mcp --header "Authorization: Bearer tlfy_IhrSchluessel"
```

**Claude Desktop, Cursor und andere Clients** (`mcpServers`-Konfiguration)

```json
{
  "mcpServers": {
    "telofy": {
      "url": "https://api.telofy.app/mcp",
      "headers": { "Authorization": "Bearer tlfy_IhrSchluessel" }
    }
  }
}
```

Pro Schlüssel sind bis zu 60 Anfragen pro Minute möglich. Ungültige oder widerrufene Schlüssel liefern eine saubere Fehlermeldung statt Daten.

## Über Telofy

Telofy ist der digitale Empfang für Praxen, Handwerk, Gastronomie, Kanzleien und viele weitere Betriebe: Anrufe annehmen, Termine buchen und umbuchen, Bestellungen direkt auf den Küchendrucker, Weiterleitung nach eigenen Regeln, Anbindung an über 8.000 Programme über Zapier, Make und n8n. DSGVO-konform, ab 79 € im Monat, monatlich kündbar.

Mehr auf **[telofy.de](https://telofy.de)** · [Was ist ein KI-Telefonassistent?](https://telofy.de/wissen/was-ist-ein-ki-telefonassistent) · [Preise](https://telofy.de/preise)

---

## English

**[Telofy](https://telofy.de) is an AI phone receptionist for small businesses in Germany.** It answers every call, books appointments, takes orders and files a finished summary in the customer portal.

This remote MCP server (`https://api.telofy.app/mcp`, Streamable HTTP) lets AI assistants read your Telofy account: `list_calls`, `list_outcomes` (leads, tickets, appointments, info requests) and `list_appointments`. Read-only, scoped to your own account, processed in the EU.

Create an API key (`tlfy_…`) in the [Telofy portal](https://telofy.app) under *Integrations* and send it as `Authorization: Bearer <key>`.
