## pgvecto.rs benchmark

### laion-768-5m-ip

index build time:
- pgvectors:
  - hnsw (default 5 segments): 38:05
  - hnsw : 
  - hnsw + SQ: 1:48:00
  - hnsw + PQ x4 : 10:40:40
- pgvector: 3:29:00

filter:

| option | probability | precision | rps    | note   | file                                                     |
| ------ | ----------- | --------- | ------ | ------ | -------------------------------------------------------- |
| rust   | 0.5         | 97.22%    | 382.08 |        | [rust-0.5-filter.json](rust-0.5-filter.json)             |
| rust   | 0.1         | 86.24%    | 366.17 |        | [rust-0.1-filter.json](rust-0.1-filter.json)             |
| rust   | 0.01        | 9.96%     | 375.20 |        | [rust-0.01-filter.json](rust-0.01-filter.json)           |
| rust   | 0.01        | 86.68%    | 109.34 | k=1000 | [rust-0.01-filter-1000.json](rust-0.01-filter-1000.json) |

without filter:

| option | k   | precision | rps    | note       | file                                                 |
| ------ | --- | --------- | ------ | ---------- | ---------------------------------------------------- |
| flat   | 50  | 92.49%    | 881.40 |            | [rust-50.json](rust-50.json)                         |
| flat   | 100 | 95.68%    | 809.21 |            | [rust-100.json](rust-100.json)                       |
| flat   | 200 | 97.09%    | 783.08 |            | [rust-200.json](rust-200.json)                       |
| flat   | 500 | 97.95%    | 594.50 |            | [rust-500.json](rust-500.json)                       |
| flat   | 100 | 97.90%    | 248.89 | 5 segments | [rust-100-5-segments.json](rust-100-5-segments.json) |
| SQ     | 50  | 90.66%    | 809.40 |            | [rust-50-sq.json](rust-50-sq.json)                   |
| SQ     | 100 | 93.60%    | 761.87 |            | [rust-100-sq.json](rust-100-sq.json)                 |
| SQ     | 200 | 95.04%    | 699.77 |            | [rust-200-sq.json](rust-200-sq.json)                 |
| SQ     | 500 | 95.75%    | 536.11 |            | [rust-500-sq.json](rust-500-sq.json)                 |
| PQ x4  | 50  | 91.04%    | 492.81 |            | [rust-50-pq-x4.json](rust-50-pq-x4.json)             |
| PQ x4  | 100 | 93.96%    | 354.34 |            | [rust-100-pq-x4.json](rust-100-pq-x4.json)           |
| PQ x4  | 200 | 95.27%    | 236.62 |            | [rust-200-pq-x4.json](rust-200-pq-x4.json)           |
| PQ x4  | 500 | 96.02%    | 129.32 |            | [rust-500-pq-x4.json](rust-500-pq-x4.json)           |
| c      | 50  | 92.47%    | 644.35 |            | [c-50.json](c-50.json)                               |
| c      | 100 | 95.41%    | 475.95 |            | [c-100.json](c-100.json)                             |
| c      | 200 | 96.90%    | 307.75 |            | [c-200.json](c-200.json)                             |
| c      | 500 | 97.94%    | 161.01 |            | [c-500.json](c-500.json)                             |
