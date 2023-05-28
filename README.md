# riris
Remote InterSystems IRIS command execution
This is a simple py script (meant to be run from CLI) that uses the "irisnative" module and allow you to execute a variety of things on a remote iris instance.
We are all good to execute things on the instance that is installed on the local machine, but what do you need to do to get something done on a remote server?
With RIRIS you can do this in an easy way. You can script it with bash or other, or you can import the module

# installation
You need to have python 3 installed and also the irisnative module
After that there's no need of installing the application, it's just a single py file

# Help
`
usage: riris [-H] [-h host] [-s port] [-n namespace] [-u user] [-p password] [-v]
             {cls,rtn,set,get,kil,cod,sql} ...

common options:
  -H, --help                           Print this help
  -h host, --host host                 Destination host
  -s port, --port port                 Destination port
  -n namespace, --namespace namespace  Namespace
  -u user, --user user                 IRIS username
  -p password, --password password     IRIS password, if omitted it will be requested
  -v, --verbose                        Verbosity


specific options:
  cls
    Run a class method
    usage: riris cls [-H] [cname] [method] [arguments ...]
    arguments:
      cname       Class to be called
      method      Method to be called
      arguments   Method parameters
    examples:
      ./riris -h iris-server -p SYS cls %Library.Utility Date 5

  rtn
    Run a routine
    usage: riris rtn [-H] [fname] [rname] [arguments ...]
    arguments:
      fname       Funciton to be called
      rname       Routine to be called
      arguments   Routine parameters
    examples:
      ./riris -h iris-server -p SYS -n user rtn ^zcustomtst

  set
    Set a global
    usage: riris set [-H] [value] [gname] [subscripts ...]
    arguments:
      value       Value
      gname       Global name
      subscripts  Global subscripts
    examples:
      ./riris -h iris-server -p SYS set 1 ^pTest
      ./riris -h iris-server -p SYS set 1 ^pTest ciao

  get
    Get a global
    usage: riris get [-H] [-r | -j] [gname] [subscripts ...]
    arguments:
      gname             Global name
      subscripts        Global subscripts
    examples:
      ./riris -h iris-server -p SYS get ^pTest
      ./riris -h iris-server -p SYS get -r ^pTest
      ./riris -h iris-server -p SYS get -j ^pTest
      ./riris -h iris-server -p SYS get ^pTest("1")

  kil
    Kill a global
    usage: riris kil [-H] [gname] [subscripts ...]
    arguments:
      gname       Global name
      subscripts  Global subscripts
    examples:
      ./riris -h iris-server -p SYS kil ^pTest ciao
      ./riris -h iris-server -p SYS kil ^pTest

  cod
    Run code in a textfile
    usage: riris cod [-H] -U [OS_USERNAME] -P [OS_PASSWORD] [-L] [file]
    arguments:
        -H, --help                                     Print this help
        -U [OS_USERNAME], --os-username [OS_USERNAME]  Remote OS username
        -P [OS_PASSWORD], --os-password [OS_PASSWORD]  Remote OS password
        -L, --log                                      Log to file
        file                                           File with code to be executed
    examples:
      ./riris -h iris-server -p SYS cod -U root -P trakcare -L ./test_code
      where test_code contains:
        k ^zdbg
        s ^zdbg="done with riris code!!!"
        w ^zdbg

  sql
    Run sql code (without jdbc)
    usage: riris sql [-H] -U [OS_USERNAME] -P [OS_PASSWORD] [sql ...]
    arguments:
        -H, --help                                     Print this help
        -U [OS_USERNAME], --os-username [OS_USERNAME]  Remote OS username
        -P [OS_PASSWORD], --os-password [OS_PASSWORD]  Remote OS password
        sql                                            SQL query to be executed
    examples:
      ./riris -h iris-server -p SYS sql -U root -P trakcare ./test_sql
      ./riris -h iris-server -p SYS sql -U root -P trakcare select \* from Config.confg
      where test_sql contains:
        select \* from Config.confg
`
