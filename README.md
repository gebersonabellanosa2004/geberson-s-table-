import javax.swing.*;
import java.util.ArrayList;

public class JOptionPaneContactListApp {
    private static ArrayList<String> contactList = new ArrayList<>();

    public static void main(String[] args) {
        while (true) {
            String[] options = {"Add Contact", "View Contacts", "Delete Contact", "Exit"};
            int choice = JOptionPane.showOptionDialog(null, "Choose an option:", "Contact List Application",
                    JOptionPane.DEFAULT_OPTION, JOptionPane.INFORMATION_MESSAGE, null, options, options[0]);

            switch (choice) {
                case 0 -> addContact();
                case 1 -> viewContacts();
                case 2 -> deleteContact();
                case 3 -> System.exit(0);
                default -> JOptionPane.showMessageDialog(null, "Invalid choice. Try again.");
            }
        }
    }

    private static void addContact() {
        String name = JOptionPane.showInputDialog("Enter Contact Name:");
        if (name != null && !name.trim().isEmpty()) {
            contactList.add(name.trim());
            JOptionPane.showMessageDialog(null, "Contact added successfully.");
        } else {
            JOptionPane.showMessageDialog(null, "Invalid input. Try again.");
        }
    }

    private static void viewContacts() {
        if (contactList.isEmpty()) {
            JOptionPane.showMessageDialog(null, "No contacts available.");
        } else {
            StringBuilder contacts = new StringBuilder("Contact List:\n");
            for (int i = 0; i < contactList.size(); i++) {
                contacts.append(i + 1).append(") ").append(contactList.get(i)).append("\n");
            }
            JOptionPane.showMessageDialog(null, contacts.toString());
        }
    }

    private static void deleteContact() {
        if (contactList.isEmpty()) {
            JOptionPane.showMessageDialog(null, "No contacts to delete.");
            return;
        }

        String indexStr = JOptionPane.showInputDialog("Enter contact number to delete:");
        try {
            int index = Integer.parseInt(indexStr) - 1;
            if (index >= 0 && index < contactList.size()) {
                contactList.remove(index);
                JOptionPane.showMessageDialog(null, "Contact deleted successfully.");
            } else {
                JOptionPane.showMessageDialog(null, "Invalid contact number.");
            }
        } catch (NumberFormatException e) {
            JOptionPane.showMessageDialog(null, "Invalid input. Please enter a number.");
        }
    }
}
