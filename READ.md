// Package Declaration
package moviebooking;

// Import Statements
import java.util.HashMap;
import java.util.Map;
import java.util.Scanner;

// Class Declaration
public class MovieTicketBooking {

    // Constants for seating arrangement
    private static final int ROWS = 5;
    private static final int COLS = 10;

    // Data structure to store booking status
    private static boolean[][] seatAvailability = new boolean[ROWS][COLS];

    // Data structure to store username and password for front desk login
    private static Map<String, String> frontDeskCredentials = new HashMap<>();

    // Main method
    public static void main(String[] args) {
        initializeSeats();
        initializeFrontDeskCredentials();

        // Scanner for user input
        Scanner scanner = new Scanner(System.in);

        // Front Desk Login
        System.out.println("Welcome to the Movie Ticket Booking System!");
        System.out.print("Enter username for front desk login: ");
        String username = scanner.nextLine();
        System.out.print("Enter password for front desk login: ");
        String password = scanner.nextLine();

        // Front Desk Authentication
        if (authenticateFrontDesk(username, password)) {
            System.out.println("Login successful!\n");

            // Main Menu
            while (true) {
                System.out.println("1. View Seating Arrangement");
                System.out.println("2. Book Ticket");
                System.out.println("3. Update Password");
                System.out.println("4. Exit");
                System.out.print("Enter your choice: ");
                int choice = scanner.nextInt();
                scanner.nextLine(); // Consume the newline

                switch (choice) {
                    case 1:
                        viewSeatingArrangement();
                        break;
                    case 2:
                        bookTicket(scanner);
                        break;
                    case 3:
                        updatePassword(scanner);
                        break;
                    case 4:
                        System.out.println("Exiting program. Thank you!");
                        System.exit(0);
                        break;
                    default:
                        System.out.println("Invalid choice. Please try again.");
                        break;
                }
            }
        } else {
            System.out.println("Login failed. Exiting program.");
        }
    }

    // Method to initialize seat availability
    private static void initializeSeats() {
        for (int i = 0; i < ROWS; i++) {
            for (int j = 0; j < COLS; j++) {
                seatAvailability[i][j] = true;
            }
        }
    }

    // Method to initialize front desk login credentials
    private static void initializeFrontDeskCredentials() {
        frontDeskCredentials.put("admin", "admin@123");
    }

    // Method to authenticate front desk login
    private static boolean authenticateFrontDesk(String username, String password) {
        return frontDeskCredentials.containsKey(username) && frontDeskCredentials.get(username).equals(password);
    }

    // Method to view seating arrangement
    private static void viewSeatingArrangement() {
        System.out.println("Seating Arrangement:");
        for (int i = 0; i < ROWS; i++) {
            for (int j = 0; j < COLS; j++) {
                System.out.print(seatAvailability[i][j] ? "O " : "X ");
            }
            System.out.println();
        }
        System.out.println();
    }

    // Method to book a ticket
    private static void bookTicket(Scanner scanner) {
        System.out.print("Enter booking date: ");
        String bookingDate = scanner.nextLine();
        System.out.print("Enter show time: ");
        String showTime = scanner.nextLine();

        // Display available seats
        viewSeatingArrangement();

        System.out.print("Enter seat selection (e.g., B1 or B1-B5): ");
        String seatSelection = scanner.nextLine();

        // TODO: Implement logic to calculate amount and book the ticket

        System.out.println("Ticket booked successfully!");
    }

    // Method to update front desk password
    private static void updatePassword(Scanner scanner) {
        System.out.print("Enter new password: ");
        String newPassword = scanner.nextLine();
        frontDeskCredentials.put("admin", newPassword);
        System.out.println("Password updated successfully!");
    }
}
