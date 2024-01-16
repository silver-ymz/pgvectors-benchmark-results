## pgvecto.rs benchmark

---

machine: [n2-standard-8](https://cloud.google.com/compute/docs/general-purpose-machines#n2_machine_types) (8 vCPUs, 32 GB memory)

### laion-768-5m-ip

index build time:
- pgvectors:
  - hnsw (default 5 segments): **38:05**
  - hnsw: **1:08:08**
  - hnsw + SQ: **1:48:00**
  - hnsw + PQ x4: **10:40:40**
  - hnsw + PQ x16: **6:23:17**
  - hnsw + PQ x64: **1:54:38**
  - hnsw + fp16: **48:22**
  - hnsw (filter): **1:47:07**
- pgvector: **3:29:00**

filter:

| probability | ef_search | precision | rps     | file                                                                     |
| ----------- | --------- | --------- | ------- | ------------------------------------------------------------------------ |
| rust        | -         | -         | -       | -                                                                        |
| 0.5         | 100       | 95.27%    | 1142.06 | [rust-0.5-filter.json](results/rust-0.5-filter.json)                     |
| 0.1         | 100       | 83.29%    | 1098.98 | [rust-0.1-filter.json](results/rust-0.1-filter.json)                     |
| 0.01        | 100       | 9.94%     | 1093.60 | [rust-0.01-filter.json](results/rust-0.01-filter.json)                   |
| 0.01        | 1000      | 85.31%    | 345.24  | [rust-0.01-filter-1000.json](results/rust-0.01-filter-1000.json)         |
| c           | -         | -         | -       | -                                                                        |
| 0.5         | 100       | 96.26%    | 465.36  | [c-0.5-filter.json](results/c-0.5-filter.json)                           |
| 0.1         | 100       | 84.94%    | 447.13  | [c-0.1-filter.json](results/c-0.1-filter.json)                           |
| 0.01        | 100       | 10.31%    | 405.02  | [c-0.01-filter.json](results/c-0.01-filter.json)                         |
| 0.01        | 1000      | 86.93%    | 77.17   | [c-0.01-filter-1000.json](results/c-0.01-filter-1000.json)               |
| 0.01 top100 | 1000      | 10.41%    | 77.04   | [c-0.01-filter-1000-top100.json](results/c-0.01-filter-1000-top100.json) |

filter with vbase:

| probability | ef_search | precision | rps     | file                                                                                     |
| ----------- | --------- | --------- | ------- | ---------------------------------------------------------------------------------------- |
| top10       | -         | -         | -       | -                                                                                        |
| 0.5         | 50        | 91.36%    | 1185.93 | [rust-0.5-filter-vbase-50.json](results/rust-0.5-filter-vbase-50.json)                   |
| 0.5         | 100       | 95.01%    | 1141.62 | [rust-0.5-filter-vbase.json](results/rust-0.5-filter-vbase.json)                         |
| 0.5         | 200       | 96.65%    | 1034.07 | [rust-0.5-filter-vbase-200.json](results/rust-0.5-filter-vbase-200.json)                 |
| 0.5         | 500       | 97.56%    | 764.91  | [rust-0.5-filter-vbase-500.json](results/rust-0.5-filter-vbase-500.json)                 |
| 0.1         | 50        | 90.25%    | 818.20  | [rust-0.1-filter-vbase-50.json](results/rust-0.1-filter-vbase-50.json)                   |
| 0.1         | 100       | 91.60%    | 852.64  | [rust-0.1-filter-vbase.json](results/rust-0.1-filter-vbase.json)                         |
| 0.1         | 200       | 94.92%    | 777.98  | [rust-0.1-filter-vbase-200.json](results/rust-0.1-filter-vbase-200.json)                 |
| 0.1         | 500       | 97.15%    | 652.29  | [rust-0.1-filter-vbase-500.json](results/rust-0.1-filter-vbase-500.json)                 |
| 0.01        | 50        | 94.64%    | 163.04  | [rust-0.01-filter-vbase-50.json](results/rust-0.01-filter-vbase-50.json)                 |
| 0.01        | 100       | 94.64%    | 163.88  | [rust-0.01-filter-vbase.json](results/rust-0.01-filter-vbase.json)                       |
| 0.01        | 200       | 94.65%    | 166.94  | [rust-0.01-filter-vbase-200.json](results/rust-0.01-filter-vbase-200.json)               |
| 0.01        | 500       | 94.67%    | 174.34  | [rust-0.01-filter-vbase-500.json](results/rust-0.01-filter-vbase-500.json)               |
| top100      | -         | -         | -       | -                                                                                        |
| 0.01        | 50        | 95.51%    | 18.89   | [rust-0.01-filter-vbase-50-top100.json](results/rust-0.01-filter-vbase-50-top100.json)   |
| 0.01        | 100       | 95.52%    | 18.89   | [rust-0.01-filter-vbase-top100.json](results/rust-0.01-filter-vbase-top100.json)         |
| 0.01        | 200       | 95.52%    | 18.98   | [rust-0.01-filter-vbase-200-top100.json](results/rust-0.01-filter-vbase-200-top100.json) |
| 0.01        | 500       | 95.52%    | 19.13   | [rust-0.01-filter-vbase-500-top100.json](results/rust-0.01-filter-vbase-500-top100.json) |

without filter:

| option     | ef_search | precision | rps    | file                                                         |
| ---------- | --------- | --------- | ------ | ------------------------------------------------------------ |
|            | 50        | 92.49%    | 881.40 | [rust-50.json](results/rust-50.json)                         |
|            | 100       | 95.68%    | 809.21 | [rust-100.json](results/rust-100.json)                       |
|            | 200       | 97.09%    | 783.08 | [rust-200.json](results/rust-200.json)                       |
|            | 500       | 97.95%    | 594.50 | [rust-500.json](results/rust-500.json)                       |
| 5 segments | 100       | 97.90%    | 248.89 | [rust-100-5-segments.json](results/rust-100-5-segments.json) |
| SQ         | 50        | 90.66%    | 809.40 | [rust-50-sq.json](results/rust-50-sq.json)                   |
| SQ         | 100       | 93.60%    | 761.87 | [rust-100-sq.json](results/rust-100-sq.json)                 |
| SQ         | 200       | 95.04%    | 699.77 | [rust-200-sq.json](results/rust-200-sq.json)                 |
| SQ         | 500       | 95.75%    | 536.11 | [rust-500-sq.json](results/rust-500-sq.json)                 |
| PQ x4      | 50        | 91.04%    | 492.81 | [rust-50-pq-x4.json](results/rust-50-pq-x4.json)             |
| PQ x4      | 100       | 93.96%    | 354.34 | [rust-100-pq-x4.json](results/rust-100-pq-x4.json)           |
| PQ x4      | 200       | 95.27%    | 236.62 | [rust-200-pq-x4.json](results/rust-200-pq-x4.json)           |
| PQ x4      | 500       | 96.02%    | 129.32 | [rust-500-pq-x4.json](results/rust-500-pq-x4.json)           |
| PQ x16     | 50        | 64.52%    | 853.45 | [rust-50-pq-x16.json](results/rust-50-pq-x16.json)           |
| PQ x16     | 100       | 67.13%    | 684.01 | [rust-100-pq-x16.json](results/rust-100-pq-x16.json)         |
| PQ x16     | 200       | 68.53%    | 544.80 | [rust-200-pq-x16.json](results/rust-200-pq-x16.json)         |
| PQ x16     | 500       | 69.41%    | 340.56 | [rust-500-pq-x16.json](results/rust-500-pq-x16.json)         |
| PQ x64     | 50        | 14.81%    | 926.08 | [rust-50-pq-x64.json](results/rust-50-pq-x64.json)           |
| PQ x64     | 100       | 17.78%    | 865.11 | [rust-100-pq-x64.json](results/rust-100-pq-x64.json)         |
| PQ x64     | 200       | 19.90%    | 803.96 | [rust-200-pq-x64.json](results/rust-200-pq-x64.json)         |
| PQ x64     | 500       | 21.63%    | 619.43 | [rust-500-pq-x64.json](results/rust-500-pq-x64.json)         |
| fp16       | 50        | 92.72%    | 826.12 | [rust-50-fp16.json](results/rust-50-fp16.json)               |
| fp16       | 100       | 95.93%    | 817.83 | [rust-100-fp16.json](results/rust-100-fp16.json)             |
| fp16       | 200       | 97.40%    | 771.72 | [rust-200-fp16.json](results/rust-200-fp16.json)             |
| fp16       | 500       | 98.24%    | 636.76 | [rust-500-fp16.json](results/rust-500-fp16.json)             |
| c          | 50        | 92.47%    | 644.35 | [c-50.json](results/c-50.json)                               |
| c          | 100       | 95.41%    | 475.95 | [c-100.json](results/c-100.json)                             |
| c          | 200       | 96.90%    | 307.75 | [c-200.json](results/c-200.json)                             |
| c          | 500       | 97.94%    | 161.01 | [c-500.json](results/c-500.json)                             |

### 

---

machine: [c3-standard-8](https://cloud.google.com/compute/docs/general-purpose-machines#c3_machine_types) (8 vCPUs, 32 GB memory)

### laion-768-5m-ip

index build time:
- pgvectors:
  - hnsw: **54:00**
  - hnsw + SQ: **51:00**
  - hnsw + PQ x4: **5:49:00**
  - hnsw + PQ x16: **2:41:00**
  - hnsw + PQ x64: **1:37:00**
  - hnsw + fp16: **33:00**
- pgvector: **2:03:00**

| option | ef_search | precision | rps     | file                                                                     |
| ------ | --------- | --------- | ------- | ------------------------------------------------------------------------ |
|        | 50        | 92.64%    | 1351.58 | [rust-50-machine-2.json](results/rust-50-machine-2.json)                 |
|        | 100       | 95.75%    | 1211.65 | [rust-100-machine-2.json](results/rust-100-machine-2.json)               |
|        | 200       | 97.19%    | 1136.96 | [rust-200-machine-2.json](results/rust-200-machine-2.json)               |
|        | 500       | 98.01%    | 870.02  | [rust-500-machine-2.json](results/rust-500-machine-2.json)               |
| SQ     | 50        | 90.73%    | 1383.45 | [rust-50-sq-machine-2.json](results/rust-50-sq-machine-2.json)           |
| SQ     | 100       | 93.82%    | 1251.76 | [rust-100-sq-machine-2.json](results/rust-100-sq-machine-2.json)         |
| SQ     | 200       | 95.29%    | 1208.06 | [rust-200-sq-machine-2.json](results/rust-200-sq-machine-2.json)         |
| SQ     | 500       | 96.05%    | 942.06  | [rust-500-sq-machine-2.json](results/rust-500-sq-machine-2.json)         |
| PQ x4  | 50        | 90.85%    | 975.75  | [rust-50-pq-x4-machine-2.json](results/rust-50-pq-x4-machine-2.json)     |
| PQ x4  | 100       | 94.01%    | 705.53  | [rust-100-pq-x4-machine-2.json](results/rust-100-pq-x4-machine-2.json)   |
| PQ x4  | 200       | 95.46%    | 492.85  | [rust-200-pq-x4-machine-2.json](results/rust-200-pq-x4-machine-2.json)   |
| PQ x4  | 500       | 96.21%    | 270.84  | [rust-500-pq-x4-machine-2.json](results/rust-500-pq-x4-machine-2.json)   |
| PQ x16 | 50        | 64.82%    | 1284.55 | [rust-50-pq-x16-machine-2.json](results/rust-50-pq-x16-machine-2.json)   |
| PQ x16 | 100       | 67.16%    | 1099.84 | [rust-100-pq-x16-machine-2.json](results/rust-100-pq-x16-machine-2.json) |
| PQ x16 | 200       | 68.52%    | 895.42  | [rust-200-pq-x16-machine-2.json](results/rust-200-pq-x16-machine-2.json) |
| PQ x16 | 500       | 69.28%    | 569.28  | [rust-500-pq-x16-machine-2.json](results/rust-500-pq-x16-machine-2.json) |
| PQ x64 | 50        | 14.68%    | 1362.89 | [rust-50-pq-x64-machine-2.json](results/rust-50-pq-x64-machine-2.json)   |
| PQ x64 | 100       | 17.44%    | 1255.63 | [rust-100-pq-x64-machine-2.json](results/rust-100-pq-x64-machine-2.json) |
| PQ x64 | 200       | 19.68%    | 1168.35 | [rust-200-pq-x64-machine-2.json](results/rust-200-pq-x64-machine-2.json) |
| PQ x64 | 500       | 21.37%    | 960.10  | [rust-500-pq-x64-machine-2.json](results/rust-500-pq-x64-machine-2.json) |
| fp16   | 50        | 91.34%    | 1405.93 | [rust-50-fp16-machine-2.json](results/rust-50-fp16-machine-2.json)       |
| fp16   | 100       | 94.68%    | 1267.52 | [rust-100-fp16-machine-2.json](results/rust-100-fp16-machine-2.json)     |
| fp16   | 200       | 96.21%    | 1186.97 | [rust-200-fp16-machine-2.json](results/rust-200-fp16-machine-2.json)     |
| fp16   | 500       | 96.95%    | 1012.19 | [rust-500-fp16-machine-2.json](results/rust-500-fp16-machine-2.json)     |
| c      | 50        | 92.50%    | 1003.63 | [c-50-machine-2.json](results/c-50-machine-2.json)                       |
| c      | 100       | 95.49%    | 728.88  | [c-100-machine-2.json](results/c-100-machine-2.json)                     |
| c      | 200       | 97.06%    | 496.19  | [c-200-machine-2.json](results/c-200-machine-2.json)                     |
| c      | 500       | 97.95%    | 255.55  | [c-500-machine-2.json](results/c-500-machine-2.json)                     |

### dbpedia-openai-1M-1536-angular

index build time:
- pgvectors: **16:51**
- pgvector: **22:45**

m=36, ef_construction=128

| ef_search | precision | rps     | file                                               |
| --------- | --------- | ------- | -------------------------------------------------- |
| rust      | -         | -       | -                                                  |
| 10        | 78.69%    | 1058.68 | [rust-openai-10.json](results/rust-openai-10.json) |
| 32        | 93.48%    | 1011.49 | [rust-openai-32.json](results/rust-openai-32.json) |
| 40        | 94.78%    | 1001.29 | [rust-openai-40.json](results/rust-openai-40.json) |
| c         | -         | -       | -                                                  |
| 10        | 87.50%    | 956.61  | [c-openai-10.json.json](results/c-openai-10.json)  |
| 32        | 95.72%    | 718.88  | [c-openai-32.json.json](results/c-openai-32.json)  |
| 40        | 96.50%    | 654.01  | [c-openai-40.json.json](results/c-openai-40.json)  |