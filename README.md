# A robust, vagrantized, docker based dev environment

This is research on creating developer environments that are trivially
deployable and flexible to use.


The main goals are to creatae an environment that is

1. Trivially deployabe:
   The less steps the better. We assume Vagrant and VirtualBox running
   correctly and nothing else. To achieve this we try to stick to
   standarizations of managing infrastructure and application lifecycles
   (vagrant and docker respectively).
    1. Vagrant has become a de-facto industry standard for (dev-)infrastructure
       lifecycle management, so we use it to shrink the dev environment setup
       steps to the one `vagrant up`.
    1. Docker is the current leader in standardizing an applications lifecycle
       (or if You wish a processes lifecycle) and service level interaction
       into a standard vocabulary. Also capable of dealing as a name based
       service discovery agent.
1. Understandable
   The set up needs to be as declarative as possible. Succinctness is also a
   big plus. The initial goal is to encode as much of the target environments
   details into the Stock `Vagrantfile`.
1. Robust
   The resulting environment must be failure resistant across as many hosts as
   possible as well as guarantee reliable builds in the future. It is very
   often the case that an update to a vagrant box or docker containers base
   leads to failing environment builds.
   To eliminate this we should keep two things in mind:
    * Package manager updates make environments
      non-deterministic.
    * Explicit version pinning is a hard requirement for
      guaranteeing environment consistency. Even soft
      version pinning (eg: matching for same major version
      on a linux distro) cannot guarantee future
      interference.


## Notes

### Sudo requirement

Mac and Linux users will have to provide sudo credentials during
`vagrant up` and `vagrant reload` operations since the host NFS
daemon will be restarted during provisioning to share the
project directory with the host.


### NFS

Our OS of choice, CoreOS does not provide VirtualBox shared
folders due to the lack of VB guest extensions. The CoreOS Linux
developers opt for NFS mounting the project directory instead.
This means that **You MUST have NFS Deamon installed**. But
this shouldn be provided oob for most Linuxes and MacOSs.


### Windows users

> Windows users should change to a Linux based OS. The author
> recommends ArchLinux and Debian.

Joke aside, there are some extra things Windows users need to do:

* Vagrant NFS mounting capability.
  Vagrant on Windows cannot do NFS oob. so You will need to
  install the Vagrant Windows NFS plugin from Github:
  https://github.com/winnfsd/vagrant-winnfsd
  Alternatively:
  https://github.com/coreos/bugs/issues/1358

