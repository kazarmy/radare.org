# Microtasks

It is strongly recommended that students who want to apply to the radare2 GSoC/RSoC projects will perform a small tasks, to get the idea of students’ capabilities and make them familiar with radare2 codebase, structure and development process. Here is the list of such “qualification” tasks:

### INDEX

## Analysis

The current code analysis have many little caveats and issues which may be good to be addressed, fixing them and writing more tests is very important to stabilize and enhance it.

[See these issues](https://github.com/radare/radare2/issues?q=is%3Aissue+is%3Aopen+label%3Aanal)

## META - Graphs [#6967](https://github.com/radare/radare2/issues/6967)

### Smarter lines in graphs 

Avoid overlapping edges, currently the ascii art graphs does not overlap nodes, but some edge lines are passing thru. [#6011](https://github.com/radare/radare2/issues/6011)

![Nodes overlapping edges](https://cloud.githubusercontent.com/assets/10424605/19608188/36215ed8-97d8-11e6-8a7f-df3aef804454.png)
![Edges overlapping edges](https://cloud.githubusercontent.com/assets/10424605/19608195/3b7f4e1c-97d8-11e6-81ed-a6b515b1c7d9.png)

### Node groups

Being able to select multiple nodes in the graph and group them to colorize them and specify a name for them. [#2952](https://github.com/radare/radare2/issues/2952)

### Save/restore graph state

This task is necessary when node grouping or layout have changed, this information can be stored in projects by just reusing the `agn` and `age` commands to recreate a graph and feeding the body of the nodes in base64. 

## Diassemblers and assemblers
### Lua bytecode

Add disassembler, assembler and analyzer for the latest LUA vm. See [Issue #3836](https://github.com/radare/radare2/issues/3836)

![image](https://cloud.githubusercontent.com/assets/1408600/23942585/0d771cfa-096d-11e7-944f-c0323b0d918c.png)
![image](https://cloud.githubusercontent.com/assets/1408600/23942598/1bd53a0c-096d-11e7-80be-c7102085b091.png)


### Python bytecode
See [universal python disassembler](https://github.com/evanw/unwind) for example and [Issue #4228](https://github.com/radare/radare2/issues/4228) for current state of it.

![image](https://image.slidesharecdn.com/tailbytespygotham-140819135745-phpapp02/95/tco-in-python-via-bytecode-manipulation-7-638.jpg)

## META - RAGG2 [#6949](https://github.com/radare/radare2/issues/6949)

Ragg2 - simplistic [compiler for C-like syntax](http://radare.today/posts/payloads-in-c/) into tiny binaries for x86-32/64 and arm. Programs generated by ragg2 are relocatable and can be injected in a running process or on-disk binary file. Fixing  ragg2 issues will help a lot for creating small payloads for exploiting tasks.

## Refactoring
### Sdbtization
Radare2 is being slowly refactored to store all the information about session, user metadata and state of debugger in the [SDB](https://github.com/radare/sdb) - simple key-value database. This work still ungoing. So helping us with a few sdbtization bugs will introduce you into the radare2 codebase structure.
[See issues](https://github.com/radare/radare2/issues?q=is%3Aopen+is%3Aissue+label%3Asdbtization)

### ESILization
Radare2 has its own intermediate language - ESIL, but not yet support it for all architectures. So
the task is to add ESIL support to any architecture, which doesn't has it yet.
[See issues](https://github.com/radare/radare2/issues?utf8=%E2%9C%93&q=is%3Aissue%20is%3Aopen%20label%3Aesil) for the related bugs.

## Unicode (UTF-8) support everywhere

This task requires implementing proper support for multibyte characters in RConsCanvas in order to render UTF-8 characters in the graphs for having better ascii-art boxes and lines.

- [Support for the various languages - #2032](https://github.com/radare/radare2/issues/2032)
- [Option to enable view of unicode strings - #4997](https://github.com/radare/radare2/issues/4997)

![image](https://cloud.githubusercontent.com/assets/1408600/23970139/2728377c-09c9-11e7-8653-a167205ac153.png)
![image](https://cloud.githubusercontent.com/assets/1408600/23970169/3c1ce88a-09c9-11e7-9dc7-0da71d9bc1c6.png)

## File formats
### META - Portable Executable format [#921](https://github.com/radare/radare2/issues/6921)
There are lot of missing features in the current PE file parser as you can see in this META Issue.

![](https://image.slidesharecdn.com/44con2013workshop-exploringtheportableexecutableformat-130916113833-phpapp01/95/exploring-the-portable-executable-format-18-638.jpg)

### Proper MDMP (Windows minidump) and PGDM (Windows kernel minidump) support
There is basic MDMP file format support in [radare2-extras](https://github.com/radare/radare2-extras/tree/master/libr/bin/format/mdmp). It should be properly parsed, added ability to automatically load PDB symbols, improved autoanalysis and entry-point searching. Also
there should be a support for kernel minidumps as well.

![image](https://cloud.githubusercontent.com/assets/1408600/23970288/9ecd3520-09c9-11e7-9733-0e8d2dfe512b.png)


### PCAP loading support
Add pcap support. That will allow radare2 to replay debug sessions without actual calling of the debugger. [See issue](https://github.com/radare/radare2/issues/3574) for more details.

![image](https://cloud.githubusercontent.com/assets/1408600/23970352/bd7112d0-09c9-11e7-84b4-11946b3a2c9e.png)


### Better support for AOT and ART binaries

Current version of r2 is able to load ART and AOT binaries, but we are not yet able to extract all the information that lives in there

![image](https://cloud.githubusercontent.com/assets/1408600/23970539/62632152-09ca-11e7-976e-e35f067af344.png)

### Fix dyldcache

Dyldcache for user libraries and kernel modules is already supported, but it is not working because of the api changes in RBin. This task implies writing tests for dyldcache (we need to cook a dyldcache that can be distributable, not the ones from Apple). And fix the rbin api to get this working.

## Debugging
### Support remote iOS debugging

Support gdb:// against apple’s debugserver. This feature already works for i386 simulator, but fails when using arm/arm64 backend on real hardware).

### Better support for Activities and Permissions (list them, references, etc)

Take ideas from Androguard, and be able to follow execution flow paths to understand which permissions are used in a specific region of code, how to reach a specific activity, etc.


### Support to spawn Apps, not just programs
See `debugserver -x springboard` and such to spawn apps from the backboard otherwise they get killed.


