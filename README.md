# ePIC_preTDR_nHCal_DIS_MCPart
Analysis of ePIC reconstructed data. Just follow these steps:


### Create directories for condor jobs:

```Sh
mkdir.sh
```

### Submit jobs:

```Sh
sbatch --array=1-200 submitPythia_ep.sh | tee submit.log
```

### Get container and run ```eic-shell```:

```Sh
curl --location https://get.epic-eic.org | bash -s -- -c jug_xl -v 22.11-main-stable
./eic-shell
```

### When jobs finish merge results:

```Sh
cd output/output/
cmod u+x haddmerge.pl . | tee hadd.log
mkdir ../../output/data
cp <merged_output.root> ../../output/data/output_primary_full.root
```


### Run macros:

```Sh
cd output/data/
root -l -b -q drawAcceptance_All.C+
```

### Get the plots in:

```Sh
ls output/output/Acceptance/
```

