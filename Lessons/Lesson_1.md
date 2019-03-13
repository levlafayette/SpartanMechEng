-- *Slide* --
### Goals For This Morning
* Part 1: Learning about supercomputers and Spartan.
* Part 2: Logging on an exploring the Linux Environment.
* Part 3: Learning about Environment Modules and the Slurm job submission system.
* Part 4: Submitting test jobs.
* Part 5: Slurm Command Summaries
-- *Slide End* --

-- *Slide* --
### Slide Respository
* A copy of these slides and sample code is available at: `https://github.com/UoM-ResPlat-DevOps/SpartanMechEng`
* A copy of information about HPC at the University of Melbourne is available at `https://dashboard.hpc.unimelb.edu.au`. See also `man spartan` on the cluster and the `/usr/local/common/` directories for more help and code exammples.
* Help is available at: `hpc-support@unimelb.edu.au`. Other courses also conducted by Research Platforms.
-- *Slide End* --

-- *Slide* --
### Part I: Helpdesk
* Read the Message of the Day when you login!
* If a user has problems with submitting a job, or needs a new application or extension to an existing application installed, or if their submissions are generated unexpected errors etc., an email can be sent to the helpdesk: `hpc­-support@unimelb.edu.au`. 
* Do not email individual sysadmins; we need consolidated records. Please be informative about the error or issue. Don't try to use sudo!
-- *Slide End* --

-- *Slide* --
### Part 1: Supercomputers and HPC
* "Supercomputer" means any single computer system that has exceptional processing power for its time. 
* One popular metric (LINPACK) is the number of floating­ point operations per second (FLOPS) such a system can carry out (http://top500.org). HPC Challenge and HPCG are broader, more interesting metrics. 
* High Performance Computer (HPC) is any computer system whose architecture allows for above average performance. High Throughput Computing (HTC) is an architecture for maximum job completion; capability vs capacity computing.
-- *Slide End* --

-- *Slide* --
### Part 1: Clusters and Research Computing
* Clustered computing is when two or more computers serve a single resource. This improves performance and provides redundancy in case of failure system. Typically commodity systems with a high-speed local network.
* Research computing is the software applications used by the scientific community to aid research. Does not necessarily equate with high performance computing, or the use of clusters.­ It is whatever researchers use and do. Not issues of producibility and environments.
-- *Slide End* --

-- *Slide* --
### Part 1: Parallel Computing
* With a cluster architecture, applications can be more easily parallelised across them. *Data parallel*, running same task in parallel; the horse and cart example, Monte Carlo experiments. *Task parallel*, running independent tasks in parallel with communication; driving a car, molecullar modelling.
* Further examples of serial versus parallel; weather forecasting, aerodynamic design, fluid mechanics, radiation modelling, molecullar dynamics, CGI rendering for popular movies, etc. Reality is a parallel system!
-- *Slide End* --

-- *Slide* --
### Part 1: Use for MechEng
* Plenty of good MechEng software available for Linux; Ansys, ABAQUS, NASTRAN etc. But much of this is licensed.
* Spartan does have OpenFOAM, Comsol (group restriction), and a variety of relevant mathematical tools including Matlab, Octave, and R. Plus general purpose programming (e.g., Python, C/C++, Fortran), and scripting - a very powerful tool for automating changes.
* HPC job submission is essential for computation for capability (multinode) or capacity (multicore).
-- *Slide End* --

-- *Slide* --
### Part 1: HPC Cluster and Parallel Processing Components
* A chassis or rack, containing multiple computer system units, interconnect, and providing power.
* Computer system units or nodes, containing memory, local disk, and sockets.
* Sockets contain a processor which has one or more cores which do the processing.
* Logical processes have shared resources (e.g., memory) which may have multiple instruction stream threads.
-- *Slide End* --

-- *Slide* --
### Part 1: Generic HPC Cluster Design
<img src="https://raw.githubusercontent.com/UoM-ResPlat-DevOps/SpartanIntro/master/Images/genericcluster.png" />
Image originally from the VPAC
-- *Slide End* --

-- *Slide* --
### Part 1: Valedictions King Edward
* From 2011-2015 UniMelb's general cluster was Edward (previous system was Alfred); new system is Spartan (not Æthelstan or Ælfweard)
* A review was conducted looking at the infrastructure and metrics of Edward, the University's general HPC system since 2011. Edward's usage statistics show that single-core and low memory jobs dominate; 76.35% of jobs from Feb 9 2015 to Feb 9 2016 were single core, and 96.83% used 1-4GB of memory.
-- *Slide End* --

-- *Slide* --
### Part 1: What's Different About Spartan?
* Recommended solution was to make use of existing NeCTAR Research cloud with an expansion of general cloud compute provisioning and use of a smaller "true HPC" system on bare metal nodes.
* Matches Sparta's citenzship structure. Spartan is not "HPC in the Cloud", it's a chimera HPC/Cloud hybrid.
* Other institutions (e.g., University of Freiburg) do "Cloud on HPC". 
-- *Slide End* --

-- *Slide* --
### Part 1: Spartan Design
<img src="https://raw.githubusercontent.com/UoM-ResPlat-DevOps/SpartanIntro/master/Images/spartanlayout.png" />
-- *Slide End* --

-- *Slide* --
### Part 1: Spartan Hardware
* Physical partition 1 is 19 nodes, 228 cores, 21 GB per core,  2 socket Intel E5-2643 v3 CPU with 6-core per socket, 3.4GHz, 254GB memory, 2x 1.2TB SAS drives, 2x 40GbE network Mellanox 2100. 
* Cloud partition is 165 virtual machines with over 1,980 cores, dual CPU Intel(R) Xeon(R) Gold 6138 CPU, 2.00GHz, 10GBe Cisco Nexus. 
* GPU partition for LIEF grant recipients, 1,752 core, 4 P100 Nvidia GPUs per node
* Storage: 4.3PB `/scratch` NFS over RDMA, `/project` and `/home`.
-- *Slide End* --

-- *Slide* --
### Part I: Accounts and Projects
* Spartan uses its an authentication that is tied to the university Security Assertion Markup Language (SAML). The login URL is `https://dashboard.hpc.unimelb.edu.au/karaage`
* Users on Spartan must belong to a project. Projects must be led by a University of Melbourne researcher (the "Principal Investigator") and are subject to approval by the Head of Research Compute Services. Participants in a project can be researchers or research support staff from anywhere.
* Select Department from this list: `https://gitlab.unimelb.edu.au/resplat-cloud/uom-cloud-dashboard/blob/uom/queens/nectar_dashboard/rcallocation/choices_dept.py`
* Projects have their own project directory for files (500GB default).
-- *Slide End* --

-- *Slide* --
### Part I: Logging In
* To log on to a HPC system, you will need a user account and password and a Secure Shell (ssh) client. Linux distributions almost always include SSH as part of the default installation as does 
Mac OS 10.x. For MS-­Windows users, the free PuTTY client is recommended (http://putty.org). 
* To transfer files use scp, WinSCP, Filezilla (`https://filezilla-project.org/`), or rsync.
* Example login: `lev@spartan.hpc.unimelb.edu.au`
-- *Slide End* --

-- *Slide* --
### Part I: SSH Keys, Config, Data Transfers
* Consider using an `.ssh/config` file and using passwordless SSH by creating a keypair and adding to your `.ssh/authorized_keys` file on Spartan.
* SSH Keys will make your life easier. Follow the instructions here: `https://dashboard.hpc.unimelb.edu.au/faq/#how-do-setup-passwordless-ssh-login`
* Both useful for data transfers. c.f., `https://dashboard.hpc.unimelb.edu.au/managing_data/` 
-- *Slide End* --

-- *Slide* --
### Part I: Latency, Bandwidth, Data Location
* Latency is the speed of data transfer, bandwidth is the "width" of the "band" of data transfer.
* Using a road analogy, "latency" is the smoothness of the surface, "bandwith" is the number of lanes.
* Distance is a *very* important factor. Data for processing should be kept as close as possible to the processor.
* As Grace Hopper used to say: "Mind your nanoseconds!" https://www.youtube.com/watch?v=JEpsKnWZrJ8
-- *Slide End* --

-- *Slide* --
### Part 2: This is a GNU/Linux CLI World 
<img src="https://raw.githubusercontent.com/UoM-ResPlat-DevOps/SpartanIntro/master/Images/gnulinux.png" align="center" height="25%" width="25%" vspace="5" hspace="5" />
-- *Slide End* --

-- *Slide* --
### Part 2: This is a GNU/Linux World CLI II
* The command­line interface provides a great deal more power and is very resource efficient. 
* GNU/Linux scales and does so with stability and efficiency.
* Critical software such as the Message Parsing Interface (MPI) and nearly all scientific programs are designed to work with GNU/Linux. 
* The operating system and many applications are provided as "free and open source" which are better placed to improve, optimize and maintain.
-- *Slide End* --

-- *Slide* --
### Part 2: File System Hierarchy
* When a user logs in on a Linux or other UNIX-like system on the command line, they start in their home directory (`/home/<<username>>`). Explore file system hierarchy. Project directory in `/data/projects/<<projectID>>`.
* "Everything in the UNIX system is a file" (Kernighan & Pike, 1984, 41). 
* See `https://swcarpentry.github.io/shell-novice/fig/standard-filesystem-hierarchy.svg`
-- *Slide End* --

-- *Slide* --
### Part 2: Exploring The Environment
| Command     | Explanation                                                                |
|:------------|:--------------------------------------------------------------------------:|
|`whoami`   | "Who Am I?; prints the effective user id                                  |
|`pwd`      | "Print working directory"|
|`ls`       | "List" directory listing                                                   |	
-- *Slide End* --

-- *Slide* --
### Part 2: Command Options
* Linux commands often come with options expressed as: `<command> --<option[s]>`
* Options can be expressed as full words or abbreviated characters.

| Command     | Explanation                                                                |
|-------------|:--------------------------------------------------------------------------:|
|`ls -lart`   | Directory listing with options (long, all, reverse time)                   |
|`ls -lash`   | Directory listing with options (long, all, size in human readable	   |
-- *Slide End* --

-- *Slide* --
### Part 2: The Online Manual
Linux commands come with "man" (manual) pages, which provide a terse description of the meaning and options available to a command. A verbose alternative to man is info. 

| Command             | Explanation                                                      |
|:--------------------|:-----------------------------------------------------------------|
|`man <command`       | Display the manual entry for the command                         |
|`info <command>`     | A verbose description of the command                             |
| `whatis <command>`  | A terse description of the command                               |
-- *Slide End* --

-- *Slide* --
### Part 2: Pipes
Linux also have very useful 'pipes' and redirect commands. To pipe one command through another use the '|' symbol.

| Command            | Explanation                                                         |
|:-------------------|:-------------------------------------------------------------------:|
| <code>who -u  &#124; less</code> | "Who" shows who is logged on and how long they've been idle.        |
| <code>ps afux &#124; less</code> | "ps" provides a list of current processes. Check `man ps`           |
-- *Slide End* --

-- *Slide* --
### Part 2: Redirects
To redirect output use the '>' symbol. To redirect input (for example, to feed data to a command) use the '<'. Concatenation is achieved through the use of '>>' symbol. 

| Command           | Explanation                                                          |
|:------------------|:--------------------------------------------------------------------:|
| `w > list.txt`  | 'w' is a combination of who, uptime and ps -a, redirected            |
| `w >> list.txt` | Same command, concatenated                                           |
-- *Slide End* --

-- *Slide* --
### Part 2: Files and Text Editing I
* Linux filenames can be constructed of any characters except the forward slash, which is for directory navigation. However it is best to avoid punctuation marks, non-printing characters (e.g., spaces). It is *much* better to use underscores or CamelCase instead of spaces, newlines etc (including in job names).
* Linux is case-sensitive with its filenames (e.g., list.txt, LIST.txt lisT.txT are different).
-- *Slide End* --

-- *Slide* --
### Part 2: Files and Text Editing II
* Files do not usually require a program association suffix, although you may find this convenient (a C compiler like files to have .c in their suffix, for example). 
* The type of file can be determined with the `file` command. The type returned will usually be text, executable binaries, archives, or a catch-all "data" file.
* There are three text editors usually available on Linux systems on the command-line. These are `nano` (1989, as `pico`) and `vim` (or `vi`), and or `emacs` (both 1976). See `https://www.vimgolf.com/`
-- *Slide End* --

-- *Slide* --
### Part 2: Copying Files to a Local Systems
To get a copy of the files from an external source to your home directory, you will probably want to use `wget`, or `git`, or `scp`.

| Command           | Explanation                                                          |
|:------------------|:--------------------------------------------------------------------:|
| `wget URL`      | Non-interactive download of files over http, https, ftp etc.           |
| `git clone URL` | Clone a repository into a new directory.                               |
-- *Slide End* --

-- *Slide* --
### Part 2: Copying Files Within a Local Systems 
To copy a file from within a system use the `cp` command. Common options include `-r` to copy an entire directory

| Command           | Explanation                                                          |
|:------------------|:--------------------------------------------------------------------:|
| `cp source destination`      | Copy a file from source to destination                    |
| `cp -r source destination` | Recursive copy (e.g., a directory)		           |
| `cp -a source destination` | Recursive copy as archive (permissions, links)		   |
-- *Slide End* --

-- *Slide* --
### Part 2: Copying Files Between Systems
To copy files to between systems desktop use SCP (secure copy protocol) or SFTP (secure file transfer protocol), combining the ssh and cp functionality. The `cp` options can also be used. The source or destination address should also require a remote shell login.

| Command           | Explanation                                                          |
|:------------------|:--------------------------------------------------------------------:|
| `scp source.address:/path/ destination.address:/path/`| Copies files on a network        |
-- *Slide End* --

-- *Slide* --
### Part 2: Synchronising Files and Directories I
* The `rsync` utility provides a fast way to keep two collections of files "in sync" by tracking changes.    
* The source or destination address should also require a remote shell login.    
For example; `rsync -avz --update lev@spartan.hpc.unimelb.edu.au:files/workfiles .`
-- *Slide End* --

-- *Slide* --
### Part 2: Synchronising Files and Directories II

| Command           | Explanation                                                          |
|:------------------|:--------------------------------------------------------------------:|
| `rsync source destination`| General rsync command  |
| `rsync -avze ssh username@remotemachine:/path/to/source .` | With ssh encryption |
-- *Slide End* --

-- *Slide* --
### Part 2: Synchronising Files and Directories III
* The `rsync -avz` command ensures that it is in archive mode (recursive, copies symlinks, preserves permissions), is verbose, and compresses on transmission. 
* The --update restricts the copy only to files that are newer than the destination. 
* Note that rsync is "trailing slash sensitive". A trailing / on a source means "copy the contents of this directory". Without a trailing slash it means "copy the directory".
-- *Slide End* --

-- *Slide* --
### Part 2: Synchronising Files and Directories IV
* Rsync can be used in a synchronise mode with the --delete flag.  Consider this with the `-n`, or `--dry-run` options first!

| Command           | Explanation                                                          |
|:------------------|:--------------------------------------------------------------------:|
| `rsync -avz --update source/ username@remotemachine:/path/to/destination| Synchronise, keep older files  |
| `rsync -avz --delete source/ username@remotemachine:/path/to/destination| Synchronise, absolutely |
-- *Slide End* --

-- *Slide* --
### Part 2: Creating Directories, Moving Files
* Directories can be created with the `mkdir` command (e.g., `mkdir braf`).
* Files can be copied with the `cp` command (e.g., `cp gattaca.txt gattaca2.txt`)
* Files can be moved with the `mv` command (e.g., `mv gattaca2.txt braf`)
-- *Slide End* --

-- *Slide* --
### Part 2: File Differences
* File differences can be determined by timestamp (e.g., `ls -l gattaca.txt braf/gattaca.txt`)
* Content differences can be determined by the `diff` command (e.g., `diff gattaca.txt braf/gattaca.txt`)
* For a side-by-side representation use the command `sdiff` instead.
* The command `comm` can compare two files, lines by line (e.g., `comm gattaca.txt braf/gattaca.txt`).
-- *Slide End* --

-- *Slide* --
### Part 2: Searches and Wildcards
* To search for files use the find command (e.g., `find . -name '*.txt'`). Compare with `locate` and `whereis`.
* To search within files, use the `grep` command (e.g., `grep -i ATEK braf/*` or `grep -l`)
* The most common wildcard is `*`, but there is also `?` (single character).
* There are also range searches (e.g., `[a-z]` any character between a and z, inclusive)
-- *Slide End* --

-- *Slide* --
### Part 2: Deletions
* Files can be deleted with the `rm` command (e.g., `rm gattaca.txt`)
* Empty directories can be deleted with the `rmdir` command (e.g., `rmdir braf`)
* Directories, files, subdirectories etc can be delted with `rm -rf <<dir>>`
* BE VERY CAREFUL, ESPECIALLY WITH WILDCARDS!
* Consider the difference between `rm matlab *` to `rm matlab*`.
-- *Slide End* --

-- *Slide* --
### Part 2: Why The File Differences Mattered
<blockquote>
BRAF is a human gene that makes a protein (imaginatively) named B-Raf. This protein is involved in sending signals inside cells, which are involved in directing cell growth. In 2002, it was shown to be faulty (mutated) in human cancers. In particular the difference that between the two files "ATVKSRWSGS" and "ATEKSRWSGS" is the difference which leads to susceptibility to metastatic melanoma. 
</blockquote>
-- *Slide End* --

-- *Slide* --
### Part 3: A Dynamic Environment
* Environment modules provide for the dynamic modification of the user's environment via module files, such as the location of the application's executables, its manual path, the library path, and so forth.
* Modulefiles also have the advantages of being shared on many users on a system (such as an HPC system) and easily allowing multiple installations of the same application but with different versions and compilation options.
* Check the current environment with the `env` (environment) command.
-- *Slide End* --

-- *Slide* --
### Part 3: Environment Modules  Commands
* The are two implementations of environment modules. The classic modules system was available on the Edward HPC, and the newer Lmod is on Spartan. LMod is considered superior for hierarchies of modules.
-- *Slide End* --

-- *Slide* --
### Part 3: Module Commands I
| Command                         | Explanation                                            |
|---------------------------------|:------------------------------------------------------:|
| `module help`                 | List of switches, commands and arguments for modules   |
| `module avail`                | Lists all the modules which are available to be loaded.|
| `module display <modulefile>` | Display paths etc for modulefile                       |
-- *Slide End* --

-- *Slide* --
### Part 3: Module Commands I
| Command                         | Explanation                                            |
|---------------------------------|:------------------------------------------------------:|
| `module load <modulefile>`    | Loads paths etc to user's environment                  |
| `module unload <modulefile>`  | Unloads paths etc from user's environment.             |
| `module list`                 | lists all the modules currently loaded.                |
-- *Slide End* --

-- *Slide* --
### Part 3: Module Commands III
* There is also the `module switch <modulefile1> <modulefile2>`, which unloads one modulefile (modulefile1) and loads another (modulefile2).
* Lmod modules also support regular expressions, e.g., `module -r avail "^Python"`
* On Spartan there is also the lmod-specific `module spider <modulename>, which traverses through the system for all modules and provides a description.
-- *Slide End* --

-- *Slide* --
### Part 3: Portable Batch System I
* The Portable Batch System (or simply PBS) performs job scheduling by assigning unattended background tasks expressed as batch jobs, among the available resources.
* Originally developed by MRJ Technology Solutions under contract to NASA in the early 1990s. Released as an open-source product as OpenPBS. Forked by Adaptive Computing as TORQUE (Terascale Open-source Resource and QUEue Manager). Many of the original engineering team now part of Altair Engineering who have their own commercial version, PBSPro.
-- *Slide End* --

-- *Slide* --
### Part 3: Portable Batch System II
* A batch system typically consists of a resource manager (e.g., TORQUE) and a job scheduler (e.g., Maui, Moab), or a combination (e.g., PBSPro, Slurm).
*  TORQUE and MOAB was used on the Edward HPC system. Slurm is used on Spartan.
-- *Slide End* --

-- *Slide* --
### Part 3: Slurm Workload Manager
* Slurm, used on Spartan, began development as a collaborative effort primarily by Lawrence Livermore National Laboratory, SchedMD, Linux NetworX, Hewlett-Packard, and Groupe Bull as a Free Software resource manager. As of November 2015, TOP500 list of most powerful computers in the world indicates that Slurm is the workload manager on six of the top ten systems. Slurm's design is very modular with about 100 optional plugins.
* There is a repository for converting PBS to Slurm: https://github.com/bjpop/pbs2Slurm
-- *Slide End* --

-- *Slide* --
### Part 3: Job Submission Principles
* The steps for job submission are (a) setup and launch., (b) monitor., and (c) retrieve results and analyse. Jobs are launched from the login node with resource requests and, when the job scheduler decides, run on compute nodes. Some directories (e.g.,. user home or project directories) are shared across the entire cluster so output is an accessible place.
* Job scripts are simply resource requests (understood by scheduler), a batch of commands (understood by shell) with output to files.
-- *Slide End* --

-- *Slide* --
### Part 3: Fair Share
* A cluster is a shared environment thus a a resource requesting system. Policies ensure that everyone has a "fair share" to the resources (e.g., user processor limits).
* Spartan's general partition (cloud, physical) treat all jobs equally. The GPGPU has allocation based on purchasing.
-- *Slide End* --

-- *Slide* --
### Part 3: DON'T RUN JOBS ON THE LOGIN NODE!
* The login node is a **particularly** shared resource. All users will access the login node in order to check their files, submit jobs etc. If one or more users start to run computationally or I/O intensive tasks on the login node (such as forwarding of graphics, copying large files, running multicore jobs), then that will make operations difficult for everyone.
-- *Slide End* --

-- *Slide* --
<img src="http://levlafayette.com/files/rabbitjobs.png" width="100%" height="100%" title="Job submission using rabbits" />
From the IBM 'Red Book' on Job Submission.
-- *Slide End* --

-- *Slide* --
### Part 2: Partitions and Queues
* Setup and launch consists of writing a short script that initially makes resource requests 
(walltime, processors, memory, queues) and then commands (loading modules, changing 
directories, running executables against datasets etc), and optionally checking queueing system.
* Core command for checking paritions is `sinfo -s`, or `sinfo -p $partition` for partition and node status. Major partitions are: `cloud`, `physical`, `gpgpu`. Note also `longcloud`, and `shortgpgpu`.
* Core command for checking queue `squeue` or `showq` (on Spartan).
-- *Slide End* --

-- *Slide* --
### Part 2: Job Status
* Core command for job submission `sbatch [jobscript]` 
* Core command for checking job `squeue -j [jobid]`, detailed command `scontrol show job [jobid]` (SLURM), or all user's jobs `squeue -u [username]`.
* Core command for deleting job `scancel [jobid]`
* Basic resource usage `sacct -j [jobid] --format=JobID,JobName,MaxRSS,Elapsed` (or `-u [username]`
-- *Slide End* --

-- *Slide* --
### Part 3: Single Core Job
```bash
#!/bin/bash
#SBATCH -­p cloud
#SBATCH ­­--time=01:00:00
#SBATCH ­­--ntasks=1
module load my­app­compiler/version
my­app data
```
-- *Slide End* --

-- *Slide* --
* Examples at `/usr/local/common/MATLAB`, `/usr/local/common/R`, `/usr/local/OpenFOAM`; note that the job can call other scripts. Note that Slurm has full and abbreviated directives.
-- *Slide End* --

-- *Slide* --
### Part 3 : Multicore and Multithreaded Jobs
* In Slurm, `ntasks` means number of tasks, whereas `cpus-per-task` allocates processor cores. In most jobs (serial, MPI) this is 1 by default.
* With shared-memory multithreaded jobs on (e.g., OpenMP), modify the `--cpus-per-task` to a maximum of the cores in the node. <b>Note: not available in OpenFOAM.</b><br />
`#SBATCH ­­--cpus-­per-­task=8`
* See examples at `/usr/local/common/FSL/`
-- *Slide End* --

-- *Slide* --
### Part 3 : Multinode Jobs I
* For distributed-memory multicore job using message passing, the multinode partition has to be 
invoked and the resource requests altered e.g.,
`#!/bin/bash`<br />
`#SBATCH -­p physical`<br />
`#SBATCH ­­--nodes=2`<br />
`#SBATCH ­­--ntasks-per-node=8`<br />
`module load my­app­compiler/version`<br />
`srun my­mpi­app`
-- *Slide End* --

-- *Slide* --
### Part 3 : Multinode Jobs II
* Multinodes jobs should be run on the `physical` partition which has the higher interconnect speed.
* Multinode jobs on Spartan may be slower if they have a lot of interprocess communication and they cross compute nodes.
* This said, multinodes jobs can also request total tasks/cores rather than allocating them per node. e.g., `#SBATCH ­­--ntasks=16`<br />
* See examples at `/usr/local/common/Python`, `/usr/local/common/OpenFOAM`
-- *Slide End* --

-- *Slide* --
### Part 3 : OpenFOAM Multinode Jobs
* Multicore OpenFOAM jobs require a `decomposeParDict` file (see `LES/oppositeBurningPanels/system/decomposeParDict`) to break up mesh and fields.
* Sometimes you *might* want to reconstruct the decomposed domain (use `reconstructPar`).
* In `decomposeParDict` Subdomains = Tasks. Must include `simpleCoeffs` for number of subdomains in x, y, z. Must include delta, a cell-skew factor (typically 10^-3)
-- *Slide End* --

-- *Slide* --
### Part 3 : OpenFOAM Decompose Methods
* Method is how task is split up (`simple` or `scotch` is easiest!)
* Simple: Geometric decomposition, domain split into pieces by direction (e.g., 2 in x, 1 in y etc)
* Hierarchical: As simple except order is specified (first Y then X). See `multiphase/reactingTwoPhaseEulerFoam/laminar/bubbleColumnEvaporating/system/decomposeParDict`
* Scotch: Requires no geometric input from the user and attempts to minimise the number of processor boundaries. User can specificy weights with `processorWeights`. See `multiphase/interFoam/RAS/DTCHull/system/decomposeParDict`
* Manual: User specifies call to particular processor. 
* Methods have their own compulsory entries; `scotch` doesn't require any!
-- *Slide End* --

-- *Slide* --
### Part 3 : Job Script Generator
<img src="https://raw.githubusercontent.com/UoM-ResPlat-DevOps/SpartanIntro/master/Images/cat-asleep-on-keyboard.jpg" width="100%" height="100%" title="Lazy cat" />
` https://dashboard.hpc.unimelb.edu.au/guides/script_generator/ `
-- *Slide End* --

-- *Slide* --
### Part 4: Interactive Jobs
* An interactive job, based on the resource requests made on the command  line, puts the user on to a compute node. This is typically done if they user wants to run a  large script (and shouldn't do it on the login node), or wants to test or debug a job. The  following command would launch one node with two processors for ten minutes.
`sinteractive ­­--nodes=1 --­­ntasks-­per-­node=2 --­­time=0:10:0`
* Example and instructions at `/usr/local/common/interact` and examples in `/usr/local/common/OpenFOAM`
-- *Slide End* --

-- *Slide* --
### Part 4 : Job/Batch Arrays
* With a job or batch array the same batch script, and therefore the same resource requests, is used multiple  times. A typical example is to apply the same task across multiple datasets. The following example submits 10 batch jobs with myapp running against datasets dataset1.csv, dataset2.csv, ... 
dataset10.csv
`#SBATCH ­­array=1­-10`<br />
`myapp ${Slurm_ARRAY_TASK_ID}.csv`
* Examples at `/usr/local/common/array` and `/usr/local/common/Octave`.
-- *Slide End* --

-- *Slide* --
### Part 4 : Job/Batch Dependencies
* A dependency condition is established on which the launching of a batch script depends, creating a conditional pipeline. The dependency directives consist of `after`, `afterok`, `afternotok`, `before`, `beforeok`, `beforenotok`. A typical use case is where the output of one job is required as the input of the next job. Multiple job dependencies are specified with colon separated values.
`#SBATCH ­­dependency=afterok:myfirstjobid mysecondjob`
* Examples at `/usr/local/common/depend/`
-- *Slide End* --

-- *Slide* --
### Part 4 : Multiple Job Steps
* Sometimes a job needs to consist of several steps that need to be carried on sequence, even if the individual components are in parallel. In this case the entire job resource set can be called with an aggregation of walltime and with a maximum reduction operation for memory and resources.
* Whilst this can be convenient, to include everything in a single script, it runs the risk on a busy system of being inefficient in the queue.
-- *Slide End* --

-- *Slide* --
### Part 4 : Multiple Job Steps II
```
#!/bin/bash
#SBATCH --­partition physical
#SBATCH ­­--nodes=2
#SBATCH ­­--ntasks=12
#SBATCH --time=24:00:00
srun -N 2 -n 12 -t 06:00:00 ./my­mpi­app
export OMP_NUM_THREADS=6
srun -N 1 -n2 -c $OMP_NUM_THREADS -t 12:00:00 ./myompapp
srun -N 1 -n 1 -t 06:00:00 ./myserialapp
```
-- *Slide End* --

-- *Slide* --
### Part 4: Backfilling
* Many schedulers and resource managers use a backfilling algorithm to improve system utilisation and maximise job throughout. 
* When more resource intensive (e.g., multiple node) jobs are running it is possible that gaps ends up in the resource allocation. To fill these gaps a best effort is made for low-resource jobs to slot into these spaces.
* For example, on an 8-core node, an 8 core job is running, a 4 core job is launched, then an 8 core job, then another 4 core job. The two 4 core jobs will run before the second 8 core job.
-- *Slide End* --

-- *Slide* --
### Part 4: Memory Allocation
* By default the scheduler will set memory equal to the total amount on a compute node divided by the number of cores requested. In some cases this might not be enough (e.g., very large dataset that needs to be loaded with low level of parallelisation).
* Additional memory can be allocated with the `--mem=[mem][M|G|T]` directive (entire job) or `--mem-per-cpu=[mem][M|G|T]` (per core). Maximum should be based around total cores -1 (for system processes). The --mem-per-cpu directive is for threads for OpenMP applications and processor ranks for MPI.
-- *Slide End* --

-- *Slide* --
### Part 4: Staging
* Local disk is typically faster than shared disks. If you find that your read-writes are slow and you are making use of a lot of I/O you may need to stage your data.
* Spartan has `/data` for /home and /projects (large, slower), `/scratch` for temporary storage data (faster), and as local disk, `/var/local/tmp` (fastest, not shared). You may need to copy data between these locations. 
-- *Slide End* --

-- *Slide* --
### Part 5: Slurm User Commands
| User Commad    | Slurm Command           | 
|----------------|------------------------:|
|Job submission  |sbatch [script_file]     |
|Job delete      |scancel [job_id]         |
|Job status      |squeue [job_id]          |
|Job status      |squeue -u [user_name]    |
|Node list       |sinfo -N                 |
|Queue list      |squeue                   |
|Cluster status  |sinfo               	   |
-- *Slide End* --

-- *Slide* --
### Part 5: Slurm Job Commands I
| Job Specification     | Slurm Command              | 
|-----------------------|---------------------------:|
|Script directive       |`#SBATCH`                   |
|Queue                  |`-p [queue]`                |
|Job Name               |`--job-name=[name]`         |
|Nodes                  |`-N [min[-max]]`            |
|CPU Count              |`-n [count]`                |
|Wall Clock Limit       |`-t [days-hh:mm:ss]`        |
-- *Slide End* --

-- *Slide* --
### Part 5: Slurm Job Commands II
| Job Specification     | Slurm Command              | 
|-----------------------|---------------------------:|
|Event Address          |`--mail-user=[address]`     |
|Event Notification     |`--mail-type=[events]`      |
|Memory Size            |`--mem=[mem][M|G|T]`        |
|Proc Memory Size       |`--mem-per-cpu=[mem][M|G|T]`|
-- *Slide End* --

-- *Slide* --
### Part 5: Slurm Environment Commands
| Environment Command   | Slurm (Command)         | 
|-----------------------|------------------------:|
|Job ID                 |`$SLURM_JOBID`           |
|Submit Directory       |`$SLURM_SUBMIT_DIR`      |
|Submit Host            |`$SLURM_SUBMIT_HOST`     |
|Node List              |`$SLURM_JOB_NODELIST`    |
|Job Array Index        |`$SLURM_ARRAY_TASK_ID`   |
-- *Slide End* --

-- *Slide* --
### Part 0: Goals For This Afternoon
* Part 1: Advanced Linux Commands.
* Part 2: Regular Expressions.
* Part 3: Shells In General, Bash in Particular.
* Part 4: Variables, Loops, Conditionals, and Functions.
* Part 5: Shell Scripts with Slurm.
-- *Slide End* --

-- *Slide* --
### Part 1:  Archiving and Compressing Files
* Copy the file from `/usr/local/common/HPCshells/class.tar.gz` to the home directory.
* The double-barelled suffix, .tar.gz indicates that it is an archive ("tape archive"!) and compressed (with the gzip application). Such a file (often appearing as *.tgz) is often referred to as a "tarball".
* The type of a file can often be determined by the file command: `file class.tar.gz`
-- *Slide End* --

-- *Slide* --
### Part 1: Archiving and Compressing Files cont...
* To review the contents of a tarball (check for tarbombs!): `tar tf class.tar.gz`
* To recover from a tarbomb: `tar tf tarbomb.tar | xargs rm -rf`
* To extract (and compare value of compression): `tar xvf class.tar.gz`
* To create a tarball: `tar cvfz name.tar.gz directory/`
-- *Slide End* --

-- *Slide* --
### Part 1: Archiving and Compressing Files cont ...
* Another common compression algorithm that Linux users are likely to encounter with regularity is bzip2.
* Efficient in size, slower in decompression speed.
* To create a bzip2 tarball: `tar cvfj class.tar.bz2 class/`
* To check the contents: `tar tjf class.tar.gz` 
* To extract and uncompress the tarball : `tar xvf class.tar.bz2`
-- *Slide End* --

-- *Slide* --
### Part 1: Redirections and Tee
* A core principle of UNIX-like operating systems is that the output of one program should be usable as the input to another.
* The introductory lesson included basic commands for redirection, concatenation, and piping.
* Process streams as well as data streams can be redirected: `diff <(ssh user@spartan.hpc.unimelb.edu.au ls -R /home/lev/data) <(ls -R /home/lev/workdata)`
* The default behaviour is to accept inputs from the terminal (standard input) and display the results, either output or errors, to the terminal (standard output). 
-- *Slide End* --

-- *Slide* --
### Part 1: Redirections and Tee cont..
* Redirections can be further modified by placing a number next immediately before the redirector, which affects which stream is being used for redirection. These numbers are 0 for standard input, 1 for standard output and 2 for standard error. e.g., `ls -d /home/username/seismic 2> error.txt`
* Standard error can also to be redirected to the same destination that standard output is directed to using 2>&1; it merges stderr (2) into stdout (1).
-- *Slide End* --

-- *Slide* --
### Part 1: Redirections and Tee cont..
* The tee command copies standard input to standard output and also to any files included in the tee. When combined with pipes it takes input from a single direction and outputs it two directions. e.g.,  `who -u | tee whofile.txt | grep username`
-- *Slide End* --

-- *Slide* --
### Part 1: Redirections and Tee Summary
| Redirection Syntax                | Explanation                                                    |
|:----------------------------------|:--------------------------------------------------------------:|
|`command > file`                   | Redirect standard output to a file                             |
|`command >> file`                  | Redirect standard output to end of file                        |
|`command 2> file`                  | Redirect standard error to a file                              |
|`command > file 2>&1`              | Redirect standard output and standard error to file            |
-- *Slide End* --

-- *Slide* --
### Part 1: Redirections and Tee Summary cont..
| Redirection Syntax                | Explanation                                                    |
|:----------------------------------|:--------------------------------------------------------------:|
|`command -options < file`          | Redirect a file as standard input to a command                 |
|`command >> file 2>&1`             | Redirect standard and standard error to end of file            |
| <code>command &#124; command2</code>  | Pipe standard output to a second command                   |
-- *Slide End* --

-- *Slide* --
### Part 1: Redirections and Tee Summary cont..
| Redirection Syntax                | Explanation                                                    |
|:----------------------------------|:--------------------------------------------------------------:|
|<code>command 2>&1 &#124; command2</code>  | Pipe standard output and standard error to a second command    |
|<code>command1 &#124; tee file &#124; command2</code> | Apply command1 and command2 to file        |
-- *Slide End* --

-- *Slide* --
### Part 1: File Attributes, Types, Ownership
* The `ls -l` command illustrates file ownership (user, group), file type, permissions, and date when last modified.
* The first character is type; a "-" for a regular file, a "d" for a directory, and "l" for a symbolic link. Less common file types include "b" for block devices (e.g., hard drives, ram etc), "c" for character devices which stream data one character at a time (e.g., mice, keyboards, virtual terminals).
* In UNIX-like operating systems devices are a type of file as well, and are structured under the `/dev` directory. 
-- *Slide End* --

-- *Slide* --
### Part 1: File Attributes, Types, Ownership
*  Permissions are expressed in a block of three for "user, group, others" and for permission type (read r, write w, execute x). Executable also implies 'searching', thus "x" is usually found for directories as well.
* An "s" in the execute field indicated setuid. Causes any user or process to have access to system resources as though they are the owner of the file. If the bit is set for the group, the set group ID bit is set and the user running the program is given access based on access permission for the group the file belongs to.
-- *Slide End* --

-- *Slide* --
### Part 1: File Attributes, Types, Ownership cont
* There is "t", "save text attribute", or more commonly known as "sticky bit" in the execute field allows a user to delete or modify only those files in the directory that they own or have write permission for. A typical example is the /tmp directory, which is world-writeable.
* The change permissions of a file use the `chmod` command. To chmod a file you have to own it. The command is : chmod [option] [symbolic | octal] file. For options, the most common is `-R` or `--recursive` which changes files and directories recursively.
-- *Slide End* --

-- *Slide* --
### Part 1: File Attributes, Types, Ownership cont
* For symbolic notation, first establish the user reference, either "u" (user, the owner of the file), "g" (group, members of the file's group), "o" (others, neither the owner or group members), or "a" (all). If a user reference is not specified the operator and mode applies to all.
* Then determine the operation; either "+" (add the mode), "-" remove the mode, or "=" (equals, mode only equals that expression). Finally, specify the mode permissions as described above, "r" (read), "w" (write), "x" (execute), "s" (setuid, setgid), "t" (sticky). 
-- *Slide End* --

-- *Slide* --
### Part 1: File Attributes, Types, Ownership cont
* In octal notation a three or four digit base-8 value is presented derived from the sum of the component bits, so the equivalent of "r" in symbolic notation adds 4 in octal notation (binary 100), "w" in symbolic notation adds 2 in octal notation (binary 010) and "x" adds 1 in octal notation (binary 001). No permissions adds 0 (binary 000). For special modes the first octal digit is either set to 4 (setuid), 2 (setgid), or 1 (sticky). The sum of the three (or four components) thus makes up an alternative exact notation for the chmod command.
-- *Slide End* --

-- *Slide* --
### Part 1: File Attributes, Types, Ownership cont
* If you have root permission, you can make use of the `chown` (change owner) command. Usually group is optional on the grounds that users are usually provided ownership. A common use is to provide ownership to web-writeable directories e.g., (`chown -R www-data:www-data /var/www/files`). 
-- *Slide End* --

-- *Slide* --
### Part 1: File Attributes, Types, Ownership cont
* A `umask` ("user mask") which we encountered in the .bashrc limiting the permission modes for files and directories created by a process. When a program or script creates a file or directory, it specifies  permissions. Typical umask values are 022 (removing the write permission for the group and others) and 002 (removing the write permission for others).
-- *Slide End* --

-- *Slide* --
### Part 1: Links and File Content
* The ln command creates a link, associating one file with another. There are two basic types; a hard link (the default) and a symbolic link. 
* The core difference is that a hard link is a specific location of physical data, whereas a symbolic link is an abstract location of another file. Hard links cannot link directories and nor can they cross system boundaries; symbolic links can do both of these. 
* The general syntax for links is: `ln [option] source destination` .This most common option is `-s`, to create a symbolic link. The source is the original file. The destination is the link.
-- *Slide End* --

-- *Slide* --
### Part 1: Links and File Content cont...
* With a hard link: File1 -> Data1 and File2 -> Data1 . With a symbolic link: File2 -> File1 -> Data1
* A file consists of a filename and an inode reference. The reference maps to the actual inode. The inode contains the permissions, and data address. More than one filename can have the same inode reference
* Links are particularly useful if you want to share a file with another user, such as working on a collaborative paper (ensure that read/write access is granted). 
-- *Slide End* --

-- *Slide* --
### Part 1: File Manipulation Commands
* The command head and tail print the first and last ten lines of a file by default. The standard syntax is `[head..tail] [option] [file]`. The most typical option is `-n` for the number of lines. 
* Rename will rename the specified files by replacing the first occurrence of expression in their name by replacement. e.g., `rename .txt .bak *.txt`
-- *Slide End* --

-- *Slide* --
### Part 1: File Manipulation Commands cont...
* Split can be used to split large files into smaller components. The general syntax is `split [OPTION]... [INPUT [PREFIX]]`. Common options include byte (-b #) or linecount (-l #, default of 1000) for the new files. The input is the filename and the prefix is the output, PREFIXaa, PREFIXab etc.
-- *Slide End* --

-- *Slide* --
### Part 1: File Manipulation Commands cont...
* Sort will organise a text file into an order specified by options and output to a specific file, if desired. The general syntax is `sort [option] [input file] -o [filename]`. Some of the options include -b (ignore beginning spaces), -d (use dictionary order, ignore punctuation), -g (general, natural language), -m (merge two input files into one sorted output, -r (sort in reverse order) and -V (version number order).
* To filter repeated lines in a text file use uniq. The standard syntax is `uniq [options] [input file] [output file]`. 
-- *Slide End* --

-- *Slide* --
### Part 1: System Information Commands
* The du "disk usage' command has the standard syntax of `du [options] [file]`. Without any arguments du will print all files, entering directories recursively, and provide output in kilobytes. Most commonly experessed as `du -sh` (disk usage, summary form, human readable)
*  The following is a handy use of xargs is to parse a directory list and output the results to a file. The command script below runs a disk usage in summary, sorts in order of size and exports to the file diskuse.txt. The "\n" is to ignore spaces in filenames.
`du -sk * | sort -nr | cut -f2 | xargs -d "\n" du -sh  > diskuse.txt`
-- *Slide End* --

-- *Slide* -- 
### Part 1: System Information Commands cont...
* The command 'df' will generate a report of file system disk space usage.
* The command `free -h` provides total, used, and free memory on a system.
* A typical command to access system information is `uname`, with the simple syntax `uname [options]`. The most common command is uname -a (all) which provides, in order, kernel name, network node name, kernel release and version, machine hardware name, processor and hardware platform (if known), and operating system. 
-- *Slide End* --

-- *Slide* --
### Part 1: System Information Commands cont...
* Another useful source for system information is the /proc directory. The directory doesn't actually contain 'real' files but runtime system information. Examples: `less /proc/cpuinfo`, `less /proc/filesystems`, `less /proc/uptime`,
`less /proc/loadavg`, `less /proc/meminfo`, `less /proc/mounts`, `less /proc/partitions`
* The command `lscpu` will provide information about the processor architecture as well gathered from /proc/cpuinfo including the number of CPUs, threads, cores, and sockets. 
-- *Slide End* --

-- *Slide* --
### Part 2: Regular Expressions and Metacharacters
* The main text searching, substitution, and reporting tools are grep, sed (stream editor), and awk (programming language) respectively.
* Regular expressions have meta-characters, some of which are described below.

| Metacharacter | Explanation         | Example                                          |
|:--------------|:-------------------|:-----------------------------------------------|
| ^             | Beginning of line anchor   | `grep '^row' /usr/share/dict/words`       |
| $             | End of line anchor         | `grep 'row$' /usr/share/dict/words`       |
-- *Slide End* --

-- *Slide* --
### Part 2: Regular Expressions and Metacharacters cont..
| Metacharacter | Explanation        | Example   |
|---------------|--------------------|-----------|
| .             | Any single character       | `grep '^...row...$' /usr/share/dict/words` |
| *             | Match zero plus preceding characters | `grep '^...row.*' /usr/share/dict/words`   |
| [ ]           | Matches one in the set                 | `grep '^[Pp].row..$' /usr/share/dict/words`    |
-- *Slide End* --

-- *Slide* --
### Part 2: Regular Expressions and Metacharacters cont..
| Metacharacter | Explanation        | Example   |
|---------------|--------------------|-----------|
| [x-y]		| Matches on in the range                | `grep '^[s-u].row..$' /usr/share/dict/words`   |
| [^ ]          | Matches one character not in the set   |  `grep '^[^a].row..$' /usr/share/dict/words`   |
| `|`     | Logical OR   |  `grep '^[^a|P].row..$' /usr/share/dict/words`   |
-- *Slide End* --

-- *Slide* --
### Part 2: Regular Expressions and Metacharacters cont..
| Metacharacter | Explanation        | Example   |
|---------------|--------------------|-----------|
| [^x-y]        | Matches any character not in the range | `grep '^[^a-z].row..$' /usr/share/dict/words` |
| \             | Escape a metacharacter |  `grep '^A\.$' /usr/share/dict/words`
-- *Slide End* --

-- *Slide* --
### Part 2: Regular Expressions and Metacharacters cont...
* The 'matches one in the set' metacharacter has a number of options that one may find useful.

| Metacharacter| Explanation                                             |
|--------------|---------------------------------------------------------|
| [:digit:]    | Only the digits 0 to 9                                  |
| [:alnum:]    | Any alphanumeric character 0 to 9 OR A to Z or a to z.  | 
| [:alpha:]    | Any alpha character A to Z or a to z.                   |
| [:blank:]    | Space and TAB characters only.                          |
-- *Slide End* --

-- *Slide* --
### Part 2: Regular Expressions and Metacharacters cont...
* Metacharacters can be combined in an interesting manner with grep options. Examples; (i) using grep to count the number of empty lines in a file; `grep -c '^$' filename` (ii) a search for words with no vowels; `grep -v "[aeiou]" /usr/share/dict/words`
-- *Slide End* --

-- *Slide* --
### Part 2:  Text Manipulation with sed
* Sed makes text transformation on an input stream (e.g., file) and has the general form of `sed [OPTION] [SCRIPT] [INPUT]`. Some common options are `e` (multiple scripts per command), `-f` (add script file) and `-i` (in-place editing).
* The general form of a script is `Command/RegExp/Replacement/Flags`. The most common command is `s` for `substitute`, and the most common flags are `g` for global replacement thoughout each line and `I` to ignore case. 
* Sed has alternative three alternative delimiters in its scripts; '/', ':', or '|'
-- *Slide End* --

-- *Slide* --
### Part 2: Text Manipulation with sed cont...
| Command                | Explanation                                                              |
|------------------------|:-------------------------------------------------------------------------|
| `sed 's/^/     /'`       | Insert five whitespaces at the beginning of every line.                  | 
| `sed '/baz/s/foo/bar/g'` |  Substitute all instances of 'foo' with 'bar' on lines that start with 'baz' |
| `sed '/baz/!s/foo/bar/g'`| Substitute "foo" with "bar" except for lines which contain "baz" |
| `sed /^$/d`    | Delete all blank lines.                                                    |
| `sed s/ *$//` | Delete all spaces at the end of every line.             |
-- *Slide End* --

-- *Slide* --
###  Part 2: Text Manipulation with sed cont...
| Command               | Explanation                             |
|-----------------------|----------------------------------------|
| `sed -i 's/$/\r/g'`     | *nix to MS-Windows, adds CR.            | 
| `sed -i 's/\r$//g'`     | MS-Windows to *nix, removes CR          |

* A popular list of one-line sed commands can be found at the following URL 
http://sed.sourceforge.net/sed1line.txt
-- *Slide End* --

-- *Slide* --
###  Part 2: Report Presentation with awk
* Awk is a data driven programming language, its name derived from the surname initial of the designers (Alfred Aho, Peter Weinberger, and Brian Kernighan). Awk is particularly good at understanding and manipulating text structured by fields - such as tables of rows and columns. 
* The essential organization of an AWK program follows the form: pattern { action }. This is sometimes structured with BEGIN and END which specify actions to be taken before any lines are read, and after the last line is read. With it's structured data features, awk can print columns by number ($0 equals everything).
-- *Slide End* --

-- *Slide* --
### Part 2: Report Presentation with awk
* By default awk uses a space as the internal field separator. To use a comma invoke with `-F` e.g. `awk -F"," '{print $3}' quakes.csv`
* Adding new separators to the standard output print of multiple fields is recommended - otherwise AWK will print without any separators. For example; `awk -F"," '{print $1 " : " $3}' quakes.csv`
* Other commands can be piped through awk: `awk -F"," '{print $1 " : " $3 | "sort"}' quakes.csv | less`
-- *Slide End* --

-- *Slide* --
### Part 2: Report Presentation with awk cont...
* 'NR' specified the row number. More examples:
`awk -F"," 'END {print NR}' quakes.csv`    
`awk -F"," 'NR>1{print $3 "," $2 "," $1}' quakes.csv`   
`awk -F"," '(NR <2) || (NR!=6) && (NR<9)' quakes.csv > selection.txt`   
-- *Slide End* --

-- *Slide* --
### Part 2: Report Presentation with awk cont...
* Other useful awk one-liners make use of the arithmetic functions of this programming language:
* Print the total number of fields in $file.    
`awk '{totalf = totalf + NF }; END {print totalf}' $file`
* Print the sum of the fields (columns) of every line (row); NF is number of field.    
`awk '{sum=0; for (i=1; i<=NF; i++) sum=sum+$i; print sum}' $file`	
* A popular list of one-line awk commands can be found at the following URL   
`http://www.pement.org/awk/awk1line.txt`
-- *Slide End* --

-- *Slide* --
### Part 3: Shells and Login Files
* The default shell environment is the Bash shell (Bourne-again shell). The shell is a program that acts as command interpreter between the user and the kernel.
* When Bash is invoked as an interactive login shell it first reads and executes commands from the file `/etc/profile`. It looks for `~/.bash_profile`, `~/.bash_login`, and `~/.profile`, in that order, and reads and executes commands from the first one that exists and is readable.
-- *Slide End* --

-- *Slide* --
### Part 3: Shells and Login Files cont...
* Users can modify their `.bash_profile` to ensure that they have the environmental features that they want when they login.
* When a command is entered it is stored in `.bash_history`
* When a login shell exits, Bash reads and executes commands from the file `~/.bash_logout`, if it exists. 
-- *Slide End* --

-- *Slide* --
### Part 3: Example extended .bash_profile
* A sample extended `.bash_profile` is available from the directory `/usr/local/common/HPCshells`
* Includes alias, history size modifications etc.
-- *Slide End* --

-- *Slide* --
### Part 3: Various Shells
* Examples of various shells include the *nix-universal Bourne shell (sh) Bourne-Again shell (bash), Z shell (zsh), Korn shell (ksh), extended C shell (tcsh) and the friendly interactive shell (fish). There is even an amusing attempt to develop a shell into a text-based adventure game (Adventure shell, available at `http://nadvsh.sourceforge.net/`).
* To view what shells are available; `ls -l /bin/*sh*`
-- *Slide End* --

-- *Slide* --
### Part 3: Various Shells cont...
* Each have different features and often slightly different syntax, which is mostly beyond the scope of this course. However among bash and tsch the following are two major differences.

| Value       |    bash          |    tcsh             |
|-------------|------------------|--------------------|
|Variable     |  `var=val`       |  `set var=val`        |
|Environment  |  `export var=val`  |  `setenv var val`     | 
-- *Slide End* --

-- *Slide* --
### Part 3: Bash Shell Shortcuts
| Value       | Explanation                                                                     |
|-------------|:--------------------------------------------------------------------------------|
| ~           | Shortcut to user's home directory.                                              | 
| .           | The current directory.                                                          | 
| ..          | One level up in the file system hierarchy.                                      | 
| TAB         | Autocompletion suggestions.                                                     | 
| !!          | Repeat last typed command; can be combined with other commands.                 | 
| !ec	      | Repeat last typed command that started with 'ec'                                |
| &&          | Combine commands if the first succeeds (e.g., make && make install)                     | 
| &#124;&#124; | Alternative command if the first fails (e.g., make makefile1 &#124;&#124; make Makefile)  | 
-- *Slide End* --

-- *Slide* --
### Part 3: Bash Shell Shortcuts cont...
| Value       | Explanation                                                                     |
|-------------|:--------------------------------------------------------------------------------|
| ctrl+w      | Remove word behind cursor.                                                      | 
| ctrl+u      | Delete everything from cursor to beginning of the line                          | 
| alt+f       | Go forward to the end of the previous word                                      | 
| alt+b       | Move cursor back to the beginning of the previous word                          | 
| ctrl+d      | Quick logout.                                                                   | 
| ctrl+r      | Recursive search through your history to locate previous commands.              | 
| ctrl+z      | Stop the current process.                                                       |
-- *Slide End* --

-- *Slide* --
### Part 3: Use of Shell Scripting
* Shell scripts combine Linux commands with logical operations. It is an underrated utility, but it is not the answer for everything.
* They are not always great at resource intensive tasks (e.g., extensive file operations) where speed is important. They are certainly not recommended for heavy-duty mathematical operations (e.g., floating point) - use programming language instead. They are not recommended in situations where data structures, multi-dimensional arrays (it's not a database!) and port/socket I/O is important. 
-- *Slide End* --

-- *Slide* --
### Part 3: Scripts with Variables
*  The most basic form of scripting simply follows commands in sequence, such as this rather undeveloped backup script, which runs tar and gzip on the home directory. A version of this is available at: `/usr/local/common/HPCshells/backup1.sh`
* Not much of a script! Consider what parts can be made into variables. `/usr/local/common/HPCshells/backup2.sh`
* A variable is prefaced by a dollar sign ($) to refer to its value. 
-- *Slide End* --

-- *Slide* --
### Part 3: Special Characters
* There are also a number of special characters in bash scripting. 
* Quoting disables these characters for the content within the quotes. Both single and double quotes can be used, and single quotes can be used to incorporate double quotes. 
* "Backtick" quotation marks can be used for command substitution within the script, but they are not POSIX standard. 
* Examples: 
`echo 'The "Sedimentary" and the "Igenuous" argue about metamorphism'`   
`echo "There are $(ls | wc -l) files in $(pwd)"`
-- *Slide End* --

-- *Slide* --
### Part 3: Scripts with Loops
* In addition to variable assignments, bash scripting allows for loops (for/do, while/do, util/do). 
* The for loop executes stated commands for each value in the list.
* The while loop allows for repetitive execution of a list of commands, as long as the command controlling the while loop executes successfully.
* The until loop executes until the test condition executes successfully.
-- *Slide End* --

-- *Slide* --
### Part 3: Scripts with Loops cont...
* See simple `for` loop example in `/usr/local/common/OpenFOAM/cavity/Allclean`
* More examples of these scripts are in  `/usr/local/common/HPCshells/loops.txt`
* These can be converted to permanent scripts e.g., `/usr/local/common/HPCshells/lowercaserename.sh` and `/usr/local/common/HPCshells/sshtrigger.sh`
-- *Slide End* --

-- *Slide* --
### Part 3: Scripts with Conditionals
* A set of conditions can be expressed through an if/then/fi structure. A single test with an alternative set of commands is expressed if/then/else/fi. Finally, a switch-like structure can be constructed through a series of elif statements in a if/then/elif/elif/.../else/fi structure. i.e.,
1. if..then..fi statement (Simple) 
2. if..then..else..fi statement (Optional) 
3. if..elif..else..fi statement (Ladder) 
4. if..then..else..if..then..fi..fi..(Nested) 
* An example is available at: `/usr/local/common/HPCshells/filetest.sh`
-- *Slide End* --

-- *Slide* --
### Part 3: Scripts with Conditionals cont...
* There are several conditional expressions that could be used to test with the files. The following are few common examples; 

| Value                           |Explanation                                                   |
|---------------------------------|-------------------------------------------------------------|
| [ -e filepath ]                 | Returns true if file exists.                                 |
| [$var lt value ] [ gt ] [ eq ]  | Returns true if less than, greater than or equal             |
| [ -f filepath ]                 | Returns true if filepath is actually a file.                 |
| [ -x filepath ]                 | Returns true if file exists and executable.                  |
-- *Slide End* --

-- *Slide* --
### Part 3: Scripts with Conditionals cont...
| Value                           |Explanation                                                   |
|---------------------------------|-------------------------------------------------------------|
| [ -S filepath ]                 | Returns true if file exists and its a socket file.           |
| [ expr1 -a expr2 ]              | Returns true if both the expression is true.                 |
| [ expr1 -o expr2 ]              | Returns true if either of the expression1 or 2 is true.      | 
-- *Slide End* --

-- *Slide* --
### Part 3: Scripts with Conditionals cont...
* Conditionals can also be interrupted and resumed using the 'break' and 'continue' statements. The break command terminates the loop (breaks out of it), while continue causes a jump to the next iteration (repetition) of the loop, skipping all the remaining commands in that particular loop cycle. Examples at: `/usr/local/common/HPCshells/break.sh` and `/usr/local/common/HPCshells/continue.sh`
* A variant on the conditional to escape the problems associated with deeply nested if-then-else statements is the `case` statement. The first match executes the listed commands. Examples at: `/usr/local/common/HPCshells/case.sh`
-- *Slide End* --

-- *Slide* --
### Part 3: Script Selects and Functions
* The select command with conditionals can be used to create simple menus for users which prompts them for their input. There is an example at: `/usr/local/common/HPCshells/select.sh`
* Functions subroutines or subscripts within a shell script, which can have local variables, accept, and return parameters. Functions may not be empty. See the example at: `/usr/local/common/HPCshells/hellofunction.sh`
* See also example of functions in `/usr/local/common/OpenFOAM/cavity/Allrun`
-- *Slide End* --

-- *Slide* --
### Part 3: Scripting Conventions
* There are several scripting conventions which make the code more effective, more robust, more portable, and more readable. Therefore use them!
* The following example at: `/usr/local/common/HPCshells/findemails.sh` and the datafile `/usr/local/common/HPCshells/hidden.txt` will illustrate some of these conventions.
-- *Slide End* --

-- *Slide* --
### Part 3: Scripting Conventions cont...
* Liberally comment your code so that other readers know what it does. Use explicit variable names. Use output to tell the user what is happening. Use variables when appropriate rather than hard-coded paths. Provide exit statements to clear variables and provide an error code.
* A common conditional, and sadly often forgotten, is whether or not a script has the requiste files for input and output specified!
* Invite user input with the 'read' command; protect against escape characters with the 'raw' option.
-- *Slide End* --

-- *Slide* --
### Part 3: Metacharacters
* Metacharacters have meaning beyond their literal meaning. Powerful, but use with caution (e.g., wildcards). Metacharacter meaning depends very much on the context, which can cause problems. For example;
* the semi-colon can be a command separator in a script or a double as a terminator in a case statement. 
* the colon represents a null command in a script, or as a field separator (e.g., in `/etc/passwd`).
* the dot (.) is used to source a filename, to represent the current working directory as a path, to represent a character in regular expression, or in multiple form as a sequence.
-- *Slide End* --

-- *Slide* --
### Part 3: Metacharacters cont ..
* Single quotes however will interpret anything literally between the quotes as a string with no interpretation to a meta-character (aka 'strong quoting'). Double quotes will substitute a limited set which are usually the symbols which are wanted in their interpreted mode. e.g., variables, backticks, and sometimes backslash escapes. (aka "weak quoting"). n example is given at `/usr/local/common/HPCshells/quotes.sh`
-- *Slide End* --

-- *Slide* --
### Part 3: Metacharacters cont ..
* In some cases backtics are seen for command substitution. This is not a POSIX standard, it does exist for historical reasons. Nesting commands with backticks also requires escape characters; the deeper the nesting the more escape characters required. e.g., echo "Hello, $(whoami)".
-- *Slide End* --

-- *Slide* --
### Part 3: Script Commands
* A script can also be initiated in the background with an ampersand. 
* The commands `fg` (foreground) and `bg` (background) are complementary manipulations of processes.  Jobs can be suspended with Cntrl-Z to return to the terminal. 
* A background job can be killed with `kill %job-number`. A listing of jobs can be achieved with the `jobs` command.
-- *Slide End* --

-- *Slide* --
### Part 3: Script  Commands cont...
* For example;
`eval 'for i in {1..100}; do sleep 2; echo "Igneous" >> rocks.txt ; done' &`    
`eval 'for i in {1..100}; do sleep 2; echo "Sedimentary" >> rocks.txt ; done'`    
`eval 'for i in {1..100}; do sleep 2; echo "Metamorphic" >> rocks.txt ; done' &`    
* It is important not to run large scripts on the login node. Set up a job on a compute node with `sinteractive`.
-- *Slide End* --

-- *Slide* --
### Part 4: Shell Scripting Example with Slurm
* Because SLURM calls a shell when launched any shell commands can can also be used in a Slurm script. 
* As an example, an MD Drug Docking experiment, MD3 -  Aspirin to A2 phospholipase, includes a range of Linux commands and shell script structures. This includes variable assignment, redirections, and loops. This job can be copied to a local directory and lauched like any other Slurm job. The jobscript and data files are at: `/usr/local/common/HPCshells/NAMD/drugdock.Slurm`
-- *Slide End* --

-- *Slide* --
### Part 4: Automatic Script Generation
* A heredoc (also known as a here-string or here-document) is a file or input literal, a section of source code that is treated as a separate file with specified delimiters. In various Unix shells the '<<' with a delimiter name will treat subsequent code until the identifier as reached as a separate file. With the addition of a minus sign, leading tabs are ignored which aid formatting. 
-- *Slide End* --

-- *Slide* --
### Part 4: Automatic Script Generation cont...
* For example, the command `tr a-z A-Z << END_TEXT` will conduct a translate on all data until a END_TEXT is reached in the doc for or `tr a-z A-Z <<< 'igneous sedimentary metamorphic'` in the string form. Variables can also be parsed. e.g.., `rocks='igneous sedimentary metamorphic'`, `tr a-z A-Z <<< $rocks`. 
* Heredocs can also be used however to create Slurm scripts. A loop can be used to create multiple jobs for submission. See `/usr/local/common/HPCshells/heres/herescript.sh`. See also `/usr/local/common/Gaussian`
-- *Slide End* --

