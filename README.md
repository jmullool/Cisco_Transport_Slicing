# Cisco Transport Slicing- Setup and Sample Payloads for Various Slicing Use-cases 

This is a repo of sample payloads and usage for deploying Cisco's Transport Slicing Solution with Cisco's Network Services Orchestrator (NSO).
The Slicing YANG model is based off of an early version of the IETF work specified here: 
https://datatracker.ietf.org/doc/html/draft-ietf-teas-ietf-network-slice-nbi-yang-03

Long term, Cisco will trying to maintain compatibility between models, but some differences are exist as Cisco has augmented the model to support additional
optional parameters. 

## Prerequisits

It is assumed you have a working NSO 6.1 System with the latest T-SDN CFP loaded. Additionally, you optionally can have a CNC5.0 system installed which includes NSO 6.1 and the required T-SDN CFPs.


## Installing and Verifying the Slicing package

Place the ncs-6.1-ietf-network-slice-service-EXAMPLE-5.0.0.tar.gz file into your running directory's packages folder on NSO. Then do a package-reload command at the NCS CLI. Verify that the package is "UP".

```
admin@ncs-6.1# packages reload
...

reload-result {
    package ietf-network-slice-service
    result true
}

.....

admin@ncs-6.1# show packages package oper-status 
                                                                                                                             PACKAGE                          
                                               PROGRAM                                                                       META     FILE                    
                                               CODE     JAVA           PYTHON         BAD NCS  PACKAGE  PACKAGE  CIRCULAR    DATA     LOAD   ERROR            
NAME                                       UP  ERROR    UNINITIALIZED  UNINITIALIZED  VERSION  NAME     VERSION  DEPENDENCY  ERROR    ERROR  INFO   WARNINGS  
--------------------------------------------------------------------------------------------------------------------------------------------------------------
cisco-aa-service-assurance                 X   -        -              -              -        -        -        -           -        -      -      -         
cisco-cs-sr-te-cfp                         X   -        -              -              -        -        -        -           -        -      -      -         
cisco-flat-L2vpn-fp-internal               X   -        -              -              -        -        -        -           -        -      -      -         
cisco-flat-L3vpn-fp-internal               X   -        -              -              -        -        -        -           -        -      -      -         
cisco-internet-access-service-fp           X   -        -              -              -        -        -        -           -        -      -      -         
cisco-internet-access-service-fp-internal  X   -        -              -              -        -        -        -           -        -      -      -         
cisco-ios-cli-6.86                         X   -        -              -              -        -        -        -           -        -      -      -         
cisco-iosxr-cli-7.45                       X   -        -              -              -        -        -        -           -        -      -      -         
cisco-iosxr-nc-7.7                         X   -        -              -              -        -        -        -           -        -      -      -         
cisco-pm-fp                                X   -        -              -              -        -        -        -           -        -      -      -         
cisco-pm-fp-internal                       X   -        -              -              -        -        -        -           -        -      -      -         
cisco-rsvp-te-fp                           X   -        -              -              -        -        -        -           -        -      -      -         
cisco-sr-te-cfp                            X   -        -              -              -        -        -        -           -        -      -      -         
cisco-sr-te-cfp-internal                   X   -        -              -              -        -        -        -           -        -      -      -         
cisco-tm-tc-fp                             X   -        -              -              -        -        -        -           -        -      -      -         
cisco-tsdn-core-fp-common                  X   -        -              -              -        -        -        -           -        -      -      -         
core-fp-common                             X   -        -              -              -        -        -        -           -        -      -      -         
core-fp-delete-tag-service                 X   -        -              -              -        -        -        -           -        -      -      -         
core-fp-plan-notif-generator               X   -        -              -              -        -        -        -           -        -      -      -         
custom-template-utils                      X   -        -              -              -        -        -        -           -        -      -      -         
cw-device-auth                             X   -        -              -              -        -        -        -           -        -      -      -         
cw-dlm-fp                                  X   -        -              -              -        -        -        -           -        -      -      -         
ietf-l2vpn-nm                              X   -        -              -              -        -        -        -           -        -      -      -         
ietf-l3vpn-nm                              X   -        -              -              -        -        -        -           -        -      -      -         
ietf-network-slice-service                 X   -        -              -              -        -        -        -           -        -      -      -         
ietf-te-fp                                 X   -        -              -              -        -        -        -           -        -      -      -         
lsa-utils                                  X   -        -              -              -        -        -        -           -        -      -      -         
resource-manager                           X   -        -              -              -        -        -        -           -        -      -      -         
```

### One-time configurations to set-up the system:


```
test line

```

Example:
```
test line
```
#### Test



