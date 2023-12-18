laion-768-5m-ip

index build time:
- pgvectors: 38:05
- pgvector: 3:29:00

| option | probability | precision | rps    |
| ------ | ----------- | --------- | ------ |
| rust   | 0.5         | 97.22%    | 382.08 |
| rust   | 0.1         | 86.24%    | 366.17 |
| rust   | 0.01        | 9.96%     | 375.20 |
| rust   | 0.01        | 86.68%    | 109.34 | k 1000 |
| rust   | no          | 97.90%    | 248.89 |
| c      | no          | 95.41%    | 32.96  |