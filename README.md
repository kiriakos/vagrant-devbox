# A robust, vagrantized, docker based dev environment

This is research on creating developer environments that
are trivially deployable nad flexible to use.

The main goals are to creatae an environment that is

1. Trivially deployabe:
   The less steps the better. We assume Vagrant and VirtualBox 
   running correctly and nothing else. To achieve this we try
   to stick to standarizations of managing infrastructure and
   application lifecycles (vagrant and docker respectively). 
    1. Vagrant has become a de-facto industry standard for 
       (dev-)infrastructure lifecycle management, so we use it
       to shrink the dev environment setups steps to the one
       `vagrant up`
    1. Docker is the current leader in standardizing an
       applications lifecycle (or if You wish a processes 
       lifecycle) and service level interaction into a 
       standard vocabulary. Also capable of dealing as a
       name based service discovery agent.
1. Understandable
   The set up needs to be as declarative as possible. 
   Succinctness is also a big plus.
   The initial goal is to encode as much of the target
   environments details into the Stock `Vagrantfile`
1. Robust
   The resulting environment must be failure resistant
   across as many hosts as possible as well as guarantee
   reliable builds in the future. It is very often the case
   that an update to a vagrant box or docker containers base
   leads to failing environment builds. 
   To eliminate this we should keep two things in mind:
    * Package manager updates make environments 
      non-deterministic.
    * Explicit version pinning is a hard requirement for 
      guaranteeing environment consistency. Even soft 
      version pinning (eg: matching for same major version
      on a linux distro) cannot guarantee future 
      interference.


    



