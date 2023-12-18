laion-768-5m-ip

index build time:
- pgvectors: 38:05
- pgvector: 3:29:00

filter:

| option | probability | precision | rps    | note   | file                                                     |
| ------ | ----------- | --------- | ------ | ------ | -------------------------------------------------------- |
| rust   | 0.5         | 97.22%    | 382.08 |        | [rust-0.5-filter.json](rust-0.5-filter.json)             |
| rust   | 0.1         | 86.24%    | 366.17 |        | [rust-0.1-filter.json](rust-0.1-filter.json)             |
| rust   | 0.01        | 9.96%     | 375.20 |        | [rust-0.01-filter.json](rust-0.01-filter.json)           |
| rust   | 0.01        | 86.68%    | 109.34 | k=1000 | [rust-0.01-filter-1000.json](rust-0.01-filter-1000.json) |

without filter:

| option | k   | precision | rps    | note | file                           |
| ------ | --- | --------- | ------ | ---- | ------------------------------ |
| rust   | 100 | 97.90%    | 248.89 |      | [rust-100.json](rust-100.json) |
| c      | 50  | 92.47%    | 644.35 |      | [c-50.json](c-50.json)         |
| c      | 100 | 95.41%    | 475.95 |      | [c-100.json](c-100.json)       |
| c      | 200 | 96.90%    | 307.75 |      | [c-200.json](c-200.json)       |
| c      | 500 | 97.94%    | 161.01 |      | [c-500.json](c-500.json)       |
