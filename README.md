# condor sumbission tools
These scripts facilitate running any executable in condor which satisfies certain requirements:

## Executable requirements:
The exe must have the first parameter be the inputfile to run on, and the second parameter to be the output filename, followed by any number of parameters you like
ex:
```bash
# ./gammajetSkim.exe <inputfile> <outputfile> [jetname] [is_pp]
./gammajetSkim.exe /mnt/hadoop/cms/store/user/luck/2015-Data-promptRECO-photonSkims/pp-photonHLTFilter-v0-HiForest/0.root /export/d00/scratch/dav2105/ztrees/g.pp-photonHLTFilter-v0-HiForest.root ak3PFJetAnalyzer 1
```

## How to use:
You need an input file list, a good place to put the output (like hadoop), any necessary input files in a tgz file, and the compiled and tested executable. Then just use the prun.sh command:
ex:
```bash
# ./prun.sh <input-list> <out-dir> <inputfile.tgz> <exe> [args]
./prun.sh HIPhoton40AndZ-PbPb-photonHLTFilter-v3.txt /mnt/hadoop/cms/store/user/velicanu/unmerged/ residuals.tgz gammajetSkim.exe akPu3PFJetAnalyzer 0
# condor_submit path_to/pmerge.condor
```
This will run the executbale in one job per file in the input-list and output a jobNumber.root file in the output directory.

Make sure to test the exe *interactively* and with a *few* jobs before running on the full dataset!
