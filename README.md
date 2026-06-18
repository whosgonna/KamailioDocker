## Kamailio Dockerfile (kitchen sink version)

The `/build/Dockerfile` in this project will create a Debian 13 based image
with Kamailio 6.1 containing **all** modules in the packages from the official
Kamailio Debs repository (https://deb.kamailio.org/), as well as `sngrep`,
`kamcli`, and `sipexer`.
