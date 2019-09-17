# Protected_convection_ZM

This repository holds the Zhang McFarlane convective scheme (Zhang and McFarlane, 1995) in CAM 5.0 (Neale et al. 1995),
modified to "protect" convection from entraining dry air in selected locations. Each pocket is ~ 2.5 x 2.5 degrees in size. 
Inside this pocket, convection only entrains with saturated air. 

The code works by asking if the current location is inside a protected location. If yes, then it implements 
protections in two separate places within the code. 

  i) Transform the entraining CAPE closure (Neale et al. 2012) back into an undilute CAPE 
      in the subroutine 'closure. (easy) 
      
  ii) Make the updrafts and downdrafts interact with saturated air in the subroutine 'cldprp' (less easy). 
  
  Also, the code uses Newton's method, which sometimes fails to converge when 
  inverting the plume entropy to deduce temperature. In these cases, the code uses Halley's method (which has not yet failed).
  
  Search for !FA within the code to examine all the modifications. 
  
  To run these codes in your version of CAM/CEMS. Place 
   
   i) user_nl_cam in your case directory (CASE_DIR)
   
   ii)namelist_definition.xml, zm_conv.F90 and zm_conv_intr.F90 in CASE_DIR/SourceMods/src.cam,
   and build.
