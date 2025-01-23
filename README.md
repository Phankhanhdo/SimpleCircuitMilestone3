# Import necessary modules
from typing import Dict

# Define basic classes for Bus, Resistor, Load, and Vsource
class Bus:
    def __init__(self, name):
        # Each bus has a name and a voltage value (default to 0.0)
        self.name = name
        self.voltage = 0.0  # Default voltage value

class Resistor:
    def __init__(self, name, bus1, bus2, resistance):
        # A resistor connects two buses and has a resistance value
        self.name = name
        self.bus1 = bus1
        self.bus2 = bus2
        self.resistance = resistance

class Load:
    def __init__(self, name, bus, power, voltage):
        # A load is connected to a single bus and has a power and voltage rating
        self.name = name
        self.bus = bus
        self.power = power
        self.voltage = voltage

class Vsource:
    def __init__(self, name, bus, voltage):
        # A voltage source connects to a single bus and provides a specified voltage
        self.name = name
        self.bus = bus
        self.voltage = voltage

# Circuit class
class Circuit:
    def __init__(self, name: str):
        # Initialize the circuit with a name and empty dictionaries for components
        self.name = name
        self.buses: Dict[str, Bus] = {}
        self.resistors: Dict[str, Resistor] = {}
        self.loads: Dict[str, Load] = {}
        self.vsource: Vsource = None
        self.i: float = 0.0  # Circuit current

    def add_bus(self, name: str):
        # Add a bus to the circuit if it doesn't already exist
        if name not in self.buses:
            self.buses[name] = Bus(name)

    def add_resistor_element(self, name: str, bus1: str, bus2: str, resistance: float):
        # Ensure both buses exist before adding the resistor
        self.add_bus(bus1)
        self.add_bus(bus2)
        self.resistors[name] = Resistor(name, bus1, bus2, resistance)

    def add_load_element(self, name: str, bus: str, power: float, voltage: float):
        # Ensure the bus exists before adding the load
        self.add_bus(bus)
        self.loads[name] = Load(name, bus, power, voltage)

    def add_vsource_element(self, name: str, bus: str, voltage: float):
        # Ensure the bus exists before adding the voltage source
        self.add_bus(bus)
        self.vsource = Vsource(name, bus, voltage)

    def set_i(self, current: float):
        # Set the current flowing through the circuit
        self.i = current

    def print_nodal_voltage(self):
        # Print the voltage at each bus in the circuit
        print("Nodal Voltages:")
        for bus_name, bus in self.buses.items():
            print(f"Bus {bus_name}: {bus.voltage:.2f} V")

    def print_circuit_current(self):
        # Print the current flowing through the circuit
        print(f"Circuit Current: {self.i:.2f} A")

# Test the Circuit class with simple functionality
def main():
    circuit = Circuit("Basic Circuit")  # Create a circuit object

    # Add a voltage source
    circuit.add_vsource_element("V1", "A", 10.0)  # Voltage source at Bus A with 10V

    # Add a resistor
    circuit.add_resistor_element("R1", "A", "B", 100.0)  # Resistor between Bus A and Bus B with 100 ohms

    # Add a load
    circuit.add_load_element("L1", "B", 50.0, 5.0)  # Load at Bus B with 50W and 5V

    # Set circuit current
    circuit.set_i(0.1)  # Current of 0.1A in the circuit

    # Display current and nodal voltages
    circuit.buses["A"].voltage = 10.0  # Set voltage at Bus A
    circuit.buses["B"].voltage = 5.0   # Set voltage at Bus B
    circuit.print_circuit_current()  # Print circuit current
    circuit.print_nodal_voltage()    # Print nodal voltages

if __name__ == "__main__":
    main()
