Counting every DS↔Process arrow from the DFD:

| Process | DS→P (Read) | P→DS (Write) | Subtotal |
|---|---|---|---|
| P1.0 | 3 | 2 | **5** |
| P2.0 | 6 | 5 | **11** |
| P3.0 | 4 | 4 (incl. 3 read-only) | **10** |
| P4.0 | 11 | 9 | **20** |
| P5.0 | 14 | 11 | **25** |
| P6.0 | 6 | 3 | **9** |
| P7.0 | 6 | 2 | **8** |
| P8.0 | 7 | 2 | **9** |
| **Total** | **57** | **38** | **97** |

**97 total DS↔Process connectors.**

P4.0 and P5.0 dominate because they touch the most stores — P4.0 owns the entire task/rubric stack (DS12–DS16, DS23–DS26), and P5.0 owns the quiz/assessment stack (DS17–DS27) plus shares rubrics with P4.0. These two processes alone account for **45 of 97** connectors (46%).