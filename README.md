# OpenFisk

OpenFisk is an open-source Python library that collects functions for tax-related calculations.

<img src="https://repository-images.githubusercontent.com/758609579/cf155288-4800-4c9c-90af-d8e6a8b3289d" alt="OpenFisk Logo" width="300px"/>

## Features

- **Comprehensive**: Supports income, sales, and asset tax calculations.
- **Global**: Provides modules per geography to account for regional tax models.
- **Current**: Regularly updated to reflect the latest tax laws.
- **Collaborative**: Improved through community contributions.
- **Efficient**: Optimized for performance, integrates with `numpy`.

## Installation

To install OpenFisk, run the following command:

```bash
pip install openfisk
```

## Quick Start

Here's an example of how to calculate income tax using OpenFisk, using the income tax model for the Netherlands:

```python
import numpy as np
from openfisk.nl.income import calculate_income_tax

# Example incomes to calculate tax for
taxable_incomes = np.array([10000, 30000, 50000])
# Define tax bands (lower bounds) for the progressive tax system
tax_bands = np.array([0, 20000, 40000, np.inf])
# Define the tax rates for the respective bands
tax_rates =  np.array([0.1, 0.2, 0.3])

# Calculate the income tax for each income in taxable_incomes
taxes_due = calculate_income_tax(taxable_incomes, tax_bands, tax_rates)

# Output the tax due for each income level
print(taxes_due)
```

## Contributing

We are looking for contributors! Please read the [Contribution Guide](./CONTRIBUTING.md) for details on our code of conduct, and the process for submitting pull requests.

## License

This project is licensed under the MIT License - see the [LICENSE](./LICENSE) file for details.
