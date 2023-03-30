

[root@new-transport-nso-6 M7]# ls -l
total 212
-rw-r--r--. 1 root root  4481 Feb 25 14:44 00_README.txt
-rw-r--r--. 1 root root  1168 Mar  5 11:11 0a_odn_policies.cli
-rw-r--r--. 1 root root   740 Feb 25 14:42 0b_resource_pools.cli
-rw-r--r--. 1 root root   173 Feb 25 14:43 0c_l2vpn_pool.cli
-rw-r--r--. 1 root root   629 Mar  4 19:35 0d_pm-profiles.cli
-rw-r--r--. 1 root root   353 Feb 25 14:42 0e_y1731.cli
-rw-r--r--. 1 root root 19079 Mar  5 11:11 0f_slicing-pre-configs.cli
-rw-r--r--. 1 root root  1728 Feb 25 14:42 a_L3_A2A_dedicated_eMBB.cli
-rw-r--r--. 1 root root  1728 Mar  1 17:28 a_L3_A2A_dedicated_Gold.cli
-rw-r--r--. 1 root root  1732 Mar  4 22:54 a_L3_A2A_dedicated_URLLC.cli
-rw-r--r--. 1 root root    78 Feb 25 14:42 b_update_L3_eMBB_to_URLLC.cli
-rw-r--r--. 1 root root   877 Feb 25 14:42 c_L2_P2P_eMBB.cli
-rw-r--r--. 1 root root   878 Feb 25 14:42 c_L2_P2P_URLLC.cli
-rw-r--r--. 1 root root  1158 Feb 25 14:42 d_L2_MP_dedicated_eMBB.cli
-rw-r--r--. 1 root root  2245 Feb 26 16:53 e_L3_A2A_dedicated_URLLC_shared_eMBB.cli
-rw-r--r--. 1 root root  2246 Feb 26 16:53 e_L3_A2A_dedicated_URLLC_shared_eMBB_withoutSSC.cli
-rw-r--r--. 1 root root  2662 Feb 26 17:07 f_L3_A2A_multi-dedicated_shared.cli
-rw-r--r--. 1 root root  2133 Feb 26 17:08 g_L2_MP_multi-dedicated_shared.cli
-rw-r--r--. 1 root root  2364 Feb 25 14:42 h_L3_HubSpoke_dedicated_error.cli
-rw-r--r--. 1 root root  1858 Feb 25 14:42 h_L3_HubSpoke_dedicated_URLLC.cli
-rw-r--r--. 1 root root  1293 Feb 25 14:42 i_L2_HubSpoke_dedicated_URLLC.cli
-rw-r--r--. 1 root root  2320 Feb 27 12:57 j_L3_HS_dedicated_shared_nohub.cli
-rw-r--r--. 1 root root  2824 Feb 27 12:58 j_L3_HS_dedicated_shared_withhub.cli
-rw-r--r--. 1 root root  2212 Feb 27 16:09 k_L2_HS_multi-dedicated_shared.cli
-rw-r--r--. 1 root root  1593 Feb 27 23:27 l_L2_HS_dedicated_URLLC_addRT.cli
-rw-r--r--. 1 root root  1996 Feb 27 23:29 l_L3_A2A_dedicated_eMBB_addRT.cli
-rw-r--r--. 1 root root  2158 Feb 27 23:34 l_L3_HS_dedicated_URLLC_addRT.cli
-rw-r--r--. 1 root root  1755 Feb 27 23:55 m_L3_A2A_dedicated_eMBB_manual_and_auto_RD.cli
-rw-r--r--. 1 root root  1781 Feb 27 23:37 m_L3_A2A_dedicated_eMBB_manualRD.cli
-rw-r--r--. 1 root root  1164 Feb 27 23:43 n_L2_MP_dedicated_BWOD_1G.cli
-rw-r--r--. 1 root root   924 Feb 27 23:44 n_L2_P2P_dedicated_BWOD_custom.cli
-rw-r--r--. 1 root root  1781 Feb 28 00:30 n_L3_A2A_dedicated_BWOD_custom.cli
-rw-r--r--. 1 root root  1732 Mar  4 12:44 o_L3_A2A_dedicated_ENCRYPT.cli
-rw-r--r--. 1 root root  1737 Mar  4 23:11 p_L3_A2A_dedicated_eMBB_PM.cli
-rw-r--r--. 1 root root  1738 Mar  4 23:11 p_L3_A2A_dedicated_URLLC_PM.cli
-rw-r--r--. 1 root root  1739 Feb 28 00:24 q_L3_A2A_dedicated_DSCP_Flow.cli
-rw-r--r--. 1 root root   361 Mar  5 15:43 q_per-flow-cleanup-odn_headends.cli
-rw-r--r--. 1 root root   213 Mar  5 16:01 q_per-flow-prereq-odn_headends_1.cli
-rw-r--r--. 1 root root   690 Mar  5 16:02 q_per-flow-prereq-odn_headends_2.cli
-rw-r--r--. 1 root root 12798 Mar  5 16:39 q_README_perFlow.txt
-rw-r--r--. 1 root root  1739 Mar  5 00:43 r_L3_A2A_dedicated_Disjoint_North.cli
-rw-r--r--. 1 root root  1739 Mar  5 11:13 r_L3_A2A_dedicated_Disjoint_South.cli
-rw-r--r--. 1 root root  1740 Mar  1 17:16 s_L3_A2A_dedicated_Delay_10ms.cli
-rw-r--r--. 1 root root  1735 Mar  1 17:18 s_L3_A2A_dedicated_Delay_7ms.cli
-rw-r--r--. 1 root root   488 Mar  5 17:13 s_README_cumulative-bounds.txt

--------------------------------------------------------------------------------------

Pre-slice Instantiation setup scripts:

Load files 0a through 0f in order.

---------------------------------------------------------------------------------------

 
Slice Test-Cases (test letters maps to payload name):

a- Three site any-to_any L3 Slice with various catalog entries, eMBB, URLLC, Gold (Gold=no SR-TE but high priority QoS)

b- Switch from eMBB to URLLC

c- L2 P2P 

d- Three site a2a L2 Multi-Point 

e- One shared slice L3 site with eMBB (NAPA) and one any-to_any L3 dedicated URLLC Slice (FORD) with two sites with Single-sided-control and another payload without without SSC.

f- One shared slice L3 site with eMBB (NAPA) and two dedicated slices, each with one site any-to-any L3. Ford with URLLC with Single-sided-control and Chevy with eMBB

g- One shared slice L2 (any to any) site with eMBB (NAPA) and two dedicated slices, each with one site any-to-any L2. Ford with URLLC with Single-sided-control and Chevy with eMBB (same test case as f but for L2).

h- Three site hub-spoke L3 slice with URLLC (two spokes can not communicate with each other). Also a test error payload with hub and spoke site on same PE 

i- Three site hub-spoke L2 slice with URLLC (two spokes can not communicate with each other).

j- One shared slice L3 site with eMBB (NAPA) and one dedicated hub-spoke slice (1) one with no hub specified, just spokes (2) another with a hub specified on same PE as shared site.  Both are Ford spokes with URLLC with Single-sided-control


k- One shared slice L2 (any to any) site with eMBB (NAPA) and two dedicated slices, each are hub-spoke L2, with each only having a spoke defined. Ford with URLLC with Single-sided-control and Chevy with eMBB  

l- Same as a, h, i but using manaul RT assignment, along with adding extra RTs for SDP 1.

m- Same as #a, but using manaul RD assignment (and mix with auto SDPs)

n- Mix of BWOD Use cases, using new BWOD catalog entries. (1)  with BWOD custom entry, (2) with BWOD 1G entry (pre-defined in sr-te template). (enable BWOD COE feature in CNC)

o- Same as a, but with Encrypted Slice type using Flex-Algo 129 with link affinities.

p- same as a, but using catalof entry that specifes SR-PM for both delay (URLLC) and liveness (eMBB))

q- Testing for DSCP per-flow based slices. Need to view README as this is technically not supported slice type but we can make work. load pre-requisit configs to setup headends with proper ODN templates. 

r- same as a, but using Disjoint Path slice type via flex-algo 131 or 132 for a North bound path or a South bound path

s- Same as a, but workaround to support  "cumulative bound metrics" or bounded slice delays. Need to view README and manaully configure proper ODN templates on headends. 






 

 
 

