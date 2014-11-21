# Handson README
This handson uses the variable of `%i` to demonstrate usage of template for port management.

%i: this is the string between the "@" character and the suffix of the unit name. e.g. given unit file name of "apache1@80.service", value of %i == 80

At first, write a template file: apache.service.template 

and then create several symbolic files pointing to this template file:

      ln -s apache.service.template apache1@80.service
      ln -s apache.service.template apache2@80.service
      ln -s apache.service.template apache3@80.service
      ln -s apache.service.template apache4@8001.service
      ln -s apache.service.template apache5@8001.service
      ln -s apache.service.template apache6@8002.service

Next, use fleetctl to launch services:

      $ fleetctl start *.service
      $ fleetctl list-units
      UNIT          STATE       LOAD    ACTIVE  SUB DESC        MACHINE
      apache1@80.service    launched    loaded  active  running Apache Frontend 34aa3ef6.../${IPADDRESS1}
      apache2@80.service    launched    loaded  active  running Apache Frontend ba04d7eb.../${IPADRESS2}
      apache3@80.service    launched    loaded  active  running Apache Frontend cff39c03.../${IPADDRESS3}
      apache4@8001.service  launched    loaded  active  running Apache Frontend ba04d7eb.../${IPADRESS2}
      apache5@8001.service  launched    loaded  active  running Apache Frontend 34aa3ef6.../${IPADDRESS1}
      apache6@8002.service  launched    loaded  active  running Apache Frontend ba04d7eb.../${IPADRESS2}


#A reference on unit varibles

## systemd specifiers

When evaluating the `[X-Fleet]` section, fleet supports a subset of systemd's [specifiers][systemd specifiers] to perform variable substitution. The following specifiers are currently supported:

* `%n`
* `%N`
* `%p`
* `%i`

For the meaning of the specifiers, refer to the official [systemd documentation][systemd specifiers].

[systemd specifiers]: http://www.freedesktop.org/software/systemd/man/systemd.unit.html#Specifiers

