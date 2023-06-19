Per-Flow Slicing Example and prep.

Goal: 
Have DSCP Best Effort traffic (DSCP 0) follow the eMBB SR-TE path (color 100)
Have DSCP High Priority traffic (DSCP 46) follow the URLLC SR-TE path (color 110).

Pre-requesets:

(1) per-flow bsid range must be setup on each PE:
mpls label blocks
 block name per-flow-bsid-block type pfp start 40000 end 41000 client any
!

(2) proper input QoS policy maps must be built. The below policy map worked on the NCS5500, though it's unclear if they are working or just 
the default classification behaviour on the PEs are setting the EXP via default dscp--exp mapping where exp then sets forwarding-class (FC)
! 
policy-map per-flow-test
 class PRIORITY
  set mpls experimental imposition 5
  set traffic-class 5
 ! 
 class Best_Effort
  set mpls experimental imposition 0
  set traffic-class 0
 ! 
 class class-default
 ! 
 end-policy-map
! 

(3) Ensure that a headless odn template called DSC_Flow for color 500 has been created in the sr-te:
cisco-sr-te-cfp:sr-te odn odn-template DSCP_Flow
 color 500
! 

(4) Build the proper slicing template:
network-slice-services slo-sle-templates slo-sle-template DSCP_Flow
 template-description    "For L3 Slices: DSCP Flow Based Path Forwarding Selection DSCP EF --> URLLC, other-->eMBB"
 qos-policy L3 input-policy per-flow-test
 qos-policy L3 output-policy Egress-LowLatency
 forwarding-plane-policy DSCP_Flow
 service-assurance heuristics monitoring-state enable
 service-assurance heuristics L3 profile-name "Gold_L3VPN_ConfigProfile system"
 service-assurance heuristics L3 rule-name "Rule-L3VPN-NM system"
!

(5) via NSO load these two pre-req files in proper order to pre-configure headends with proper ODN templates:
load merge q_per-flow-prereq-odn_headends_1.cli
load merge q_per-flow-prereq-odn_headends_2.cli

It is assumed that the ODN templates have already been built and in the first prereq file we are just adding the manual headends.

Note: These files are required becuase (a) sr-te CFP does not support per-flow commands for color 500 and
(b) slicing package does not support per-flow slicing thus colors 100 and 110 are not dynamically loaded.


(4) Deploy the slice
load merge q_L3_A2A_dedicated_DSCP_Flow.cli


Test the per-flow behavior by pinging with different DSCPs from end system:

DSCP=0 by default, notice this traffic round-trip time is ~20ms which is characteristic of eMBB path:
ATL-CE#
ATL-CE#ping 172.16.1.12
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 172.16.1.12, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 21/21/22 ms


Now test DSCP=46 (EF) and notice the round-trip time is ~2ms which is characteristic of URLLC low delay path:


ATL-CE#ping 
Protocol [ip]: 
Target IP address: 172.16.1.12
Repeat count [5]: 
Datagram size [100]: 
Timeout in seconds [2]: 
Extended commands [n]: y
Ingress ping [n]: 
Source address or interface: 
DSCP Value [0]: 46
Set DF bit in IP header? [no]: 
Validate reply data? [no]: 
Data pattern [0x0000ABCD]: 
Loose, Strict, Record, Timestamp, Verbose[none]: 
Sweep range of sizes [n]: 
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 172.16.1.12, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 2/2/3 ms
ATL-CE#
ATL-CE#
ATL-CE#


Cleanup:

delete the slice:
admin@ncs-6.1(config)# no network-slice-services slice-service slice-L3-ACME 


Clean up the static ODN templates that were configured:
admin@ncs-6.1(config)#load merge  q_per-flow-cleanup-odn_headends.cli


Show commands:

segment-routing
 traffic-eng
  on-demand color 100
   dynamic
    pcep
    !
    metric
     type igp
    !
   !
  !
  on-demand color 110
   dynamic
    pcep
    !
    metric
    !
   !
   constraints
    segments
     sid-algorithm 128
    !
   !
  !
  on-demand color 500
   per-flow
    forward-class 0 color 100
    forward-class 1 color 100
    forward-class 5 color 110
   !      
  !       

P/0/RP0/CPU0:Node-4#show segment-routing traffic-eng policy 
Sun Mar  5 21:31:31.333 UTC

SR-TE policy database
---------------------

Color: 500, End-point: 192.168.255.21
  Name: srte_c_500_ep_192.168.255.21
  Status:
    Admin: up  Operational: up for 00:25:39 (since Mar  5 21:05:51.407)
  Candidate-paths:
    Preference: 100 (BGP ODN) (active)
      Requested BSID: dynamic
      Per-flow Information:
        Forward     PDP     PDP 
          Class   Color  Status 
        ------- ------- ------- 
              0     100      Up 
              1     100      Up 
              5     110      Up 
        Default Forward Class: 0
  Attributes:
    Binding SID: 40105
    Forward Class: Not Configured
    Steering labeled-services disabled: no
    Steering BGP disabled: no
    IPv6 caps enable: yes
    Invalidation drop enabled: no
    Max Install Standby Candidate Paths: 0

Color: 100, End-point: 192.168.255.21
  Name: srte_c_100_ep_192.168.255.21
  Status:
    Admin: up  Operational: up for 00:25:39 (since Mar  5 21:05:51.400)
  Candidate-paths:
    Preference: 200 (SR-TE ODN) (inactive) (shutdown)
      Requested BSID: dynamic
      Constraints:
        Protection Type: protected-preferred
        Maximum SID Depth: 12 
      Dynamic (inactive)
        Metric Type: IGP,   Path Accumulated Metric: 0 
    Preference: 100 (SR-TE ODN) (active)
      Requested BSID: dynamic
      PCC info:
        Symbolic name: srte_c_100_ep_192.168.255.21_discr_100
        PLSP-ID: 196
      Constraints:
        Protection Type: protected-preferred
        Maximum SID Depth: 12 
      Dynamic (pce 192.168.255.7) (valid)
        Metric Type: IGP,   Path Accumulated Metric: 25000 
          16105 [Prefix-SID, 192.168.255.21]
  Attributes:
    Binding SID: 24023
    Forward Class: Not Configured
    Steering labeled-services disabled: no
    Steering BGP disabled: no
    IPv6 caps enable: yes
    Invalidation drop enabled: no
    Max Install Standby Candidate Paths: 0

Color: 110, End-point: 192.168.255.21
  Name: srte_c_110_ep_192.168.255.21
  Status:
    Admin: up  Operational: up for 00:25:39 (since Mar  5 21:05:51.400)
  Candidate-paths:
    Preference: 200 (SR-TE ODN) (inactive) (shutdown)
      Requested BSID: dynamic
      Constraints:
        Prefix-SID Algorithm: 128
        Protection Type: protected-preferred
        Maximum SID Depth: 12 
      Dynamic (inactive)
        Metric Type: TE,   Path Accumulated Metric: 0 
    Preference: 100 (SR-TE ODN) (active)
      Requested BSID: dynamic
      PCC info:
        Symbolic name: srte_c_110_ep_192.168.255.21_discr_100
        PLSP-ID: 197
      Constraints:
        Prefix-SID Algorithm: 128
        Protection Type: protected-preferred
        Maximum SID Depth: 12 
      Dynamic (pce 192.168.255.7) (valid)
        Metric Type: LATENCY,   Path Accumulated Metric: 3 
          16805 [Prefix-SID, 192.168.255.21]
  Attributes:
    Binding SID: 24024
    Forward Class: Not Configured
    Steering labeled-services disabled: no
    Steering BGP disabled: no
    IPv6 caps enable: yes
    Invalidation drop enabled: no
    Max Install Standby Candidate Paths: 0

Color: 500, End-point: 192.168.255.23
  Name: srte_c_500_ep_192.168.255.23
  Status:
    Admin: up  Operational: up for 00:25:39 (since Mar  5 21:05:51.407)
  Candidate-paths:
    Preference: 100 (BGP ODN) (active)
      Requested BSID: dynamic
      Per-flow Information:
        Forward     PDP     PDP 
          Class   Color  Status 
        ------- ------- ------- 
              0     100      Up 
              1     100      Up 
              5     110      Up 
        Default Forward Class: 0
  Attributes:
    Binding SID: 40108
    Forward Class: Not Configured
    Steering labeled-services disabled: no
    Steering BGP disabled: no
    IPv6 caps enable: yes
    Invalidation drop enabled: no
    Max Install Standby Candidate Paths: 0

Color: 100, End-point: 192.168.255.23
  Name: srte_c_100_ep_192.168.255.23
  Status:
    Admin: up  Operational: up for 00:25:39 (since Mar  5 21:05:51.400)
  Candidate-paths:
    Preference: 200 (SR-TE ODN) (inactive) (shutdown)
      Requested BSID: dynamic
      Constraints:
        Protection Type: protected-preferred
        Maximum SID Depth: 12 
      Dynamic (inactive)
        Metric Type: IGP,   Path Accumulated Metric: 0 
    Preference: 100 (SR-TE ODN) (active)
      Requested BSID: dynamic
      PCC info:
        Symbolic name: srte_c_100_ep_192.168.255.23_discr_100
        PLSP-ID: 198
      Constraints:
        Protection Type: protected-preferred
        Maximum SID Depth: 12 
      Dynamic (pce 192.168.255.7) (valid)
        Metric Type: IGP,   Path Accumulated Metric: 10000 
          16102 [Prefix-SID, 192.168.255.23]
  Attributes:
    Binding SID: 24025
    Forward Class: Not Configured
    Steering labeled-services disabled: no
    Steering BGP disabled: no
    IPv6 caps enable: yes
    Invalidation drop enabled: no
    Max Install Standby Candidate Paths: 0

Color: 110, End-point: 192.168.255.23
  Name: srte_c_110_ep_192.168.255.23
  Status:
    Admin: up  Operational: up for 00:25:39 (since Mar  5 21:05:51.401)
  Candidate-paths:
    Preference: 200 (SR-TE ODN) (inactive) (shutdown)
      Requested BSID: dynamic
      Constraints:
        Prefix-SID Algorithm: 128
        Protection Type: protected-preferred
        Maximum SID Depth: 12 
      Dynamic (inactive)
        Metric Type: TE,   Path Accumulated Metric: 0 
    Preference: 100 (SR-TE ODN) (active)
      Requested BSID: dynamic
      PCC info:
        Symbolic name: srte_c_110_ep_192.168.255.23_discr_100
        PLSP-ID: 199
      Constraints:
        Prefix-SID Algorithm: 128
        Protection Type: protected-preferred
        Maximum SID Depth: 12 
      Dynamic (pce 192.168.255.7) (valid)
        Metric Type: LATENCY,   Path Accumulated Metric: 1 
          16802 [Prefix-SID, 192.168.255.23]
  Attributes:
    Binding SID: 24026
    Forward Class: Not Configured
    Steering labeled-services disabled: no
    Steering BGP disabled: no
    IPv6 caps enable: yes
    Invalidation drop enabled: no
    Max Install Standby Candidate Paths: 0

RP/0/RP0/CPU0:Node-4# 

RP/0/RP0/CPU0:Node-4#show policy-map interface TenGigE 0/0/0/10.401
Sun Mar  5 21:33:45.964 UTC

TenGigE0/0/0/10.401 input: per-flow-test

Class PRIORITY
  Classification statistics          (packets/bytes)     (rate - kbps)
    Matched             :                   5/610                  0
    Transmitted         :                   5/610                  0
    Total Dropped       :                   0/0                    0
Class Best_Effort
  Classification statistics          (packets/bytes)     (rate - kbps)
    Matched             :               16853/2181514              10
    Transmitted         :               16853/2181514              10
    Total Dropped       :                   0/0                    0
Class class-default
  Classification statistics          (packets/bytes)     (rate - kbps)
    Matched             :                   0/0                    0
    Transmitted         :                   0/0                    0
    Total Dropped       :                   0/0                    0
Policy Bag Stats time: 1678052022451  [Local Time: 03/05/23 21:33:42.451] 

TenGigE0/0/0/10.401 output: Egress-LowLatency

Class TC3
  Classification statistics          (packets/bytes)     (rate - kbps)
    Matched             :                   0/0                    0
    Transmitted         :                   0/0                    0
    Total Dropped       :                   0/0                    0
  Queueing statistics
    Queue ID                             : 1395 
    Taildropped(packets/bytes)           : 0/0
Class TC1
  Classification statistics          (packets/bytes)     (rate - kbps)
    Matched             :                   0/0                    0
    Transmitted         :                   0/0                    0
    Total Dropped       :                   0/0                    0
  Queueing statistics
    Queue ID                             : 1393 
    Taildropped(packets/bytes)           : 0/0
Class TC5
  Classification statistics          (packets/bytes)     (rate - kbps)
    Matched             :                   5/630                  0
    Transmitted         :                   5/630                  0
    Total Dropped       :                   0/0                    0
  Queueing statistics
    Queue ID                             : 1397 
    Taildropped(packets/bytes)           : 0/0
Class class-default
  Classification statistics          (packets/bytes)     (rate - kbps)
    Matched             :               16853/2248926              10
    Transmitted         :               16853/2248926              10
    Total Dropped       :                   0/0                    0
  Queueing statistics
    Queue ID                             : 1392 
    Taildropped(packets/bytes)           : 0/0






