
The Below config needs to be manaully configured on each headend. Note: XR device NED does not yet support cumulative bounds metric. Either does SR-TE CFP


segment-routing
 traffic-eng
  on-demand color 130
   dynamic
    pcep
    !
    metric
     type igp
    !
    bounds
     cumulative
      type latency 10
     !
    !
   !
  !
  on-demand color 131
   dynamic
    pcep
    !
    metric
     type igp
    !
    bounds
     cumulative
      type latency 7
     !
    !
   !
  !


