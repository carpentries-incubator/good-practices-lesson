---
title: Modular Code Development
teaching: 30
exercises: 30
---

:::::::::::::::::::::::::::::::::::::: questions 

- What are the benefits of writing modular code in terms of maintenance and scalability?
- How can nested code be targeted and improved through modularization?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Understand the key characteristics that make code modular and why it is advantageous.
- Learn strategies for identifying potential modules within complex code to improve readability and reusability.

::::::::::::::::::::::::::::::::::::::::::::::::

## What is modularity?

Modularity refers to the practice of building software from smaller, self-contained, and independent elements. Each element is designed to handle a specific set of tasks, contributing to the overall functionality of the system.

We will explain modular coding in the slides. You can view the slides [here](https://lyashevska.github.io/ds-cr-slides/).

::::::::::::::::::::::::::::::::::::: challenge 

## Modularity (20 min)

Carefully review the following code snippet:

```python
def convert_temperature(temperature, unit):
    if unit == "F":
        # Convert Fahrenheit to Celsius
        celsius = (temperature - 32) * (5 / 9)
        if celsius < -273.15:
            # Invalid temperature, below absolute zero
            return "Invalid temperature"
        else:
            # Convert Celsius to Kelvin
            kelvin = celsius + 273.15
            if kelvin < 0:
                # Invalid temperature, below absolute zero
                return "Invalid temperature"
            else:
                fahrenheit = (celsius * (9 / 5)) + 32
                if fahrenheit < -459.67:
                    # Invalid temperature, below absolute zero
                    return "Invalid temperature"
                else:
                    return celsius, kelvin
    elif unit == "C":
        # Convert Celsius to Fahrenheit
        fahrenheit = (temperature * (9 / 5)) + 32
        if fahrenheit < -459.67:
            # Invalid temperature, below absolute zero
            return "Invalid temperature"
        else:
            # Convert Celsius to Kelvin
            kelvin = temperature + 273.15
            if kelvin < 0:
                # Invalid temperature, below absolute zero
                return "Invalid temperature"
            else:
                return fahrenheit, kelvin
    elif unit == "K":
        # Convert Kelvin to Celsius
        celsius = temperature - 273.15
        if celsius < -273.15:
            # Invalid temperature, below absolute zero
            return "Invalid temperature"
        else:
            # Convert Celsius to Fahrenheit
            fahrenheit = (celsius * (9 / 5)) + 32
            if fahrenheit < -459.67:
                # Invalid temperature, below absolute zero
                return "Invalid temperature"
            else:
                return celsius, fahrenheit
    else:
        return "Invalid unit"
```

Refactor the code by extracting functions without altering its functionality.

- What functions did you create?
- What strategies did you use to identify them?

Share your answers in the collaborative document.

:::::::::::::::::::::::: solution 

## Solution 1 - Basic

```python
def celsius_to_fahrenheit(celsius):
    """
    Converts a temperature from Celsius to Fahrenheit.

    Args:
        celsius (float): The temperature in Celsius.

    Returns:
        float: The temperature in Fahrenheit.
    """
    return (celsius * (9 / 5)) + 32


def fahrenheit_to_celsius(fahrenheit):
    """
    Converts a temperature from Fahrenheit to Celsius.

    Args:
        fahrenheit (float): The temperature in Fahrenheit.

    Returns:
        float: The temperature in Celsius.
    """
    return (fahrenheit - 32) * (5 / 9)


def celsius_to_kelvin(celsius):
    """
    Converts a temperature from Celsius to Kelvin.

    Args:
        celsius (float): The temperature in Celsius.

    Returns:
        float: The temperature in Kelvin.
    """
    return celsius + 273.15


def kelvin_to_celsius(kelvin):
    """
    Converts a temperature from Kelvin to Celsius.

    Args:
        kelvin (float): The temperature in Kelvin.

    Returns:
        float: The temperature in Celsius.
    """
    return kelvin - 273.15


def check_temperature_validity(temperature, unit):
    """
    Checks if a temperature is valid for a given unit.

    Args:
        temperature (float): The temperature to check.
        unit (str): The unit of the temperature. Must be "C", "F", or "K".

    Returns:
        bool: True if the temperature is valid, False otherwise.
    """
    abs_zero = {"C": -273.15, "F": -459.67, "K": 0}
    if temperature < abs_zero[unit]:
        return False
    return True


def check_unit_validity(unit):
    """
    Checks if a unit is valid.

    Args:
        unit (str): The unit to check. Must be "C", "F", or "K".

    Returns:
        bool: True if the unit is valid, False otherwise.
    """
    if not unit in ["C", "F", "K"]:
        return False
    return True


def convert_temperature(temperature, unit):
    """
    Converts a temperature from one unit to another.

    Args:
        temperature (float): The temperature to convert.
        unit (str): The unit of the temperature. Must be "C", "F", or "K".

    Returns:
        tuple: A tuple containing the converted temperature in Celsius and Kelvin units.

    Raises:
        ValueError: If the unit is not "C", "F", or "K".
        ValueError: If the temperature is below absolute zero for the given unit.

    Examples:
        >>> convert_temperature(32, "F")
        (0.0, 273.15)
        >>> convert_temperature(0, "C")
        (32.0, 273.15)
        >>> convert_temperature(273.15, "K")
        (0.0, -459.67)
    """
    if not check_unit_validity(unit):
        raise ValueError("Invalid unit")
    if not check_temperature_validity(temperature, unit):
        raise ValueError("Invalid temperature")
    if unit == "F":
        celsius = fahrenheit_to_celsius(temperature)
        kelvin = celsius_to_kelvin(celsius)
        return celsius, kelvin
    if unit == "C":
        fahrenheit = celsius_to_fahrenheit(temperature)
        kelvin = celsius_to_kelvin(temperature)
        return fahrenheit, kelvin
    if unit == "K":
        celsius = kelvin_to_celsius(temperature)
        fahrenheit = celsius_to_fahrenheit(celsius)
        return celsius, fahrenheit

if __name__ == "__main__":
    print(convert_temperature(0, "C"))
    print(convert_temperature(0, "F"))
    print(convert_temperature(0, "K"))
    print(convert_temperature(-500, "K"))
    print(convert_temperature(-500, "C"))
    print(convert_temperature(-500, "F"))
    print(convert_temperature(-500, "B"))
```

:::::::::::::::::::::::::::::::::
:::::::::::::::::::::::: solution

## Solution 2 - Advanced

```python
class TemperatureConverter:
    """
    A class for converting temperatures between Celsius, Fahrenheit, and Kelvin.
    """

    def __init__(self):
        """
        Initializes the TemperatureConverter object with a dictionary of absolute zero temperatures for each unit.
        """
        self.abs_zero = {"C": -273.15, "F": -459.67, "K": 0}

    def celsius_to_fahrenheit(self, celsius):
        """
        Converts a temperature from Celsius to Fahrenheit.

        Args:
            celsius (float): The temperature in Celsius.

        Returns:
            float: The temperature in Fahrenheit.
        """
        return (celsius * (9 / 5)) + 32

    def fahrenheit_to_celsius(self, fahrenheit):
        """
        Converts a temperature from Fahrenheit to Celsius.

        Args:
            fahrenheit (float): The temperature in Fahrenheit.

        Returns:
            float: The temperature in Celsius.
        """
        return (fahrenheit - 32) * (5 / 9)

    def celsius_to_kelvin(self, celsius):
        """
        Converts a temperature from Celsius to Kelvin.

        Args:
            celsius (float): The temperature in Celsius.

        Returns:
            float: The temperature in Kelvin.
        """
        return celsius + 273.15

    def kelvin_to_celsius(self, kelvin):
        """
        Converts a temperature from Kelvin to Celsius.

        Args:
            kelvin (float): The temperature in Kelvin.

        Returns:
            float: The temperature in Celsius.
        """
        return kelvin - 273.15

    def check_temperature_validity(self, temperature, unit):
        """
        Checks if a given temperature is valid for a given unit.

        Args:
            temperature (float): The temperature to check.
            unit (str): The unit to check the temperature against.

        Returns:
            bool: True if the temperature is valid for the unit, False otherwise.
        """
        if temperature < self.abs_zero[unit]:
            return False
        return True

    def check_unit_validity(self, unit):
        """
        Checks if a given unit is valid.

        Args:
            unit (str): The unit to check.

        Returns:
            bool: True if the unit is valid, False otherwise.
        """
        if unit not in ["C", "F", "K"]:
            return False
        return True

    def convert_temperature(self, temperature, unit):
        """
        Converts a temperature from one unit to another.

        Args:
            temperature (float): The temperature to convert.
            unit (str): The unit of the temperature.

        Returns:
            tuple: A tuple containing the converted temperature in the other two units.
        """
        if not self.check_unit_validity(unit):
            raise ValueError("Invalid unit")
        if not self.check_temperature_validity(temperature, unit):
            raise ValueError("Invalid temperature")
        if unit == "F":
            celsius = self.fahrenheit_to_celsius(temperature)
            kelvin = self.celsius_to_kelvin(celsius)
            return celsius, kelvin
        if unit == "C":
            fahrenheit = self.celsius_to_fahrenheit(temperature)
            kelvin = self.celsius_to_kelvin(temperature)
            return fahrenheit, kelvin
        if unit == "K":
            celsius = self.kelvin_to_celsius(temperature)
            fahrenheit = self.celsius_to_fahrenheit(celsius)
            return celsius, fahrenheit

if __name__ == "__main__":
    converter = TemperatureConverter()
    print(converter.convert_temperature(0, "C"))
    print(converter.convert_temperature(0, "F"))
    print(converter.convert_temperature(0, "K"))
    print(converter.convert_temperature(-500, "K"))
    print(convert_temperature(-500, "C"))
    print(convert_temperature(-500, "F"))
    print(convert_temperature(0, "X"))
```

:::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: keypoints 

- Software is built from smaller, self-contained elements, each handling specific tasks.
- Modular code enhances robustness, readability, and ease of maintenance.
- Modules can be reused across projects, promoting efficiency.
- Good modules perform limited, defined tasks and have descriptive names.
- Focus on readability and use tests to guide modularization.

::::::::::::::::::::::::::::::::::::::::::::::::
