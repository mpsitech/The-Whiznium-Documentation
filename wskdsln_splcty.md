[back](./README.md)

# Creating The Whiznium StarterKit Device Simplicity Studio Solution From Scratch

In preparation for the following instructions, clone the [Whiznium StarterKit Device Git repository](https://github.com/mpsitech/wskd-Whiznium-StarterKit-Device) into an auxiliary folder, e.g. to ``C:\Users\mpsitech\temp\wskd``.

Launch Simplicity Studio and perform the following steps for setting up a new project:

- in the main menu, navigate to __File__ -> __New__ -> __Silicon Labs Project Wizard...__
- as __Target Board__, select "EFM8UB1 Universal Bee Starter Kit Board"
- if not automatically filled in, the __Target Device__ should be "EFM8UB10F16G-B-QFN28"
- choose "8051 SDK" under __SDK__ and hit __NEXT__
- on the __Examples__ tab, select __Empty C Project__ and hit __NEXT__ again
- on the __Configuration__ tab, enter "ubdk" as __Project name__ and click __FINIISH__

The newly created project should now show up in the __Project Explorer__. Incorporating Whiznium StarterKit Device files is best done in the Windows File Explorer, for these manipulations it is better to close Simplicity Studio. The steps under the solution directory (typically at ``C:\Users\mpsitech\SimplicityStudio\v5_workspace\ubdk``) are as follows:

- add an ``inc`` directory next to ``src``
- from ``C:\Users\mpsitech\temp\wskd\mcuwskd\ubdk``, copy all .h files to ``inc`` and all .c files to ``src``
- delete the original file ``src\ubdk_main.c``

Perform the remaining project configuration in Simplicity Studio by re-opening it and navigating to __Simplicity IDE__. Open __Properties__ from the context menu that pops up when right-clicking on ``ubdk``:

- in __C/C++ Build__ -> __Settings__, __Keil 8051 Compiler__ -> __Includes__, add ``"${workspace_loc:/${ProjName}/inc}"`` and ``"${StudioSdkPath}/Device/EFM8UB1/VCPXpress"``
- in __C/C++ Build__ -> __Settings__, __Keil 8051 Compiler__ -> __Optimization__, select __Level__ 8
- in __C/C++ Build__ -> __Settings__, __Keil 8051 Linker__ -> __Libraries__, add ``"${StudioSdkPath}/Device/EFM8UB1/VCPXpress/VCPXpress.lib"``

To test the configuration, navigate to __Project__ -> __Build Project__ in the main menu. The last lines of the console output should read

```
Program Size: data=166.6 xdata=228 const=2148 code=13442
LX51 RUN COMPLETE.  17 WARNING(S),  0 ERROR(S)
Finished building target: ubdk.omf

03:09:52 Build Finished. 0 errors, 17 warnings. (took 2s.266ms)
```

---

In case of problems, please do not hesitate to contact MPSI Technologles at [support@mpsitech.com](mailto:support@mpsitech.com).
