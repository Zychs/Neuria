import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Journal journal = new Journal();
        CommandParser parser = new CommandParser(journal);
        Scanner scanner = new Scanner(System.in);

        System.out.println("Journal App - Command Mode");
        System.out.println("Use: ADD \"title\" \"content\" | SHOW | EXIT");

        while (true) {
            System.out.print("> ");
            String command = scanner.nextLine();

            if (command.equalsIgnoreCase("EXIT")) {
                System.out.println("Exiting...");
                break;
            }

            parser.parseCommand(command);
        }
    }

    public static void exportEntries(List<String> entries, String filename) {
        try (BufferedWriter writer = new BufferedWriter(new FileWriter(filename))) {
            for (String entry : entries) {
                writer.write(entry);
                writer.newLine();
                writer.write("-----");
                writer.newLine();
            }
            System.out.println("Entries exported to " + filename);
        } catch (IOException e) {
            System.out.println("Error exporting entries: " + e.getMessage());
        }
    }
}
