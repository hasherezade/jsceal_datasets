# Sample:

MD5 = `e27ae65977287bdfb7b0e15fd3603f85`

SHA256 = [`b73c3d732bb6bff8b9088cc0dcbadb35eea0802056324f1b6295cb9277c62755`](https://www.virustotal.com/gui/file/b73c3d732bb6bff8b9088cc0dcbadb35eea0802056324f1b6295cb9277c62755)

# Benchmark

| Model   |      Functions     | Time |Mode|
|----------|:-------------:|------:|------:|
| gpt-5.4-mini (temperature=0) |  220/224 | 0.54m | basic, bulk |
| claude-sonnet-4-6 |  223/224 | 1.59m | basic, bulk |
| gpt-5.6-terra (temperature=1) |  223/224| 1.56m | basic, bulk |
| claude-sonnet-5 |  223/224| 1.08m | basic, bulk |
| gpt-5.4-mini (temperature=0)|  21523/21915 | 34.84m | greedy, bulk |
| claude-sonnet-4-6 |  21878/21915| 132.51m (2h 12m)| greedy, bulk |
| gpt-5.6-terra (temperature=1) |  21415/21915| 103.06m (1h 43m) | greedy, bulk |
| claude-sonnet-5 |  21595/21915 | 79.00m (1h 19m) | greedy, bulk |

