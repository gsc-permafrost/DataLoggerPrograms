## Instructions for EasyFlux_DL_OP_with_LI7700 program

This program (EasyFlux_DL_CR1000XOP_v2_02_LI7700) is for an application of integrating LI-7700 into an IRGASON (open path) eddy covariance system. It is based on the original program (EasyFlux_DL_CR1000XOP_v2.01) for the open path system IRGASON. Please find the EasyFlux DL manual here,  https://s.campbellsci.com/documents/us/manuals/easyflux-dl-cr6op.pdf . This brief instruction should be considered as an extension of the full EasyFlux DL manual. 
If you want to see the lines in the program related to LI-7700 (methane sensor), search for key word ‘SENSOR_LI7700’. In line #65, turn on flag ‘SENSOR_LI7700’ (set it to TRUE) to retain all LI-7700 parts in the program; turn it off (set it to FALSE) to remove all lines in the program if conditional compile is used. 
LI-7700 portion of the program is not exchangeable between EasyFlux DL OP (program for IRGASON or EC150) and EasyFlux DL CP (program for CPEC310 or EC155).

To set up LI-7700, data-logger and program:

1.	Wiring instructions can be found between lines #680 and 692. An ethernet cable is used to directly connect LI-7700 and datalogger (CR1000X). Please set up the IP address on both LI-7700 and CR1000X accordingly. Also set the output frequency of LI-7700 as the same as IRGASON (usually at 10 Hz).

2.	In lines #2629 and 2630, two variables ‘SEPARATION_X_GA_77’ and ‘SEPARATION_Y_GA_77’ are declared. They define the position of LI-7700 in the coordinate system of sonic anemometer (CSAT3) and will be used to compute the spatial separation of two sensors or the signal delay between them. Currently two arbitrary values are assigned to them. Customers need to replace them with the true measurements at their site. The unit for ‘SEPARATION_X_GA_77’ and ‘SEPARATION_Y_GA_77’ is meter and please assign the correct sign to them.

3.	In lines #2623 and 2624, two variables define the upper and lower thresholds for CH4 density measurements. Their purpose is to filter out the outlier or unreasonable values and exclude them from CH4 flux calculation. Customers are welcome to adjust them to better reflect the reality at their site.

4.	Most importantly, one needs to pay attention to the variable order in the LI-7700 output line. LI-Cor’s documents were not very consistent in describing LI-7700 output line. Some documents indicated that the 5th variable in the output line was CH4 density (CH4D) while the 6th was the mole fraction (CH4), while others suggested an opposite order. However, LI-Cor documents consistently pointed out CH4 density (CH4D) should be selected and used in flux calculation. We strongly recommend that customers should run terminal programs (Hyper Terminal or Tera Term) on their PC to check out the variable order in the output line and then change the program (array index in line #7709; its value could be 5 or 6 based on the position of CH4D in the output line) if necessary. 
