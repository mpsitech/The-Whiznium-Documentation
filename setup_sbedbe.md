[back](./README.md)

# Setting Up WhizniumSBE On Your Workstation

The following instructions have been tested on a Linux workstation running ubuntu 20.04, and on an M1 Mac running macOS 12.1.

It is assumed that for ``${WHIZDEVROOT}``, ``${WHIZSDKROOT}`` and ``${WHIZROOT}``, ``/home/<username>/whiznium_dev``, ``/home/<username>/whiznium`` and ``/home/<username>/whiznium_sdk``, respectively, have been chosen (Mac: ``/home/<username>`` is replaced by ``/Users/<username>``).

Note: for now it is required to have a local Whizniun installation as obtained by the following instructions. In future, _Whiznium as a Service_, the cloud-based Whiznium solution provided by MPSI Technologies can substitute as a convenient alternative. This solution has the advantage of automatically coming with the latest Whiznium updates.

## Building WhizniumSBE from source

- run WhizniumSBE (_wznm_) setup; this script clones the latest WhizniumSBE sources into ``${WHIZDEVROOT}/rep/wznm`` and performs a full build of the database access library _dbswznm_, the engine _wznmd_ and the two operation engines _wznmopd1_ / _wznmopd2_ within ``${WHIZSDKROOT}/build``:
```
cd ${WHIZDEVROOT}/setup/wznm
chmod 755 setup_wznm.sh
./setup_wznm.sh
```

- when prompted for identification towards MariaDB (Mac: MySQL), it is possible to adapt the default user name and password, relevant for pre-existing MariaDB (Mac: MySQL) installations

- generate a key and self-signed certificate to allow HTTPS:
```
cd ${WHIZROOT}/bin/wznmd
openssl genrsa -out server.key 4096
openssl req -days 365 -out server.pem -new -x509 -key server.key
```
Note that clients will get confused when different applications (such as WhizniumDBE) on the same computer try using a different key - thus, if you already have certificate and key for your machine, just copy the files into ``${WHIZROOT}/bin/wznmd``.

## Test-running WhizniumSBE

WhizniumSBE is a WhizniumSBE project and as such can leverage WhizniumSBE's out-of-the-box feature of distributed computing. The runtime setup consists of the database, one _main engine_ the clients talk to and two _operation engines_ which perform atomic compute operations, e.g. composing single source code files. This scenario is depicted below:

![](setup_sbedbe/Wznmd_Wznmopd.png)

To run WhizniumSBE, open three terminals (1), (2) and (3).

For Mac, in each terminal, specify the dynamic library path
```
export set DYLD_LIBRARY_PATH=/Users/mpsitech/whiznium_sdk/lib:/opt/homebrew/lib:/opt/homebrew/opt/curl/lib:/opt/homebrew/opt/libgit2/lib:/opt/homebrew/opt/libmicrohttpd/lib:/opt/homebrew/opt/libxml2/lib:/opt/homebrew/opt/openssl@3/lib:/usr/local/mysql/lib
```

Run, respectively:

- in (1):
```
cd ${WHIZROOT}/bin/wznmd
./Wznmd
Wznmd >> clearAll
```

- in (2):
```
cd ${WHIZROOT}/bin/wznmopd1
./Wznmopd1
```

- in (3):
```
cd ${WHIZROOT}/bin/wznmopd2
./Wznmopd2
```

- in (1), verify connections:
```
Wznmd >> showNodes
```

- e.g. in Chrome, open https://127.0.0.1:13106

This screen should show up:

![](setup_sbedbe/Wznmd.png)

- log in with username/password: temp/asdf1234
- in the __Session__ menu, choose __Close session__
- back on the (1) command line, type ``Wznmd >> quit``

The full (1) command line output should read:
```
Welcome to WhizniumSBE v1.1.3!
	starting 4 job processor threads ... {120292, 120293, 120294, 120295} success
	starting operation engine client thread ... success
	starting operation engine server ... success
	starting application server ... success
Initialization complete.

Wznmd >> clearAll 
	temporary account created for user 'temp', expires 18-12-2020 15:00:12; use password 'asdf1234' to log in
Wznmd >> showNodes
	node 1 at 127.0.0.1:13146 running 4 op processors
	node 2 at 127.0.0.1:13150 running 4 op processors
Wznmd >> quit
```

Actually working with WhizniumSBE requires preparing an initialization file with your environment-specific information, optionally using the _WhizniumSBE Bootstrap_ helper tool. This is descripbed in the first section of the [WhizniumSBE Development Workflow](./sbe.md) document.

# Setting Up WhizniumDBE On Your Workstation

The procedure is almost identical to the coresponding steps for WhizniumSBE.

## Building WhizniumDBE from source

- run WhizniumDBE (_wdbe_) setup:
```
cd setup/wdbe
chmod 755 setup_wdbe.sh
./setup_wdbe.sh
```

- when prompted for identification towards MariaDB (Mac: MySQL), it is possible to adapt the default user name and password, relevant for pre-existing MariaDB (Mac: MySQL) installations

- copy certificate and key files from the WhizniumSBE engine's folder:
```
cd ${WHIZROOT}/bin/wdbed
cp ../wznmd/server.* .
```

## Test-running WhizniumDBE

The WhizniumDBE runtime configuration, in analogy to WhizniumSBE is depicted below:

![](setup_sbedbe/Wdbed_Wdbeopd.png)

To run WhizniumDBE, open three terminals (1), (2) and (3).

For Mac, in each terminal, specify the dynamic library path
```
export set DYLD_LIBRARY_PATH=/Users/mpsitech/whiznium_sdk/lib:/opt/homebrew/lib:/opt/homebrew/opt/curl/lib:/opt/homebrew/opt/libgit2/lib:/opt/homebrew/opt/libmicrohttpd/lib:/opt/homebrew/opt/libxml2/lib:/opt/homebrew/opt/openssl@3/lib:/usr/local/mysql/lib
```

Run, respectively:

- in (1):
```
cd ${WHIZROOT}/bin/wdbed
./Wdbed
Wdbed >> clearAll
```

- in (2):
```
cd ${WHIZROOT}/bin/wdbeopd1
./Wdbeopd1
```

- in (3):
```
cd ${WHIZROOT}/bin/wdbeopd2
./Wdbeopd2
```

- in (1), verify connections:
```
Wdbed >> showNodes
```

- e.g. in Chrome, open https://127.0.0.1:13105

This screen should show up:

![](setup_sbedbe/Wdbed.png)

- log in with username/password: temp/asdf1234
- in the __Session__ menu, choose __Close session__
- back on the (1) command line, type ``Wdbed >> quit``

The full (1) command line output should read:
```
Welcome to WhizniumDBE v1.1.3!
	starting 4 job processor threads ... {126507, 126508, 126509, 126510} success
	starting operation engine client thread ... success
	starting operation engine server ... success
	starting application server ... success
Initialization complete.

Wdbed >> clearAll
	temporary account created for user 'temp', expires 18-12-2020 16:30:52; use password 'asdf1234' to log in
Wdbed >> showNodes
	node 1 at 127.0.0.1:13145 running 4 op processors
	node 2 at 127.0.0.1:13149 running 4 op processors
Wdbed >> quit
```

A description of how to include WhizniumDBE in the everyday developer experience can be found in the first section of the [WhizniumDBE Development Workflow](./dbe.md) document.

---

In case of problems, please do not hesitate to contact MPSI Technologles at [support@mpsitech.com](mailto:support@mpsitech.com).
