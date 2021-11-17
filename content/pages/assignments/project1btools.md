---
content_type: page
parent_title: Assignments
parent_uid: c614faf8-894f-e345-14ec-83a1fd01388d
title: 'Project 1, Part B: Tools'
uid: 2ceb9b1b-12cd-c3aa-054d-bf4d06429f42
---

  
zChaff

zChaff is a very efficient implementation of the complete SAT solver, Chaff. zChaff takes sentences in CNF form and produces an assignment, if one exists.  
More information about zChaff can be found at the [zChaff homepage](http://www.princeton.edu/~chaff/zchaff.html).  
Information on the standard DIMACS CNF format can be found [here](http://logic.pdmi.ras.ru/~basolver/dimacs.html). Here is ;[one example](/courses/electrical-engineering-and-computer-science/6-825-techniques-in-artificial-intelligence-sma-5504-fall-2002/assignments/test1.dimacs) ;of a CNF sentence in the DIMACS format, and here is ;[another example](/courses/electrical-engineering-and-computer-science/6-825-techniques-in-artificial-intelligence-sma-5504-fall-2002/assignments/test2.dimacs).  
  
To get zChaff, download one of the following files:  

| &nbsp; | Instructions | Tested On |
| [zChaff binary for Linux]({{< baseurl >}}/resources/zchaff2001217linux) |  {{< br >}}{{< br >}} 1.  Download the gzipped file{{< br >}}2.  Execute: gunzip zchaff.2001.2.17.linux.gz{{< br >}}3.  Execute: chmod +x zchaff.2001.2.17.linux{{< br >}}4.  To Run: ./zchaff.2001.2.17.linux ;test1.dimacs {{< br >}}{{< br >}}  | RedHat Linux 6.2, Debian GNU/Linux 2.4.9, Mandrake 8.0 |
| [zChaff binary for Solaris]({{< baseurl >}}/resources/zchaff2001217solaris) |  {{< br >}}{{< br >}} 1.  Download the gzipped file{{< br >}}2.  Execute: gunzip zchaff.2001.2.17.solaris.gz{{< br >}}3.  Execute: chmod +x zchaff.2001.2.17.solaris{{< br >}}4.  To Run: ./zchaff.2001.2.17.solaris test1.dimacs {{< br >}}{{< br >}}  | Athena |
| [zChaff C++ source code]({{< baseurl >}}/resources/zchaff2001217srctar) |  {{< br >}}{{< br >}} 1.  Download the gzipped tar file{{< br >}}2.  Execute: gunzip zchaff.2001.2.17.src.tar.gz{{< br >}}3.  Execute: tar -xvf zchaff.2001.2.17.src.tar{{< br >}}4.  Execute: make  {{< br >}}    or  {{< br >}}    make TARGET{{< br >}}5.  To Run: ./asap test1.dimacs {{< br >}}{{< br >}}  | Compiles and runs on Debian GNU/Linux 2.4.9 and Mandrake 8.0, but not on RedHat 6.2.  {{< br >}}Requires libstdc++-libc6.1-2.so.3 

What remains is to turn sentences in our CNF format into DIMACS format, and to turn zChaff's assignments into Interpretations for the original sentences.  
We have written routines to do the two conversions as part of the ; techniques.PL.CNF class.  
  
Here is how you can use the routines:  

1.  In your program, convert the CNF sentence into a DIMACS-format sentence, and record the mapping of CNF variable names to DIMACS variable names:
    
    *   CNF.pl2dimacs( CnfFilenameString ); ;// creates two files: "CnfFilenameString.dimacs" and "CnfFilenameString.dimacs.map"
    *   CNF.pl2dimacs( CnfFilenameString, DimacsFilneameString ); // creates two files: "DimacsFilneameString" and "DimacsFilneameString.map"
    *   CNF.pl2dimacs( CnfSentence, DimacsFilenameString ); // creates two files: "DimacsFilneameString" and "DimacsFilneameString.map"
    
      
    
2.  At the command line (or with a system call), run zChaff on the DIMACS file  
    
    *   zchaff.2001.2.17.solaris `mysentence.dimacs >! mysentence.zchaff`
    
      
    
3.  In your program, convert the zChaff output into an Interpretation for the original CNF sentence. ;Note that the Interpretation will be `null` if zChaff did not find an assignment.
    *   Interpretation interp = CNF.zchaffToInterpretation( "mysentence.zchaff","mysentence.dimacs.map");