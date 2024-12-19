# Course Selection Algorithm

A Python-based system for optimizing course selection based on academic requirements using Integer Linear Programming (ILP) and network flow algorithms.

## Overview

This project provides two approaches to solving the course selection problem:
1. An ILP-based solution using PuLP
2. A network flow-based solution using graph algorithms

Both approaches help students select courses that satisfy distribution requirements while minimizing the total number of courses needed.

## Requirements

- Python 3.8+
- Dependencies:
  - pulp
  - pandas
  - networkx
  - csv
  - logging

Install dependencies using:
```bash
pip install -r requirements.txt
```

## Input Format

The program accepts CSV files with the following format:
```
Course Number,Name,Codes
AAAS 102,Introduction to African American Studies,"CCI, CZ, SS"
```

Where:
- Course Number: Department code followed by course number
- Name: Course title
- Codes: Comma-separated list of requirement codes

### Valid Codes

Areas of Knowledge (AOK):
- ALP: Arts, Literature, and Performance
- CZ: Civilizations
- NS: Natural Sciences
- QS: Quantitative Studies
- SS: Social Sciences

Modes of Inquiry (MOI):
- CCI: Cross-Cultural Inquiry
- STS: Science, Technology, and Society
- EI: Ethical Inquiry
- R: Research
- W: Writing
- FL: Foreign Language

Special:
- SGLE: Small Group Learning Experience (automatically added for courses ending in 'S')

## Usage

### Basic Usage
```bash
python course_selector.py input_courses.csv
```

### Output
The program will:
1. Generate a list of selected courses that satisfy all requirements
2. Save the selection to `selected_courses.csv`
3. Provide detailed logging of the solution process

## Algorithm Details

### ILP Approach
The Integer Linear Programming solution:
1. Bins courses by unique code combinations
2. Creates decision variables for course selection and code allocation
3. Minimizes total courses while satisfying all requirements
4. Handles special cases like FL300+ courses with dual gadget system

### Network Flow Approach
The Max Flow solution:
1. Constructs a flow network with:
   - Source node connected to course bins
   - Intermediate nodes for requirement allocation
   - Sink node collecting requirement satisfaction
2. Finds all possible maximum flows
3. Selects flows that minimize course count

### Special Constraints

#### Foreign Language (FL) Requirements
- Can be satisfied by either:
  - 3 courses at 100/200 level
  - 1 course at 300+ level
- 300+ level courses use a dual-gadget system:
  - Gadget 1: 3 MOI codes (no FL)
  - Gadget 2: 2 MOI codes + FL requirement

#### Small Group Learning Experience (SGLE)
- Automatically detected for courses ending in 'S'
- Requires 2 courses minimum

## Error Handling

The program includes comprehensive error checking:
- Input validation
- Requirement coverage analysis
- Infeasibility detection
- Detailed logging for debugging

## License

MIT License - See LICENSE file for details

## Authors

- Zakk Heile - Duke University
