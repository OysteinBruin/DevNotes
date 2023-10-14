

Setting environment variable to enable access to build worker:
 - Option 1: set env var on `appveyor.yml` under `environment` section: `APPVEYOR_RDP_PASSWORD: <your password>`
 - Option 2 (preferred): set env var on project setting on www.appveyor.com: Settings->Environment-> Add variable

## Accessing Windows build worker via Remote Desktop (RDP)

Set RDP password in `APPVEYOR_RDP_PASSWORD` environment variable 
V
Add the following to your appveyor.yml file at the place where RDP access should be enabled::
```yml
init:
  - ps: iex ((new-object net.webclient).DownloadString('https://raw.githubusercontent.com/appveyor/ci/master/scripts/enable-rdp.ps1'))
```

## Accessing Linux build worker via Secure Shell

Set public SSH key in `APPVEYOR_SSH_KEY` environment variable

Add the following to your appveyor.yml file at the place where RDP access should be enabled::
```yml
init:
  - ps: iex ((new-object net.webclient).DownloadString('https://raw.githubusercontent.com/appveyor/ci/master/scripts/enable-rdp.ps1'))
```


RDP session is limited by overall build time (60 min).

[source - Windows build worker](https://www.appveyor.com/docs/how-to/rdp-to-build-worker/) 
[source - Linux build worker](https://www.appveyor.com/docs/how-to/ssh-to-build-worker/)