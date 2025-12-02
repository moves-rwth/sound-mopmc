This page contains supplemental material for the paper 

> *Tools and Algorithms for Sound Multi-Objective Probabilistic Model Checking*
> by Arnd Hartmanns, Tim Quatmann, and Mark van Wijk

All data is available in the [Github repository](https://github.com/moves-rwth/sound-mopmc).

## Tools

**mcsta** 
The version exercised in our experiments is available as a  [Linux x86 binary](mcsta/modest-linux-x64.zip) under [this license](mcsta/License.txt). Mcsta is part of [The Modest Toolset](https://www.modestchecker.net).

Download the zipped package and extract it to a destination of your choice. Then start mcsta from the command line like this `./modest mcsta -?`.

**Storm**
The version exercised in our experiments can be build [from source](storm/storm.zip) under [GPLv3](storm/LICENSE.txt).

To install Storm, follow [these instructions](https://www.stormchecker.org/documentation/obtain-storm/build.html). Roughly, on a Linux system this may work as follows:

```bash
# install dependencies
sudo apt-get install automake build-essential cmake git libboost-dev libginac-dev libglpk-dev libgmp-dev libhwloc-dev libeigen3-dev libxerces-c-dev libz3-dev

cd storm # change into storm directory
mkdir build; cd build
cmake ..
make storm-cli -j4
```

You can now run storm e.g. via `storm/build/bin/storm --help`

## Benchmarks
The benchmark set can be browsed [here](https://github.com/moves-rwth/sound-mopmc/tree/main/qcomp/benchmarks). It extends the benchmarks from the [QComp Repository](https://github.com/ahartmanns/qcomp/tree/master/benchmarks).

## Experiments

#### Reviewing Experiments
An interactive table with raw logfiles can be found [here](table/table.html).
The rows indicate the benchmark instance whereas the column show the respective tool configuration and parameters in the format `tool.solver.epsilon/gamma`.



#### Reproducing Experiments
To reproduce experiments, you can do the following:

```bash
# set environment variable to the root of this repository
export MDPMC_DIR=/your/path/to/stound-mopmc

# create symlinks for storm and modest binaries (make sure that tools are installed)
cd $MDPMC_DIR
mkdir -p bin
ln -s $PWD/mcsta/Modest/modest $PWD/bin/modest
ln -s $PWD/storm/tmp/storm/build/bin/storm $PWD/bin/storm
```

Now you can select any experiment in the [table](table/table.html) and copy-paste the listed invocation command into your terminal, e.g.,

```bash
$MDPMC_DIR/bin/modest mcsta $MDPMC_DIR/qcomp/benchmarks/mdp/wlan/wlan.0.jani --props multi_pos -E COL=0 --unsafe -D -S Memory  --alg ValueIteration --mo-epsilon 1e-3 --mo-gamma 0.5 --lp-solver HiGHS
```



