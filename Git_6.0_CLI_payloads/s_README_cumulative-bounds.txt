
Note: SR-TE CFP does not yet support cumulative constraint commands.
Also need to remove pcep processing as cumualtive is only suppported at pcc.

The following commands are in the pre-requisit files

(1) Build custom template

devices template ct-color-130-10ms
 ned-id cisco-iosxr-cli-7.52
  config
   segment-routing traffic-eng on-demand color 130
    dynamic bounds cumulative type latency
     value 10000
    !
   !
  !
 !
!
devices template ct-color-131-7ms
 ned-id cisco-iosxr-cli-7.52
  config
   segment-routing traffic-eng on-demand color 131
    dynamic bounds cumulative type latency
     value 7000
    !
   !
  !
 !
!

(2) Build ODN Policy Templates

cisco-sr-te-cfp:sr-te odn odn-template eMBB_10ms
 custom-template ct-color-130-10ms
 color 130
 dynamic metric-type igp
!
cisco-sr-te-cfp:sr-te odn odn-template eMBB_7ms
 custom-template ct-color-131-7ms
 color 131
 dynamic metric-type igp
!


Now the Slice Template can be created.




