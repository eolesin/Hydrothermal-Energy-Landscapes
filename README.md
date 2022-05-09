# Hydrothermal-Energy-Landscapes
editing and creating a new thermodynamic database to feed GWB, and how to run the energy modeling

# Getsp.py
#the species involved in the GWB file you're working with to start. Not needed for further analysis.

```
python Getsp.py React_output_100x.txt
```

# CheckType.py
#check which databases thermodynamic info are sourced from. Combine with subcrt commands of interest as input, and specify which database you want to see entries from.
#Save the output, and use as INPUT for Polish_CheckType.sh  *****

```
python CheckType.py subcrt_commands_database.txt thermo.com.v8.r6+_mod051112_p50bar_JMVF.dat r6 > checktypeout.txt
```


# Polish_CheckType.sh
#Takes output file from CheckType.py and adds header with pressure and temperatures of choice. 
#Eliminates unncessary columns from previous output and comments out H2O(g) line.

#Type this in the command line. The program takes user inputs of pressure and temp one at a time.
```
sh Polish_CheckType.sh
```

# MakeRscript_v3.py
#This creates an R script for you that includes all your subcrt commands of interest and also adds in Fe(OH)3 oxidation as a factor.
#INPUTS: output of Polish_CheckType.sh and subcrt_commands.txt AND indicate which database (thermo, r6)

```
python MakeRscript_v3.py polish_checktypeout.txt subcrt_commands_database.txt r6 > r_script_withSam.R
```

# r_script_withSam.R
#Import into R base or R studio. Make sure to clear your environment first before running commands.
#Basically without Rscript usage in the terminal, you need to paste the commands of the script into R.

#Output is: logK_out.txt

# ChangeDb_v3.py 
#Replace the logK values in the database. Database is subsequently used in GWB for modeling energy landscape with new chemical activity delineated.
```
python ChangeDb_v3.py logK_out.txt thermo.com.v8.r6+_mod051112_p50bar_JMVF.dat > Aurora_thermo400.dat 
```
