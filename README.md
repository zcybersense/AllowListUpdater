# Allow List  - File Update Algorithm

## Project Description

This project automates the process of updating an allow list for a healthcare company's restricted subnetwork. The algorithm identifies and removes unauthorized IP addresses listed in a remove list from the allow list file. This ensures efficient and secure access control.

## Scenario

You are a security professional working at a healthcare company. Your task is to regularly update a file that identifies employees who can access restricted content. Employees are restricted access based on their IP address. The allow list contains IP addresses permitted to access the subnetwork, and the remove list specifies which IP addresses to remove. 

The Python algorithm reads the allow list, removes IPs from the remove list, and updates the allow list with the revised set of IPs.

---

## Full Python Code

Below is the complete Python script used in this project:

```python
def update_file(import_file, remove_list):
    """
    Updates the allow list file by removing IP addresses from the remove list.

    Parameters:
    import_file (str): The file path of the allow list.
    remove_list (list): List of IP addresses to remove.

    Returns:
    None
    """
    # Open the file to read its contents
    with open(import_file, "r") as file:
        ip_addresses = file.read()

    # Use .splitlines() to convert the content into a list of lines
    ip_addresses = ip_addresses.splitlines()

    # Filter the IP addresses, excluding those in the remove list
    ip_addresses = [ip for ip in ip_addresses if ip not in remove_list]

    # Convert the updated list back to a string with line breaks
    updated_ip_addresses = "\n".join(ip_addresses)

    # Write the updated IP addresses back to the file
    with open(import_file, "w") as file:
        file.write(updated_ip_addresses)

# Call the function to update the file
import_file = "allow_list.txt"
remove_list = ["192.168.97.225", "192.168.158.170", "192.168.201.40", "192.168.58.57"]
update_file(import_file, remove_list)

# Verify by reading and displaying the updated file contents
with open(import_file, "r") as file:
    updated_content = file.read()

print("Updated File Content:")
print(updated_content)
