[back](./README.md)

# WhizniumDBE Development Workflow

## Bootstrapping WhizniumDBE (to be performed once)

As described in [Setting Up WhizniumSBE and WhizniumDBE On Your Workstation](./setup_sbedbe.md), section "Test-running WhizniumDBE", WhizniumDBE consists of three executables which need to be launched.

Initial fill of the WhizniumDBE master database is facilitated by the cross-platform Java tool _WhizniumDBE Bootstrap_. It can be found at ``${WHIZDEVROOT}/tools/wdbp`` and is launched from the command-line like this:
```
cd ${WHIZDEVROOT}/tools/wdbp
java -jar Wdbp.jar
```

The following UI is presented:

![](dbe/Wdbp.png)

The __Perform tool initialization ...__ action will ask for an initialization file (containing e.g. users, module templates and machine/library paths), by default located at ``${WHIZDEVROOT}/projects/wdbe/ini/IexWdbeIni.txt``. In addition, the archive of code file templates needs to be specified, it can be found at ``${WHIZDEVROOT}/projects/wdbe/ini/files.tgz``.

If the corresponding section in the initialization file has been left unaltered, credentials for the default user are wdbeuser/asdf1234; they can be employed to log into WhizniumDBE via web-UI at https://127.0.0.1:13105.

The WhizniumDBE navigation screen should look like this:

![](dbe/CrdWdbeNav.png)

The second section of _WhizniumDBE Bootstrap_ revolves around synchronization of the local project repository directory, by default at ``${WHIZDEVROOT}/rep`` with the WhizniumDBE master database. In a first step, initiated by __Locate repository root directory ...__, a local scan of the selected directory identifies WhizniumDBE projects by their characteristic folder structure. Actual synchronization takes place in the second step, triggered by __Bootstrap ...__.  After successful execution, WhizniumDBE is ready to iterate source code trees of the local projects.

## Iterating source code trees with WhizniumDBE (to be performed regularily while developing)

Source code tree iteration using WhizniumDBE is - besides, obviously, model file editing - the only step which is added to the typical embedded software development workflow when using Whiznium. The cross-platform Java tool _WhizniumDBE Iterator_ allows to do this in just a few clicks. It can be found at ``${WHIZDEVROOT}/tools/wdit`` and is launched from the command-line like this:
```
cd ${WHIZDEVROOT}/tools/wdit
java -jar Wdit.jar
```

The following UI is presented:

![](dbe/Wdit.png)

After connecting to WhizniumDBE (__Connect ...__), the list of projects is populated. Upon selection of a specific project, it is possible to step to a next version (based on updated model information) by choosing the __Step version and iterate source code tree ...__ action. Some workflow options, such as how to increment the version number, Git/non-Git options, can be selected, before the actual iteration is performed. If no error is found, _WhizniumDBE Iterator_ proceeds with uploading the existing source code tree and progressing existing manual code into the newly generated source code tree. The sequence is finalized by committing/downloading the new version of the source code tree.

Should errors be present in the existing source code tree's _insertion points_ (e.g. of type ``-- IP xyz --- IBEGIN/IEND``), it is required to fix these errors. In that case, only the __Iterate source code tree ...__ action needs to be executed, as version stepping has already completed at this stage.

For a behind the scenes look of _WhizniumDBE Iterator_'s basic functionality, it is worth looking at the __Version__ card menu of WhizniumDBE:

![](dbe/CrdWdbeVer.png)

The listed import actions are performed before actual source code is written.

---

In case of problems, please do not hesitate to contact MPSI Technologles at [support@mpsitech.com](mailto:support@mpsitech.com).
