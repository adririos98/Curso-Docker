## Crear YAML
```yaml
# Descarga la imagen de Ubuntu 22.04
FROM ubuntu:22.04
# Mantenedor del contenedor
MAINTAINER AdriánHernándezRios adrian.sevilla@dockercurso.com
# Definir ambiente de entorno
ENV PRUEBA1 datos1
ENV PRUEBA2 datos2
ENV PRUEBA3 datos3
ENV PRUEBA4 datos4
# Instalar Git
RUN apt-get update && apt-get install -y \
        curl
# Indica los puertos TCP/IP los cuales se pueden accede a los servicios del contenedor
EXPOSE 80/tcp
EXPOSE 443/udp
EXPOSE 53
```

## GENERAR IMAGEN
```shell

[root@anacoluto-win ~]# docker build --file Dockerfilelabs-AdrianRios -t pruebacursoadri:1.0 .
Sending build context to Docker daemon  1.275GB
Step 1/10 : FROM ubuntu:22.04
 ---> 27941809078c
Step 2/10 : MAINTAINER AdriánHernándezRios adrian.sevilla@dockercurso.com
 ---> Using cache
 ---> 277fcdbed95d
Step 3/10 : ENV PRUEBA1 datos1
 ---> Running in 9cf9ee63df9b
Removing intermediate container 9cf9ee63df9b
 ---> ee1444958ae5
Step 4/10 : ENV PRUEBA2 datos2
 ---> Running in 4741817aaf82
Removing intermediate container 4741817aaf82
 ---> b874de198fd3
Step 5/10 : ENV PRUEBA3 datos3
 ---> Running in 02ef81af8c50
Removing intermediate container 02ef81af8c50
 ---> 57740610bd76
Step 6/10 : ENV PRUEBA4 datos4
 ---> Running in 89f1b655d532
Removing intermediate container 89f1b655d532
 ---> 0d02b1e47b28
Step 7/10 : RUN apt-get update && apt-get install -y         curl
 ---> Running in 38319bc8e6bd
Get:1 http://archive.ubuntu.com/ubuntu jammy InRelease [270 kB]
Get:2 http://security.ubuntu.com/ubuntu jammy-security InRelease [110 kB]
Get:3 http://archive.ubuntu.com/ubuntu jammy-updates InRelease [114 kB]
Get:4 http://archive.ubuntu.com/ubuntu jammy-backports InRelease [99.8 kB]
Get:5 http://archive.ubuntu.com/ubuntu jammy/universe amd64 Packages [17.5 MB]
Get:6 http://security.ubuntu.com/ubuntu jammy-security/multiverse amd64 Packages [4644 B]
Get:7 http://security.ubuntu.com/ubuntu jammy-security/main amd64 Packages [303 kB]
Get:8 http://security.ubuntu.com/ubuntu jammy-security/universe amd64 Packages [119 kB]
Get:9 http://security.ubuntu.com/ubuntu jammy-security/restricted amd64 Packages [276 kB]
Get:10 http://archive.ubuntu.com/ubuntu jammy/main amd64 Packages [1792 kB]
Get:11 http://archive.ubuntu.com/ubuntu jammy/multiverse amd64 Packages [266 kB]
Get:12 http://archive.ubuntu.com/ubuntu jammy/restricted amd64 Packages [164 kB]
Get:13 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 Packages [602 kB]
Get:14 http://archive.ubuntu.com/ubuntu jammy-updates/universe amd64 Packages [243 kB]
Get:15 http://archive.ubuntu.com/ubuntu jammy-updates/multiverse amd64 Packages [7791 B]
Get:16 http://archive.ubuntu.com/ubuntu jammy-updates/restricted amd64 Packages [319 kB]
Get:17 http://archive.ubuntu.com/ubuntu jammy-backports/universe amd64 Packages [5814 B]
Fetched 22.2 MB in 16s (1418 kB/s)
Reading package lists...
Reading package lists...
Building dependency tree...
Reading state information...
The following additional packages will be installed:
  ca-certificates libbrotli1 libcurl4 libldap-2.5-0 libldap-common
  libnghttp2-14 libpsl5 librtmp1 libsasl2-2 libsasl2-modules
  libsasl2-modules-db libssh-4 openssl publicsuffix
Suggested packages:
  libsasl2-modules-gssapi-mit | libsasl2-modules-gssapi-heimdal
  libsasl2-modules-ldap libsasl2-modules-otp libsasl2-modules-sql
The following NEW packages will be installed:
  ca-certificates curl libbrotli1 libcurl4 libldap-2.5-0 libldap-common
  libnghttp2-14 libpsl5 librtmp1 libsasl2-2 libsasl2-modules
  libsasl2-modules-db libssh-4 openssl publicsuffix
0 upgraded, 15 newly installed, 0 to remove and 16 not upgraded.
Need to get 2970 kB of archives.
After this operation, 7063 kB of additional disk space will be used.
Get:1 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 openssl amd64 3.0.2-0ubuntu1.6 [1184 kB]
Get:2 http://archive.ubuntu.com/ubuntu jammy/main amd64 ca-certificates all 20211016 [148 kB]
Get:3 http://archive.ubuntu.com/ubuntu jammy/main amd64 libnghttp2-14 amd64 1.43.0-1build3 [76.3 kB]
Get:4 http://archive.ubuntu.com/ubuntu jammy/main amd64 libpsl5 amd64 0.21.0-1.2build2 [58.4 kB]
Get:5 http://archive.ubuntu.com/ubuntu jammy/main amd64 publicsuffix all 20211207.1025-1 [129 kB]
Get:6 http://archive.ubuntu.com/ubuntu jammy/main amd64 libbrotli1 amd64 1.0.9-2build6 [315 kB]
Get:7 http://archive.ubuntu.com/ubuntu jammy/main amd64 libsasl2-modules-db amd64 2.1.27+dfsg2-3ubuntu1 [20.8 kB]
Get:8 http://archive.ubuntu.com/ubuntu jammy/main amd64 libsasl2-2 amd64 2.1.27+dfsg2-3ubuntu1 [53.9 kB]
Get:9 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libldap-2.5-0 amd64 2.5.12+dfsg-0ubuntu0.22.04.1 [184 kB]
Get:10 http://archive.ubuntu.com/ubuntu jammy/main amd64 librtmp1 amd64 2.4+20151223.gitfa8646d.1-2build4 [58.2 kB]
Get:11 http://archive.ubuntu.com/ubuntu jammy/main amd64 libssh-4 amd64 0.9.6-2build1 [184 kB]
Get:12 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libcurl4 amd64 7.81.0-1ubuntu1.3 [290 kB]
Get:13 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 curl amd64 7.81.0-1ubuntu1.3 [194 kB]
Get:14 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libldap-common all 2.5.12+dfsg-0ubuntu0.22.04.1 [16.4 kB]
Get:15 http://archive.ubuntu.com/ubuntu jammy/main amd64 libsasl2-modules amd64 2.1.27+dfsg2-3ubuntu1 [57.5 kB]
debconf: delaying package configuration, since apt-utils is not installed
Fetched 2970 kB in 5s (569 kB/s)
Selecting previously unselected package openssl.
(Reading database ... 4395 files and directories currently installed.)
Preparing to unpack .../00-openssl_3.0.2-0ubuntu1.6_amd64.deb ...
Unpacking openssl (3.0.2-0ubuntu1.6) ...
Selecting previously unselected package ca-certificates.
Preparing to unpack .../01-ca-certificates_20211016_all.deb ...
Unpacking ca-certificates (20211016) ...
Selecting previously unselected package libnghttp2-14:amd64.
Preparing to unpack .../02-libnghttp2-14_1.43.0-1build3_amd64.deb ...
Unpacking libnghttp2-14:amd64 (1.43.0-1build3) ...
Selecting previously unselected package libpsl5:amd64.
Preparing to unpack .../03-libpsl5_0.21.0-1.2build2_amd64.deb ...
Unpacking libpsl5:amd64 (0.21.0-1.2build2) ...
Selecting previously unselected package publicsuffix.
Preparing to unpack .../04-publicsuffix_20211207.1025-1_all.deb ...
Unpacking publicsuffix (20211207.1025-1) ...
Selecting previously unselected package libbrotli1:amd64.
Preparing to unpack .../05-libbrotli1_1.0.9-2build6_amd64.deb ...
Unpacking libbrotli1:amd64 (1.0.9-2build6) ...
Selecting previously unselected package libsasl2-modules-db:amd64.
Preparing to unpack .../06-libsasl2-modules-db_2.1.27+dfsg2-3ubuntu1_amd64.deb ...
Unpacking libsasl2-modules-db:amd64 (2.1.27+dfsg2-3ubuntu1) ...
Selecting previously unselected package libsasl2-2:amd64.
Preparing to unpack .../07-libsasl2-2_2.1.27+dfsg2-3ubuntu1_amd64.deb ...
Unpacking libsasl2-2:amd64 (2.1.27+dfsg2-3ubuntu1) ...
Selecting previously unselected package libldap-2.5-0:amd64.
Preparing to unpack .../08-libldap-2.5-0_2.5.12+dfsg-0ubuntu0.22.04.1_amd64.deb ...
Unpacking libldap-2.5-0:amd64 (2.5.12+dfsg-0ubuntu0.22.04.1) ...
Selecting previously unselected package librtmp1:amd64.
Preparing to unpack .../09-librtmp1_2.4+20151223.gitfa8646d.1-2build4_amd64.deb ...
Unpacking librtmp1:amd64 (2.4+20151223.gitfa8646d.1-2build4) ...
Selecting previously unselected package libssh-4:amd64.
Preparing to unpack .../10-libssh-4_0.9.6-2build1_amd64.deb ...
Unpacking libssh-4:amd64 (0.9.6-2build1) ...
Selecting previously unselected package libcurl4:amd64.
Preparing to unpack .../11-libcurl4_7.81.0-1ubuntu1.3_amd64.deb ...
Unpacking libcurl4:amd64 (7.81.0-1ubuntu1.3) ...
Selecting previously unselected package curl.
Preparing to unpack .../12-curl_7.81.0-1ubuntu1.3_amd64.deb ...
Unpacking curl (7.81.0-1ubuntu1.3) ...
Selecting previously unselected package libldap-common.
Preparing to unpack .../13-libldap-common_2.5.12+dfsg-0ubuntu0.22.04.1_all.deb ...
Unpacking libldap-common (2.5.12+dfsg-0ubuntu0.22.04.1) ...
Selecting previously unselected package libsasl2-modules:amd64.
Preparing to unpack .../14-libsasl2-modules_2.1.27+dfsg2-3ubuntu1_amd64.deb ...
Unpacking libsasl2-modules:amd64 (2.1.27+dfsg2-3ubuntu1) ...
Setting up libpsl5:amd64 (0.21.0-1.2build2) ...
Setting up libbrotli1:amd64 (1.0.9-2build6) ...
Setting up libsasl2-modules:amd64 (2.1.27+dfsg2-3ubuntu1) ...
Setting up libnghttp2-14:amd64 (1.43.0-1build3) ...
Setting up libldap-common (2.5.12+dfsg-0ubuntu0.22.04.1) ...
Setting up libsasl2-modules-db:amd64 (2.1.27+dfsg2-3ubuntu1) ...
Setting up librtmp1:amd64 (2.4+20151223.gitfa8646d.1-2build4) ...
Setting up libsasl2-2:amd64 (2.1.27+dfsg2-3ubuntu1) ...
Setting up libssh-4:amd64 (0.9.6-2build1) ...
Setting up openssl (3.0.2-0ubuntu1.6) ...
Setting up publicsuffix (20211207.1025-1) ...
Setting up libldap-2.5-0:amd64 (2.5.12+dfsg-0ubuntu0.22.04.1) ...
Setting up ca-certificates (20211016) ...
debconf: unable to initialize frontend: Dialog
debconf: (TERM is not set, so the dialog frontend is not usable.)
debconf: falling back to frontend: Readline
debconf: unable to initialize frontend: Readline
debconf: (Can't locate Term/ReadLine.pm in @INC (you may need to install the Term::ReadLine module) (@INC contains: /etc/perl /usr/local/lib/x86_64-linux-gnu/perl/5.34.0 /usr/local/share/perl/5.34.0 /usr/lib/x86_64-linux-gnu/perl5/5.34 /usr/share/perl5 /usr/lib/x86_64-linux-gnu/perl-base /usr/lib/x86_64-linux-gnu/perl/5.34 /usr/share/perl/5.34 /usr/local/lib/site_perl) at /usr/share/perl5/Debconf/FrontEnd/Readline.pm line 7.)
debconf: falling back to frontend: Teletype
Updating certificates in /etc/ssl/certs...
127 added, 0 removed; done.
Setting up libcurl4:amd64 (7.81.0-1ubuntu1.3) ...
Setting up curl (7.81.0-1ubuntu1.3) ...
Processing triggers for libc-bin (2.35-0ubuntu3) ...
Processing triggers for ca-certificates (20211016) ...
Updating certificates in /etc/ssl/certs...
0 added, 0 removed; done.
Running hooks in /etc/ca-certificates/update.d...
done.
Removing intermediate container 38319bc8e6bd
 ---> 4c3eb328e61c
Step 8/10 : EXPOSE 80/tcp
 ---> Running in 7cb881992587
Removing intermediate container 7cb881992587
 ---> 5203f4ed2be7
Step 9/10 : EXPOSE 443/udp
 ---> Running in 4f6e62b29bbc
Removing intermediate container 4f6e62b29bbc
 ---> f987a10ec4f9
Step 10/10 : EXPOSE 53
 ---> Running in 4293f6f23668
Removing intermediate container 4293f6f23668
 ---> 33ba4405727c
Successfully built 33ba4405727c
Successfully tagged pruebacursoadri:1.0


```

## CREAR CONTENEDOR
```shell
[root@anacoluto-win ~]# docker run -dit pruebacursoadri:1.0
a9d38398d36ec95e2500ee8e751927c555852d424a57a2b44aa27162734599ee
[root@anacoluto-win ~]# docker ps
CONTAINER ID   IMAGE                 COMMAND   CREATED          STATUS          PORTS                     NAMES
a9d38398d36e   pruebacursoadri:1.0   "bash"    7 seconds ago    Up 4 seconds    53/tcp, 80/tcp, 443/udp   hungry_haibt
[root@anacoluto-win ~]# docker inspect a9d38398d36e
[
    {
        "Id": "a9d38398d36ec95e2500ee8e751927c555852d424a57a2b44aa27162734599ee",
        "Created": "2022-08-03T11:23:20.930724269Z",
        "Path": "bash",
        "Args": [],
        "State": {
            "Status": "running",
            "Running": true,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 7004,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2022-08-03T11:23:23.209711161Z",
            "FinishedAt": "0001-01-01T00:00:00Z"
        },
        "Image": "sha256:33ba4405727c6bdb00ef15cfbb3876b2f5eed36ce3a6de2cc16f3863996960ed",
        "ResolvConfPath": "/var/lib/docker/containers/a9d38398d36ec95e2500ee8e751927c555852d424a57a2b44aa27162734599ee/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/a9d38398d36ec95e2500ee8e751927c555852d424a57a2b44aa27162734599ee/hostname",
        "HostsPath": "/var/lib/docker/containers/a9d38398d36ec95e2500ee8e751927c555852d424a57a2b44aa27162734599ee/hosts",
        "LogPath": "/var/lib/docker/containers/a9d38398d36ec95e2500ee8e751927c555852d424a57a2b44aa27162734599ee/a9d38398d36ec95e2500ee8e751927c555852d424a57a2b44aa27162734599ee-json.log",
        "Name": "/hungry_haibt",
        "RestartCount": 0,
        "Driver": "overlay2",
        "Platform": "linux",
        "MountLabel": "",
        "ProcessLabel": "",
        "AppArmorProfile": "",
        "ExecIDs": null,
        "HostConfig": {
            "Binds": null,
            "ContainerIDFile": "",
            "LogConfig": {
                "Type": "json-file",
                "Config": {}
            },
            "NetworkMode": "default",
            "PortBindings": {},
            "RestartPolicy": {
                "Name": "no",
                "MaximumRetryCount": 0
            },
            "AutoRemove": false,
            "VolumeDriver": "",
            "VolumesFrom": null,
            "CapAdd": null,
            "CapDrop": null,
            "CgroupnsMode": "host",
            "Dns": [],
            "DnsOptions": [],
            "DnsSearch": [],
            "ExtraHosts": null,
            "GroupAdd": null,
            "IpcMode": "private",
            "Cgroup": "",
            "Links": null,
            "OomScoreAdj": 0,
            "PidMode": "",
            "Privileged": false,
            "PublishAllPorts": false,
            "ReadonlyRootfs": false,
            "SecurityOpt": null,
            "UTSMode": "",
            "UsernsMode": "",
            "ShmSize": 67108864,
            "Runtime": "runc",
            "ConsoleSize": [
                0,
                0
            ],
            "Isolation": "",
            "CpuShares": 0,
            "Memory": 0,
            "NanoCpus": 0,
            "CgroupParent": "",
            "BlkioWeight": 0,
            "BlkioWeightDevice": [],
            "BlkioDeviceReadBps": null,
            "BlkioDeviceWriteBps": null,
            "BlkioDeviceReadIOps": null,
            "BlkioDeviceWriteIOps": null,
            "CpuPeriod": 0,
            "CpuQuota": 0,
            "CpuRealtimePeriod": 0,
            "CpuRealtimeRuntime": 0,
            "CpusetCpus": "",
            "CpusetMems": "",
            "Devices": [],
            "DeviceCgroupRules": null,
            "DeviceRequests": null,
            "KernelMemory": 0,
            "KernelMemoryTCP": 0,
            "MemoryReservation": 0,
            "MemorySwap": 0,
            "MemorySwappiness": null,
            "OomKillDisable": false,
            "PidsLimit": null,
            "Ulimits": null,
            "CpuCount": 0,
            "CpuPercent": 0,
            "IOMaximumIOps": 0,
            "IOMaximumBandwidth": 0,
            "MaskedPaths": [
                "/proc/asound",
                "/proc/acpi",
                "/proc/kcore",
                "/proc/keys",
                "/proc/latency_stats",
                "/proc/timer_list",
                "/proc/timer_stats",
                "/proc/sched_debug",
                "/proc/scsi",
                "/sys/firmware"
            ],
            "ReadonlyPaths": [
                "/proc/bus",
                "/proc/fs",
                "/proc/irq",
                "/proc/sys",
                "/proc/sysrq-trigger"
            ]
        },
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/b0a3ce1071c9b3b20d81907c3c0b4076beac11037ec632a74b163568d295474b-init/diff:/var/lib/docker/overlay2/76673ab0f17706438df884c76cfca3f59ade90957a7a0bc0983655b9a7653252/diff:/var/lib/docker/overlay2/24d444d910470c91015ecdd977bef0bce00c42cca59abe611622a243b263d43d/diff",
                "MergedDir": "/var/lib/docker/overlay2/b0a3ce1071c9b3b20d81907c3c0b4076beac11037ec632a74b163568d295474b/merged",
                "UpperDir": "/var/lib/docker/overlay2/b0a3ce1071c9b3b20d81907c3c0b4076beac11037ec632a74b163568d295474b/diff",
                "WorkDir": "/var/lib/docker/overlay2/b0a3ce1071c9b3b20d81907c3c0b4076beac11037ec632a74b163568d295474b/work"
            },
            "Name": "overlay2"
        },
        "Mounts": [],
        "Config": {
            "Hostname": "a9d38398d36e",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "ExposedPorts": {
                "443/udp": {},
                "53/tcp": {},
                "80/tcp": {}
            },
            "Tty": true,
            "OpenStdin": true,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "PRUEBA1=datos1",
                "PRUEBA2=datos2",
                "PRUEBA3=datos3",
                "PRUEBA4=datos4"
            ],
            "Cmd": [
                "bash"
            ],
            "Image": "pruebacursoadri:1.0",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": null,
            "OnBuild": null,
            "Labels": {}
        },
        "NetworkSettings": {
            "Bridge": "",
            "SandboxID": "e0534f92a4f9dd0c8f365e4504fe9859f1e444e458baa4b59611879b4e756394",
            "HairpinMode": false,
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "Ports": {
                "443/udp": null,
                "53/tcp": null,
                "80/tcp": null
            },
            "SandboxKey": "/var/run/docker/netns/e0534f92a4f9",
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "EndpointID": "29699011cebfc75887b875c99fe9e5123a2b7d45edb4bbc6180b0d7e7c027415",
            "Gateway": "172.17.0.1",
            "GlobalIPv6Address": "",
            "GlobalIPv6PrefixLen": 0,
            "IPAddress": "172.17.0.3",
            "IPPrefixLen": 16,
            "IPv6Gateway": "",
            "MacAddress": "02:42:ac:11:00:03",
            "Networks": {
                "bridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "NetworkID": "32073dac32d58dac478bc704002aaaa522c6fc557337ceff486041f559cc9d55",
                    "EndpointID": "29699011cebfc75887b875c99fe9e5123a2b7d45edb4bbc6180b0d7e7c027415",
                    "Gateway": "172.17.0.1",
                    "IPAddress": "172.17.0.3",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "MacAddress": "02:42:ac:11:00:03",
                    "DriverOpts": null
                }
            }
        }
    }
]
```