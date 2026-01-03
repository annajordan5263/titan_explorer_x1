# 泰坦勘探者-X1 (Titan Explorer X1)

**Version:** 1.0.0  
**License:** [GPL v3](./LICENSE)  
**Target Platform:** ADLINK MXE-5500 (x86_64) / ARMv8  
**Domain:** Paleorobotics, Cretaceous Exploration, Biomechanics, Fluid Dynamics

## Overview

泰坦勘探者-X1 (Titan Explorer X1) 是一个科研与工业级别的C语言算法库，其设计灵感来源于白垩纪晚期巴塔哥尼亚地区的植食性泰坦巨龙类恐龙——埃拉尔巨龙属 (*Elaltitan lilloi*) 的生物特征。该项目旨在为模拟此类巨型恐龙行为和生物力学特性的机器人平台提供核心控制算法。

本库实现了包括栖息地评估、行为模式切换、植食性取食模拟、四足运动控制、刚体动力学、流体力学（空气阻力）以及材料力学在内的多个模块，并特别集成了基于**逆压梯度湍流边界层 (APG-TBL)** 理论的空气动力学模型，以应对巴塔哥尼亚地区的强风环境。

## Key Features

*   **Biomechanically Accurate:** Algorithms are grounded in paleontological research (e.g., Carballido et al., 2012) on *Elaltitan*.
*   **Industrial-Grade:** Designed for real-time performance and reliability on embedded systems like the ADLINK MXE-5500.
*   **Real-Time Performance:** Optimized for low latency (sub-10ms on target hardware).
*   **Advanced Aerodynamics:** Includes specialized APG-TBL modeling for stability in high-wind environments.
*   **GPL v3 Licensed:** Fully open-source for academic and commercial use and modification.
*   **Modular Design:** Clear separation of concerns for easy maintenance and extension.

## Installation on ADLINK MXE-5500

```bash
# Install dependencies
sudo apt update
sudo apt install build-essential cmake

# Clone and build the project
git clone https://github.com/your-repo/titan_explorer_x1.git # Replace with actual repo URL
cd titan_explorer_x1
mkdir build && cd build
cmake -DCMAKE_BUILD_TYPE=Release ..
make -j4 # Use number of cores available

# Install to system directories (requires sudo)
sudo make install
```

## Usage

### C Program

After installation, compile your C program linking against the library:

```c
// example.c
#include <stdio.h>
#include "habit.h" // Include desired headers

int main() {
    double score = habit_calculate_score(25.0, 70.0);
    printf("Habitat Score: %.2f\n", score);
    return 0;
}
```

```bash
gcc -o example example.c -ltitan_x1
./example
```

### Command Line Test

Run the provided test executable:

```bash
/opt/titan_x1/bin/titan_test
```

### Python Test (C API)

Execute the Python test script:

```bash
python3 /path/to/titan_explorer_x1/test/test_titan.py
```

## Directory Structure (After Installation)

*   `/opt/titan_x1/bin/`: Installed executable test program (`titan_test`).
*   `/opt/titan_x1/lib/`: Installed shared library (`libtitan_x1.so`).
*   `/opt/titan_x1/include/`: Installed C header files.
*   `/opt/titan_x1/LICENSE`: GPL v3 license file.
*   `/opt/titan_x1/README.md`: This file (if installed).

## Modules

*   `habit`: Models habitat preference based on temperature and humidity.
*   `behavior`: Implements a state machine for walking, feeding, and resting.
*   `feeding`: Simulates vegetation intake for a herbivore.
*   `motion_control`: Handles quadrupedal gait generation and inverse kinematics.
*   `dynamics`: Simplified rigid-body dynamics calculations.
*   `fluid_dynamics`: Basic air drag model.
*   `material_mechanics`: Stress/strain calculations for structural components.
*   `aerodynamics`: Advanced air force and moment calculations based on robot geometry and wind.
*   `apgtbl`: Specialized module for adverse pressure gradient turbulent boundary layer analysis, crucial for stability in high winds.

## ADLINK-Specific Optimization

*   Compiled with `-march=native` (or `-march=atom` for Atom-specific) for optimal performance on the target processor.
*   Memory usage is optimized for the 4GB RAM constraint.
*   Power management considerations are included in the design.

## Scientific References

1.  Carballido, J. L., et al. (2012). *Journal of Vertebrate Paleontology*, 32(1), 1-19.
2.  Gelfo, J. N., et al. (2009). *Cretaceous Research*, 30(3), 596-604.
3.  Kubisch, R., et al. (2018). *PLOS ONE*, 13(2), e0192425.
4.  Sillero, J. A., et al. (2013). *Physics of Fluids*, 25(12), 121301.
5.  Spalart, P. R., & Allmaras, S. R. (1994). *La Recherche Aerospatiale*, 1, 5-21.

## Development & Contributing

This project is designed to be extensible. Contributions are welcome, especially those that enhance the biological accuracy or engineering robustness of the models. Please ensure any contributions adhere to the GPL v3 license.

## License

This project is licensed under the GNU General Public License v3.0 (GPL v3). See the [LICENSE](./LICENSE) file for details.