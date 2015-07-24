# Alignment

Setup Muon Alignment in 74X for early Run2 data:

    cmsrel CMSSW_7_4_6_patch3
    cd CMSSW_7_4_6_patch3/src/
    cmsenv
    
    git clone https://github.com/cms-mual/Alignment.git -b CMSSW_7_4_X_DATA
    git clone https://github.com/cms-mual/TrackingTools.git -b CMSSW_7_4_X
    git clone https://github.com/cms-mual/MuAlSupplementaryFiles.git -b CMSSW_7_4_X_DATA
    
    cp MuAlSupplementaryFiles/* .
    ln -s Alignment/MuonAlignmentAlgorithms/scripts/createJobs.py
    ln -s Alignment/MuonAlignmentAlgorithms/python/gather_cfg.py
    ln -s Alignment/MuonAlignmentAlgorithms/python/align_cfg.py
    
    scram b -j 16

Run DT alignment:

    ./createJobs.py data_DT-1100-110001_SingleMuon_Run2015B-PromptReco-v1_RECO_7_4_6_patch3_pt20_v1_ 3 \
    74X_dataRun2_Prompt_v0_AlignmentRcd.db \
    --gprcdconnect sqlite_file:74X_dataRun2_Prompt_v0_GlobalPositionRcd.db \
    --gprcd GlobalPositionRcd
    --inputInBlocks SingleMuon_Run2015B-PromptReco-v1_RECO.py \
    --json Cert_246908-251883_13TeV_PromptReco_Collisions15_JSON_MuonPhys_v2.txt \
    -s data_DT-1100-110001_SingleMuon_Run2015B-PromptReco-v1_RECO_7_4_6_patch3_pt20_v1.sh \
    --validationLabel data_DT-1100-110001_SingleMuon_Run2015B-PromptReco-v1_RECO_7_4_6_patch3_pt20_v1 \
    --globalTag 74X_dataRun2_Prompt_v0 \
    --minTrackPt 20 --maxTrackPt 200 \
    --noCSC \
    --maxDxy 0.2 --minNCrossedChambers 1 --residualsModel pureGaussian --peakNSigma 2. \
    --station123params 110001 --station4params 100001 --cscparams 100001 --useResiduals 1100 \
    --mapplots --curvatureplots --segdiffplots --extraPlots \
    --b --user_mail youremail \
    --createAlignNtuple --noCleanUp \
    --trackerconnect sqlite_file:/afs/cern.ch/cms/CAF/CMSALCA/ALCA_TRACKERALIGN/PayLoads/2015-07-15_PseudoPCLupdate/TkAlignment.db \
    --trackeralignment testTag
    
    source data_DT-1100-110001_SingleMuon_Run2015B-PromptReco-v1_RECO_7_4_6_patch3_pt20_v1.sh

Run CSC Alignment:

    ./createJobs.py data_CSC-1100-110001_SingleMuon_Run2015B-PromptReco-v1_RECO_7_4_6_patch3_pt20_v1_ 3 \
    74X_dataRun2_Prompt_v0_AlignmentRcd.db \
    --gprcdconnect sqlite_file:74X_dataRun2_Prompt_v0_GlobalPositionRcd.db \
    --gprcd GlobalPositionRcd
    --inputInBlocks SingleMuon_Run2015B-PromptReco-v1_RECO.py \
    --json Cert_246908-251883_13TeV_PromptReco_Collisions15_JSON_MuonPhys_v2.txt \
    -s data_CSC-1100-110001_SingleMuon_Run2015B-PromptReco-v1_RECO_7_4_6_patch3_pt20_v1.sh \
    --validationLabel data_CSC-1100-110001_SingleMuon_Run2015B-PromptReco-v1_RECO_7_4_6_patch3_pt20_v1 \
    --globalTag 74X_dataRun2_Prompt_v0 \
    --minTrackPt 20 --maxTrackPt 200 \
    --noDT \
    --maxDxy 0.2 --minNCrossedChambers 1 --residualsModel pureGaussian --peakNSigma 2. \
    --station123params 110001 --station4params 100001 --cscparams 100001 --useResiduals 1100 \
    --mapplots --curvatureplots --segdiffplots --extraPlots \
    --b --user_mail youremail \
    --createAlignNtuple --noCleanUp \
    --trackerconnect sqlite_file:/afs/cern.ch/cms/CAF/CMSALCA/ALCA_TRACKERALIGN/PayLoads/2015-07-15_PseudoPCLupdate/TkAlignment.db \
    --trackeralignment testTag
    
    source data_CSC-1100-110001_SingleMuon_Run2015B-PromptReco-v1_RECO_7_4_6_patch3_pt20_v1.sh
