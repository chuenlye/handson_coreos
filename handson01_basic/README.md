# fleetctl
 - command line client of fleet to manage the whole cluster
 - can be used from any node of cluster
 - can be used from your local laptop ! 

## how to use fleetctl from your laptop
using `--tunnel` option or enviroment variable `FLEETCTL_TUNNEL`

  $ ssh-add ~/.ssh/${YOUR_PRIVATE_KEY}

  cat >> ~/.bashrc <<EOF
  export FLEETCTL_TUNNEL=IP_OF_ANY_HOST_IN_CLUSTER
  EOF
  source ~/.bashrc

## useful commands

    $ fleetctl start myfirst.service
    or 
    $ fleetctl start *.service

    fleet start == fleetctl submit + fleet load + fleetctl start

    $ fleetctl list-units
    $ fleetctl list-units -l
    $ fleetctl cat myfirst.service
    $ fleetctl list-machines
    $ fleetctl list-machines -l
    $ fleetctl journal myfirst.service
    $ fleetctl journal -f myfirst.service
    $ fleetctl destroy myfirst.service
    $ fleetctl destroy *.service  #全部のcontainerを一括で削除してclean環境に戻って楽です！

    fleetctl destroy == fleetctl stop + fleetctl unload + fleetctl destroy

    $ fleetctl debug-info

    fleetctl sshでserverにlogin:
    $ fleetctl ssh myfirst.service/MACHINE_ID

    Loginしてからclusterのetcd情報を確認：
    $ etcdctl ls --recursive
    $ etcdctl get SOME_KEY

