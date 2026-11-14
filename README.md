# C++ Daily Exercises

## Project Overview

**C++ Daily Exercises** is a structured, version-controlled repository dedicated to daily algorithm and data structure practice, competitive programming (OI/ACM) problem-setting, and local automated testing. 

The primary objective of this repository is to maintain a rigorous, professional standard for algorithm training. Instead of relying solely on online judges (OJ), this repository establishes a localized, self-contained environment. Each problem is fully documented, provided with test cases, and configured for local execution, simulating the strict time and memory constraints of a real competition.

## Repository Structure

The repository follows a highly standardized directory layout. Each day's practice is encapsulated within a dedicated folder (e.g., `Day 1`, `Day 2`) to ensure isolation and modularity.

~~~text
Cpp-Daily-Excercises/
├── README.md               # Project documentation (this file)
├── .gitignore              # Git ignore rules (ignoring binaries, test outputs, etc.)
└── Day 1/                  # Daily practice folder
    ├── problem.md          # The problem statement (in pure English with LaTeX)
    ├── config.json         # Local judge configuration (time limit, memory limit, checker)
    ├── solution.cpp        # (Optional) The accepted reference solution
    └── testcases/          # Test cases for local evaluation
        ├── 1/
        │   ├── 1.in        # Test case 1: Input data
        │   └── 1.ans       # Test case 1: Expected output
        ├── 2/
        │   ├── 2.in
        │   └── 2.ans
        └── ...
~~~

## Problem Format Specifications

To maintain consistency, all problems within this repository must be documented in `problem.md` using strict Markdown and LaTeX formatting. Every `problem.md` file must contain the following sections:

1. **Problem Statement**: A clear background description, precise mathematical definitions, and a formalized description of the objective.
2. **Input Format**: A rigorous specification of the data types, the order of inputs, and any implicit assumptions (e.g., graph connectivity or edge sorting).
3. **Output Format**: The exact structure of the expected output, including modulus requirements (e.g., `mod 998244353`) if applicable.
4. **Samples**: At least two clear input/output pairs to help understand the problem mechanics. These must correspond exactly to the test cases in the `testcases` directory.
5. **Constraints and Hints**: 
    - A detailed table of variable ranges (e.g., `1 <= N <= 1000`).
    - Time and memory limits.
    - Algorithmic hints or expected time complexity (e.g., state compression DP, $O(N \log N)$ sorting).
6. **Difficulty**: A numerical rating (e.g., `1.00`) placed at the very bottom of the file to objectively indicate the problem's complexity relative to a baseline.

## Local Testing Workflow

To ensure code correctness before committing, it is highly recommended to use a local competitive programming helper tool, such as **Competitive Programming Helper (CPH)** or **Cpeditor** in Visual Studio Code.

### Automated Testing (Recommended)
1. Open the `problem.md` or `solution.cpp` file in VS Code.
2. The CPH extension will automatically detect the corresponding `.in` and `.ans` files in the `testcases/` directory.
3. Run your code, and the extension will automatically compare your output against the `.ans` files and report the execution time and memory usage.

### Manual Compilation & Testing
You can also test your code manually via the terminal:

~~~bash
# Compile the solution with optimization flags
g++ -O2 -std=c++17 solution.cpp -o solution

# Execute the compiled program with a specific test case
./solution < testcases/1/1.in > my_output.txt

# Compare the generated output with the expected answer
diff my_output.txt testcases/1/1.ans
~~~
*Note: If the `diff` command returns nothing, it means your output matches the expected answer exactly.*

## Contribution and Version Control Guidelines

This repository is maintained using Git and hosted on GitHub. To contribute or add a new daily exercise, follow these steps:

1. **Create a New Day Folder**: Create a folder named `Day X` (e.g., `Day 2`).
2. **Draft the Problem**: Write the `problem.md` following the format specifications above.
3. **Prepare Test Cases**: Create the `testcases` directory. Generate a minimum of 3 test points, ranging from small edge cases to maximum constraint scenarios. Ensure every `.in` file has a corresponding `.ans` file.
4. **Write the Configuration**: Add a `config.json` specifying the time limit (in milliseconds) and memory limit (in megabytes).
5. **Commit and Push**:
~~~bash
git add .
git commit -m "feat: add Day X problem, reference solution, and test cases"
git push origin main
~~~

## Future Expansions

The current structure is designed to be highly extensible. Future updates to this repository may include:
- **Automated CI/CD Pipeline**: Utilizing GitHub Actions to automatically compile the `solution.cpp` and run it against all test cases upon every push.
- **Custom Checkers**: Implementing specialized `checker.cpp` files for problems that require Special Judges (SPJ).
- **Algorithmic Templates**: Adding a dedicated `/Templates` folder containing standard implementations of Data Structures and Algorithms (e.g., Segment Trees, DSU, Network Flow).

## License

This repository is intended for personal educational and competitive programming training purposes. All problem statements and test cases are generated and curated locally.

## Quick Links
- [Problem Archive](#) (Coming soon)
- [Algorithm Topics Index](Topics.md)
---
*Maintained by Makeline-pon. Focus on logic, optimize the process.*