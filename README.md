# NiagaraExportBql2json 🆓🔄

[![Niagara 4.14+](https://img.shields.io/badge/Niagara-4.14%2B-blue)](https://www.tridium.com)
[![Free to use](https://img.shields.io/badge/Free_to_use-brightgreen)](LICENSE)
[![License: MIT](https://img.shields.io/badge/License-MIT-green)](LICENSE)

> **🆓 Free • Convert any Niagara BQL query result to JSON — points, alarms, history. Anything BQL can reach.**
This module can convert Niagara BQL query results into JSON format output, facilitating the display of Niagara point data on standard HTML pages. The relevant usage instructions are included within the module.
<img width="2065" height="337" alt="image" src="https://github.com/user-attachments/assets/0b58eaa8-36f0-452e-9938-e92c9eb52663" />

The standard json format is as following sample:
<img width="994" height="297" alt="image" src="https://github.com/user-attachments/assets/f78d4d34-5130-4e62-af09-31c5e0d1c952" />

Here is red-high alarm bql to json:
alarm:|bql:select alarmData.sourceName as 'sourceName', source as 'source', timestamp as 'timestamp', normalTime as 'normalTimestamp', sourceState as 'state', alarmClass as 'alarmClass', alarmData.msgText as 'msgText', ackState as 'ackState', uuid as 'uuid' where timestamp > '2026-03-24T00:00:00.000+08:00' and alarmClass = 'Red_High' order by timestamp desc
<img width="2073" height="336" alt="image" src="https://github.com/user-attachments/assets/028fabf1-87f7-4eb3-9ade-f61c7db4a719" />

---

## Support & Contact

- **Email**: [jason.zhang@gline-net.com](mailto:jason.zhang@gline-net.com)
- **WhatsApp**: [+86 138 0199 0968](https://wa.me/8613801909968)
- **Web**: [www.glineweb.com](https://www.glineweb.com)
- **Tools**: [jason912.github.io](https://jason912.github.io) — Niagara module catalog

**Shanghai Gline Net Co., Ltd.** — Your Partner in Smarter Automation

---

© 2026 Shanghai Gline Net Co., Ltd. All rights reserved.