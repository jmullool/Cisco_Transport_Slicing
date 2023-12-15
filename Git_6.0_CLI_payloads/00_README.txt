[root@NSO-CNC240 Git_6.0_CLI_payloads]# ls -l
total 232
-rw-r--r--. 1 root root  6395 Dec 15 00:46 00_README.txt
-rw-r--r--. 1 root root   900 Dec 15 00:46 0aa_custom_templates.cli
-rw-r--r--. 1 root root  1878 Dec 15 00:46 0a_odn_policies.cli
-rw-r--r--. 1 root root   740 Dec 15 00:46 0b_resource_pools.cli
-rw-r--r--. 1 root root   173 Dec 15 00:46 0c_l2vpn_pool.cli
-rw-r--r--. 1 root root   596 Dec 15 00:46 0d_pm-profiles.cli
-rw-r--r--. 1 root root   353 Dec 15 00:46 0e_y1731.cli
-rw-r--r--. 1 root root 26535 Dec 15 00:46 0f_slicing-pre-configs.cli
-rw-r--r--. 1 root root  1808 Dec 15 00:46 a_L3_A2A_dedicated_eMBB.cli
-rw-r--r--. 1 root root  1808 Dec 15 00:46 a_L3_A2A_dedicated_Gold.cli
-rw-r--r--. 1 root root  1813 Dec 15 00:46 a_L3_A2A_dedicated_URLLC.cli
-rw-r--r--. 1 root root   146 Dec 15 00:46 b_update_L3_eMBB_to_URLLC.cli
-rw-r--r--. 1 root root   160 Dec 15 00:46 b_update_L3_eMBB_to_URLLC_PM.cli
-rw-r--r--. 1 root root   945 Dec 15 00:46 c_L2_P2P_eMBB.cli
-rw-r--r--. 1 root root   945 Dec 15 00:46 c_L2_P2P_URLLC.cli
-rw-r--r--. 1 root root   955 Dec 15 00:46 c_L2_P2P_URLLC_NoFA.cli.test
-rw-r--r--. 1 root root  1237 Dec 15 00:46 d_L2_MP_dedicated_eMBB.cli
-rw-r--r--. 1 root root  2447 Dec 15 00:46 e_L3_A2A_dedicated_URLLC_shared_eMBB.cli
-rw-r--r--. 1 root root  2473 Dec 15 00:46 e_L3_A2A_dedicated_URLLC_shared_eMBB_noSSC.cli
-rw-r--r--. 1 root root  2969 Dec 15 00:46 f_L3_A2A_multi-dedicated_shared.cli
-rw-r--r--. 1 root root  2430 Dec 15 00:46 g_L2_MP_multi-dedicated_shared.cli
-rw-r--r--. 1 root root  2482 Dec 15 00:46 h_L3_HubSpoke_dedicated_error.cli
-rw-r--r--. 1 root root  1949 Dec 15 00:46 h_L3_HubSpoke_dedicated_URLLC.cli
-rw-r--r--. 1 root root  1385 Dec 15 00:46 i_L2_HubSpoke_dedicated_URLLC.cli
-rw-r--r--. 1 root root  2567 Dec 15 00:46 j_L3_HS_dedicated_shared_nohub.cli
-rw-r--r--. 1 root root  3073 Dec 15 00:46 j_L3_HS_dedicated_shared_withhub.cli
-rw-r--r--. 1 root root  2634 Dec 15 00:46 k_L2_HS_multi-dedicated_shared.cli
-rw-r--r--. 1 root root  1720 Dec 15 00:46 l_L2_HS_dedicated_URLLC_addRT.cli
-rw-r--r--. 1 root root  2123 Dec 15 00:46 l_L3_A2A_dedicated_eMBB_addRT.cli
-rw-r--r--. 1 root root  2284 Dec 15 00:46 l_L3_HS_dedicated_URLLC_addRT.cli
-rw-r--r--. 1 root root  1886 Dec 15 00:46 m_L3_A2A_dedicated_eMBB_manual_and_auto_RD.cli
-rw-r--r--. 1 root root  1893 Dec 15 00:46 m_L3_A2A_dedicated_eMBB_manualRD.cli
-rw-r--r--. 1 root root  1265 Dec 15 00:46 n_L2_MP_dedicated_BWOD_1G.cli
-rw-r--r--. 1 root root  1046 Dec 15 00:46 n_L2_P2P_dedicated_BWOD_custom.cli
-rw-r--r--. 1 root root  1894 Dec 15 00:46 n_L3_A2A_dedicated_BWOD_custom.cli
-rw-r--r--. 1 root root  1819 Dec 15 00:46 o_L3_A2A_dedicated_ENCRYPT.cli
-rw-r--r--. 1 root root  1818 Dec 15 00:46 p_L3_A2A_dedicated_eMBB_PM.cli
-rw-r--r--. 1 root root  1829 Dec 15 00:46 p_L3_A2A_dedicated_URLLC_NoFA_PM.cli
-rw-r--r--. 1 root root  1819 Dec 15 00:46 p_L3_A2A_dedicated_URLLC_PM.cli
-rw-r--r--. 1 root root  1833 Dec 15 00:46 q_L3_A2A_dedicated_DSCP_Flow.cli
-rw-r--r--. 1 root root 12905 Dec 15 00:46 q_README_perFlow.txt
-rw-r--r--. 1 root root  1836 Dec 15 00:46 r_L3_A2A_dedicated_Disjoint_North.cli
-rw-r--r--. 1 root root  1836 Dec 15 00:46 r_L3_A2A_dedicated_Disjoint_South.cli
-rw-r--r--. 1 root root  1828 Dec 15 00:46 s_L3_A2A_dedicated_Delay_10ms.cli
-rw-r--r--. 1 root root  1823 Dec 15 00:46 s_L3_A2A_dedicated_Delay_7ms.cli
-rw-r--r--. 1 root root   955 Dec 15 00:46 s_README_cumulative-bounds.txt
-rw-r--r--. 1 root root  2589 Dec 15 00:46 t_L3_A2A_dedicated_disjoint_shared_URLLC.cli
-rw-r--r--. 1 root root  3122 Dec 15 00:46 t_L3_A2A_dedicated_disjt_FA_shared_URLLC.cli

--------------------------------------------------------------------------------------

Pre-slice Instantiation setup scripts:

Load files 0aa through 0f in order.

---------------------------------------------------------------------------------------

 
Slice Test-Cases (test letters maps to payload name): Be aware some payloads may use the same endpoints, so proper cleanup is required before
creating a new slice.

a- Three site any-to_any L3 Slice with various catalog entries, eMBB, URLLC, Gold (Gold=no SR-TE but high priority QoS)

b- Switch from eMBB to URLLC

c- L2 P2P 

d- Three site a2a L2 Multi-Point 

e- One shared slice L3 site with eMBB (NAPA) and one any-to_any L3 dedicated URLLC Slice (FORD) with two sites with Single-sided-control and another payload without without SSC.

f- One shared slice L3 site with eMBB (NAPA) and two dedicated slices, each with one site any-to-any L3. Ford with URLLC with Single-sided-control and Chevy with eMBB

g- One shared slice L2 (any to any) site with eMBB (NAPA) and two dedicated slices, each with one site any-to-any L2. Ford with URLLC with Single-sided-control and Chevy with eMBB (same test case as f but for L2).

h- Three site hub-spoke L3 slice with URLLC (two spokes can not communicate with each other). Also a test error payload with hub and spoke site on same PE 

i- Three site hub-spoke L2 slice with URLLC (two spokes can not communicate with each other).

j- One shared slice L3 site with eMBB (NAPA) and one dedicated hub-spoke slice (1) one with no hub specified, just spokes (2) another payload with both a shared slice and a hub specified on same PE as shared site.  Both are Ford spokes with URLLC with Single-sided-control


k- One shared slice L2 (any to any) site with eMBB (NAPA) and two dedicated slices, each are hub-spoke L2, with each only having a spoke defined. Ford with URLLC with Single-sided-control and Chevy with eMBB  

l- Same as a, h, i but using manaul RT assignment, along with adding extra RTs for SDP 1.

m- Same as #a, but using manaul RD assignment (and mix with auto SDPs)

n- Mix of BWOD Use cases, using new BWOD catalog entries. (1)  with BWOD custom entry, (2) with BWOD 1G entry (pre-defined in sr-te template). (enable BWOD COE feature in CNC)

o- Same as a, but with Encrypted Slice type using Flex-Algo 129 with link affinities.

p- same as a, but using catalog entry that specifes SR-PM for both delay (URLLC) and liveness (eMBB))

q- Testing for DSCP per-flow based slices. Need to view README as this is technically not supported slice type but we can make work. load pre-requisit configs (custom-template and ODN policy) to allow for non supported CFP commands. 

r- same as a, but using Disjoint Path slice type via flex-algo 131 or 132 for a North bound path or a South bound path

s- Same as a, but workaround to support  "cumulative bound metrics" or bounded slice delays. Need to view README and manaully configure proper custom-templates and ODN templates to allow for unsupported CFP commands. 

t- rework of CNC example from docuementaiton but using slicing services. Intent includes disjoint paths for traffic sent from Node-5 to either Node-4 or Node-2 (only one direction) and low latency. Two solutions identiied, one using disjoint path command in ODN template and the other using disjoint FA policy.




 

 
 

