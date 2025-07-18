# verilator --help
Displays the help message with a list of available options and usage. This is your go-to for checking how to use different flags and arguments.

# verilator --version
Prints the current version of Verilator installed on your system.

Example output:

yaml
Copy
Edit
Verilator 5.020 2024-03-15 rev v5.020
# verilator --binary -j 0 [options] [source_files.v]... [opt_c_files.cpp/c/cc/a/o/so]
This command compiles and builds the C++ simulation binary in one go, using multithreading with -j (job count).

--binary: Automatically runs make to generate the simulator executable after translating Verilog to C++.

-j 0: Uses all available CPU cores (you can replace 0 with a specific number for threads).

[source_files.v]: Your Verilog source files.

[*.cpp]: Optional C/C++ testbench or support files.

✅ Use case: Quick full build and simulate.

# verilator --cc [options] [source_files.v]... [opt_c_files.cpp/c/cc/a/o/so]
This generates C++ output only, placing it in obj_dir/, but does not compile it.

Use this if you want to modify or inspect the generated simulation files before compiling manually with make.

✅ Use case: When you want more control over how/when you compile the simulation.

# verilator --sc [options] [source_files.v]... [opt_c_files.cpp/c/cc/a/o/so]
Generates output for SystemC-based simulation instead of C++.

SystemC must be installed and linked properly.

Useful in mixed-language simulation or high-level modeling.

✅ Use case: Advanced simulation environments using SystemC.

# verilator --lint-only -Wall [source_files.v]...
Performs only syntax and semantic checking (linting), without generating simulation code.

-Wall: Enables all warnings.

Great for debugging or checking coding style.

✅ Use case: Static checking of Verilog for bugs, warnings, or style errors — like gcc -Wall for C/C++.

🧠 Summary Table
Command	Purpose
--help	Show help info
--version	Show Verilator version
--binary -j 0	Translate & build complete binary (multi-threaded)
--cc	Generate C++ files only
--sc	Generate SystemC code
--lint-only -Wall	Check Verilog code, show warnings/errors







##


Verilator has a rich set of commands and flags for simulation, linting, code generation, and performance tuning. Here's a categorized list of the **most important and useful Verilator commands and options**, beyond the ones you already mentioned.

---

## 🛠️ **Main Commands**

| Command         | Description                                  |
| --------------- | -------------------------------------------- |
| `--cc`          | Generate C++ code for Verilog simulation     |
| `--sc`          | Generate SystemC code                        |
| `--binary`      | Run make to build simulator binary           |
| `--lint-only`   | Lint Verilog (no C++ output)                 |
| `--help`        | Show help                                    |
| `--version`     | Print version                                |
| `--xml-only`    | Output XML file with parsed module structure |
| `--dump-tree`   | Dump internal Verilator AST                  |
| `--list-public` | List all public symbols                      |

---

## ⚙️ **Compilation & Build Options**

| Option                | Description                                                |
| --------------------- | ---------------------------------------------------------- |
| `-j <n>`              | Use `n` threads during `make` (use with `--binary`)        |
| `-Wall`               | Enable all warnings                                        |
| `--exe`               | Specify `.cpp` testbench or additional source files        |
| `--Mdir <dir>`        | Output generated files to `<dir>` (default: `obj_dir/`)    |
| `--top-module <name>` | Specify top module explicitly                              |
| `--prefix <name>`     | Prefix all generated classes/functions with name           |
| `--trace`             | Enable waveform trace dump support (VCD/FST)               |
| `--trace-fst`         | Use FST (faster than VCD) for waveform dumping             |
| `--build`             | Same as `--binary` but forces re-make                      |
| `--timing`            | Add timing (delay) statements for gates                    |
| `--output-split <n>`  | Split output into `n` source files to speed up compilation |
| `--public`            | Export all internal signals (can be viewed from C++)       |

---

## 📤 **Output Control**

| Option                    | Description                      |
| ------------------------- | -------------------------------- |
| `--exe`                   | Provide your `.cpp` testbench    |
| `--Mdir obj_dir/yourname` | Output directory                 |
| `--prefix MyDesign_`      | Prefix for generated C++ classes |
| `--trace` / `--trace-fst` | Generate waveform output         |
| `--vcdname my_dump.vcd`   | Change VCD output filename       |

---

## 📋 **Warnings and Linting**

| Option               | Description                                     |
| -------------------- | ----------------------------------------------- |
| `-Wall`              | Enable all warnings                             |
| `-Wno-<warn>`        | Suppress a specific warning (e.g. `-Wno-fatal`) |
| `--warn-all`         | Alias for `-Wall`                               |
| `--lint-only`        | Lint check only                                 |
| `--fatal-warnings`   | Treat warnings as fatal errors                  |
| `--Wno-TIMESCALEMOD` | Suppress timescale-related warnings             |

---

## 🧪 **Simulation Features**

| Option            | Description                                          |
| ----------------- | ---------------------------------------------------- |
| `--trace`         | Enable VCD waveform output                           |
| `--trace-structs` | Dump full structs in waveforms                       |
| `--coverage`      | Enable coverage tracking                             |
| `--prof-c`        | Insert performance profiling hooks (C-level)         |
| `--assert`        | Enable Verilog/SystemVerilog assertions              |
| `--threads`       | Enable multithreaded model evaluation (experimental) |

---

## 🧠 **Advanced/Utility Commands**

| Option                  | Description                                         |
| ----------------------- | --------------------------------------------------- |
| `--debug`               | Enable internal debug messages                      |
| `--dump-tree`           | Show parsed syntax tree                             |
| `--stats`               | Print performance and usage statistics              |
| `--xml-only`            | Output an XML representation of the model structure |
| `--output-split-ctrace` | Emit call traces per split file                     |
| `--no-timing`           | Ignore timing delays (`#10`) during simulation      |

---

## 📘 Example Usage

```bash
# Simple build and simulate with waveform trace
verilator --cc adder.v --exe testbench.cpp --trace --build
./obj_dir/Vadder
```

---

Would you like a reference cheat sheet PDF or want to create a Makefile setup to manage large designs?

