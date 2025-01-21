# 
class Circuit:
    # Step 1: Initialize the circuit
    def __init__(self, name: str):
        """
        Initialize a Circuit object with a name and empty dictionaries for components.
        """
        self.name = name  # Name of the circuit
        self.buses = {}  # Dictionary to store bus objects (e.g., {"A": {"voltage": None}})
        self.resistors = {}  # Dictionary to store resistor objects
        self.loads = {}  # Dictionary to store load objects
        self.vsource = None  # Voltage source object
        self.i = 0.0  # Current flowing through the circuit (default is 0.0 A)

    # Step 2: Add a bus to the circuit
    def add_bus(self, bus: str):
        """
        Add a bus to the circuit.
        """
        self.buses[bus] = {"voltage": None}  # Initialize bus with unknown voltage
        print(f"Bus '{bus}' added to the circuit.")

    # Step 3: Add a resistor element
    def add_resistor_element(self, name: str, bus1: str, bus2: str, r: float):
        """
        Add a resistor to the circuit between two buses.
        """
        if bus1 not in self.buses or bus2 not in self.buses:
            raise ValueError("Both buses must be added to the circuit before adding a resistor.")
        self.resistors[name] = {"bus1": bus1, "bus2": bus2, "resistance": r}
        print(f"Resistor '{name}' with resistance {r}Ω added between '{bus1}' and '{bus2}'.")

    # Step 4: Add a load element
    def add_load_element(self, name: str, bus1: str, p: float, v: float):
        """
        Add a load to the circuit connected to a specific bus.
        """
        if bus1 not in self.buses:
            raise ValueError("The bus must be added to the circuit before adding a load.")
        self.loads[name] = {"bus": bus1, "power": p, "voltage": v}
        print(f"Load '{name}' added to bus '{bus1}' with power {p}W and voltage {v}V.")

    # Step 5: Add a voltage source
    def add_vsource_element(self, name: str, bus1: str, bus2: str, v: float):
        """
        Add a voltage source to the circuit between two buses.
        """
        if bus1 not in self.buses or bus2 not in self.buses:
            raise ValueError("Both buses must be added to the circuit before adding a voltage source.")
        self.vsource = {"name": name, "bus1": bus1, "bus2": bus2, "voltage": v}
        print(f"Voltage source '{name}' added with voltage {v}V between '{bus1}' and '{bus2}'.")

    # Step 6: Set the current flowing through the circuit
    def set_i(self, i: float):
        """
        Set the current flowing through the circuit.
        """
        self.i = i
        print(f"Current set to {i}A.")

    # Step 7: Print the nodal voltages
    def print_nodal_voltage(self):
        """
        Print the voltage at each bus in the circuit.
        """
        for bus, details in self.buses.items():
            voltage = details.get("voltage", "Unknown")  # Placeholder for voltage
            print(f"Bus '{bus}': Voltage = {voltage}")

    # Step 8: Print the circuit current
    def print_circuit_current(self):
        """
        Print the current flowing through the circuit.
        """
        print(f"Current through the circuit: {self.i}A")

# Import the Circuit class (assuming it is implemented in a separate file named circuit.py)
from Circuit import Circuit

# Step 1: Create an instance of Circuit
circuit = Circuit("Simple Circuit")
# Explanation: A new Circuit object is created with the name "Simple Circuit".
# This initializes the circuit's attributes (buses, resistors, loads, vsource, i) as empty.

# Step 2: Add buses to the circuit
circuit.add_bus("A")  # Add bus "A"
circuit.add_bus("B")  # Add bus "B"
# Explanation: The buses dictionary in the circuit is updated to include "A" and "B".
# Each bus is initialized with a placeholder for voltage, which is currently None.

# Step 3: Add a resistor to the circuit
circuit.add_resistor_element("R1", "A", "B", 100.0)
# Explanation: A resistor named "R1" with resistance 100Ω is added between buses "A" and "B".
# The resistor's details (connected buses and resistance) are stored in the resistors dictionary.

# Step 4: Add a load to the circuit
circuit.add_load_element("L1", "A", 50.0, 10.0)
# Explanation: A load named "L1" is added to bus "A" with a power consumption of 50W and an operating voltage of 10V.
# The load's details are stored in the loads dictionary.

# Step 5: Add a voltage source to the circuit
circuit.add_vsource_element("VS1", "A", "B", 12.0)
# Explanation: A voltage source named "VS1" with a voltage of 12V is added between buses "A" and "B".
# The voltage source details are stored in the vsource attribute.

# Step 6: Set the circuit current
circuit.set_i(0.12)
# Explanation: The current flowing through the circuit is set to 0.12A.
# This updates the `i` attribute of the circuit.

# Step 7: Print nodal voltages
circuit.print_nodal_voltage()
# Explanation: This method iterates through the buses dictionary and prints the voltage at each bus.
# Since voltage calculation is not yet implemented, the voltage is currently displayed as "Unknown".

# Step 8: Print circuit current
circuit.print_circuit_current()
# Explanation: This method prints the total current flowing through the circuit, which was set earlier to 0.12A.
