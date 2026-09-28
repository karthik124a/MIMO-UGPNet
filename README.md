# MIMO-UGPNet

True MIMO-OTFS implementation of GEPNet based on the original UGPNet project.

## Dimensions

- Nt: transmit antennas
- Nr: receive antennas
- M: OTFS delay bins
- N: OTFS Doppler/time bins
- Complex H: [Nr*M*N, Nt*M*N]
- Real H: [2*Nr*M*N, 2*Nt*M*N]
- GNN nodes: 2*Nt*M*N

Each Tx/Rx antenna pair has an independent OTFS multipath block. The complete MIMO channel is assembled from those blocks and scaled by 1/sqrt(Nt).

## Files

Gen_dat.py contains MIMO-OTFS data generation, MMSE and conventional EP.
EP.py contains the rectangular-channel EP/LMMSE update.
GEPNet.py and GNN.py contain the trainable detector.
Data_loader.py contains training/testing loaders.
Train_Eval_funcs.py contains training/evaluation/SER logic.
parsers.py contains MIMO/OTFS configuration.
main_with_genData.py is the training entry point.
mainTestScript.py is the testing entry point.

## Install

```bash
pip install numpy torch matplotlib
```

## Train: 4Tx x 4Rx, M=N=4

```bash
python main_with_genData.py --Nr 4 --Nt_list 4 --M 4 --N 4
```

## Test

```bash
python mainTestScript.py --Nr 4 --Nt_list 4 --Nt_list_test 4 --M 4 --N 4
```

## Example: 4Tx x 8Rx

```bash
python main_with_genData.py --Nr 8 --Nt_list 4 --M 4 --N 4
```

## Small smoke test

```bash
python main_with_genData.py --Nr 2 --Nt_list 2 --M 2 --N 2 --samples 32 --batch_size 8 --validation_size 8 --n_epochs 1 --iter_GEPNet 2 --iter_GNN 1
```

Train new checkpoints for MIMO. Checkpoints from the original SISO/square formulation are not dimension-compatible with this implementation.
