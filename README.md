# SimPickGen
Autonomous Pick-and-Place execution in Isaac Sim using cuRobo, logging synchronized multi-modal data (joints &amp; vision) for Embodied AI.

## Installation Guide for SimPickGen
This guide walks you through setting up the environment to run SimPickGen — an autonomous pick-and-place system in NVIDIA Isaac Sim, powered by cuRobo and logging synchronized multi-modal data (vision, joints, end-effector pose, language commands) for Embodied AI.

> ✅ Verified on Isaac Sim 5.0 (Workstation)  
⚠️ Avoid numpy>=2.0 due to [known crash](https://github.com/isaac-sim/IsaacLab/issues/3312)

#### Step1. Install NVIDIA Isaac Sim (Workstation)
Go to the official download page:
- [Isaac Sim 4.5 Workstation Installation](https://docs.isaacsim.omniverse.nvidia.com/4.5.0/installation/install_workstation.html) or 
- [Isaac Sim 5.0 Workstation Installation](https://docs.isaacsim.omniverse.nvidia.com/5.0.0/installation/install_workstation.html)(Recommend)
  
Download and install Isaac Sim 5.0 (or 4.5) — Workstation version is required.

#### Step2. Install cuRobo for Use with Isaac Sim
Follow [the official cuRobo installation instructions for Isaac Sim integration](https://curobo.org/get_started/1_install_instructions.html#install-for-use-in-isaac-sim):

- Install CUDA 11.8 or newer, following cuda_instructions and add to your path with: `export PATH=/usr/local/cuda-11.8/bin${PATH:+:${PATH}}`
- Install NVIDIA Isaac Sim 4.5 or 5.0 (see [step 1](#1-install-nvidia-isaac-sim-workstation)).
- Add an alias to Isaac Sim’s python in your bashrc file:`echo "alias omni_python='/path/to/your_isaacsim/python.sh'" >> ~/.bashrc`and source it with `source ~/.bashrc`. If your isaac sim path is different, change the path accordingly.
- Install git lfs with `sudo apt install git-lfs`.
- Install these additional packages: `omni_python -m pip install tomli wheel ninja`.

- Clone cuRobo repository with `git clone https://github.com/NVlabs/curobo.git`, move inside the cloned repo with `cd curobo`.

- run `omni_python -m pip install -e .[isaacsim] --no-build-isolation`, where `omni_python` refers to `./python.sh` from isaac sim installation (info).

- Run `omni_python examples/isaac_sim/motion_gen_reacher.py` to run a motion generation example. Once Isaac Sim loads, click play and move the target cube to start generating motions.

#### Step3. Install Required Python Dependencies
Use `omni_python` to install project-specific packages inside Isaac Sim’s environment
`
omni_python -m pip install h5py numpy==1.26.0 tyro
`
> 🔍 Why numpy==1.26.0?  
Isaac Sim’s synthetic data pipeline (via omni.syntheticdata) fails with numpy>=2.0 due to internal dtype handling, causing:`TypeError: Unable to write from unknown dtype, kind=f, size=0`  
Pinning to 1.26.0 resolves this while remaining compatible with PyTorch and cuRobo.  
Refer to [known crash](https://github.com/isaac-sim/IsaacLab/issues/3312)

#### Step4. Ready to Run SimPickGen!
 - clone SimPickGen repo:`git clone https://github.com/bluejade115/SimPickGen.git`
 - Install SimPickGen by `cd SimPickGen && omni_python -m pip install -e .`
 - Run examples:`omni_python examples/pickplce_banana.py`
## demo
franka_pickplace_banana_with_camera:

[demo](https://github.com/user-attachments/assets/8457a37e-136e-4e60-9493-4c7594d20ddb)

franka_record_data_demo:

[demo](https://github.com/user-attachments/assets/3ead98a1-c794-42fa-998a-1aee1c0b3c8a)



