# NiagaraExportBql2json 🔄

[![Niagara 4.14+](https://img.shields.io/badge/Niagara-4.14%2B-blue)](https://www.tridium.com)
[![License: MIT](https://img.shields.io/badge/License-MIT-green)](LICENSE)
[![Contact](https://img.shields.io/badge/Contact-WhatsApp-brightgreen)](https://wa.me/8613801909968)

> **Convert any Niagara BQL query result to JSON — points, alarms, history, anything BQL can reach.**

---

## What Is It?

A Niagara 4 module that executes BQL queries and returns the results as clean JSON. If you can write a BQL query for it, this module can convert it to JSON — no middleware, no scripting, no extra hardware.

### What You Can Query

| Data | BQL Source | Example |
|------|-----------|---------|
| **Point values & status** | `control:ControlPoint` | Current temperature, humidity, pressure, status flags |
| **All alarms** | `alarm:Alarm` | All active/recent alarms across the station |
| **Alarms by category** | `alarm:Alarm where alarmClass = 'Red_High'` | Critical vs warning vs info alarms |
| **Alarms by time range** | `alarm:Alarm where timestamp > '2026-03-24T00:00:00.000+08:00'` | Yesterday's alarms, last hour, etc. |
| **Alarm acknowledgment status** | With `ackState` field | Who acknowledged what, when |
| **Historical data** | `history:HistoryRecord` | Trend data over any time period |
| **Component properties** | `baja:Component` | Any slot/property on any component |

> **In short: if BQL can query it, this module can JSON-ify it.**

---

## Why JSON?

Raw Niagara data locked in Workbench is useful — but JSON opens the door to everything else:

| Use Case | How It Works |
|----------|-------------|
| 🤖 **AI data analysis** | Feed JSON to DeepSeek, OpenAI, or your own ML models |
| 🌐 **Custom web UI** | Build beautiful dashboards with any JS framework (React, Vue, etc.) |
| 📊 **Custom reports** | Format JSON into PDF/Excel with your reporting tool |
| 📡 **Data export** | Send JSON via MQTT, REST, or save to file — see companion modules below |
| 🔄 **Third-party integration** | Any system that speaks JSON can now consume Niagara data |

### Companion Modules

Pair with other Gline modules for a complete data pipeline:

```
Niagara Station → BQL Query → JSON → StringToFile (save to station file)
                                    → FTP Client (upload to remote server)
                                    → SFTP Client (secure file transfer)
                                    → MQTT Client (publish to broker)
                                    → REST API (serve via HTTP)
```

---

## Quick Start

```bash
# 1. Install gline.pem certificate into your station trust store

# 2. Add glineExportJson-rt.jar to your modules/ directory

# 3. Restart station

# 4. Drag the ExportJson component into your program

# 5. Configure your BQL query — for example:
#    station:|slot:/Drivers/yourNetwork/points|bql:select name,out.value,out.status from control:ControlPoint

# 6. Trigger → JSON output written to your configured destination
```

---

## BQL Examples

### All live point values under a folder

```sql
station:|slot:/Drivers/MQTT/Liyu/points/BA_7F|bql:select name,slotPath,type,out.value as 'value',out.status as 'status' from control:ControlPoint
```

### Red-high alarms in a time range

```sql
alarm:|bql:select alarmData.sourceName as 'sourceName', source as 'source', timestamp as 'timestamp', normalTime as 'normalTimestamp', sourceState as 'state', alarmClass as 'alarmClass', alarmData.msgText as 'msgText', ackState as 'ackState', uuid as 'uuid' where timestamp > '2026-03-24T00:00:00.000+08:00' and alarmClass = 'Red_High' order by timestamp desc
```

### History data (last 24 hours)

```sql
history:|slot:/History/yourHistoryName|bql:select * where timestamp > '2026-03-24T00:00:00.000+08:00' order by timestamp
```

### Alarms by category

```sql
alarm:|bql:select ... where alarmClass = 'Red_High'
alarm:|bql:select ... where alarmClass = 'Yellow_Med'
alarm:|bql:select ... where alarmClass = 'Blue_Low'
```

---

## Output Format

```json
[
  {
    "name": "Temperature",
    "slotPath": "/Drivers/BACnet/points/Temperature",
    "type": "NumericPoint",
    "value": 23.5,
    "status": "ok"
  },
  {
    "name": "Humidity",
    "slotPath": "/Drivers/BACnet/points/Humidity",
    "type": "NumericPoint",
    "value": 55.2,
    "status": "ok"
  }
]
```

---

## Requirements

| Component | Requirement |
|-----------|-------------|
| **Niagara** | 4.14 or later |
| **JAR signing** | Requires gline.pem certificate |
| **BQL knowledge** | Standard Niagara BQL syntax |

---

## Support & Contact

Need help writing BQL queries? Want a custom JSON format? We build data pipelines for Niagara.

- **Email**: [jason.zhang@gline-net.com](mailto:jason.zhang@gline-net.com)
- **WhatsApp**: [+86 138 0199 0968](https://wa.me/8613801909968)

**Shanghai Gline Net Co., Ltd.** — Your Partner in Smarter Automation

---

© 2026 Shanghai Gline Net Co., Ltd. All rights reserved.
