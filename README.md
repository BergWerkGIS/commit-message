commit-message
==============

experimenting with commit message parsing, geared towards [publish binary] on AppVeyor

parsing commit messages in batch files it cumbersome.
parsing in Powershell is easy.
unfortunately getting the result back from PS is not:

* CMD, has set of env vars
  * --> PS, new process, but inherits env vars from CMD, set env var base on analysis of commit message
* CMD <-- env vars from PS are lost, because the process has terminated

### solution, kind of hackish:
setting env var in CMD from output of PS:


```
for /F "tokens=1 usebackq" %%i in (`powershell .\parse-commit-message.ps1`) DO SET PUBLISH=%%i

```


AppVeyor:

[![Build status](https://ci.appveyor.com/api/projects/status/60mllt5lyohrdaaq?svg=true)](https://ci.appveyor.com/project/BergWerkGIS/commit-message)
